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
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/CoreProxy.json"><code>CoreProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/CoreProxy.readable.json"><code>CoreProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>AccountProxy</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/AccountProxy.json"><code>AccountProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/AccountProxy.readable.json"><code>AccountProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>USDProxy</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/USDProxy.json"><code>USDProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/USDProxy.readable.json"><code>USDProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>OracleManagerProxy</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/OracleManagerProxy.json"><code>OracleManagerProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/OracleManagerProxy.readable.json"><code>OracleManagerProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>TrustedMulticallForwarder</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/TrustedMulticallForwarder.json"><code>TrustedMulticallForwarder.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/TrustedMulticallForwarder.readable.json"><code>TrustedMulticallForwarder.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>SpotMarketProxy</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/SpotMarketProxy.json"><code>SpotMarketProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/SpotMarketProxy.readable.json"><code>SpotMarketProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>PerpsMarketProxy</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/PerpsMarketProxy.json"><code>PerpsMarketProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/PerpsMarketProxy.readable.json"><code>PerpsMarketProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>PerpsAccountProxy</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/PerpsAccountProxy.json"><code>PerpsAccountProxy.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/PerpsAccountProxy.readable.json"><code>PerpsAccountProxy.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>USDCToken</td>
      <td>undefined</td>
      <td>
        <a href="./42161-arbthetix/USDCToken.json"><code>USDCToken.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/USDCToken.readable.json"><code>USDCToken.readable.json</code></a>
      </td>
    </tr>
    <tr>
      <td>AllErrors</td>
      <td>n/a</td>
      <td>
        <a href="./42161-arbthetix/AllErrors.json"><code>AllErrors.json</code></a>
      </td>
      <td>
        <a href="./42161-arbthetix/AllErrors.readable.json"><code>AllErrors.readable.json</code></a>
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
        <a href="./42161-arbthetix/meta.json"><code>meta.json</code></a>
      </td>
    </tr>
    <tr>
      <td>Extra outputs</td>
      <td>
        <a href="./42161-arbthetix/extras.json"><code>extras.json</code></a>
      </td>
    </tr>
    <tr>
      <td>Cannon state</td>
      <td>
        <a href="./42161-arbthetix/cannon.json"><code>cannon.json</code></a>
      </td>
    </tr>
  </tbody>
</table>

# Collateral `ARB` Arbitrum

Token address: undefined

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
      <td>3</td>
      <td><code>3000000000000000000</code> / <code>0x29a2241af62c0000</code></td>
    </tr>
    <tr>
      <td>liquidationRatioD18</td>
      <td>1.5</td>
      <td><code>1500000000000000000</code> / <code>0x14d1120d7b160000</code></td>
    </tr>
    <tr>
      <td>liquidationRewardD18</td>
      <td>0.01</td>
      <td><code>10000000000000000</code> / <code>0x2386f26fc10000</code></td>
    </tr>
    <tr>
      <td>oracleNodeId</td>
      <td></td>
      <td><code>"0xe2f4515e5eb6c16b3b394e6649460beab2cb0a9ed05347dace0bd7da3824ce83"</code></td>
    </tr>
    <tr>
      <td>minDelegationD18</td>
      <td>0.01</td>
      <td><code>10000000000000000</code> / <code>0x2386f26fc10000</code></td>
    </tr>
  </tbody>
</table>

# Collateral `USDh` DollarWifHat

Token address: undefined

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

# Collateral `WETH` Wrapped Ether

Token address: undefined

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
      <td>3</td>
      <td><code>3000000000000000000</code> / <code>0x29a2241af62c0000</code></td>
    </tr>
    <tr>
      <td>liquidationRatioD18</td>
      <td>1.5</td>
      <td><code>1500000000000000000</code> / <code>0x14d1120d7b160000</code></td>
    </tr>
    <tr>
      <td>liquidationRewardD18</td>
      <td>0.01</td>
      <td><code>10000000000000000</code> / <code>0x2386f26fc10000</code></td>
    </tr>
    <tr>
      <td>oracleNodeId</td>
      <td></td>
      <td><code>"0x8d846863d33e135e0dccd38de7ddf2f78e36f629b527111ceb82c3b4b625a47c"</code></td>
    </tr>
    <tr>
      <td>minDelegationD18</td>
      <td>0.01</td>
      <td><code>10000000000000000</code> / <code>0x2386f26fc10000</code></td>
    </tr>
  </tbody>
</table>

# Perps Market ETH / Ethereum

