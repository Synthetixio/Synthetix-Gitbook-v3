---
description: A guide to help developers start interacting with Synthetix V3
---

# Developer FAQ

### General

Where can I get assets on OP Goerli?&#x20;

* `ETH`: Optimism Goerli ETH is available from various faucets. We recommend the official [Optimism faucet](https://app.optimism.io/faucet) but there are also [other faucets](https://community.optimism.io/docs/useful-tools/faucets/) available.
* `snxETH`: You can wrap OP Goerli ETH into snxETH on "Spot" tab of [the market prototype](https://synthetix-markets-prototype.vercel.app/). This is the easiest way to get assets for testing if you have testnet ETH.
* `snxUSD`: snxETH acquired through wrapping can be sold for snxUSD on the spot market prototype.

## Smart Contracts

* All v3 contracts are under proxy, to find which you have to check the cannon file.&#x20;
* Cannon is the tooling used to define v3, see [https://usecannon.com/packages/synthetix](https://usecannon.com/packages/synthetix)
* Owner is the address indicated by the `owner` function, depends on network.&#x20;
* Function to use for enabling feature flag to all is `setFeatureFlagAllowAll` I believe
* Decide any error from v3 with `cannon decode synthetix-omnibus --chain-id 1 {paste 0x error code here}`

### **Spot Markets**

How can I swap assets?

1. Navigate to the [spot market prototype](https://synthetix-markets-prototype.vercel.app/)
2. Prepare your order and click "Submit order". If a token approval is required, you will be prompted with two transactions.
3. Wait 10 seconds and refresh the page
4. Click "View Pending Orders", open the "Committed" tab, and check the "My Orders" button
5. When the "Settle" button is enabled, click it and submit the transaction.

### Perps Markets V3

How do I get started with the V3 perps markets?

* There is a single proxy for all interactions with perps. You can find the proxy address and ABI [here](addresses-+-abis.md).

Is there a way to fetch the list of available markets?

* Call the `getMarkets` function to retrieve the list of `marketIds`
* Additional market info call be retrieved by calling `getMarketSummary` with those market ids and reviewing the `MarketCreated` events.
* Fetch other market settings using the `marketId` using functions like `getFundingParameters` and `getLiquidationParameters`

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

How can I submit a perps order?

* Orders are handled asynchronously. Traders submit a `commitOrder` transaction, which creates an order to be settled by a keeper.
* The `commitOrder` function takes a struct containing all of the order information as an argument. You can see an example order commitment [here](https://goerli-optimism.etherscan.io/tx/0xed1091e6572f199943c7adc167058679f53cd1bde8749cb521e45676c8715364) including the arguments to create this struct.

Are there events emitted to track orders?

* Orders emit `OrderCommitted` and `OrderSettled` events to track these interactions.
* For a sample `OrderCommitted` event, review [this transaction](https://goerli-optimism.etherscan.io/tx/0xed1091e6572f199943c7adc167058679f53cd1bde8749cb521e45676c8715364#eventlog).
* For a sample `OrderSettled` event, review [this transaction](https://goerli-optimism.etherscan.io/tx/0x83cab229af206b4f76921b3abe99e590a77a4300d31736ce8d4a165221461071#eventlog).
* See [this repo](https://github.com/Synthetixio/synthetix-v3/tree/main/markets/perps-market/subgraph) for a subgraph implementation

How are perps orders settled?

* Keepers settle orders after the `settlementTime` has been reached. You can get this time from the `OrderCommitted` event or by calling `getOrder` for an account.
* The `settle` function reverts with information for retrieving the offchain price data (`url` and `data`)
* The `settlePythOrder` function take this price data as well as an argument with encoded `accountId` and `marketId` parameters. Review [this transaction](https://goerli-optimism.etherscan.io/tx/0x83cab229af206b4f76921b3abe99e590a77a4300d31736ce8d4a165221461071) to see sample inputs.

What are the major differences between Perps V2 and V3?

* **Perps Accounts -** Before interacting with the markets traders first create an account, represented as an NFT. An account on Optimism can own many perps accounts, which allows for isolating collateral and opening many positions on a market. Each interaction will take this `accountId` as a parameter.
* **Cross margin -** All positions in a perps account are cross-margined against the provided collateral. If the account's collateral drops below their maintenance margin, all positions will be closed and all collateral in the account will be liquidated.
* **Alternate collateral** **-** Perps accounts can now contain more collateral types than sUSD. These collaterals will increase your available margin based on the latest oracle price. If the total USD value of these collaterals drops below your maintenance margin, all collateral types will be liquidated. \


\


\
