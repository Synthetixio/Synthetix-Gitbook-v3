# Registering a Market

Markets can be integrated with the Synthetix protocol to access credit capacity from liquidity providers. Markets report a balance of debt, may deposit snxUSD, and withdraw snxUSD depending on the amount of liquidity delegated to them by pools (which determines their credit capacity).[​](https://snx-v3-docs.vercel.app/pools-markets/integrating-markets#registering-markets)

{% hint style="info" %}
**Synthetix V3 is currently in alpha.** Only governance can register markets until an SCCP alters the feature flag.
{% endhint %}

Before a market can interact with the protocol, it must be registered using the `registerMarket` function. This function accepts the address of a market, which will be able to integrate with Synthetix (to perform actions like depositing and withdrawing snxUSD) using the ID returned by the function.

Markets cannot be registered unless they conform to the `IMarket` interface. See [Integrating Synthetix](integrating-synthetix.md) for more information on the functions that must be implemented.

Derivatives market implementations can be [registered](registering-a-market.md) with the Synthetix protocol if they conform to the `IMarket` interface. This consists of just three functions:

* `function name(uint128 marketId) external view returns (string memory);` - A function which should return a human-readable name for the given market.
* `function reportedDebt(uint129 marketId) external view returns (uint);` - A function which should return the total value of debt issued by the market (to be collateralized by the assets in the pools backing it), denominated with 18 decimals places.
* `function minimumCredit(uint128 marketId) external view returns (uint);` - A function which returns the amount of credit under which pools cannot rescind credit delegated to the market. This value is dollar-denominated, with 18 decimals places. If the market implementation does not intend to lock collateral, this function can just `return 0;`. **Note that the amount of credit available to a market may still fall below this amount due to price action of the collateral backing it.**
