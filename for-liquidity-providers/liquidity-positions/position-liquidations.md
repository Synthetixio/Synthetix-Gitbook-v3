# Position Liquidations

When the collateralization ratio of a particular liquidity position drops below the liquidation collateralization ratio for its corresponding collateral type, the position may be liquidated. When this occurs, the collateral and debt associated with the position are distributed among all of the other liquidity position participating in the pool with the same collateral type pro-rata (after a fixed amount of the collateral is provided to the liquidator, typically a bot, as an incentive).

Anyone can check if a liquidity position can be liquidated with the `isPositionLiquidatable` function. If this function returns `true`, then the position may be liquidated with the `liquidate` function. The address calling the function will receive `liquidationRewardD18` per the `getCollateralConfiguration` function (or all of the position’s collateral if it is less than this amount).