Perps market ID: <code>100</code>

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
      <td>maxCollateralAmount of snxUSD (market <code>0</code>)</td>
      <td><code>MaxUint256</code></td>
      <td><code>MaxUint256</code> / <code>0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff</code></td>
    </tr>
    <tr>
      <td>maxMarketSize</td>
      <td>5.25 k</td>
      <td><code>5250000000000000000000</code> / <code>0x011c9a62d04ed0c80000</code></td>
    </tr>
    <tr>
      <td>maxOpenInterest</td>
      <td>5.25 k</td>
      <td><code>5250000000000000000000</code> / <code>0x011c9a62d04ed0c80000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>skewScale</td>
      <td>10 m</td>
      <td><code>10000000000000000000000000</code> / <code>0x084595161401484a000000</code></td>
    </tr>
    <tr>
      <td>maxFundingVelocity</td>
      <td>9</td>
      <td><code>9000000000000000000</code> / <code>0x7ce66c50e2840000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>makerFee</td>
      <td>0.0002</td>
      <td><code>200000000000000</code> / <code>0xb5e620f48000</code></td>
    </tr>
    <tr>
      <td>takerFee</td>
      <td>0.0005</td>
      <td><code>500000000000000</code> / <code>0x01c6bf52634000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>initialMarginRatioD18</td>
      <td>8.92</td>
      <td><code>8920000000000000000</code> / <code>0x7bca34bd647c0000</code></td>
    </tr>
    <tr>
      <td>minimumInitialMarginRatioD18</td>
      <td>0.02</td>
      <td><code>20000000000000000</code> / <code>0x470de4df820000</code></td>
    </tr>
    <tr>
      <td>maintenanceMarginScalarD18</td>
      <td>0.28</td>
      <td><code>280000000000000000</code> / <code>0x03e2c284391c0000</code></td>
    </tr>
    <tr>
      <td>flagRewardRatioD18</td>
      <td>0.0003</td>
      <td><code>300000000000000</code> / <code>0x0110d9316ec000</code></td>
    </tr>
    <tr>
      <td>minimumPositionMargin</td>
      <td>50</td>
      <td><code>50000000000000000000</code> / <code>0x02b5e3af16b1880000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>maxLiquidationLimitAccumulationMultiplier</td>
      <td>1.5</td>
      <td><code>1500000000000000000</code> / <code>0x14d1120d7b160000</code></td>
    </tr>
    <tr>
      <td>maxSecondsInLiquidationWindow</td>
      <td>30</td>
      <td><code>30</code> / <code>0x1e</code></td>
    </tr>
    <tr>
      <td>maxLiquidationPd</td>
      <td>0.0005</td>
      <td><code>500000000000000</code> / <code>0x01c6bf52634000</code></td>
    </tr>
    <tr>
      <td>endorsedLiquidator</td>
      <td></td>
      <td>undefined</td>
    </tr>
    <tr>
      <td>minKeeperRewardUsd</td>
      <td>5</td>
      <td><code>5000000000000000000</code> / <code>0x4563918244f40000</code></td>
    </tr>
    <tr>
      <td>minKeeperProfitRatioD18</td>
      <td>0.3</td>
      <td><code>300000000000000000</code> / <code>0x0429d069189e0000</code></td>
    </tr>
    <tr>
      <td>maxKeeperRewardUsd</td>
      <td>100</td>
      <td><code>100000000000000000000</code> / <code>0x056bc75e2d63100000</code></td>
    </tr>
    <tr>
      <td>maxKeeperScalingRatioD18</td>
      <td>0.3</td>
      <td><code>300000000000000000</code> / <code>0x0429d069189e0000</code></td>
    </tr>
  </tbody>
</table>
<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">Settlement strategy parameter</th>
      <th width="100">Value</th>
      <th width="800">Raw value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>strategyId</td>
      <td>0</td>
      <td><code>0</code></td>
    </tr>
    <tr>
      <td>strategyType</td>
      <td>PYTH</td>
      <td><code>0</code></td>
    </tr>
    <tr>
      <td>settlementDelay</td>
      <td>2</td>
      <td><code>2</code> / <code>0x02</code></td>
    </tr>
    <tr>
      <td>settlementWindowDuration</td>
      <td>60</td>
      <td><code>60</code> / <code>0x3c</code></td>
    </tr>
    <tr>
      <td>priceVerificationContract</td>
      <td></td>
      <td>undefined</td>
    </tr>
    <tr>
      <td>feedId</td>
      <td></td>
      <td><code>"0xff61491a931112ddf1bd8147cd1b641375f79f5825126d665480874634fd0ace"</code></td>
    </tr>
    <tr>
      <td>settlementReward</td>
      <td>1</td>
      <td><code>1000000000000000000</code> / <code>0x0de0b6b3a7640000</code></td>
    </tr>
    <tr>
      <td>disabled</td>
      <td>✅ Enabled</td>
      <td><code>false</code></td>
    </tr>
    <tr>
      <td>commitmentPriceDelay</td>
      <td>2</td>
      <td><code>2</code> / <code>0x02</code></td>
    </tr>
  </tbody>
</table>

# Perps Market BTC / Bitcoin

