# V3 Frequently Asked Questions (FAQ)

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

<summary>How is SNX staking evolving with V3?</summary>

**Answer:** The power is with stakers in V3, thanks to multi-collateral staking and permissionless pools. V3 creates a generalized system agnostic to collateral type. Liquidity providers can deposit any governance-approved collateral into Pools, which is then used to provide liquidity to derivative markets. In the future, the creation of markets and vaults will be permissionless, giving liquidity providers fine-tune control of their market exposure.

The new Pool and Vault system has two key benefits:

1. Better risk management: Users can select one of many liquidity pools, which are connected to one or more markets, allowing more fine-tuned control of LP risk.
2. Wider collateral range: The V3 system is collateral agnostic, allowing any governance-approved asset to serve as collateral for borrowing sUSD and delegate to derivative markets.

Stakers have an increasing range of Pools to allocate their capital. This gives stakers more control over their collateral as the V3 system provides many more options for fine-tuned control.

</details>

<details>

<summary>What types of collateral will there be outside of SNX?</summary>

**Answer:** The V3 system is created to be entirely agnostic to collateral; any ERC-20 with sufficient price feed can be added as collateral. Synthetix governance will determine which assets to support in addition to SNX.

Synthetix V3 features a generalized collateral vault system that is agnostic to collateral types. Over time, Synthetix Governance will determine which assets to support as collateral in addition to the current SNX (staking) and ETH (wrappers). Multi-collateral staking will increase sUSD liquidity and the markets supported by Synthetix. Collateral options will have adjustable variables, such as collateral requirements and rewards, which can be adjusted by governance.

</details>

<details>

<summary>What is the cross-chain vision for Synthetix?</summary>

**Answer**: The endstate goal of cross-chain Synthetix is to power derivative markets on any governance-approved EVM chain with a fully interoperable system. This will allow Synthetix-powered protocols to onboard traders on any chain and deliver the same low-fee deep liquidity trading experience to new users.

As of Oct 2023, Governance is exploring an initial deployment plan on Base Network to experiment with new collateral types, fee sharing, and V3 markets.

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

<summary>What are the main challenges for users Synthetix foresees as the protocol transitions from V2 to V3?</summary>

**Answer:** The transition from V2 to V3 is intended to improve the user experience with Synthetix by giving more flexibility in how LPs allocate their collateral and which derivatives markets builders can integrate with the system.

In the beginning of the transition, Synthetix will set up the Spartan Council Pool, which will include all legacy positions from V2 and will back Perps V3 and Spot Synths. The liquidity provisioning experience in this period should remain similar to what users currently experience on V2. As V3 becomes more built out, with permissionless markets tapping into permissionless liquidity pools, users will have a greater selection of how and where to allocate their collateral.

Further as we transition to V3, there will be two non-fungible USD stablecoins that will be live at the same time. Users should be aware that any markets built on the V3 system will be using the new stablecoin and that external pools or integrations may require an update to the new version.

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

Developers can use [Cannon](https://t.co/hcGnoDWtND), a tool for managing protocol deployments that is built and maintained by Synthetix core contributors.\
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
