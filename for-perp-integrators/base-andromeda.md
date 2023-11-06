---
description: An evolving reference for Perps V3 on Base
---

# Base Andromeda

#### Configuration

* Unique to Andromeda Base is the use of a USDC wrapper, enabling USDC to be used as collateral for LPs, and for margin as perp traders.
* The configuration of Base Goerli can be seen [on Cannon](https://usecannon.com/packages/synthetix-omnibus/3.3.3-dev.e141cd8c/84531-andromeda)
* Configuration explained:&#x20;
  * traders margins with sUSD and LPs collect fees in sUSD (minted)
  * this is the part that deploys a fake USDC and makes the spot market [https://github.com/Synthetixio/synthetix-deployments/pull/66/files#diff-dc0e4e9b2b24d1fcf9c5a8ffd5b5548955777eff55c71dd0ab208dc04e84a89b](https://github.com/Synthetixio/synthetix-deployments/pull/66/files#diff-dc0e4e9b2b24d1fcf9c5a8ffd5b5548955777eff55c71dd0ab208dc04e84a89b)
  * You can go USDC <-> sUSDC (with wrap/unwrap) on the spot market
  * sUSD <-> sUSDC (with buy/sell).&#x20;
  * No fee on these, all atomic so can be composed with multicalls
  * [https://github.com/pyth-network/pyth-sdk-solidity/blob/main/MockPyth.sol](https://github.com/pyth-network/pyth-sdk-solidity/blob/main/MockPyth.sol)
* _Coming: Andromeda Base Sandbox - in the meantime see the more general_ [sandbox-with-perps.md](sandbox-with-perps.md "mention")

#### For LPs

1. Take USDC
2. Wrap to sUSDC
3. Deposit sUSDC
4. Delegate sUSDC

#### For Traders/Integrators

If I am a trader with USDC, I should:

1. Wrap USDC for sUSDC
2. Swap sUSDC for sUSD with Spot Market
3. Deposit the sUSD to the Perps Market

#### Notable changes from Testnet Competition

* Interface: [Staleness Tolerance](https://github.com/Synthetixio/synthetix-v3/pull/1860)
* Keepers: [Gas based keeper rewards](https://github.com/Synthetixio/synthetix-v3/pull/1890)

#### Working timeline

* Perps V3 in audit from Nov 6th
* V3 Core mainnet release from Nov 13th
* Perps V3 mainnet release from Nov 20th

