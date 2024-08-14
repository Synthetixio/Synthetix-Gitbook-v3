# Liquidity Pools

Pools are referenced by an ID number. Pools may fit the following classifications:

* **Preferred Pool** (also referred to as the Spartan Council Pool) - This is the main pool managed [by governance](../../for-governance-participants/synthetix-governance.md). This is the pool suggested by default for liquidity providers to participate in. This pool's ID can be retrieved by calling the `getPreferredPool` function.
* **Approved Pools** - The Spartan Council also specifies approved pools with IDs that can be retrieved with the `getApprovedPools` function. This is expected to be a series of pools owned by the Spartan Council with exposure to different combinations of markets.
* **Zero Pool** (also referred to as delegating to “no pool”) - A pool exists at ID `0` which backs no markets and never can (because it has no owner). Depositing collateral with this pool is similar to using a decentralized borrowing protocol, where the only functionality is minting and burning snxUSD.
* **Permissionlessly Created Pools** - During Synthetix V3 Alpha/Beta phases, a feature flag has been set which disables the permissionless creation of pools. When governance chooses to alter this feature flag, anyone will be able to [create and configure their own pool](../../for-liquidity-pool-managers/creating-and-configuring-pools.md).

{% hint style="info" %}
Any liquidity position delegated to a pool could be indirectly liquidated by the owner of the pool. There is always risk, but be especially cautious when providing liquidity to pools that aren’t approved by governance.
{% endhint %}
