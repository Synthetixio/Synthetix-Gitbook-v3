# Quick Start

Run a local node with clean deployment of the Synthetix core system, mock collateral, the oracle manager, a spot market, and a perps market with the following command:

```
npx @usecannon/cli synthetix-sandbox
```

To export the ABIs and contract addresses for this deployment, run the following command:

```
npx @usecannon/cli inspect synthetix-sandbox --write-deployments ./deployments 
```

_Remember to always interact with the proxy contracts instead of the router or modules directly._

Check out the [**Synthetix Sandbox repository**](https://github.com/synthetixio/synthetix-sandbox) to see the specifics of how this node is configured. You can fork the repository, make modifications to the Cannonfile to create different scenarios, and use `SampleIntegration.sol` as a boilerplate for developing smart contract integrations.

If you have questions, reach out in the #dev-portal channel of the [Synthetix Discord server](https://discord.gg/synthetix).

