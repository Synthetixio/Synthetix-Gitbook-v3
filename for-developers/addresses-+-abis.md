# Addresses + ABIs

See the [synthetix-deployments](https://github.com/synthetixio/synthetix-deployments) GitOps repository for more information.

To download the Addresses + ABIs for Synthetix via the command line, you can run the following command:

```sh
npx @usecannon/cli inspect synthetix-omnibus \
  --write-deployments ./deployments \
  --chain-id <CHAIN_ID> \
  --preset <PRESET>
```
## Mainnet

Chain ID: 1

| System         | Address                                                                                                               | ABI                                               |
| -------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| Synthetix Core | [0xffffffaEff0B96Ea8e4f94b2253f31abdD875847](https://etherscan.io/address/0xffffffaEff0B96Ea8e4f94b2253f31abdD875847) | [View/Download](./abis/1-main-SynthetixCore.json) |
| snxAccount NFT | [0x0E429603D3Cb1DFae4E6F52Add5fE82d96d77Dac](https://etherscan.io/address/0x0E429603D3Cb1DFae4E6F52Add5fE82d96d77Dac) | [View/Download](./abis/1-main-snxAccountNFT.json) |
| snxUSD Token   | [0xb2F30A7C980f052f02563fb518dcc39e6bf38175](https://etherscan.io/address/0xb2F30A7C980f052f02563fb518dcc39e6bf38175) | [View/Download](./abis/1-main-snxUSDToken.json)   |
| Oracle Manager | [0x0aaF300E148378489a8A471DD3e9E53E30cb42e3](https://etherscan.io/address/0x0aaF300E148378489a8A471DD3e9E53E30cb42e3) | [View/Download](./abis/1-main-OracleManager.json) |
| SNX Token      | [0xC011a73ee8576Fb46F5E1c5751cA3B9Fe0af2a6F](https://etherscan.io/address/0xC011a73ee8576Fb46F5E1c5751cA3B9Fe0af2a6F) | _ERC-20 compliant_                                |

## Goerli

Chain ID: 5

| System         | Address                                                                                                                      | ABI                                               |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| Synthetix Core | [0x895CE54BBA4f14FeFbF0624673DC303054De0652](https://goerli.etherscan.io/address/0x895CE54BBA4f14FeFbF0624673DC303054De0652) | [View/Download](./abis/5-main-SynthetixCore.json) |
| snxAccount NFT | [0xf19BdaE737d61A91cd0aeb3E32D0E11f9eF7aE5c](https://goerli.etherscan.io/address/0xf19BdaE737d61A91cd0aeb3E32D0E11f9eF7aE5c) | [View/Download](./abis/5-main-snxAccountNFT.json) |
| snxUSD Token   | [0x50f194b9949759510cE3700f759D64ac429dcC76](https://goerli.etherscan.io/address/0x50f194b9949759510cE3700f759D64ac429dcC76) | [View/Download](./abis/5-main-snxUSDToken.json)   |
| Oracle Manager | [0x21a642c7b2B511f934DDD1250E2335899696ED0e](https://goerli.etherscan.io/address/0x21a642c7b2B511f934DDD1250E2335899696ED0e) | [View/Download](./abis/5-main-OracleManager.json) |
| SNX Token      | [0x51f44ca59b867E005e48FA573Cb8df83FC7f7597](https://goerli.etherscan.io/address/0x51f44ca59b867E005e48FA573Cb8df83FC7f7597) | _ERC-20 compliant_                                |

## Sepolia

Chain ID: 11155111

| System         | Address                                                                                                                       | ABI                                                      |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Synthetix Core | [0x76490713314fCEC173f44e99346F54c6e92a8E42](https://sepolia.etherscan.io/address/0x76490713314fCEC173f44e99346F54c6e92a8E42) | [View/Download](./abis/11155111-main-SynthetixCore.json) |
| snxAccount NFT | [0xe487Ad4291019b33e2230F8E2FB1fb6490325260](https://sepolia.etherscan.io/address/0xe487Ad4291019b33e2230F8E2FB1fb6490325260) | [View/Download](./abis/11155111-main-snxAccountNFT.json) |
| snxUSD Token   | [0x1b791d05E437C78039424749243F5A79E747525e](https://sepolia.etherscan.io/address/0x1b791d05E437C78039424749243F5A79E747525e) | [View/Download](./abis/11155111-main-snxUSDToken.json)   |
| Oracle Manager | [0x12aE0D5CD26f212bFE242DA78139d463019f7a73](https://sepolia.etherscan.io/address/0x12aE0D5CD26f212bFE242DA78139d463019f7a73) | [View/Download](./abis/11155111-main-OracleManager.json) |

## Optimism

Chain ID: 10

| System         | Address                                                                                                                          | ABI                                                |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| Synthetix Core | [0xffffffaEff0B96Ea8e4f94b2253f31abdD875847](https://optimistic.etherscan.io/address/0xffffffaEff0B96Ea8e4f94b2253f31abdD875847) | [View/Download](./abis/10-main-SynthetixCore.json) |
| snxAccount NFT | [0x0E429603D3Cb1DFae4E6F52Add5fE82d96d77Dac](https://optimistic.etherscan.io/address/0x0E429603D3Cb1DFae4E6F52Add5fE82d96d77Dac) | [View/Download](./abis/10-main-snxAccountNFT.json) |
| snxUSD Token   | [0xb2F30A7C980f052f02563fb518dcc39e6bf38175](https://optimistic.etherscan.io/address/0xb2F30A7C980f052f02563fb518dcc39e6bf38175) | [View/Download](./abis/10-main-snxUSDToken.json)   |
| Oracle Manager | [0x0aaF300E148378489a8A471DD3e9E53E30cb42e3](https://optimistic.etherscan.io/address/0x0aaF300E148378489a8A471DD3e9E53E30cb42e3) | [View/Download](./abis/10-main-OracleManager.json) |
| Spot Market    | [0x38908Ee087D7db73A1Bd1ecab9AAb8E8c9C74595](https://optimistic.etherscan.io/address/0x38908Ee087D7db73A1Bd1ecab9AAb8E8c9C74595) | [View/Download](./abis/10-main-SpotMarket.json)    |
| SNX Token      | [0x8700dAec35aF8Ff88c16BdF0418774CB3D7599B4](https://optimistic.etherscan.io/address/0x8700dAec35aF8Ff88c16BdF0418774CB3D7599B4) | _ERC-20 compliant_                                 |

## Optimistic Goerli

Chain ID: 420

| System                   | Address                                                                                                                               | ABI                                                   |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Synthetix Core           | [0x76490713314fCEC173f44e99346F54c6e92a8E42](https://goerli-optimism.etherscan.io/address/0x76490713314fCEC173f44e99346F54c6e92a8E42) | [View/Download](./abis/420-main-SynthetixCore.json)   |
| snxAccount NFT           | [0x1b791d05E437C78039424749243F5A79E747525e](https://goerli-optimism.etherscan.io/address/0x1b791d05E437C78039424749243F5A79E747525e) | [View/Download](./abis/420-main-snxAccountNFT.json)   |
| snxUSD Token             | [0xe487Ad4291019b33e2230F8E2FB1fb6490325260](https://goerli-optimism.etherscan.io/address/0xe487Ad4291019b33e2230F8E2FB1fb6490325260) | [View/Download](./abis/420-main-snxUSDToken.json)     |
| Oracle Manager           | [0x12aE0D5CD26f212bFE242DA78139d463019f7a73](https://goerli-optimism.etherscan.io/address/0x12aE0D5CD26f212bFE242DA78139d463019f7a73) | [View/Download](./abis/420-main-OracleManager.json)   |
| Spot Market              | [0x5FF4b3aacdeC86782d8c757FAa638d8790799E83](https://goerli-optimism.etherscan.io/address/0x5FF4b3aacdeC86782d8c757FAa638d8790799E83) | [View/Download](./abis/420-main-SpotMarket.json)      |
| Perps Market             | [0xf272382cB3BE898A8CdB1A23BE056fA2Fcf4513b](https://goerli-optimism.etherscan.io/address/0xf272382cB3BE898A8CdB1A23BE056fA2Fcf4513b) | [View/Download](./abis/420-main-PerpsMarket.json)     |
| Perps Market Account NFT | [0x01C2f64ABd46AF20950736f3C3e1a9cfc5c36c82](https://goerli-optimism.etherscan.io/address/0x01C2f64ABd46AF20950736f3C3e1a9cfc5c36c82) | [View/Download](./abis/420-main-PerpsAccountNFT.json) |
| SNX Token                | [0x2E5ED97596a8368EB9E44B1f3F25B2E813845303](https://goerli-optimism.etherscan.io/address/0x2E5ED97596a8368EB9E44B1f3F25B2E813845303) | _ERC-20 compliant_                                    |

## Dev on Optimism Goerli

Chain ID: 420

| System                   | Address                                                                                                                               | ABI                                                  |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Synthetix Core           | [0x3f1faD3d8C531A5a3f7ae8d045c37e2075A241A0](https://goerli-optimism.etherscan.io/address/0x3f1faD3d8C531A5a3f7ae8d045c37e2075A241A0) | [View/Download](./abis/420-dev-SynthetixCore.json)   |
| snxAccount NFT           | [0x1daA414B74A7581405e8B17bac5B29F31042B7C6](https://goerli-optimism.etherscan.io/address/0x1daA414B74A7581405e8B17bac5B29F31042B7C6) | [View/Download](./abis/420-dev-snxAccountNFT.json)   |
| snxUSD Token             | [0xE0D30C1f189496388B0f5F1c32e75327135F26b8](https://goerli-optimism.etherscan.io/address/0xE0D30C1f189496388B0f5F1c32e75327135F26b8) | [View/Download](./abis/420-dev-snxUSDToken.json)     |
| Oracle Manager           | [0x47b8f4EC2D0ef7ADfa97927A597d2C73B3A7e81d](https://goerli-optimism.etherscan.io/address/0x47b8f4EC2D0ef7ADfa97927A597d2C73B3A7e81d) | [View/Download](./abis/420-dev-OracleManager.json)   |
| Spot Market              | [0x9bC0DD3436669Ab76C553214B1740CE5E6EbF18e](https://goerli-optimism.etherscan.io/address/0x9bC0DD3436669Ab76C553214B1740CE5E6EbF18e) | [View/Download](./abis/420-dev-SpotMarket.json)      |
| Perps Market             | [0x8EdfbD5c6aB7167cf7dc7E62D9FeAA59720a2e7E](https://goerli-optimism.etherscan.io/address/0x8EdfbD5c6aB7167cf7dc7E62D9FeAA59720a2e7E) | [View/Download](./abis/420-dev-PerpsMarket.json)     |
| Perps Market Account NFT | [0x6fBe7F0f515C2126638aAF60a351a98b27f62925](https://goerli-optimism.etherscan.io/address/0x6fBe7F0f515C2126638aAF60a351a98b27f62925) | [View/Download](./abis/420-dev-PerpsAccountNFT.json) |
| SNX Token                | [0x2E5ED97596a8368EB9E44B1f3F25B2E813845303](https://goerli-optimism.etherscan.io/address/0x2E5ED97596a8368EB9E44B1f3F25B2E813845303) | _ERC-20 compliant_                                   |

## Andromeda on Base

Chain ID: 8453

| System                   | Address                                                                                                               | ABI                                                         |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Synthetix Core           | [0x32C222A9A159782aFD7529c87FA34b96CA72C696](https://basescan.org/address/0x32C222A9A159782aFD7529c87FA34b96CA72C696) | [View/Download](./abis/8453-andromeda-SynthetixCore.json)   |
| snxAccount NFT           | [0x63f4Dd0434BEB5baeCD27F3778a909278d8cf5b8](https://basescan.org/address/0x63f4Dd0434BEB5baeCD27F3778a909278d8cf5b8) | [View/Download](./abis/8453-andromeda-snxAccountNFT.json)   |
| snxUSD Token             | [0x09d51516F38980035153a554c26Df3C6f51a23C3](https://basescan.org/address/0x09d51516F38980035153a554c26Df3C6f51a23C3) | [View/Download](./abis/8453-andromeda-snxUSDToken.json)     |
| Oracle Manager           | [0x3d07CBC5Cb9376A67E76C0655Fe239dDa8E2B264](https://basescan.org/address/0x3d07CBC5Cb9376A67E76C0655Fe239dDa8E2B264) | [View/Download](./abis/8453-andromeda-OracleManager.json)   |
| Spot Market              | [0x18141523403e2595D31b22604AcB8Fc06a4CaA61](https://basescan.org/address/0x18141523403e2595D31b22604AcB8Fc06a4CaA61) | [View/Download](./abis/8453-andromeda-SpotMarket.json)      |
| Perps Market             | [0x0A2AF931eFFd34b81ebcc57E3d3c9B1E1dE1C9Ce](https://basescan.org/address/0x0A2AF931eFFd34b81ebcc57E3d3c9B1E1dE1C9Ce) | [View/Download](./abis/8453-andromeda-PerpsMarket.json)     |
| Perps Market Account NFT | [0xcb68b813210aFa0373F076239Ad4803f8809e8cf](https://basescan.org/address/0xcb68b813210aFa0373F076239Ad4803f8809e8cf) | [View/Download](./abis/8453-andromeda-PerpsAccountNFT.json) |

## Base Goerli

Chain ID: 84531

| System         | Address                                                                                                                      | ABI                                                   |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Synthetix Core | [0x3a0B49f5B93a95453BdaCfc3653E15F982A0187A](https://goerli.basescan.org/address/0x3a0B49f5B93a95453BdaCfc3653E15F982A0187A) | [View/Download](./abis/84531-main-SynthetixCore.json) |
| snxAccount NFT | [0x1146D135842015662c46f284FBDb253EDE225fCE](https://goerli.basescan.org/address/0x1146D135842015662c46f284FBDb253EDE225fCE) | [View/Download](./abis/84531-main-snxAccountNFT.json) |
| snxUSD Token   | [0x2b99243d983d515c611a09Ae673399553452ce18](https://goerli.basescan.org/address/0x2b99243d983d515c611a09Ae673399553452ce18) | [View/Download](./abis/84531-main-snxUSDToken.json)   |
| Oracle Manager | [0xDca879a959f7B2AB73A6AC59bF84F647Eb6f203e](https://goerli.basescan.org/address/0xDca879a959f7B2AB73A6AC59bF84F647Eb6f203e) | [View/Download](./abis/84531-main-OracleManager.json) |
| Spot Market    | [0x897CAf492D824a88d374f742E898f56FbD33d631](https://goerli.basescan.org/address/0x897CAf492D824a88d374f742E898f56FbD33d631) | [View/Download](./abis/84531-main-SpotMarket.json)    |

## Competition on Base Goerli

Chain ID: 84531

| System                         | Address                                                                                                                      | ABI                                                               |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Synthetix Core                 | [0xa53346A1684DAB73EFfd048fA40Fb1fA9327fDe9](https://goerli.basescan.org/address/0xa53346A1684DAB73EFfd048fA40Fb1fA9327fDe9) | [View/Download](./abis/84531-competition-SynthetixCore.json)      |
| snxAccount NFT                 | [0xdD066734028Cb1f07AC8CEdd054BA64Ea05b8461](https://goerli.basescan.org/address/0xdD066734028Cb1f07AC8CEdd054BA64Ea05b8461) | [View/Download](./abis/84531-competition-snxAccountNFT.json)      |
| snxUSD Token                   | [0x579c612E4Bf390f5504DB9f76b6F5759A3172279](https://goerli.basescan.org/address/0x579c612E4Bf390f5504DB9f76b6F5759A3172279) | [View/Download](./abis/84531-competition-snxUSDToken.json)        |
| Oracle Manager                 | [0xbAbfb6e9f914C1EfBBFFAdeE6cd86B23927434C8](https://goerli.basescan.org/address/0xbAbfb6e9f914C1EfBBFFAdeE6cd86B23927434C8) | [View/Download](./abis/84531-competition-OracleManager.json)      |
| Spot Market                    | [0x17633A63083dbd4941891F87Bdf31B896e91e2B9](https://goerli.basescan.org/address/0x17633A63083dbd4941891F87Bdf31B896e91e2B9) | [View/Download](./abis/84531-competition-SpotMarket.json)         |
| Perps Market                   | [0x9863Dae3f4b5F4Ffe3A841a21565d57F2BA10E87](https://goerli.basescan.org/address/0x9863Dae3f4b5F4Ffe3A841a21565d57F2BA10E87) | [View/Download](./abis/84531-competition-PerpsMarket.json)        |
| Perps Market Account NFT       | [0x518F2905b24AE298Ca06C1137b806DD5ACD493b6](https://goerli.basescan.org/address/0x518F2905b24AE298Ca06C1137b806DD5ACD493b6) | [View/Download](./abis/84531-competition-PerpsAccountNFT.json)    |
| Fake Collateral Fake SNX $fSNX | [0xB2b425098CfEe7dc29d7c437f8578EC02c44A5Ed](https://goerli.basescan.org/address/0xB2b425098CfEe7dc29d7c437f8578EC02c44A5Ed) | [View/Download](./abis/84531-competition-FakeCollateralfSNX.json) |

## Andromeda on Base Goerli

Chain ID: 84531

| System                               | Address                                                                                                                      | ABI                                                              |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Synthetix Core                       | [0xF4Df9Dd327Fd30695d478c3c8a2fffAddcdD0d31](https://goerli.basescan.org/address/0xF4Df9Dd327Fd30695d478c3c8a2fffAddcdD0d31) | [View/Download](./abis/84531-andromeda-SynthetixCore.json)       |
| snxAccount NFT                       | [0xa88694d0025dd96194D1B0237fDEbf7D1D34B02F](https://goerli.basescan.org/address/0xa88694d0025dd96194D1B0237fDEbf7D1D34B02F) | [View/Download](./abis/84531-andromeda-snxAccountNFT.json)       |
| snxUSD Token                         | [0xa89163A087fe38022690C313b5D4BBF12574637f](https://goerli.basescan.org/address/0xa89163A087fe38022690C313b5D4BBF12574637f) | [View/Download](./abis/84531-andromeda-snxUSDToken.json)         |
| Oracle Manager                       | [0x439e6cbAaF61C63f406687907022960088801EC0](https://goerli.basescan.org/address/0x439e6cbAaF61C63f406687907022960088801EC0) | [View/Download](./abis/84531-andromeda-OracleManager.json)       |
| Spot Market                          | [0x26f3EcFa0Aa924649cfd4b74C57637e910A983a4](https://goerli.basescan.org/address/0x26f3EcFa0Aa924649cfd4b74C57637e910A983a4) | [View/Download](./abis/84531-andromeda-SpotMarket.json)          |
| Perps Market                         | [0x75c43165ea38cB857C45216a37C5405A7656673c](https://goerli.basescan.org/address/0x75c43165ea38cB857C45216a37C5405A7656673c) | [View/Download](./abis/84531-andromeda-PerpsMarket.json)         |
| Perps Market Account NFT             | [0xD8FD25C1A4d90244699f5Eb1966dB07FbDE9dcFa](https://goerli.basescan.org/address/0xD8FD25C1A4d90244699f5Eb1966dB07FbDE9dcFa) | [View/Download](./abis/84531-andromeda-PerpsAccountNFT.json)     |
| Fake Collateral Fake USD Coin $fUSDC | [0x4967d1987930b2CD183dAB4B6C40B8745DD2eba1](https://goerli.basescan.org/address/0x4967d1987930b2CD183dAB4B6C40B8745DD2eba1) | [View/Download](./abis/84531-andromeda-FakeCollateralfUSDC.json) |

## Polygon Mumbai

Chain ID: 80001

| System         | Address                                                                                                                         | ABI                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Synthetix Core | [0x76490713314fCEC173f44e99346F54c6e92a8E42](https://mumbai.polygonscan.com/address/0x76490713314fCEC173f44e99346F54c6e92a8E42) | [View/Download](./abis/80001-main-SynthetixCore.json) |
| snxAccount NFT | [0xe487Ad4291019b33e2230F8E2FB1fb6490325260](https://mumbai.polygonscan.com/address/0xe487Ad4291019b33e2230F8E2FB1fb6490325260) | [View/Download](./abis/80001-main-snxAccountNFT.json) |
| snxUSD Token   | [0x1b791d05E437C78039424749243F5A79E747525e](https://mumbai.polygonscan.com/address/0x1b791d05E437C78039424749243F5A79E747525e) | [View/Download](./abis/80001-main-snxUSDToken.json)   |
| Oracle Manager | [0x12aE0D5CD26f212bFE242DA78139d463019f7a73](https://mumbai.polygonscan.com/address/0x12aE0D5CD26f212bFE242DA78139d463019f7a73) | [View/Download](./abis/80001-main-OracleManager.json) |

