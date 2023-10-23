---
description: What will you build on v3?
---

# Build on v3

{% hint style="info" %}
v3 is in alpha, but now is the time to start building
{% endhint %}

<figure><img src="../.gitbook/assets/Twitter_post_-_4 (1).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://mirror.xyz/cavalier.eth/w0pXCYaek7Bz_EfMmfoo6tpKhOUK-xOTcY223xl1JZE" %}
An outline of v3, its components and possibilities
{% endembed %}

{% embed url="https://mirror.xyz/cavalier.eth/zC1SNu43jUCV7UjudJtDVrv6H74snpDa1hyChPFyYTg" %}
The case for building on Synthetix v3
{% endembed %}

{% embed url="https://t.me/+Jwf641J8a6M1ZTI1" %}
Telegram group for integrator discussions
{% endembed %}

## Why build on v3

Synthetix v3 solves the cold-start and scaling liquidity problems for derivate protocols, with more than $500m of liquidity waiting for new markets. Synthetix is an endlessly composable and configurable liquidity layer; backing derivative Markets, so they can scale faster, and LPs can accrue more fees.

* Product:&#x20;
  * Cold-start liquidity: Synthetix Liquidity Providers can allocate their collateral to your Pool in a few clicks
  * Scaling liquidity: Incentivize your own Pool, or attract existing Pools to back your Market
* Technical:&#x20;
  * Speed: It's trivial to create and configure Pools/Markets/Rewards
  * Security: v3 has been audited by both Open Zeppelin and Iosiro

## Playbook for building on v3

1. **Create your Market:** Create a new derivatives Market, or adapt your existing product, following [market-development-guide.md](../for-developers/market-development-guide.md "mention"), and conforming to the `IMarket` interface in [integrating-synthetix.md](integrating-synthetix.md "mention")
2. **Register your Market:** Propose an [SCCP](https://docs.synthetix.io/dao/how-to-write-sip-sccps) to Synthetix governance for your Market to be registered _(this governance requirement goes away once permissionless Markets are enabled by Spartan Council)_
3. **Get collateral:** Request some of the existing $500m+ LP collateral in the Synthetix system for your Market
   1. request collateral from an existing Pool OR
   2. propose a new Pool of your own via [SCCP](https://docs.synthetix.io/dao/how-to-write-sip-sccps), and attract Synthetix LPs[creating-and-configuring-pools.md](../for-liquidity-pool-managers/creating-and-configuring-pools.md "mention") _(this governance requirement goes away once permissionless Pools are enabled by Spartan Council)_

Your high performing Market will be attractive to other Pools and Synthetix LPs.

<figure><img src="../.gitbook/assets/v3 flywheel  (1).jpg" alt=""><figcaption><p>The lifecycle of adding a Market and attracting collateral</p></figcaption></figure>

<figure><img src="../.gitbook/assets/v3 playbook (2).jpg" alt=""><figcaption><p>The evolution of requesting existing collateral, and wrapping the Synthetix v3 primitives into your own interface</p></figcaption></figure>

## Use cases

* Want to create a novel derivatives product? You could create a v3 Market, then request one of the existing Pools to delegate your Market some collateral, or create a Pool.
* Want to control your own liquidity? You could propose to create a new Pool, and offer additional token incentives to Liquidity Providers with the Rewards Manager.&#x20;

## Next steps

1. Join the integrator telegram group to ask questions&#x20;
2. Follow [Synthetix Integrators](https://twitter.com/i/lists/1677086706246520832) list on X

{% embed url="https://t.me/+Jwf641J8a6M1ZTI1" %}

## Notes

* See [development-progress.md](../development-progress.md "mention") for more details on enabled collateral and other milestones.
