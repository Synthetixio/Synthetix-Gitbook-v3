# Perps V3

{% hint style="info" %}
Perps V3 is live on Base, but (predominantly internal) updates are planned
{% endhint %}

### Perps V3.0 features and updates

* Cross margin: account margin can be used across multiple positions on markets
* Only async (delayed offchain) orders: atomic orders can be gamed very easily by front runners; async orders seems to be the way forward in general.
* No order cancellation: you couldn't cancel within settlement window anyway so it was pointless to add cancel after the order has expired. Removed one extra action for keepers to perform and LPs to pay for.
* Accounts with Role Based Access Control for modifying collateral, opening/closing positions - enabling full extensibility and composability.
* Improved liquidations and no more endorsed liquidators
* Constraints to note
  * Single position per market&#x20;
  * Single pending order

{% embed url="https://github.com/Synthetixio/synthetix-v3/tree/main/markets/perps-market" %}

### Expected features for v3.1

* Changes to funding rates

### Expected features for v3.2

* Multi collateral: accepts any synths configured in the system as margin for an account

## SDK

To better understand how to trade perps, see

[perps-python-sdk.md](perps-python-sdk.md "mention")

## Workflow

### Factory Owner

{% hint style="info" %}
This is permissioned
{% endhint %}

* Each proxy is considered to be one “supermarket”, and is initialized with the factory owner as the owner of this supermarket. The supermarket consists of a set of markets that it controls for which cross margin is applied. Each account that’s created is scoped to the supermarket and cannot be used on other supermarkets.
* Supermarkets can only be initialized once which registers them with the Core system using the following call (returns the registered market id with core system):

```solidity
function initializeFactory() external returns (uint128);
```

* Owner can set other global parameters that apply to all markets:

