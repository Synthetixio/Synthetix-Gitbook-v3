# Addresses + ABIs

Find all the deployment details in the [deployment-info.md](deployment-info.md "mention") section.&#x20;

* [Mainnet: 1-main](../deployment-info/1-main.md "mention")
* [Sepolia: 11155111-main](../deployment-info/11155111-main.md "mention")
* [Sepolia Carina: 11155111-carina](../deployment-info/11155111-carina.md "mention")
* [Optimism Mainnet: 10-main](../deployment-info/10-main.md "mention")
* [Base Mainnet Andromeda: 8453-andromeda](../deployment-info/8453-andromeda.md "mention")
* [Base Sepolia Andromeda: 84532-andromeda](../deployment-info/84532-andromeda.md "mention")
* [Arbitrum Sepolia: 421614-main](../deployment-info/421614-main.md "mention")

The code for deployments can be found in the [synthetix-deployments](https://github.com/synthetixio/synthetix-deployments) GitOps repository.

To download the Addresses + ABIs for Synthetix via the command line with `cannon`, you can run the following command:

```sh
npx @usecannon/cli inspect synthetix-omnibus@${PRESET} \
  --write-deployments ./deployments \
  --chain-id ${CHAIN_ID}
```
