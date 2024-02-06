---
description: Evolving reference for Core V3 + Perps V3 on Base
---

# Base Andromeda

{% hint style="info" %}
### Evolving timeline

* Andromeda on [Base Goerli](https://usecannon.com/packages/synthetix-omnibus/latest/84531-andromeda)&#x20;
* Andromeda on [Base Sepolia](https://usecannon.com/packages/synthetix-omnibus/latest/84532-andromeda)
* Andromeda on [Base Mainnet](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda)
* TBC: Public launch and announcements
{% endhint %}

## Introduction

Andromeda is the combination of

* Core V3&#x20;
* Perps V3
* USDC as collateral

The Spot Market is included, but only to be used as a mechanism to exchange the assets brought by traders and LPs (USDC) for the internal accounting tokens (sUSDC and sUSD).

## Configuration

* Unique to Andromeda Base is the use of a USDC wrapper, enabling USDC to appear to be used as collateral for LPs, and as margin as perp traders.
* Underneath, USDC is wrapped and or traded into sUSDC for LP collateral (and collecting fees), and sUSD as perp margin
* The full configuration of Base Goerli can be seen [on Cannon](https://usecannon.com/packages/synthetix-omnibus/3.3.3-dev.e141cd8c/84531-andromeda)
* See [#andromeda-on-base-goerli](../for-developers/addresses-+-abis.md#andromeda-on-base-goerli "mention") for Addresses and ABIs
* Configuration explained:&#x20;
  * [this is the part](https://github.com/Synthetixio/synthetix-deployments/pull/66/files#diff-dc0e4e9b2b24d1fcf9c5a8ffd5b5548955777eff55c71dd0ab208dc04e84a89b) that deploys sUSDC (a USDC synth) and creates the spot market
  * &#x20;USDC <--> sUSDC can be wrapped/unwrapped on the spot market
  * sUSD <--> sUSDC can be bought/sold on the spot market
  * No fee on these, all atomic so can be composed with multicalls
* _Coming: Andromeda Base Sandbox - in the meantime see the more general_ [sandbox-with-perps.md](sandbox-with-perps.md "mention") _can be used once USDC is wrapped and swapped to sUSD_

{% embed url="https://usecannon.com/packages/synthetix-omnibus/latest/84531-andromeda" %}
Base Goerli Andromeda
{% endembed %}

{% hint style="info" %}
The Andromeda Release is configured to use oracle contracts which comply with [ERC-7412](https://eips.ethereum.org/EIPS/eip-7412). Use [the client library](https://erc7412.synthetix.io/) when building off-chain integrations like UIs and bots.
{% endhint %}

## For LPs

LPs can arrive with USDC to provide liquidity (LP). The contracts or integrators need to:

1. Wrap USDC to sUSDC on the Spot Market
   1. Function: `SpotMarketProxy.wrap(marketId, wrapAmount, amountReceived)`
   2. Example: `wrap(1, 1000000000000000000, 1000000000000000000)`
2. Deposit sUSDC to Pool
3. Delegate sUSDC to Market

When withdrawing, initial collateral plus any fees can be withdrawn, then unwrapped from sUSDC to USDC.

## For Perp Traders/Integrators

**Traders** can take the following actions:

* Create an account
* Manage margin balances
* Commit orders

**Keepers** can take the following actions:

* Settle orders committed by traders
* Liquidate accounts

Additionally, integrators can create a seamless trading experience using USDC by utilizing the wrapper and spot market. Since `USDC-sUSDC` and `sUSDC-sUSD` exchanges are both 1:1 swaps, integrators can easily prepare a multicall to "zap" between USDC in their wallet and their account margin.

### **Create an Account**

To deposit margin , you must specify an accountId.

* Call `PerpsMarketProxy.createAccount()` to create an account with a random `accountId`
* You can also specify an `accountId`, which will revert if the account already exists

See [creating accounts](perps-v3.md#create-account) for more technical docs.

### **Managing Margin Balances**

Each perps account holds assets to use as margin for their positions. Currently Andromeda supports USDC collateral through the use of a token wrapper. Fetch margin balances using these functions on the `PerpsMarketProxy` contract:

* `totalCollateralValue(accountId)`: Get the USD value of all collateral in the account
* `getAvailableMargin(accountId)`: Get the USD value of the margin available to use as collateral for future positions
* `getWithdrawableMargin(accountId)`: Get the USD value of the margin you can withdraw immediately
* `getRequiredMargins(accountId)`: Get USD values of the margin requirements for the specified account, given their open positions

### Preparing Margin Transactions

Integrators can directly deposit and withdraw USDC by preparing a multicall to execute in a single transaction. These transactions interact with the `SpotMarketProxy` to wrap and swap USDC for sUSD. Use `marketId = 1` for `sUSDC`. Matching values like `wrapAmount` and `amountReceived` in the transactions will guarantee this 1:1 swap.

All transactions should be prepared as a multicall and sent to the `TrustedMulticallForwarder` contracts using `aggregate3Value`.

#### **Prerequisites**

An account must meet the following requirements to execute USDC transfers between their wallet and a perps account.

**Deposit:**

* Holds an account NFT for perps. See [creating an account](perps-v3.md#create-account).
* Approve `SpotMarketProxy` to transfer USDC
* Approve `SpotMarketProxy` to transfer sUSDC
* Approve `PerpsMarketProxy` to transfer sUSD

**Withdraw:**

* Account NFT has some withdrawable margin
* Approve `SpotMarketProxy` to transfer sUSD
* Approve `SpotMarketProxy` to transfer sUSDC

**Deposit perp margin**

1. `USDC -> sUSDC` - Wrap USDC on the spot market
   1. Function: `SpotMarketProxy.wrap(marketId, wrapAmount, amountReceived)`
   2. Example: `wrap(1, 1000000000000000000, 1000000000000000000)`
2. `sUSDC -> sUSD` - Sell sUSDC for sUSD on the spot market
   1. Function: `SpotMarketProxy.sell(marketId, synthAmount, minUsdAmount, referrer)`
   2. Example: `sell(1, 1000000000000000000, 1000000000000000000, 0x0000000000000000000000000000000000000000)`
3. Deposit sUSD
   1. Function: `PerpsMarketProxy.modifyCollateral(accountId, synthMarketId, amountDelta)`
   2. Example: `modifyCollateral(12345, 0, 1000000000000000000)`

**Withdraw perp margin**

1. Withdraw sUSD
   1. Function: `PerpsMarketProxy.modifyCollateral(accountId, synthMarketId, amountDelta)`
   2. Example: `modifyCollateral(12345, 0, -1000000000000000000)`
2. `sUSD -> sUSDC` - Buy sUSDC on the spot market
   1. Function: `SpotMarketProxy.buy(marketId, usdAmount, minAmountReceived, referrer)`
   2. Example: `buy(1, 1000000000000000000, 1000000000000000000, 0x0000000000000000000000000000000000000000)`
3. `sUSDC -> USDC` - Unwrap sUSDC on the spot market
   1. Function: `SpotMarketProxy.unwrap(marketId, unwrapAmount, minAmountReceived)`
   2. Example: `unwrap(1, 1000000000000000000, 1000000000000000000)`

**Sample Margin Transactions**

* [Deposit](https://goerli.basescan.org/tx/0x95461a5b05c40c91c952bc06b0d292ec16ffd0c750a7b708a8564183b9b08cf4)
* [Withdraw](https://goerli.basescan.org/tx/0x4b6d29faaa75223fe1d690993c5e93ef316fc823385cbc52f505927f65702319)

### Trading

Given an account with some available margin, a trader can commit orders to a perps market. That order will be settled by a keeper according to the specified `settlementStrategyId`. The Andromeda deployment uses Pyth oracles to settle your order at a future price after a short delay.

See more technical details about preparing orders on [this page](perps-v3.md#commit-order).

**Committing Orders**

Call PerpsMarketProxy.commitOrder(commitment) to commit an order. The input commitment is a tuple configuring the order. Here are some recommendations for those inputs:

1. `marketId`: Call `getMarkets()` and `metadata` to get more info about the markets
2. `accountId`: The `accountId` that has available margin
3. `sizeDelta`: A wei value of the size in units of the asset being traded
4. `settlementStrategyId`: Recommended `0` for Pyth settlement. Call `getSettlementStrategy` for more details
5. `acceptablePrice`: Minimum fill price for longs, maximum fill price for shorts
6. `trackingCode`: A bytes32 encoded value for tracking integrator volume
7. `referrer`: An address for configured integrators to receive a share of fees.

See a sample order commitment transaction [here](https://sepolia.basescan.org/tx/0x18e8a3314775b4a0f95da7c36b8a4e3d74f5284c2ba2597e2127d4fe99dfad49).

**Order Settlement**

Orders will typically be settled by a keeper who fetches the price data from Pyth and fills orders for a fee. You can check `getOrder(accountId)` for a given account to view the status of the order. The `sizeDelta` will be set to 0 when the order is filled, otherwise it will expire and can be replaced with another order.

See a sample order settlement transaction [here](https://sepolia.basescan.org/tx/0xca9b5eaa1853bbb449a30ad93d54364fb6395dc65d92c1686381e29562ca22a0).

### Useful links

* Perp order settlement and liquidation keepers are running on Goerli, and you can run your own [perps-v3-keeper.md](perps-v3-keeper.md "mention")
* [Base Goerli keeper for order settlement and liquidation](https://goerli.basescan.org/address/0x4A58e0d29558111bfDc07Dc12Ca0fF7fcD0d0d75)&#x20;
* [Base Goerli Perp trades](https://goerli.basescan.org/token/0xa89163A087fe38022690C313b5D4BBF12574637f)&#x20;
