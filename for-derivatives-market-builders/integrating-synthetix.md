# Operating a Market

## Managing Credit & Debt[​](https://snx-v3-docs.vercel.app/pools-markets/integrating-markets#managing-credit--debt) <a href="#managing-credit--debt" id="managing-credit--debt"></a>

When a market receives snxUSD (e.g. by selling a synthetic asset), it should deposit them into the market manager using the `depositMarketUsd` function. This effectively credits all of the pools (and relevant liquidity positions) backing this market, pro-rata.

When a market needs to pay out snxUSD (e.g. when a synthetic asset is sold back to the market), it may withdraw snxUSD from the market manager using the `withdrawMarketUsd` function. This increases debt among all of the pools (and relevant liquidity positions) backing this market, pro-rata. A market can withdraw no more than the amount returned by the `getWithdrawableMarketUsd` function.

The amount of snxUSD withdrawn by the market minus the amount deposited can be retrieved using the `getMarketNetIssuance` function. (Note that this value can be negative.) This, plus the `getMarketReportedBalance`, results in the `getMarketTotalDebt`. The amount of collateral backing the market can be retrieved with the `getMarketCollateral` function.

## Minimum Delegation Duration

Market implementations may call the `setMarketMinDelegateTime` with a duration (of seconds) which must elapse between calls where a pool or liquidity provider alters their delegation to this market. Similar to the `minimumCredit` value, if this is set very aggressively, liquidity providers will be disinclined to delegate collateral to the market.

This functionality helps mitigate the front-running of liquidity providers. For example, an active liquidity provider or pool manager may be able to anticipate that a market will call `depositMarketUsd` with a large amount, delegate collateral to the market just before this transaction, and then remove their collateral just after the transaction completes. The intention here would be to extract risk-free yield at the expense of passive liquidity providers; this is limited if the minimum delegation duration forces them to continue to be exposed to the market's performance for a longer time period.

## Market-Provided Collateral

Governance may permit specific markets to deposit collateral. Markets are able to use the value of the collateral directly towards their credit capacity. An example use case for this is the wrapper functionality in the [Spot Market implementation](../for-developers/spot-market.md) where, for example, one ETH could be deposited to issue one snxETH.

Market-provided collateral opens up new market design mechanisms to support scalability of the stablecoin, as this collateral can be minted against at it's full value. Allowing any market to take advantage of the functionality would introduce significant risk to the protocol, as there isn't a liquidations mechanism for this collateral. Accordingly, governance is able to permit specific markets to utilize this feature, up to a cap, after assessing that the market implementation introduces sufficient risk mitigation in its design.

### &#x20;<a href="#managing-credit--debt" id="managing-credit--debt"></a>