Perps market ID: <code>200</code>

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
      <td>maxCollateralAmount of snxUSD (market <code>0</code>)</td>
      <td><code>MaxUint256</code></td>
      <td><code>MaxUint256</code> / <code>0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff</code></td>
    </tr>
    <tr>
      <td>maxMarketSize</td>
      <td>300</td>
      <td><code>300000000000000000000</code> / <code>0x1043561a8829300000</code></td>
    </tr>
    <tr>
      <td>maxOpenInterest</td>
      <td>300</td>
      <td><code>300000000000000000000</code> / <code>0x1043561a8829300000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>skewScale</td>
      <td>100 k</td>
      <td><code>100000000000000000000000</code> / <code>0x152d02c7e14af6800000</code></td>
    </tr>
    <tr>
      <td>maxFundingVelocity</td>
      <td>9</td>
      <td><code>9000000000000000000</code> / <code>0x7ce66c50e2840000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>makerFee</td>
      <td>0.0002</td>
      <td><code>200000000000000</code> / <code>0xb5e620f48000</code></td>
    </tr>
    <tr>
      <td>takerFee</td>
      <td>0.0005</td>
      <td><code>500000000000000</code> / <code>0x01c6bf52634000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>initialMarginRatioD18</td>
      <td>13.35</td>
      <td><code>13350000000000000000</code> / <code>0xb944ba44c7770000</code></td>
    </tr>
    <tr>
      <td>minimumInitialMarginRatioD18</td>
      <td>0.02</td>
      <td><code>20000000000000000</code> / <code>0x470de4df820000</code></td>
    </tr>
    <tr>
      <td>maintenanceMarginScalarD18</td>
      <td>0.28</td>
      <td><code>280000000000000000</code> / <code>0x03e2c284391c0000</code></td>
    </tr>
    <tr>
      <td>flagRewardRatioD18</td>
      <td>0.0003</td>
      <td><code>300000000000000</code> / <code>0x0110d9316ec000</code></td>
    </tr>
    <tr>
      <td>minimumPositionMargin</td>
      <td>50</td>
      <td><code>50000000000000000000</code> / <code>0x02b5e3af16b1880000</code></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>maxLiquidationLimitAccumulationMultiplier</td>
      <td>1.5</td>
      <td><code>1500000000000000000</code> / <code>0x14d1120d7b160000</code></td>
    </tr>
    <tr>
      <td>maxSecondsInLiquidationWindow</td>
      <td>30</td>
      <td><code>30</code> / <code>0x1e</code></td>
    </tr>
    <tr>
      <td>maxLiquidationPd</td>
      <td>0.0005</td>
      <td><code>500000000000000</code> / <code>0x01c6bf52634000</code></td>
    </tr>
    <tr>
      <td>endorsedLiquidator</td>
      <td></td>
      <td>undefined</td>
    </tr>
    <tr>
      <td>minKeeperRewardUsd</td>
      <td>5</td>
      <td><code>5000000000000000000</code> / <code>0x4563918244f40000</code></td>
    </tr>
    <tr>
      <td>minKeeperProfitRatioD18</td>
      <td>0.3</td>
      <td><code>300000000000000000</code> / <code>0x0429d069189e0000</code></td>
    </tr>
    <tr>
      <td>maxKeeperRewardUsd</td>
      <td>100</td>
      <td><code>100000000000000000000</code> / <code>0x056bc75e2d63100000</code></td>
    </tr>
    <tr>
      <td>maxKeeperScalingRatioD18</td>
      <td>0.3</td>
      <td><code>300000000000000000</code> / <code>0x0429d069189e0000</code></td>
    </tr>
  </tbody>
</table>
<table data-full-width="true">
  <thead>
    <tr>
      <th width="400">Settlement strategy parameter</th>
      <th width="100">Value</th>
      <th width="800">Raw value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>strategyId</td>
      <td>0</td>
      <td><code>0</code></td>
    </tr>
    <tr>
      <td>strategyType</td>
      <td>PYTH</td>
      <td><code>0</code></td>
    </tr>
    <tr>
      <td>settlementDelay</td>
      <td>2</td>
      <td><code>2</code> / <code>0x02</code></td>
    </tr>
    <tr>
      <td>settlementWindowDuration</td>
      <td>60</td>
      <td><code>60</code> / <code>0x3c</code></td>
    </tr>
    <tr>
      <td>priceVerificationContract</td>
      <td></td>
      <td>undefined</td>
    </tr>
    <tr>
      <td>feedId</td>
      <td></td>
      <td><code>"0xe62df6c8b4a85fe1a67db44dc12de5db330f7ac66b72dc658afedf0f4a415b43"</code></td>
    </tr>
    <tr>
      <td>settlementReward</td>
      <td>1</td>
      <td><code>1000000000000000000</code> / <code>0x0de0b6b3a7640000</code></td>
    </tr>
    <tr>
      <td>disabled</td>
      <td>✅ Enabled</td>
      <td><code>false</code></td>
    </tr>
    <tr>
      <td>commitmentPriceDelay</td>
      <td>2</td>
      <td><code>2</code> / <code>0x02</code></td>
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
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>AccountProxy</td>
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>USDProxy</td>
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>OracleManagerProxy</td>
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>TrustedMulticallForwarder</td>
      <td>n/a</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>SpotMarketProxy</td>
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>PerpsMarketProxy</td>
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>PerpsAccountProxy</td>
      <td>undefined</td>
      <td>n/a</td>
    </tr>
    <tr>
      <td>USDCToken</td>
      <td>undefined</td>
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
      <td>undefined</td>
      <td>n/a</td>
    </tr>
  </tbody>
</table>

