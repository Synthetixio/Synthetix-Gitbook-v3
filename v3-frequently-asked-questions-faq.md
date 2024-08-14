# V3 FAQ

Welcome to the V3 Frequently Asked Questions (FAQ) section. This guide is designed to address common questions regarding the V3 release of Synthetix. As the platform evolves, expect this section to see regular updates and revisions to ensure clarity and up-to-date information for our community.

<details>

<summary>Who is Synthetix V3 built for?</summary>

**Answer:** Synthetix V3 is built with both LPs and derivatives projects in mind.

Derivatives projects will be able to tap into Synthetix liquidity both through existing markets like Perps and Spot Synths, or by building their own derivatives markets. We’ve explored some of the opportunities for new markets, like options, insurance funds, sports AMMs and more, all of which will be able to leverage existing Synthetix liquidity to bootstrap trading activity.

LPs will have greater flexibility to allocate collateral to markets based on their risk profile. As mentioned in another answer, the new Pool and Vault system has two key benefits for LPs:

1. Better risk management: Users can select one of many liquidity pools, which are connected to one or more markets, allowing more fine-tuned control of LP risk.
2. Wider collateral range: The V3 system is oracle agnostic, allowing any governance-approved asset to serve as collateral for borrowing sUSD and delegate to derivative markets.

</details>

<details>

<summary>How is staking evolving with V3?</summary>

**Answer:** The power is with stakers in V3, thanks to multi-collateral staking and permissionless pools. V3 creates a generalized system agnostic to collateral type. Liquidity providers can deposit any governance-approved collateral into Pools, which is then used to provide liquidity to derivative markets. In the future, the creation of markets and vaults will be permissionless, giving liquidity providers fine-tune control of their market exposure.

The new Pool and Vault system has two key benefits:

1. Better risk management: Users can select one of many liquidity pools, which are connected to one or more markets, allowing more fine-tuned control of LP risk.
2. Wider collateral range: The V3 system is collateral agnostic, allowing any governance-approved asset to serve as collateral for borrowing sUSD and delegate to derivative markets.

Stakers have an increasing range of Pools to allocate their capital. This gives stakers more control over their collateral as the V3 system provides many more options for fine-tuned control.

</details>

<details>

<summary>What is the cross-chain vision for Synthetix?</summary>

**Answer**: The endstate goal of cross-chain Synthetix is to power derivative markets on any governance-approved EVM chain with a fully interoperable system. This will allow Synthetix-powered protocols to onboard traders on any chain and deliver the same low-fee deep liquidity trading experience to new users.

</details>

<details>

<summary>How is V3 different from other derivatives platforms?</summary>

**Answer:** Simply put, Synthetix V3 isn’t like any other derivatives protocol because it isn’t a derivatives protocol. Instead, Synthetix is a liquidity layer that helps to power derivative protocols with its infrastructure and liquidity. This is a new era of Synthetix. New architecture, new premise, and a fundamentally new offering: _the liquidity layer for defi._

Synthetix will power a multi-market ecosystem, encompassing perpetual futures, spot, options, insurance, exotics, and more, all backed by Synthetix Liquidity. With this vision, V3 paves the way for a new generation of derivative markets, where builders can leverage the protocol and bootstrap their communities for success - a new and exciting premise for Synthetix and the Ethereum ecosystem.

The liquidity-as-a-service model appeals to new DeFi protocols seeking increased liquidity for on-chain derivatives so they can build on Synthetix easily and efficiently. With Synthetix Perps as an example, frontend integrators like Kwenta and Polynomial utilize Synthetix’ liquidity to power perps trading, boasting deep liquidity and historically low fees. Off-chain oracles reduce fees to 5-10bps, and risk management tools ensure market neutrality over the long term. These features combine to ensure Synthetix leads the way in decentralized derivatives.

</details>

<details>

<summary>Why should projects integrate with Synthetix Liquidity?</summary>

**Answer:** Launching a derivatives protocol can be challenging, with teams often faced with the cold-start problem – not enough liquidity to attract users, and not enough users to attract liquidity providers. With Synthetix, developers can create new markets and seamlessly attract liquidity. In this way, almost any derivative protocol can be built on top of Synthetix V3, as opposed to building from the ground up. Learn more on how protocols can integrate with Synthetix V3 [here](https://docs.synthetix.io/v/v3/).

</details>

<details>

<summary>What incentive do projects have to build on Synthetix V3?</summary>

**Answer:** The incentives for building on Synthetix V3 are numerous and impactful:

1. **Infrastructure:** Synthetix V3 abstracts away the complexities of building your own infrastructure. This enables derivative developers to primarily focus on market design and innovation rather than backend complexities.
2. **Liquidity:** A common challenge for most protocols is generating sufficient liquidity to support derivative traders effectively. Synthetix addresses this with a deep liquidity pool to back derivatives, ensuring that protocols can thrive.
3. **Rewards:** The Partner Volume Rewards program rewards derivative developers and protocols for generating trading volume using Synthetix Perps.

</details>

<details>

<summary>What will change in V3 Perps?</summary>

**Answer:**\
\
Building on the successes of  Perps V2, V3 introduces several upgrades to improve the trading and developer experience:

* Multi Collateral: Supports multiple collateral types, currently limited to synths registered with the V3 spot market; this is expected to include sUSD, sETH, sBTC, and other governance-approved spot synths.
* Cross margin: account margin can be used across positions on markets natively rather than via smart wallets with front-end integrators.
* Account-Based Access Controls: Enables delegation of account permissions, such as modifying collateral and managing positions, to additional addresses, enhancing extensibility and composability.
* Liquidation Improvements: Implements gradual, non-sandwichable liquidation of large positions, with configurable delays between partial liquidations.
* Deterministic Settlements: Improves the settlement process to ensure that the execution price is the earliest valid price post-commitment, minimizing the impact of network congestion.
* Key limitations
  * Single position per market (same as v2)
  * Only async orders (no other order types) (delayed offchain orders)
  * Single pending order
  * No cancellation of orders; once order is expired, a new order can be placed.

</details>

<details>

<summary>What tooling and resources are available for building on Synthetix V3?</summary>

**Answer:** Synthetix will offer a variety of resources for builders looking to integrate with the V3 system. To start, all builders should review our documentation here: [https://docs.synthetix.io/v/v3/](https://docs.synthetix.io/v/v3/). This repository should contain all the relevant contracts, guides, and FAQs for building on top of Synthetix.

Developers can use [Cannon](https://usecannon.com/), a tool for managing protocol deployments that is built and maintained by Synthetix core contributors.\
\
SDKs are also being developed to interface with Synthetix Perps.

</details>

<details>

<summary>Are there any significant differences between sUSD and snxUSD?</summary>

**Answer:** There will not be significant differences between sUSD and snxUSD (note that once V3 is fully live, sUSD will be the new stablecoin, and sUSDLegacy will be what is currently called sUSD from our V2 systems). sUSD and snxUSD will be non-fungible with one another, as they are generated by different versions of Synthetix.

</details>

<details>

<summary>How will oracles be used permissionlessly in V3?</summary>

**Answer:** Synthetix V3 will maintain agnostic oracle management for markets. This means market creators can choose from multiple oracle solutions, including Chainlink and Pyth, to set up custom aggregation - giving them more control over the oracles that power their markets. The oracle manager opens up new opportunities for supporting new markets and assets.

</details>
