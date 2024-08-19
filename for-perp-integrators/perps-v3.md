# Perps V3

Perps v3 is designed for onchain perpetual futures trading of a wide range of assets, on optimistic EVM rollups.

{% embed url="https://github.com/Synthetixio/synthetix-v3/tree/main/markets/perps-market" %}

* **Traders** can take the following actions:
  * Create an account
  * Manage margin balances
  * Commit orders
  * Delegate access
* **Keepers** can take the following actions:
  * Settle orders committed by traders
  * Liquidate accounts

## Features

### Perps V3.1&#x20;

* Cross margin: account margin can be used across multiple positions on markets
* Only async (delayed offchain) orders: async orders seems to be the way forward in general
* No order cancellation: Removed one extra action for keepers to perform and LPs to pay for
* Role Based Access Control for modifying collateral, opening/closing positions - for full extensibility and composability
* Utilization interest rate
* Single position per market , and single pending order

### Perps v3.2

* Multi collateral: accepts any synths configured in the system as margin for an account

### What are the major differences between Perps V2 and V3?

* **Perps Accounts -** Before interacting with the markets traders first create an account, represented as an NFT. An account on Optimism can own many perps accounts, which allows for isolating collateral and opening many positions on a market. Each interaction will take this `accountId` as a parameter.
* **Cross margin -** All positions in a perps account are cross-margined against the provided collateral. If the account's collateral drops below their maintenance margin, all positions will be closed and all collateral in the account will be liquidated.
* **Alternate collateral** **-** Perps accounts can now contain more collateral types than sUSD. These collaterals will increase your available margin based on the latest oracle price. If the total USD value of these collaterals drops below your maintenance margin, all collateral types will be liquidated.&#x20;

## Start here

### Trading SDK

To better understand how to trade perps, see [perps-python-sdk.md](perps-python-sdk.md "mention")

### End to End Tests

{% hint style="success" %}
To best understand the process of building a perp trading integration, see the below tests:

