# Creating Accounts

To deposit collateral in the Synthetix protocol, users must first create an account. Accounts are represented as ERC-721 compliant tokens (NFTs). They can be transferred between wallets using any app with general support for NFTs.

**Anyone can mint an account token by calling the `createAccount()` function on the** [**Synthetix Core address**](../for-developers/addresses-+-abis.md)**.** Other than gas fees, there is no cost to mint an account token. When creating an account, can optionally pass in the `requestedAccountId` parameter for an ID with a value below `type(uint128).max / 2` that isn't already in use.

The account token's ERC-721 compliant interface is exposed at the [Account Token address](../for-developers/addresses-+-abis.md). All other logic pertaining to accounts, including the `createAccount` function, is available at the Synthetix Core address.

### Account Permissions

Accounts can delegate permissions to addresses other than the owner. This is useful to improve security (e.g. by owning the account with a hardware wallet and using a software wallet with reduced permissions for more common activities, like claiming rewards) or for collaboratively managing liquidity positions.

* `ADMIN` - Admins have permission to do everything that the account owner can (including granting and revoking permissions for other addresses) except for transferring account ownership.
* `WITHDRAW` - Addresses with this permission may call the `withdraw` function) on behalf of the account.
* `REWARDS` - Addresses with this permission may call the `claimRewards` function on behalf of the account.
* `MINT` - Addresses with this permission may call the `mintUSD` function on behalf of the account.
* `DELEGATE` - Addresses with this permission may call the `delegateCollateral` function on behalf of the account.

**Note that there are no permissions for `DEPOSIT` or `BURN`**. These are permissionless operations, which can be performed by anyone on any liquidity position because they improve the position's health.

Permissions are handled by the [Account Module](https://github.com/Synthetixio/synthetix-v3/blob/main/protocol/synthetix/contracts/modules/account/AccountTokenModule.sol), exposed at the [Synthetix Core address](../for-developers/addresses-+-abis.md). Each permission listed above should be encoded/decoded as `bytes32` when making requests.

The `hasPermission` function returns whether an address has a particular permission for a given account. The `getAccountPermissions` function returns all of the addresses and their respective permissions for a given account. The account owner (and addresses with the `ADMIN` permission) may call the `grantPermission` and `revokePermission` functions. An address may also revoke its own permissions with the `renouncePermission` function.
