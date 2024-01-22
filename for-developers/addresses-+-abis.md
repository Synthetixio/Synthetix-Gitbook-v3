# Addresses + ABIs

Find all the deployment details in the [deployment-info.md](deployment-info.md "mention") section.&#x20;

* [1-main.md](../deployment-info/1-main.md "mention")
* [5-main.md](../deployment-info/5-main.md "mention")
* [11155111-main.md](../deployment-info/11155111-main.md "mention")
* [10-main.md](../deployment-info/10-main.md "mention")
* [420-main.md](../deployment-info/420-main.md "mention")
* [8453-andromeda.md](../deployment-info/8453-andromeda.md "mention")
* [84531-andromeda.md](../deployment-info/84531-andromeda.md "mention")
* [84532-andromeda.md](../deployment-info/84532-andromeda.md "mention")

The code for deployments can be found in the [synthetix-deployments](https://github.com/synthetixio/synthetix-deployments) GitOps repository.

To download the Addresses + ABIs for Synthetix via the command line with `cannon`, you can run the following command:

```sh
npx @usecannon/cli inspect synthetix-omnibus@${PRESET} \
  --write-deployments ./deployments \
  --chain-id ${CHAIN_ID}
```