[synthetix-v3/GlobalPerpsMarketConfiguration.sol at main · Synthetixio/synthetix-v3](https://github.com/Synthetixio/synthetix-v3/blob/main/markets/perps-market/contracts/storage/GlobalPerpsMarketConfiguration.sol)

#### Create perps market:

```solidity
    function createMarket(
        uint128 requestedMarketId,
        string memory marketName,
        string memory marketSymbol
    ) external returns (uint128);
```

* Two markets have been created on OP Goerli so far:
  * `100`: ETH market
  * `200`: BTC market

#### Set configuration parameters

* If you need the configuration of any of the above created markets, here are the functions you can call:

```solidity
function getSettlementStrategy(
        uint128 marketId,
        uint256 strategyId
    ) external view returns (SettlementStrategy.Data memory settlementStrategy);

function getLiquidationParameters(
        uint128 marketId
    )
        external
        view
        returns (
            uint256 initialMarginRatioD18,
            uint256 minimumInitialMarginRatioD18,
            uint256 maintenanceMarginScalarD18,
            uint256 liquidationRewardRatioD18,
            uint256 maxLiquidationLimitAccumulationMultiplier,
            uint256 maxSecondsInLiquidationWindow,
            uint256 minimumPositionMargin
        );

function getFundingParameters(
        uint128 marketId
    ) external view returns (uint256 skewScale, uint256 maxFundingVelocity);

function getMaxMarketSize(uint128 marketId) external view returns (uint256 maxMarketSize);

function getOrderFees(
        uint128 marketId
    ) external view returns (uint256 makerFeeRatio, uint256 takerFeeRatio);

function getLockedOiRatio(uint128 marketId) external view returns (uint256 lockedOiRatioD18);
```

[synthetix-v3/PerpsMarketConfiguration.sol at main · Synthetixio/synthetix-v3](https://github.com/Synthetixio/synthetix-v3/blob/main/markets/perps-market/contracts/storage/PerpsMarketConfiguration.sol#L21)

#### Add settlement strategy for async orders:

```solidity
    function addSettlementStrategy(
        uint128 marketId,
        SettlementStrategy.Data memory strategy
    ) external returns (uint256 strategyId);
```

* A strategy has been added on OP goerli. You can always query `getSettlementStrategy` to get the details.

## Trader

{% hint style="info" %}
This is how integrators or front ends
{% endhint %}

#### Create account:

`function createAccount(uint128 requestedAccountId) external;`

* Re-using the `AccountModule` from v3 core system which comes packaged with RBAC.
* The account owner can delegate **`PERPS_MODIFY_COLLATERAL`** role to another address using:

```solidity
    function grantPermission(
        uint128 accountId,
        bytes32 permission,
        address user
    ) external
```

#### Modify collateral:

```solidity
function modifyCollateral(uint128 accountId, uint128 synthMarketId, int amountDelta) external;
```

* Use `0` as `synthMarketId` for snxUSD.
* Use any other synth that has a `maxCollateralAmount` set by owner of factory to add to account’s margin.
*   By providing a negative `amountDelta`, you are able to withdraw collateral of your choosing.

    Note: there are checks in place to ensure you cannot remove more than the required maintenance margin.

#### Commit Order:

```solidity
    function commitOrder(
        AsyncOrder.OrderCommitmentRequest memory commitment
    )

    struct OrderCommitmentRequest {
        /**
         * @dev Order market id.
         */
        uint128 marketId;
        /**
         * @dev Order account id.
         */
        uint128 accountId;
        /**
         * @dev Order size delta (of asset units expressed in decimal 18 digits). It can be positive or negative.
         */
        int128 sizeDelta;
        /**
         * @dev Settlement strategy used for the order.
         */
        uint128 settlementStrategyId;
        /**
         * @dev Acceptable price set at submission. Compared against the fill price.
         */
        uint256 acceptablePrice;
        /**
         * @dev An optional code provided by frontends to assist with tracking the source of volume and fees.
         */
        bytes32 trackingCode;
        /**
         * @dev Referrer address to send the referrer fees to, if configured.
         */
        address referrer;
    }
```

* `sizeDelta` is the change in size of the position. Can determine long/short based on this value.
* A settlement strategy is required in order to commit orders. Here’s an example of one that uses a pyth offchain settlement strategy:

```solidity
strategy: {
  strategyType: 0,
  settlementDelay: bn(5),
  settlementWindowDuration: bn(120),
  priceVerificationContract: 0xff1a0f4744e8582DF1aE09D5611b887B6a12925C,
  feedId: 0xca80ba6dc32e08d06f1aa886011eed1d77c77be9eb761cc10d72b7d0a2fd57a6, // op goerli  
  url: "<https://api.synthetix.io/pyth-testnet/api/get_vaa_ccip?data={data}>", // testnet
  settlementReward: bn(5),
  priceWindowDuration: bn(240),
  disabled: false,
}
```

## Liquidation Keepers

* Call either:
  * `function liquidate(uint128 accountId) external`
    * If the account is already flagged for liquidation, the call will proceed with liquidating as much of the account’s position as possible.
    * If the account is not, it will check if the account is eligible and proceed to liquidate.
    * Otherwise, the call reverts.
  * `function liquidateFlagged() external`
    * Iterates through all accounts flagged for liquidation and attempts to liquidate.
    * Gas could be high but so are the rewards 💰

## Settlement Keepers

* `function settle(uint128 marketId, uint128 accountId) external`
  * if the order is valid and within settlement window, this function will settle the order and update its accounting of the new position.

### Other Notes:

#### Liquidation Margins

An account is subject to margin requirements as determined by the following values configurable for each market:

```solidity
uint256 initialMarginFraction;
uint256 minimumInitialMarginFraction;
uint256 maintenaceMarginScalar;
uint256 liquidationMarginRatio;
```

When opening a position on a given market, the initial margin requirement is a fraction of the notional value. The fraction is determined by calculating the size’s impact on the skew (position size / skewScale), multiplied by the `initialMarginFraction`plus the `minimumInitialMarginScalar`.

Once a positive is live, the liquidation threshold is determined by the `maintenceMargin`which is the initialMargin requirement multiplied by the configured `maintenceMarginScalar`.

To determine if an account is liquidatable, the account’s `availableMargin` must be greater than all calculated maintenance margins combined for each market the account has a position open. The maintenance margin also includes the liquidation settlement reward configured per market as a % of the notional size being liquidated.

`availableMargin` is determined by subtracting any unrealized pnl to the available collateral margin.

Available functions that will come in handy:

```solidity
// returns account's available margin taking into account positions unrealized pnl
function getAvailableMargin(uint128 accountId) external view returns (int256 availableMargin);

// returns how much a trader can withdraw from their account based on margin requirements and avialable collateral
function getWithdrawableMargin(
        uint128 accountId
    ) external view returns (int256 withdrawableMargin);

// returns the current margin requirements for the given account id
function getRequiredMargins(
        uint128 accountId
    )
        external
        view
        returns (
            uint256 requiredInitialMargin,
            uint256 requiredMaintenanceMargin,
            uint256 totalAccumulatedLiquidationRewards,
            uint256 maxLiquidationReward
        );
```

#### Estimate Order Validity

There are some functions you can call initially to determine if an order will go through:

```solidity
// for a given sizeDelta, will return how much total account margin is required
function requiredMarginForOrder(
        uint128 marketId,
        uint128 accountId,
        int128 sizeDelta
    ) external view returns (uint256 requiredMargin);

// useful to show the order fees that would be incurred for a given sizeDelta
function computeOrderFees(
        uint128 marketId,
        int128 sizeDelta
    ) external view returns (uint256 orderFees, uint256 fillPrice);
```

#### Max Liquidatable Amount

Each market has parameters that dictate how much can be liquidated at any given point.

```solidity
uint256 maxSecondsInLiquidationWindow;
uint256 maxLiquidationLimitAccumulationMultiplier;
```

The equation for max liquidation per second is as follows:

```solidity
maxLiquidationAmountPerSecond = (makerFee + takerFee) * skewScale * maxLiquidationLimitAccumulationMultiplier
```

_Note_: _the multiplier is an additional way to limit max liquidation amount per market._

Based on the configured window, `maxSecondsInLiquidationWindow`, and `maxLiquidationAmountPerSecond`, the max liquidatable amount in any given window is:

`maxSecondsInLiquidationWindow * maxLiquidationAmountPerSecond`

Example:

```solidity
ETH Market:
maxLiquidationAmountPerSecond = 100 ETH
maxSecondsInLiquidationWindow = 5 seconds
```

In this scenario, a max of `500 ETH`can be liquidated in a 5 second window.
