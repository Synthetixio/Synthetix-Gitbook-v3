---
description: This applies to v3, not v2
---

# Developer FAQ

### General v3

Where can I get Goerli snxETH? `0xC2ecD777d06FFDF8B3179286BEabF52B67E9d991`

* You can wrap goerli eth into snxETH on [the market prototype](https://synthetix-markets-prototype.vercel.app/), probably the easiest way if you have some eth on testnet.

Where can I get Goerli snxUSD?

*

### Perps v3

Is there a way to fetch the list of markets like `allProxiedMarketSummaries` on Perps v2?

* Being worked on

Is there a method similar to `postTradeDetails` to build a preview of the trade, including fees, fill price, liquidation etc?

* These are all separate functions right now (estimate fees, get a fill price, etc) but this could be another view to request.

How can I tell if an account has an open order?

* Orders can be fetched using the `getOrder(marketId, accountId)` function. The `sizeDelta` value is set to 0 when orders are cancelled. The other values are stored until another order is committed to save gas.\


\


\
