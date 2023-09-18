# Creating and Configuring Pools

**Liquidity Pools** distribute credit and debt between liquidity providers and derivatives markets. A pool's manager (i.e. owner) can decide which market to provide with liquidity and set relevant configuration values.

## Creating Pools[​](https://snx-v3-docs.vercel.app/pools-markets/delegating-credit-and-debt#creating-pools) <a href="#creating-pools" id="creating-pools"></a>

{% hint style="info" %}
**Synthetix V3 is currently in alpha.** Only governance can create pools until an SCCP alters the feature flag.
{% endhint %}

Pools may be created using the `createPool` function. Ownership can then be transferred with the `nominatePoolOwner` and `acceptPoolOwnership` functions. Ownership nomination may also be renounced with the `renouncePoolNomination`.

Pools may also have human-readable names stored on-chain, which can be set by the owner using the `setPoolName` function and retrieved with the `getPoolName` function.

## Configuring Pools[​](https://snx-v3-docs.vercel.app/pools-markets/delegating-credit-and-debt#configuring-pools) <a href="#configuring-pools" id="configuring-pools"></a>

The owner of a pool may set a list of markets to back (with corresponding **weights** and **maximum debt share values**) using the `setPoolConfiguration` function.

Fundamentally, this configuration effects the share of a market's profit/loss that a pool will assume, the maximum amount of debt the pool is willing to assume, and the credit capacity (i.e. amount of withdrawable snxUSD) provided to each market.

There are a couple scenarios in which a pool's configuration is restricted in how it can be updated:

* The pool configuration change will be prevented if it would leave the total amount of credit capacity provided to a market lower than the amount it returns in its `minimumCredit` function.
* The pool configuration cannot be changed unless the minimum collateral delegation duration has elapsed since the last time `setPoolConfiguration` was called for this pool.

### Collateral Configuration

By default, pools accept all collateral types approved by governance (using the configuration set by governance). Pool owners can set pool-specific collateral configurations using the `setPoolCollateralConfiguration` function.

`issuanceRatioD18` is a custom issuance ratio for the specified collateral type. The system will always use the greater of this value and the issuance ratio set by governance. (Setting this value to  the maximum integer value effectively turns off minting using this collateral type in this pool.)

`collateralLimitD18` is the maximum total amount of collateral that this pool will accept for the specified collateral type. (Note that if this is less than the `minDelegationD18` value, this pool has opted out of accepting this collateral type.)

In the pool configuration (not to be confused with the pool _collateral_ configuration), pool owners can set the `collateralDisabledByDefault` value to `true`. In this case, new collateral types cannot be delegated to this pool. The pool owner must set a `collateralLimitD18` value to accept it. In other words, `collateralLimitD18 == 0` means that the pool will accept an unlimited amount of this collateral, unless `collateralDisabledByDefault` is set to `true`.

### Calculating Credit Capacity[​](https://snx-v3-docs.vercel.app/pools-markets/delegating-credit-and-debt#calculating-credit-capacity) <a href="#calculating-credit-capacity" id="calculating-credit-capacity"></a>

To understand how the pool configuration function works, it's useful to see how it effects the available credit capacity (i.e. amount of withdrawable snxUSD) provided to markets.

**Weights** determine what proportion of the liquidity in a particular pool should be allocated to each market. For example, if a pool has $500,000 of liquidity with a weight of 3 assigned to an snxBTC market and a weight 1 assigned to an snxEUR market, the collateral provided to these markets would be $375,000 and $125,000, respectively.

Then, a **maximum debt share value** is determined. We take the lesser of these two values:

* The maximum debt share value set in the pool's configuration, per above. The maximum debt share value also allows a pool to stop backing a market if it accrues too much debt. (See [Credit and Debt Distribution](credit-and-debt-distribution.md) for more details.)
* The **minimum liquidity ratio** is applied to the collateral value after factoring in the weights. For instance, if the collateral value derived from the weights minus the vault's debt which has already been assigned is $100 and the minimum liquidity ratio is set to 200%, this maximum debt share value would be $0.50. This value is added to the existing debt share value to determine the number of dollars per debt share than can be assumed before the market exceed the minimum liquidity ratio. So if the current debt share value is $0.25, in this case, the maximum debt share value calculated here would be $0.75. This maximum debt share value fluctuates over time, as the value of the debt, the value of the collateral, and amount of the collateral backing a market changes over time.

The credit capacity that a market gets is the difference between the maximum debt share value subtracted by the current debt per share value. For instance, if the collateral value derived from the weights is $100, the maximum debt share value is $0.75, and the current debt share value is $0.25, the actual credit capacity provided to the market would be $50.[​](https://snx-v3-docs.vercel.app/pools-markets/delegating-credit-and-debt#available-credit)

Finally, the available credit capacity for a market can be calculated by taking the total credit capacity provided to it across all pools, subtracting its amount of reported debt and its net issuance (i.e. the amount of stablecoins it has minted minus the amount it has burned). This is the maximum amount of stablecoins it is allowed to withdraw. If it begins to report debt such that its available credit drops below 0, the market becomes insolvent and positions which are backing this market no longer accrue debt.

### Debt Shares

The collateral value provided to markets (described above in the discussion of weights) is essentially the amount of value available to back the derivatives issued by a market—both the snxUSD it withdraws and the reported debt, which represents the value of the derivatives the market has issued.

By providing liquidity to a market, liquidity pools assume pro-rata shares of the market's changes in debt, positive or negative. (See [Credit and Debt Distribution](credit-and-debt-distribution.md) for more details.) In other words, if a pool provides more weight towards a particular market (all else equal), they will incur greater gains if the market is profitable and greater losses if the market is not. If other pools begin to provide liquidity to market, the original pool's share of gains/losses will decrease. This results in Synthetix creating a market for derivatives liquidity.

If a market has earned $2 of profit for every $1 dollar of credit capacity assigned to it, it's debt share value would be -$2. This is effectively a market's lifetime PnL.

