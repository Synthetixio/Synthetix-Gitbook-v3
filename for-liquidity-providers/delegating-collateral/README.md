# Delegating Collateral

Providing liquidity to pools involves two function calls, `deposit` and `delegateCollateral`. `deposit` transfers collateral to the Synthetix Core address and associates it with the relevant account. `delegateCollateral` assigns the collateral to a pool, creating or updating a [**liquidity position**](../liquidity-positions/).

<figure><img src="../../.gitbook/assets/V3_Docs_Diagram_02.png" alt=""><figcaption></figcaption></figure>

`deposit` and `withdraw` increase and decrease the amount of available collateral associated with an account. `delegateCollateral` will increase/decrease the amount of available collateral by altering the amount provided to a specified pool. These functions may be called together using the `multicall` function, so end users need to only execute one transaction.

When delegating, the position size must be greater than a minimum amount, specified by governance per collateral type. This generally serves as the [liquidation reward](../liquidity-positions/position-liquidations.md) for the position.

There are a few scenarios in which collateral may not have its delegation reduced or be withdrawn:

* Delegated collateral may only be reduced if the liquidity position’s resulting C-Ratio is greater than the Issuance C-Ratio for its collateral type. In other words, liquidity providers can only retrieve their collateral if they pay off their debt.
* Delegated collateral may not be reduced if the resulting credit capacity for any of the markets connected to the pool would drop below the market's [minimum credit value](../../for-derivatives-market-builders/integrating-synthetix.md).
* Delegated collateral may not be adjusted unless the minimum collateral delegation duration has elapsed since the last time `delegateCollateral` was called pertaining to this liquidity position. This is a mechanism which allows markets to mitigate the risk of active liquidity providers front-running market activity.
* Available collateral may not be withdrawn unless the globally configured withdraw timeout has elapsed since this account has last been interacted with. This is a global system safety parameter which may eventually be set to 0 via [SCCP](https://sips.synthetix.io/all-sccp/).

The types of collateral which are accepted by the protocol are configured globally by governance. Enabling, disabling, or changing the settings pertaining to collateral may be proposed via [SCCP](https://sips.synthetix.io/all-sccp/). Retrieve information about the currently accepted collateral types with the `getCollateralConfigurations` function.
