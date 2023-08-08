# Registering a Market

Markets can be integrated with the Synthetix protocol to access credit capacity from liquidity providers. Markets report a balance of debt, may deposit snxUSD, and withdraw snxUSD depending on the amount of liquidity delegated to them by pools (which determines their credit capacity).[​](https://snx-v3-docs.vercel.app/pools-markets/integrating-markets#registering-markets)

{% hint style="info" %}
**Synthetix V3 is currently in alpha.** Only governance can register markets until an SCCP alters the feature flag.
{% endhint %}

Before a market can interact with the protocol, it must be registered using the `registerMarket` function. This function accepts the address of a market, which will be able to integrate with Synthetix (to perform actions like depositing and withdrawing snxUSD) using the ID returned by the function.

Markets cannot be registered unless they conform to the `IMarket` interface. See [Integrating Synthetix](integrating-synthetix.md) for more information on the functions that must be implemented.
