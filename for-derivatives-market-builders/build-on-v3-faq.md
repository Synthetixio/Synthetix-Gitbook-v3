---
description: Considerations for creating new products on v3
---

# Build on v3 FAQ

> What all is needed to do this?

[#playbook-for-building-on-v3](build-on-v3.md#playbook-for-building-on-v3 "mention")

> Is a new Pool required?&#x20;

Not necessarily, because existing Pools could choose to delegate some of their collateral to your Market, but you need to convince the Pool owners to do so.

> Is a new Market required?&#x20;

Usually yes. Your Market is what draws on liquidity delegated to it, by existing Pools (or your own Pool if you create one). A profitable Market deposits earnings (and potentially rewards) to the Pools providing liquidity.

> Can a Market swap snxUSD for another assets? (eg WETH)

A Market must conform to the [IMarket](registering-a-market.md) interface, which means it can only deposit/withdraw snxUSD to/from Pools, but is free to interact with the wider defi ecosystem in any reasonable way.

> Can a Market accept another asset directly? (eg WETH)&#x20;

See above

> Can the Market owner impose a fee that incentivizes them?

Market owners are free to decide how their Markets function. Ultimately Markets are judged and compared on their performance (withdrawals and deposits to Pools) over time.

