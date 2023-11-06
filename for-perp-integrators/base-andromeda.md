---
description: An evolving reference for Perps V3 on Base
---

# Base Andromeda

### Configuration

* Unique to Andromeda Base is the use of a USDC wrapper, enabling USDC to appear to be used as collateral for LPs, and as margin as perp traders.
* Underneath, USDC is wrapped and or traded into sUSDC for LP collateral (and collecting fees), and sUSD as perp margin
* The full configuration of Base Goerli can be seen [on Cannon](https://usecannon.com/packages/synthetix-omnibus/3.3.3-dev.e141cd8c/84531-andromeda)
* Configuration explained:&#x20;
  * [this is the part](https://github.com/Synthetixio/synthetix-deployments/pull/66/files#diff-dc0e4e9b2b24d1fcf9c5a8ffd5b5548955777eff55c71dd0ab208dc04e84a89b) that deploys a synthUSDC and makes the spot market
  * &#x20;USDC <-> sUSDC can be wrapped/unwrapped on the spot market
  * sUSD <-> sUSDC can be bought/sold on the spot market
  * No fee on these, all atomic so can be composed with multicalls
* _Coming: Andromeda Base Sandbox - in the meantime see the more general_ [sandbox-with-perps.md](sandbox-with-perps.md "mention") _can be used once USDC is wrapped and swapped to sUSD_
* TODO: [https://github.com/pyth-network/pyth-sdk-solidity/blob/main/MockPyth.sol](https://github.com/pyth-network/pyth-sdk-solidity/blob/main/MockPyth.sol)

#### For LPs

LPs can arrive with USDC to LP:

1. Wrap USDC to sUSDC
2. Deposit sUSDC
3. Delegate sUSDC

When withdrawing, initial collateral plus any fees can be withdrawn, then unwrapped from sUSDC to USDC.

#### For Traders/Integrators

If I am a trader or integrator wanting to margin with USDC:

1. Wrap USDC for sUSDC
2. Swap sUSDC for sUSD with Spot Market
3. Deposit the sUSD to the Perps Market

Reverse this when withdrawing any margin and profits, by withdrawing sUSD, swapping for sUSDC, and unwrapping to USDC.

### Notable changes from Testnet Competition

* Interface: [Staleness Tolerance](https://github.com/Synthetixio/synthetix-v3/pull/1860)
* Keepers: [Gas based keeper rewards](https://github.com/Synthetixio/synthetix-v3/pull/1890)

### Working timeline

* Perps V3 in audit from Nov 6th
* V3 Core mainnet release from Nov 13th
* Perps V3 mainnet release from Nov 20th

