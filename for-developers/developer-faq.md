---
description: A guide to help developers start interacting with Synthetix V3
---

# Developer FAQ

## Testnet Assets

Where can I get assets on OP Goerli?&#x20;

* `ETH`: Optimism Goerli ETH is available from various faucets. We recommend the official [Optimism faucet](https://app.optimism.io/faucet) but there are also [other faucets](https://community.optimism.io/docs/useful-tools/faucets/) available.
* `snxETH`: You can wrap OP Goerli ETH into snxETH on "Spot" tab of [the market prototype](https://synthetix-markets-prototype.vercel.app/). This is the easiest way to get assets for testing if you have testnet ETH.
* `snxUSD`: snxETH acquired through wrapping can be sold for snxUSD on the spot market prototype.

Where can I get assets on Base or Arbitrum Goerli?&#x20;

* Testnet stablecoins can be acquired on [Base Sepolia](https://sepolia.basescan.org/address/0xa1ae612e07511a947783c629295678c07748bc7a) or [Arbitrum Seplia](https://sepolia.arbiscan.io/address/0xdfe41770267faa60832c39dd9819a5fb030b3b3b). Use the function `deposit_eth`, specify the address of the stablecoin (snxUSD, fUSDC, sUSDC) and send some ETH to receive stable coins. Note that for perp integrators, you can use snxUSD as margin. If you want to have sETH for using as margin sUSD can easily be swapped to sETH with the [Spot Market](developer-faq.md#spot-markets).

## Smart Contracts

* All v3 contracts are under proxy, to find which you have to check the cannon file.&#x20;
* Cannon is the tooling used to define v3, see [https://usecannon.com/packages/synthetix](https://usecannon.com/packages/synthetix)
* Owner is the address indicated by the `owner` function, depends on network.&#x20;
* Function to use for enabling feature flag to all is `setFeatureFlagAllowAll` I believe
* Decide any error from v3 with `cannon decode synthetix-omnibus --chain-id 1 {paste 0x error code here}`

## **Spot Market**

How can I swap assets?

1. Navigate to the [spot market prototype](https://synthetix-markets-prototype.vercel.app/)
2. Prepare your order and click "Submit order". If a token approval is required, you will be prompted with two transactions.
3. Wait 10 seconds and refresh the page
4. Click "View Pending Orders", open the "Committed" tab, and check the "My Orders" button
5. When the "Settle" button is enabled, click it and submit the transaction.
