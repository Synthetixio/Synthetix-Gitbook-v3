# Minting and Burning snxUSD

The protocol generates **snxUSD**, a decentralized, over-collateralized stablecoin backed by the collateral deposited in the Synthetix protocol. snxUSD is an ERC-20 token used by markets integrated with Synthetix.

{% hint style="info" %}
Minting and burning effects an account's available balance. snxUSD must be deposited before minting and withdrawn after burning.
{% endhint %}

Once a liquidity position has been created by delegating collateral, liquidity providers can take out an interest-free loan of snxUSD by "minting" it. snxUSD is minted by calling the `mintUsd` function. The debt of the position increases by $1 for each snxUSD token minted.

Liquidity providers may not mint snxUSD such that their position’s c-ratio drops below the Issuance C-Ratio for the relevant collateral type. The Issuance C-Ratio for each collateral type is set by governance. The `getCollateralConfiguration` function will return the Issuance C-ratio, represented as an integer with 18 decimal places.

snxUSD can also be used to repay loans by "burning" it. snxUSD is burned by calling the `burnUsd` function. This decreases the debt of a position by $1 per snxUSD burned, regardless of whether this debt was accrued from minting snxUSD or from debt distributed to it by a market. To reduce the collateral delegated to a position, debt must be repaid such that the resulting C-Ratio is above the Issuance C-Ratio.

{% hint style="info" %}
snxUSD is integrated with [Chainlink's CCIP](https://chain.link/cross-chain) to allow for secure, decentralized cross-chain transfers of snxUSD between networks with a Synthetix deployment.
{% endhint %}