* [Perp trading with USDC margin on Base Sepolia](https://github.com/Synthetixio/synthetix-deployments/blob/main/e2e/tests/omnibus-base-sepolia-andromeda.toml/Perps\_Trading.e2e.js)
* [Perp trading with multicollateral margin on Arbitrum Sepolia](https://github.com/Synthetixio/synthetix-deployments/blob/main/e2e/tests/omnibus-arbitrum-sepolia.toml/Perps\_trading.e2e.js)
{% endhint %}

## Requirements

{% hint style="info" %}
Perps v3 configured to use oracle contracts which comply with [ERC-7412](https://eips.ethereum.org/EIPS/eip-7412). Use [the client library](https://erc7412.synthetix.io/) when building off-chain integrations like UIs and bots.
{% endhint %}

## Get started

* There is a single proxy for all interactions with perps. You can find the proxy address and ABI [here](../for-developers/addresses-+-abis.md)
* Call the `getMarkets` function to retrieve the list of `marketIds` the list of available markets.
* Additional market info call be retrieved by calling `getMarketSummary` with those market ids and reviewing the `MarketCreated` events.
* Fetch other market settings using the `marketId` using functions like `getFundingParameters` and `getLiquidationParameters`

## Account Creation

* Call `PerpsMarketProxy.createAccount()` to create an account with a random `accountId`
* You can also specify an `accountId`, which will revert if the account already exists

```solidity
function createAccount(uint128 requestedAccountId) external;
```

* Re-using the `AccountModule` from v3 core system which comes packaged with RBAC.
* The account owner can delegate **`PERPS_MODIFY_COLLATERAL`** role to another address using:

```solidity
    function grantPermission(
        uint128 accountId,
        bytes32 permission,
        address user
    ) external
```

## Deposit Margin

{% hint style="warning" %}
For Base see [base-andromeda.md](base-andromeda.md "mention")to handle USDC
{% endhint %}

1. Approve spending margin
2. Deposit margin with ModifyCollateral

{% code overflow="wrap" %}
```solidity
function modifyCollateral(uint128 accountId, uint128 synthMarketId, int amountDelta) external;
```
{% endcode %}

### **Managing Margin Balances**

{% hint style="warning" %}
For Base see [base-andromeda.md](base-andromeda.md "mention")to handle USDC
{% endhint %}

Each perps account holds assets to use as margin for their positions. Fetch margin balances using these functions on the `PerpsMarketProxy` contract:

* `totalCollateralValue(accountId)`: Get the USD value of all collateral in the account
* `getAvailableMargin(accountId)`: Get the USD value of the margin available to use as collateral for future positions
* `getWithdrawableMargin(accountId)`: Get the USD value of the margin you can withdraw immediately
* `getRequiredMargins(accountId)`: Get USD values of the margin requirements for the specified account, given their open positions

## Commit Order

{% hint style="success" %}
See a sample order commitment transaction [here](https://sepolia.basescan.org/tx/0x18e8a3314775b4a0f95da7c36b8a4e3d74f5284c2ba2597e2127d4fe99dfad49).
{% endhint %}

Given an account with some available margin, a trader can commit orders to a perps market. That order will be settled by a keeper according to the specified `settlementStrategyId`. The Andromeda deployment uses Pyth oracles to settle your order at a future price after a short delay.

* Orders are handled asynchronously. Traders submit a `commitOrder` transaction, which creates an order to be settled by a keeper.
* The `commitOrder` function takes a struct containing all of the order information as an argument. You can see an example order commitment [here](https://goerli-optimism.etherscan.io/tx/0xed1091e6572f199943c7adc167058679f53cd1bde8749cb521e45676c8715364) including the arguments to create this struct.
* Use `0` as `synthMarketId` for snxUSD.
* Use any other synth that has a `maxCollateralAmount` set by owner of factory to add to account’s margin.
*   By providing a negative `amountDelta`, you are able to withdraw collateral of your choosing.

    Note: there are checks in place to ensure you cannot remove more than the required maintenance margin.

Call PerpsMarketProxy.commitOrder(commitment) to commit an order. The input commitment is a tuple configuring the order. Here are some recommendations for those inputs:

1. `marketId`: Call `getMarkets()` and `metadata` to get more info about the markets
2. `accountId`: The `accountId` that has available margin
3. `sizeDelta`: A wei value of the size in units of the asset being traded
4. `settlementStrategyId`: Recommended `0` for Pyth settlement. Call `getSettlementStrategy` for more details
5. `acceptablePrice`: Minimum fill price for longs, maximum fill price for shorts
6. `trackingCode`: A bytes32 encoded value for tracking integrator volume
7. `referrer`: An address for configured integrators to receive a share of fees.

{% code overflow="wrap" %}
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
{% endcode %}

* `sizeDelta` is the change in size of the position. Can determine long/short based on this value.
* A settlement strategy is required in order to commit orders. Here’s an example of one that uses a pyth offchain settlement strategy:

{% code overflow="wrap" %}
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
{% endcode %}

## Order Settlement

{% hint style="success" %}
See a sample order settlement transaction [here](https://sepolia.basescan.org/tx/0xca9b5eaa1853bbb449a30ad93d54364fb6395dc65d92c1686381e29562ca22a0).
{% endhint %}

Orders will typically be settled by a keeper (which you can run - see [perps-v3-keeper.md](perps-v3-keeper.md "mention")) who fetches the price data from Pyth and fills orders for a fee. You can check `getOrder(accountId)` for a given account to view the status of the order. The `sizeDelta` will be set to 0 when the order is filled, otherwise it will expire and can be replaced with another order.

Events emitted to track orders:

* Orders emit `OrderCommitted` and `OrderSettled` events to track these interactions.
* For a sample `OrderCommitted` event, review [this transaction](https://goerli-optimism.etherscan.io/tx/0xed1091e6572f199943c7adc167058679f53cd1bde8749cb521e45676c8715364#eventlog).
* For a sample `OrderSettled` event, review [this transaction](https://goerli-optimism.etherscan.io/tx/0x83cab229af206b4f76921b3abe99e590a77a4300d31736ce8d4a165221461071#eventlog).
* See [this repo](https://github.com/Synthetixio/synthetix-v3/tree/main/markets/perps-market/subgraph) for a subgraph implementation

## Order status

Is there a method to build a trade preview including fees, fill price, and liquidation prices?

* There is no single method for quotes, however there are individual methods for these values.
* `computeOrderFees` will return the fees and estimated fill price for a given order size.
* Liquidation prices are not available directly. Since positions are cross-margined individual position liquidation prices will change depending on the market. Instead, you can fetch the margin requirements using `getRequiredMargins`
* Positions are liquidated when an account's `availableMargin` is below the `requiredMaintenanceMargin`

How can I tell if an account has an open order?

* Fetch orders using the `getOrder(marketId, accountId)` function.
* If the `sizeDelta` value is 0 there is no open order. When an order is filled, this value is set to 0.
* Other values may be returned when there is not an open order. These values are not reset to reduce gas used during order settlement.

How can I tell if an account has an open position?

* Fetch position using the `getOpenPosition(marketId, accountId)` function.
* The return will include the position size as well as any funding and pnl accrued since the position was opened.

## Settlement Keepers

* Keepers settle orders after the `settlementTime` has been reached. You can get this time from the `OrderCommitted` event or by calling `getOrder` for an account.
* The `settle` function reverts with information for retrieving the offchain price data (`url` and `data`)
* The `settlePythOrder` function take this price data as well as an argument with encoded `accountId` and `marketId` parameters. Review [this transaction](https://goerli-optimism.etherscan.io/tx/0x83cab229af206b4f76921b3abe99e590a77a4300d31736ce8d4a165221461071) to see sample inputs.

```solidity
function settle(uint128 marketId, uint128 accountId) external
```

If the order is valid and within settlement window, this function will settle the order and update its accounting of the new position.

More info at [perps-v3-keeper.md](perps-v3-keeper.md "mention")

## Liquidation Keepers

Call either:

```solidity
function liquidate(uint128 accountId) external
```

* If the account is already flagged for liquidation, the call will proceed with liquidating as much of the account’s position as possible.
* If the account is not, it will check if the account is eligible and proceed to liquidate.
* Otherwise, the call reverts.

```solidity
function liquidateFlagged() external
```

* Iterates through all accounts flagged for liquidation and attempts to liquidate.
* Gas could be high but so are the rewards 💰

## Other Notes

### Liquidation Margins

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

{% code overflow="wrap" %}
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
{% endcode %}

### Estimate Order Validity

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

### Max Liquidatable Amount

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



{% hint style="warning" %}
Below functions are permissioned to Synthetix governance
{% endhint %}

## Factory Owner

Each proxy is considered to be one “supermarket”, and is initialized with the factory owner as the owner of this supermarket. The supermarket consists of a set of markets that it controls for which cross margin is applied. Each account that’s created is scoped to the supermarket and cannot be used on other supermarkets.

Supermarkets can only be initialized once which registers them with the Core system using the following call (returns the registered market id with core system):

```solidity
function initializeFactory() external returns (uint128);
```

Owner can set other global parameters that apply to all markets:

[synthetix-v3/GlobalPerpsMarketConfiguration.sol at main · Synthetixio/synthetix-v3](https://github.com/Synthetixio/synthetix-v3/blob/main/markets/perps-market/contracts/storage/GlobalPerpsMarketConfiguration.sol)

### Create perps market:

```solidity
    function createMarket(
        uint128 requestedMarketId,
        string memory marketName,
        string memory marketSymbol
    ) external returns (uint128);
```

Two markets have been created on OP Goerli so far:

* `100`: ETH market
* `200`: BTC market

### Set configuration parameters

If you need the configuration of any of the above created markets, here are the functions you can call:

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

### Add settlement strategy for async orders

```solidity
    function addSettlementStrategy(
        uint128 marketId,
        SettlementStrategy.Data memory strategy
    ) external returns (uint256 strategyId);
```

You can always query `getSettlementStrategy` to get the details.
