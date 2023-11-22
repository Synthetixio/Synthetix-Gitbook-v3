---
description: Evolving reference for Core V3 + Perps V3 on Base
---

# Base Andromeda

{% hint style="info" %}
### INTERIM timeline&#x20;

* Week beginning Nov 6th: Perps V3 starting audit  ✅
* Week beginning Nov 13th: Andromeda 3.3.3 on [Base Goerli](https://usecannon.com/packages/synthetix-omnibus/latest/84531-andromeda) ✅
* Week beginning Nov 20th: Andromeda 3.4.0 on Base mainnet 🚧
* Week beginning Dec 4th: Andromeda 3.5.0 on Base mainnet (pending Perp audit)&#x20;
* TBC: Public launch of Andromeda on Base mainnet and announcements
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
* Configuration explained:&#x20;
  * [this is the part](https://github.com/Synthetixio/synthetix-deployments/pull/66/files#diff-dc0e4e9b2b24d1fcf9c5a8ffd5b5548955777eff55c71dd0ab208dc04e84a89b) that deploys sUSDC (a USDC synth) and creates the spot market
  * &#x20;USDC <-> sUSDC can be wrapped/unwrapped on the spot market
  * sUSD <-> sUSDC can be bought/sold on the spot market
  * No fee on these, all atomic so can be composed with multicalls
* _Coming: Andromeda Base Sandbox - in the meantime see the more general_ [sandbox-with-perps.md](sandbox-with-perps.md "mention") _can be used once USDC is wrapped and swapped to sUSD_

// TODO: [https://github.com/pyth-network/pyth-sdk-solidity/blob/main/MockPyth.sol](https://github.com/pyth-network/pyth-sdk-solidity/blob/main/MockPyth.sol)

{% embed url="https://usecannon.com/packages/synthetix-omnibus/latest/84531-andromeda" %}
Base Goerli Andromeda
{% endembed %}

## For LPs

LPs can arrive with USDC to provide liquidity (LP). The contracts or integrators need to:

1. Wrap USDC to sUSDC on the Spot Market
   1. Function: `SpotMarketProxy.wrap(marketId, wrapAmount, amountReceived)`
   2. Example: `wrap(1, 1000000000000000000, 1000000000000000000)`
2. Deposit sUSDC to Pool
3. Delegate sUSDC to Market

// TODO: are fees in sUSD and need to be swapped back to USDC?

When withdrawing, initial collateral plus any fees can be withdrawn, then unwrapped from sUSDC to USDC.

## For Traders/Integrators

Integrators can create a seamless trading experience using USDC by utilizing the wrapper and spot  market. Since `USDC-sUSDC` and `sUSDC-sUSD` exchanges are both 1:1 swaps, integrators can easily create a "zap" between USDC in their wallet and their account margin.

### **Prerequisites**

An account must meet the following requirements to execute USDC transfers between their wallet and a perps account.

**Deposit:**

* Holds an account NFT for perps
* Approve `SpotMarketProxy` to transfer USDC
* Approve `SpotMarketProxy` to transfer sUSDC
* Approve `PerpsMarketProxy` to transfer sUSD

**Withdraw:**

* Account NFT has some withdrawable margin
* Approve `SpotMarketProxy` to transfer sUSD
* Approve `SpotMarketProxy` to transfer sUSDC

### Preparing the Transactions

If you meet these requirements you can prepare a multicall to execute in a single transaction. Use `marketId = 1` for `sUSDC`. Matching values like `wrapAmount` and `amountReceived` in the transactions will guarantee this 1:1 swap.

All transactions should be prepared as a multicall and sent to the `TrustedMulticallForwarder` contracts using `aggregate3Value`.

**Deposit:**&#x20;

1. `USDC -> sUSDC` - Wrap USDC on the spot market
   1. Function: `SpotMarketProxy.wrap(marketId, wrapAmount, amountReceived)`
   2. Example: `wrap(1, 1000000000000000000, 1000000000000000000)`
2. `sUSDC -> sUSD` - Sell sUSDC for sUSD on the spot market
   1. Function: `SpotMarketProxy.sell(marketId, synthAmount, minUsdAmount, referrer)`
   2. Example: `sell(1, 1000000000000000000, 1000000000000000000, 0x0000000000000000000000000000000000000000)`
3. Deposit sUSD
   1. Function: `PerpsMarketProxy.modifyCollateral(accountId, synthMarketId, amountDelta)`
   2. Example: `modifyCollateral(12345, 0, 1000000000000000000)`

**Withdraw:**

1. Withdraw sUSD
   1. Function: `PerpsMarketProxy.modifyCollateral(accountId, synthMarketId, amountDelta)`
   2. Example: `modifyCollateral(12345, 0, -1000000000000000000)`
2. `sUSD -> sUSDC` - Buy sUSDC on the spot market
   1. Function: `SpotMarketProxy.buy(marketId, usdAmount, minAmountReceived, referrer)`
   2. Example: `buy(1, 1000000000000000000, 1000000000000000000, 0x0000000000000000000000000000000000000000)`
3. `sUSDC -> USDC` - Unwrap sUSDC on the spot market
   1. Function: `SpotMarketProxy.unwrap(marketId, unwrapAmount, minAmountReceived)`
   2. Example: `unwrap(1, 1000000000000000000, 1000000000000000000)`

**Sample Transactions**

* [Deposit](https://goerli.basescan.org/tx/0x95461a5b05c40c91c952bc06b0d292ec16ffd0c750a7b708a8564183b9b08cf4)
* [Withdraw](https://goerli.basescan.org/tx/0x4b6d29faaa75223fe1d690993c5e93ef316fc823385cbc52f505927f65702319)

### Notable changes from Testnet Competition

* Interface: [Staleness Tolerance](https://github.com/Synthetixio/synthetix-v3/pull/1860)
* Keepers: [Gas based keeper rewards](https://github.com/Synthetixio/synthetix-v3/pull/1890)

### Notable recent changes

{% embed url="https://rattle-ticket-183.notion.site/Perps-andromeda-branch-changes-512cf7a6c696463da0980907f00511ea?pvs=4" %}

