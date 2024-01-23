# Contracts

<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">System</th>
      <th width="500">Address</th>
      <th width="500">ABI</th>
      <th width="500">Readable ABI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CoreProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x895CE54BBA4f14FeFbF0624673DC303054De0652"><code>0x895CE54BBA4f14FeFbF0624673DC303054De0652</code></a>
      </td>
      <td>
        <a href="./5-main/CoreProxy.json"><code>CoreProxy.json</code></a>
      </td>
      <td>
        <a href="./5-main/CoreProxy.readable.json"><code>CoreProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>AccountProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0xf19BdaE737d61A91cd0aeb3E32D0E11f9eF7aE5c"><code>0xf19BdaE737d61A91cd0aeb3E32D0E11f9eF7aE5c</code></a>
      </td>
      <td>
        <a href="./5-main/AccountProxy.json"><code>AccountProxy.json</code></a>
      </td>
      <td>
        <a href="./5-main/AccountProxy.readable.json"><code>AccountProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>USDProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x50f194b9949759510cE3700f759D64ac429dcC76"><code>0x50f194b9949759510cE3700f759D64ac429dcC76</code></a>
      </td>
      <td>
        <a href="./5-main/USDProxy.json"><code>USDProxy.json</code></a>
      </td>
      <td>
        <a href="./5-main/USDProxy.readable.json"><code>USDProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>OracleManagerProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x21a642c7b2B511f934DDD1250E2335899696ED0e"><code>0x21a642c7b2B511f934DDD1250E2335899696ED0e</code></a>
      </td>
      <td>
        <a href="./5-main/OracleManagerProxy.json"><code>OracleManagerProxy.json</code></a>
      </td>
      <td>
        <a href="./5-main/OracleManagerProxy.readable.json"><code>OracleManagerProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>SNXToken</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x51f44ca59b867E005e48FA573Cb8df83FC7f7597"><code>0x51f44ca59b867E005e48FA573Cb8df83FC7f7597</code></a>
      </td>
      <td>
        <a href="./5-main/SNXToken.json"><code>SNXToken.json</code></a>
      </td>
      <td>
        <a href="./5-main/SNXToken.readable.json"><code>SNXToken.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>AllErrors</td>
      <td>n/a</td>
      <td>
        <a href="./5-main/AllErrors.json"><code>AllErrors.json</code></a>
      </td>
      <td>
        <a href="./5-main/AllErrors.readable.json"><code>AllErrors.readable.json</code></a>
      </td>
    </tr>
  </tbody>
</table>
<table data-full-width="true">
  <thead>
    <tr>
      <th width="400"></th>
      <th width="500">JSON</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Deployment meta</td>
      <td>
        <a href="./5-main/meta.json"><code>meta.json</code></a>
      </td>
    </tr>
    <tr>
      <td>Extra outputs</td>
      <td>
        <a href="./5-main/extras.json"><code>extras.json</code></a>
      </td>
    </tr>
    <tr>
      <td>Cannon state</td>
      <td>
        <a href="./5-main/cannon.json"><code>cannon.json</code></a>
      </td>
    </tr>
  </tbody>
</table>

# Collateral `SNX` Synthetix Network Token

Token address: <a href="https://goerli.etherscan.io/address/0x51f44ca59b867E005e48FA573Cb8df83FC7f7597"><code>0x51f44ca59b867E005e48FA573Cb8df83FC7f7597</code></a>

