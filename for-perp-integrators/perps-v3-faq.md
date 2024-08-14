# Perps V3 FAQ

What are the major differences between Perps V2 and V3?

* **Perps Accounts -** Before interacting with the markets traders first create an account, represented as an NFT. An account on Optimism can own many perps accounts, which allows for isolating collateral and opening many positions on a market. Each interaction will take this `accountId` as a parameter.
* **Cross margin -** All positions in a perps account are cross-margined against the provided collateral. If the account's collateral drops below their maintenance margin, all positions will be closed and all collateral in the account will be liquidated.
* **Alternate collateral** **-** Perps accounts can now contain more collateral types than sUSD. These collaterals will increase your available margin based on the latest oracle price. If the total USD value of these collaterals drops below your maintenance margin, all collateral types will be liquidated. \
