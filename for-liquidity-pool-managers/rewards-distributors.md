# Rewards Distributors

Pool owners may register and remove **rewards distributors** from the vaults in their pools. Rewards distributors are smart contracts which can distribute rewards among all of the liquidity positions in a specified vault (instantaneously or over time) and allow these rewards to be collected.

## Creating a Rewards Distributor[​](https://snx-v3-docs.vercel.app/pools-markets/rewards#rewards-distributor) <a href="#rewards-distributor" id="rewards-distributor"></a>

Reward distributors must conform to the `IRewardDistributor` interface. This includes a `payout` function which should transfer `amount` of rewards to the `sender` address:

```
function payout(uint128 accountId, uint128 poolId, address collateralType, address sender, uint amount) external returns (bool);
```

{% hint style="info" %}
**For security reasons, the payout function should always revert unless `msg.sender` is equal to Synthetix Core address.**
{% endhint %}

A pool owner can then connect a rewards distributor to a vault with the `registerRewardsDistributor` function. (Note that due to gas considerations, no more than 10 rewards distributors may be connected to a given vault at time.) To remove a rewards distributor, the pool owner can call the `removeRewardsDistributor` function.

### Rewards Distributor Example

Below is an example Rewards Distributor contract that can be used to develop your own.

{% @github-files/github-code-block %}

Below is an example transaction that:

1. Registers a Rewards Distributor contract
2. to poolId 69
3. with SNX (on Optimism Goerli)

{% embed url="https://goerli-optimism.etherscan.io/tx/0xcbc66ab9276aa828149cabbe40c7eb88408d9963664ac37f9f69c4f228a7811e" %}

## Distributing Rewards <a href="#rewards-manager" id="rewards-manager"></a>

A registered rewards distributor can call the `distributeRewards` function. The `poolId` and `collateralType` parameters identify the relevant vault. `amount` indicates the total amount of tokens to be distributed starting at the `start` timestamp over `duration` seconds. Note that `duration` may be set to 0, such that the rewards are distributed instantaneously based on the pro-rata distribution at `start`. A rewards distributor can call the `distributeRewards` function multiple times, adding to the rewards already distributed to those participating in the vault.

Anyone can static call the `claimRewards` function to see what an account ID can claim from a distributor registered to a specified vault, accounting for amounts previously claimed. Then, an address that owns (or has relevant permissions on) that account can call the `claimRewards` function. This, in turn, calls the `payout` function on the rewards distributor with the appropriate amount.