<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">Parameter name</th>
      <th width="100">Value</th>
      <th width="800">Raw value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>depositingEnabled</td>
      <td>✅ Enabled</td>
      <td><code>true</code></td>
    </tr>
    <tr>
      <td>decimals</td>
      <td>18</td>
      <td><code>18</code></td>
    </tr>
    <tr>
      <td>issuanceRatioD18</td>
      <td>4</td>
      <td><code>4000000000000000000</code> / <code>0x3782dace9d900000</code></td>
    </tr>
    <tr>
      <td>liquidationRatioD18</td>
      <td>1.5</td>
      <td><code>1500000000000000000</code> / <code>0x14d1120d7b160000</code></td>
    </tr>
    <tr>
      <td>liquidationRewardD18</td>
      <td>10</td>
      <td><code>10000000000000000000</code> / <code>0x8ac7230489e80000</code></td>
    </tr>
    <tr>
      <td>oracleNodeId</td>
      <td></td>
      <td><code>"0xaa597fc5dc4bb2a987bcc268e5a78848bf89076a5eb82caee451718e756af311"</code></td>
    </tr>
    <tr>
      <td>minDelegationD18</td>
      <td>10</td>
      <td><code>10000000000000000000</code> / <code>0x8ac7230489e80000</code></td>
    </tr>
  </tbody>
</table>

# Collateral `snxUSD` Synthetic USD Token v3

Token address: <a href="https://goerli.etherscan.io/address/0x50f194b9949759510cE3700f759D64ac429dcC76"><code>0x50f194b9949759510cE3700f759D64ac429dcC76</code></a>

<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">Parameter name</th>
      <th width="100">Value</th>
      <th width="800">Raw value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>depositingEnabled</td>
      <td>✅ Enabled</td>
      <td><code>true</code></td>
    </tr>
    <tr>
      <td>decimals</td>
      <td>18</td>
      <td><code>18</code></td>
    </tr>
    <tr>
      <td>issuanceRatioD18</td>
      <td>10</td>
      <td><code>10000000000000000000</code> / <code>0x8ac7230489e80000</code></td>
    </tr>
    <tr>
      <td>liquidationRatioD18</td>
      <td>10</td>
      <td><code>10000000000000000000</code> / <code>0x8ac7230489e80000</code></td>
    </tr>
    <tr>
      <td>liquidationRewardD18</td>
      <td>0</td>
      <td><code>0</code> / <code>0x00</code></td>
    </tr>
    <tr>
      <td>oracleNodeId</td>
      <td></td>
      <td><code>"0x066ef68c9d9ca51eee861aeb5bce51a12e61f06f10bf62243c563671ae3a9733"</code></td>
    </tr>
    <tr>
      <td>minDelegationD18</td>
      <td><code>MaxUint256</code></td>
      <td><code>MaxUint256</code> / <code>0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff</code></td>
    </tr>
  </tbody>
</table>

# Owners

<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">System</th>
      <th width="500">Owner</th>
      <th width="500">Nominated owner</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CoreProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x40BFB5479A0E2529865c65ffEb392E6EE032fa2D"><code>0x40BFB5479A0E2529865c65ffEb392E6EE032fa2D</code></a>
      </td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>AccountProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x895CE54BBA4f14FeFbF0624673DC303054De0652"><code>0x895CE54BBA4f14FeFbF0624673DC303054De0652</code></a>
      </td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>USDProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x895CE54BBA4f14FeFbF0624673DC303054De0652"><code>0x895CE54BBA4f14FeFbF0624673DC303054De0652</code></a>
      </td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>OracleManagerProxy</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9"><code>0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9</code></a>
      </td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>SNXToken</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9"><code>0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9</code></a>
      </td>
      <td>n/a</td>
    </tr>
  </tbody>
</table>

<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">Pool</th>
      <th width="500">Owner</th>
      <th width="500">Nominated owner</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>1</code> Spartan Council Pool <i>* preferred</i></td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9"><code>0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9</code></a>
      </td>
      <td>n/a</td>
    </tr>
    <tr>
      <td><code>69</code> Passive SNX Pool</td>
      <td>
        <a href="https://goerli.etherscan.io/address/0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9"><code>0x48914229deDd5A9922f44441ffCCfC2Cb7856Ee9</code></a>
      </td>
      <td>n/a</td>
    </tr>
  </tbody>
</table>

