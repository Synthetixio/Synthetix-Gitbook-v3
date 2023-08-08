# Credit and Debt Distribution

The Synthetix protocol allows for a many-to-many relationship between liquidity pools and derivatives markets. Liquidity providers extend credit to and have their debt adjusted by markets when joining liquidity pools. Liquidity providers may modify their position in pools and pools may alter their configuration in relation to markets over time, subject to a handful of restrictions. Markets can have an unlimited number of pools backing them with no effect on their gas usage.

One way to think about Synthetix is that it generates a stablecoin as a collateralized debt position while also allowing markets to mint and burn stablecoins on behalf of positions which opt into the liquidity pools backing them. In addition to this, markets have the ability to report debt (the value of derivatives that they've issued) which the liquidity positions backing it assume. Subject to governance-configured limits, markets may be allowed to provide their own collateral to increase their credit capacity.

## Balancing Pools

As outlined in the [Configuring Pools​](creating-and-configuring-pools.md#configuring-pools) section, collateral from individual positions are collected into vaults within pools and then assigned to an array of markets based on weights set by a pool owner.

The value of the collateral (and the resulting available credit capacity) assigned to each market is a cached value in the protocol, ensuring that traders are able to interact with markets without encountering scaling issues pertaining to gas usage. This automatically called when liquidity providers delegate collateral to a pool, when a pool's configuration is updated, or liquidations are processed. This can also be executed by anyone by using the external function `rebalancePool`.

Note that if this value becomes stale and price action (for example) is not taken into account, it does not risk insolvency for the stablecoin. Markets' issuance is limited by the minimum liquidity ratio and if too much debt is accrued relative to collateral value, liquidators will still have an opportunity to liquidate [positions](../for-liquidity-providers/liquidity-positions/position-liquidations.md) and [vaults](collateral-vaults/vault-liquidations.md).

## The Debt Distribution Chain

Debt adjustments from markets are distributed through pools to vaults into individual liquidity positions. This is accounted for with the [debt shares](creating-and-configuring-pools.md#debt-shares) system, which relies primarily on [`Distribution.sol`](https://github.com/Synthetixio/synthetix-v3/blob/main/protocol/synthetix/contracts/storage/Distribution.sol).

Each debt share has a corresponding dollar value of debt that it is responsible for. The maximum debt share value (set when pools are configured to back markets) indicates the value above which the pool is effectively removed from backing the market. This is functionally similar to a "stop loss" mechanism, where if a market started reporting a very large amount of debt, liquidity providers would have their exposure limited. If a pool is removed from backing a market due to this mechanism, they will also no longer receive negative debt adjustments (e.g. from earned fees).

Debt in the Synthetix system is accounted for as a signed integer, meaning that it can be a negative value. Negative debt can be thought of essentially as credit which a liquidity provider could use to issue additional snxUSD. In an extreme example, a market that only ever deposited snxUSD and never reported debt would have a growing negative debt balance. Liquidity providers backing this market would be earning credit which they could use to collectively mint this balance of snxUSD. Importantly, markets are unable to report negative debt; markets can only reduce debt by depositing snxUSD. If markets report a very high value of debt, liquidity positions will be protected by the maximum debt share value mechanism, as outlined above.

