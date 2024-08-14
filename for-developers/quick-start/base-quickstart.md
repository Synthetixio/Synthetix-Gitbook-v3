# Base Quickstart

[Synthetix V3](https://github.com/synthetixio/synthetix-v3) consists of multiple systems, deployed via [an omnibus](https://github.com/Synthetixio/synthetix-deployments/blob/main/omnibus-base-mainnet-andromeda.toml) on [Base](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda) and other chains.

* Synthetix's [core system](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda/interact/system/CoreProxy/0x32C222A9A159782aFD7529c87FA34b96CA72C696) holds collateral and manages liquidity provisioning for the deployment. It issues an [account NFT](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda/interact/system/AccountProxy/0x63f4Dd0434BEB5baeCD27F3778a909278d8cf5b8) to liquidity providers and [a stablecoin](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda/interact/system/USDProxy/0x09d51516F38980035153a554c26Df3C6f51a23C3) used by traders.
* There is a [spot market](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda/interact/spotFactory/SpotMarketProxy/0x18141523403e2595D31b22604AcB8Fc06a4CaA61) used to wrap USDC into synthetic USDC (for LPs) and this can be "sold" into the stablecoin. All of these exchanges happen 1:1. Additional types of collateral may be introduced in the future.
* The [perpetual futures market](https://app.gitbook.com/s/v5Uy5QOMZ00RFWLf1gmn/protocol-design) issues an [account NFT](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda/interact/perpsFactory/PerpsAccountProxy/0xcb68b813210aFa0373F076239Ad4803f8809e8cf) to traders.
* All of the systems integrate with the [oracle manager](https://usecannon.com/packages/synthetix-omnibus/latest/8453-andromeda/interact/system.oracle\_manager/Proxy/0x3d07CBC5Cb9376A67E76C0655Fe239dDa8E2B264) to assess the value of collateral and derivatives.

### Building Apps/Front-ends

To start a local node with running with the same configuration as the Base deployment and retrieve the addresses/ABIs:

```
npm i -g @usecannon/cli
cannon inspect synthetix-omnibus@andromeda --write-deployments ./deployment
cannon synthetix-omnibus@andromeda
```

### For Python Developers

If you are interested in building bots or scripts to trade perps using the **Python SDK**, check out the [playground](https://github.com/Synthetixio/sdk-playground) or [read the docs](../../for-perp-integrators/perps-python-sdk.md).

### For JavaScript/TypeScript Developers

You can retrieve the addresses and ABIs for the Synthetix deployment on Base and call functions using viem as follows:

```javascript
import { createPublicClient, http } from 'viem';
import { base } from 'viem/chains';
import { getCannonContract, traceActions } from '@usecannon/builder';

async function getCollateralConfigurations(){
    // Retrieve deployment data
    const CoreProxy = await getCannonContract({
        package: 'synthetix-omnibus@andromeda',
        chainId: base.id,
        contractName: 'CoreProxy',
    });
    
    // Create a client with the ability to decode errors from the CoreProxy
    const publicClient = createPublicClient({ 
        chain: base,
        transport: http()
      }).extend(traceActions(CoreProxy));

    // Call a smart contract function and log the result
    const result = await publicClient.readContract({
        ...CoreProxy,
        functionName: 'getCollateralConfigurations',
        args: [false],
    })
    console.log(result);
}

getCollateralConfigurations();
```

