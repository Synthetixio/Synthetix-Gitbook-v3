# Smart Contracts

## Synthetix Core

### Account Module

#### getAccountPermissions

  ```solidity
  function getAccountPermissions(uint128 accountId) external view returns (struct IAccountModule.AccountPermissions[] accountPerms)
  ```

  Returns an array of `AccountPermission` for the provided `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose permissions are being retrieved.

**Returns**
* `accountPerms` (*struct IAccountModule.AccountPermissions[]*) - An array of AccountPermission objects describing the permissions granted to the account.
#### createAccount

  ```solidity
  function createAccount(uint128 requestedAccountId) external
  ```

  Mints an account token with id `requestedAccountId` to `ERC2771Context._msgSender()`.

**Parameters**
* `requestedAccountId` (*uint128*) - The id requested for the account being created. Reverts if id already exists. Requirements: - `requestedAccountId` must not already be minted. - `requestedAccountId` must be less than type(uint128).max / 2 Emits a {AccountCreated} event.

#### createAccount

  ```solidity
  function createAccount() external returns (uint128 accountId)
  ```

  Mints an account token with an available id to `ERC2771Context._msgSender()`.

Emits a {AccountCreated} event.

#### notifyAccountTransfer

  ```solidity
  function notifyAccountTransfer(address to, uint128 accountId) external
  ```

  Called by AccountTokenModule to notify the system when the account token is transferred.

  Resets user permissions and assigns ownership of the account token to the new holder.

**Parameters**
* `to` (*address*) - The new holder of the account NFT.
* `accountId` (*uint128*) - The id of the account that was just transferred. Requirements: - `ERC2771Context._msgSender()` must be the account token.

#### grantPermission

  ```solidity
  function grantPermission(uint128 accountId, bytes32 permission, address user) external
  ```

  Grants `permission` to `user` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that granted the permission.
* `permission` (*bytes32*) - The bytes32 identifier of the permission.
* `user` (*address*) - The target address that received the permission. Requirements: - `ERC2771Context._msgSender()` must own the account token with ID `accountId` or have the "admin" permission. Emits a {PermissionGranted} event.

#### revokePermission

  ```solidity
  function revokePermission(uint128 accountId, bytes32 permission, address user) external
  ```

  Revokes `permission` from `user` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that revoked the permission.
* `permission` (*bytes32*) - The bytes32 identifier of the permission.
* `user` (*address*) - The target address that no longer has the permission. Requirements: - `ERC2771Context._msgSender()` must own the account token with ID `accountId` or have the "admin" permission. Emits a {PermissionRevoked} event.

#### renouncePermission

  ```solidity
  function renouncePermission(uint128 accountId, bytes32 permission) external
  ```

  Revokes `permission` from `ERC2771Context._msgSender()` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose permission was renounced.
* `permission` (*bytes32*) - The bytes32 identifier of the permission. Emits a {PermissionRevoked} event.

#### hasPermission

  ```solidity
  function hasPermission(uint128 accountId, bytes32 permission, address user) external view returns (bool hasPermission)
  ```

  Returns `true` if `user` has been granted `permission` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose permission is being queried.
* `permission` (*bytes32*) - The bytes32 identifier of the permission.
* `user` (*address*) - The target address whose permission is being queried.

**Returns**
* `hasPermission` (*bool*) - A boolean with the response of the query.
#### isAuthorized

  ```solidity
  function isAuthorized(uint128 accountId, bytes32 permission, address target) external view returns (bool isAuthorized)
  ```

  Returns `true` if `target` is authorized to `permission` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose permission is being queried.
* `permission` (*bytes32*) - The bytes32 identifier of the permission.
* `target` (*address*) - The target address whose permission is being queried.

**Returns**
* `isAuthorized` (*bool*) - A boolean with the response of the query.
#### getAccountTokenAddress

  ```solidity
  function getAccountTokenAddress() external view returns (address accountNftToken)
  ```

  Returns the address for the account token used by the module.

**Returns**
* `accountNftToken` (*address*) - The address of the account token.
#### getAccountOwner

  ```solidity
  function getAccountOwner(uint128 accountId) external view returns (address owner)
  ```

  Returns the address that owns a given account, as recorded by the system.

**Parameters**
* `accountId` (*uint128*) - The account id whose owner is being retrieved.

**Returns**
* `owner` (*address*) - The owner of the given account id.
#### getAccountLastInteraction

  ```solidity
  function getAccountLastInteraction(uint128 accountId) external view returns (uint256 timestamp)
  ```

  Returns the last unix timestamp that a permissioned action was taken with this account

**Parameters**
* `accountId` (*uint128*) - The account id to check

**Returns**
* `timestamp` (*uint256*) - The unix timestamp of the last time a permissioned action occured with the account

#### AccountCreated

  ```solidity
  event AccountCreated(uint128 accountId, address owner)
  ```

  Emitted when an account token with id `accountId` is minted to `sender`.

**Parameters**
* `accountId` (*uint128*) - The id of the account.
* `owner` (*address*) - The address that owns the created account.

#### PermissionGranted

  ```solidity
  event PermissionGranted(uint128 accountId, bytes32 permission, address user, address sender)
  ```

  Emitted when `user` is granted `permission` by `sender` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that granted the permission.
* `permission` (*bytes32*) - The bytes32 identifier of the permission.
* `user` (*address*) - The target address to whom the permission was granted.
* `sender` (*address*) - The Address that granted the permission.

#### PermissionRevoked

  ```solidity
  event PermissionRevoked(uint128 accountId, bytes32 permission, address user, address sender)
  ```

  Emitted when `user` has `permission` renounced or revoked by `sender` for account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that has had the permission revoked.
* `permission` (*bytes32*) - The bytes32 identifier of the permission.
* `user` (*address*) - The target address for which the permission was revoked.
* `sender` (*address*) - The address that revoked the permission.

### Account Token Module

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns whether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, string uri) external
  ```

  Initializes the token with name, symbol, and uri.

#### mint

  ```solidity
  function mint(address to, uint256 tokenId) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `tokenId` (*uint256*) - The ID of the newly minted token

#### safeMint

  ```solidity
  function safeMint(address to, uint256 tokenId, bytes data) external
  ```

  Allows the owner to mint tokens. Verifies that the receiver can receive the token

**Parameters**
* `to` (*address*) - The address to receive the newly minted token.
* `tokenId` (*uint256*) - The ID of the newly minted token
* `data` (*bytes*) - any data which should be sent to the receiver

#### burn

  ```solidity
  function burn(uint256 tokenId) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `tokenId` (*uint256*) - The token to burn

#### setAllowance

  ```solidity
  function setAllowance(uint256 tokenId, address spender) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `tokenId` (*uint256*) - The token which should be allowed to spender
* `spender` (*address*) - The address that is given allowance.

#### setBaseTokenURI

  ```solidity
  function setBaseTokenURI(string uri) external
  ```

  Allows the owner to update the base token URI.

**Parameters**
* `uri` (*string*) - The new base token uri

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total amount of tokens stored by the contract.

#### tokenOfOwnerByIndex

  ```solidity
  function tokenOfOwnerByIndex(address owner, uint256 index) external view returns (uint256)
  ```

  Returns a token ID owned by `owner` at a given `index` of its token list.
Use along with {balanceOf} to enumerate all of ``owner``'s tokens.

Requirements:
- `owner` must be a valid address
- `index` must be less than the balance of the tokens for the owner

#### tokenByIndex

  ```solidity
  function tokenByIndex(uint256 index) external view returns (uint256)
  ```

  Returns a token ID at a given `index` of all the tokens stored by the contract.
Use along with {totalSupply} to enumerate all tokens.

Requirements:
- `index` must be less than the total supply of the tokens

#### balanceOf

  ```solidity
  function balanceOf(address holder) external view returns (uint256 balance)
  ```

  Returns the number of tokens in ``owner``'s account.

Requirements:

- `holder` must be a valid address

#### ownerOf

  ```solidity
  function ownerOf(uint256 tokenId) external view returns (address owner)
  ```

  Returns the owner of the `tokenId` token.

Requirements:

- `tokenId` must exist.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId, bytes data) external
  ```

  Safely transfers `tokenId` token from `from` to `to`.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId) external
  ```

  Safely transfers `tokenId` token from `from` to `to`, checking first that contract recipients
are aware of the ERC721 protocol to prevent tokens from being forever locked.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must have been allowed to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 tokenId) external
  ```

  Transfers `tokenId` token from `from` to `to`.

WARNING: Usage of this method is discouraged, use {safeTransferFrom} whenever possible.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.

Emits a {Transfer} event.

#### approve

  ```solidity
  function approve(address to, uint256 tokenId) external
  ```

  Gives permission to `to` to transfer `tokenId` token to another account.
The approval is cleared when the token is transferred.

Only a single account can be approved at a time, so approving the zero address clears previous approvals.

Requirements:

- The caller must own the token or be an approved operator.
- `tokenId` must exist.

Emits an {Approval} event.

#### setApprovalForAll

  ```solidity
  function setApprovalForAll(address operator, bool approved) external
  ```

  Approve or remove `operator` as an operator for the caller.
Operators can call {transferFrom} or {safeTransferFrom} for any token owned by the caller.

Requirements:

- The `operator` cannot be the caller.

Emits an {ApprovalForAll} event.

#### getApproved

  ```solidity
  function getApproved(uint256 tokenId) external view returns (address operator)
  ```

  Returns the account approved for `tokenId` token.

Requirements:

- `tokenId` must exist.

#### isApprovedForAll

  ```solidity
  function isApprovedForAll(address owner, address operator) external view returns (bool)
  ```

  Returns if the `operator` is allowed to manage all of the assets of `owner`.

See {setApprovalForAll}

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 tokenId)
  ```

  Emitted when `tokenId` token is transferred from `from` to `to`.

#### Approval

  ```solidity
  event Approval(address owner, address approved, uint256 tokenId)
  ```

  Emitted when `owner` enables `approved` to manage the `tokenId` token.

#### ApprovalForAll

  ```solidity
  event ApprovalForAll(address owner, address operator, bool approved)
  ```

  Emitted when `owner` enables or disables (`approved`) `operator` to manage all of its assets.

### Associate Debt Module

#### associateDebt

  ```solidity
  function associateDebt(uint128 marketId, uint128 poolId, address collateralType, uint128 accountId, uint256 amount) external returns (int256 debtAmount)
  ```

  Allows a market to associate debt with a specific position.
The specified debt will be removed from all vault participants pro-rata. After removing the debt, the amount will
be allocated directly to the specified account.
**NOTE**: if the specified account is an existing staker on the vault, their position will be included in the pro-rata
reduction. Ex: if there are 10 users staking 10 USD of debt on a pool, and associate debt is called with 10 USD on one of those users,
their debt after the operation is complete will be 19 USD. This might seem unusual, but its actually ideal behavior when
your market has incurred some new debt, and it wants to allocate this amount directly to a specific user. In this case, the user's
debt balance would increase pro rata, but then get decreased pro-rata, and then increased to the full amount on their account. All
other accounts would be left with no change to their debt, however.

**Parameters**
* `marketId` (*uint128*) - The id of the market to which debt was associated.
* `poolId` (*uint128*) - The id of the pool associated to the target market.
* `collateralType` (*address*) - The address of the collateral type that acts as collateral in the corresponding pool.
* `accountId` (*uint128*) - The id of the account whose debt is being associated.
* `amount` (*uint256*) - The amount of debt being associated with the specified account, denominated with 18 decimals of precision.

**Returns**
* `debtAmount` (*int256*) - The updated debt of the position, denominated with 18 decimals of precision.

#### DebtAssociated

  ```solidity
  event DebtAssociated(uint128 marketId, uint128 poolId, address collateralType, uint128 accountId, uint256 amount, int256 updatedDebt)
  ```

  Emitted when `associateDebt` is called.

**Parameters**
* `marketId` (*uint128*) - The id of the market to which debt was associated.
* `poolId` (*uint128*) - The id of the pool associated to the target market.
* `collateralType` (*address*) - The address of the collateral type that acts as collateral in the corresponding pool.
* `accountId` (*uint128*) - The id of the account whose debt is being associated.
* `amount` (*uint256*) - The amount of debt being associated with the specified account, denominated with 18 decimals of precision.
* `updatedDebt` (*int256*) - The total updated debt of the account, denominated with 18 decimals of precision

### Collateral Configuration Module

#### configureCollateral

  ```solidity
  function configureCollateral(struct CollateralConfiguration.Data config) external
  ```

  Creates or updates the configuration for the given `collateralType`.

**Parameters**
* `config` (*struct CollateralConfiguration.Data*) - The CollateralConfiguration object describing the new configuration. Requirements: - `ERC2771Context._msgSender()` must be the owner of the system. Emits a {CollateralConfigured} event.

#### getCollateralConfigurations

  ```solidity
  function getCollateralConfigurations(bool hideDisabled) external view returns (struct CollateralConfiguration.Data[] collaterals)
  ```

  Returns a list of detailed information pertaining to all collateral types registered in the system.

  Optionally returns only those that are currently enabled.

**Parameters**
* `hideDisabled` (*bool*) - Wether to hide disabled collaterals or just return the full list of collaterals in the system.

**Returns**
* `collaterals` (*struct CollateralConfiguration.Data[]*) - The list of collateral configuration objects set in the system.
#### getCollateralConfiguration

  ```solidity
  function getCollateralConfiguration(address collateralType) external view returns (struct CollateralConfiguration.Data collateral)
  ```

  Returns detailed information pertaining the specified collateral type.

**Parameters**
* `collateralType` (*address*) - The address for the collateral whose configuration is being queried.

**Returns**
* `collateral` (*struct CollateralConfiguration.Data*) - The configuration object describing the given collateral.
#### getCollateralPrice

  ```solidity
  function getCollateralPrice(address collateralType) external view returns (uint256 priceD18)
  ```

  Returns the current value of a specified collateral type.

**Parameters**
* `collateralType` (*address*) - The address for the collateral whose price is being queried.

**Returns**
* `priceD18` (*uint256*) - The price of the given collateral, denominated with 18 decimals of precision.

#### CollateralConfigured

  ```solidity
  event CollateralConfigured(address collateralType, struct CollateralConfiguration.Data config)
  ```

  Emitted when a collateral type’s configuration is created or updated.

**Parameters**
* `collateralType` (*address*) - The address of the collateral type that was just configured.
* `config` (*struct CollateralConfiguration.Data*) - The object with the newly configured details.

### Collateral Module

#### deposit

  ```solidity
  function deposit(uint128 accountId, address collateralType, uint256 tokenAmount) external
  ```

  Deposits `tokenAmount` of collateral of type `collateralType` into account `accountId`.

  Anyone can deposit into anyone's active account without restriction.
Depositing to account will automatically clear expired locks on a user's account. If there are an
extremely large number of locks to process, it may not be possible to call `deposit` due to the block gas
limit. In cases such as these, `cleanExpiredLocks` must be called first to clear any outstanding locks.

**Parameters**
* `accountId` (*uint128*) - The id of the account that is making the deposit.
* `collateralType` (*address*) - The address of the token to be deposited.
* `tokenAmount` (*uint256*) - The amount being deposited, denominated in the token's native decimal representation. Emits a {Deposited} event.

#### withdraw

  ```solidity
  function withdraw(uint128 accountId, address collateralType, uint256 tokenAmount) external
  ```

  Withdraws `tokenAmount` of collateral of type `collateralType` from account `accountId`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that is making the withdrawal.
* `collateralType` (*address*) - The address of the token to be withdrawn.
* `tokenAmount` (*uint256*) - The amount being withdrawn, denominated in the token's native decimal representation. Requirements: - `ERC2771Context._msgSender()` must be the owner of the account, have the `ADMIN` permission, or have the `WITHDRAW` permission. Emits a {Withdrawn} event.

#### getAccountCollateral

  ```solidity
  function getAccountCollateral(uint128 accountId, address collateralType) external view returns (uint256 totalDeposited, uint256 totalAssigned, uint256 totalLocked)
  ```

  Returns the total values pertaining to account `accountId` for `collateralType`.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose collateral is being queried.
* `collateralType` (*address*) - The address of the collateral type whose amount is being queried.

**Returns**
* `totalDeposited` (*uint256*) - The total collateral deposited in the account, denominated with 18 decimals of precision.
* `totalAssigned` (*uint256*) - The amount of collateral in the account that is delegated to pools, denominated with 18 decimals of precision.
* `totalLocked` (*uint256*) - The amount of collateral in the account that cannot currently be undelegated from a pool, denominated with 18 decimals of precision.
#### getAccountAvailableCollateral

  ```solidity
  function getAccountAvailableCollateral(uint128 accountId, address collateralType) external view returns (uint256 amountD18)
  ```

  Returns the amount of collateral of type `collateralType` deposited with account `accountId` that can be withdrawn or delegated to pools.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose collateral is being queried.
* `collateralType` (*address*) - The address of the collateral type whose amount is being queried.

**Returns**
* `amountD18` (*uint256*) - The amount of collateral that is available for withdrawal or delegation, denominated with 18 decimals of precision.
#### cleanExpiredLocks

  ```solidity
  function cleanExpiredLocks(uint128 accountId, address collateralType, uint256 offset, uint256 count) external returns (uint256 cleared, uint256 remainingLockAmountD18)
  ```

  Clean expired locks from locked collateral arrays for an account/collateral type. It includes offset and items to prevent gas exhaustion. If both, offset and items, are 0 it will traverse the whole array (unlimited).

**Parameters**
* `accountId` (*uint128*) - The id of the account whose locks are being cleared.
* `collateralType` (*address*) - The address of the collateral type to clean locks for.
* `offset` (*uint256*) - The index of the first lock to clear.
* `count` (*uint256*) - The number of slots to check for cleaning locks. Set to 0 to clean all locks at/after offset

**Returns**
* `cleared` (*uint256*) - the number of locks that were actually expired (and therefore cleared)
* `remainingLockAmountD18` (*uint256*) - 
#### getLocks

  ```solidity
  function getLocks(uint128 accountId, address collateralType, uint256 offset, uint256 count) external view returns (struct CollateralLock.Data[] locks)
  ```

  Get a list of locks existing in account. Lists all locks in storage, even if they are expired

**Parameters**
* `accountId` (*uint128*) - The id of the account whose locks we want to read
* `collateralType` (*address*) - The address of the collateral type for locks we want to read
* `offset` (*uint256*) - The index of the first lock to read
* `count` (*uint256*) - The number of slots to check for cleaning locks. Set to 0 to read all locks after offset

#### createLock

  ```solidity
  function createLock(uint128 accountId, address collateralType, uint256 amount, uint64 expireTimestamp) external
  ```

  Create a new lock on the given account. you must have `admin` permission on the specified account to create a lock.

  Collateral can be withdrawn from the system if it is not assigned or delegated to a pool. Collateral locks are an additional restriction that applies on top of that. I.e. if collateral is not assigned to a pool, but has a lock, it cannot be withdrawn.
Collateral locks are initially intended for the Synthetix v2 to v3 migration, but may be used in the future by the Spartan Council, for example, to create and hand off accounts whose withdrawals from the system are locked for a given amount of time.

**Parameters**
* `accountId` (*uint128*) - The id of the account for which a lock is to be created.
* `collateralType` (*address*) - The address of the collateral type for which the lock will be created.
* `amount` (*uint256*) - The amount of collateral tokens to wrap in the lock being created, denominated with 18 decimals of precision.
* `expireTimestamp` (*uint64*) - The date in which the lock will become clearable.

#### Deposited

  ```solidity
  event Deposited(uint128 accountId, address collateralType, uint256 tokenAmount, address sender)
  ```

  Emitted when `tokenAmount` of collateral of type `collateralType` is deposited to account `accountId` by `sender`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that deposited collateral.
* `collateralType` (*address*) - The address of the collateral that was deposited.
* `tokenAmount` (*uint256*) - The amount of collateral that was deposited, denominated in the token's native decimal representation.
* `sender` (*address*) - The address of the account that triggered the deposit.

#### CollateralLockCreated

  ```solidity
  event CollateralLockCreated(uint128 accountId, address collateralType, uint256 tokenAmount, uint64 expireTimestamp)
  ```

  Emitted when a lock is created on someone's account

**Parameters**
* `accountId` (*uint128*) - The id of the account that received a lock
* `collateralType` (*address*) - The address of the collateral type that was locked
* `tokenAmount` (*uint256*) - The amount of collateral that was locked, demoninated in system units (1e18)
* `expireTimestamp` (*uint64*) - unix timestamp at which the lock is due to expire

#### CollateralLockExpired

  ```solidity
  event CollateralLockExpired(uint256 tokenAmount, uint64 expireTimestamp)
  ```

  Emitted when a lock is cleared from an account due to expiration

**Parameters**
* `tokenAmount` (*uint256*) - The amount of collateral that was unlocked, demoninated in system units (1e18)
* `expireTimestamp` (*uint64*) - unix timestamp at which the unlock is due to expire

#### Withdrawn

  ```solidity
  event Withdrawn(uint128 accountId, address collateralType, uint256 tokenAmount, address sender)
  ```

  Emitted when `tokenAmount` of collateral of type `collateralType` is withdrawn from account `accountId` by `sender`.

**Parameters**
* `accountId` (*uint128*) - The id of the account that withdrew collateral.
* `collateralType` (*address*) - The address of the collateral that was withdrawn.
* `tokenAmount` (*uint256*) - The amount of collateral that was withdrawn, denominated in the token's native decimal representation.
* `sender` (*address*) - The address of the account that triggered the withdrawal.

### Cross ChainUSD Module

#### transferCrossChain

  ```solidity
  function transferCrossChain(uint64 destChainId, uint256 amount) external payable returns (uint256 gasTokenUsed)
  ```

  Allows users to transfer tokens cross-chain using CCIP.

**Parameters**
* `destChainId` (*uint64*) - The id of the chain where tokens are to be transferred to.
* `amount` (*uint256*) - The amount of tokens to be transferred, denominated with 18 decimals of precision.

**Returns**
* `gasTokenUsed` (*uint256*) - The amount of fees paid in the cross-chain transfer, denominated with 18 decimals of precision.

#### TransferCrossChainInitiated

  ```solidity
  event TransferCrossChainInitiated(uint64 destChainId, uint256 amount, address sender)
  ```

### IssueUSD Module

#### mintUsd

  ```solidity
  function mintUsd(uint128 accountId, uint128 poolId, address collateralType, uint256 amount) external
  ```

  Mints {amount} of snxUSD with the specified liquidity position.

**Parameters**
* `accountId` (*uint128*) - The id of the account that is minting snxUSD.
* `poolId` (*uint128*) - The id of the pool whose collateral will be used to back up the mint.
* `collateralType` (*address*) - The address of the collateral that will be used to back up the mint.
* `amount` (*uint256*) - The amount of snxUSD to be minted, denominated with 18 decimals of precision. Requirements: - `ERC2771Context._msgSender()` must be the owner of the account, have the `ADMIN` permission, or have the `MINT` permission. - After minting, the collateralization ratio of the liquidity position must not be below the target collateralization ratio for the corresponding collateral type. Emits a {UsdMinted} event.

#### burnUsd

  ```solidity
  function burnUsd(uint128 accountId, uint128 poolId, address collateralType, uint256 amount) external
  ```

  Burns {amount} of snxUSD with the specified liquidity position.

**Parameters**
* `accountId` (*uint128*) - The id of the account that is burning snxUSD.
* `poolId` (*uint128*) - The id of the pool whose collateral was used to back up the snxUSD.
* `collateralType` (*address*) - The address of the collateral that was used to back up the snxUSD.
* `amount` (*uint256*) - The amount of snxUSD to be burnt, denominated with 18 decimals of precision. Emits a {UsdMinted} event.

#### UsdMinted

  ```solidity
  event UsdMinted(uint128 accountId, uint128 poolId, address collateralType, uint256 amount, address sender)
  ```

  Emitted when {sender} mints {amount} of snxUSD with the specified liquidity position.

**Parameters**
* `accountId` (*uint128*) - The id of the account for which snxUSD was emitted.
* `poolId` (*uint128*) - The id of the pool whose collateral was used to emit the snxUSD.
* `collateralType` (*address*) - The address of the collateral that is backing up the emitted snxUSD.
* `amount` (*uint256*) - The amount of snxUSD emitted, denominated with 18 decimals of precision.
* `sender` (*address*) - The address that triggered the operation.

#### UsdBurned

  ```solidity
  event UsdBurned(uint128 accountId, uint128 poolId, address collateralType, uint256 amount, address sender)
  ```

  Emitted when {sender} burns {amount} of snxUSD with the specified liquidity position.

**Parameters**
* `accountId` (*uint128*) - The id of the account for which snxUSD was burned.
* `poolId` (*uint128*) - The id of the pool whose collateral was used to emit the snxUSD.
* `collateralType` (*address*) - The address of the collateral that was backing up the emitted snxUSD.
* `amount` (*uint256*) - The amount of snxUSD burned, denominated with 18 decimals of precision.
* `sender` (*address*) - The address that triggered the operation.

### Liquidation Module

#### liquidate

  ```solidity
  function liquidate(uint128 accountId, uint128 poolId, address collateralType, uint128 liquidateAsAccountId) external returns (struct ILiquidationModule.LiquidationData liquidationData)
  ```

  Liquidates a position by distributing its debt and collateral among other positions in its vault.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose position is to be liquidated.
* `poolId` (*uint128*) - The id of the pool which holds the position that is to be liquidated.
* `collateralType` (*address*) - The address of the collateral being used in the position that is to be liquidated.
* `liquidateAsAccountId` (*uint128*) - Account id that will receive the rewards from the liquidation.

**Returns**
* `liquidationData` (*struct ILiquidationModule.LiquidationData*) - Information about the position that was liquidated.
#### liquidateVault

  ```solidity
  function liquidateVault(uint128 poolId, address collateralType, uint128 liquidateAsAccountId, uint256 maxUsd) external returns (struct ILiquidationModule.LiquidationData liquidationData)
  ```

  Liquidates an entire vault.

  Can only be done if the vault itself is under collateralized.
LiquidateAsAccountId determines which account to deposit the seized collateral into (this is necessary particularly if the collateral in the vault is vesting).
Will only liquidate a portion of the debt for the vault if `maxUsd` is supplied.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose vault is being liquidated.
* `collateralType` (*address*) - The address of the collateral whose vault is being liquidated.
* `liquidateAsAccountId` (*uint128*) - 
* `maxUsd` (*uint256*) - The maximum amount of USD that the liquidator is willing to provide for the liquidation, denominated with 18 decimals of precision.

**Returns**
* `liquidationData` (*struct ILiquidationModule.LiquidationData*) - Information about the vault that was liquidated.
#### isPositionLiquidatable

  ```solidity
  function isPositionLiquidatable(uint128 accountId, uint128 poolId, address collateralType) external returns (bool canLiquidate)
  ```

  Determines whether a specified position is liquidatable.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose position is being queried for liquidation.
* `poolId` (*uint128*) - The id of the pool whose position is being queried for liquidation.
* `collateralType` (*address*) - The address of the collateral backing up the position being queried for liquidation.

**Returns**
* `canLiquidate` (*bool*) - A boolean with the response to the query.
#### isVaultLiquidatable

  ```solidity
  function isVaultLiquidatable(uint128 poolId, address collateralType) external returns (bool canVaultLiquidate)
  ```

  Determines whether a specified vault is liquidatable.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that owns the vault that is being queried for liquidation.
* `collateralType` (*address*) - The address of the collateral being held at the vault that is being queried for liquidation.

**Returns**
* `canVaultLiquidate` (*bool*) - A boolean with the response to the query.

#### Liquidation

  ```solidity
  event Liquidation(uint128 accountId, uint128 poolId, address collateralType, struct ILiquidationModule.LiquidationData liquidationData, uint128 liquidateAsAccountId, address sender)
  ```

  Emitted when an account is liquidated.

**Parameters**
* `accountId` (*uint128*) - The id of the account that was liquidated.
* `poolId` (*uint128*) - The pool id of the position that was liquidated.
* `collateralType` (*address*) - The collateral type used in the position that was liquidated.
* `liquidationData` (*struct ILiquidationModule.LiquidationData*) - The amount of collateral liquidated, debt liquidated, and collateral awarded to the liquidator.
* `liquidateAsAccountId` (*uint128*) - Account id that will receive the rewards from the liquidation.
* `sender` (*address*) - The address of the account that is triggering the liquidation.

#### VaultLiquidation

  ```solidity
  event VaultLiquidation(uint128 poolId, address collateralType, struct ILiquidationModule.LiquidationData liquidationData, uint128 liquidateAsAccountId, address sender)
  ```

  Emitted when a vault is liquidated.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose vault was liquidated.
* `collateralType` (*address*) - The collateral address of the vault that was liquidated.
* `liquidationData` (*struct ILiquidationModule.LiquidationData*) - The amount of collateral liquidated, debt liquidated, and collateral awarded to the liquidator.
* `liquidateAsAccountId` (*uint128*) - Account id that will receive the rewards from the liquidation.
* `sender` (*address*) - The address of the account that is triggering the liquidation.

### Market Collateral Module

#### depositMarketCollateral

  ```solidity
  function depositMarketCollateral(uint128 marketId, address collateralType, uint256 amount) external
  ```

  Allows a market to deposit collateral.

**Parameters**
* `marketId` (*uint128*) - The id of the market in which the collateral was directly deposited.
* `collateralType` (*address*) - The address of the collateral that was deposited in the market.
* `amount` (*uint256*) - The amount of collateral that was deposited, denominated in the token's native decimal representation.

#### withdrawMarketCollateral

  ```solidity
  function withdrawMarketCollateral(uint128 marketId, address collateralType, uint256 amount) external
  ```

  Allows a market to withdraw collateral that it has previously deposited.

**Parameters**
* `marketId` (*uint128*) - The id of the market from which the collateral was withdrawn.
* `collateralType` (*address*) - The address of the collateral that was withdrawn from the market.
* `amount` (*uint256*) - The amount of collateral that was withdrawn, denominated in the token's native decimal representation.

#### configureMaximumMarketCollateral

  ```solidity
  function configureMaximumMarketCollateral(uint128 marketId, address collateralType, uint256 amount) external
  ```

  Allow the system owner to configure the maximum amount of a given collateral type that a specified market is allowed to deposit.

**Parameters**
* `marketId` (*uint128*) - The id of the market for which the maximum is to be configured.
* `collateralType` (*address*) - The address of the collateral for which the maximum is to be applied.
* `amount` (*uint256*) - The amount that is to be set as the new maximum, denominated with 18 decimals of precision.

#### getMaximumMarketCollateral

  ```solidity
  function getMaximumMarketCollateral(uint128 marketId, address collateralType) external view returns (uint256 amountD18)
  ```

  Return the total maximum amount of a given collateral type that a specified market is allowed to deposit.

**Parameters**
* `marketId` (*uint128*) - The id of the market for which the maximum is being queried.
* `collateralType` (*address*) - The address of the collateral for which the maximum is being queried.

**Returns**
* `amountD18` (*uint256*) - The maximum amount of collateral set for the market, denominated with 18 decimals of precision.
#### getMarketCollateralAmount

  ```solidity
  function getMarketCollateralAmount(uint128 marketId, address collateralType) external view returns (uint256 amountD18)
  ```

  Return the total amount of a given collateral type that a specified market has deposited.

**Parameters**
* `marketId` (*uint128*) - The id of the market for which the directly deposited collateral amount is being queried.
* `collateralType` (*address*) - The address of the collateral for which the amount is being queried.

**Returns**
* `amountD18` (*uint256*) - The total amount of collateral of this type delegated to the market, denominated with 18 decimals of precision.
#### getMarketCollateralValue

  ```solidity
  function getMarketCollateralValue(uint128 marketId) external view returns (uint256 valueD18)
  ```

  Return the total value of collateral that a specified market has deposited.

**Parameters**
* `marketId` (*uint128*) - The id of the market for which the directly deposited collateral amount is being queried.

**Returns**
* `valueD18` (*uint256*) - The total value of collateral deposited by the market, denominated with 18 decimals of precision.

#### MarketCollateralDeposited

  ```solidity
  event MarketCollateralDeposited(uint128 marketId, address collateralType, uint256 tokenAmount, address sender, int128 creditCapacity, int128 netIssuance, uint256 depositedCollateralValue, uint256 reportedDebt)
  ```

  Emitted when `amount` of collateral of type `collateralType` is deposited to market `marketId` by `sender`.

**Parameters**
* `marketId` (*uint128*) - The id of the market in which collateral was deposited.
* `collateralType` (*address*) - The address of the collateral that was directly deposited in the market.
* `tokenAmount` (*uint256*) - The amount of tokens that were deposited, denominated in the token's native decimal representation.
* `sender` (*address*) - The address that triggered the deposit.
* `creditCapacity` (*int128*) - Updated credit capacity of the market after depositing collateral.
* `netIssuance` (*int128*) - Updated net issuance.
* `depositedCollateralValue` (*uint256*) - Updated deposited collateral value of the market.
* `reportedDebt` (*uint256*) - Updated reported debt of the market after depositing collateral.

#### MarketCollateralWithdrawn

  ```solidity
  event MarketCollateralWithdrawn(uint128 marketId, address collateralType, uint256 tokenAmount, address sender, int128 creditCapacity, int128 netIssuance, uint256 depositedCollateralValue, uint256 reportedDebt)
  ```

  Emitted when `amount` of collateral of type `collateralType` is withdrawn from market `marketId` by `sender`.

**Parameters**
* `marketId` (*uint128*) - The id of the market from which collateral was withdrawn.
* `collateralType` (*address*) - The address of the collateral that was withdrawn from the market.
* `tokenAmount` (*uint256*) - The amount of tokens that were withdrawn, denominated in the token's native decimal representation.
* `sender` (*address*) - The address that triggered the withdrawal.
* `creditCapacity` (*int128*) - Updated credit capacity of the market after withdrawing.
* `netIssuance` (*int128*) - Updated net issuance.
* `depositedCollateralValue` (*uint256*) - Updated deposited collateral value of the market.
* `reportedDebt` (*uint256*) - Updated reported debt of the market after withdrawing collateral.

#### MaximumMarketCollateralConfigured

  ```solidity
  event MaximumMarketCollateralConfigured(uint128 marketId, address collateralType, uint256 systemAmount, address owner)
  ```

  Emitted when the system owner specifies the maximum depositable collateral of a given type in a given market.

**Parameters**
* `marketId` (*uint128*) - The id of the market for which the maximum was configured.
* `collateralType` (*address*) - The address of the collateral for which the maximum was configured.
* `systemAmount` (*uint256*) - The amount to which the maximum was set, denominated with 18 decimals of precision.
* `owner` (*address*) - The owner of the system, which triggered the configuration change.

### Market Manager Module

#### registerMarket

  ```solidity
  function registerMarket(address market) external returns (uint128 newMarketId)
  ```

  Connects an external market to the system.

  Creates a Market object to track the external market, and returns the newly created market id.

**Parameters**
* `market` (*address*) - The address of the external market that is to be registered in the system.

**Returns**
* `newMarketId` (*uint128*) - The id with which the market will be registered in the system.
#### depositMarketUsd

  ```solidity
  function depositMarketUsd(uint128 marketId, address target, uint256 amount) external returns (uint256 feeAmount)
  ```

  Allows an external market connected to the system to deposit USD in the system.

  The system burns the incoming USD, increases the market's credit capacity, and reduces its issuance.
See `IMarket`.

**Parameters**
* `marketId` (*uint128*) - The id of the market in which snxUSD will be deposited.
* `target` (*address*) - The address of the account on who's behalf the deposit will be made.
* `amount` (*uint256*) - The amount of snxUSD to be deposited, denominated with 18 decimals of precision.

**Returns**
* `feeAmount` (*uint256*) - Fee collected by the core system. Always 0 in the current implementation.
#### withdrawMarketUsd

  ```solidity
  function withdrawMarketUsd(uint128 marketId, address target, uint256 amount) external returns (uint256 feeAmount)
  ```

  Allows an external market connected to the system to withdraw snxUSD from the system.

  The system mints the requested snxUSD (provided that the market has sufficient credit), reduces the market's credit capacity, and increases its net issuance.
See `IMarket`.

**Parameters**
* `marketId` (*uint128*) - The id of the market from which snxUSD will be withdrawn.
* `target` (*address*) - The address of the account that will receive the withdrawn snxUSD.
* `amount` (*uint256*) - The amount of snxUSD to be withdraw, denominated with 18 decimals of precision.

**Returns**
* `feeAmount` (*uint256*) - Fee collected by the core system. Always 0 in the current implementation.
#### getMarketFees

  ```solidity
  function getMarketFees(uint128 marketId, uint256 amount) external view returns (uint256 depositFeeAmount, uint256 withdrawFeeAmount)
  ```

  Get the amount of fees paid in USD for a call to `depositMarketUsd` and `withdrawMarketUsd` for the given market and amount

**Parameters**
* `marketId` (*uint128*) - The market to check fees for
* `amount` (*uint256*) - The amount deposited or withdrawn in USD

**Returns**
* `depositFeeAmount` (*uint256*) - the amount of USD paid for a call to `depositMarketUsd`, always 0
* `withdrawFeeAmount` (*uint256*) - the amount of USD paid for a call to `withdrawMarketUsd`, always 0
#### getWithdrawableMarketUsd

  ```solidity
  function getWithdrawableMarketUsd(uint128 marketId) external view returns (uint256 withdrawableD18)
  ```

  Returns the total withdrawable snxUSD amount for the specified market.

**Parameters**
* `marketId` (*uint128*) - The id of the market whose withdrawable USD amount is being queried.

**Returns**
* `withdrawableD18` (*uint256*) - The total amount of snxUSD that the market could withdraw at the time of the query, denominated with 18 decimals of precision.
#### getMarketAddress

  ```solidity
  function getMarketAddress(uint128 marketId) external view returns (address marketAddress)
  ```

  Returns the contract address for the specified market.

**Parameters**
* `marketId` (*uint128*) - The id of the market

**Returns**
* `marketAddress` (*address*) - The contract address for the specified market
#### getMarketNetIssuance

  ```solidity
  function getMarketNetIssuance(uint128 marketId) external view returns (int128 issuanceD18)
  ```

  Returns the net issuance of the specified market (snxUSD withdrawn - snxUSD deposited).

**Parameters**
* `marketId` (*uint128*) - The id of the market whose net issuance is being queried.

**Returns**
* `issuanceD18` (*int128*) - The net issuance of the market, denominated with 18 decimals of precision.
#### getMarketReportedDebt

  ```solidity
  function getMarketReportedDebt(uint128 marketId) external view returns (uint256 reportedDebtD18)
  ```

  Returns the reported debt of the specified market.

**Parameters**
* `marketId` (*uint128*) - The id of the market whose reported debt is being queried.

**Returns**
* `reportedDebtD18` (*uint256*) - The market's reported debt, denominated with 18 decimals of precision.
#### getMarketTotalDebt

  ```solidity
  function getMarketTotalDebt(uint128 marketId) external view returns (int256 totalDebtD18)
  ```

  Returns the total debt of the specified market.

**Parameters**
* `marketId` (*uint128*) - The id of the market whose debt is being queried.

**Returns**
* `totalDebtD18` (*int256*) - The total debt of the market, denominated with 18 decimals of precision.
#### getMarketCollateral

  ```solidity
  function getMarketCollateral(uint128 marketId) external view returns (uint256 valueD18)
  ```

  Returns the total snxUSD value of the collateral for the specified market.

**Parameters**
* `marketId` (*uint128*) - The id of the market whose collateral is being queried.

**Returns**
* `valueD18` (*uint256*) - The market's total snxUSD value of collateral, denominated with 18 decimals of precision.
#### getMarketDebtPerShare

  ```solidity
  function getMarketDebtPerShare(uint128 marketId) external returns (int256 debtPerShareD18)
  ```

  Returns the value per share of the debt of the specified market.

  This is not a view function, and actually updates the entire debt distribution chain.

**Parameters**
* `marketId` (*uint128*) - The id of the market whose debt per share is being queried.

**Returns**
* `debtPerShareD18` (*int256*) - The market's debt per share value, denominated with 18 decimals of precision.
#### isMarketCapacityLocked

  ```solidity
  function isMarketCapacityLocked(uint128 marketId) external view returns (bool isLocked)
  ```

  Returns whether the capacity of the specified market is locked.

**Parameters**
* `marketId` (*uint128*) - The id of the market whose capacity is being queried.

**Returns**
* `isLocked` (*bool*) - A boolean that is true if the market's capacity is locked at the time of the query.
#### getUsdToken

  ```solidity
  function getUsdToken() external view returns (contract IERC20)
  ```

  Returns the USD token associated with this synthetix core system

#### getOracleManager

  ```solidity
  function getOracleManager() external view returns (contract IOracleManager)
  ```

  Retrieve the systems' configured oracle manager address

#### distributeDebtToPools

  ```solidity
  function distributeDebtToPools(uint128 marketId, uint256 maxIter) external returns (bool finishedDistributing)
  ```

  Update a market's current debt registration with the system.
This function is provided as an escape hatch for pool griefing, preventing
overwhelming the system with a series of very small pools and creating high gas
costs to update an account.

**Parameters**
* `marketId` (*uint128*) - the id of the market that needs pools bumped
* `maxIter` (*uint256*) - 

**Returns**
* `finishedDistributing` (*bool*) - whether or not all bumpable pools have been bumped and target price has been reached
#### setMarketMinDelegateTime

  ```solidity
  function setMarketMinDelegateTime(uint128 marketId, uint32 minDelegateTime) external
  ```

  allows for a market to set its minimum delegation time. This is useful for preventing stakers from frontrunning rewards or losses
by limiting the frequency of `delegateCollateral` (or `setPoolConfiguration`) calls. By default, there is no minimum delegation time.

**Parameters**
* `marketId` (*uint128*) - the id of the market that wants to set delegation time.
* `minDelegateTime` (*uint32*) - the minimum number of seconds between delegation calls. Note: this value must be less than the globally defined maximum minDelegateTime

#### getMarketMinDelegateTime

  ```solidity
  function getMarketMinDelegateTime(uint128 marketId) external view returns (uint32)
  ```

  Retrieve the minimum delegation time of a market

**Parameters**
* `marketId` (*uint128*) - the id of the market

#### setMinLiquidityRatio

  ```solidity
  function setMinLiquidityRatio(uint128 marketId, uint256 minLiquidityRatio) external
  ```

  Allows the system owner (not the pool owner) to set a market-specific minimum liquidity ratio.

**Parameters**
* `marketId` (*uint128*) - the id of the market
* `minLiquidityRatio` (*uint256*) - The new market-specific minimum liquidity ratio, denominated with 18 decimals of precision. (100% is represented by 1 followed by 18 zeros.)

#### getMinLiquidityRatio

  ```solidity
  function getMinLiquidityRatio(uint128 marketId) external view returns (uint256 minRatioD18)
  ```

  Retrieves the market-specific minimum liquidity ratio.

**Parameters**
* `marketId` (*uint128*) - the id of the market

**Returns**
* `minRatioD18` (*uint256*) - The current market-specific minimum liquidity ratio, denominated with 18 decimals of precision. (100% is represented by 1 followed by 18 zeros.)
#### getMarketPools

  ```solidity
  function getMarketPools(uint128 marketId) external returns (uint128[] inRangePoolIds, uint128[] outRangePoolIds)
  ```

#### getMarketPoolDebtDistribution

  ```solidity
  function getMarketPoolDebtDistribution(uint128 marketId, uint128 poolId) external returns (uint256 sharesD18, uint128 totalSharesD18, int128 valuePerShareD27)
  ```

#### MarketRegistered

  ```solidity
  event MarketRegistered(address market, uint128 marketId, address sender)
  ```

  Emitted when a new market is registered in the system.

**Parameters**
* `market` (*address*) - The address of the external market that was registered in the system.
* `marketId` (*uint128*) - The id with which the market was registered in the system.
* `sender` (*address*) - The account that trigger the registration of the market.

#### MarketUsdDeposited

  ```solidity
  event MarketUsdDeposited(uint128 marketId, address target, uint256 amount, address market, int128 creditCapacity, int128 netIssuance, uint256 depositedCollateralValue)
  ```

  Emitted when a market deposits snxUSD in the system.

**Parameters**
* `marketId` (*uint128*) - The id of the market that deposited snxUSD in the system.
* `target` (*address*) - The address of the account that provided the snxUSD in the deposit.
* `amount` (*uint256*) - The amount of snxUSD deposited in the system, denominated with 18 decimals of precision.
* `market` (*address*) - The address of the external market that is depositing.
* `creditCapacity` (*int128*) - Updated credit capacity of the market after depositing.
* `netIssuance` (*int128*) - Updated net issuance.
* `depositedCollateralValue` (*uint256*) - Updated deposited collateral value of the market.

#### MarketUsdWithdrawn

  ```solidity
  event MarketUsdWithdrawn(uint128 marketId, address target, uint256 amount, address market, int128 creditCapacity, int128 netIssuance, uint256 depositedCollateralValue)
  ```

  Emitted when a market withdraws snxUSD from the system.

**Parameters**
* `marketId` (*uint128*) - The id of the market that withdrew snxUSD from the system.
* `target` (*address*) - The address of the account that received the snxUSD in the withdrawal.
* `amount` (*uint256*) - The amount of snxUSD withdrawn from the system, denominated with 18 decimals of precision.
* `market` (*address*) - The address of the external market that is withdrawing.
* `creditCapacity` (*int128*) - Updated credit capacity of the market after withdrawing.
* `netIssuance` (*int128*) - Updated net issuance.
* `depositedCollateralValue` (*uint256*) - Updated deposited collateral value of the market

#### SetMinDelegateTime

  ```solidity
  event SetMinDelegateTime(uint128 marketId, uint32 minDelegateTime)
  ```

  Emitted when a market sets an updated minimum delegation time

**Parameters**
* `marketId` (*uint128*) - The id of the market that the setting is applied to
* `minDelegateTime` (*uint32*) - The minimum amount of time between delegation changes

#### SetMarketMinLiquidityRatio

  ```solidity
  event SetMarketMinLiquidityRatio(uint128 marketId, uint256 minLiquidityRatio)
  ```

  Emitted when a market-specific minimum liquidity ratio is set

**Parameters**
* `marketId` (*uint128*) - The id of the market that the setting is applied to
* `minLiquidityRatio` (*uint256*) - The new market-specific minimum liquidity ratio

### Pool Configuration Module

#### setPreferredPool

  ```solidity
  function setPreferredPool(uint128 poolId) external
  ```

  Sets the unique system preferred pool.

  Note: The preferred pool does not receive any special treatment. It is only signaled as preferred here.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that is to be set as preferred.

#### addApprovedPool

  ```solidity
  function addApprovedPool(uint128 poolId) external
  ```

  Marks a pool as approved by the system owner.

  Approved pools do not receive any special treatment. They are only signaled as approved here.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that is to be approved.

#### removeApprovedPool

  ```solidity
  function removeApprovedPool(uint128 poolId) external
  ```

  Un-marks a pool as preferred by the system owner.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that is to be no longer approved.

#### getPreferredPool

  ```solidity
  function getPreferredPool() external view returns (uint128 poolId)
  ```

  Retrieves the unique system preferred pool.

**Returns**
* `poolId` (*uint128*) - The id of the pool that is currently set as preferred in the system.
#### getApprovedPools

  ```solidity
  function getApprovedPools() external view returns (uint256[] poolIds)
  ```

  Retrieves the pool that are approved by the system owner.

**Returns**
* `poolIds` (*uint256[]*) - An array with all of the pool ids that are approved in the system.

#### PreferredPoolSet

  ```solidity
  event PreferredPoolSet(uint256 poolId)
  ```

  Emitted when the system owner sets the preferred pool.

**Parameters**
* `poolId` (*uint256*) - The id of the pool that was set as preferred.

#### PoolApprovedAdded

  ```solidity
  event PoolApprovedAdded(uint256 poolId)
  ```

  Emitted when the system owner adds an approved pool.

**Parameters**
* `poolId` (*uint256*) - The id of the pool that was approved.

#### PoolApprovedRemoved

  ```solidity
  event PoolApprovedRemoved(uint256 poolId)
  ```

  Emitted when the system owner removes an approved pool.

**Parameters**
* `poolId` (*uint256*) - The id of the pool that is no longer approved.

### Pool Module

#### createPool

  ```solidity
  function createPool(uint128 requestedPoolId, address owner) external
  ```

  Creates a pool with the requested pool id.

**Parameters**
* `requestedPoolId` (*uint128*) - The requested id for the new pool. Reverts if the id is not available.
* `owner` (*address*) - The address that will own the newly created pool.

#### setPoolConfiguration

  ```solidity
  function setPoolConfiguration(uint128 poolId, struct MarketConfiguration.Data[] marketDistribution) external
  ```

  Allows the pool owner to configure the pool.

  The pool's configuration is composed of an array of MarketConfiguration objects, which describe which markets the pool provides liquidity to, in what proportion, and to what extent.
Incoming market ids need to be provided in ascending order.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose configuration is being set.
* `marketDistribution` (*struct MarketConfiguration.Data[]*) - The array of market configuration objects that define the list of markets that are connected to the system.

#### setPoolCollateralConfiguration

  ```solidity
  function setPoolCollateralConfiguration(uint128 poolId, address collateralType, struct PoolCollateralConfiguration.Data newConfig) external
  ```

  Allows the pool owner to set the configuration of a specific collateral type for their pool.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose configuration is being set.
* `collateralType` (*address*) - The collate
* `newConfig` (*struct PoolCollateralConfiguration.Data*) - The config to set

#### getPoolCollateralConfiguration

  ```solidity
  function getPoolCollateralConfiguration(uint128 poolId, address collateralType) external view returns (struct PoolCollateralConfiguration.Data config)
  ```

  Retrieves the pool configuration of a specific collateral type.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose configuration is being returned.
* `collateralType` (*address*) - The address of the collateral.

**Returns**
* `config` (*struct PoolCollateralConfiguration.Data*) - The PoolCollateralConfiguration object that describes the requested collateral configuration of the pool.
#### setPoolCollateralDisabledByDefault

  ```solidity
  function setPoolCollateralDisabledByDefault(uint128 poolId, bool disabled) external
  ```

  Allows collaterals accepeted by the system to be accepeted by the pool by default

**Parameters**
* `poolId` (*uint128*) - The id of the pool.
* `disabled` (*bool*) - If set to true new collaterals will be disabled for the pool.

#### getPoolConfiguration

  ```solidity
  function getPoolConfiguration(uint128 poolId) external view returns (struct MarketConfiguration.Data[] markets)
  ```

  Retrieves the MarketConfiguration of the specified pool.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose configuration is being queried.

**Returns**
* `markets` (*struct MarketConfiguration.Data[]*) - The array of MarketConfiguration objects that describe the pool's configuration.
#### setPoolName

  ```solidity
  function setPoolName(uint128 poolId, string name) external
  ```

  Allows the owner of the pool to set the pool's name.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose name is being set.
* `name` (*string*) - The new name to give to the pool.

#### getPoolName

  ```solidity
  function getPoolName(uint128 poolId) external view returns (string poolName)
  ```

  Returns the pool's name.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose name is being queried.

**Returns**
* `poolName` (*string*) - The current name of the pool.
#### nominatePoolOwner

  ```solidity
  function nominatePoolOwner(address nominatedOwner, uint128 poolId) external
  ```

  Allows the current pool owner to nominate a new owner.

**Parameters**
* `nominatedOwner` (*address*) - The address to nominate os the new pool owner.
* `poolId` (*uint128*) - The id whose ownership is being transferred.

#### acceptPoolOwnership

  ```solidity
  function acceptPoolOwnership(uint128 poolId) external
  ```

  After a new pool owner has been nominated, allows it to accept the nomination and thus ownership of the pool.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the caller is to accept ownership.

#### revokePoolNomination

  ```solidity
  function revokePoolNomination(uint128 poolId) external
  ```

  After a new pool owner has been nominated, allows it to reject the nomination.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the new owner nomination is to be revoked.

#### renouncePoolNomination

  ```solidity
  function renouncePoolNomination(uint128 poolId) external
  ```

  Allows the current nominated owner to renounce the nomination.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the caller is renouncing ownership nomination.

#### renouncePoolOwnership

  ```solidity
  function renouncePoolOwnership(uint128 poolId) external
  ```

  Allows the current owner to renounce his ownership.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the caller is renouncing ownership nomination.

#### getPoolOwner

  ```solidity
  function getPoolOwner(uint128 poolId) external view returns (address owner)
  ```

  Returns the current pool owner.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose ownership is being queried.

**Returns**
* `owner` (*address*) - The current owner of the pool.
#### getNominatedPoolOwner

  ```solidity
  function getNominatedPoolOwner(uint128 poolId) external view returns (address nominatedOwner)
  ```

  Returns the current nominated pool owner.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose nominated owner is being queried.

**Returns**
* `nominatedOwner` (*address*) - The current nominated owner of the pool.
#### setMinLiquidityRatio

  ```solidity
  function setMinLiquidityRatio(uint256 minLiquidityRatio) external
  ```

  Allows the system owner (not the pool owner) to set the system-wide minimum liquidity ratio.

**Parameters**
* `minLiquidityRatio` (*uint256*) - The new system-wide minimum liquidity ratio, denominated with 18 decimals of precision. (100% is represented by 1 followed by 18 zeros.)

#### getPoolCollateralIssuanceRatio

  ```solidity
  function getPoolCollateralIssuanceRatio(uint128 poolId, address collateral) external view returns (uint256 issuanceRatioD18)
  ```

  returns a pool minimum issuance ratio

**Parameters**
* `poolId` (*uint128*) - The id of the pool for to check the collateral for.
* `collateral` (*address*) - The address of the collateral.

#### getMinLiquidityRatio

  ```solidity
  function getMinLiquidityRatio() external view returns (uint256 minRatioD18)
  ```

  Retrieves the system-wide minimum liquidity ratio.

**Returns**
* `minRatioD18` (*uint256*) - The current system-wide minimum liquidity ratio, denominated with 18 decimals of precision. (100% is represented by 1 followed by 18 zeros.)
#### rebalancePool

  ```solidity
  function rebalancePool(uint128 poolId, address optionalCollateralType) external
  ```

  Distributes cached debt in a pool to its vaults and updates market credit capacities.

**Parameters**
* `poolId` (*uint128*) - the pool to rebalance
* `optionalCollateralType` (*address*) - in addition to rebalancing the pool, calculate updated collaterals and debts for the specified vault

#### PoolCreated

  ```solidity
  event PoolCreated(uint128 poolId, address owner, address sender)
  ```

  Gets fired when pool will be created.

**Parameters**
* `poolId` (*uint128*) - The id of the newly created pool.
* `owner` (*address*) - The owner of the newly created pool.
* `sender` (*address*) - The address that triggered the creation of the pool.

#### PoolOwnerNominated

  ```solidity
  event PoolOwnerNominated(uint128 poolId, address nominatedOwner, address owner)
  ```

  Gets fired when pool owner proposes a new owner.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the nomination ocurred.
* `nominatedOwner` (*address*) - The address that was nominated as the new owner of the pool.
* `owner` (*address*) - The address of the current owner of the pool.

#### PoolOwnershipAccepted

  ```solidity
  event PoolOwnershipAccepted(uint128 poolId, address owner)
  ```

  Gets fired when pool nominee accepts nomination.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the owner nomination was accepted.
* `owner` (*address*) - The address of the new owner of the pool, which accepted the nomination.

#### PoolNominationRevoked

  ```solidity
  event PoolNominationRevoked(uint128 poolId, address owner)
  ```

  Gets fired when pool owner revokes nomination.

**Parameters**
* `poolId` (*uint128*) - The id of the pool in which the nomination was revoked.
* `owner` (*address*) - The current owner of the pool.

#### PoolNominationRenounced

  ```solidity
  event PoolNominationRenounced(uint128 poolId, address owner)
  ```

  Gets fired when pool nominee renounces nomination.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the owner nomination was renounced.
* `owner` (*address*) - The current owner of the pool.

#### PoolOwnershipRenounced

  ```solidity
  event PoolOwnershipRenounced(uint128 poolId, address owner)
  ```

  Gets fired when pool owner renounces his own ownership.

**Parameters**
* `poolId` (*uint128*) - The id of the pool for which the owner nomination was renounced.
* `owner` (*address*) - 

#### PoolNameUpdated

  ```solidity
  event PoolNameUpdated(uint128 poolId, string name, address sender)
  ```

  Gets fired when pool name changes.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose name was updated.
* `name` (*string*) - The new name of the pool.
* `sender` (*address*) - The address that triggered the rename of the pool.

#### PoolConfigurationSet

  ```solidity
  event PoolConfigurationSet(uint128 poolId, struct MarketConfiguration.Data[] markets, address sender)
  ```

  Gets fired when pool gets configured.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose configuration was set.
* `markets` (*struct MarketConfiguration.Data[]*) - Array of configuration data of the markets that were connected to the pool.
* `sender` (*address*) - The address that triggered the pool configuration.

#### PoolCollateralConfigurationUpdated

  ```solidity
  event PoolCollateralConfigurationUpdated(uint128 poolId, address collateralType, struct PoolCollateralConfiguration.Data config)
  ```

#### SetMinLiquidityRatio

  ```solidity
  event SetMinLiquidityRatio(uint256 minLiquidityRatio)
  ```

  Emitted when a system-wide minimum liquidity ratio is set

**Parameters**
* `minLiquidityRatio` (*uint256*) - The new system-wide minimum liquidity ratio

#### PoolCollateralDisabledByDefaultSet

  ```solidity
  event PoolCollateralDisabledByDefaultSet(uint128 poolId, bool disabled)
  ```

  Allows collaterals accepeted by the system to be accepeted by the pool by default

**Parameters**
* `poolId` (*uint128*) - The id of the pool.
* `disabled` (*bool*) - Shows if new collateral's will be dsiabled by default for the pool

### Rewards Manager Module

#### registerRewardsDistributor

  ```solidity
  function registerRewardsDistributor(uint128 poolId, address collateralType, address distributor) external
  ```

  Called by pool owner to register rewards for vault participants.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose rewards are to be managed by the specified distributor.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the reward distributor to be registered.

#### removeRewardsDistributor

  ```solidity
  function removeRewardsDistributor(uint128 poolId, address collateralType, address distributor) external
  ```

  Called by pool owner to remove a registered rewards distributor for vault participants.
WARNING: if you remove a rewards distributor, the same address can never be re-registered again. If you
simply want to turn off
rewards, call `distributeRewards` with 0 emission. If you need to completely reset the rewards distributor
again, create a new rewards distributor at a new address and register the new one.
This function is provided since the number of rewards distributors added to an account is finite,
so you can remove an unused rewards distributor if need be.
NOTE: unclaimed rewards can still be claimed after a rewards distributor is removed (though any
rewards-over-time will be halted)

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose rewards are to be managed by the specified distributor.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the reward distributor to be registered.

#### distributeRewards

  ```solidity
  function distributeRewards(uint128 poolId, address collateralType, uint256 amount, uint64 start, uint32 duration) external returns (int256 cancelledAmount)
  ```

  Called by a registered distributor to set up rewards for vault participants.

  Will revert if the caller is not a registered distributor.

**Parameters**
* `poolId` (*uint128*) - The id of the pool to distribute rewards to.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `amount` (*uint256*) - The amount of rewards to be distributed.
* `start` (*uint64*) - The date at which the rewards will begin to be claimable.
* `duration` (*uint32*) - The period after which all distributed rewards will be claimable.

**Returns**
* `cancelledAmount` (*int256*) - the amount of reward which was previously issued on a call to `distributeRewards`, but will ultimately not be distributed due to the duration period being interrupted by the start of this new distribution
#### distributeRewardsByOwner

  ```solidity
  function distributeRewardsByOwner(uint128 poolId, address collateralType, address rewardsDistributor, uint256 amount, uint64 start, uint32 duration) external returns (int256 cancelledAmount)
  ```

  Called by owner of a pool to set rewards for vault participants. This method
of reward setting is generally intended to only be used to recover from a case where the
distributor state is out of sync with the core system state, or if the distributor is only
able to payout and not capable of distributing its own rewards.

  Will revert if the caller is not the owner of the pool.

**Parameters**
* `poolId` (*uint128*) - The id of the pool to distribute rewards to.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `rewardsDistributor` (*address*) - The address of the reward distributor which pays out the tokens.
* `amount` (*uint256*) - The amount of rewards to be distributed.
* `start` (*uint64*) - The date at which the rewards will begin to be claimable.
* `duration` (*uint32*) - The period after which all distributed rewards will be claimable.

#### claimRewards

  ```solidity
  function claimRewards(uint128 accountId, uint128 poolId, address collateralType, address distributor) external returns (uint256 amountClaimedD18)
  ```

  Allows a user with appropriate permissions to claim rewards associated with a position.

**Parameters**
* `accountId` (*uint128*) - The id of the account that is to claim the rewards.
* `poolId` (*uint128*) - The id of the pool to claim rewards on.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the rewards distributor associated with the rewards being claimed.

**Returns**
* `amountClaimedD18` (*uint256*) - The amount of rewards that were available for the account and thus claimed.
#### claimPoolRewards

  ```solidity
  function claimPoolRewards(uint128 accountId, uint128 poolId, address collateralType, address distributor) external returns (uint256 amountClaimedD18)
  ```

  Allows a user with appropriate permissions to claim rewards associated with a position for rewards issued at the pool level.

**Parameters**
* `accountId` (*uint128*) - The id of the account that is to claim the rewards.
* `poolId` (*uint128*) - The id of the pool to claim rewards on.
* `collateralType` (*address*) - The address of the collateral used by the user to gain rewards from the pool level.
* `distributor` (*address*) - The address of the rewards distributor associated with the rewards being claimed.

**Returns**
* `amountClaimedD18` (*uint256*) - The amount of rewards that were available for the account and thus claimed.
#### updateRewards

  ```solidity
  function updateRewards(uint128 poolId, address collateralType, uint128 accountId) external returns (uint256[] claimableD18, address[] distributors, uint256 numPoolRewards)
  ```

  For a given position, return the rewards that can currently be claimed.

**Parameters**
* `poolId` (*uint128*) - The id of the pool being queried.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `accountId` (*uint128*) - The id of the account whose available rewards are being queried.

**Returns**
* `claimableD18` (*uint256[]*) - An array of ids of the reward entries that are claimable by the position.
* `distributors` (*address[]*) - An array with the addresses of the reward distributors associated with the claimable rewards.
* `numPoolRewards` (*uint256*) - Returns how many of the first returned rewards are pool level rewards (the rest are vault)
#### getRewardRate

  ```solidity
  function getRewardRate(uint128 poolId, address collateralType, address distributor) external view returns (uint256 rateD18)
  ```

  Returns the number of individual units of amount emitted per second per share for the given poolId, collateralType, distributor vault.

**Parameters**
* `poolId` (*uint128*) - The id of the pool being queried.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the rewards distributor associated with the rewards in question.

**Returns**
* `rateD18` (*uint256*) - The queried rewards rate.
#### getAvailableRewards

  ```solidity
  function getAvailableRewards(uint128 accountId, uint128 poolId, address collateralType, address distributor) external returns (uint256 rewardAmount)
  ```

  Returns the amount of claimable rewards for a given account position for a vault distributor.

**Parameters**
* `accountId` (*uint128*) - The id of the account to look up rewards on.
* `poolId` (*uint128*) - The id of the pool to claim rewards on.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the rewards distributor associated with the rewards being claimed.

**Returns**
* `rewardAmount` (*uint256*) - The amount of available rewards that are available for the provided account.
#### getAvailablePoolRewards

  ```solidity
  function getAvailablePoolRewards(uint128 accountId, uint128 poolId, address collateralType, address distributor) external returns (uint256 rewardAmount)
  ```

  Returns the amount of claimable rewards for a given account position for a pool level distributor.

**Parameters**
* `accountId` (*uint128*) - The id of the account to look up rewards on.
* `poolId` (*uint128*) - The id of the pool to claim rewards on.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the rewards distributor associated with the rewards being claimed.

**Returns**
* `rewardAmount` (*uint256*) - The amount of available rewards that are available for the provided account.

#### RewardsDistributed

  ```solidity
  event RewardsDistributed(uint128 poolId, address collateralType, address distributor, uint256 amount, uint256 start, uint256 duration)
  ```

  Emitted when the pool owner or an existing reward distributor sets up rewards for vault participants.

**Parameters**
* `poolId` (*uint128*) - The id of the pool on which rewards were distributed.
* `collateralType` (*address*) - The collateral type of the pool on which rewards were distributed.
* `distributor` (*address*) - The reward distributor associated to the rewards that were distributed.
* `amount` (*uint256*) - The amount of rewards that were distributed.
* `start` (*uint256*) - The date one which the rewards will begin to be claimable.
* `duration` (*uint256*) - The time in which all of the distributed rewards will be claimable.

#### RewardsClaimed

  ```solidity
  event RewardsClaimed(uint128 accountId, uint128 poolId, address collateralType, address distributor, uint256 amount)
  ```

  Emitted when a vault participant claims rewards.

**Parameters**
* `accountId` (*uint128*) - The id of the account that claimed the rewards.
* `poolId` (*uint128*) - The id of the pool where the rewards were claimed.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the rewards distributor associated with these rewards.
* `amount` (*uint256*) - The amount of rewards that were claimed.

#### RewardsDistributorRegistered

  ```solidity
  event RewardsDistributorRegistered(uint128 poolId, address collateralType, address distributor)
  ```

  Emitted when a new rewards distributor is registered.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose reward distributor was registered.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the newly registered reward distributor.

#### RewardsDistributorRemoved

  ```solidity
  event RewardsDistributorRemoved(uint128 poolId, address collateralType, address distributor)
  ```

  Emitted when an already registered rewards distributor is removed.

**Parameters**
* `poolId` (*uint128*) - The id of the pool whose reward distributor was registered.
* `collateralType` (*address*) - The address of the collateral used in the pool's rewards.
* `distributor` (*address*) - The address of the registered reward distributor.

### USD Token Module

#### burnWithAllowance

  ```solidity
  function burnWithAllowance(address from, address spender, uint256 amount) external
  ```

  Allows the core system to burn snxUSD held by the `from` address, provided that it has given allowance to `spender`.

**Parameters**
* `from` (*address*) - The address that holds the snxUSD to be burned.
* `spender` (*address*) - The address to which the holder has given allowance to.
* `amount` (*uint256*) - The amount of snxUSD to be burned, denominated with 18 decimals of precision.

#### burn

  ```solidity
  function burn(uint256 amount) external
  ```

  Destroys `amount` of snxUSD tokens from the caller. This is derived from ERC20Burnable.sol and is currently included for testing purposes with CCIP token pools.

**Parameters**
* `amount` (*uint256*) - The amount of snxUSD to be burned, denominated with 18 decimals of precision.

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns wether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, uint8 tokenDecimals) external
  ```

  Initializes the token with name, symbol, and decimals.

#### mint

  ```solidity
  function mint(address to, uint256 amount) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `amount` (*uint256*) - The amount of tokens to mint.

#### burn

  ```solidity
  function burn(address from, uint256 amount) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `from` (*address*) - The address whose tokens will be burnt.
* `amount` (*uint256*) - The amount of tokens to burn.

#### setAllowance

  ```solidity
  function setAllowance(address from, address spender, uint256 amount) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `from` (*address*) - The address that is providing allowance.
* `spender` (*address*) - The address that is given allowance.
* `amount` (*uint256*) - The amount of allowance being given.

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Network Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Retrieves the number of decimals used by the token. The default is 18.

**Returns**
* `[0]` (*uint8*) - The number of decimals.
#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total number of tokens in circulation (minted - burnt).

**Returns**
* `[0]` (*uint256*) - The total number of tokens.
#### balanceOf

  ```solidity
  function balanceOf(address owner) external view returns (uint256)
  ```

  Returns the balance of a user.

**Parameters**
* `owner` (*address*) - The address whose balance is being retrieved.

**Returns**
* `[0]` (*uint256*) - The number of tokens owned by the user.
#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns how many tokens a user has allowed another user to transfer on its behalf.

**Parameters**
* `owner` (*address*) - The user who has given the allowance.
* `spender` (*address*) - The user who was given the allowance.

**Returns**
* `[0]` (*uint256*) - The amount of tokens `spender` can transfer on `owner`'s behalf.
#### transfer

  ```solidity
  function transfer(address to, uint256 amount) external returns (bool)
  ```

  Transfer tokens from one address to another.

**Parameters**
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The amount of tokens to be transferred.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### approve

  ```solidity
  function approve(address spender, uint256 amount) external returns (bool)
  ```

  Allows users to provide allowance to other users so that they can transfer tokens on their behalf.

**Parameters**
* `spender` (*address*) - The address that is receiving the allowance.
* `amount` (*uint256*) - The amount of tokens that are being added to the allowance.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### increaseAllowance

  ```solidity
  function increaseAllowance(address spender, uint256 addedValue) external returns (bool)
  ```

  Atomically increases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.

#### decreaseAllowance

  ```solidity
  function decreaseAllowance(address spender, uint256 subtractedValue) external returns (bool)
  ```

  Atomically decreases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least
`subtractedValue`.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 amount) external returns (bool)
  ```

  Allows a user who has been given allowance to transfer tokens on another user's behalf.

**Parameters**
* `from` (*address*) - The address that owns the tokens that are being transferred.
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The number of tokens to transfer.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 amount)
  ```

  Emitted when tokens have been transferred.

**Parameters**
* `from` (*address*) - The address that originally owned the tokens.
* `to` (*address*) - The address that received the tokens.
* `amount` (*uint256*) - The number of tokens that were transferred.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 amount)
  ```

  Emitted when a user has provided allowance to another user for transferring tokens on its behalf.

**Parameters**
* `owner` (*address*) - The address that is providing the allowance.
* `spender` (*address*) - The address that received the allowance.
* `amount` (*uint256*) - The number of tokens that were added to `spender`'s allowance.

### Vault Module

#### delegateCollateral

  ```solidity
  function delegateCollateral(uint128 accountId, uint128 poolId, address collateralType, uint256 amount, uint256 leverage) external
  ```

  Updates an account's delegated collateral amount for the specified pool and collateral type pair.

**Parameters**
* `accountId` (*uint128*) - The id of the account associated with the position that will be updated.
* `poolId` (*uint128*) - The id of the pool associated with the position.
* `collateralType` (*address*) - The address of the collateral used in the position.
* `amount` (*uint256*) - The new amount of collateral delegated in the position, denominated with 18 decimals of precision.
* `leverage` (*uint256*) - The new leverage amount used in the position, denominated with 18 decimals of precision. Requirements: - `ERC2771Context._msgSender()` must be the owner of the account, have the `ADMIN` permission, or have the `DELEGATE` permission. - If increasing the amount delegated, it must not exceed the available collateral (`getAccountAvailableCollateral`) associated with the account. - If decreasing the amount delegated, the liquidity position must have a collateralization ratio greater than the target collateralization ratio for the corresponding collateral type. Emits a {DelegationUpdated} event.

#### getPositionCollateralRatio

  ```solidity
  function getPositionCollateralRatio(uint128 accountId, uint128 poolId, address collateralType) external returns (uint256 ratioD18)
  ```

  Returns the collateralization ratio of the specified liquidity position. If debt is negative, this function will return 0.

  Call this function using `callStatic` to treat it as a view function.
The return value is a percentage with 18 decimals places.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose collateralization ratio is being queried.
* `poolId` (*uint128*) - The id of the pool in which the account's position is held.
* `collateralType` (*address*) - The address of the collateral used in the queried position.

**Returns**
* `ratioD18` (*uint256*) - The collateralization ratio of the position (collateral / debt), denominated with 18 decimals of precision.
#### getPositionDebt

  ```solidity
  function getPositionDebt(uint128 accountId, uint128 poolId, address collateralType) external returns (int256 debtD18)
  ```

  Returns the debt of the specified liquidity position. Credit is expressed as negative debt.

  This is not a view function, and actually updates the entire debt distribution chain.
Call this function using `callStatic` to treat it as a view function.

**Parameters**
* `accountId` (*uint128*) - The id of the account being queried.
* `poolId` (*uint128*) - The id of the pool in which the account's position is held.
* `collateralType` (*address*) - The address of the collateral used in the queried position.

**Returns**
* `debtD18` (*int256*) - The amount of debt held by the position, denominated with 18 decimals of precision.
#### getPositionCollateral

  ```solidity
  function getPositionCollateral(uint128 accountId, uint128 poolId, address collateralType) external view returns (uint256 collateralAmountD18)
  ```

  Returns the amount of the collateral associated with the specified liquidity position.

  Call this function using `callStatic` to treat it as a view function.
collateralAmount is represented as an integer with 18 decimals.

**Parameters**
* `accountId` (*uint128*) - The id of the account being queried.
* `poolId` (*uint128*) - The id of the pool in which the account's position is held.
* `collateralType` (*address*) - The address of the collateral used in the queried position.

**Returns**
* `collateralAmountD18` (*uint256*) - The amount of collateral used in the position, denominated with 18 decimals of precision.
#### getPosition

  ```solidity
  function getPosition(uint128 accountId, uint128 poolId, address collateralType) external returns (uint256 collateralAmountD18, uint256 collateralValueD18, int256 debtD18, uint256 collateralizationRatioD18)
  ```

  Returns all information pertaining to a specified liquidity position in the vault module.

**Parameters**
* `accountId` (*uint128*) - The id of the account being queried.
* `poolId` (*uint128*) - The id of the pool in which the account's position is held.
* `collateralType` (*address*) - The address of the collateral used in the queried position.

**Returns**
* `collateralAmountD18` (*uint256*) - The amount of collateral used in the position, denominated with 18 decimals of precision.
* `collateralValueD18` (*uint256*) - The value of the collateral used in the position, denominated with 18 decimals of precision.
* `debtD18` (*int256*) - The amount of debt held in the position, denominated with 18 decimals of precision.
* `collateralizationRatioD18` (*uint256*) - The collateralization ratio of the position (collateral / debt), denominated with 18 decimals of precision.
#### getVaultDebt

  ```solidity
  function getVaultDebt(uint128 poolId, address collateralType) external returns (int256 debtD18)
  ```

  Returns the total debt (or credit) that the vault is responsible for. Credit is expressed as negative debt.

  This is not a view function, and actually updates the entire debt distribution chain.
Call this function using `callStatic` to treat it as a view function.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that owns the vault whose debt is being queried.
* `collateralType` (*address*) - The address of the collateral of the associated vault.

**Returns**
* `debtD18` (*int256*) - The overall debt of the vault, denominated with 18 decimals of precision.
#### getVaultCollateral

  ```solidity
  function getVaultCollateral(uint128 poolId, address collateralType) external view returns (uint256 collateralAmountD18, uint256 collateralValueD18)
  ```

  Returns the amount and value of the collateral held by the vault.

  Call this function using `callStatic` to treat it as a view function.
collateralAmount is represented as an integer with 18 decimals.
collateralValue is represented as an integer with the number of decimals specified by the collateralType.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that owns the vault whose collateral is being queried.
* `collateralType` (*address*) - The address of the collateral of the associated vault.

**Returns**
* `collateralAmountD18` (*uint256*) - The collateral amount of the vault, denominated with 18 decimals of precision.
* `collateralValueD18` (*uint256*) - The collateral value of the vault, denominated with 18 decimals of precision.
#### getVaultCollateralRatio

  ```solidity
  function getVaultCollateralRatio(uint128 poolId, address collateralType) external returns (uint256 ratioD18)
  ```

  Returns the collateralization ratio of the vault. If debt is negative, this function will return 0.

  Call this function using `callStatic` to treat it as a view function.
The return value is a percentage with 18 decimals places.

**Parameters**
* `poolId` (*uint128*) - The id of the pool that owns the vault whose collateralization ratio is being queried.
* `collateralType` (*address*) - The address of the collateral of the associated vault.

**Returns**
* `ratioD18` (*uint256*) - The collateralization ratio of the vault, denominated with 18 decimals of precision.

#### DelegationUpdated

  ```solidity
  event DelegationUpdated(uint128 accountId, uint128 poolId, address collateralType, uint256 amount, uint256 leverage, address sender)
  ```

  Emitted when {sender} updates the delegation of collateral in the specified liquidity position.

**Parameters**
* `accountId` (*uint128*) - The id of the account whose position was updated.
* `poolId` (*uint128*) - The id of the pool in which the position was updated.
* `collateralType` (*address*) - The address of the collateral associated to the position.
* `amount` (*uint256*) - The new amount of the position, denominated with 18 decimals of precision.
* `leverage` (*uint256*) - The new leverage value of the position, denominated with 18 decimals of precision.
* `sender` (*address*) - The address that triggered the update of the position.

## Utility Core Contracts

### IConfigurable

#### acceptConfigurerRole

  ```solidity
  function acceptConfigurerRole() external
  ```

  Allows a nominated address to accept the configurer role of the contract.

  Reverts if the caller is not nominated.

#### nominateNewConfigurer

  ```solidity
  function nominateNewConfigurer(address newNominatedConfigurer) external
  ```

  Allows the current owner or configurer to nominate a new configurer.

  The nominated owner will have to call `acceptOwnership` in a separate transaction in order to finalize the action and become the new contract owner.

**Parameters**
* `newNominatedConfigurer` (*address*) - The address that is to become nominated.

#### renounceConfigurerNomination

  ```solidity
  function renounceConfigurerNomination() external
  ```

  Allows a nominated configurer to reject the nomination.

#### setConfigurer

  ```solidity
  function setConfigurer(address newConfigurer) external
  ```

  Allows the owner of the contract to set the configurer address.

#### configurer

  ```solidity
  function configurer() external view returns (address)
  ```

  Returns the current configurer of the contract.

#### nominatedConfigurer

  ```solidity
  function nominatedConfigurer() external view returns (address)
  ```

  Returns the current nominated configurer of the contract.

  Only one address can be nominated at a time.

#### ConfigurerNominated

  ```solidity
  event ConfigurerNominated(address newConfigurer)
  ```

  Emitted when an address has been nominated as configurer.

**Parameters**
* `newConfigurer` (*address*) - The address that has been nominated.

#### ConfigurerChanged

  ```solidity
  event ConfigurerChanged(address oldConfigurer, address newConfigurer)
  ```

  Emitted when the configurer of the contract has changed.

**Parameters**
* `oldConfigurer` (*address*) - The previous configurer of the contract.
* `newConfigurer` (*address*) - The new configurer of the contract.

### IERC165

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### IERC20

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Network Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Retrieves the number of decimals used by the token. The default is 18.

**Returns**
* `[0]` (*uint8*) - The number of decimals.
#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total number of tokens in circulation (minted - burnt).

**Returns**
* `[0]` (*uint256*) - The total number of tokens.
#### balanceOf

  ```solidity
  function balanceOf(address owner) external view returns (uint256)
  ```

  Returns the balance of a user.

**Parameters**
* `owner` (*address*) - The address whose balance is being retrieved.

**Returns**
* `[0]` (*uint256*) - The number of tokens owned by the user.
#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns how many tokens a user has allowed another user to transfer on its behalf.

**Parameters**
* `owner` (*address*) - The user who has given the allowance.
* `spender` (*address*) - The user who was given the allowance.

**Returns**
* `[0]` (*uint256*) - The amount of tokens `spender` can transfer on `owner`'s behalf.
#### transfer

  ```solidity
  function transfer(address to, uint256 amount) external returns (bool)
  ```

  Transfer tokens from one address to another.

**Parameters**
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The amount of tokens to be transferred.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### approve

  ```solidity
  function approve(address spender, uint256 amount) external returns (bool)
  ```

  Allows users to provide allowance to other users so that they can transfer tokens on their behalf.

**Parameters**
* `spender` (*address*) - The address that is receiving the allowance.
* `amount` (*uint256*) - The amount of tokens that are being added to the allowance.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### increaseAllowance

  ```solidity
  function increaseAllowance(address spender, uint256 addedValue) external returns (bool)
  ```

  Atomically increases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.

#### decreaseAllowance

  ```solidity
  function decreaseAllowance(address spender, uint256 subtractedValue) external returns (bool)
  ```

  Atomically decreases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least
`subtractedValue`.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 amount) external returns (bool)
  ```

  Allows a user who has been given allowance to transfer tokens on another user's behalf.

**Parameters**
* `from` (*address*) - The address that owns the tokens that are being transferred.
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The number of tokens to transfer.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 amount)
  ```

  Emitted when tokens have been transferred.

**Parameters**
* `from` (*address*) - The address that originally owned the tokens.
* `to` (*address*) - The address that received the tokens.
* `amount` (*uint256*) - The number of tokens that were transferred.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 amount)
  ```

  Emitted when a user has provided allowance to another user for transferring tokens on its behalf.

**Parameters**
* `owner` (*address*) - The address that is providing the allowance.
* `spender` (*address*) - The address that received the allowance.
* `amount` (*uint256*) - The number of tokens that were added to `spender`'s allowance.

### IERC20Permit

#### permit

  ```solidity
  function permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external
  ```

  Sets `value` as the allowance of `spender` over ``owner``'s tokens,
given ``owner``'s signed approval.

IMPORTANT: The same issues {IERC20-approve} has related to transaction
ordering also apply here.

Emits an {Approval} event.

Requirements:

- `spender` cannot be the zero address.
- `deadline` must be a timestamp in the future.
- `v`, `r` and `s` must be a valid `secp256k1` signature from `owner`
over the EIP712-formatted function arguments.
- the signature must use ``owner``'s current nonce (see {nonces}).

For more information on the signature format, see the
https://eips.ethereum.org/EIPS/eip-2612#specification[relevant EIP
section].

#### nonces

  ```solidity
  function nonces(address owner) external view returns (uint256)
  ```

  Returns the current nonce for `owner`. This value must be
included whenever a signature is generated for {permit}.

Every successful call to {permit} increases ``owner``'s nonce by one. This
prevents a signature from being used multiple times.

#### DOMAIN_SEPARATOR

  ```solidity
  function DOMAIN_SEPARATOR() external view returns (bytes32)
  ```

  Returns the domain separator used in the encoding of the signature for {permit}, as defined by {EIP712}.

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Network Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Retrieves the number of decimals used by the token. The default is 18.

**Returns**
* `[0]` (*uint8*) - The number of decimals.
#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total number of tokens in circulation (minted - burnt).

**Returns**
* `[0]` (*uint256*) - The total number of tokens.
#### balanceOf

  ```solidity
  function balanceOf(address owner) external view returns (uint256)
  ```

  Returns the balance of a user.

**Parameters**
* `owner` (*address*) - The address whose balance is being retrieved.

**Returns**
* `[0]` (*uint256*) - The number of tokens owned by the user.
#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns how many tokens a user has allowed another user to transfer on its behalf.

**Parameters**
* `owner` (*address*) - The user who has given the allowance.
* `spender` (*address*) - The user who was given the allowance.

**Returns**
* `[0]` (*uint256*) - The amount of tokens `spender` can transfer on `owner`'s behalf.
#### transfer

  ```solidity
  function transfer(address to, uint256 amount) external returns (bool)
  ```

  Transfer tokens from one address to another.

**Parameters**
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The amount of tokens to be transferred.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### approve

  ```solidity
  function approve(address spender, uint256 amount) external returns (bool)
  ```

  Allows users to provide allowance to other users so that they can transfer tokens on their behalf.

**Parameters**
* `spender` (*address*) - The address that is receiving the allowance.
* `amount` (*uint256*) - The amount of tokens that are being added to the allowance.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### increaseAllowance

  ```solidity
  function increaseAllowance(address spender, uint256 addedValue) external returns (bool)
  ```

  Atomically increases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.

#### decreaseAllowance

  ```solidity
  function decreaseAllowance(address spender, uint256 subtractedValue) external returns (bool)
  ```

  Atomically decreases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least
`subtractedValue`.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 amount) external returns (bool)
  ```

  Allows a user who has been given allowance to transfer tokens on another user's behalf.

**Parameters**
* `from` (*address*) - The address that owns the tokens that are being transferred.
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The number of tokens to transfer.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 amount)
  ```

  Emitted when tokens have been transferred.

**Parameters**
* `from` (*address*) - The address that originally owned the tokens.
* `to` (*address*) - The address that received the tokens.
* `amount` (*uint256*) - The number of tokens that were transferred.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 amount)
  ```

  Emitted when a user has provided allowance to another user for transferring tokens on its behalf.

**Parameters**
* `owner` (*address*) - The address that is providing the allowance.
* `spender` (*address*) - The address that received the allowance.
* `amount` (*uint256*) - The number of tokens that were added to `spender`'s allowance.

### IERC721

#### balanceOf

  ```solidity
  function balanceOf(address holder) external view returns (uint256 balance)
  ```

  Returns the number of tokens in ``owner``'s account.

Requirements:

- `holder` must be a valid address

#### ownerOf

  ```solidity
  function ownerOf(uint256 tokenId) external view returns (address owner)
  ```

  Returns the owner of the `tokenId` token.

Requirements:

- `tokenId` must exist.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId, bytes data) external
  ```

  Safely transfers `tokenId` token from `from` to `to`.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId) external
  ```

  Safely transfers `tokenId` token from `from` to `to`, checking first that contract recipients
are aware of the ERC721 protocol to prevent tokens from being forever locked.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must have been allowed to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 tokenId) external
  ```

  Transfers `tokenId` token from `from` to `to`.

WARNING: Usage of this method is discouraged, use {safeTransferFrom} whenever possible.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.

Emits a {Transfer} event.

#### approve

  ```solidity
  function approve(address to, uint256 tokenId) external
  ```

  Gives permission to `to` to transfer `tokenId` token to another account.
The approval is cleared when the token is transferred.

Only a single account can be approved at a time, so approving the zero address clears previous approvals.

Requirements:

- The caller must own the token or be an approved operator.
- `tokenId` must exist.

Emits an {Approval} event.

#### setApprovalForAll

  ```solidity
  function setApprovalForAll(address operator, bool approved) external
  ```

  Approve or remove `operator` as an operator for the caller.
Operators can call {transferFrom} or {safeTransferFrom} for any token owned by the caller.

Requirements:

- The `operator` cannot be the caller.

Emits an {ApprovalForAll} event.

#### getApproved

  ```solidity
  function getApproved(uint256 tokenId) external view returns (address operator)
  ```

  Returns the account approved for `tokenId` token.

Requirements:

- `tokenId` must exist.

#### isApprovedForAll

  ```solidity
  function isApprovedForAll(address owner, address operator) external view returns (bool)
  ```

  Returns if the `operator` is allowed to manage all of the assets of `owner`.

See {setApprovalForAll}

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 tokenId)
  ```

  Emitted when `tokenId` token is transferred from `from` to `to`.

#### Approval

  ```solidity
  event Approval(address owner, address approved, uint256 tokenId)
  ```

  Emitted when `owner` enables `approved` to manage the `tokenId` token.

#### ApprovalForAll

  ```solidity
  event ApprovalForAll(address owner, address operator, bool approved)
  ```

  Emitted when `owner` enables or disables (`approved`) `operator` to manage all of its assets.

### IERC721Enumerable

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total amount of tokens stored by the contract.

#### tokenOfOwnerByIndex

  ```solidity
  function tokenOfOwnerByIndex(address owner, uint256 index) external view returns (uint256)
  ```

  Returns a token ID owned by `owner` at a given `index` of its token list.
Use along with {balanceOf} to enumerate all of ``owner``'s tokens.

Requirements:
- `owner` must be a valid address
- `index` must be less than the balance of the tokens for the owner

#### tokenByIndex

  ```solidity
  function tokenByIndex(uint256 index) external view returns (uint256)
  ```

  Returns a token ID at a given `index` of all the tokens stored by the contract.
Use along with {totalSupply} to enumerate all tokens.

Requirements:
- `index` must be less than the total supply of the tokens

#### balanceOf

  ```solidity
  function balanceOf(address holder) external view returns (uint256 balance)
  ```

  Returns the number of tokens in ``owner``'s account.

Requirements:

- `holder` must be a valid address

#### ownerOf

  ```solidity
  function ownerOf(uint256 tokenId) external view returns (address owner)
  ```

  Returns the owner of the `tokenId` token.

Requirements:

- `tokenId` must exist.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId, bytes data) external
  ```

  Safely transfers `tokenId` token from `from` to `to`.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId) external
  ```

  Safely transfers `tokenId` token from `from` to `to`, checking first that contract recipients
are aware of the ERC721 protocol to prevent tokens from being forever locked.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must have been allowed to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 tokenId) external
  ```

  Transfers `tokenId` token from `from` to `to`.

WARNING: Usage of this method is discouraged, use {safeTransferFrom} whenever possible.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.

Emits a {Transfer} event.

#### approve

  ```solidity
  function approve(address to, uint256 tokenId) external
  ```

  Gives permission to `to` to transfer `tokenId` token to another account.
The approval is cleared when the token is transferred.

Only a single account can be approved at a time, so approving the zero address clears previous approvals.

Requirements:

- The caller must own the token or be an approved operator.
- `tokenId` must exist.

Emits an {Approval} event.

#### setApprovalForAll

  ```solidity
  function setApprovalForAll(address operator, bool approved) external
  ```

  Approve or remove `operator` as an operator for the caller.
Operators can call {transferFrom} or {safeTransferFrom} for any token owned by the caller.

Requirements:

- The `operator` cannot be the caller.

Emits an {ApprovalForAll} event.

#### getApproved

  ```solidity
  function getApproved(uint256 tokenId) external view returns (address operator)
  ```

  Returns the account approved for `tokenId` token.

Requirements:

- `tokenId` must exist.

#### isApprovedForAll

  ```solidity
  function isApprovedForAll(address owner, address operator) external view returns (bool)
  ```

  Returns if the `operator` is allowed to manage all of the assets of `owner`.

See {setApprovalForAll}

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 tokenId)
  ```

  Emitted when `tokenId` token is transferred from `from` to `to`.

#### Approval

  ```solidity
  event Approval(address owner, address approved, uint256 tokenId)
  ```

  Emitted when `owner` enables `approved` to manage the `tokenId` token.

#### ApprovalForAll

  ```solidity
  event ApprovalForAll(address owner, address operator, bool approved)
  ```

  Emitted when `owner` enables or disables (`approved`) `operator` to manage all of its assets.

### IERC721Metadata

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Account Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX-ACC".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### tokenURI

  ```solidity
  function tokenURI(uint256 tokenId) external view returns (string)
  ```

  Retrieves the off-chain URI where the specified token id may contain associated data, such as images, audio, etc.

**Parameters**
* `tokenId` (*uint256*) - The numeric id of the token in question.

**Returns**
* `[0]` (*string*) - The URI of the token in question.
#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### IERC721Receiver

#### onERC721Received

  ```solidity
  function onERC721Received(address operator, address from, uint256 tokenId, bytes data) external returns (bytes4)
  ```

  Function that will be called by ERC721 tokens implementing the `safeTransferFrom` function.

  The contract transferring the token will revert if the receiving contract does not implement this function.

**Parameters**
* `operator` (*address*) - The address that is executing the transfer.
* `from` (*address*) - The address whose token is being transferred.
* `tokenId` (*uint256*) - The numeric id of the token being transferred.
* `data` (*bytes*) - Optional additional data that may be passed by the operator, and could be used by the implementing contract.

**Returns**
* `[0]` (*bytes4*) - The selector of this function (IERC721Receiver.onERC721Received.selector). Caller will revert if not returned.

### IOwnable

#### acceptOwnership

  ```solidity
  function acceptOwnership() external
  ```

  Allows a nominated address to accept ownership of the contract.

  Reverts if the caller is not nominated.

#### nominateNewOwner

  ```solidity
  function nominateNewOwner(address newNominatedOwner) external
  ```

  Allows the current owner to nominate a new owner.

  The nominated owner will have to call `acceptOwnership` in a separate transaction in order to finalize the action and become the new contract owner.

**Parameters**
* `newNominatedOwner` (*address*) - The address that is to become nominated.

#### renounceNomination

  ```solidity
  function renounceNomination() external
  ```

  Allows a nominated owner to reject the nomination.

#### owner

  ```solidity
  function owner() external view returns (address)
  ```

  Returns the current owner of the contract.

#### nominatedOwner

  ```solidity
  function nominatedOwner() external view returns (address)
  ```

  Returns the current nominated owner of the contract.

  Only one address can be nominated at a time.

#### OwnerNominated

  ```solidity
  event OwnerNominated(address newOwner)
  ```

  Emitted when an address has been nominated.

**Parameters**
* `newOwner` (*address*) - The address that has been nominated.

#### OwnerChanged

  ```solidity
  event OwnerChanged(address oldOwner, address newOwner)
  ```

  Emitted when the owner of the contract has changed.

**Parameters**
* `oldOwner` (*address*) - The previous owner of the contract.
* `newOwner` (*address*) - The new owner of the contract.

### IUUPSImplementation

#### upgradeTo

  ```solidity
  function upgradeTo(address newImplementation) external
  ```

  Allows the proxy to be upgraded to a new implementation.

  Will revert if `newImplementation` is not upgradeable.
The implementation of this function needs to be protected by some sort of access control such as `onlyOwner`.

**Parameters**
* `newImplementation` (*address*) - The address of the proxy's new implementation.

#### simulateUpgradeTo

  ```solidity
  function simulateUpgradeTo(address newImplementation) external
  ```

  Function used to determine if a new implementation will be able to receive future upgrades in `upgradeTo`.

  This function will always revert, but will revert with different error messages. The function `upgradeTo` uses this error to determine the future upgradeability of the implementation in question.

**Parameters**
* `newImplementation` (*address*) - The address of the new implementation being tested for future upgradeability.

#### getImplementation

  ```solidity
  function getImplementation() external view returns (address)
  ```

  Retrieves the current implementation of the proxy.

**Returns**
* `[0]` (*address*) - The address of the current implementation.

#### Upgraded

  ```solidity
  event Upgraded(address self, address implementation)
  ```

  Emitted when the implementation of the proxy has been upgraded.

**Parameters**
* `self` (*address*) - The address of the proxy whose implementation was upgraded.
* `implementation` (*address*) - The address of the proxy's new implementation.

## Utility Core Modules

### Associated Systems Module

#### initOrUpgradeToken

  ```solidity
  function initOrUpgradeToken(bytes32 id, string name, string symbol, uint8 decimals, address impl) external
  ```

  Creates or initializes a managed associated ERC20 token.

**Parameters**
* `id` (*bytes32*) - The bytes32 identifier of the associated system. If the id is new to the system, it will create a new proxy for the associated system.
* `name` (*string*) - The token name that will be used to initialize the proxy.
* `symbol` (*string*) - The token symbol that will be used to initialize the proxy.
* `decimals` (*uint8*) - The token decimals that will be used to initialize the proxy.
* `impl` (*address*) - The ERC20 implementation of the proxy.

#### initOrUpgradeNft

  ```solidity
  function initOrUpgradeNft(bytes32 id, string name, string symbol, string uri, address impl) external
  ```

  Creates or initializes a managed associated ERC721 token.

**Parameters**
* `id` (*bytes32*) - The bytes32 identifier of the associated system. If the id is new to the system, it will create a new proxy for the associated system.
* `name` (*string*) - The token name that will be used to initialize the proxy.
* `symbol` (*string*) - The token symbol that will be used to initialize the proxy.
* `uri` (*string*) - The token uri that will be used to initialize the proxy.
* `impl` (*address*) - The ERC721 implementation of the proxy.

#### registerUnmanagedSystem

  ```solidity
  function registerUnmanagedSystem(bytes32 id, address endpoint) external
  ```

  Registers an unmanaged external contract in the system.

**Parameters**
* `id` (*bytes32*) - The bytes32 identifier to use to reference the associated system.
* `endpoint` (*address*) - The address of the associated system. Note: The system will not be able to control or upgrade the associated system, only communicate with it.

#### getAssociatedSystem

  ```solidity
  function getAssociatedSystem(bytes32 id) external view returns (address addr, bytes32 kind)
  ```

  Retrieves an associated system.

**Parameters**
* `id` (*bytes32*) - The bytes32 identifier used to reference the associated system.

**Returns**
* `addr` (*address*) - The external contract address of the associated system.
* `kind` (*bytes32*) - The type of associated system (managed ERC20, managed ERC721, unmanaged, etc - See the AssociatedSystem util).

#### AssociatedSystemSet

  ```solidity
  event AssociatedSystemSet(bytes32 kind, bytes32 id, address proxy, address impl)
  ```

  Emitted when an associated system is set.

**Parameters**
* `kind` (*bytes32*) - The type of associated system (managed ERC20, managed ERC721, unmanaged, etc - See the AssociatedSystem util).
* `id` (*bytes32*) - The bytes32 identifier of the associated system.
* `proxy` (*address*) - The main external contract address of the associated system.
* `impl` (*address*) - The address of the implementation of the associated system (if not behind a proxy, will equal `proxy`).

### Decay Token Module

#### setDecayRate

  ```solidity
  function setDecayRate(uint256 _rate) external
  ```

  Updates the decay rate for a year

**Parameters**
* `_rate` (*uint256*) - The decay rate with 18 decimals (1e16 means 1% decay per year).

#### decayRate

  ```solidity
  function decayRate() external view returns (uint256)
  ```

  get decay rate for a year

#### advanceEpoch

  ```solidity
  function advanceEpoch() external returns (uint256)
  ```

  advance epoch manually in order to avoid precision loss

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns wether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, uint8 tokenDecimals) external
  ```

  Initializes the token with name, symbol, and decimals.

#### mint

  ```solidity
  function mint(address to, uint256 amount) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `amount` (*uint256*) - The amount of tokens to mint.

#### burn

  ```solidity
  function burn(address from, uint256 amount) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `from` (*address*) - The address whose tokens will be burnt.
* `amount` (*uint256*) - The amount of tokens to burn.

#### setAllowance

  ```solidity
  function setAllowance(address from, address spender, uint256 amount) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `from` (*address*) - The address that is providing allowance.
* `spender` (*address*) - The address that is given allowance.
* `amount` (*uint256*) - The amount of allowance being given.

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Network Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Retrieves the number of decimals used by the token. The default is 18.

**Returns**
* `[0]` (*uint8*) - The number of decimals.
#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total number of tokens in circulation (minted - burnt).

**Returns**
* `[0]` (*uint256*) - The total number of tokens.
#### balanceOf

  ```solidity
  function balanceOf(address owner) external view returns (uint256)
  ```

  Returns the balance of a user.

**Parameters**
* `owner` (*address*) - The address whose balance is being retrieved.

**Returns**
* `[0]` (*uint256*) - The number of tokens owned by the user.
#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns how many tokens a user has allowed another user to transfer on its behalf.

**Parameters**
* `owner` (*address*) - The user who has given the allowance.
* `spender` (*address*) - The user who was given the allowance.

**Returns**
* `[0]` (*uint256*) - The amount of tokens `spender` can transfer on `owner`'s behalf.
#### transfer

  ```solidity
  function transfer(address to, uint256 amount) external returns (bool)
  ```

  Transfer tokens from one address to another.

**Parameters**
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The amount of tokens to be transferred.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### approve

  ```solidity
  function approve(address spender, uint256 amount) external returns (bool)
  ```

  Allows users to provide allowance to other users so that they can transfer tokens on their behalf.

**Parameters**
* `spender` (*address*) - The address that is receiving the allowance.
* `amount` (*uint256*) - The amount of tokens that are being added to the allowance.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### increaseAllowance

  ```solidity
  function increaseAllowance(address spender, uint256 addedValue) external returns (bool)
  ```

  Atomically increases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.

#### decreaseAllowance

  ```solidity
  function decreaseAllowance(address spender, uint256 subtractedValue) external returns (bool)
  ```

  Atomically decreases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least
`subtractedValue`.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 amount) external returns (bool)
  ```

  Allows a user who has been given allowance to transfer tokens on another user's behalf.

**Parameters**
* `from` (*address*) - The address that owns the tokens that are being transferred.
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The number of tokens to transfer.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 amount)
  ```

  Emitted when tokens have been transferred.

**Parameters**
* `from` (*address*) - The address that originally owned the tokens.
* `to` (*address*) - The address that received the tokens.
* `amount` (*uint256*) - The number of tokens that were transferred.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 amount)
  ```

  Emitted when a user has provided allowance to another user for transferring tokens on its behalf.

**Parameters**
* `owner` (*address*) - The address that is providing the allowance.
* `spender` (*address*) - The address that received the allowance.
* `amount` (*uint256*) - The number of tokens that were added to `spender`'s allowance.

### Feature Flag Module

#### setFeatureFlagAllowAll

  ```solidity
  function setFeatureFlagAllowAll(bytes32 feature, bool allowAll) external
  ```

  Enables or disables free access to a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `allowAll` (*bool*) - True to allow anyone to use the feature, false to fallback to the allowlist.

#### setFeatureFlagDenyAll

  ```solidity
  function setFeatureFlagDenyAll(bytes32 feature, bool denyAll) external
  ```

  Enables or disables free access to a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `denyAll` (*bool*) - True to allow noone to use the feature, false to fallback to the allowlist.

#### addToFeatureFlagAllowlist

  ```solidity
  function addToFeatureFlagAllowlist(bytes32 feature, address account) external
  ```

  Allows an address to use a feature.

  This function does nothing if the specified account is already on the allowlist.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that is allowed to use the feature.

#### removeFromFeatureFlagAllowlist

  ```solidity
  function removeFromFeatureFlagAllowlist(bytes32 feature, address account) external
  ```

  Disallows an address from using a feature.

  This function does nothing if the specified account is already on the allowlist.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that is disallowed from using the feature.

#### setDeniers

  ```solidity
  function setDeniers(bytes32 feature, address[] deniers) external
  ```

  Sets addresses which can disable a feature (but not enable it). Overwrites any preexisting data.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `deniers` (*address[]*) - The addresses which should have the ability to unilaterally disable the feature

#### getDeniers

  ```solidity
  function getDeniers(bytes32 feature) external view returns (address[])
  ```

  Gets the list of address which can block a feature

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

#### getFeatureFlagAllowAll

  ```solidity
  function getFeatureFlagAllowAll(bytes32 feature) external view returns (bool)
  ```

  Determines if the given feature is freely allowed to all users.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

**Returns**
* `[0]` (*bool*) - True if anyone is allowed to use the feature, false if per-user control is used.
#### getFeatureFlagDenyAll

  ```solidity
  function getFeatureFlagDenyAll(bytes32 feature) external view returns (bool)
  ```

  Determines if the given feature is denied to all users.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

**Returns**
* `[0]` (*bool*) - True if noone is allowed to use the feature.
#### getFeatureFlagAllowlist

  ```solidity
  function getFeatureFlagAllowlist(bytes32 feature) external view returns (address[])
  ```

  Returns a list of addresses that are allowed to use the specified feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

**Returns**
* `[0]` (*address[]*) - The queried list of addresses.
#### isFeatureAllowed

  ```solidity
  function isFeatureAllowed(bytes32 feature, address account) external view returns (bool)
  ```

  Determines if an address can use the specified feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that is being queried for access to the feature.

**Returns**
* `[0]` (*bool*) - A boolean with the response to the query.

#### FeatureFlagAllowAllSet

  ```solidity
  event FeatureFlagAllowAllSet(bytes32 feature, bool allowAll)
  ```

  Emitted when general access has been given or removed for a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `allowAll` (*bool*) - True if the feature was allowed for everyone and false if it is only allowed for those included in the allowlist.

#### FeatureFlagDenyAllSet

  ```solidity
  event FeatureFlagDenyAllSet(bytes32 feature, bool denyAll)
  ```

  Emitted when general access has been blocked for a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `denyAll` (*bool*) - True if the feature was blocked for everyone and false if it is only allowed for those included in the allowlist or if allowAll is set to true.

#### FeatureFlagAllowlistAdded

  ```solidity
  event FeatureFlagAllowlistAdded(bytes32 feature, address account)
  ```

  Emitted when an address was given access to a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that was given access to the feature.

#### FeatureFlagAllowlistRemoved

  ```solidity
  event FeatureFlagAllowlistRemoved(bytes32 feature, address account)
  ```

  Emitted when access to a feature has been removed from an address.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that no longer has access to the feature.

#### FeatureFlagDeniersReset

  ```solidity
  event FeatureFlagDeniersReset(bytes32 feature, address[] deniers)
  ```

  Emitted when the list of addresses which can block a feature has been updated

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `deniers` (*address[]*) - The list of addresses which are allowed to block a feature

### Nft Module

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns whether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, string uri) external
  ```

  Initializes the token with name, symbol, and uri.

#### mint

  ```solidity
  function mint(address to, uint256 tokenId) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `tokenId` (*uint256*) - The ID of the newly minted token

#### safeMint

  ```solidity
  function safeMint(address to, uint256 tokenId, bytes data) external
  ```

  Allows the owner to mint tokens. Verifies that the receiver can receive the token

**Parameters**
* `to` (*address*) - The address to receive the newly minted token.
* `tokenId` (*uint256*) - The ID of the newly minted token
* `data` (*bytes*) - any data which should be sent to the receiver

#### burn

  ```solidity
  function burn(uint256 tokenId) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `tokenId` (*uint256*) - The token to burn

#### setAllowance

  ```solidity
  function setAllowance(uint256 tokenId, address spender) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `tokenId` (*uint256*) - The token which should be allowed to spender
* `spender` (*address*) - The address that is given allowance.

#### setBaseTokenURI

  ```solidity
  function setBaseTokenURI(string uri) external
  ```

  Allows the owner to update the base token URI.

**Parameters**
* `uri` (*string*) - The new base token uri

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total amount of tokens stored by the contract.

#### tokenOfOwnerByIndex

  ```solidity
  function tokenOfOwnerByIndex(address owner, uint256 index) external view returns (uint256)
  ```

  Returns a token ID owned by `owner` at a given `index` of its token list.
Use along with {balanceOf} to enumerate all of ``owner``'s tokens.

Requirements:
- `owner` must be a valid address
- `index` must be less than the balance of the tokens for the owner

#### tokenByIndex

  ```solidity
  function tokenByIndex(uint256 index) external view returns (uint256)
  ```

  Returns a token ID at a given `index` of all the tokens stored by the contract.
Use along with {totalSupply} to enumerate all tokens.

Requirements:
- `index` must be less than the total supply of the tokens

#### balanceOf

  ```solidity
  function balanceOf(address holder) external view returns (uint256 balance)
  ```

  Returns the number of tokens in ``owner``'s account.

Requirements:

- `holder` must be a valid address

#### ownerOf

  ```solidity
  function ownerOf(uint256 tokenId) external view returns (address owner)
  ```

  Returns the owner of the `tokenId` token.

Requirements:

- `tokenId` must exist.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId, bytes data) external
  ```

  Safely transfers `tokenId` token from `from` to `to`.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId) external
  ```

  Safely transfers `tokenId` token from `from` to `to`, checking first that contract recipients
are aware of the ERC721 protocol to prevent tokens from being forever locked.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must have been allowed to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 tokenId) external
  ```

  Transfers `tokenId` token from `from` to `to`.

WARNING: Usage of this method is discouraged, use {safeTransferFrom} whenever possible.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.

Emits a {Transfer} event.

#### approve

  ```solidity
  function approve(address to, uint256 tokenId) external
  ```

  Gives permission to `to` to transfer `tokenId` token to another account.
The approval is cleared when the token is transferred.

Only a single account can be approved at a time, so approving the zero address clears previous approvals.

Requirements:

- The caller must own the token or be an approved operator.
- `tokenId` must exist.

Emits an {Approval} event.

#### setApprovalForAll

  ```solidity
  function setApprovalForAll(address operator, bool approved) external
  ```

  Approve or remove `operator` as an operator for the caller.
Operators can call {transferFrom} or {safeTransferFrom} for any token owned by the caller.

Requirements:

- The `operator` cannot be the caller.

Emits an {ApprovalForAll} event.

#### getApproved

  ```solidity
  function getApproved(uint256 tokenId) external view returns (address operator)
  ```

  Returns the account approved for `tokenId` token.

Requirements:

- `tokenId` must exist.

#### isApprovedForAll

  ```solidity
  function isApprovedForAll(address owner, address operator) external view returns (bool)
  ```

  Returns if the `operator` is allowed to manage all of the assets of `owner`.

See {setApprovalForAll}

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 tokenId)
  ```

  Emitted when `tokenId` token is transferred from `from` to `to`.

#### Approval

  ```solidity
  event Approval(address owner, address approved, uint256 tokenId)
  ```

  Emitted when `owner` enables `approved` to manage the `tokenId` token.

#### ApprovalForAll

  ```solidity
  event ApprovalForAll(address owner, address operator, bool approved)
  ```

  Emitted when `owner` enables or disables (`approved`) `operator` to manage all of its assets.

### Owner Module

### Sample Feature Flag Module

#### setFeatureFlaggedValue

  ```solidity
  function setFeatureFlaggedValue(uint256 valueToSet) external
  ```

#### getFeatureFlaggedValue

  ```solidity
  function getFeatureFlaggedValue() external view returns (uint256)
  ```

### Sample Owned Module

#### setProtectedValue

  ```solidity
  function setProtectedValue(uint256 newProtectedValue) external payable
  ```

#### getProtectedValue

  ```solidity
  function getProtectedValue() external view returns (uint256)
  ```

### Token Module

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns wether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, uint8 tokenDecimals) external
  ```

  Initializes the token with name, symbol, and decimals.

#### mint

  ```solidity
  function mint(address to, uint256 amount) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `amount` (*uint256*) - The amount of tokens to mint.

#### burn

  ```solidity
  function burn(address from, uint256 amount) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `from` (*address*) - The address whose tokens will be burnt.
* `amount` (*uint256*) - The amount of tokens to burn.

#### setAllowance

  ```solidity
  function setAllowance(address from, address spender, uint256 amount) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `from` (*address*) - The address that is providing allowance.
* `spender` (*address*) - The address that is given allowance.
* `amount` (*uint256*) - The amount of allowance being given.

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Network Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Retrieves the number of decimals used by the token. The default is 18.

**Returns**
* `[0]` (*uint8*) - The number of decimals.
#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total number of tokens in circulation (minted - burnt).

**Returns**
* `[0]` (*uint256*) - The total number of tokens.
#### balanceOf

  ```solidity
  function balanceOf(address owner) external view returns (uint256)
  ```

  Returns the balance of a user.

**Parameters**
* `owner` (*address*) - The address whose balance is being retrieved.

**Returns**
* `[0]` (*uint256*) - The number of tokens owned by the user.
#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns how many tokens a user has allowed another user to transfer on its behalf.

**Parameters**
* `owner` (*address*) - The user who has given the allowance.
* `spender` (*address*) - The user who was given the allowance.

**Returns**
* `[0]` (*uint256*) - The amount of tokens `spender` can transfer on `owner`'s behalf.
#### transfer

  ```solidity
  function transfer(address to, uint256 amount) external returns (bool)
  ```

  Transfer tokens from one address to another.

**Parameters**
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The amount of tokens to be transferred.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### approve

  ```solidity
  function approve(address spender, uint256 amount) external returns (bool)
  ```

  Allows users to provide allowance to other users so that they can transfer tokens on their behalf.

**Parameters**
* `spender` (*address*) - The address that is receiving the allowance.
* `amount` (*uint256*) - The amount of tokens that are being added to the allowance.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### increaseAllowance

  ```solidity
  function increaseAllowance(address spender, uint256 addedValue) external returns (bool)
  ```

  Atomically increases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.

#### decreaseAllowance

  ```solidity
  function decreaseAllowance(address spender, uint256 subtractedValue) external returns (bool)
  ```

  Atomically decreases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least
`subtractedValue`.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 amount) external returns (bool)
  ```

  Allows a user who has been given allowance to transfer tokens on another user's behalf.

**Parameters**
* `from` (*address*) - The address that owns the tokens that are being transferred.
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The number of tokens to transfer.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 amount)
  ```

  Emitted when tokens have been transferred.

**Parameters**
* `from` (*address*) - The address that originally owned the tokens.
* `to` (*address*) - The address that received the tokens.
* `amount` (*uint256*) - The number of tokens that were transferred.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 amount)
  ```

  Emitted when a user has provided allowance to another user for transferring tokens on its behalf.

**Parameters**
* `owner` (*address*) - The address that is providing the allowance.
* `spender` (*address*) - The address that received the allowance.
* `amount` (*uint256*) - The number of tokens that were added to `spender`'s allowance.

### IWormhole

#### publishMessage

  ```solidity
  function publishMessage(uint32 nonce, bytes payload, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

#### initialize

  ```solidity
  function initialize() external
  ```

#### parseAndVerifyVM

  ```solidity
  function parseAndVerifyVM(bytes encodedVM) external view returns (struct IWormhole.VM vm, bool valid, string reason)
  ```

#### verifyVM

  ```solidity
  function verifyVM(struct IWormhole.VM vm) external view returns (bool valid, string reason)
  ```

#### verifySignatures

  ```solidity
  function verifySignatures(bytes32 hash, struct IWormhole.Signature[] signatures, struct IWormhole.GuardianSet guardianSet) external pure returns (bool valid, string reason)
  ```

#### parseVM

  ```solidity
  function parseVM(bytes encodedVM) external pure returns (struct IWormhole.VM vm)
  ```

#### quorum

  ```solidity
  function quorum(uint256 numGuardians) external pure returns (uint256 numSignaturesRequiredForQuorum)
  ```

#### getGuardianSet

  ```solidity
  function getGuardianSet(uint32 index) external view returns (struct IWormhole.GuardianSet)
  ```

#### getCurrentGuardianSetIndex

  ```solidity
  function getCurrentGuardianSetIndex() external view returns (uint32)
  ```

#### getGuardianSetExpiry

  ```solidity
  function getGuardianSetExpiry() external view returns (uint32)
  ```

#### governanceActionIsConsumed

  ```solidity
  function governanceActionIsConsumed(bytes32 hash) external view returns (bool)
  ```

#### isInitialized

  ```solidity
  function isInitialized(address impl) external view returns (bool)
  ```

#### chainId

  ```solidity
  function chainId() external view returns (uint16)
  ```

#### isFork

  ```solidity
  function isFork() external view returns (bool)
  ```

#### governanceChainId

  ```solidity
  function governanceChainId() external view returns (uint16)
  ```

#### governanceContract

  ```solidity
  function governanceContract() external view returns (bytes32)
  ```

#### messageFee

  ```solidity
  function messageFee() external view returns (uint256)
  ```

#### evmChainId

  ```solidity
  function evmChainId() external view returns (uint256)
  ```

#### nextSequence

  ```solidity
  function nextSequence(address emitter) external view returns (uint64)
  ```

#### parseContractUpgrade

  ```solidity
  function parseContractUpgrade(bytes encodedUpgrade) external pure returns (struct IWormhole.ContractUpgrade cu)
  ```

#### parseGuardianSetUpgrade

  ```solidity
  function parseGuardianSetUpgrade(bytes encodedUpgrade) external pure returns (struct IWormhole.GuardianSetUpgrade gsu)
  ```

#### parseSetMessageFee

  ```solidity
  function parseSetMessageFee(bytes encodedSetMessageFee) external pure returns (struct IWormhole.SetMessageFee smf)
  ```

#### parseTransferFees

  ```solidity
  function parseTransferFees(bytes encodedTransferFees) external pure returns (struct IWormhole.TransferFees tf)
  ```

#### parseRecoverChainId

  ```solidity
  function parseRecoverChainId(bytes encodedRecoverChainId) external pure returns (struct IWormhole.RecoverChainId rci)
  ```

#### submitContractUpgrade

  ```solidity
  function submitContractUpgrade(bytes _vm) external
  ```

#### submitSetMessageFee

  ```solidity
  function submitSetMessageFee(bytes _vm) external
  ```

#### submitNewGuardianSet

  ```solidity
  function submitNewGuardianSet(bytes _vm) external
  ```

#### submitTransferFees

  ```solidity
  function submitTransferFees(bytes _vm) external
  ```

#### submitRecoverChainId

  ```solidity
  function submitRecoverChainId(bytes _vm) external
  ```

#### LogMessagePublished

  ```solidity
  event LogMessagePublished(address sender, uint64 sequence, uint32 nonce, bytes payload, uint8 consistencyLevel)
  ```

#### ContractUpgraded

  ```solidity
  event ContractUpgraded(address oldContract, address newContract)
  ```

#### GuardianSetAdded

  ```solidity
  event GuardianSetAdded(uint32 index)
  ```

### IWormholeReceiver

#### receiveWormholeMessages

  ```solidity
  function receiveWormholeMessages(bytes payload, bytes[] additionalMessages, bytes32 sourceAddress, uint16 sourceChain, bytes32 deliveryHash) external payable
  ```

  When a `send` is performed with this contract as the target, this function will be
    invoked by the WormholeRelayer contract

NOTE: This function should be restricted such that only the Wormhole Relayer contract can call it.

We also recommend that this function checks that `sourceChain` and `sourceAddress` are indeed who
      you expect to have requested the calling of `send` on the source chain

The invocation of this function corresponding to the `send` request will have msg.value equal
  to the receiverValue specified in the send request.

If the invocation of this function reverts or exceeds the gas limit
  specified by the send requester, this delivery will result in a `ReceiverFailure`.

**Parameters**
* `payload` (*bytes*) - - an arbitrary message which was included in the delivery by the     requester. This message's signature will already have been verified (as long as msg.sender is the Wormhole Relayer contract)
* `additionalMessages` (*bytes[]*) - - Additional messages which were requested to be included in this delivery.      Note: There are no contract-level guarantees that the messages in this array are what was requested      so **you should verify any sensitive information given here!**      For example, if a 'VaaKey' was specified on the source chain, then MAKE SURE the corresponding message here      has valid signatures (by calling `parseAndVerifyVM(message)` on the Wormhole core contract)      This field can be used to perform and relay TokenBridge or CCTP transfers, and there are example      usages of this at         https://github.com/wormhole-foundation/hello-token         https://github.com/wormhole-foundation/hello-cctp
* `sourceAddress` (*bytes32*) - - the (wormhole format) address on the sending chain which requested     this delivery.
* `sourceChain` (*uint16*) - - the wormhole chain ID where this delivery was requested.
* `deliveryHash` (*bytes32*) - - the VAA hash of the deliveryVAA.

### VaaKey

  VaaKey identifies a wormhole message

```solidity
struct VaaKey {
  uint16 chainId;
  bytes32 emitterAddress;
  uint64 sequence;
}
```

### VAA_KEY_TYPE

  ```solidity
  uint8 VAA_KEY_TYPE
  ```

### MessageKey

```solidity
struct MessageKey {
  uint8 keyType;
  bytes encodedKey;
}
```

### IWormholeRelayerBase

#### getRegisteredWormholeRelayerContract

  ```solidity
  function getRegisteredWormholeRelayerContract(uint16 chainId) external view returns (bytes32)
  ```

#### deliveryAttempted

  ```solidity
  function deliveryAttempted(bytes32 deliveryHash) external view returns (bool attempted)
  ```

  Returns true if a delivery has been attempted for the given deliveryHash
Note: invalid deliveries where the tx reverts are not considered attempted

#### deliverySuccessBlock

  ```solidity
  function deliverySuccessBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number at which a delivery was successfully executed

#### deliveryFailureBlock

  ```solidity
  function deliveryFailureBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number of the latest attempt to execute a delivery that failed

#### SendEvent

  ```solidity
  event SendEvent(uint64 sequence, uint256 deliveryQuote, uint256 paymentForExtraReceiverValue)
  ```

### IWormholeRelayerSend

#### sendPayloadToEvm

  ```solidity
  function sendPayloadToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

Any refunds (from leftover gas) will be paid to the delivery provider. In order to receive the refunds, use the `sendPayloadToEvm` function
with `refundChain` and `refundAddress` as parameters

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendPayloadToEvm

  ```solidity
  function sendPayloadToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit, uint16 refundChain, address refundAddress) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendVaasToEvm

  ```solidity
  function sendVaasToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit, struct VaaKey[] vaaKeys) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

Any refunds (from leftover gas) will be paid to the delivery provider. In order to receive the refunds, use the `sendVaasToEvm` function
with `refundChain` and `refundAddress` as parameters

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendVaasToEvm

  ```solidity
  function sendVaasToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit, struct VaaKey[] vaaKeys, uint16 refundChain, address refundAddress) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendToEvm

  ```solidity
  function sendToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, uint256 gasLimit, uint16 refundChain, address refundAddress, address deliveryProviderAddress, struct VaaKey[] vaaKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit, deliveryProviderAddress) + paymentForExtraReceiverValue

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendToEvm

  ```solidity
  function sendToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, uint256 gasLimit, uint16 refundChain, address refundAddress, address deliveryProviderAddress, struct MessageKey[] messageKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and external messages specified by `messageKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit, deliveryProviderAddress) + paymentForExtraReceiverValue

Note: MessageKeys can specify wormhole messages (VaaKeys) or other types of messages (ex. USDC CCTP attestations). Ensure the selected
DeliveryProvider supports all the MessageKey.keyType values specified or it will not be delivered!

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `messageKeys` (*struct MessageKey[]*) - Additional messagess to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### send

  ```solidity
  function send(uint16 targetChain, bytes32 targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, bytes encodedExecutionParameters, uint16 refundChain, bytes32 refundAddress, address deliveryProviderAddress, struct VaaKey[] vaaKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteDeliveryPrice(targetChain, receiverValue, encodedExecutionParameters, deliveryProviderAddress) + paymentForExtraReceiverValue

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*bytes32*) - address to call on targetChain (that implements IWormholeReceiver), in Wormhole bytes32 format
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `encodedExecutionParameters` (*bytes*) - encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*bytes32*) - The address on `refundChain` to deliver any refund to, in Wormhole bytes32 format
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### send

  ```solidity
  function send(uint16 targetChain, bytes32 targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, bytes encodedExecutionParameters, uint16 refundChain, bytes32 refundAddress, address deliveryProviderAddress, struct MessageKey[] messageKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteDeliveryPrice(targetChain, receiverValue, encodedExecutionParameters, deliveryProviderAddress) + paymentForExtraReceiverValue

Note: MessageKeys can specify wormhole messages (VaaKeys) or other types of messages (ex. USDC CCTP attestations). Ensure the selected
DeliveryProvider supports all the MessageKey.keyType values specified or it will not be delivered!

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*bytes32*) - address to call on targetChain (that implements IWormholeReceiver), in Wormhole bytes32 format
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `encodedExecutionParameters` (*bytes*) - encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*bytes32*) - The address on `refundChain` to deliver any refund to, in Wormhole bytes32 format
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `messageKeys` (*struct MessageKey[]*) - Additional messagess to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### resendToEvm

  ```solidity
  function resendToEvm(struct VaaKey deliveryVaaKey, uint16 targetChain, uint256 newReceiverValue, uint256 newGasLimit, address newDeliveryProviderAddress) external payable returns (uint64 sequence)
  ```

  Requests a previously published delivery instruction to be redelivered
(e.g. with a different delivery provider)

This function must be called with `msg.value` equal to
quoteEVMDeliveryPrice(targetChain, newReceiverValue, newGasLimit, newDeliveryProviderAddress)

 @notice *** This will only be able to succeed if the following is true **
        - newGasLimit >= gas limit of the old instruction
        - newReceiverValue >= receiver value of the old instruction
        - newDeliveryProvider's `targetChainRefundPerGasUnused` >= old relay provider's `targetChainRefundPerGasUnused`

*** This will only be able to succeed if the following is true **
        - newGasLimit >= gas limit of the old instruction
        - newReceiverValue >= receiver value of the old instruction

**Parameters**
* `deliveryVaaKey` (*struct VaaKey*) - VaaKey identifying the wormhole message containing the        previously published delivery instructions
* `targetChain` (*uint16*) - The target chain that the original delivery targeted. Must match targetChain from original delivery instructions
* `newReceiverValue` (*uint256*) - new msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `newGasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider, to the refund chain and address specified in the original request
* `newDeliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing redelivery instructions
#### resend

  ```solidity
  function resend(struct VaaKey deliveryVaaKey, uint16 targetChain, uint256 newReceiverValue, bytes newEncodedExecutionParameters, address newDeliveryProviderAddress) external payable returns (uint64 sequence)
  ```

  Requests a previously published delivery instruction to be redelivered

This function must be called with `msg.value` equal to
quoteDeliveryPrice(targetChain, newReceiverValue, newEncodedExecutionParameters, newDeliveryProviderAddress)

**Parameters**
* `deliveryVaaKey` (*struct VaaKey*) - VaaKey identifying the wormhole message containing the        previously published delivery instructions
* `targetChain` (*uint16*) - The target chain that the original delivery targeted. Must match targetChain from original delivery instructions
* `newReceiverValue` (*uint256*) - new msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `newEncodedExecutionParameters` (*bytes*) - new encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `newDeliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing redelivery instructions  @notice *** This will only be able to succeed if the following is true **         - (For EVM_V1) newGasLimit >= gas limit of the old instruction         - newReceiverValue >= receiver value of the old instruction         - (For EVM_V1) newDeliveryProvider's `targetChainRefundPerGasUnused` >= old relay provider's `targetChainRefundPerGasUnused`
#### quoteEVMDeliveryPrice

  ```solidity
  function quoteEVMDeliveryPrice(uint16 targetChain, uint256 receiverValue, uint256 gasLimit) external view returns (uint256 nativePriceQuote, uint256 targetChainRefundPerGasUnused)
  ```

  Returns the price to request a relay to chain `targetChain`, using the default delivery provider

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.

**Returns**
* `nativePriceQuote` (*uint256*) - Price, in units of current chain currency, that the delivery provider charges to perform the relay
* `targetChainRefundPerGasUnused` (*uint256*) - amount of target chain currency that will be refunded per unit of gas unused,         if a refundAddress is specified.         Note: This value can be overridden by the delivery provider on the target chain. The returned value here should be considered to be a         promise by the delivery provider of the amount of refund per gas unused that will be returned to the refundAddress at the target chain.         If a delivery provider decides to override, this will be visible as part of the emitted Delivery event on the target chain.
#### quoteEVMDeliveryPrice

  ```solidity
  function quoteEVMDeliveryPrice(uint16 targetChain, uint256 receiverValue, uint256 gasLimit, address deliveryProviderAddress) external view returns (uint256 nativePriceQuote, uint256 targetChainRefundPerGasUnused)
  ```

  Returns the price to request a relay to chain `targetChain`, using delivery provider `deliveryProviderAddress`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `nativePriceQuote` (*uint256*) - Price, in units of current chain currency, that the delivery provider charges to perform the relay
* `targetChainRefundPerGasUnused` (*uint256*) - amount of target chain currency that will be refunded per unit of gas unused,         if a refundAddress is specified         Note: This value can be overridden by the delivery provider on the target chain. The returned value here should be considered to be a         promise by the delivery provider of the amount of refund per gas unused that will be returned to the refundAddress at the target chain.         If a delivery provider decides to override, this will be visible as part of the emitted Delivery event on the target chain.
#### quoteDeliveryPrice

  ```solidity
  function quoteDeliveryPrice(uint16 targetChain, uint256 receiverValue, bytes encodedExecutionParameters, address deliveryProviderAddress) external view returns (uint256 nativePriceQuote, bytes encodedExecutionInfo)
  ```

  Returns the price to request a relay to chain `targetChain`, using delivery provider `deliveryProviderAddress`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `encodedExecutionParameters` (*bytes*) - encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `nativePriceQuote` (*uint256*) - Price, in units of current chain currency, that the delivery provider charges to perform the relay
* `encodedExecutionInfo` (*bytes*) - encoded information on how the delivery will be executed        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` and `targetChainRefundPerGasUnused`             (which is the amount of target chain currency that will be refunded per unit of gas unused,              if a refundAddress is specified)
#### quoteNativeForChain

  ```solidity
  function quoteNativeForChain(uint16 targetChain, uint256 currentChainAmount, address deliveryProviderAddress) external view returns (uint256 targetChainAmount)
  ```

  Returns the (extra) amount of target chain currency that `targetAddress`
will be called with, if the `paymentForExtraReceiverValue` field is set to `currentChainAmount`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `currentChainAmount` (*uint256*) - The value that `paymentForExtraReceiverValue` will be set to
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `targetChainAmount` (*uint256*) - The amount such that if `targetAddress` will be called with `msg.value` equal to         receiverValue + targetChainAmount
#### getDefaultDeliveryProvider

  ```solidity
  function getDefaultDeliveryProvider() external view returns (address deliveryProvider)
  ```

  Returns the address of the current default delivery provider

**Returns**
* `deliveryProvider` (*address*) - The address of (the default delivery provider)'s contract on this source   chain. This must be a contract that implements IDeliveryProvider.
#### getRegisteredWormholeRelayerContract

  ```solidity
  function getRegisteredWormholeRelayerContract(uint16 chainId) external view returns (bytes32)
  ```

#### deliveryAttempted

  ```solidity
  function deliveryAttempted(bytes32 deliveryHash) external view returns (bool attempted)
  ```

  Returns true if a delivery has been attempted for the given deliveryHash
Note: invalid deliveries where the tx reverts are not considered attempted

#### deliverySuccessBlock

  ```solidity
  function deliverySuccessBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number at which a delivery was successfully executed

#### deliveryFailureBlock

  ```solidity
  function deliveryFailureBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number of the latest attempt to execute a delivery that failed

#### SendEvent

  ```solidity
  event SendEvent(uint64 sequence, uint256 deliveryQuote, uint256 paymentForExtraReceiverValue)
  ```

### IWormholeRelayerDelivery

#### deliver

  ```solidity
  function deliver(bytes[] encodedVMs, bytes encodedDeliveryVAA, address payable relayerRefundAddress, bytes deliveryOverrides) external payable
  ```

  The delivery provider calls `deliver` to relay messages as described by one delivery instruction

The delivery provider must pass in the specified (by VaaKeys[]) signed wormhole messages (VAAs) from the source chain
as well as the signed wormhole message with the delivery instructions (the delivery VAA)

The messages will be relayed to the target address (with the specified gas limit and receiver value) iff the following checks are met:
- the delivery VAA has a valid signature
- the delivery VAA's emitter is one of these WormholeRelayer contracts
- the delivery provider passed in at least enough of this chain's currency as msg.value (enough meaning the maximum possible refund)
- the instruction's target chain is this chain
- the relayed signed VAAs match the descriptions in container.messages (the VAA hashes match, or the emitter address, sequence number pair matches, depending on the description given)

**Parameters**
* `encodedVMs` (*bytes[]*) - - An array of signed wormhole messages (all from the same source chain     transaction)
* `encodedDeliveryVAA` (*bytes*) - - Signed wormhole message from the source chain's WormholeRelayer     contract with payload being the encoded delivery instruction container
* `relayerRefundAddress` (*address payable*) - - The address to which any refunds to the delivery provider     should be sent
* `deliveryOverrides` (*bytes*) - - Optional overrides field which must be either an empty bytes array or     an encoded DeliveryOverride struct

#### getRegisteredWormholeRelayerContract

  ```solidity
  function getRegisteredWormholeRelayerContract(uint16 chainId) external view returns (bytes32)
  ```

#### deliveryAttempted

  ```solidity
  function deliveryAttempted(bytes32 deliveryHash) external view returns (bool attempted)
  ```

  Returns true if a delivery has been attempted for the given deliveryHash
Note: invalid deliveries where the tx reverts are not considered attempted

#### deliverySuccessBlock

  ```solidity
  function deliverySuccessBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number at which a delivery was successfully executed

#### deliveryFailureBlock

  ```solidity
  function deliveryFailureBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number of the latest attempt to execute a delivery that failed

#### Delivery

  ```solidity
  event Delivery(address recipientContract, uint16 sourceChain, uint64 sequence, bytes32 deliveryVaaHash, enum IWormholeRelayerDelivery.DeliveryStatus status, uint256 gasUsed, enum IWormholeRelayerDelivery.RefundStatus refundStatus, bytes additionalStatusInfo, bytes overridesInfo)
  ```

#### SendEvent

  ```solidity
  event SendEvent(uint64 sequence, uint256 deliveryQuote, uint256 paymentForExtraReceiverValue)
  ```

### IWormholeRelayer

#### sendPayloadToEvm

  ```solidity
  function sendPayloadToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

Any refunds (from leftover gas) will be paid to the delivery provider. In order to receive the refunds, use the `sendPayloadToEvm` function
with `refundChain` and `refundAddress` as parameters

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendPayloadToEvm

  ```solidity
  function sendPayloadToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit, uint16 refundChain, address refundAddress) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendVaasToEvm

  ```solidity
  function sendVaasToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit, struct VaaKey[] vaaKeys) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

Any refunds (from leftover gas) will be paid to the delivery provider. In order to receive the refunds, use the `sendVaasToEvm` function
with `refundChain` and `refundAddress` as parameters

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendVaasToEvm

  ```solidity
  function sendVaasToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 gasLimit, struct VaaKey[] vaaKeys, uint16 refundChain, address refundAddress) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the default delivery provider
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to `receiverValue`

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to `quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit)`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendToEvm

  ```solidity
  function sendToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, uint256 gasLimit, uint16 refundChain, address refundAddress, address deliveryProviderAddress, struct VaaKey[] vaaKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit, deliveryProviderAddress) + paymentForExtraReceiverValue

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### sendToEvm

  ```solidity
  function sendToEvm(uint16 targetChain, address targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, uint256 gasLimit, uint16 refundChain, address refundAddress, address deliveryProviderAddress, struct MessageKey[] messageKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and external messages specified by `messageKeys` to the address `targetAddress` on chain `targetChain`
with gas limit `gasLimit` and `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteEVMDeliveryPrice(targetChain, receiverValue, gasLimit, deliveryProviderAddress) + paymentForExtraReceiverValue

Note: MessageKeys can specify wormhole messages (VaaKeys) or other types of messages (ex. USDC CCTP attestations). Ensure the selected
DeliveryProvider supports all the MessageKey.keyType values specified or it will not be delivered!

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*address*) - address to call on targetChain (that implements IWormholeReceiver)
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*address*) - The address on `refundChain` to deliver any refund to
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `messageKeys` (*struct MessageKey[]*) - Additional messagess to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### send

  ```solidity
  function send(uint16 targetChain, bytes32 targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, bytes encodedExecutionParameters, uint16 refundChain, bytes32 refundAddress, address deliveryProviderAddress, struct VaaKey[] vaaKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteDeliveryPrice(targetChain, receiverValue, encodedExecutionParameters, deliveryProviderAddress) + paymentForExtraReceiverValue

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*bytes32*) - address to call on targetChain (that implements IWormholeReceiver), in Wormhole bytes32 format
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `encodedExecutionParameters` (*bytes*) - encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*bytes32*) - The address on `refundChain` to deliver any refund to, in Wormhole bytes32 format
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `vaaKeys` (*struct VaaKey[]*) - Additional VAAs to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### send

  ```solidity
  function send(uint16 targetChain, bytes32 targetAddress, bytes payload, uint256 receiverValue, uint256 paymentForExtraReceiverValue, bytes encodedExecutionParameters, uint16 refundChain, bytes32 refundAddress, address deliveryProviderAddress, struct MessageKey[] messageKeys, uint8 consistencyLevel) external payable returns (uint64 sequence)
  ```

  Publishes an instruction for the delivery provider at `deliveryProviderAddress`
to relay a payload and VAAs specified by `vaaKeys` to the address `targetAddress` on chain `targetChain`
with `msg.value` equal to
receiverValue + (arbitrary amount that is paid for by paymentForExtraReceiverValue of this chain's wei) in targetChain wei.

Any refunds (from leftover gas) will be sent to `refundAddress` on chain `refundChain`
`targetAddress` must implement the IWormholeReceiver interface

This function must be called with `msg.value` equal to
quoteDeliveryPrice(targetChain, receiverValue, encodedExecutionParameters, deliveryProviderAddress) + paymentForExtraReceiverValue

Note: MessageKeys can specify wormhole messages (VaaKeys) or other types of messages (ex. USDC CCTP attestations). Ensure the selected
DeliveryProvider supports all the MessageKey.keyType values specified or it will not be delivered!

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `targetAddress` (*bytes32*) - address to call on targetChain (that implements IWormholeReceiver), in Wormhole bytes32 format
* `payload` (*bytes*) - arbitrary bytes to pass in as parameter in call to `targetAddress`
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `paymentForExtraReceiverValue` (*uint256*) - amount (in current chain currency units) to spend on extra receiverValue        (in addition to the `receiverValue` specified)
* `encodedExecutionParameters` (*bytes*) - encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `refundChain` (*uint16*) - The chain to deliver any refund to, in Wormhole Chain ID format
* `refundAddress` (*bytes32*) - The address on `refundChain` to deliver any refund to, in Wormhole bytes32 format
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider
* `messageKeys` (*struct MessageKey[]*) - Additional messagess to pass in as parameter in call to `targetAddress`
* `consistencyLevel` (*uint8*) - Consistency level with which to publish the delivery instructions - see        https://book.wormhole.com/wormhole/3_coreLayerContracts.html?highlight=consistency#consistency-levels

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing delivery instructions
#### resendToEvm

  ```solidity
  function resendToEvm(struct VaaKey deliveryVaaKey, uint16 targetChain, uint256 newReceiverValue, uint256 newGasLimit, address newDeliveryProviderAddress) external payable returns (uint64 sequence)
  ```

  Requests a previously published delivery instruction to be redelivered
(e.g. with a different delivery provider)

This function must be called with `msg.value` equal to
quoteEVMDeliveryPrice(targetChain, newReceiverValue, newGasLimit, newDeliveryProviderAddress)

 @notice *** This will only be able to succeed if the following is true **
        - newGasLimit >= gas limit of the old instruction
        - newReceiverValue >= receiver value of the old instruction
        - newDeliveryProvider's `targetChainRefundPerGasUnused` >= old relay provider's `targetChainRefundPerGasUnused`

*** This will only be able to succeed if the following is true **
        - newGasLimit >= gas limit of the old instruction
        - newReceiverValue >= receiver value of the old instruction

**Parameters**
* `deliveryVaaKey` (*struct VaaKey*) - VaaKey identifying the wormhole message containing the        previously published delivery instructions
* `targetChain` (*uint16*) - The target chain that the original delivery targeted. Must match targetChain from original delivery instructions
* `newReceiverValue` (*uint256*) - new msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `newGasLimit` (*uint256*) - gas limit with which to call `targetAddress`. Any units of gas unused will be refunded according to the        `targetChainRefundPerGasUnused` rate quoted by the delivery provider, to the refund chain and address specified in the original request
* `newDeliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing redelivery instructions
#### resend

  ```solidity
  function resend(struct VaaKey deliveryVaaKey, uint16 targetChain, uint256 newReceiverValue, bytes newEncodedExecutionParameters, address newDeliveryProviderAddress) external payable returns (uint64 sequence)
  ```

  Requests a previously published delivery instruction to be redelivered

This function must be called with `msg.value` equal to
quoteDeliveryPrice(targetChain, newReceiverValue, newEncodedExecutionParameters, newDeliveryProviderAddress)

**Parameters**
* `deliveryVaaKey` (*struct VaaKey*) - VaaKey identifying the wormhole message containing the        previously published delivery instructions
* `targetChain` (*uint16*) - The target chain that the original delivery targeted. Must match targetChain from original delivery instructions
* `newReceiverValue` (*uint256*) - new msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `newEncodedExecutionParameters` (*bytes*) - new encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `newDeliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `sequence` (*uint64*) - sequence number of published VAA containing redelivery instructions  @notice *** This will only be able to succeed if the following is true **         - (For EVM_V1) newGasLimit >= gas limit of the old instruction         - newReceiverValue >= receiver value of the old instruction         - (For EVM_V1) newDeliveryProvider's `targetChainRefundPerGasUnused` >= old relay provider's `targetChainRefundPerGasUnused`
#### quoteEVMDeliveryPrice

  ```solidity
  function quoteEVMDeliveryPrice(uint16 targetChain, uint256 receiverValue, uint256 gasLimit) external view returns (uint256 nativePriceQuote, uint256 targetChainRefundPerGasUnused)
  ```

  Returns the price to request a relay to chain `targetChain`, using the default delivery provider

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.

**Returns**
* `nativePriceQuote` (*uint256*) - Price, in units of current chain currency, that the delivery provider charges to perform the relay
* `targetChainRefundPerGasUnused` (*uint256*) - amount of target chain currency that will be refunded per unit of gas unused,         if a refundAddress is specified.         Note: This value can be overridden by the delivery provider on the target chain. The returned value here should be considered to be a         promise by the delivery provider of the amount of refund per gas unused that will be returned to the refundAddress at the target chain.         If a delivery provider decides to override, this will be visible as part of the emitted Delivery event on the target chain.
#### quoteEVMDeliveryPrice

  ```solidity
  function quoteEVMDeliveryPrice(uint16 targetChain, uint256 receiverValue, uint256 gasLimit, address deliveryProviderAddress) external view returns (uint256 nativePriceQuote, uint256 targetChainRefundPerGasUnused)
  ```

  Returns the price to request a relay to chain `targetChain`, using delivery provider `deliveryProviderAddress`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `gasLimit` (*uint256*) - gas limit with which to call `targetAddress`.
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `nativePriceQuote` (*uint256*) - Price, in units of current chain currency, that the delivery provider charges to perform the relay
* `targetChainRefundPerGasUnused` (*uint256*) - amount of target chain currency that will be refunded per unit of gas unused,         if a refundAddress is specified         Note: This value can be overridden by the delivery provider on the target chain. The returned value here should be considered to be a         promise by the delivery provider of the amount of refund per gas unused that will be returned to the refundAddress at the target chain.         If a delivery provider decides to override, this will be visible as part of the emitted Delivery event on the target chain.
#### quoteDeliveryPrice

  ```solidity
  function quoteDeliveryPrice(uint16 targetChain, uint256 receiverValue, bytes encodedExecutionParameters, address deliveryProviderAddress) external view returns (uint256 nativePriceQuote, bytes encodedExecutionInfo)
  ```

  Returns the price to request a relay to chain `targetChain`, using delivery provider `deliveryProviderAddress`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `receiverValue` (*uint256*) - msg.value that delivery provider should pass in for call to `targetAddress` (in targetChain currency units)
* `encodedExecutionParameters` (*bytes*) - encoded information on how to execute delivery that may impact pricing        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` with which to call `targetAddress`
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `nativePriceQuote` (*uint256*) - Price, in units of current chain currency, that the delivery provider charges to perform the relay
* `encodedExecutionInfo` (*bytes*) - encoded information on how the delivery will be executed        e.g. for version EVM_V1, this is a struct that encodes the `gasLimit` and `targetChainRefundPerGasUnused`             (which is the amount of target chain currency that will be refunded per unit of gas unused,              if a refundAddress is specified)
#### quoteNativeForChain

  ```solidity
  function quoteNativeForChain(uint16 targetChain, uint256 currentChainAmount, address deliveryProviderAddress) external view returns (uint256 targetChainAmount)
  ```

  Returns the (extra) amount of target chain currency that `targetAddress`
will be called with, if the `paymentForExtraReceiverValue` field is set to `currentChainAmount`

**Parameters**
* `targetChain` (*uint16*) - in Wormhole Chain ID format
* `currentChainAmount` (*uint256*) - The value that `paymentForExtraReceiverValue` will be set to
* `deliveryProviderAddress` (*address*) - The address of the desired delivery provider's implementation of IDeliveryProvider

**Returns**
* `targetChainAmount` (*uint256*) - The amount such that if `targetAddress` will be called with `msg.value` equal to         receiverValue + targetChainAmount
#### getDefaultDeliveryProvider

  ```solidity
  function getDefaultDeliveryProvider() external view returns (address deliveryProvider)
  ```

  Returns the address of the current default delivery provider

**Returns**
* `deliveryProvider` (*address*) - The address of (the default delivery provider)'s contract on this source   chain. This must be a contract that implements IDeliveryProvider.
#### deliver

  ```solidity
  function deliver(bytes[] encodedVMs, bytes encodedDeliveryVAA, address payable relayerRefundAddress, bytes deliveryOverrides) external payable
  ```

  The delivery provider calls `deliver` to relay messages as described by one delivery instruction

The delivery provider must pass in the specified (by VaaKeys[]) signed wormhole messages (VAAs) from the source chain
as well as the signed wormhole message with the delivery instructions (the delivery VAA)

The messages will be relayed to the target address (with the specified gas limit and receiver value) iff the following checks are met:
- the delivery VAA has a valid signature
- the delivery VAA's emitter is one of these WormholeRelayer contracts
- the delivery provider passed in at least enough of this chain's currency as msg.value (enough meaning the maximum possible refund)
- the instruction's target chain is this chain
- the relayed signed VAAs match the descriptions in container.messages (the VAA hashes match, or the emitter address, sequence number pair matches, depending on the description given)

**Parameters**
* `encodedVMs` (*bytes[]*) - - An array of signed wormhole messages (all from the same source chain     transaction)
* `encodedDeliveryVAA` (*bytes*) - - Signed wormhole message from the source chain's WormholeRelayer     contract with payload being the encoded delivery instruction container
* `relayerRefundAddress` (*address payable*) - - The address to which any refunds to the delivery provider     should be sent
* `deliveryOverrides` (*bytes*) - - Optional overrides field which must be either an empty bytes array or     an encoded DeliveryOverride struct

#### getRegisteredWormholeRelayerContract

  ```solidity
  function getRegisteredWormholeRelayerContract(uint16 chainId) external view returns (bytes32)
  ```

#### deliveryAttempted

  ```solidity
  function deliveryAttempted(bytes32 deliveryHash) external view returns (bool attempted)
  ```

  Returns true if a delivery has been attempted for the given deliveryHash
Note: invalid deliveries where the tx reverts are not considered attempted

#### deliverySuccessBlock

  ```solidity
  function deliverySuccessBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number at which a delivery was successfully executed

#### deliveryFailureBlock

  ```solidity
  function deliveryFailureBlock(bytes32 deliveryHash) external view returns (uint256 blockNumber)
  ```

  block number of the latest attempt to execute a delivery that failed

#### Delivery

  ```solidity
  event Delivery(address recipientContract, uint16 sourceChain, uint64 sequence, bytes32 deliveryVaaHash, enum IWormholeRelayerDelivery.DeliveryStatus status, uint256 gasUsed, enum IWormholeRelayerDelivery.RefundStatus refundStatus, bytes additionalStatusInfo, bytes overridesInfo)
  ```

#### SendEvent

  ```solidity
  event SendEvent(uint64 sequence, uint256 deliveryQuote, uint256 paymentForExtraReceiverValue)
  ```

### RETURNDATA_TRUNCATION_THRESHOLD

  ```solidity
  uint256 RETURNDATA_TRUNCATION_THRESHOLD
  ```

### InvalidMsgValue

  ```solidity
  error InvalidMsgValue(uint256 msgValue, uint256 totalFee)
  ```

### RequestedGasLimitTooLow

  ```solidity
  error RequestedGasLimitTooLow()
  ```

### DeliveryProviderDoesNotSupportTargetChain

  ```solidity
  error DeliveryProviderDoesNotSupportTargetChain(address relayer, uint16 chainId)
  ```

### DeliveryProviderCannotReceivePayment

  ```solidity
  error DeliveryProviderCannotReceivePayment()
  ```

### DeliveryProviderDoesNotSupportMessageKeyType

  ```solidity
  error DeliveryProviderDoesNotSupportMessageKeyType(uint8 keyType)
  ```

### ReentrantDelivery

  ```solidity
  error ReentrantDelivery(address msgSender, address lockedBy)
  ```

### InvalidPayloadId

  ```solidity
  error InvalidPayloadId(uint8 parsed, uint8 expected)
  ```

### InvalidPayloadLength

  ```solidity
  error InvalidPayloadLength(uint256 received, uint256 expected)
  ```

### InvalidVaaKeyType

  ```solidity
  error InvalidVaaKeyType(uint8 parsed)
  ```

### TooManyMessageKeys

  ```solidity
  error TooManyMessageKeys(uint256 numMessageKeys)
  ```

### InvalidDeliveryVaa

  ```solidity
  error InvalidDeliveryVaa(string reason)
  ```

### InvalidEmitter

  ```solidity
  error InvalidEmitter(bytes32 emitter, bytes32 registered, uint16 chainId)
  ```

### MessageKeysLengthDoesNotMatchMessagesLength

  ```solidity
  error MessageKeysLengthDoesNotMatchMessagesLength(uint256 keys, uint256 vaas)
  ```

### VaaKeysDoNotMatchVaas

  ```solidity
  error VaaKeysDoNotMatchVaas(uint8 index)
  ```

### RequesterNotWormholeRelayer

  ```solidity
  error RequesterNotWormholeRelayer()
  ```

### TargetChainIsNotThisChain

  ```solidity
  error TargetChainIsNotThisChain(uint16 targetChain)
  ```

### InvalidOverrideGasLimit

  ```solidity
  error InvalidOverrideGasLimit()
  ```

### InvalidOverrideReceiverValue

  ```solidity
  error InvalidOverrideReceiverValue()
  ```

### InvalidOverrideRefundPerGasUnused

  ```solidity
  error InvalidOverrideRefundPerGasUnused()
  ```

### InsufficientRelayerFunds

  ```solidity
  error InsufficientRelayerFunds(uint256 msgValue, uint256 minimum)
  ```

### NotAnEvmAddress

  ```solidity
  error NotAnEvmAddress(bytes32)
  ```

## Spot Market

### Async Order Configuration Module

#### addSettlementStrategy

  ```solidity
  function addSettlementStrategy(uint128 synthMarketId, struct SettlementStrategy.Data strategy) external returns (uint256 strategyId)
  ```

  Adds new settlement strategy to the specified market id.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market to associate the strategy with.
* `strategy` (*struct SettlementStrategy.Data*) - Settlement strategy data. see SettlementStrategy.Data struct.

**Returns**
* `strategyId` (*uint256*) - newly created settlement strategy id.
#### setSettlementStrategyEnabled

  ```solidity
  function setSettlementStrategyEnabled(uint128 synthMarketId, uint256 strategyId, bool enabled) external
  ```

  Sets the strategy to enabled or disabled.

  when disabled, the strategy will be invalid for committing of new async orders.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market associated with the strategy.
* `strategyId` (*uint256*) - id of the strategy.
* `enabled` (*bool*) - set enabled/disabled.

#### setSettlementStrategy

  ```solidity
  function setSettlementStrategy(uint128 synthMarketId, uint256 strategyId, struct SettlementStrategy.Data strategy) external
  ```

  updates the strategy with the new strategy passed in.

  THIS WILL OVERRIDE ANY SETTINGS FOR EXISTING ORDERS

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market associated with the strategy.
* `strategyId` (*uint256*) - id of the strategy.
* `strategy` (*struct SettlementStrategy.Data*) - new strategy config

#### getSettlementStrategy

  ```solidity
  function getSettlementStrategy(uint128 marketId, uint256 strategyId) external view returns (struct SettlementStrategy.Data settlementStrategy)
  ```

  Returns the settlement strategy data for given market/strategy id.

**Parameters**
* `marketId` (*uint128*) - Id of the market associated with the strategy.
* `strategyId` (*uint256*) - id of the strategy.

**Returns**
* `settlementStrategy` (*struct SettlementStrategy.Data*) - 

#### SettlementStrategyAdded

  ```solidity
  event SettlementStrategyAdded(uint128 synthMarketId, uint256 strategyId)
  ```

  Gets fired when new settlement strategy is added.

**Parameters**
* `synthMarketId` (*uint128*) - adds settlement strategy to this specific market.
* `strategyId` (*uint256*) - the newly created settlement strategy id.

#### SettlementStrategySet

  ```solidity
  event SettlementStrategySet(uint128 synthMarketId, uint256 strategyId, struct SettlementStrategy.Data strategy)
  ```

  Gets fired when settlement strategy is enabled/disabled.

  currently only enabled/disabled flag can be updated.

**Parameters**
* `synthMarketId` (*uint128*) - adds settlement strategy to this specific market.
* `strategyId` (*uint256*) - id of the strategy.
* `strategy` (*struct SettlementStrategy.Data*) - updated strategy

### Async Order Module

#### commitOrder

  ```solidity
  function commitOrder(uint128 marketId, enum Transaction.Type orderType, uint256 amountProvided, uint256 settlementStrategyId, uint256 minimumSettlementAmount, address referrer) external returns (struct AsyncOrderClaim.Data asyncOrderClaim)
  ```

  Commit an async order via this function

  commitment transfers the amountProvided into the contract and escrows the funds until settlement.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `orderType` (*enum Transaction.Type*) - Should send either 2 or 3 which correlates to the transaction type enum defined in Transaction.Type.
* `amountProvided` (*uint256*) - amount of value provided by the user for trade. Should have enough allowance.
* `settlementStrategyId` (*uint256*) - id of the settlement strategy used for trade.
* `minimumSettlementAmount` (*uint256*) - minimum amount of value returned to trader after fees.
* `referrer` (*address*) - Optional address of the referrer, for fee share

**Returns**
* `asyncOrderClaim` (*struct AsyncOrderClaim.Data*) - claim details (see AsyncOrderClaim.Data struct).
#### cancelOrder

  ```solidity
  function cancelOrder(uint128 marketId, uint128 asyncOrderId) external
  ```

  Cancel an async order via this function

  cancellation transfers the amountProvided back to the trader without any fee collection
cancellation can only happen after the settlement time has passed
needs to satisfy commitmentTime + settlementDelay + settlementDuration < block.timestamp

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `asyncOrderId` (*uint128*) - id of the async order created during commitment.

#### getAsyncOrderClaim

  ```solidity
  function getAsyncOrderClaim(uint128 marketId, uint128 asyncOrderId) external view returns (struct AsyncOrderClaim.Data asyncOrderClaim)
  ```

  Get async order claim details

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `asyncOrderId` (*uint128*) - id of the async order created during commitment.

**Returns**
* `asyncOrderClaim` (*struct AsyncOrderClaim.Data*) - claim details (see AsyncOrderClaim.Data struct).

#### OrderCommitted

  ```solidity
  event OrderCommitted(uint128 marketId, enum Transaction.Type orderType, uint256 amountProvided, uint128 asyncOrderId, address sender, address referrer)
  ```

  Gets fired when a new order is committed.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `orderType` (*enum Transaction.Type*) - Should send either 2 or 3 which correlates to the transaction type enum defined in Transaction.Type.
* `amountProvided` (*uint256*) - amount of value provided by the user for trade.
* `asyncOrderId` (*uint128*) - id of the async order created (used for settlements).
* `sender` (*address*) - trader address.
* `referrer` (*address*) - Optional address of the referrer, for fee share

#### OrderCancelled

  ```solidity
  event OrderCancelled(uint128 marketId, uint128 asyncOrderId, struct AsyncOrderClaim.Data asyncOrderClaim, address sender)
  ```

  Gets fired when an order is cancelled.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `asyncOrderId` (*uint128*) - id of the async order.
* `asyncOrderClaim` (*struct AsyncOrderClaim.Data*) - claim details (see AsyncOrderClaim.Data struct).
* `sender` (*address*) - trader address and also the receiver of the funds.

### Async Order Settlement Module

#### settleOrder

  ```solidity
  function settleOrder(uint128 marketId, uint128 asyncOrderId) external returns (uint256 finalOrderAmount, struct OrderFees.Data)
  ```

  Settle already created async order via this function

  if the strategy is onchain, the settlement is done similar to an atomic buy except with settlement time
if the strategy is offchain, this function will revert with OffchainLookup error and the client should perform offchain lookup and call the callback specified see: EIP-3668

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `asyncOrderId` (*uint128*) - id of the async order created during commitment.

**Returns**
* `finalOrderAmount` (*uint256*) - amount returned to trader after fees.
* `[1]` (*struct OrderFees.Data*) - OrderFees.Data breakdown of all the fees incurred for the transaction.

#### OrderSettled

  ```solidity
  event OrderSettled(uint128 marketId, uint128 asyncOrderId, uint256 finalOrderAmount, struct OrderFees.Data fees, uint256 collectedFees, address settler, uint256 price, enum Transaction.Type orderType)
  ```

  Gets fired when an order is settled.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `asyncOrderId` (*uint128*) - id of the async order.
* `finalOrderAmount` (*uint256*) - amount returned to trader after fees.
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
* `collectedFees` (*uint256*) - fees collected by the configured fee collector.
* `settler` (*address*) - address that settled the order.
* `price` (*uint256*) - 
* `orderType` (*enum Transaction.Type*) - 

### Atomic Order Module

#### buyExactIn

  ```solidity
  function buyExactIn(uint128 synthMarketId, uint256 amountUsd, uint256 minAmountReceived, address referrer) external returns (uint256 synthAmount, struct OrderFees.Data fees)
  ```

  Initiates a buy trade returning synth for the specified amountUsd.

  Transfers the specified amountUsd, collects fees through configured fee collector, returns synth to the trader.
Leftover fees not collected get deposited into the market manager to improve market PnL.
Uses the buyFeedId configured for the market.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market used for the trade.
* `amountUsd` (*uint256*) - Amount of snxUSD trader is providing allowance for the trade.
* `minAmountReceived` (*uint256*) - Min Amount of synth is expected the trader to receive otherwise the transaction will revert.
* `referrer` (*address*) - Optional address of the referrer, for fee share

**Returns**
* `synthAmount` (*uint256*) - Synth received on the trade based on amount provided by trader.
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
#### buy

  ```solidity
  function buy(uint128 marketId, uint256 usdAmount, uint256 minAmountReceived, address referrer) external returns (uint256 synthAmount, struct OrderFees.Data fees)
  ```

  alias for buyExactIn

**Parameters**
* `marketId` (*uint128*) - (see buyExactIn)
* `usdAmount` (*uint256*) - (see buyExactIn)
* `minAmountReceived` (*uint256*) - (see buyExactIn)
* `referrer` (*address*) - (see buyExactIn)

**Returns**
* `synthAmount` (*uint256*) - (see buyExactIn)
* `fees` (*struct OrderFees.Data*) - (see buyExactIn)
#### buyExactOut

  ```solidity
  function buyExactOut(uint128 synthMarketId, uint256 synthAmount, uint256 maxUsdAmount, address referrer) external returns (uint256 usdAmountCharged, struct OrderFees.Data fees)
  ```

  user provides the synth amount they'd like to buy, and the function charges the USD amount which includes fees

  the inverse of buyExactIn

**Parameters**
* `synthMarketId` (*uint128*) - market id value
* `synthAmount` (*uint256*) - the amount of synth the trader wants to buy
* `maxUsdAmount` (*uint256*) - max amount the trader is willing to pay for the specified synth
* `referrer` (*address*) - optional address of the referrer, for fee share

**Returns**
* `usdAmountCharged` (*uint256*) - amount of USD charged for the trade
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction
#### quoteBuyExactIn

  ```solidity
  function quoteBuyExactIn(uint128 synthMarketId, uint256 usdAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 synthAmount, struct OrderFees.Data fees)
  ```

  quote for buyExactIn.  same parameters and return values as buyExactIn

**Parameters**
* `synthMarketId` (*uint128*) - market id value
* `usdAmount` (*uint256*) - amount of USD to use for the trade
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `synthAmount` (*uint256*) - return amount of synth given the USD amount - fees
* `fees` (*struct OrderFees.Data*) - breakdown of all the quoted fees for the buy txn
#### quoteBuyExactOut

  ```solidity
  function quoteBuyExactOut(uint128 synthMarketId, uint256 synthAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 usdAmountCharged, struct OrderFees.Data)
  ```

  quote for buyExactOut.  same parameters and return values as buyExactOut

**Parameters**
* `synthMarketId` (*uint128*) - market id value
* `synthAmount` (*uint256*) - amount of synth requested
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `usdAmountCharged` (*uint256*) - USD amount charged for the synth requested - fees
* `[1]` (*struct OrderFees.Data*) - fees  breakdown of all the quoted fees for the buy txn
#### sellExactIn

  ```solidity
  function sellExactIn(uint128 synthMarketId, uint256 sellAmount, uint256 minAmountReceived, address referrer) external returns (uint256 returnAmount, struct OrderFees.Data fees)
  ```

  Initiates a sell trade returning snxUSD for the specified amount of synth (sellAmount)

  Transfers the specified synth, collects fees through configured fee collector, returns snxUSD to the trader.
Leftover fees not collected get deposited into the market manager to improve market PnL.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market used for the trade.
* `sellAmount` (*uint256*) - Amount of synth provided by trader for trade into snxUSD.
* `minAmountReceived` (*uint256*) - Min Amount of snxUSD trader expects to receive for the trade
* `referrer` (*address*) - Optional address of the referrer, for fee share

**Returns**
* `returnAmount` (*uint256*) - Amount of snxUSD returned to user
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
#### sellExactOut

  ```solidity
  function sellExactOut(uint128 marketId, uint256 usdAmount, uint256 maxSynthAmount, address referrer) external returns (uint256 synthToBurn, struct OrderFees.Data fees)
  ```

  initiates a trade where trader specifies USD amount they'd like to receive

  the inverse of sellExactIn

**Parameters**
* `marketId` (*uint128*) - synth market id
* `usdAmount` (*uint256*) - amount of USD trader wants to receive
* `maxSynthAmount` (*uint256*) - max amount of synth trader is willing to use to receive the specified USD amount
* `referrer` (*address*) - optional address of the referrer, for fee share

**Returns**
* `synthToBurn` (*uint256*) - amount of synth charged for the specified usd amount
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction
#### sell

  ```solidity
  function sell(uint128 marketId, uint256 synthAmount, uint256 minUsdAmount, address referrer) external returns (uint256 usdAmountReceived, struct OrderFees.Data fees)
  ```

  alias for sellExactIn

**Parameters**
* `marketId` (*uint128*) - (see sellExactIn)
* `synthAmount` (*uint256*) - (see sellExactIn)
* `minUsdAmount` (*uint256*) - (see sellExactIn)
* `referrer` (*address*) - (see sellExactIn)

**Returns**
* `usdAmountReceived` (*uint256*) - (see sellExactIn)
* `fees` (*struct OrderFees.Data*) - (see sellExactIn)
#### quoteSellExactIn

  ```solidity
  function quoteSellExactIn(uint128 marketId, uint256 synthAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 returnAmount, struct OrderFees.Data fees)
  ```

  quote for sellExactIn

  returns expected USD amount trader would receive for the specified synth amount

**Parameters**
* `marketId` (*uint128*) - synth market id
* `synthAmount` (*uint256*) - synth amount trader is providing for the trade
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `returnAmount` (*uint256*) - amount of USD expected back
* `fees` (*struct OrderFees.Data*) - breakdown of all the quoted fees for the txn
#### quoteSellExactOut

  ```solidity
  function quoteSellExactOut(uint128 marketId, uint256 usdAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 synthToBurn, struct OrderFees.Data fees)
  ```

  quote for sellExactOut

  returns expected synth amount expected from trader for the requested USD amount

**Parameters**
* `marketId` (*uint128*) - synth market id
* `usdAmount` (*uint256*) - USD amount trader wants to receive
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `synthToBurn` (*uint256*) - amount of synth expected from trader
* `fees` (*struct OrderFees.Data*) - breakdown of all the quoted fees for the txn
#### getMarketSkew

  ```solidity
  function getMarketSkew(uint128 marketId) external view returns (int256 marketSkew)
  ```

  gets the current market skew

**Parameters**
* `marketId` (*uint128*) - synth market id

**Returns**
* `marketSkew` (*int256*) - the skew

#### SynthBought

  ```solidity
  event SynthBought(uint256 synthMarketId, uint256 synthReturned, struct OrderFees.Data fees, uint256 collectedFees, address referrer, uint256 price)
  ```

  Gets fired when buy trade is complete

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market used for the trade.
* `synthReturned` (*uint256*) - Synth received on the trade based on amount provided by trader.
* `fees` (*struct OrderFees.Data*) - breakdown of all fees incurred for transaction.
* `collectedFees` (*uint256*) - Fees collected by the configured FeeCollector for the market (rest of the fees are deposited to market manager).
* `referrer` (*address*) - Optional address of the referrer, for fee share
* `price` (*uint256*) - 

#### SynthSold

  ```solidity
  event SynthSold(uint256 synthMarketId, uint256 amountReturned, struct OrderFees.Data fees, uint256 collectedFees, address referrer, uint256 price)
  ```

  Gets fired when sell trade is complete

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market used for the trade.
* `amountReturned` (*uint256*) - Amount of snxUSD returned to user based on synth provided by trader.
* `fees` (*struct OrderFees.Data*) - breakdown of all fees incurred for transaction.
* `collectedFees` (*uint256*) - Fees collected by the configured FeeCollector for the market (rest of the fees are deposited to market manager).
* `referrer` (*address*) - Optional address of the referrer, for fee share
* `price` (*uint256*) - 

### Market Configuration Module

#### getMarketFees

  ```solidity
  function getMarketFees(uint128 synthMarketId) external returns (uint256 atomicFixedFee, uint256 asyncFixedFee, int256 wrapFee, int256 unwrapFee)
  ```

  gets the atomic fixed fee for a given market

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the fee applies to.

**Returns**
* `atomicFixedFee` (*uint256*) - fixed fee amount represented in bips with 18 decimals.
* `asyncFixedFee` (*uint256*) - fixed fee amount represented in bips with 18 decimals.
* `wrapFee` (*int256*) - wrapping fee in %, 18 decimals. Can be negative.
* `unwrapFee` (*int256*) - unwrapping fee in %, 18 decimals. Can be negative.
#### setAtomicFixedFee

  ```solidity
  function setAtomicFixedFee(uint128 synthMarketId, uint256 atomicFixedFee) external
  ```

  sets the atomic fixed fee for a given market

  only marketOwner can set the fee

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the fee applies to.
* `atomicFixedFee` (*uint256*) - fixed fee amount represented in bips with 18 decimals.

#### setAsyncFixedFee

  ```solidity
  function setAsyncFixedFee(uint128 synthMarketId, uint256 asyncFixedFee) external
  ```

  sets the async fixed fee for a given market

  only marketOwner can set the fee

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the fee applies to.
* `asyncFixedFee` (*uint256*) - fixed fee amount represented in bips with 18 decimals.

#### setMarketSkewScale

  ```solidity
  function setMarketSkewScale(uint128 synthMarketId, uint256 skewScale) external
  ```

  sets the skew scale for a given market

  only marketOwner can set the skew scale

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the skew scale applies to.
* `skewScale` (*uint256*) - max amount of synth which makes the skew 100%. the fee is derived as a % of the max value.  100% premium means outstanding synth == skewScale.

#### getMarketSkewScale

  ```solidity
  function getMarketSkewScale(uint128 synthMarketId) external view returns (uint256 skewScale)
  ```

  gets the skew scale for a given market

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the skew scale applies to.

**Returns**
* `skewScale` (*uint256*) - max amount of synth which makes the skew 100%. the fee is derived as a % of the max value.  100% premium means outstanding synth == skewScale.
#### setMarketUtilizationFees

  ```solidity
  function setMarketUtilizationFees(uint128 synthMarketId, uint256 utilizationFeeRate) external
  ```

  sets the market utilization fee for a given market

  only marketOwner can set the fee
100% utilization means the fee is 0.  120% utilization means the fee is 20% * this fee rate (in bips).

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the utilization fee applies to.
* `utilizationFeeRate` (*uint256*) - the rate is represented in bips with 18 decimals and is the rate at which fee increases based on the % above 100% utilization of the delegated collateral for the market.

#### getMarketUtilizationFees

  ```solidity
  function getMarketUtilizationFees(uint128 synthMarketId) external view returns (uint256 utilizationFeeRate)
  ```

  gets the market utilization fee for a given market

  100% utilization means the fee is 0.  120% utilization means the fee is 20% * this fee rate (in bips).

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the utilization fee applies to.

**Returns**
* `utilizationFeeRate` (*uint256*) - the rate is represented in bips with 18 decimals and is the rate at which fee increases based on the % above 100% utilization of the delegated collateral for the market.
#### setCollateralLeverage

  ```solidity
  function setCollateralLeverage(uint128 synthMarketId, uint256 collateralLeverage) external
  ```

  sets the collateral leverage for a given market

  only marketOwner can set the leverage
this leverage value is a value applied to delegated collateral which is compared to outstanding synth to determine utilization of market, and locked amounts

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the collateral leverage applies to.
* `collateralLeverage` (*uint256*) - the leverage is represented as % with 18 decimals. 1 = 1x leverage

#### getCollateralLeverage

  ```solidity
  function getCollateralLeverage(uint128 synthMarketId) external view returns (uint256 collateralLeverage)
  ```

  gets the collateral leverage for a given market

  this leverage value is a value applied to delegated collateral which is compared to outstanding synth to determine utilization of market, and locked amounts

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the collateral leverage applies to.

**Returns**
* `collateralLeverage` (*uint256*) - the leverage is represented as % with 18 decimals. 1 = 1x leverage
#### setCustomTransactorFees

  ```solidity
  function setCustomTransactorFees(uint128 synthMarketId, address transactor, uint256 fixedFeeAmount) external
  ```

  sets the fixed fee for a given market and transactor

  overrides both the atomic and async fixed fees
only marketOwner can set the fee
especially useful for direct integrations where configured traders get a discount

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the custom transactor fee applies to.
* `transactor` (*address*) - address of the trader getting discounted fees.
* `fixedFeeAmount` (*uint256*) - the fixed fee applying to the provided transactor.

#### getCustomTransactorFees

  ```solidity
  function getCustomTransactorFees(uint128 synthMarketId, address transactor) external view returns (uint256 fixedFeeAmount)
  ```

  gets the fixed fee for a given market and transactor

  overrides both the atomic and async fixed fees
especially useful for direct integrations where configured traders get a discount

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the custom transactor fee applies to.
* `transactor` (*address*) - address of the trader getting discounted fees.

**Returns**
* `fixedFeeAmount` (*uint256*) - the fixed fee applying to the provided transactor.
#### setFeeCollector

  ```solidity
  function setFeeCollector(uint128 synthMarketId, address feeCollector) external
  ```

  sets a custom fee collector for a given market

  only marketOwner can set the fee collector
a use case here would be if the market owner wants to collect the fees via this contract and distribute via rewards distributor to SNX holders for example.
if fee collector is not set, the fees are deposited into the market manager.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the fee collector applies to.
* `feeCollector` (*address*) - address of the fee collector inheriting the IFeeCollector interface.

#### getFeeCollector

  ```solidity
  function getFeeCollector(uint128 synthMarketId) external view returns (address feeCollector)
  ```

  gets a custom fee collector for a given market

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the fee collector applies to.

**Returns**
* `feeCollector` (*address*) - address of the fee collector inheriting the IFeeCollector interface.
#### setWrapperFees

  ```solidity
  function setWrapperFees(uint128 synthMarketId, int256 wrapFee, int256 unwrapFee) external
  ```

  sets wrapper related fees.

  only marketOwner can set the wrapper fees
fees can be negative.  this is a way to unwind the wrapper if needed by providing incentives.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market the wrapper fees apply to.
* `wrapFee` (*int256*) - wrapping fee in %, 18 decimals. Can be negative.
* `unwrapFee` (*int256*) - unwrapping fee in %, 18 decimals. Can be negative.

#### updateReferrerShare

  ```solidity
  function updateReferrerShare(uint128 marketId, address referrer, uint256 sharePercentage) external
  ```

  Update the referral share percentage for a given market

**Parameters**
* `marketId` (*uint128*) - id of the market
* `referrer` (*address*) - The address of the referrer
* `sharePercentage` (*uint256*) - The new share percentage for the referrer

#### getReferrerShare

  ```solidity
  function getReferrerShare(uint128 marketId, address referrer) external view returns (uint256 sharePercentage)
  ```

  get the referral share percentage for a given market

**Parameters**
* `marketId` (*uint128*) - id of the market
* `referrer` (*address*) - The address of the referrer

**Returns**
* `sharePercentage` (*uint256*) - The new share percentage for the referrer

#### MarketUtilizationFeesSet

  ```solidity
  event MarketUtilizationFeesSet(uint256 synthMarketId, uint256 utilizationFeeRate)
  ```

  emitted when market utilization fees are set for specified market

**Parameters**
* `synthMarketId` (*uint256*) - market id
* `utilizationFeeRate` (*uint256*) - utilization fee rate value

#### MarketSkewScaleSet

  ```solidity
  event MarketSkewScaleSet(uint256 synthMarketId, uint256 skewScale)
  ```

  emitted when the skew scale is set for a market

**Parameters**
* `synthMarketId` (*uint256*) - market id
* `skewScale` (*uint256*) - skew scale value

#### CollateralLeverageSet

  ```solidity
  event CollateralLeverageSet(uint256 synthMarketId, uint256 collateralLeverage)
  ```

  emitted when the collateral leverage is set for a market

**Parameters**
* `synthMarketId` (*uint256*) - market id
* `collateralLeverage` (*uint256*) - leverage value

#### AtomicFixedFeeSet

  ```solidity
  event AtomicFixedFeeSet(uint256 synthMarketId, uint256 atomicFixedFee)
  ```

  emitted when the fixed fee for atomic orders is set.

**Parameters**
* `synthMarketId` (*uint256*) - market id
* `atomicFixedFee` (*uint256*) - fee value

#### AsyncFixedFeeSet

  ```solidity
  event AsyncFixedFeeSet(uint256 synthMarketId, uint256 asyncFixedFee)
  ```

  emitted when the fixed fee for async orders is set.

**Parameters**
* `synthMarketId` (*uint256*) - market id
* `asyncFixedFee` (*uint256*) - fee value

#### TransactorFixedFeeSet

  ```solidity
  event TransactorFixedFeeSet(uint256 synthMarketId, address transactor, uint256 fixedFeeAmount)
  ```

  emitted when the fixed fee is set for a given transactor

  this overrides the async/atomic fixed fees for a given transactor

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market to set the fees for.
* `transactor` (*address*) - fixed fee for the transactor (overrides the global fixed fee)
* `fixedFeeAmount` (*uint256*) - the fixed fee for the corresponding market, and transactor

#### FeeCollectorSet

  ```solidity
  event FeeCollectorSet(uint256 synthMarketId, address feeCollector)
  ```

  emitted when custom fee collector is set for a given market

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market to set the collector for.
* `feeCollector` (*address*) - the address of the fee collector to set.

#### WrapperFeesSet

  ```solidity
  event WrapperFeesSet(uint256 synthMarketId, int256 wrapFee, int256 unwrapFee)
  ```

  emitted when wrapper fees are set for a given market

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market to set the wrapper fees.
* `wrapFee` (*int256*) - wrapping fee in %, 18 decimals. Can be negative.
* `unwrapFee` (*int256*) - unwrapping fee in %, 18 decimals. Can be negative.

#### ReferrerShareUpdated

  ```solidity
  event ReferrerShareUpdated(uint128 marketId, address referrer, uint256 sharePercentage)
  ```

  Emitted when the share percentage for a referrer address has been updated.

**Parameters**
* `marketId` (*uint128*) - Id of the market
* `referrer` (*address*) - The address of the referrer
* `sharePercentage` (*uint256*) - The new share percentage for the referrer

### Spot Market Factory Module

#### setSynthetix

  ```solidity
  function setSynthetix(contract ISynthetixSystem synthetix) external
  ```

  Sets the v3 synthetix core system.

  Pulls in the USDToken and oracle manager from the synthetix core system and sets those appropriately.

**Parameters**
* `synthetix` (*contract ISynthetixSystem*) - synthetix v3 core system address

#### setSynthImplementation

  ```solidity
  function setSynthImplementation(address synthImplementation) external
  ```

  When a new synth is created, this is the erc20 implementation that is used.

**Parameters**
* `synthImplementation` (*address*) - erc20 implementation address

#### createSynth

  ```solidity
  function createSynth(string tokenName, string tokenSymbol, address synthOwner) external returns (uint128 synthMarketId)
  ```

  Creates a new synth market with synthetix v3 core system via market manager

  The synth is created using the initial synth implementation and creates a proxy for future upgrades of the synth implementation.
Sets up the market owner who can update configuration for the synth.

**Parameters**
* `tokenName` (*string*) - name of synth (i.e Synthetix ETH)
* `tokenSymbol` (*string*) - symbol of synth (i.e snxETH)
* `synthOwner` (*address*) - owner of the market that's created.

**Returns**
* `synthMarketId` (*uint128*) - id of the synth market that was created
#### getSynth

  ```solidity
  function getSynth(uint128 marketId) external view returns (address synthAddress)
  ```

  Get the proxy address of the synth for the provided marketId

  Uses associated systems module to retrieve the token address.

**Parameters**
* `marketId` (*uint128*) - id of the market

**Returns**
* `synthAddress` (*address*) - address of the proxy for the synth
#### getSynthImpl

  ```solidity
  function getSynthImpl(uint128 marketId) external view returns (address implAddress)
  ```

  Get the implementation address of the synth for the provided marketId.
This address should not be used directly--use `getSynth` instead

  Uses associated systems module to retrieve the token address.

**Parameters**
* `marketId` (*uint128*) - id of the market

**Returns**
* `implAddress` (*address*) - address of the proxy for the synth
#### updatePriceData

  ```solidity
  function updatePriceData(uint128 marketId, bytes32 buyFeedId, bytes32 sellFeedId, uint256 strictPriceStalenessTolerance) external
  ```

  Update the price data for a given market.

  Only the market owner can call this function.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `buyFeedId` (*bytes32*) - the oracle manager buy feed node id
* `sellFeedId` (*bytes32*) - the oracle manager sell feed node id
* `strictPriceStalenessTolerance` (*uint256*) - configurable price staleness tolerance used for transacting

#### getPriceData

  ```solidity
  function getPriceData(uint128 marketId) external view returns (bytes32 buyFeedId, bytes32 sellFeedId, uint256 strictPriceStalenessTolerance)
  ```

  Gets the price data for a given market.

  Only the market owner can call this function.

**Parameters**
* `marketId` (*uint128*) - id of the market

**Returns**
* `buyFeedId` (*bytes32*) - the oracle manager buy feed node id
* `sellFeedId` (*bytes32*) - the oracle manager sell feed node id
* `strictPriceStalenessTolerance` (*uint256*) - configurable price staleness tolerance used for transacting
#### upgradeSynthImpl

  ```solidity
  function upgradeSynthImpl(uint128 marketId) external
  ```

  upgrades the synth implementation to the current implementation for the specified market.
Anyone who is willing and able to spend the gas can call this method.

  The synth implementation is upgraded via the proxy.

**Parameters**
* `marketId` (*uint128*) - id of the market

#### setDecayRate

  ```solidity
  function setDecayRate(uint128 marketId, uint256 rate) external
  ```

  Allows market to adjust decay rate of the synth

**Parameters**
* `marketId` (*uint128*) - the market to update the synth decay rate for
* `rate` (*uint256*) - APY to decay of the synth to decay by, as a 18 decimal ratio

#### nominateMarketOwner

  ```solidity
  function nominateMarketOwner(uint128 synthMarketId, address newNominatedOwner) external
  ```

  Allows the current market owner to nominate a new owner.

  The nominated owner will have to call `acceptOwnership` in a separate transaction in order to finalize the action and become the new contract owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value
* `newNominatedOwner` (*address*) - The address that is to become nominated.

#### acceptMarketOwnership

  ```solidity
  function acceptMarketOwnership(uint128 synthMarketId) external
  ```

  Allows a nominated address to accept ownership of the market.

  Reverts if the caller is not nominated.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### renounceMarketNomination

  ```solidity
  function renounceMarketNomination(uint128 synthMarketId) external
  ```

  Allows a nominated address to renounce ownership of the market.

  Reverts if the caller is not nominated.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### renounceMarketOwnership

  ```solidity
  function renounceMarketOwnership(uint128 synthMarketId) external
  ```

  Allows the market owner to renounce his ownership.

  Reverts if the caller is not the owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### getMarketOwner

  ```solidity
  function getMarketOwner(uint128 synthMarketId) external view returns (address)
  ```

  Returns market owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### getNominatedMarketOwner

  ```solidity
  function getNominatedMarketOwner(uint128 synthMarketId) external view returns (address)
  ```

  Returns nominated market owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### indexPrice

  ```solidity
  function indexPrice(uint128 marketId, uint128 transactionType, enum Price.Tolerance priceTolerance) external view returns (uint256 price)
  ```

  Get current price based on type of transaction and tolerance

**Parameters**
* `marketId` (*uint128*) - synth market id value
* `transactionType` (*uint128*) - type of txn
* `priceTolerance` (*enum Price.Tolerance*) - staleness tolerance to use for price

**Returns**
* `price` (*uint256*) - current price of the synth
#### name

  ```solidity
  function name(uint128 marketId) external view returns (string)
  ```

  returns a human-readable name for a given market

#### reportedDebt

  ```solidity
  function reportedDebt(uint128 marketId) external view returns (uint256)
  ```

  returns amount of USD that the market would try to mint if everything was withdrawn

#### minimumCredit

  ```solidity
  function minimumCredit(uint128 marketId) external view returns (uint256)
  ```

  prevents reduction of available credit capacity by specifying this amount, for which withdrawals will be disallowed

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

#### SynthetixSystemSet

  ```solidity
  event SynthetixSystemSet(address synthetix, address usdTokenAddress, address oracleManager)
  ```

  Gets fired when the synthetix is set

**Parameters**
* `synthetix` (*address*) - address of the synthetix core contract
* `usdTokenAddress` (*address*) - address of the USDToken contract
* `oracleManager` (*address*) - address of the Oracle Manager contract

#### SynthImplementationSet

  ```solidity
  event SynthImplementationSet(address synthImplementation)
  ```

  Gets fired when the synth implementation is set

**Parameters**
* `synthImplementation` (*address*) - address of the synth implementation

#### SynthRegistered

  ```solidity
  event SynthRegistered(uint256 synthMarketId, address synthTokenAddress)
  ```

  Gets fired when the synth is registered as a market.

**Parameters**
* `synthMarketId` (*uint256*) - Id of the synth market that was created
* `synthTokenAddress` (*address*) - address of the newly created synth token

#### SynthImplementationUpgraded

  ```solidity
  event SynthImplementationUpgraded(uint256 synthMarketId, address proxy, address implementation)
  ```

  Gets fired when the synth's implementation is updated on the corresponding proxy.

**Parameters**
* `synthMarketId` (*uint256*) - 
* `proxy` (*address*) - the synth proxy servicing the latest implementation
* `implementation` (*address*) - the latest implementation of the synth

#### SynthPriceDataUpdated

  ```solidity
  event SynthPriceDataUpdated(uint256 synthMarketId, bytes32 buyFeedId, bytes32 sellFeedId, uint256 strictStalenessTolerance)
  ```

  Gets fired when the market's price feeds are updated, compatible with oracle manager

**Parameters**
* `synthMarketId` (*uint256*) - 
* `buyFeedId` (*bytes32*) - the oracle manager feed id for the buy price
* `sellFeedId` (*bytes32*) - the oracle manager feed id for the sell price
* `strictStalenessTolerance` (*uint256*) - 

#### DecayRateUpdated

  ```solidity
  event DecayRateUpdated(uint128 marketId, uint256 rate)
  ```

  Gets fired when the market's price feeds are updated, compatible with oracle manager

**Parameters**
* `marketId` (*uint128*) - Id of the synth market
* `rate` (*uint256*) - the new decay rate (1e16 means 1% decay per year)

#### MarketOwnerNominated

  ```solidity
  event MarketOwnerNominated(uint128 marketId, address newOwner)
  ```

  Emitted when an address has been nominated.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `newOwner` (*address*) - The address that has been nominated.

#### MarketNominationRenounced

  ```solidity
  event MarketNominationRenounced(uint128 marketId, address nominee)
  ```

  Emitted when market nominee renounces nomination.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `nominee` (*address*) - The address that has been nominated.

#### MarketOwnerChanged

  ```solidity
  event MarketOwnerChanged(uint128 marketId, address oldOwner, address newOwner)
  ```

  Emitted when the owner of the market has changed.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `oldOwner` (*address*) - The previous owner of the market.
* `newOwner` (*address*) - The new owner of the market.

### Synth Token Module

#### setDecayRate

  ```solidity
  function setDecayRate(uint256 _rate) external
  ```

  Updates the decay rate for a year

**Parameters**
* `_rate` (*uint256*) - The decay rate with 18 decimals (1e16 means 1% decay per year).

#### decayRate

  ```solidity
  function decayRate() external view returns (uint256)
  ```

  get decay rate for a year

#### advanceEpoch

  ```solidity
  function advanceEpoch() external returns (uint256)
  ```

  advance epoch manually in order to avoid precision loss

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns wether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, uint8 tokenDecimals) external
  ```

  Initializes the token with name, symbol, and decimals.

#### mint

  ```solidity
  function mint(address to, uint256 amount) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `amount` (*uint256*) - The amount of tokens to mint.

#### burn

  ```solidity
  function burn(address from, uint256 amount) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `from` (*address*) - The address whose tokens will be burnt.
* `amount` (*uint256*) - The amount of tokens to burn.

#### setAllowance

  ```solidity
  function setAllowance(address from, address spender, uint256 amount) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `from` (*address*) - The address that is providing allowance.
* `spender` (*address*) - The address that is given allowance.
* `amount` (*uint256*) - The amount of allowance being given.

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Retrieves the name of the token, e.g. "Synthetix Network Token".

**Returns**
* `[0]` (*string*) - A string with the name of the token.
#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Retrieves the symbol of the token, e.g. "SNX".

**Returns**
* `[0]` (*string*) - A string with the symbol of the token.
#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Retrieves the number of decimals used by the token. The default is 18.

**Returns**
* `[0]` (*uint8*) - The number of decimals.
#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total number of tokens in circulation (minted - burnt).

**Returns**
* `[0]` (*uint256*) - The total number of tokens.
#### balanceOf

  ```solidity
  function balanceOf(address owner) external view returns (uint256)
  ```

  Returns the balance of a user.

**Parameters**
* `owner` (*address*) - The address whose balance is being retrieved.

**Returns**
* `[0]` (*uint256*) - The number of tokens owned by the user.
#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns how many tokens a user has allowed another user to transfer on its behalf.

**Parameters**
* `owner` (*address*) - The user who has given the allowance.
* `spender` (*address*) - The user who was given the allowance.

**Returns**
* `[0]` (*uint256*) - The amount of tokens `spender` can transfer on `owner`'s behalf.
#### transfer

  ```solidity
  function transfer(address to, uint256 amount) external returns (bool)
  ```

  Transfer tokens from one address to another.

**Parameters**
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The amount of tokens to be transferred.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### approve

  ```solidity
  function approve(address spender, uint256 amount) external returns (bool)
  ```

  Allows users to provide allowance to other users so that they can transfer tokens on their behalf.

**Parameters**
* `spender` (*address*) - The address that is receiving the allowance.
* `amount` (*uint256*) - The amount of tokens that are being added to the allowance.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.
#### increaseAllowance

  ```solidity
  function increaseAllowance(address spender, uint256 addedValue) external returns (bool)
  ```

  Atomically increases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.

#### decreaseAllowance

  ```solidity
  function decreaseAllowance(address spender, uint256 subtractedValue) external returns (bool)
  ```

  Atomically decreases the allowance granted to `spender` by the caller.

This is an alternative to {approve} that can be used as a mitigation for
problems described in {IERC20-approve}.

Emits an {Approval} event indicating the updated allowance.

Requirements:

- `spender` cannot be the zero address.
- `spender` must have allowance for the caller of at least
`subtractedValue`.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 amount) external returns (bool)
  ```

  Allows a user who has been given allowance to transfer tokens on another user's behalf.

**Parameters**
* `from` (*address*) - The address that owns the tokens that are being transferred.
* `to` (*address*) - The address that will receive the tokens.
* `amount` (*uint256*) - The number of tokens to transfer.

**Returns**
* `[0]` (*bool*) - A boolean which is true if the operation succeeded.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 amount)
  ```

  Emitted when tokens have been transferred.

**Parameters**
* `from` (*address*) - The address that originally owned the tokens.
* `to` (*address*) - The address that received the tokens.
* `amount` (*uint256*) - The number of tokens that were transferred.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 amount)
  ```

  Emitted when a user has provided allowance to another user for transferring tokens on its behalf.

**Parameters**
* `owner` (*address*) - The address that is providing the allowance.
* `spender` (*address*) - The address that received the allowance.
* `amount` (*uint256*) - The number of tokens that were added to `spender`'s allowance.

### Wrapper Module

#### setWrapper

  ```solidity
  function setWrapper(uint128 marketId, address wrapCollateralType, uint256 maxWrappableAmount) external
  ```

  Used to set the wrapper supply cap for a given market and collateral type.

  If the supply cap is set to 0 or lower than the current outstanding supply, then the wrapper is disabled.
There is a synthetix v3 core system supply cap also set. If the current supply becomes higher than either the core system supply cap or the local market supply cap, wrapping will be disabled.

**Parameters**
* `marketId` (*uint128*) - Id of the market to enable wrapping for.
* `wrapCollateralType` (*address*) - The collateral being used to wrap the synth.
* `maxWrappableAmount` (*uint256*) - The maximum amount of collateral that can be wrapped.

#### getWrapper

  ```solidity
  function getWrapper(uint128 marketId) external view returns (address wrapCollateralType, uint256 maxWrappableAmount)
  ```

  Used to get the wrapper supply cap for a given market and collateral type.

**Parameters**
* `marketId` (*uint128*) - Id of the market to enable wrapping for.

**Returns**
* `wrapCollateralType` (*address*) - The collateral being used to wrap the synth.
* `maxWrappableAmount` (*uint256*) - The maximum amount of collateral that can be wrapped.
#### wrap

  ```solidity
  function wrap(uint128 marketId, uint256 wrapAmount, uint256 minAmountReceived) external returns (uint256 amountToMint, struct OrderFees.Data fees)
  ```

  Wraps the specified amount and returns similar value of synth minus the fees.

  Fees are collected from the user by way of the contract returning less synth than specified amount of collateral.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `wrapAmount` (*uint256*) - Amount of collateral to wrap.  This amount gets deposited into the market collateral manager.
* `minAmountReceived` (*uint256*) - The minimum amount of synths the trader is expected to receive, otherwise the transaction will revert.

**Returns**
* `amountToMint` (*uint256*) - Amount of synth returned to user.
* `fees` (*struct OrderFees.Data*) - breakdown of all fees. in this case, only wrapper fees are returned.
#### unwrap

  ```solidity
  function unwrap(uint128 marketId, uint256 unwrapAmount, uint256 minAmountReceived) external returns (uint256 returnCollateralAmount, struct OrderFees.Data fees)
  ```

  Unwraps the synth and returns similar value of collateral minus the fees.

  Transfers the specified synth, collects fees through configured fee collector, returns collateral minus fees to trader.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `unwrapAmount` (*uint256*) - Amount of synth trader is unwrapping.
* `minAmountReceived` (*uint256*) - The minimum amount of collateral the trader is expected to receive, otherwise the transaction will revert.

**Returns**
* `returnCollateralAmount` (*uint256*) - Amount of collateral returned.
* `fees` (*struct OrderFees.Data*) - breakdown of all fees. in this case, only wrapper fees are returned.

#### WrapperSet

  ```solidity
  event WrapperSet(uint256 synthMarketId, address wrapCollateralType, uint256 maxWrappableAmount)
  ```

  Gets fired when wrapper supply is set for a given market, collateral type.

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market the wrapper is initialized for.
* `wrapCollateralType` (*address*) - the collateral used to wrap the synth.
* `maxWrappableAmount` (*uint256*) - the local supply cap for the wrapper.

#### SynthWrapped

  ```solidity
  event SynthWrapped(uint256 synthMarketId, uint256 amountWrapped, struct OrderFees.Data fees, uint256 feesCollected)
  ```

  Gets fired after user wraps synth

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market.
* `amountWrapped` (*uint256*) - amount of synth wrapped.
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
* `feesCollected` (*uint256*) - fees collected by the configured FeeCollector for the market (rest of the fees are deposited to market manager).

#### SynthUnwrapped

  ```solidity
  event SynthUnwrapped(uint256 synthMarketId, uint256 amountUnwrapped, struct OrderFees.Data fees, uint256 feesCollected)
  ```

  Gets fired after user unwraps synth

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market.
* `amountUnwrapped` (*uint256*) - amount of synth unwrapped.
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
* `feesCollected` (*uint256*) - fees collected by the configured FeeCollector for the market (rest of the fees are deposited to market manager).

## Perps Market

### IAccountEvents

#### AccountCharged

  ```solidity
  event AccountCharged(uint128 accountId, int256 amount, uint256 accountDebt)
  ```

  Gets fired anytime an account is charged with fees, paying settlement rewards.

**Parameters**
* `accountId` (*uint128*) - Id of the account being deducted.
* `amount` (*int256*) - Amount of synth market deducted from the account.
* `accountDebt` (*uint256*) - current debt of the account after charged amount.

### Async Order Cancel Module

#### cancelOrder

  ```solidity
  function cancelOrder(uint128 accountId) external
  ```

  Cancels an order when price exceeds the acceptable price. Uses the onchain benchmark price at commitment time.

**Parameters**
* `accountId` (*uint128*) - Id of the account used for the trade.

#### OrderCancelled

  ```solidity
  event OrderCancelled(uint128 marketId, uint128 accountId, uint256 desiredPrice, uint256 fillPrice, int128 sizeDelta, uint256 settlementReward, bytes32 trackingCode, address settler)
  ```

  Gets fired when an order is cancelled.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `accountId` (*uint128*) - Id of the account used for the trade.
* `desiredPrice` (*uint256*) - Price at which the order was cancelled.
* `fillPrice` (*uint256*) - Price at which the order was cancelled.
* `sizeDelta` (*int128*) - Size delta from order.
* `settlementReward` (*uint256*) - Amount of fees collected by the settler.
* `trackingCode` (*bytes32*) - Optional code for integrator tracking purposes.
* `settler` (*address*) - address of the settler of the order.

### Async Order Module

#### commitOrder

  ```solidity
  function commitOrder(struct AsyncOrder.OrderCommitmentRequest commitment) external returns (struct AsyncOrder.Data retOrder, uint256 fees)
  ```

  Commit an async order via this function

**Parameters**
* `commitment` (*struct AsyncOrder.OrderCommitmentRequest*) - Order commitment data (see AsyncOrder.OrderCommitmentRequest struct).

**Returns**
* `retOrder` (*struct AsyncOrder.Data*) - order details (see AsyncOrder.Data struct).
* `fees` (*uint256*) - order fees (protocol + settler)
#### getOrder

  ```solidity
  function getOrder(uint128 accountId) external view returns (struct AsyncOrder.Data order)
  ```

  Get async order claim details

**Parameters**
* `accountId` (*uint128*) - id of the account.

**Returns**
* `order` (*struct AsyncOrder.Data*) - async order claim details (see AsyncOrder.Data struct).
#### computeOrderFees

  ```solidity
  function computeOrderFees(uint128 marketId, int128 sizeDelta) external view returns (uint256 orderFees, uint256 fillPrice)
  ```

  Simulates what the order fee would be for the given market with the specified size.

  Note that this does not include the settlement reward fee, which is based on the strategy type used

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `sizeDelta` (*int128*) - size of position.

**Returns**
* `orderFees` (*uint256*) - incurred fees.
* `fillPrice` (*uint256*) - price at which the order would be filled.
#### computeOrderFeesWithPrice

  ```solidity
  function computeOrderFeesWithPrice(uint128 marketId, int128 sizeDelta, uint256 price) external view returns (uint256 orderFees, uint256 fillPrice)
  ```

  Simulates what the order fee would be for the given market with the specified size.

  Note that this does not include the settlement reward fee, which is based on the strategy type used

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `sizeDelta` (*int128*) - size of position.
* `price` (*uint256*) - price of the market.

**Returns**
* `orderFees` (*uint256*) - incurred fees.
* `fillPrice` (*uint256*) - price at which the order would be filled.
#### getSettlementRewardCost

  ```solidity
  function getSettlementRewardCost(uint128 marketId, uint128 settlementStrategyId) external view returns (uint256)
  ```

  Gets the settlement cost including keeper rewards and keeper costs.

**Parameters**
* `marketId` (*uint128*) - Id of the market.
* `settlementStrategyId` (*uint128*) - Order size.

**Returns**
* `[0]` (*uint256*) - settlement cost.
#### requiredMarginForOrder

  ```solidity
  function requiredMarginForOrder(uint128 marketId, uint128 accountId, int128 sizeDelta) external view returns (uint256 requiredMargin)
  ```

  For a given market, account id, and a position size, returns the required total account margin for this order to succeed

  Useful for integrators to determine if an order will succeed or fail

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `accountId` (*uint128*) - id of the trader account.
* `sizeDelta` (*int128*) - size of position.

**Returns**
* `requiredMargin` (*uint256*) - margin required for the order to succeed.
#### requiredMarginForOrderWithPrice

  ```solidity
  function requiredMarginForOrderWithPrice(uint128 marketId, uint128 accountId, int128 sizeDelta, uint256 price) external view returns (uint256 requiredMargin)
  ```

  For a given market, account id, and a position size, and expected price returns the required total account margin for this order to succeed

  Useful for integrators to determine if an order will succeed or fail faking different price scenarios

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `accountId` (*uint128*) - id of the trader account.
* `sizeDelta` (*int128*) - size of position.
* `price` (*uint256*) - price of the market.

**Returns**
* `requiredMargin` (*uint256*) - margin required for the order to succeed.

#### OrderCommitted

  ```solidity
  event OrderCommitted(uint128 marketId, uint128 accountId, enum SettlementStrategy.Type orderType, int128 sizeDelta, uint256 acceptablePrice, uint256 commitmentTime, uint256 expectedPriceTime, uint256 settlementTime, uint256 expirationTime, bytes32 trackingCode, address sender)
  ```

  Gets fired when a new order is committed.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `accountId` (*uint128*) - Id of the account used for the trade.
* `orderType` (*enum SettlementStrategy.Type*) - Should send 0 (at time of writing) that correlates to the transaction type enum defined in SettlementStrategy.Type.
* `sizeDelta` (*int128*) - requested change in size of the order sent by the user.
* `acceptablePrice` (*uint256*) - maximum or minimum, depending on the sizeDelta direction, accepted price to settle the order, set by the user.
* `commitmentTime` (*uint256*) - Time at which the order was committed.
* `expectedPriceTime` (*uint256*) - 
* `settlementTime` (*uint256*) - start time of the settlement window.
* `expirationTime` (*uint256*) - Time at which the order expired.
* `trackingCode` (*bytes32*) - Optional code for integrator tracking purposes.
* `sender` (*address*) - address of the sender of the order. Authorized to commit by account owner.

#### PreviousOrderExpired

  ```solidity
  event PreviousOrderExpired(uint128 marketId, uint128 accountId, int128 sizeDelta, uint256 acceptablePrice, uint256 commitmentTime, bytes32 trackingCode)
  ```

  Gets fired when a new order is committed while a previous one was expired.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `accountId` (*uint128*) - Id of the account used for the trade.
* `sizeDelta` (*int128*) - requested change in size of the order sent by the user.
* `acceptablePrice` (*uint256*) - maximum or minimum, depending on the sizeDelta direction, accepted price to settle the order, set by the user.
* `commitmentTime` (*uint256*) - Time at which the order was committed.
* `trackingCode` (*bytes32*) - Optional code for integrator tracking purposes.

### Async Order Settlement Pyth Module

#### settleOrder

  ```solidity
  function settleOrder(uint128 accountId) external
  ```

  Settles an offchain order using the offchain retrieved data from pyth.

**Parameters**
* `accountId` (*uint128*) - The account id to settle the order

#### OrderSettled

  ```solidity
  event OrderSettled(uint128 marketId, uint128 accountId, uint256 fillPrice, int256 pnl, int256 accruedFunding, int128 sizeDelta, int128 newSize, uint256 totalFees, uint256 referralFees, uint256 collectedFees, uint256 settlementReward, bytes32 trackingCode, address settler)
  ```

  Gets fired when a new order is settled.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `accountId` (*uint128*) - Id of the account used for the trade.
* `fillPrice` (*uint256*) - Price at which the order was settled.
* `pnl` (*int256*) - Pnl of the previous closed position.
* `accruedFunding` (*int256*) - Accrued funding of the previous closed position.
* `sizeDelta` (*int128*) - Size delta from order.
* `newSize` (*int128*) - New size of the position after settlement.
* `totalFees` (*uint256*) - Amount of fees collected by the protocol.
* `referralFees` (*uint256*) - Amount of fees collected by the referrer.
* `collectedFees` (*uint256*) - Amount of fees collected by fee collector.
* `settlementReward` (*uint256*) - reward to sender for settling order.
* `trackingCode` (*bytes32*) - Optional code for integrator tracking purposes.
* `settler` (*address*) - address of the settler of the order.

#### InterestCharged

  ```solidity
  event InterestCharged(uint128 accountId, uint256 interest)
  ```

  Gets fired after order settles and includes the interest charged to the account.

**Parameters**
* `accountId` (*uint128*) - Id of the account used for the trade.
* `interest` (*uint256*) - interest charges

### Collateral Configuration Module

#### setCollateralConfiguration

  ```solidity
  function setCollateralConfiguration(uint128 collateralId, uint256 maxCollateralAmount, uint256 upperLimitDiscount, uint256 lowerLimitDiscount, uint256 discountScalar) external
  ```

  Sets the max collateral amount for a specific synth market.

**Parameters**
* `collateralId` (*uint128*) - Synth market id to use as collateral, 0 for snxUSD.
* `maxCollateralAmount` (*uint256*) - Max collateral amount to set for the synth market id.
* `upperLimitDiscount` (*uint256*) - Collateral value is discounted and capped at this value.  In % units.
* `lowerLimitDiscount` (*uint256*) - Collateral value is discounted and at minimum, this value.  In % units.
* `discountScalar` (*uint256*) - This value is used to scale the impactOnSkew of the collateral.

#### getCollateralConfiguration

  ```solidity
  function getCollateralConfiguration(uint128 collateralId) external view returns (uint256 maxCollateralAmount)
  ```

  Gets the max collateral amount for a specific synth market.

**Parameters**
* `collateralId` (*uint128*) - Synth market id, 0 for snxUSD.

**Returns**
* `maxCollateralAmount` (*uint256*) - max collateral amount of the specified synth market id
#### getCollateralConfigurationFull

  ```solidity
  function getCollateralConfigurationFull(uint128 collateralId) external view returns (uint256 maxCollateralAmount, uint256 upperLimitDiscount, uint256 lowerLimitDiscount, uint256 discountScalar)
  ```

  Gets the full configuration for collateral.  The above function exists for backwards compatibility; encourage all integrators to use this function

**Parameters**
* `collateralId` (*uint128*) - Synth market id, 0 for snxUSD.

**Returns**
* `maxCollateralAmount` (*uint256*) - max collateral amount of the specified synth market id
* `upperLimitDiscount` (*uint256*) - upper bound for max discount on a collateral
* `lowerLimitDiscount` (*uint256*) - lower bound for min discount on a collateral
* `discountScalar` (*uint256*) - scaling value on the impactOnSkew of the collateral (via spot market)
#### setCollateralLiquidateRewardRatio

  ```solidity
  function setCollateralLiquidateRewardRatio(uint128 collateralLiquidateRewardRatioD18) external
  ```

  Sets the collateral liquidation reward ratio.

**Parameters**
* `collateralLiquidateRewardRatioD18` (*uint128*) - the new collateral liquidation reward ratio.

#### getCollateralLiquidateRewardRatio

  ```solidity
  function getCollateralLiquidateRewardRatio() external view returns (uint128 collateralLiquidateRewardRatioD18)
  ```

  Gets the collateral liquidation reward ratio.

#### registerDistributor

  ```solidity
  function registerDistributor(address token, address distributor, uint128 collateralId, address[] poolDelegatedCollateralTypes) external
  ```

  Registers a new reward distributor.

**Parameters**
* `token` (*address*) - the collateral token address.
* `distributor` (*address*) - the distributor address.
* `collateralId` (*uint128*) - the collateral id.
* `poolDelegatedCollateralTypes` (*address[]*) - the pool delegated collateral types.

#### isRegistered

  ```solidity
  function isRegistered(address distributor) external view returns (bool)
  ```

  Checks if a distributor is registered.

**Parameters**
* `distributor` (*address*) - the distributor address.

**Returns**
* `[0]` (*bool*) - isRegistered true if the distributor is registered.
#### getRegisteredDistributor

  ```solidity
  function getRegisteredDistributor(uint128 collateralId) external view returns (address distributor, address[] poolDelegatedCollateralTypes)
  ```

  Gets the registered distributor for a collateral id.

**Parameters**
* `collateralId` (*uint128*) - the collateral id.

**Returns**
* `distributor` (*address*) - the distributor address.
* `poolDelegatedCollateralTypes` (*address[]*) - the pool delegated collateral types.

#### CollateralConfigurationSet

  ```solidity
  event CollateralConfigurationSet(uint128 collateralId, uint256 maxCollateralAmount, uint256 upperLimitDiscount, uint256 lowerLimitDiscount, uint256 discountScalar)
  ```

  Gets fired when max collateral amount for synth for all the markets is set by owner.

**Parameters**
* `collateralId` (*uint128*) - Synth market id to use as collateral, 0 for snxUSD.
* `maxCollateralAmount` (*uint256*) - max amount that was set for the synth
* `upperLimitDiscount` (*uint256*) - upper limit discount that was set for the synth
* `lowerLimitDiscount` (*uint256*) - lower limit discount that was set for the synth
* `discountScalar` (*uint256*) - discount scalar that was set for the synth

#### CollateralLiquidateRewardRatioSet

  ```solidity
  event CollateralLiquidateRewardRatioSet(uint128 collateralLiquidateRewardRatioD18)
  ```

  Gets fired when the collateral liquidation reward ratio is updated.

**Parameters**
* `collateralLiquidateRewardRatioD18` (*uint128*) - new collateral liquidation reward ratio.

#### RewardDistributorRegistered

  ```solidity
  event RewardDistributorRegistered(address distributor)
  ```

  Gets fired when a new reward distributor is registered.

**Parameters**
* `distributor` (*address*) - the new distributor address.

### IDistributorErrors

### Global Perps Market Module

#### getSupportedCollaterals

  ```solidity
  function getSupportedCollaterals() external view returns (uint256[] supportedCollaterals)
  ```

  Gets the list of supported collaterals.

**Returns**
* `supportedCollaterals` (*uint256[]*) - list of supported collateral ids. By supported collateral we mean a collateral which max is greater than zero
#### setKeeperRewardGuards

  ```solidity
  function setKeeperRewardGuards(uint256 minKeeperRewardUsd, uint256 minKeeperProfitRatioD18, uint256 maxKeeperRewardUsd, uint256 maxKeeperScalingRatioD18) external
  ```

  Sets the keeper reward guard (min and max).

**Parameters**
* `minKeeperRewardUsd` (*uint256*) - Minimum keeper reward expressed as USD value.
* `minKeeperProfitRatioD18` (*uint256*) - Minimum keeper profit ratio used together with minKeeperRewardUsd to calculate the minimum.
* `maxKeeperRewardUsd` (*uint256*) - Maximum keeper reward expressed as USD value.
* `maxKeeperScalingRatioD18` (*uint256*) - Scaling used to calculate the Maximum keeper reward together with maxKeeperRewardUsd.

#### getKeeperRewardGuards

  ```solidity
  function getKeeperRewardGuards() external view returns (uint256 minKeeperRewardUsd, uint256 minKeeperProfitRatioD18, uint256 maxKeeperRewardUsd, uint256 maxKeeperScalingRatioD18)
  ```

  Gets the keeper reward guard (min and max).

**Returns**
* `minKeeperRewardUsd` (*uint256*) - Minimum keeper reward expressed as USD value.
* `minKeeperProfitRatioD18` (*uint256*) - Minimum keeper profit ratio used together with minKeeperRewardUsd to calculate the minimum.
* `maxKeeperRewardUsd` (*uint256*) - Maximum keeper reward expressed as USD value.
* `maxKeeperScalingRatioD18` (*uint256*) - Scaling used to calculate the Maximum keeper reward together with maxKeeperRewardUsd.
#### totalGlobalCollateralValue

  ```solidity
  function totalGlobalCollateralValue() external view returns (uint256 totalCollateralValue)
  ```

  Gets the total collateral value of all deposited collateral from all traders.

**Returns**
* `totalCollateralValue` (*uint256*) - value of all collateral
#### globalCollateralValue

  ```solidity
  function globalCollateralValue(uint128 collateralId) external view returns (uint256 collateralValue)
  ```

  Gets the total collateral value of all deposited collateral from all traders.

**Parameters**
* `collateralId` (*uint128*) - the id of the collateral (0 for snxUSD)

**Returns**
* `collateralValue` (*uint256*) - value of all collateral for collateral id
#### setFeeCollector

  ```solidity
  function setFeeCollector(address feeCollector) external
  ```

  Sets the fee collector contract.

  must conform to the IFeeCollector interface

**Parameters**
* `feeCollector` (*address*) - address of the fee collector contract

#### getFeeCollector

  ```solidity
  function getFeeCollector() external view returns (address feeCollector)
  ```

  Gets the configured feeCollector contract

**Returns**
* `feeCollector` (*address*) - address of the fee collector contract
#### setPerAccountCaps

  ```solidity
  function setPerAccountCaps(uint128 maxPositionsPerAccount, uint128 maxCollateralsPerAccount) external
  ```

  Set or update the max number of Positions and Collaterals per Account

**Parameters**
* `maxPositionsPerAccount` (*uint128*) - The max number of concurrent Positions per Account
* `maxCollateralsPerAccount` (*uint128*) - The max number of concurrent Collaterals per Account

#### getPerAccountCaps

  ```solidity
  function getPerAccountCaps() external returns (uint128 maxPositionsPerAccount, uint128 maxCollateralsPerAccount)
  ```

  get the max number of Positions and Collaterals per Account

**Parameters**

#### updateReferrerShare

  ```solidity
  function updateReferrerShare(address referrer, uint256 shareRatioD18) external
  ```

  Update the referral share percentage for a referrer

**Parameters**
* `referrer` (*address*) - The address of the referrer
* `shareRatioD18` (*uint256*) - The new share percentage for the referrer

#### getReferrerShare

  ```solidity
  function getReferrerShare(address referrer) external view returns (uint256 shareRatioD18)
  ```

  get the referral share percentage for the specified referrer

**Parameters**
* `referrer` (*address*) - The address of the referrer

**Returns**
* `shareRatioD18` (*uint256*) - The configured share percentage for the referrer
#### updateKeeperCostNodeId

  ```solidity
  function updateKeeperCostNodeId(bytes32 keeperCostNodeId) external
  ```

  Set node id for keeper cost

**Parameters**
* `keeperCostNodeId` (*bytes32*) - the node id

#### getKeeperCostNodeId

  ```solidity
  function getKeeperCostNodeId() external view returns (bytes32 keeperCostNodeId)
  ```

  Get the node id for keeper cost

**Returns**
* `keeperCostNodeId` (*bytes32*) - the node id
#### getMarkets

  ```solidity
  function getMarkets() external view returns (uint256[] marketIds)
  ```

  get all existing market ids

**Returns**
* `marketIds` (*uint256[]*) - an array of existing market ids
#### setInterestRateParameters

  ```solidity
  function setInterestRateParameters(uint128 lowUtilizationInterestRateGradient, uint128 interestRateGradientBreakpoint, uint128 highUtilizationInterestRateGradient) external
  ```

  Sets the interest rate parameters

**Parameters**
* `lowUtilizationInterestRateGradient` (*uint128*) - interest rate gradient applied to utilization prior to hitting the gradient breakpoint
* `interestRateGradientBreakpoint` (*uint128*) - breakpoint at which the interest rate gradient changes from low to high
* `highUtilizationInterestRateGradient` (*uint128*) - interest rate gradient applied to utilization after hitting the gradient breakpoint

#### getInterestRateParameters

  ```solidity
  function getInterestRateParameters() external view returns (uint128 lowUtilizationInterestRateGradient, uint128 interestRateGradientBreakpoint, uint128 highUtilizationInterestRateGradient)
  ```

  Gets the interest rate parameters

**Returns**
* `lowUtilizationInterestRateGradient` (*uint128*) - 
* `interestRateGradientBreakpoint` (*uint128*) - 
* `highUtilizationInterestRateGradient` (*uint128*) - 
#### updateInterestRate

  ```solidity
  function updateInterestRate() external
  ```

  Update the market interest rate based on current utilization of the super market against backing collateral

  this is a convenience method to manually update interest rate if too much time has passed
     since last update.
interest rate gets automatically updated when a trade is made or when a position is liquidated
InterestRateUpdated event is emitted

#### InterestRateUpdated

  ```solidity
  event InterestRateUpdated(uint128 superMarketId, uint128 interestRate)
  ```

  Gets fired when the interest rate is updated.

**Parameters**
* `superMarketId` (*uint128*) - global super market id
* `interestRate` (*uint128*) - new computed interest rate

#### KeeperRewardGuardsSet

  ```solidity
  event KeeperRewardGuardsSet(uint256 minKeeperRewardUsd, uint256 minKeeperProfitRatioD18, uint256 maxKeeperRewardUsd, uint256 maxKeeperScalingRatioD18)
  ```

  Gets fired when keeper reward guard is set or updated.

**Parameters**
* `minKeeperRewardUsd` (*uint256*) - Minimum keeper reward expressed as USD value.
* `minKeeperProfitRatioD18` (*uint256*) - Minimum keeper profit ratio used together with minKeeperRewardUsd to calculate the minimum.
* `maxKeeperRewardUsd` (*uint256*) - Maximum keeper reward expressed as USD value.
* `maxKeeperScalingRatioD18` (*uint256*) - Scaling used to calculate the Maximum keeper reward together with maxKeeperRewardUsd.

#### FeeCollectorSet

  ```solidity
  event FeeCollectorSet(address feeCollector)
  ```

  emitted when custom fee collector is set

**Parameters**
* `feeCollector` (*address*) - the address of the fee collector to set.

#### ReferrerShareUpdated

  ```solidity
  event ReferrerShareUpdated(address referrer, uint256 shareRatioD18)
  ```

  Emitted when the share percentage for a referrer address has been updated.

**Parameters**
* `referrer` (*address*) - The address of the referrer
* `shareRatioD18` (*uint256*) - The new share ratio for the referrer

#### InterestRateParametersSet

  ```solidity
  event InterestRateParametersSet(uint256 lowUtilizationInterestRateGradient, uint256 interestRateGradientBreakpoint, uint256 highUtilizationInterestRateGradient)
  ```

  Emitted when interest rate parameters are set

**Parameters**
* `lowUtilizationInterestRateGradient` (*uint256*) - interest rate gradient applied to utilization prior to hitting the gradient breakpoint
* `interestRateGradientBreakpoint` (*uint256*) - breakpoint at which the interest rate gradient changes from low to high
* `highUtilizationInterestRateGradient` (*uint256*) - interest rate gradient applied to utilization after hitting the gradient breakpoint

#### PerAccountCapsSet

  ```solidity
  event PerAccountCapsSet(uint128 maxPositionsPerAccount, uint128 maxCollateralsPerAccount)
  ```

  Gets fired when the max number of Positions and Collaterals per Account are set by owner.

**Parameters**
* `maxPositionsPerAccount` (*uint128*) - The max number of concurrent Positions per Account
* `maxCollateralsPerAccount` (*uint128*) - The max number of concurrent Collaterals per Account

#### KeeperCostNodeIdUpdated

  ```solidity
  event KeeperCostNodeIdUpdated(bytes32 keeperCostNodeId)
  ```

  Gets fired when feed id for keeper cost node id is updated.

**Parameters**
* `keeperCostNodeId` (*bytes32*) - oracle node id

### Liquidation Module

#### liquidate

  ```solidity
  function liquidate(uint128 accountId) external returns (uint256 liquidationReward)
  ```

  Liquidates an account.

  according to the current situation and account size it can be a partial or full liquidation.

**Parameters**
* `accountId` (*uint128*) - Id of the account to liquidate.

**Returns**
* `liquidationReward` (*uint256*) - total reward sent to liquidator.
#### liquidateMarginOnly

  ```solidity
  function liquidateMarginOnly(uint128 accountId) external returns (uint256 liquidationReward)
  ```

  Liquidates an account's margin when no other positions exist.

  if available margin is negative and no positions exist, then account margin can be liquidated by calling this function

**Parameters**
* `accountId` (*uint128*) - Id of the account to liquidate.

**Returns**
* `liquidationReward` (*uint256*) - total reward sent to liquidator.
#### liquidateFlagged

  ```solidity
  function liquidateFlagged(uint256 maxNumberOfAccounts) external returns (uint256 liquidationReward)
  ```

  Liquidates up to maxNumberOfAccounts flagged accounts.

**Parameters**
* `maxNumberOfAccounts` (*uint256*) - max number of accounts to liquidate.

**Returns**
* `liquidationReward` (*uint256*) - total reward sent to liquidator.
#### liquidateFlaggedAccounts

  ```solidity
  function liquidateFlaggedAccounts(uint128[] accountIds) external returns (uint256 liquidationReward)
  ```

  Liquidates the listed flagged accounts.

  if any of the accounts is not flagged for liquidation it will be skipped.

**Parameters**
* `accountIds` (*uint128[]*) - list of account ids to liquidate.

**Returns**
* `liquidationReward` (*uint256*) - total reward sent to liquidator.
#### flaggedAccounts

  ```solidity
  function flaggedAccounts() external view returns (uint256[] accountIds)
  ```

  Returns the list of flagged accounts.

**Returns**
* `accountIds` (*uint256[]*) - list of flagged accounts.
#### canLiquidate

  ```solidity
  function canLiquidate(uint128 accountId) external view returns (bool isEligible)
  ```

  Returns if an account is eligible for liquidation.

**Returns**
* `isEligible` (*bool*) - 
#### canLiquidateMarginOnly

  ```solidity
  function canLiquidateMarginOnly(uint128 accountId) external view returns (bool isEligible)
  ```

  Returns if an account's margin is eligible for liquidation.

**Returns**
* `isEligible` (*bool*) - 
#### liquidationCapacity

  ```solidity
  function liquidationCapacity(uint128 marketId) external view returns (uint256 capacity, uint256 maxLiquidationInWindow, uint256 latestLiquidationTimestamp)
  ```

  Current liquidation capacity for the market

**Returns**
* `capacity` (*uint256*) - market can liquidate up to this #
* `maxLiquidationInWindow` (*uint256*) - max amount allowed to liquidate based on the current market configuration
* `latestLiquidationTimestamp` (*uint256*) - timestamp of the last liquidation of the market

#### PositionLiquidated

  ```solidity
  event PositionLiquidated(uint128 accountId, uint128 marketId, uint256 amountLiquidated, int128 currentPositionSize)
  ```

  Gets fired when an account position is liquidated .

**Parameters**
* `accountId` (*uint128*) - Id of the account liquidated.
* `marketId` (*uint128*) - Id of the position's market.
* `amountLiquidated` (*uint256*) - amount liquidated.
* `currentPositionSize` (*int128*) - position size after liquidation.

#### AccountFlaggedForLiquidation

  ```solidity
  event AccountFlaggedForLiquidation(uint128 accountId, int256 availableMargin, uint256 requiredMaintenanceMargin, uint256 liquidationReward, uint256 flagReward)
  ```

  Gets fired when an account is flagged for liquidation.

**Parameters**
* `accountId` (*uint128*) - Id of the account flagged.
* `availableMargin` (*int256*) - available margin after flagging.
* `requiredMaintenanceMargin` (*uint256*) - required maintenance margin which caused the flagging.
* `liquidationReward` (*uint256*) - reward for fully liquidating account paid when liquidation occurs.
* `flagReward` (*uint256*) - reward to keeper for flagging the account

#### AccountLiquidationAttempt

  ```solidity
  event AccountLiquidationAttempt(uint128 accountId, uint256 reward, bool fullLiquidation)
  ```

  Gets fired when an account is liquidated.

  this event is fired once per liquidation tx after the each position that can be liquidated at the time was liquidated.

**Parameters**
* `accountId` (*uint128*) - Id of the account liquidated.
* `reward` (*uint256*) - total reward sent to liquidator.
* `fullLiquidation` (*bool*) - flag indicating if it was a partial or full liquidation.

#### AccountMarginLiquidation

  ```solidity
  event AccountMarginLiquidation(uint128 accountId, uint256 seizedMarginValue, uint256 liquidationReward)
  ```

  Gets fired when an account margin is liquidated due to not paying down debt.

**Parameters**
* `accountId` (*uint128*) - Id of the account liquidated.
* `seizedMarginValue` (*uint256*) - margin seized due to liquidation.
* `liquidationReward` (*uint256*) - reward for liquidating margin account

### Market Configuration Module

#### addSettlementStrategy

  ```solidity
  function addSettlementStrategy(uint128 marketId, struct SettlementStrategy.Data strategy) external returns (uint256 strategyId)
  ```

  Add a new settlement strategy with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to add the settlement strategy.
* `strategy` (*struct SettlementStrategy.Data*) - strategy details (see SettlementStrategy.Data struct).

**Returns**
* `strategyId` (*uint256*) - id of the new settlement strategy.
#### setSettlementStrategy

  ```solidity
  function setSettlementStrategy(uint128 marketId, uint256 strategyId, struct SettlementStrategy.Data strategy) external
  ```

  updates a settlement strategy for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `strategyId` (*uint256*) - the specific strategy id.
* `strategy` (*struct SettlementStrategy.Data*) - strategy details (see SettlementStrategy.Data struct).

#### setOrderFees

  ```solidity
  function setOrderFees(uint128 marketId, uint256 makerFeeRatio, uint256 takerFeeRatio) external
  ```

  Set order fees for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to set order fees.
* `makerFeeRatio` (*uint256*) - the maker fee ratio.
* `takerFeeRatio` (*uint256*) - the taker fee ratio.

#### updatePriceData

  ```solidity
  function updatePriceData(uint128 perpsMarketId, bytes32 feedId, uint256 strictStalenessTolerance) external
  ```

  Set node id for perps market

**Parameters**
* `perpsMarketId` (*uint128*) - id of the market to set price feed.
* `feedId` (*bytes32*) - the node feed id
* `strictStalenessTolerance` (*uint256*) - strict price tolerance in seconds (used for liquidations primarily)

#### setFundingParameters

  ```solidity
  function setFundingParameters(uint128 marketId, uint256 skewScale, uint256 maxFundingVelocity) external
  ```

  Set funding parameters for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to set funding parameters.
* `skewScale` (*uint256*) - the skew scale.
* `maxFundingVelocity` (*uint256*) - the max funding velocity.

#### setMaxLiquidationParameters

  ```solidity
  function setMaxLiquidationParameters(uint128 marketId, uint256 maxLiquidationLimitAccumulationMultiplier, uint256 maxSecondsInLiquidationWindow, uint256 maxLiquidationPd, address endorsedLiquidator) external
  ```

  Set liquidation parameters for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to set liquidation parameters.
* `maxLiquidationLimitAccumulationMultiplier` (*uint256*) - the max liquidation limit accumulation multiplier.
* `maxSecondsInLiquidationWindow` (*uint256*) - the max seconds in liquidation window (used together with the acc multiplier to get max liquidation per window).
* `maxLiquidationPd` (*uint256*) - max allowed pd when calculating max liquidation amount
* `endorsedLiquidator` (*address*) - address of the endorsed liquidator who can fully liquidate accounts without any restriction

#### setLiquidationParameters

  ```solidity
  function setLiquidationParameters(uint128 marketId, uint256 initialMarginRatioD18, uint256 minimumInitialMarginRatioD18, uint256 maintenanceMarginScalarD18, uint256 flagRewardRatioD18, uint256 minimumPositionMargin) external
  ```

  Set liquidation parameters for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to set liquidation parameters.
* `initialMarginRatioD18` (*uint256*) - the initial margin ratio (as decimal with 18 digits precision).
* `minimumInitialMarginRatioD18` (*uint256*) - the minimum initial margin ratio (as decimal with 18 digits precision).
* `maintenanceMarginScalarD18` (*uint256*) - the maintenance margin scalar relative to the initial margin ratio (as decimal with 18 digits precision).
* `flagRewardRatioD18` (*uint256*) - the flag reward ratio (as decimal with 18 digits precision).
* `minimumPositionMargin` (*uint256*) - the minimum position margin.

#### setMaxMarketSize

  ```solidity
  function setMaxMarketSize(uint128 marketId, uint256 maxMarketSize) external
  ```

  Set the max size of an specific market with this function.

  This controls the maximum open interest a market can have on either side (Long | Short). So the total Open Interest (with zero skew) for a market can be up to max market size * 2.

**Parameters**
* `marketId` (*uint128*) - id of the market to set the max market value.
* `maxMarketSize` (*uint256*) - the max market size in market asset units.

#### setMaxMarketValue

  ```solidity
  function setMaxMarketValue(uint128 marketId, uint256 maxMarketValue) external
  ```

  Set the max value in USD of an specific market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to set the max market value.
* `maxMarketValue` (*uint256*) - the max market size in market USD value.

#### setLockedOiRatio

  ```solidity
  function setLockedOiRatio(uint128 marketId, uint256 lockedOiRatioD18) external
  ```

  Set the locked OI Ratio for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market to set locked OI ratio.
* `lockedOiRatioD18` (*uint256*) - the locked OI ratio skew scale (as decimal with 18 digits precision).

#### setSettlementStrategyEnabled

  ```solidity
  function setSettlementStrategyEnabled(uint128 marketId, uint256 strategyId, bool enabled) external
  ```

  Enable or disable a settlement strategy for a market with this function.

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `strategyId` (*uint256*) - the specific strategy.
* `enabled` (*bool*) - whether the strategy is enabled or disabled.

#### getSettlementStrategy

  ```solidity
  function getSettlementStrategy(uint128 marketId, uint256 strategyId) external view returns (struct SettlementStrategy.Data settlementStrategy)
  ```

  Gets the settlement strategy details.

**Parameters**
* `marketId` (*uint128*) - id of the market.
* `strategyId` (*uint256*) - id of the settlement strategy.

**Returns**
* `settlementStrategy` (*struct SettlementStrategy.Data*) - strategy details (see SettlementStrategy.Data struct).
#### getMaxLiquidationParameters

  ```solidity
  function getMaxLiquidationParameters(uint128 marketId) external view returns (uint256 maxLiquidationLimitAccumulationMultiplier, uint256 maxSecondsInLiquidationWindow, uint256 maxLiquidationPd, address endorsedLiquidator)
  ```

  Gets liquidation parameters details of a market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `maxLiquidationLimitAccumulationMultiplier` (*uint256*) - the max liquidation limit accumulation multiplier.
* `maxSecondsInLiquidationWindow` (*uint256*) - the max seconds in liquidation window (used together with the acc multiplier to get max liquidation per window).
* `maxLiquidationPd` (*uint256*) - max allowed pd when calculating max liquidation amount
* `endorsedLiquidator` (*address*) - address of the endorsed liquidator who can fully liquidate accounts without any restriction
#### getLiquidationParameters

  ```solidity
  function getLiquidationParameters(uint128 marketId) external view returns (uint256 initialMarginRatioD18, uint256 minimumInitialMarginRatioD18, uint256 maintenanceMarginScalarD18, uint256 flagRewardRatioD18, uint256 minimumPositionMargin)
  ```

  Gets liquidation parameters details of a market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `initialMarginRatioD18` (*uint256*) - the initial margin ratio (as decimal with 18 digits precision).
* `minimumInitialMarginRatioD18` (*uint256*) - the minimum initial margin ratio (as decimal with 18 digits precision).
* `maintenanceMarginScalarD18` (*uint256*) - the maintenance margin scalar relative to the initial margin ratio (as decimal with 18 digits precision).
* `flagRewardRatioD18` (*uint256*) - the flag reward ratio (as decimal with 18 digits precision).
* `minimumPositionMargin` (*uint256*) - the minimum position margin.
#### getFundingParameters

  ```solidity
  function getFundingParameters(uint128 marketId) external view returns (uint256 skewScale, uint256 maxFundingVelocity)
  ```

  Gets funding parameters of a market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `skewScale` (*uint256*) - the skew scale.
* `maxFundingVelocity` (*uint256*) - the max funding velocity.
#### getMaxMarketSize

  ```solidity
  function getMaxMarketSize(uint128 marketId) external view returns (uint256 maxMarketSize)
  ```

  Gets the max size of an specific market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `maxMarketSize` (*uint256*) - the max market size in market asset units.
#### getMaxMarketValue

  ```solidity
  function getMaxMarketValue(uint128 marketId) external view returns (uint256 maxMarketValue)
  ```

  Gets the max size (in value) of an specific market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `maxMarketValue` (*uint256*) - the max market size in market USD value.
#### getOrderFees

  ```solidity
  function getOrderFees(uint128 marketId) external view returns (uint256 makerFeeRatio, uint256 takerFeeRatio)
  ```

  Gets the order fees of a market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `makerFeeRatio` (*uint256*) - the maker fee ratio.
* `takerFeeRatio` (*uint256*) - the taker fee ratio.
#### getLockedOiRatio

  ```solidity
  function getLockedOiRatio(uint128 marketId) external view returns (uint256 lockedOiRatioD18)
  ```

  Gets the locked OI ratio of a market.

**Parameters**
* `marketId` (*uint128*) - id of the market.

**Returns**
* `lockedOiRatioD18` (*uint256*) - the locked OI ratio skew scale (as decimal with 18 digits precision).
#### getPriceData

  ```solidity
  function getPriceData(uint128 perpsMarketId) external view returns (bytes32 feedId, uint256 strictStalenessTolerance)
  ```

  Set node id for perps market

**Parameters**
* `perpsMarketId` (*uint128*) - id of the market to set price feed.

**Returns**
* `feedId` (*bytes32*) - the node feed id to get price
* `strictStalenessTolerance` (*uint256*) - 

#### SettlementStrategyAdded

  ```solidity
  event SettlementStrategyAdded(uint128 marketId, struct SettlementStrategy.Data strategy, uint256 strategyId)
  ```

  Gets fired when new settlement strategy is added.

**Parameters**
* `marketId` (*uint128*) - adds settlement strategy to this specific market.
* `strategy` (*struct SettlementStrategy.Data*) - the strategy configuration.
* `strategyId` (*uint256*) - the newly created settlement strategy id.

#### SettlementStrategySet

  ```solidity
  event SettlementStrategySet(uint128 marketId, uint256 strategyId, struct SettlementStrategy.Data strategy)
  ```

  Gets fired when new settlement strategy is updated.

**Parameters**
* `marketId` (*uint128*) - adds settlement strategy to this specific market.
* `strategyId` (*uint256*) - the newly created settlement strategy id.
* `strategy` (*struct SettlementStrategy.Data*) - the strategy configuration.

#### MarketPriceDataUpdated

  ```solidity
  event MarketPriceDataUpdated(uint128 marketId, bytes32 feedId, uint256 strictStalenessTolerance)
  ```

  Gets fired when feed id for perps market is updated.

**Parameters**
* `marketId` (*uint128*) - id of perps market
* `feedId` (*bytes32*) - oracle node id
* `strictStalenessTolerance` (*uint256*) - strict price tolerance in seconds (used for liquidations primarily)

#### OrderFeesSet

  ```solidity
  event OrderFeesSet(uint128 marketId, uint256 makerFeeRatio, uint256 takerFeeRatio)
  ```

  Gets fired when order fees are updated.

**Parameters**
* `marketId` (*uint128*) - udpates fees to this specific market.
* `makerFeeRatio` (*uint256*) - the maker fee ratio.
* `takerFeeRatio` (*uint256*) - the taker fee ratio.

#### FundingParametersSet

  ```solidity
  event FundingParametersSet(uint128 marketId, uint256 skewScale, uint256 maxFundingVelocity)
  ```

  Gets fired when funding parameters are updated.

**Parameters**
* `marketId` (*uint128*) - udpates funding parameters to this specific market.
* `skewScale` (*uint256*) - the skew scale.
* `maxFundingVelocity` (*uint256*) - the max funding velocity.

#### MaxLiquidationParametersSet

  ```solidity
  event MaxLiquidationParametersSet(uint128 marketId, uint256 maxLiquidationLimitAccumulationMultiplier, uint256 maxSecondsInLiquidationWindow, uint256 maxLiquidationPd, address endorsedLiquidator)
  ```

  Gets fired when parameters for max liquidation are set

**Parameters**
* `marketId` (*uint128*) - updates funding parameters to this specific market.
* `maxLiquidationLimitAccumulationMultiplier` (*uint256*) - the max liquidation limit accumulation multiplier.
* `maxSecondsInLiquidationWindow` (*uint256*) - the max seconds in liquidation window (used together with the acc multiplier to get max liquidation per window).
* `maxLiquidationPd` (*uint256*) - 
* `endorsedLiquidator` (*address*) - 

#### LiquidationParametersSet

  ```solidity
  event LiquidationParametersSet(uint128 marketId, uint256 initialMarginRatioD18, uint256 maintenanceMarginRatioD18, uint256 minimumInitialMarginRatioD18, uint256 flagRewardRatioD18, uint256 minimumPositionMargin)
  ```

  Gets fired when liquidation parameters are updated.

**Parameters**
* `marketId` (*uint128*) - udpates funding parameters to this specific market.
* `initialMarginRatioD18` (*uint256*) - the initial margin ratio (as decimal with 18 digits precision).
* `maintenanceMarginRatioD18` (*uint256*) - the maintenance margin ratio (as decimal with 18 digits precision).
* `minimumInitialMarginRatioD18` (*uint256*) - 
* `flagRewardRatioD18` (*uint256*) - the flag reward ratio (as decimal with 18 digits precision).
* `minimumPositionMargin` (*uint256*) - the minimum position margin.

#### MaxMarketSizeSet

  ```solidity
  event MaxMarketSizeSet(uint128 marketId, uint256 maxMarketSize)
  ```

  Gets fired when max market value is updated.

**Parameters**
* `marketId` (*uint128*) - udpates funding parameters to this specific market.
* `maxMarketSize` (*uint256*) - the max market size in units.

#### MaxMarketValueSet

  ```solidity
  event MaxMarketValueSet(uint128 marketId, uint256 maxMarketValue)
  ```

  Gets fired when max market value is updated.

**Parameters**
* `marketId` (*uint128*) - udpates funding parameters to this specific market.
* `maxMarketValue` (*uint256*) - the max market value in USD.

#### LockedOiRatioSet

  ```solidity
  event LockedOiRatioSet(uint128 marketId, uint256 lockedOiRatioD18)
  ```

  Gets fired when locked oi ratio is updated.

**Parameters**
* `marketId` (*uint128*) - udpates funding parameters to this specific market.
* `lockedOiRatioD18` (*uint256*) - the locked OI ratio skew scale (as decimal with 18 digits precision).

### IMarketEvents

#### MarketUpdated

  ```solidity
  event MarketUpdated(uint128 marketId, uint256 price, int256 skew, uint256 size, int256 sizeDelta, int256 currentFundingRate, int256 currentFundingVelocity, uint128 interestRate)
  ```

  Gets fired when the size of a market is updated by new orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Id of the market used for the trade.
* `price` (*uint256*) - Price at the time of this event.
* `skew` (*int256*) - Market skew at the time of the trade. Positive values mean more longs.
* `size` (*uint256*) - Size of the entire market after settlement.
* `sizeDelta` (*int256*) - Change in market size during this update.
* `currentFundingRate` (*int256*) - The current funding rate of this market (0.001 = 0.1% per day)
* `currentFundingVelocity` (*int256*) - The current rate of change of the funding rate (0.001 = +0.1% per day)
* `interestRate` (*uint128*) - Current supermarket interest rate based on updated market OI.

### Perps Account Module

#### modifyCollateral

  ```solidity
  function modifyCollateral(uint128 accountId, uint128 collateralId, int256 amountDelta) external
  ```

  Modify the collateral delegated to the account.

**Parameters**
* `accountId` (*uint128*) - Id of the account.
* `collateralId` (*uint128*) - Id of the synth market used as collateral. Synth market id, 0 for snxUSD.
* `amountDelta` (*int256*) - requested change in amount of collateral delegated to the account.

#### getCollateralAmount

  ```solidity
  function getCollateralAmount(uint128 accountId, uint128 collateralId) external view returns (uint256)
  ```

  Gets the account's collateral value for a specific collateral.

**Parameters**
* `accountId` (*uint128*) - Id of the account.
* `collateralId` (*uint128*) - Id of the synth market used as collateral. Synth market id, 0 for snxUSD.

**Returns**
* `[0]` (*uint256*) - collateralValue collateral value of the account.
#### getAccountCollateralIds

  ```solidity
  function getAccountCollateralIds(uint128 accountId) external view returns (uint256[])
  ```

  Gets the account's collaterals ids

**Parameters**
* `accountId` (*uint128*) - Id of the account.

#### getAccountOpenPositions

  ```solidity
  function getAccountOpenPositions(uint128 accountId) external view returns (uint256[])
  ```

  Gets all markets that a given account id has a position in

**Parameters**
* `accountId` (*uint128*) - Id of the account.

#### totalCollateralValue

  ```solidity
  function totalCollateralValue(uint128 accountId) external view returns (uint256)
  ```

  Gets the account's total collateral value without the discount applied.

**Parameters**
* `accountId` (*uint128*) - Id of the account.

**Returns**
* `[0]` (*uint256*) - collateralValue total collateral value of the account without discount. USD denominated.
#### totalAccountOpenInterest

  ```solidity
  function totalAccountOpenInterest(uint128 accountId) external view returns (uint256)
  ```

  Gets the account's total open interest value.

**Parameters**
* `accountId` (*uint128*) - Id of the account.

**Returns**
* `[0]` (*uint256*) - openInterestValue total open interest value of the account.
#### getOpenPosition

  ```solidity
  function getOpenPosition(uint128 accountId, uint128 marketId) external view returns (int256 totalPnl, int256 accruedFunding, int128 positionSize, uint256 owedInterest)
  ```

  Gets the details of an open position.

**Parameters**
* `accountId` (*uint128*) - Id of the account.
* `marketId` (*uint128*) - Id of the position market.

**Returns**
* `totalPnl` (*int256*) - pnl of the entire position including funding.
* `accruedFunding` (*int256*) - accrued funding of the position.
* `positionSize` (*int128*) - size of the position.
* `owedInterest` (*uint256*) - interest owed due to open position.
#### getOpenPositionSize

  ```solidity
  function getOpenPositionSize(uint128 accountId, uint128 marketId) external view returns (int128 positionSize)
  ```

  Gets an account open position data for a given account id and market id
this function doesn't have any price staleness requirement

**Parameters**
* `accountId` (*uint128*) - Id of the account.
* `marketId` (*uint128*) - Id of the position market.

#### getAvailableMargin

  ```solidity
  function getAvailableMargin(uint128 accountId) external view returns (int256 availableMargin)
  ```

  Gets the available margin of an account. It can be negative due to pnl.

**Parameters**
* `accountId` (*uint128*) - Id of the account.

**Returns**
* `availableMargin` (*int256*) - available margin of the position.
#### getWithdrawableMargin

  ```solidity
  function getWithdrawableMargin(uint128 accountId) external view returns (int256 withdrawableMargin)
  ```

  Gets the exact withdrawable amount a trader has available from this account while holding the account's current positions.

**Parameters**
* `accountId` (*uint128*) - Id of the account.

**Returns**
* `withdrawableMargin` (*int256*) - available margin to withdraw.
#### getRequiredMargins

  ```solidity
  function getRequiredMargins(uint128 accountId) external view returns (uint256 requiredInitialMargin, uint256 requiredMaintenanceMargin, uint256 maxLiquidationReward)
  ```

  Gets the initial/maintenance margins across all positions that an account has open.

  Note that requiredInitialMargin and requiredMaintenanceMargin includes the liquidation rewards, in case you want the value without it you need to substract maxLiquidationReward.

**Parameters**
* `accountId` (*uint128*) - Id of the account.

**Returns**
* `requiredInitialMargin` (*uint256*) - initial margin req (used when withdrawing collateral).
* `requiredMaintenanceMargin` (*uint256*) - maintenance margin req (used to determine liquidation threshold).
* `maxLiquidationReward` (*uint256*) - max liquidation reward the keeper would receive if account was fully liquidated. Note here that the accumulated rewards are checked against the global max/min configured liquidation rewards.
#### payDebt

  ```solidity
  function payDebt(uint128 accountId, uint256 amount) external
  ```

  Allows anyone to pay an account's debt

**Parameters**
* `accountId` (*uint128*) - Id of the account.
* `amount` (*uint256*) - debt amount to pay off

#### debt

  ```solidity
  function debt(uint128 accountId) external view returns (uint256 accountDebt)
  ```

  Returns account's debt

**Parameters**
* `accountId` (*uint128*) - Id of the account.

**Returns**
* `accountDebt` (*uint256*) - specified account id's debt

#### CollateralModified

  ```solidity
  event CollateralModified(uint128 accountId, uint128 collateralId, int256 amountDelta, address sender)
  ```

  Gets fired when an account colateral is modified.

**Parameters**
* `accountId` (*uint128*) - Id of the account.
* `collateralId` (*uint128*) - Id of the synth market used as collateral. Synth market id, 0 for snxUSD.
* `amountDelta` (*int256*) - requested change in amount of collateral delegated to the account.
* `sender` (*address*) - address of the sender of the size modification. Authorized by account owner.

#### DebtPaid

  ```solidity
  event DebtPaid(uint128 accountId, uint256 amount, address sender)
  ```

### Perps Market Factory Module

#### initializeFactory

  ```solidity
  function initializeFactory(contract ISynthetixSystem synthetix, contract ISpotMarketSystem spotMarket) external returns (uint128)
  ```

  Initializes the factory.

  this function should be called only once.

**Returns**
* `[0]` (*uint128*) - globalPerpsMarketId Id of the global perps market id.
#### setPerpsMarketName

  ```solidity
  function setPerpsMarketName(string marketName) external
  ```

  Sets the perps market name.

**Parameters**
* `marketName` (*string*) - the new perps market name.

#### createMarket

  ```solidity
  function createMarket(uint128 requestedMarketId, string marketName, string marketSymbol) external returns (uint128)
  ```

  Creates a new market.

**Parameters**
* `requestedMarketId` (*uint128*) - id of the market to create.
* `marketName` (*string*) - name of the market to create.
* `marketSymbol` (*string*) - symbol of the market to create.

**Returns**
* `[0]` (*uint128*) - perpsMarketId Id of the created perps market.
#### interestRate

  ```solidity
  function interestRate() external view returns (uint128 rate)
  ```

  Returns the current market interest rate

**Returns**
* `rate` (*uint128*) - 
#### utilizationRate

  ```solidity
  function utilizationRate() external view returns (uint256 rate, uint256 delegatedCollateral, uint256 lockedCredit)
  ```

  Returns the super market utilization rate

  The rate is the minimumCredit / delegatedCollateral available.
Locked credit is the sum of all markets open interest * configured lockedOiRatio
delegatedCollateral is the avaialble collateral value for markets to withdraw, delegated by LPs

**Returns**
* `rate` (*uint256*) - 
* `delegatedCollateral` (*uint256*) - 
* `lockedCredit` (*uint256*) - credit locked based on OI & lockedOiRatio
#### name

  ```solidity
  function name(uint128 marketId) external view returns (string)
  ```

  returns a human-readable name for a given market

#### reportedDebt

  ```solidity
  function reportedDebt(uint128 marketId) external view returns (uint256)
  ```

  returns amount of USD that the market would try to mint if everything was withdrawn

#### minimumCredit

  ```solidity
  function minimumCredit(uint128 marketId) external view returns (uint256)
  ```

  prevents reduction of available credit capacity by specifying this amount, for which withdrawals will be disallowed

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

#### FactoryInitialized

  ```solidity
  event FactoryInitialized(uint128 globalPerpsMarketId)
  ```

  Gets fired when the factory is initialized.

**Parameters**
* `globalPerpsMarketId` (*uint128*) - the new global perps market id.

#### MarketCreated

  ```solidity
  event MarketCreated(uint128 perpsMarketId, string marketName, string marketSymbol)
  ```

  Gets fired when a market is created.

**Parameters**
* `perpsMarketId` (*uint128*) - the newly created perps market id.
* `marketName` (*string*) - the newly created perps market name.
* `marketSymbol` (*string*) - the newly created perps market symbol.

### Perps Market Module

#### metadata

  ```solidity
  function metadata(uint128 marketId) external view returns (string name, string symbol)
  ```

  Gets a market metadata.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `name` (*string*) - Name of the market.
* `symbol` (*string*) - Symbol of the market.
#### skew

  ```solidity
  function skew(uint128 marketId) external view returns (int256)
  ```

  Gets a market's skew.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `[0]` (*int256*) - skew Skew of the market.
#### size

  ```solidity
  function size(uint128 marketId) external view returns (uint256)
  ```

  Gets a market's size.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `[0]` (*uint256*) - size Size of the market.
#### maxOpenInterest

  ```solidity
  function maxOpenInterest(uint128 marketId) external view returns (uint256)
  ```

  Gets a market's max open interest.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `[0]` (*uint256*) - maxOpenInterest Max open interest of the market.
#### currentFundingRate

  ```solidity
  function currentFundingRate(uint128 marketId) external view returns (int256)
  ```

  Gets a market's current funding rate.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `[0]` (*int256*) - currentFundingRate Current funding rate of the market.
#### currentFundingVelocity

  ```solidity
  function currentFundingVelocity(uint128 marketId) external view returns (int256)
  ```

  Gets a market's current funding velocity.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `[0]` (*int256*) - currentFundingVelocity Current funding velocity of the market.
#### indexPrice

  ```solidity
  function indexPrice(uint128 marketId) external view returns (uint256)
  ```

  Gets a market's index price.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `[0]` (*uint256*) - indexPrice Index price of the market.
#### fillPrice

  ```solidity
  function fillPrice(uint128 marketId, int128 orderSize, uint256 price) external view returns (uint256)
  ```

  Gets a market's fill price for a specific order size and index price.

**Parameters**
* `marketId` (*uint128*) - Id of the market.
* `orderSize` (*int128*) - Order size.
* `price` (*uint256*) - Index price.

**Returns**
* `[0]` (*uint256*) - price Fill price.
#### getMarketSummary

  ```solidity
  function getMarketSummary(uint128 marketId) external view returns (struct IPerpsMarketModule.MarketSummary summary)
  ```

  Given a marketId return a market's summary details in one call.

**Parameters**
* `marketId` (*uint128*) - Id of the market.

**Returns**
* `summary` (*struct IPerpsMarketModule.MarketSummary*) - Market summary (see MarketSummary).

## Legacy Market

### ILegacyMarket

#### v2xResolver

  ```solidity
  function v2xResolver() external view returns (contract IAddressResolver)
  ```

#### v3System

  ```solidity
  function v3System() external view returns (contract IV3CoreProxy)
  ```

#### rewardsDistributor

  ```solidity
  function rewardsDistributor() external view returns (contract ISNXDistributor)
  ```

#### convertUSD

  ```solidity
  function convertUSD(uint256 amount) external
  ```

  Called by anyone with {amount} sUSD to convert {amount} sUSD to {amount} snxUSD.
The sUSD will be burned (thereby reducing the sUSD total supply and v2x system size), and snxUSD will be minted.
Any user who has sUSD can call this function. If you have migrated to v3 and there is insufficient sUSD liquidity
to convert, consider buying snxUSD on the open market, since that means most snxUSD has already been migrated.
Requirements:
* User must first approve() the legacy market contract to spend the user's sUSD
* LegacyMarket must have already sufficient migrated collateral

**Parameters**
* `amount` (*uint256*) - the quantity to convert

#### migrate

  ```solidity
  function migrate(uint128 accountId) external
  ```

  Called by an SNX staker on v2x to convert their position to the equivalent on v3. This entails the following broad steps:
1. collect all their SNX collateral and debt from v2x
2. create a new staking account on v3 with the supplied {accountId}
3. put the collateral and debt into this newly created staking account
4. send the created staking account to the ERC2771Context._msgSender().

**Parameters**
* `accountId` (*uint128*) - the new account id that the user wants to have. can be any non-zero integer that is not already occupied.

#### migrateOnBehalf

  ```solidity
  function migrateOnBehalf(address staker, uint128 accountId) external
  ```

  Same as `migrate`, but allows for the owner to forcefully migrate any v2x staker

**Parameters**
* `staker` (*address*) - 
* `accountId` (*uint128*) - the new account id that the user wants to have. can be any non-zero integer that is not already occupied.

#### registerMarket

  ```solidity
  function registerMarket() external returns (uint128 newMarketId)
  ```

  called by the owner to register this market with v3. This is an initialization call only.

#### setSystemAddresses

  ```solidity
  function setSystemAddresses(contract IAddressResolver v2xResolverAddress, contract IV3CoreProxy v3SystemAddress, contract ISNXDistributor snxDistributor) external returns (bool didInitialize)
  ```

  called by the owner to set the addresses of the v3 and v2x systems which are needed for calls in `migrate` and `convertUSD`

**Parameters**
* `v2xResolverAddress` (*contract IAddressResolver*) - the v2x `AddressResolver` contract address. LegacyMarket can use AddressResolver to get the address of any other v2x contract.
* `v3SystemAddress` (*contract IV3CoreProxy*) - the v3 core proxy address
* `snxDistributor` (*contract ISNXDistributor*) - the SNXDistributor which should be used if an account is liquidated

#### setPauseStablecoinConversion

  ```solidity
  function setPauseStablecoinConversion(bool paused) external
  ```

  called by the owner to disable `convertUSD` (ex. in the case of an emergency)

**Parameters**
* `paused` (*bool*) - whether or not `convertUSD` should be disable

#### setPauseMigration

  ```solidity
  function setPauseMigration(bool paused) external
  ```

  called by the owner to disable `migrate` (ex. in the case of an emergency)

**Parameters**
* `paused` (*bool*) - whether or not `migrate` should be disable

#### AccountMigrated

  ```solidity
  event AccountMigrated(address staker, uint256 accountId, uint256 collateralAmount, uint256 debtAmount)
  ```

  Emitted after an account has been migrated from the (legacy) v2x system to v3

**Parameters**
* `staker` (*address*) - the address of the v2x staker that migrated
* `accountId` (*uint256*) - the new account id
* `collateralAmount` (*uint256*) - the amount of SNX migrated to v3
* `debtAmount` (*uint256*) - the value of new debt now managed by v3

#### AccountLiquidatedInMigration

  ```solidity
  event AccountLiquidatedInMigration(address staker, uint256 collateralAmount, uint256 debtAmount, uint256 cratio)
  ```

  Emitted if an account was migrated but its c-ratioi was insufficient for assigning debt in v3

**Parameters**
* `staker` (*address*) - the address of the v2x staker that migrated
* `collateralAmount` (*uint256*) - the amount of SNX migrated to v3
* `debtAmount` (*uint256*) - the value of new debt now managed by v3
* `cratio` (*uint256*) - the calculated c-ratio of the account

#### ConvertedUSD

  ```solidity
  event ConvertedUSD(address account, uint256 amount)
  ```

  Emitted after a call to `convertUSD`, moving debt from v2x to v3.

**Parameters**
* `account` (*address*) - the address of the address which provided the sUSD for conversion
* `amount` (*uint256*) - the amount of sUSD burnt, and the amount of snxUSD minted

#### PauseStablecoinConversionSet

  ```solidity
  event PauseStablecoinConversionSet(address sender, bool paused)
  ```

  Emitted after a call to `setPauseStablecoinConversion`

**Parameters**
* `sender` (*address*) - the address setting the stablecoin conversion pause status
* `paused` (*bool*) - whether stablecoin conversion is being paused or unpaused

#### PauseMigrationSet

  ```solidity
  event PauseMigrationSet(address sender, bool paused)
  ```

  Emitted after a call to `setPauseMigration`

**Parameters**
* `sender` (*address*) - the address setting the migration pause status
* `paused` (*bool*) - whether migration is being paused or unpaused

### ISNXDistributor

#### notifyRewardAmount

  ```solidity
  function notifyRewardAmount(uint256 reward) external
  ```

## BFP Market

### IBasePerpMarket

#### FundingRecomputed

  ```solidity
  event FundingRecomputed(uint128 marketId, int128 skew, int128 fundingRate, int128 fundingVelocity)
  ```

  Emitted when funding is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their funding recomputed
* `skew` (*int128*) - Current skew at the point of recomputation
* `fundingRate` (*int128*) - 
* `fundingVelocity` (*int128*) - Current instantaneous velocity at the point of recomputation

#### UtilizationRecomputed

  ```solidity
  event UtilizationRecomputed(uint128 marketId, int128 skew, uint128 utilizationRate)
  ```

  Emitted when utilization is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their utilization recomputed
* `skew` (*int128*) - Current market skew at the point of recomputation
* `utilizationRate` (*uint128*) - New utilization rate after recomputation

#### OrderCanceled

  ```solidity
  event OrderCanceled(uint128 accountId, uint128 marketId, uint256 keeperFee, uint64 commitmentTime)
  ```

  Emitted when an order is canceled.

**Parameters**
* `accountId` (*uint128*) - Account of order that was canceled
* `marketId` (*uint128*) - Market the order was canceled against
* `keeperFee` (*uint256*) - Fee paid to keeper for canceling order
* `commitmentTime` (*uint64*) - block.timestamp of order at the point of comment

#### MarketSizeUpdated

  ```solidity
  event MarketSizeUpdated(uint128 marketId, uint128 size, int128 skew)
  ```

  Emitted when the market's size is updated either due to orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Market that had their size updated
* `size` (*uint128*) - New market size post update
* `skew` (*int128*) - New market skew post update

### Feature Flag Module

#### suspendAllFeatures

  ```solidity
  function suspendAllFeatures() external
  ```

  Suspends all features. Can be called by owner or a configured "denier".

#### enableAllFeatures

  ```solidity
  function enableAllFeatures() external
  ```

  Enable all features. Can be called by owner.

#### setFeatureFlagAllowAll

  ```solidity
  function setFeatureFlagAllowAll(bytes32 feature, bool allowAll) external
  ```

  Enables or disables free access to a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `allowAll` (*bool*) - True to allow anyone to use the feature, false to fallback to the allowlist.

#### setFeatureFlagDenyAll

  ```solidity
  function setFeatureFlagDenyAll(bytes32 feature, bool denyAll) external
  ```

  Enables or disables free access to a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `denyAll` (*bool*) - True to allow noone to use the feature, false to fallback to the allowlist.

#### addToFeatureFlagAllowlist

  ```solidity
  function addToFeatureFlagAllowlist(bytes32 feature, address account) external
  ```

  Allows an address to use a feature.

  This function does nothing if the specified account is already on the allowlist.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that is allowed to use the feature.

#### removeFromFeatureFlagAllowlist

  ```solidity
  function removeFromFeatureFlagAllowlist(bytes32 feature, address account) external
  ```

  Disallows an address from using a feature.

  This function does nothing if the specified account is already on the allowlist.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that is disallowed from using the feature.

#### setDeniers

  ```solidity
  function setDeniers(bytes32 feature, address[] deniers) external
  ```

  Sets addresses which can disable a feature (but not enable it). Overwrites any preexisting data.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `deniers` (*address[]*) - The addresses which should have the ability to unilaterally disable the feature

#### getDeniers

  ```solidity
  function getDeniers(bytes32 feature) external view returns (address[])
  ```

  Gets the list of address which can block a feature

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

#### getFeatureFlagAllowAll

  ```solidity
  function getFeatureFlagAllowAll(bytes32 feature) external view returns (bool)
  ```

  Determines if the given feature is freely allowed to all users.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

**Returns**
* `[0]` (*bool*) - True if anyone is allowed to use the feature, false if per-user control is used.
#### getFeatureFlagDenyAll

  ```solidity
  function getFeatureFlagDenyAll(bytes32 feature) external view returns (bool)
  ```

  Determines if the given feature is denied to all users.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

**Returns**
* `[0]` (*bool*) - True if noone is allowed to use the feature.
#### getFeatureFlagAllowlist

  ```solidity
  function getFeatureFlagAllowlist(bytes32 feature) external view returns (address[])
  ```

  Returns a list of addresses that are allowed to use the specified feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.

**Returns**
* `[0]` (*address[]*) - The queried list of addresses.
#### isFeatureAllowed

  ```solidity
  function isFeatureAllowed(bytes32 feature, address account) external view returns (bool)
  ```

  Determines if an address can use the specified feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that is being queried for access to the feature.

**Returns**
* `[0]` (*bool*) - A boolean with the response to the query.

#### PerpMarketSuspended

  ```solidity
  event PerpMarketSuspended(bool suspended)
  ```

  Emitted when all features get suspended or enabled.

**Parameters**
* `suspended` (*bool*) - True to indicate the market was suspended or false if enabled

#### FeatureFlagAllowAllSet

  ```solidity
  event FeatureFlagAllowAllSet(bytes32 feature, bool allowAll)
  ```

  Emitted when general access has been given or removed for a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `allowAll` (*bool*) - True if the feature was allowed for everyone and false if it is only allowed for those included in the allowlist.

#### FeatureFlagDenyAllSet

  ```solidity
  event FeatureFlagDenyAllSet(bytes32 feature, bool denyAll)
  ```

  Emitted when general access has been blocked for a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `denyAll` (*bool*) - True if the feature was blocked for everyone and false if it is only allowed for those included in the allowlist or if allowAll is set to true.

#### FeatureFlagAllowlistAdded

  ```solidity
  event FeatureFlagAllowlistAdded(bytes32 feature, address account)
  ```

  Emitted when an address was given access to a feature.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that was given access to the feature.

#### FeatureFlagAllowlistRemoved

  ```solidity
  event FeatureFlagAllowlistRemoved(bytes32 feature, address account)
  ```

  Emitted when access to a feature has been removed from an address.

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `account` (*address*) - The address that no longer has access to the feature.

#### FeatureFlagDeniersReset

  ```solidity
  event FeatureFlagDeniersReset(bytes32 feature, address[] deniers)
  ```

  Emitted when the list of addresses which can block a feature has been updated

**Parameters**
* `feature` (*bytes32*) - The bytes32 id of the feature.
* `deniers` (*address[]*) - The list of addresses which are allowed to block a feature

### Liquidation Module

#### flagPosition

  ```solidity
  function flagPosition(uint128 accountId, uint128 marketId) external
  ```

  Flags position belonging to `accountId` for liquidation. A flagged position is frozen from all operations.

**Parameters**
* `accountId` (*uint128*) - Account id of position to be flagged for liquidation
* `marketId` (*uint128*) - Market id of position to be flagged for liquidation

#### liquidatePosition

  ```solidity
  function liquidatePosition(uint128 accountId, uint128 marketId) external
  ```

  Liquidates a flagged position. A position must be flagged first before it can be liquidated.

**Parameters**
* `accountId` (*uint128*) - Account id of previously flagged position for liquidation
* `marketId` (*uint128*) - Market id of previously flagged position for liquidation

#### liquidateMarginOnly

  ```solidity
  function liquidateMarginOnly(uint128 accountId, uint128 marketId) external
  ```

  Liquidates an account's margin (only) due to debt by.

**Parameters**
* `accountId` (*uint128*) - Account id the margin account to liquidate
* `marketId` (*uint128*) - Market id of the margin account to liquidate

#### getLiquidationFees

  ```solidity
  function getLiquidationFees(uint128 accountId, uint128 marketId) external view returns (uint256 liqReward, uint256 keeperFee)
  ```

  Returns fees paid to flagger and liquidator (in USD) if position successfully liquidated.

**Parameters**
* `accountId` (*uint128*) - Account of the position to query against
* `marketId` (*uint128*) - Market of the position to query against

**Returns**
* `liqReward` (*uint256*) - USD fee paid as reward to keeper for flagging position for liquidation
* `keeperFee` (*uint256*) - USD fee paid as reward to keeper for executing liquidation on flagged position
#### getRemainingLiquidatableSizeCapacity

  ```solidity
  function getRemainingLiquidatableSizeCapacity(uint128 marketId) external view returns (uint128 maxLiquidatableCapacity, uint128 remainingCapacity, uint128 lastLiquidationTime)
  ```

  Returns the remaining liquidation capacity for a given `marketId` in the current liquidation window.

**Parameters**
* `marketId` (*uint128*) - The market the to query against

**Returns**
* `maxLiquidatableCapacity` (*uint128*) - Maximum size that can be liquidated in a single chunk
* `remainingCapacity` (*uint128*) - Remaining size in the current liquidation window before cap is met
* `lastLiquidationTime` (*uint128*) - block.timestamp of when the last time a liquidation occurred
#### isPositionLiquidatable

  ```solidity
  function isPositionLiquidatable(uint128 accountId, uint128 marketId) external view returns (bool)
  ```

  Returns whether a position owned by `accountId` can be flagged for liquidated.

**Parameters**
* `accountId` (*uint128*) - Account of the position to query against
* `marketId` (*uint128*) - Market of the position to query against

**Returns**
* `[0]` (*bool*) - isPositionLiquidatable True if position can be flagged for liquidation, false otherwise
#### isMarginLiquidatable

  ```solidity
  function isMarginLiquidatable(uint128 accountId, uint128 marketId) external view returns (bool)
  ```

  Returns whether an accounts margin can be liquidated.

**Parameters**
* `accountId` (*uint128*) - Account of margin to query against
* `marketId` (*uint128*) - Market of margin to query against

**Returns**
* `[0]` (*bool*) - isMarginLiquidatable True if margin can be liquidated, false otherwise
#### getLiquidationMarginUsd

  ```solidity
  function getLiquidationMarginUsd(uint128 accountId, uint128 marketId, int128 sizeDelta) external view returns (uint256 im, uint256 mm)
  ```

  Returns the IM (initial margin) and MM (maintenance margin) for a given account, market, and sizeDelta.
        Specify a sizeDelta of 0 for the current IM/MM of an existing position.

**Parameters**
* `accountId` (*uint128*) - Account of position to query against
* `marketId` (*uint128*) - Market of position to query against
* `sizeDelta` (*int128*) - 

**Returns**
* `im` (*uint256*) - Required initial margin in USD
* `mm` (*uint256*) - Required maintenance margin in USD
#### getHealthFactor

  ```solidity
  function getHealthFactor(uint128 accountId, uint128 marketId) external view returns (uint256)
  ```

  Returns the health factor for a given `accountId` by `marketId`. <= 1 means the position can be liquidated.

**Parameters**
* `accountId` (*uint128*) - Account of position to query against
* `marketId` (*uint128*) - Market of position to query against

**Returns**
* `[0]` (*uint256*) - getHealthFactor A number, which when lte 1 results in liquidation and above 1 is healthy

#### PositionFlaggedLiquidation

  ```solidity
  event PositionFlaggedLiquidation(uint128 accountId, uint128 marketId, address flagger, uint256 flagKeeperReward, uint256 flaggedPrice)
  ```

  Emitted when a position is flagged for liquidation.

**Parameters**
* `accountId` (*uint128*) - Account of position flagged for liqudation
* `marketId` (*uint128*) - Market of the position flagged
* `flagger` (*address*) - Address of keeper that executed flag
* `flagKeeperReward` (*uint256*) - USD fee paid to keeper for invoking flag
* `flaggedPrice` (*uint256*) - Market oracle price at the time of flag

#### PositionLiquidated

  ```solidity
  event PositionLiquidated(uint128 accountId, uint128 marketId, int128 sizeBeforeLiquidation, int128 remainingSize, address keeper, address flagger, uint256 liqKeeperFee, uint256 liquidationPrice)
  ```

  Emitted when a position has been liquidated.

**Parameters**
* `accountId` (*uint128*) - Account of the liquidated position
* `marketId` (*uint128*) - Market of the liquidated position
* `sizeBeforeLiquidation` (*int128*) - Position size before liquidation occurred
* `remainingSize` (*int128*) - Position size after liquidation
* `keeper` (*address*) - Address of keeper that executed liquidation
* `flagger` (*address*) - 
* `liqKeeperFee` (*uint256*) - USD fee paid to the keeper for invoking liquidation
* `liquidationPrice` (*uint256*) - Market oracle price at the time of liquidation

#### MarginLiquidated

  ```solidity
  event MarginLiquidated(uint128 accountId, uint128 marketId, uint256 keeperReward)
  ```

  Emitted when margin is liquidated due to debt.

**Parameters**
* `accountId` (*uint128*) - Account that had their margin liquidated
* `marketId` (*uint128*) - Market of liquidated account margin (isolated)
* `keeperReward` (*uint256*) - USD fee paid to keeper for liquidating account margin

#### FundingRecomputed

  ```solidity
  event FundingRecomputed(uint128 marketId, int128 skew, int128 fundingRate, int128 fundingVelocity)
  ```

  Emitted when funding is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their funding recomputed
* `skew` (*int128*) - Current skew at the point of recomputation
* `fundingRate` (*int128*) - 
* `fundingVelocity` (*int128*) - Current instantaneous velocity at the point of recomputation

#### UtilizationRecomputed

  ```solidity
  event UtilizationRecomputed(uint128 marketId, int128 skew, uint128 utilizationRate)
  ```

  Emitted when utilization is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their utilization recomputed
* `skew` (*int128*) - Current market skew at the point of recomputation
* `utilizationRate` (*uint128*) - New utilization rate after recomputation

#### OrderCanceled

  ```solidity
  event OrderCanceled(uint128 accountId, uint128 marketId, uint256 keeperFee, uint64 commitmentTime)
  ```

  Emitted when an order is canceled.

**Parameters**
* `accountId` (*uint128*) - Account of order that was canceled
* `marketId` (*uint128*) - Market the order was canceled against
* `keeperFee` (*uint256*) - Fee paid to keeper for canceling order
* `commitmentTime` (*uint64*) - block.timestamp of order at the point of comment

#### MarketSizeUpdated

  ```solidity
  event MarketSizeUpdated(uint128 marketId, uint128 size, int128 skew)
  ```

  Emitted when the market's size is updated either due to orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Market that had their size updated
* `size` (*uint128*) - New market size post update
* `skew` (*int128*) - New market skew post update

### Margin Module

#### payDebt

  ```solidity
  function payDebt(uint128 accountId, uint128 marketId, uint128 amount) external
  ```

  Pay debt belonging to `accountId` and `marketId` with sUSD available in margin. Users can partially pay
        off their debt. If the amount is larger than the available debt, only the delta will be withdrawn from
        margin.
sUSD held in margin takes precedence over those in the caller's wallet.

**Parameters**
* `accountId` (*uint128*) - Account of the margin to pay debt on
* `marketId` (*uint128*) - Market of the margin to pay debt on
* `amount` (*uint128*) - USD amount of debt to pay off

#### withdrawAllCollateral

  ```solidity
  function withdrawAllCollateral(uint128 accountId, uint128 marketId) external
  ```

  Withdraws all deposited margin collateral for `accountId` and `marketId`.

  Will revert if account has open positions, pending orders, or any unpaid debt.

**Parameters**
* `accountId` (*uint128*) - Account of the margin account to withdraw from
* `marketId` (*uint128*) - Market of the margin account to withdraw from

#### modifyCollateral

  ```solidity
  function modifyCollateral(uint128 accountId, uint128 marketId, address collateralAddress, int256 amountDelta) external
  ```

  Modifies the `collateralAddress` margin for `accountId` on `marketId` by the `amountDelta`. A negative amount
        signifies a withdraw and positive is deposit. A variety of errors are thrown if limits or collateral
        issues are found.

  Modifying collateral will immediately deposit collateral into the Synthetix core system.

**Parameters**
* `accountId` (*uint128*) - Account to modify margin collateral against
* `marketId` (*uint128*) - Market to modify margin collateral against
* `collateralAddress` (*address*) - Address of collateral to deposit or withdraw
* `amountDelta` (*int256*) - Amount of collateral to deposit or withdraw

#### setMarginCollateralConfiguration

  ```solidity
  function setMarginCollateralConfiguration(address[] collateralAddresses, bytes32[] oracleNodeIds, uint128[] maxAllowables, uint128[] skewScales, address[] rewardDistributors) external
  ```

  Configure with collateral types, their max allowables (deposits), their skewScale and reward
        distributors. This function will reconfigure _all_ collaterals and replace the existing
        collateral set with new collaterals supplied.

**Parameters**
* `collateralAddresses` (*address[]*) - An array of collateral addresses.
* `oracleNodeIds` (*bytes32[]*) - An array of oracle nods for each collateral
* `maxAllowables` (*uint128[]*) - An array of integers to indicate the global maximum deposit amount
* `skewScales` (*uint128[]*) - An array of integers for skew scales for each collateral
* `rewardDistributors` (*address[]*) - An array of addresses to each reward distributor

#### setCollateralMaxAllowable

  ```solidity
  function setCollateralMaxAllowable(address collateralAddress, uint128 maxAllowable) external
  ```

  Set the max allowable for existing collateral by `collateralAddress`.

**Parameters**
* `collateralAddress` (*address*) - Collateral asset to configure
* `maxAllowable` (*uint128*) - New max deposit amount for the synth

#### getMarginCollateralConfiguration

  ```solidity
  function getMarginCollateralConfiguration() external view returns (struct IMarginModule.ConfiguredCollateral[])
  ```

  Returns the configured collaterals useable for margin.

**Returns**
* `[0]` (*struct IMarginModule.ConfiguredCollateral[]*) - getMarginCollateralConfiguration An array of `ConfiguredCollateral` structs representing configured collateral
#### getMarginDigest

  ```solidity
  function getMarginDigest(uint128 accountId, uint128 marketId) external view returns (struct Margin.MarginValues)
  ```

  Returns a digest of account margin USD values. See `Margin.MarginValues` for specifics.

**Parameters**
* `accountId` (*uint128*) - Account of margin to query against
* `marketId` (*uint128*) - Market of margin to query against

**Returns**
* `[0]` (*struct Margin.MarginValues*) - getMarginDigest A struct of relevant margin values in USD
#### getNetAssetValue

  ```solidity
  function getNetAssetValue(uint128 accountId, uint128 marketId, uint256 oraclePrice) external view returns (uint256)
  ```

  Returns the NAV of `account` and `marketId` given an optional `price`.

**Parameters**
* `accountId` (*uint128*) - Account of position to query against
* `marketId` (*uint128*) - Market of position to query against
* `oraclePrice` (*uint256*) - Market oracle price, uint256(0) will default to current price

**Returns**
* `[0]` (*uint256*) - getNetAssetValue The NAV of the current position in USD
#### getDiscountedCollateralPrice

  ```solidity
  function getDiscountedCollateralPrice(address collateralAddress, uint256 amount) external view returns (uint256)
  ```

  Returns the discount adjusted oracle price based on `amount` of collateral for `collateralAddress`. `amount` is
        necessary here as it simulates if `amount` were sold, what would be the impact on the skew, and
        hence the discount.

**Parameters**
* `collateralAddress` (*address*) - Address of collateral asset
* `amount` (*uint256*) - Amount of synth asset to sell

**Returns**
* `[0]` (*uint256*) - getDiscountedCollateralPrice Discounted collateral price in USD
#### getWithdrawableMargin

  ```solidity
  function getWithdrawableMargin(uint128 accountId, uint128 marketId) external view returns (uint256)
  ```

  Returns the withdrawable margin given the discounted margin for `accountId` accounting for any open
        position. Callers can invoke `getMarginDigest` to retrieve the available margin (i.e. discounted margin
        when there is a position open or marginUsd when there isn't).

**Parameters**
* `accountId` (*uint128*) - Account of the margin account to query against
* `marketId` (*uint128*) - Market of the margin account to query against

**Returns**
* `[0]` (*uint256*) - getWithdrawableMargin Amount of margin in USD that can be withdrawn
#### getMarginLiquidationOnlyReward

  ```solidity
  function getMarginLiquidationOnlyReward(uint128 accountId, uint128 marketId) external view returns (uint256)
  ```

  Returns the keeper reward for liquidating a position's margin

**Parameters**
* `accountId` (*uint128*) - Account of the margin to be liquidated
* `marketId` (*uint128*) - Market of the margin to be liquidated

**Returns**
* `[0]` (*uint256*) - getMarginLiquidationOnlyReward Amount of keeper rewards in USD

#### MarginDeposit

  ```solidity
  event MarginDeposit(address from, address to, uint256 value, address collateralAddress)
  ```

  Emitted when margin is deposited from user to market.

**Parameters**
* `from` (*address*) - Address of depositor
* `to` (*address*) - Address of recipient of deposit
* `value` (*uint256*) - Amount of assets deposited
* `collateralAddress` (*address*) - Address of collateral deposited

#### MarginWithdraw

  ```solidity
  event MarginWithdraw(address from, address to, uint256 value, address collateralAddress)
  ```

  Emitted when margin is withdrawn from market to user.

**Parameters**
* `from` (*address*) - Address of recipient of withdraw
* `to` (*address*) - Address where asset withdrawn from
* `value` (*uint256*) - Amount of assets withdrawn
* `collateralAddress` (*address*) - Address of withdrawn asset

#### MarginCollateralConfigured

  ```solidity
  event MarginCollateralConfigured(address from, uint256 collaterals)
  ```

  Emitted when collateral is configured.

**Parameters**
* `from` (*address*) - Address collateral configurer
* `collaterals` (*uint256*) - Number of collaterals configured

#### DebtPaid

  ```solidity
  event DebtPaid(uint128 accountId, uint128 marketId, uint128 oldDebt, uint128 newDebt, uint128 paidFromUsdCollateral)
  ```

  Emitted when debt is paid off.

**Parameters**
* `accountId` (*uint128*) - Account that had their debt paid
* `marketId` (*uint128*) - Market of account that had their debt paid
* `oldDebt` (*uint128*) - Debt in USD before debt payment
* `newDebt` (*uint128*) - Debt in USD after debt payment
* `paidFromUsdCollateral` (*uint128*) - Amount of debt paid directly from USD in margin

#### FundingRecomputed

  ```solidity
  event FundingRecomputed(uint128 marketId, int128 skew, int128 fundingRate, int128 fundingVelocity)
  ```

  Emitted when funding is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their funding recomputed
* `skew` (*int128*) - Current skew at the point of recomputation
* `fundingRate` (*int128*) - 
* `fundingVelocity` (*int128*) - Current instantaneous velocity at the point of recomputation

#### UtilizationRecomputed

  ```solidity
  event UtilizationRecomputed(uint128 marketId, int128 skew, uint128 utilizationRate)
  ```

  Emitted when utilization is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their utilization recomputed
* `skew` (*int128*) - Current market skew at the point of recomputation
* `utilizationRate` (*uint128*) - New utilization rate after recomputation

#### OrderCanceled

  ```solidity
  event OrderCanceled(uint128 accountId, uint128 marketId, uint256 keeperFee, uint64 commitmentTime)
  ```

  Emitted when an order is canceled.

**Parameters**
* `accountId` (*uint128*) - Account of order that was canceled
* `marketId` (*uint128*) - Market the order was canceled against
* `keeperFee` (*uint256*) - Fee paid to keeper for canceling order
* `commitmentTime` (*uint64*) - block.timestamp of order at the point of comment

#### MarketSizeUpdated

  ```solidity
  event MarketSizeUpdated(uint128 marketId, uint128 size, int128 skew)
  ```

  Emitted when the market's size is updated either due to orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Market that had their size updated
* `size` (*uint128*) - New market size post update
* `skew` (*int128*) - New market skew post update

### Market Configuration Module

#### setMarketConfiguration

  ```solidity
  function setMarketConfiguration(struct IMarketConfigurationModule.GlobalMarketConfigureParameters data) external
  ```

  Configures market parameters applied globally.

**Parameters**
* `data` (*struct IMarketConfigurationModule.GlobalMarketConfigureParameters*) - A struct of parameters to configure

#### setMarketConfigurationById

  ```solidity
  function setMarketConfigurationById(struct IMarketConfigurationModule.ConfigureByMarketParameters data) external
  ```

  Configures a market specific parameters applied to the `marketId`.

**Parameters**
* `data` (*struct IMarketConfigurationModule.ConfigureByMarketParameters*) - A struct of parameters to configure

#### setMinDelegationTime

  ```solidity
  function setMinDelegationTime(uint128 marketId, uint32 minDelegationTime) external
  ```

  Updates the minimum delegation time for a market.

**Parameters**
* `marketId` (*uint128*) - Market to update
* `minDelegationTime` (*uint32*) - Minimum delegation time in seconds

#### getMarketConfiguration

  ```solidity
  function getMarketConfiguration() external view returns (struct PerpMarketConfiguration.GlobalData)
  ```

  Returns configured global market parameters.

**Returns**
* `[0]` (*struct PerpMarketConfiguration.GlobalData*) - getMarketConfiguration A struct of configured parameters
#### getMarketConfigurationById

  ```solidity
  function getMarketConfigurationById(uint128 marketId) external view returns (struct PerpMarketConfiguration.Data)
  ```

  Returns configured market specific parameters.

**Parameters**
* `marketId` (*uint128*) - Market to query against

**Returns**
* `[0]` (*struct PerpMarketConfiguration.Data*) - getMarketConfigurationById A struct of configured parameters for marketId

#### GlobalMarketConfigured

  ```solidity
  event GlobalMarketConfigured(address from)
  ```

  Emitted when the global market config is updated.

**Parameters**
* `from` (*address*) - Address of configurer

#### MarketConfigured

  ```solidity
  event MarketConfigured(uint128 marketId, address from)
  ```

  Emitted when parameters for a specific market is updated.

**Parameters**
* `marketId` (*uint128*) - Market that configured
* `from` (*address*) - Address of configurer

#### FundingRecomputed

  ```solidity
  event FundingRecomputed(uint128 marketId, int128 skew, int128 fundingRate, int128 fundingVelocity)
  ```

  Emitted when funding is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their funding recomputed
* `skew` (*int128*) - Current skew at the point of recomputation
* `fundingRate` (*int128*) - 
* `fundingVelocity` (*int128*) - Current instantaneous velocity at the point of recomputation

#### UtilizationRecomputed

  ```solidity
  event UtilizationRecomputed(uint128 marketId, int128 skew, uint128 utilizationRate)
  ```

  Emitted when utilization is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their utilization recomputed
* `skew` (*int128*) - Current market skew at the point of recomputation
* `utilizationRate` (*uint128*) - New utilization rate after recomputation

#### OrderCanceled

  ```solidity
  event OrderCanceled(uint128 accountId, uint128 marketId, uint256 keeperFee, uint64 commitmentTime)
  ```

  Emitted when an order is canceled.

**Parameters**
* `accountId` (*uint128*) - Account of order that was canceled
* `marketId` (*uint128*) - Market the order was canceled against
* `keeperFee` (*uint256*) - Fee paid to keeper for canceling order
* `commitmentTime` (*uint64*) - block.timestamp of order at the point of comment

#### MarketSizeUpdated

  ```solidity
  event MarketSizeUpdated(uint128 marketId, uint128 size, int128 skew)
  ```

  Emitted when the market's size is updated either due to orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Market that had their size updated
* `size` (*uint128*) - New market size post update
* `skew` (*int128*) - New market skew post update

### Order Module

#### commitOrder

  ```solidity
  function commitOrder(uint128 accountId, uint128 marketId, int128 sizeDelta, uint256 limitPrice, uint128 keeperFeeBufferUsd, address[] hooks, bytes32 trackingCode) external
  ```

  Creates an order for `accountId` in `marketId` to be settled at a later time.

**Parameters**
* `accountId` (*uint128*) - Account to commit an order against
* `marketId` (*uint128*) - Market to commit an order against
* `sizeDelta` (*int128*) - Size to modify on position after settlement
* `limitPrice` (*uint256*) - The max acceptable price tolerance for settlement
* `keeperFeeBufferUsd` (*uint128*) - tip in USD to pay for settlement keepers
* `hooks` (*address[]*) - An array of settlement hook addresses for execution on settlement
* `trackingCode` (*bytes32*) - 

#### settleOrder

  ```solidity
  function settleOrder(uint128 accountId, uint128 marketId, bytes priceUpdateData) external payable
  ```

  Settles a previously committed order by `accountId` and `marketId`.

**Parameters**
* `accountId` (*uint128*) - Account of order to settle
* `marketId` (*uint128*) - Market of order to settle
* `priceUpdateData` (*bytes*) - An acceptable Pyth off-chain price blob

#### cancelOrder

  ```solidity
  function cancelOrder(uint128 accountId, uint128 marketId, bytes priceUpdateData) external payable
  ```

  Cancel a previously committed order by `accountId` and `marketId`. This can only be invoked after
        an order is ready and a keeper can prove price tolerance has been exceeded.

**Parameters**
* `accountId` (*uint128*) - Account of the order to cancel
* `marketId` (*uint128*) - Market of the order to cancel
* `priceUpdateData` (*bytes*) - An acceptable Pyth off-chain price blob

#### cancelStaleOrder

  ```solidity
  function cancelStaleOrder(uint128 accountId, uint128 marketId) external
  ```

  Cancels a previously committed order that has gone stale by `accountId` and `marketId`.
        This can only happen after an order is stale, and not settled or canceled by a keeper. This
        is a convenience method to clear stale orders without having to provide a Pyth price.

**Parameters**
* `accountId` (*uint128*) - Account of stale order to cancel
* `marketId` (*uint128*) - Market of stale order to cancel

#### getOrderDigest

  ```solidity
  function getOrderDigest(uint128 accountId, uint128 marketId) external view returns (struct IOrderModule.OrderDigest)
  ```

  Returns an order belonging to `accountId` in `marketId`.

**Parameters**
* `accountId` (*uint128*) - Account of order to fetch the digest against
* `marketId` (*uint128*) - Market of order to fetch the digest against

**Returns**
* `[0]` (*struct IOrderModule.OrderDigest*) - getOrderDigest A struct of the `OrderDigest`
#### getOrderFees

  ```solidity
  function getOrderFees(uint128 marketId, int128 sizeDelta, uint128 keeperFeeBufferUsd) external view returns (uint256 orderFee, uint256 keeperFee)
  ```

  Returns fees charged to open/close an order (along with a dynamic keeper fee).

  Order fees are charged a combination of marker/taker depending on the impact of the `sizeDelta`
     on skew. There is a scenario where if an order flips the skew, the proportion that reduces skew
     is charged with maker fees but the flipped side that expands skew is charged a taker fee.
Keeper fees are fees paid to the keeper to settle an order. The fee is based on gas but can roughly
     be translated to `orderSettlementGasUnits * block.basefee * ETH/USD + bufferUsd`. This fee is bounded
     by a configurable min/max.

**Parameters**
* `marketId` (*uint128*) - Market to query against
* `sizeDelta` (*int128*) - Size of impact on skew
* `keeperFeeBufferUsd` (*uint128*) - A tip in USD to pay for settlement keepers

**Returns**
* `orderFee` (*uint256*) - Estimated fees to be paid on settlement
* `keeperFee` (*uint256*) - Estimated fees to be paid to keeper on settlement
#### getFillPrice

  ```solidity
  function getFillPrice(uint128 marketId, int128 size) external view returns (uint256)
  ```

  Returns an oracle price adjusted by a premium/discount based on how the sizeDelta effects skew.

  The fill can be attributed or when an order is filled. The price is the oracle price + adjustment when
     which an order is settled. Intuitively, the adjustment is a discount if the size reduces the skew (i.e.
     skew is pulled closer to zero). However a premium is applied if skew expands (i.e. skew pushed away
     from zero). More can be read in SIP-279.

**Parameters**
* `marketId` (*uint128*) - Market to query against
* `size` (*int128*) - Size of impact on skew

**Returns**
* `[0]` (*uint256*) - getFillPrice Premium/discount adjusted price
#### getOraclePrice

  ```solidity
  function getOraclePrice(uint128 marketId) external view returns (uint256)
  ```

  Returns the oracle price given the `marketId`.

**Parameters**
* `marketId` (*uint128*) - Market to query against

**Returns**
* `[0]` (*uint256*) - getOraclePrice Raw oracle price

#### OrderCommitted

  ```solidity
  event OrderCommitted(uint128 accountId, uint128 marketId, uint64 commitmentTime, int128 sizeDelta, uint256 estimatedOrderFee, uint256 estimatedKeeperFee, bytes32 trackingCode)
  ```

  Emitted when an order is committed.

**Parameters**
* `accountId` (*uint128*) - Account the order belongs to
* `marketId` (*uint128*) - Market the order was committed against
* `commitmentTime` (*uint64*) - block.timestamp of commitment
* `sizeDelta` (*int128*) - Size to modify on the existing or new position after settlement
* `estimatedOrderFee` (*uint256*) - Projected fee paid to open order at the time of commitment
* `estimatedKeeperFee` (*uint256*) - Projected fee paid to keepers at the time of commitment
* `trackingCode` (*bytes32*) - 

#### OrderSettled

  ```solidity
  event OrderSettled(uint128 accountId, uint128 marketId, uint64 settlementTime, int128 sizeDelta, uint256 orderFee, uint256 keeperFee, int128 accruedFunding, uint128 accruedUtilization, int256 pnl, uint256 fillPrice, uint128 accountDebt)
  ```

  Emitted when a pending order was successfully settled.

**Parameters**
* `accountId` (*uint128*) - Account of the settled order
* `marketId` (*uint128*) - Market of the settled order
* `settlementTime` (*uint64*) - block.timestamp when order was settled
* `sizeDelta` (*int128*) - Size to modify, applied on the new or existing position
* `orderFee` (*uint256*) - Actual fee paid to settle order
* `keeperFee` (*uint256*) - Actual fee paid to keeper to settle order
* `accruedFunding` (*int128*) - Realized funding accrued on existing position before settlement
* `accruedUtilization` (*uint128*) - Realized utilization accrued on existing position before settlement
* `pnl` (*int256*) - Realized price PnL on existing position before settlement
* `fillPrice` (*uint256*) - 
* `accountDebt` (*uint128*) - Debt due to position realization after settlement

#### OrderSettlementHookExecuted

  ```solidity
  event OrderSettlementHookExecuted(uint128 accountId, uint128 marketId, address hook)
  ```

  Emitted after an order is settled with hook(s) and the hook was completely successfully.

**Parameters**
* `accountId` (*uint128*) - Account of order that was settled before hook was executed
* `marketId` (*uint128*) - Market of order that was settled before hook was executed
* `hook` (*address*) - Address of the executed settlement hook

#### FundingRecomputed

  ```solidity
  event FundingRecomputed(uint128 marketId, int128 skew, int128 fundingRate, int128 fundingVelocity)
  ```

  Emitted when funding is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their funding recomputed
* `skew` (*int128*) - Current skew at the point of recomputation
* `fundingRate` (*int128*) - 
* `fundingVelocity` (*int128*) - Current instantaneous velocity at the point of recomputation

#### UtilizationRecomputed

  ```solidity
  event UtilizationRecomputed(uint128 marketId, int128 skew, uint128 utilizationRate)
  ```

  Emitted when utilization is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their utilization recomputed
* `skew` (*int128*) - Current market skew at the point of recomputation
* `utilizationRate` (*uint128*) - New utilization rate after recomputation

#### OrderCanceled

  ```solidity
  event OrderCanceled(uint128 accountId, uint128 marketId, uint256 keeperFee, uint64 commitmentTime)
  ```

  Emitted when an order is canceled.

**Parameters**
* `accountId` (*uint128*) - Account of order that was canceled
* `marketId` (*uint128*) - Market the order was canceled against
* `keeperFee` (*uint256*) - Fee paid to keeper for canceling order
* `commitmentTime` (*uint64*) - block.timestamp of order at the point of comment

#### MarketSizeUpdated

  ```solidity
  event MarketSizeUpdated(uint128 marketId, uint128 size, int128 skew)
  ```

  Emitted when the market's size is updated either due to orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Market that had their size updated
* `size` (*uint128*) - New market size post update
* `skew` (*int128*) - New market skew post update

### Perp Account Module

#### getAccountDigest

  ```solidity
  function getAccountDigest(uint128 accountId, uint128 marketId) external view returns (struct IPerpAccountModule.AccountDigest)
  ```

  Returns a digest of the account including, but not limited to collateral, orders, positions etc.

**Parameters**
* `accountId` (*uint128*) - Account of digest to query against
* `marketId` (*uint128*) - Market of account digest to query against

**Returns**
* `[0]` (*struct IPerpAccountModule.AccountDigest*) - getAccountDigest A struct of `AccountDigest` with account details
#### getPositionDigest

  ```solidity
  function getPositionDigest(uint128 accountId, uint128 marketId) external view returns (struct IPerpAccountModule.PositionDigest)
  ```

  Returns a digest of an open position belonging to `accountId` in `marketId`.

**Parameters**
* `accountId` (*uint128*) - Account of position
* `marketId` (*uint128*) - Market position belongs to

**Returns**
* `[0]` (*struct IPerpAccountModule.PositionDigest*) - getPositionDigest A struct of `PositionDigest` with position details
#### mergeAccounts

  ```solidity
  function mergeAccounts(uint128 fromId, uint128 toId, uint128 marketId) external
  ```

  Merges two accounts, combining `fromId` into `toId` for `marketId`. Merging accounts will realize the
        position of account `toId` in addition to transferring collateral and size from one to the other. It's
        on the caller to burn the perp account NFT post merge.
        Additionally, this fn requires that account `fromId` must have just been settled, implying account
        merge operation can only be performed in the same block as settlement via multicalls on settlement or
        indirectly settlement hooks.

  Account permissions in the `fromId` account are _not_ be transferred and that we only allow
     merging accounts that use the same margin collateral as the market.

**Parameters**
* `fromId` (*uint128*) - Account to merge from
* `toId` (*uint128*) - Account to merge into
* `marketId` (*uint128*) - Market to perform the account merge

#### splitAccount

  ```solidity
  function splitAccount(uint128 fromId, uint128 toId, uint128 marketId, uint128 proportion) external
  ```

  Splits the from accounts size, collateral and debt based on the proportion provided.

  Account permissions in the `fromId` account will _not_ be transferred. This also requires the `toId` to
     be an empty account.

**Parameters**
* `fromId` (*uint128*) - Account to split from
* `toId` (*uint128*) - Account to split into
* `marketId` (*uint128*) - Market to perform the split account
* `proportion` (*uint128*) - Portion of `fromId` to split out, expressed as a decimal (e.g 0.5 = half)

#### AccountsMerged

  ```solidity
  event AccountsMerged(uint128 fromId, uint128 toId, uint128 marketId)
  ```

  Emitted when two accounts are merged.

**Parameters**
* `fromId` (*uint128*) - Account to merge from
* `toId` (*uint128*) - Account to merge into
* `marketId` (*uint128*) - Market to perform the account merge

#### AccountSplit

  ```solidity
  event AccountSplit(uint128 fromId, uint128 toId, uint128 marketId)
  ```

  Emitted when an account is split into a new one.

**Parameters**
* `fromId` (*uint128*) - Account to split from
* `toId` (*uint128*) - Account to split into
* `marketId` (*uint128*) - Market to perform the account split

### Perp Market Factory Module

#### setPyth

  ```solidity
  function setPyth(contract IPyth pyth) external
  ```

  Stores a reference to the Pyth EVM contract.

**Parameters**
* `pyth` (*contract IPyth*) - Address of Pyth verification contract

#### setEthOracleNodeId

  ```solidity
  function setEthOracleNodeId(bytes32 nodeId) external
  ```

  Stores a reference to the ETH/USD oracle node.

**Parameters**
* `nodeId` (*bytes32*) - Id of ETH/USD oracle node

#### setRewardDistributorImplementation

  ```solidity
  function setRewardDistributorImplementation(address implementation) external
  ```

  Stores the address of a base perp reward distributor contract.

**Parameters**
* `implementation` (*address*) - Address of reward distributor implementation

#### createMarket

  ```solidity
  function createMarket(struct IPerpMarketFactoryModule.CreatePerpMarketParameters data) external returns (uint128)
  ```

  Registers a new PerpMarket with Synthetix and initializes storage.

**Parameters**
* `data` (*struct IPerpMarketFactoryModule.CreatePerpMarketParameters*) - A struct of parameters to create a market with

**Returns**
* `[0]` (*uint128*) - createMarket Market id of newly created market
#### getMarketDigest

  ```solidity
  function getMarketDigest(uint128 marketId) external view returns (struct IPerpMarketFactoryModule.MarketDigest)
  ```

  Returns a digest of an existing market given the `marketId`.

**Parameters**
* `marketId` (*uint128*) - Market to query against

**Returns**
* `[0]` (*struct IPerpMarketFactoryModule.MarketDigest*) - getMarketDigest Market digest struct
#### getUtilizationDigest

  ```solidity
  function getUtilizationDigest(uint128 marketId) external view returns (struct IPerpMarketFactoryModule.UtilizationDigest)
  ```

  Returns a the utilization digest of an existing market given their `marketId`.

**Parameters**
* `marketId` (*uint128*) - Market to query the digest against

**Returns**
* `[0]` (*struct IPerpMarketFactoryModule.UtilizationDigest*) - getUtilizationDigest Utilization digest struct
#### getActiveMarketIds

  ```solidity
  function getActiveMarketIds() external view returns (uint128[])
  ```

  Returns all created market ids in the system.

**Returns**
* `[0]` (*uint128[]*) - getActiveMarketIds An array of market ids
#### recomputeUtilization

  ```solidity
  function recomputeUtilization(uint128 marketId) external
  ```

  Recomputes utilization rate for a given market

**Parameters**
* `marketId` (*uint128*) - Market to recompute against

#### recomputeFunding

  ```solidity
  function recomputeFunding(uint128 marketId) external
  ```

  Recomputes funding rate for a given market

**Parameters**
* `marketId` (*uint128*) - Market to recompute against

#### name

  ```solidity
  function name(uint128 marketId) external view returns (string)
  ```

  returns a human-readable name for a given market

#### reportedDebt

  ```solidity
  function reportedDebt(uint128 marketId) external view returns (uint256)
  ```

  returns amount of USD that the market would try to mint if everything was withdrawn

#### minimumCredit

  ```solidity
  function minimumCredit(uint128 marketId) external view returns (uint256)
  ```

  prevents reduction of available credit capacity by specifying this amount, for which withdrawals will be disallowed

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

#### MarketCreated

  ```solidity
  event MarketCreated(uint128 id, bytes32 name)
  ```

  Emitted when a market is created.

**Parameters**
* `id` (*uint128*) - Id of market
* `name` (*bytes32*) - Name of market

#### FundingRecomputed

  ```solidity
  event FundingRecomputed(uint128 marketId, int128 skew, int128 fundingRate, int128 fundingVelocity)
  ```

  Emitted when funding is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their funding recomputed
* `skew` (*int128*) - Current skew at the point of recomputation
* `fundingRate` (*int128*) - 
* `fundingVelocity` (*int128*) - Current instantaneous velocity at the point of recomputation

#### UtilizationRecomputed

  ```solidity
  event UtilizationRecomputed(uint128 marketId, int128 skew, uint128 utilizationRate)
  ```

  Emitted when utilization is computed.

**Parameters**
* `marketId` (*uint128*) - Market that had their utilization recomputed
* `skew` (*int128*) - Current market skew at the point of recomputation
* `utilizationRate` (*uint128*) - New utilization rate after recomputation

#### OrderCanceled

  ```solidity
  event OrderCanceled(uint128 accountId, uint128 marketId, uint256 keeperFee, uint64 commitmentTime)
  ```

  Emitted when an order is canceled.

**Parameters**
* `accountId` (*uint128*) - Account of order that was canceled
* `marketId` (*uint128*) - Market the order was canceled against
* `keeperFee` (*uint256*) - Fee paid to keeper for canceling order
* `commitmentTime` (*uint64*) - block.timestamp of order at the point of comment

#### MarketSizeUpdated

  ```solidity
  event MarketSizeUpdated(uint128 marketId, uint128 size, int128 skew)
  ```

  Emitted when the market's size is updated either due to orders or liquidations.

**Parameters**
* `marketId` (*uint128*) - Market that had their size updated
* `size` (*uint128*) - New market size post update
* `skew` (*int128*) - New market skew post update

### IPerpRewardDistributor

#### getPoolId

  ```solidity
  function getPoolId() external view returns (uint128)
  ```

  Returns the id of the pool this was registered with.

**Returns**
* `[0]` (*uint128*) - getPoolId Id of the pool this RD was registered with
#### getPoolCollateralTypes

  ```solidity
  function getPoolCollateralTypes() external view returns (address[])
  ```

  Returns a list of pool collateral types this distributor was registered with.

**Returns**
* `[0]` (*address[]*) - getPoolCollateralTypes An array of delegated pool collateral addresses to distribute to
#### initialize

  ```solidity
  function initialize(address rewardManager, address perpMarket, uint128 poolId_, address[] collateralTypes, address payoutToken_, string name_) external
  ```

  Initializes the PerpRewardDistributor with references, name, token to distribute etc.

**Parameters**
* `rewardManager` (*address*) - Address of the reward manager (i.e. Synthetix core proxy)
* `perpMarket` (*address*) - Address of the bfp market proxy
* `poolId_` (*uint128*) - Id of the pool this RD was registered with
* `collateralTypes` (*address[]*) - An array of delegated pool collateral types to dstribute to
* `payoutToken_` (*address*) - Reward token to distribute
* `name_` (*string*) - Name of the reward distributor

#### setShouldFailPayout

  ```solidity
  function setShouldFailPayout(bool _shouldFailedPayout) external
  ```

  Set true to disable `payout` to revert on claim or false to allow. Only callable by pool owner.

**Parameters**
* `_shouldFailedPayout` (*bool*) - True to fail subsequent payout calls, false otherwise

#### distributeRewards

  ```solidity
  function distributeRewards(address collateralType, uint256 amount) external
  ```

  Creates a new distribution entry for LPs of `collateralType` to `amount` of tokens.

**Parameters**
* `collateralType` (*address*) - Delegated collateral in pool to distribute rewards to
* `amount` (*uint256*) - Amount of reward tokens to distribute

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Returns a human-readable name for the reward distributor

#### payout

  ```solidity
  function payout(uint128 accountId, uint128 poolId, address collateralType, address sender, uint256 amount) external returns (bool)
  ```

  This function should revert if ERC2771Context._msgSender() is not the Synthetix CoreProxy address.

**Returns**
* `[0]` (*bool*) - whether or not the payout was executed
#### onPositionUpdated

  ```solidity
  function onPositionUpdated(uint128 accountId, uint128 poolId, address collateralType, uint256 newShares) external
  ```

  This function is called by the Synthetix Core Proxy whenever
a position is updated on a pool which this distributor is registered

#### token

  ```solidity
  function token() external view returns (address)
  ```

  Address to ERC-20 token distributed by this distributor, for display purposes only

  Return address(0) if providing non ERC-20 rewards

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### Perp Reward Distributor Factory Module

#### createRewardDistributor

  ```solidity
  function createRewardDistributor(struct IPerpRewardDistributorFactoryModule.CreatePerpRewardDistributorParameters data) external returns (address)
  ```

  Create a new RewardDistributor with Synthetix and initializes storage.

  The pool owner must then make a subsequent `.registerRewardDistributor` invocation against `collateralTypes`
     specified in `PerpRewardDistributor.initialize`.

**Parameters**
* `data` (*struct IPerpRewardDistributorFactoryModule.CreatePerpRewardDistributorParameters*) - A struct of parameters to create a reward distributor with

**Returns**
* `[0]` (*address*) - createRewardDistributor Address of the newly created reward distributor

#### RewardDistributorCreated

  ```solidity
  event RewardDistributorCreated(address distributor)
  ```

  Emitted when a distributor is created.

**Parameters**
* `distributor` (*address*) - Address of the reward distributor

### Settlement Hook Module

#### setSettlementHookConfiguration

  ```solidity
  function setSettlementHookConfiguration(struct ISettlementHookModule.SettlementHookConfigureParameters data) external
  ```

  Configures settlement hook parameters applied globally.

**Parameters**
* `data` (*struct ISettlementHookModule.SettlementHookConfigureParameters*) - A struct of parameters to configure with

#### getSettlementHookConfiguration

  ```solidity
  function getSettlementHookConfiguration() external view returns (struct ISettlementHookModule.SettlementHookConfigureParameters)
  ```

  Returns configured global settlement hook parameters.

**Returns**
* `[0]` (*struct ISettlementHookModule.SettlementHookConfigureParameters*) - getSettlementHookConfiguration A struct of `SettlementHookConfigureParameters` used for configuration
#### isSettlementHookWhitelisted

  ```solidity
  function isSettlementHookWhitelisted(address hook) external view returns (bool)
  ```

  Returns whether the specified hook is whitelisted.

**Parameters**
* `hook` (*address*) - Address of hook to assert

**Returns**
* `[0]` (*bool*) - isSettlementHookWhitelisted True if whitelisted, false otherwise

#### SettlementHookConfigured

  ```solidity
  event SettlementHookConfigured(address from, uint256 hooks)
  ```

  Emitted when hooks are configured.

**Parameters**
* `from` (*address*) - Address of hook configurer
* `hooks` (*uint256*) - Number of hooks configured

### Split Account Configuration Module

#### setEndorsedSplitAccounts

  ```solidity
  function setEndorsedSplitAccounts(address[] addresses) external
  ```

  Configures a list of addresses to be whitelisted for splitAccount.

**Parameters**
* `addresses` (*address[]*) - An array of addresses to whitelist

#### getEndorsedSplitAccounts

  ```solidity
  function getEndorsedSplitAccounts() external view returns (address[] addresses)
  ```

  Returns addresses allowed to split account.

**Returns**
* `addresses` (*address[]*) - list of addresses
#### isEndorsedForSplitAccount

  ```solidity
  function isEndorsedForSplitAccount(address addr) external view returns (bool)
  ```

  Returns whether the specified hook is whitelisted.

**Parameters**
* `addr` (*address*) - Address of hook to assert

**Returns**
* `[0]` (*bool*) - isEndoresedForSplitAccount True if whitelisted, false otherwise

#### SplitAccountConfigured

  ```solidity
  event SplitAccountConfigured(address from, uint256 hooks)
  ```

  Emitted when split account whitelist is configured.

**Parameters**
* `from` (*address*) - Address of configurer
* `hooks` (*uint256*) - Number of addresses configured

### ISettlementHook

#### onSettle

  ```solidity
  function onSettle(uint128 accountId, uint128 marketId, uint256 oraclePrice) external
  ```

  Invoked as the callback post order settlement.

  Implementers should verify the calling `msg.sender` is Synthetix BFP Market Proxy and
     be highly recommended that it should also be idempotent.

**Parameters**
* `accountId` (*uint128*) - Account of order that was just settled
* `marketId` (*uint128*) - Market the order was just settled on
* `oraclePrice` (*uint256*) - Pyth price used for settlement (note: not the entry fill price)

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

## Governance

### Council Token Module

#### isInitialized

  ```solidity
  function isInitialized() external view returns (bool)
  ```

  Returns whether the token has been initialized.

**Returns**
* `[0]` (*bool*) - A boolean with the result of the query.
#### initialize

  ```solidity
  function initialize(string tokenName, string tokenSymbol, string uri) external
  ```

  Initializes the token with name, symbol, and uri.

#### mint

  ```solidity
  function mint(address to, uint256 tokenId) external
  ```

  Allows the owner to mint tokens.

**Parameters**
* `to` (*address*) - The address to receive the newly minted tokens.
* `tokenId` (*uint256*) - The ID of the newly minted token

#### safeMint

  ```solidity
  function safeMint(address to, uint256 tokenId, bytes data) external
  ```

  Allows the owner to mint tokens. Verifies that the receiver can receive the token

**Parameters**
* `to` (*address*) - The address to receive the newly minted token.
* `tokenId` (*uint256*) - The ID of the newly minted token
* `data` (*bytes*) - any data which should be sent to the receiver

#### burn

  ```solidity
  function burn(uint256 tokenId) external
  ```

  Allows the owner to burn tokens.

**Parameters**
* `tokenId` (*uint256*) - The token to burn

#### setAllowance

  ```solidity
  function setAllowance(uint256 tokenId, address spender) external
  ```

  Allows an address that holds tokens to provide allowance to another.

**Parameters**
* `tokenId` (*uint256*) - The token which should be allowed to spender
* `spender` (*address*) - The address that is given allowance.

#### setBaseTokenURI

  ```solidity
  function setBaseTokenURI(string uri) external
  ```

  Allows the owner to update the base token URI.

**Parameters**
* `uri` (*string*) - The new base token uri

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the total amount of tokens stored by the contract.

#### tokenOfOwnerByIndex

  ```solidity
  function tokenOfOwnerByIndex(address owner, uint256 index) external view returns (uint256)
  ```

  Returns a token ID owned by `owner` at a given `index` of its token list.
Use along with {balanceOf} to enumerate all of ``owner``'s tokens.

Requirements:
- `owner` must be a valid address
- `index` must be less than the balance of the tokens for the owner

#### tokenByIndex

  ```solidity
  function tokenByIndex(uint256 index) external view returns (uint256)
  ```

  Returns a token ID at a given `index` of all the tokens stored by the contract.
Use along with {totalSupply} to enumerate all tokens.

Requirements:
- `index` must be less than the total supply of the tokens

#### balanceOf

  ```solidity
  function balanceOf(address holder) external view returns (uint256 balance)
  ```

  Returns the number of tokens in ``owner``'s account.

Requirements:

- `holder` must be a valid address

#### ownerOf

  ```solidity
  function ownerOf(uint256 tokenId) external view returns (address owner)
  ```

  Returns the owner of the `tokenId` token.

Requirements:

- `tokenId` must exist.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId, bytes data) external
  ```

  Safely transfers `tokenId` token from `from` to `to`.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### safeTransferFrom

  ```solidity
  function safeTransferFrom(address from, address to, uint256 tokenId) external
  ```

  Safely transfers `tokenId` token from `from` to `to`, checking first that contract recipients
are aware of the ERC721 protocol to prevent tokens from being forever locked.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must exist and be owned by `from`.
- If the caller is not `from`, it must have been allowed to move this token by either {approve} or {setApprovalForAll}.
- If `to` refers to a smart contract, it must implement {IERC721Receiver-onERC721Received}, which is called upon a safe transfer.

Emits a {Transfer} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 tokenId) external
  ```

  Transfers `tokenId` token from `from` to `to`.

WARNING: Usage of this method is discouraged, use {safeTransferFrom} whenever possible.

Requirements:

- `from` cannot be the zero address.
- `to` cannot be the zero address.
- `tokenId` token must be owned by `from`.
- If the caller is not `from`, it must be approved to move this token by either {approve} or {setApprovalForAll}.

Emits a {Transfer} event.

#### approve

  ```solidity
  function approve(address to, uint256 tokenId) external
  ```

  Gives permission to `to` to transfer `tokenId` token to another account.
The approval is cleared when the token is transferred.

Only a single account can be approved at a time, so approving the zero address clears previous approvals.

Requirements:

- The caller must own the token or be an approved operator.
- `tokenId` must exist.

Emits an {Approval} event.

#### setApprovalForAll

  ```solidity
  function setApprovalForAll(address operator, bool approved) external
  ```

  Approve or remove `operator` as an operator for the caller.
Operators can call {transferFrom} or {safeTransferFrom} for any token owned by the caller.

Requirements:

- The `operator` cannot be the caller.

Emits an {ApprovalForAll} event.

#### getApproved

  ```solidity
  function getApproved(uint256 tokenId) external view returns (address operator)
  ```

  Returns the account approved for `tokenId` token.

Requirements:

- `tokenId` must exist.

#### isApprovedForAll

  ```solidity
  function isApprovedForAll(address owner, address operator) external view returns (bool)
  ```

  Returns if the `operator` is allowed to manage all of the assets of `owner`.

See {setApprovalForAll}

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 tokenId)
  ```

  Emitted when `tokenId` token is transferred from `from` to `to`.

#### Approval

  ```solidity
  event Approval(address owner, address approved, uint256 tokenId)
  ```

  Emitted when `owner` enables `approved` to manage the `tokenId` token.

#### ApprovalForAll

  ```solidity
  event ApprovalForAll(address owner, address operator, bool approved)
  ```

  Emitted when `owner` enables or disables (`approved`) `operator` to manage all of its assets.

### IDebtShare

#### balanceOfOnPeriod

  ```solidity
  function balanceOfOnPeriod(address account, uint256 periodId) external view returns (uint256)
  ```

### Election Inspector Module

#### getEpochStartDateForIndex

  ```solidity
  function getEpochStartDateForIndex(uint256 epochIndex) external view returns (uint64)
  ```

  Returns the date in which the given epoch started

#### getEpochEndDateForIndex

  ```solidity
  function getEpochEndDateForIndex(uint256 epochIndex) external view returns (uint64)
  ```

  Returns the date in which the given epoch ended

#### getNominationPeriodStartDateForIndex

  ```solidity
  function getNominationPeriodStartDateForIndex(uint256 epochIndex) external view returns (uint64)
  ```

  Returns the date in which the Nomination period in the given epoch started

#### getVotingPeriodStartDateForIndex

  ```solidity
  function getVotingPeriodStartDateForIndex(uint256 epochIndex) external view returns (uint64)
  ```

  Returns the date in which the Voting period in the given epoch started

#### wasNominated

  ```solidity
  function wasNominated(address candidate, uint256 epochIndex) external view returns (bool)
  ```

  Shows if a candidate was nominated in the given epoch

#### getNomineesAtEpoch

  ```solidity
  function getNomineesAtEpoch(uint256 epochIndex) external view returns (address[])
  ```

  Returns a list of all nominated candidates in the given epoch

#### hasVotedInEpoch

  ```solidity
  function hasVotedInEpoch(address user, uint256 chainId, uint256 epochIndex) external view returns (bool)
  ```

  Returns if user has voted in the given election

#### getCandidateVotesInEpoch

  ```solidity
  function getCandidateVotesInEpoch(address candidate, uint256 epochIndex) external view returns (uint256)
  ```

#### getElectionWinnersInEpoch

  ```solidity
  function getElectionWinnersInEpoch(uint256 epochIndex) external view returns (address[])
  ```

  Returns the winners of the given election

### Election Module

#### initOrUpdateElectionSettings

  ```solidity
  function initOrUpdateElectionSettings(address[] initialCouncil, contract IWormhole wormholeCore, contract IWormholeRelayer wormholeRelayer, uint8 minimumActiveMembers, uint64 initialNominationPeriodStartDate, uint64 administrationPeriodDuration, uint64 nominationPeriodDuration, uint64 votingPeriodDuration) external
  ```

  Initialises the module and immediately starts the first epoch

**Parameters**
* `initialCouncil` (*address[]*) - addresses that will hold the initial council seats; Length cannot be greater than type(uint8).max or equal to 0
* `wormholeCore` (*contract IWormhole*) - wormhole contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#core-contracts
* `wormholeRelayer` (*contract IWormholeRelayer*) - wormhole relayer contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#standard-relayer
* `minimumActiveMembers` (*uint8*) - minimum number of active council members required, cannot be greater than initialCouncil length or equal to 0
* `initialNominationPeriodStartDate` (*uint64*) - start date for the first nomination period
* `administrationPeriodDuration` (*uint64*) - duration of the administration period, in days
* `nominationPeriodDuration` (*uint64*) - duration of the nomination period, in days
* `votingPeriodDuration` (*uint64*) - duration of the voting period, in days

#### tweakEpochSchedule

  ```solidity
  function tweakEpochSchedule(uint64 newNominationPeriodStartDate, uint64 newVotingPeriodStartDate, uint64 newEpochEndDate) external payable
  ```

  Adjusts the current epoch schedule requiring that the current period remains Administration

  This function takes timestamps as parameters for the new start dates for the new periods; can only be called during the Administration period

**Parameters**
* `newNominationPeriodStartDate` (*uint64*) - new start date for the nomination period
* `newVotingPeriodStartDate` (*uint64*) - new start date for the voting period
* `newEpochEndDate` (*uint64*) - new end date for the epoch

#### setNextElectionSettings

  ```solidity
  function setNextElectionSettings(uint8 epochSeatCount, uint8 minimumActiveMembers, uint64 epochDuration, uint64 nominationPeriodDuration, uint64 votingPeriodDuration, uint64 maxDateAdjustmentTolerance) external
  ```

  Adjust settings that will be used on next epoch

  can only be called during the Administration period

**Parameters**
* `epochSeatCount` (*uint8*) - number of council seats to be elected in the next epoch
* `minimumActiveMembers` (*uint8*) - minimum number of active council members required
* `epochDuration` (*uint64*) - duration of the epoch in days
* `nominationPeriodDuration` (*uint64*) - duration of the nomination period in days
* `votingPeriodDuration` (*uint64*) - duration of the voting period in days
* `maxDateAdjustmentTolerance` (*uint64*) - maximum allowed difference between the new epoch dates and the current epoch dates in days

#### dismissMembers

  ```solidity
  function dismissMembers(address[] members) external payable
  ```

  Allows the owner to remove one or more council members, triggering an election if a threshold is met

**Parameters**
* `members` (*address[]*) - list of council members to be removed

#### nominate

  ```solidity
  function nominate() external
  ```

  Allows anyone to self-nominate during the Nomination period

#### withdrawNomination

  ```solidity
  function withdrawNomination() external
  ```

  Self-withdrawal of nominations during the Nomination period

#### _recvCast

  ```solidity
  function _recvCast(uint256 epochIndex, address voter, uint256 votingPower, uint256 chainId, address[] candidates, uint256[] amounts) external
  ```

  Internal voting logic, receiving end of voting via Wormhole

#### _recvWithdrawVote

  ```solidity
  function _recvWithdrawVote(uint256 epochIndex, address voter, uint256 chainId) external
  ```

  Internal voting withdrawl logic, receiving end of withdrawing vote via Wormhole

#### evaluate

  ```solidity
  function evaluate(uint256 numBallots) external payable
  ```

  Processes ballots in batches during the Evaluation period (after epochEndDate)

  ElectionTally needs to be extended to specify how votes are counted
Should be called after all crosschain votes propogate; if called immediately when the evaluation period starts some votes have the chance of being lost

#### resolve

  ```solidity
  function resolve() external payable
  ```

  Shuffles NFTs and resolves an election after it has been evaluated

  Burns previous NFTs and mints new ones

#### isNominated

  ```solidity
  function isNominated(address candidate) external view returns (bool)
  ```

  Shows if a candidate has been nominated in the current epoch

#### getNominees

  ```solidity
  function getNominees() external view returns (address[])
  ```

  Returns a list of all nominated candidates in the current epoch

#### hasVoted

  ```solidity
  function hasVoted(address user, uint256 chainId) external view returns (bool)
  ```

  Returns if user has voted in the current election

#### getVotePower

  ```solidity
  function getVotePower(address user, uint256 chainId, uint256 electionId) external view returns (uint256)
  ```

  Returns the vote power of user in the current election

#### getBallotCandidates

  ```solidity
  function getBallotCandidates(address voter, uint256 chainId, uint256 electionId) external view returns (address[])
  ```

  Returns the list of candidates that a particular ballot has

#### isElectionEvaluated

  ```solidity
  function isElectionEvaluated() external view returns (bool)
  ```

  Returns whether all ballots in the current election have been counted

#### getBallot

  ```solidity
  function getBallot(address voter, uint256 chainId, uint256 electionId) external pure returns (struct Ballot.Data)
  ```

  Returns the number of ballots in the current election

#### getNumOfBallots

  ```solidity
  function getNumOfBallots() external view returns (uint256)
  ```

  Returns the number of ballots in the current election

#### getCandidateVotes

  ```solidity
  function getCandidateVotes(address candidate) external view returns (uint256)
  ```

  Returns the number of votes a candidate received. Requires the election to be partially or totally evaluated

#### getElectionWinners

  ```solidity
  function getElectionWinners() external view returns (address[])
  ```

  Returns the winners of the current election. Requires the election to be partially or totally evaluated

#### getCouncilToken

  ```solidity
  function getCouncilToken() external view returns (address)
  ```

  Returns the address of the council NFT token

#### getCouncilMembers

  ```solidity
  function getCouncilMembers() external view returns (address[])
  ```

  Returns the current NFT token holders

#### initElectionModuleSatellite

  ```solidity
  function initElectionModuleSatellite(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, contract IWormhole wormholeCore, contract IWormholeRelayer wormholeRelayer, address[] councilMembers) external
  ```

  Initialize the election module with the given council members and epoch schedule

  Utility method for initializing a new Satellite chain; can only be called once

**Parameters**
* `epochIndex` (*uint256*) - the index of the epoch
* `epochStartDate` (*uint64*) - the start date of the epoch (timestamp)
* `nominationPeriodStartDate` (*uint64*) - the start date of the nomination period (timestamp)
* `votingPeriodStartDate` (*uint64*) - the start date of the voting period (timestamp)
* `epochEndDate` (*uint64*) - the end date of the epoch (timestamp)
* `wormholeCore` (*contract IWormhole*) - wormhole contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#core-contracts
* `wormholeRelayer` (*contract IWormholeRelayer*) - wormhole relayer contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#standard-relayer
* `councilMembers` (*address[]*) - the initial council members

#### isElectionModuleInitialized

  ```solidity
  function isElectionModuleInitialized() external view returns (bool)
  ```

  Shows whether the module has been initialized

#### cast

  ```solidity
  function cast(address[] candidates, uint256[] amounts) external payable
  ```

  Allows anyone with vote power to vote on nominated candidates during the Voting period

  caller must use all of their voting power in one go i.e. no partial votes; casts from satellite get broadcast to mothership chain

**Parameters**
* `candidates` (*address[]*) - the candidates to vote for
* `amounts` (*uint256[]*) - the amount of votes for each candidate

#### withdrawVote

  ```solidity
  function withdrawVote() external payable
  ```

  Allows to withdraw a casted vote on the current network

#### getCurrentPeriod

  ```solidity
  function getCurrentPeriod() external view returns (uint256)
  ```

  Returns the current period type: Administration, Nomination, Voting, Evaluation

#### getEpochSchedule

  ```solidity
  function getEpochSchedule() external view returns (struct Epoch.Data epoch)
  ```

  Shows the current epoch schedule dates

#### getElectionSettings

  ```solidity
  function getElectionSettings() external view returns (struct ElectionSettings.Data settings)
  ```

  Shows the settings for the current election

#### getNextElectionSettings

  ```solidity
  function getNextElectionSettings() external view returns (struct ElectionSettings.Data settings)
  ```

  Shows the settings for the next election

#### getEpochIndex

  ```solidity
  function getEpochIndex() external view returns (uint256)
  ```

  Returns the index of the current epoch. The first epoch's index is 1

#### _recvDismissMembers

  ```solidity
  function _recvDismissMembers(address[] membersToDismiss, uint256 epochIndex) external
  ```

  Burn the council tokens from the given members; receiving end of members dismissal via Wormhole

#### _recvTweakEpochSchedule

  ```solidity
  function _recvTweakEpochSchedule(uint256 epochIndex, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate) external
  ```

  Tweak the epoch dates to the given ones, without validation because we assume that it was started from mothership

#### _recvResolve

  ```solidity
  function _recvResolve(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address[] councilMembers) external
  ```

  Burn current epoch council tokens and assign new ones, setup epoch dates. Receiving end of epoch resolution via Wormhole.

#### ElectionModuleInitialized

  ```solidity
  event ElectionModuleInitialized()
  ```

#### EpochStarted

  ```solidity
  event EpochStarted(uint256 epochId)
  ```

#### EpochScheduleUpdated

  ```solidity
  event EpochScheduleUpdated(uint64 epochId, uint64 startDate, uint64 endDate)
  ```

#### EmergencyElectionStarted

  ```solidity
  event EmergencyElectionStarted(uint256 epochId)
  ```

#### CandidateNominated

  ```solidity
  event CandidateNominated(address candidate, uint256 epochId)
  ```

#### NominationWithdrawn

  ```solidity
  event NominationWithdrawn(address candidate, uint256 epochId)
  ```

#### VoteRecorded

  ```solidity
  event VoteRecorded(address voter, uint256 chainId, uint256 epochId, uint256 votingPower, address[] candidates)
  ```

#### VoteWithdrawn

  ```solidity
  event VoteWithdrawn(address voter, uint256 chainId, uint256 epochId)
  ```

#### ElectionBatchEvaluated

  ```solidity
  event ElectionBatchEvaluated(uint256 epochId, uint256 numEvaluatedBallots, uint256 totalBallots)
  ```

#### ElectionEvaluated

  ```solidity
  event ElectionEvaluated(uint256 epochId, uint256 ballotCount)
  ```

#### CouncilMembersDismissed

  ```solidity
  event CouncilMembersDismissed(address[] dismissedMembers, uint256 epochId)
  ```

#### InitializedSatellite

  ```solidity
  event InitializedSatellite(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address[] councilMembers)
  ```

#### EpochSetup

  ```solidity
  event EpochSetup(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate)
  ```

#### EpochScheduleTweaked

  ```solidity
  event EpochScheduleTweaked(uint256 epochIndex, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate)
  ```

#### VoteCastSent

  ```solidity
  event VoteCastSent(address sender, address[] candidates, uint256[] amounts)
  ```

#### VoteWithdrawnSent

  ```solidity
  event VoteWithdrawnSent(address sender)
  ```

### IElectionModuleSatellite

#### initElectionModuleSatellite

  ```solidity
  function initElectionModuleSatellite(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, contract IWormhole wormholeCore, contract IWormholeRelayer wormholeRelayer, address[] councilMembers) external
  ```

  Initialize the election module with the given council members and epoch schedule

  Utility method for initializing a new Satellite chain; can only be called once

**Parameters**
* `epochIndex` (*uint256*) - the index of the epoch
* `epochStartDate` (*uint64*) - the start date of the epoch (timestamp)
* `nominationPeriodStartDate` (*uint64*) - the start date of the nomination period (timestamp)
* `votingPeriodStartDate` (*uint64*) - the start date of the voting period (timestamp)
* `epochEndDate` (*uint64*) - the end date of the epoch (timestamp)
* `wormholeCore` (*contract IWormhole*) - wormhole contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#core-contracts
* `wormholeRelayer` (*contract IWormholeRelayer*) - wormhole relayer contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#standard-relayer
* `councilMembers` (*address[]*) - the initial council members

#### isElectionModuleInitialized

  ```solidity
  function isElectionModuleInitialized() external view returns (bool)
  ```

  Shows whether the module has been initialized

#### cast

  ```solidity
  function cast(address[] candidates, uint256[] amounts) external payable
  ```

  Allows anyone with vote power to vote on nominated candidates during the Voting period

  caller must use all of their voting power in one go i.e. no partial votes; casts from satellite get broadcast to mothership chain

**Parameters**
* `candidates` (*address[]*) - the candidates to vote for
* `amounts` (*uint256[]*) - the amount of votes for each candidate

#### withdrawVote

  ```solidity
  function withdrawVote() external payable
  ```

  Allows to withdraw a casted vote on the current network

#### getCurrentPeriod

  ```solidity
  function getCurrentPeriod() external view returns (uint256)
  ```

  Returns the current period type: Administration, Nomination, Voting, Evaluation

#### getEpochSchedule

  ```solidity
  function getEpochSchedule() external view returns (struct Epoch.Data epoch)
  ```

  Shows the current epoch schedule dates

#### getElectionSettings

  ```solidity
  function getElectionSettings() external view returns (struct ElectionSettings.Data settings)
  ```

  Shows the settings for the current election

#### getNextElectionSettings

  ```solidity
  function getNextElectionSettings() external view returns (struct ElectionSettings.Data settings)
  ```

  Shows the settings for the next election

#### getEpochIndex

  ```solidity
  function getEpochIndex() external view returns (uint256)
  ```

  Returns the index of the current epoch. The first epoch's index is 1

#### _recvDismissMembers

  ```solidity
  function _recvDismissMembers(address[] membersToDismiss, uint256 epochIndex) external
  ```

  Burn the council tokens from the given members; receiving end of members dismissal via Wormhole

#### _recvTweakEpochSchedule

  ```solidity
  function _recvTweakEpochSchedule(uint256 epochIndex, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate) external
  ```

  Tweak the epoch dates to the given ones, without validation because we assume that it was started from mothership

#### _recvResolve

  ```solidity
  function _recvResolve(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address[] councilMembers) external
  ```

  Burn current epoch council tokens and assign new ones, setup epoch dates. Receiving end of epoch resolution via Wormhole.

#### CouncilMembersDismissed

  ```solidity
  event CouncilMembersDismissed(address[] dismissedMembers, uint256 epochId)
  ```

#### InitializedSatellite

  ```solidity
  event InitializedSatellite(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address[] councilMembers)
  ```

#### EpochSetup

  ```solidity
  event EpochSetup(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate)
  ```

#### EpochScheduleTweaked

  ```solidity
  event EpochScheduleTweaked(uint256 epochIndex, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate)
  ```

#### VoteCastSent

  ```solidity
  event VoteCastSent(address sender, address[] candidates, uint256[] amounts)
  ```

#### VoteWithdrawnSent

  ```solidity
  event VoteWithdrawnSent(address sender)
  ```

### Snapshot Vote Power Module

#### setSnapshotContract

  ```solidity
  function setSnapshotContract(address snapshotContract, enum SnapshotVotePower.WeightType weight, uint256 scale, bool enabled) external
  ```

#### takeVotePowerSnapshot

  ```solidity
  function takeVotePowerSnapshot(address snapshotContract) external returns (uint128 snapshotId)
  ```

#### prepareBallotWithSnapshot

  ```solidity
  function prepareBallotWithSnapshot(address snapshotContract, address voter) external returns (uint256 votingPower)
  ```

#### getPreparedBallot

  ```solidity
  function getPreparedBallot(address voter) external view returns (uint256 power)
  ```

#### getVotingPowerForUser

  ```solidity
  function getVotingPowerForUser(address snapshotContract, address voter, uint256 periodId) external view returns (uint256)
  ```

### Synthetix Election Module

#### initOrUpgradeElectionModule

  ```solidity
  function initOrUpgradeElectionModule(address[] firstCouncil, uint8 minimumActiveMembers, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address debtShareContract) external
  ```

  Initializes the module and immediately starts the first epoch

#### setDebtShareContract

  ```solidity
  function setDebtShareContract(address newDebtShareContractAddress) external
  ```

  Sets the Synthetix v2 DebtShare contract that determines vote power

#### getDebtShareContract

  ```solidity
  function getDebtShareContract() external view returns (address)
  ```

  Returns the Synthetix v2 DebtShare contract that determines vote power

#### setDebtShareSnapshotId

  ```solidity
  function setDebtShareSnapshotId(uint256 snapshotId) external
  ```

  Sets the Synthetix v2 DebtShare snapshot that determines vote power for this epoch

#### getDebtShareSnapshotId

  ```solidity
  function getDebtShareSnapshotId() external view returns (uint256)
  ```

  Returns the Synthetix v2 DebtShare snapshot id set for this epoch

#### getDebtShare

  ```solidity
  function getDebtShare(address user) external view returns (uint256)
  ```

  Returns the Synthetix v2 debt share for the provided address, at this epoch's snapshot

#### setCrossChainDebtShareMerkleRoot

  ```solidity
  function setCrossChainDebtShareMerkleRoot(bytes32 merkleRoot, uint256 blocknumber) external
  ```

  Allows the system owner to declare a merkle root for user debt shares on other chains for this epoch

#### getCrossChainDebtShareMerkleRoot

  ```solidity
  function getCrossChainDebtShareMerkleRoot() external view returns (bytes32)
  ```

  Returns the current epoch's merkle root for user debt shares on other chains

#### getCrossChainDebtShareMerkleRootBlockNumber

  ```solidity
  function getCrossChainDebtShareMerkleRootBlockNumber() external view returns (uint256)
  ```

  Returns the current epoch's merkle root block number

#### declareCrossChainDebtShare

  ```solidity
  function declareCrossChainDebtShare(address account, uint256 debtShare, bytes32[] merkleProof) external
  ```

  Allows users to declare their Synthetix v2 debt shares on other chains

#### getDeclaredCrossChainDebtShare

  ```solidity
  function getDeclaredCrossChainDebtShare(address account) external view returns (uint256)
  ```

  Returns the Synthetix v2 debt shares for the provided address, at this epoch's snapshot, in other chains

#### declareAndCast

  ```solidity
  function declareAndCast(uint256 debtShare, bytes32[] merkleProof, address[] candidates) external
  ```

  Declares cross chain debt shares and casts a vote

#### initOrUpdateElectionSettings

  ```solidity
  function initOrUpdateElectionSettings(address[] initialCouncil, contract IWormhole wormholeCore, contract IWormholeRelayer wormholeRelayer, uint8 minimumActiveMembers, uint64 initialNominationPeriodStartDate, uint64 administrationPeriodDuration, uint64 nominationPeriodDuration, uint64 votingPeriodDuration) external
  ```

  Initialises the module and immediately starts the first epoch

**Parameters**
* `initialCouncil` (*address[]*) - addresses that will hold the initial council seats; Length cannot be greater than type(uint8).max or equal to 0
* `wormholeCore` (*contract IWormhole*) - wormhole contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#core-contracts
* `wormholeRelayer` (*contract IWormholeRelayer*) - wormhole relayer contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#standard-relayer
* `minimumActiveMembers` (*uint8*) - minimum number of active council members required, cannot be greater than initialCouncil length or equal to 0
* `initialNominationPeriodStartDate` (*uint64*) - start date for the first nomination period
* `administrationPeriodDuration` (*uint64*) - duration of the administration period, in days
* `nominationPeriodDuration` (*uint64*) - duration of the nomination period, in days
* `votingPeriodDuration` (*uint64*) - duration of the voting period, in days

#### tweakEpochSchedule

  ```solidity
  function tweakEpochSchedule(uint64 newNominationPeriodStartDate, uint64 newVotingPeriodStartDate, uint64 newEpochEndDate) external payable
  ```

  Adjusts the current epoch schedule requiring that the current period remains Administration

  This function takes timestamps as parameters for the new start dates for the new periods; can only be called during the Administration period

**Parameters**
* `newNominationPeriodStartDate` (*uint64*) - new start date for the nomination period
* `newVotingPeriodStartDate` (*uint64*) - new start date for the voting period
* `newEpochEndDate` (*uint64*) - new end date for the epoch

#### setNextElectionSettings

  ```solidity
  function setNextElectionSettings(uint8 epochSeatCount, uint8 minimumActiveMembers, uint64 epochDuration, uint64 nominationPeriodDuration, uint64 votingPeriodDuration, uint64 maxDateAdjustmentTolerance) external
  ```

  Adjust settings that will be used on next epoch

  can only be called during the Administration period

**Parameters**
* `epochSeatCount` (*uint8*) - number of council seats to be elected in the next epoch
* `minimumActiveMembers` (*uint8*) - minimum number of active council members required
* `epochDuration` (*uint64*) - duration of the epoch in days
* `nominationPeriodDuration` (*uint64*) - duration of the nomination period in days
* `votingPeriodDuration` (*uint64*) - duration of the voting period in days
* `maxDateAdjustmentTolerance` (*uint64*) - maximum allowed difference between the new epoch dates and the current epoch dates in days

#### dismissMembers

  ```solidity
  function dismissMembers(address[] members) external payable
  ```

  Allows the owner to remove one or more council members, triggering an election if a threshold is met

**Parameters**
* `members` (*address[]*) - list of council members to be removed

#### nominate

  ```solidity
  function nominate() external
  ```

  Allows anyone to self-nominate during the Nomination period

#### withdrawNomination

  ```solidity
  function withdrawNomination() external
  ```

  Self-withdrawal of nominations during the Nomination period

#### _recvCast

  ```solidity
  function _recvCast(uint256 epochIndex, address voter, uint256 votingPower, uint256 chainId, address[] candidates, uint256[] amounts) external
  ```

  Internal voting logic, receiving end of voting via Wormhole

#### _recvWithdrawVote

  ```solidity
  function _recvWithdrawVote(uint256 epochIndex, address voter, uint256 chainId) external
  ```

  Internal voting withdrawl logic, receiving end of withdrawing vote via Wormhole

#### evaluate

  ```solidity
  function evaluate(uint256 numBallots) external payable
  ```

  Processes ballots in batches during the Evaluation period (after epochEndDate)

  ElectionTally needs to be extended to specify how votes are counted
Should be called after all crosschain votes propogate; if called immediately when the evaluation period starts some votes have the chance of being lost

#### resolve

  ```solidity
  function resolve() external payable
  ```

  Shuffles NFTs and resolves an election after it has been evaluated

  Burns previous NFTs and mints new ones

#### isNominated

  ```solidity
  function isNominated(address candidate) external view returns (bool)
  ```

  Shows if a candidate has been nominated in the current epoch

#### getNominees

  ```solidity
  function getNominees() external view returns (address[])
  ```

  Returns a list of all nominated candidates in the current epoch

#### hasVoted

  ```solidity
  function hasVoted(address user, uint256 chainId) external view returns (bool)
  ```

  Returns if user has voted in the current election

#### getVotePower

  ```solidity
  function getVotePower(address user, uint256 chainId, uint256 electionId) external view returns (uint256)
  ```

  Returns the vote power of user in the current election

#### getBallotCandidates

  ```solidity
  function getBallotCandidates(address voter, uint256 chainId, uint256 electionId) external view returns (address[])
  ```

  Returns the list of candidates that a particular ballot has

#### isElectionEvaluated

  ```solidity
  function isElectionEvaluated() external view returns (bool)
  ```

  Returns whether all ballots in the current election have been counted

#### getBallot

  ```solidity
  function getBallot(address voter, uint256 chainId, uint256 electionId) external pure returns (struct Ballot.Data)
  ```

  Returns the number of ballots in the current election

#### getNumOfBallots

  ```solidity
  function getNumOfBallots() external view returns (uint256)
  ```

  Returns the number of ballots in the current election

#### getCandidateVotes

  ```solidity
  function getCandidateVotes(address candidate) external view returns (uint256)
  ```

  Returns the number of votes a candidate received. Requires the election to be partially or totally evaluated

#### getElectionWinners

  ```solidity
  function getElectionWinners() external view returns (address[])
  ```

  Returns the winners of the current election. Requires the election to be partially or totally evaluated

#### getCouncilToken

  ```solidity
  function getCouncilToken() external view returns (address)
  ```

  Returns the address of the council NFT token

#### getCouncilMembers

  ```solidity
  function getCouncilMembers() external view returns (address[])
  ```

  Returns the current NFT token holders

#### initElectionModuleSatellite

  ```solidity
  function initElectionModuleSatellite(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, contract IWormhole wormholeCore, contract IWormholeRelayer wormholeRelayer, address[] councilMembers) external
  ```

  Initialize the election module with the given council members and epoch schedule

  Utility method for initializing a new Satellite chain; can only be called once

**Parameters**
* `epochIndex` (*uint256*) - the index of the epoch
* `epochStartDate` (*uint64*) - the start date of the epoch (timestamp)
* `nominationPeriodStartDate` (*uint64*) - the start date of the nomination period (timestamp)
* `votingPeriodStartDate` (*uint64*) - the start date of the voting period (timestamp)
* `epochEndDate` (*uint64*) - the end date of the epoch (timestamp)
* `wormholeCore` (*contract IWormhole*) - wormhole contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#core-contracts
* `wormholeRelayer` (*contract IWormholeRelayer*) - wormhole relayer contract address on the current chain https://docs.wormhole.com/wormhole/reference/constants#standard-relayer
* `councilMembers` (*address[]*) - the initial council members

#### isElectionModuleInitialized

  ```solidity
  function isElectionModuleInitialized() external view returns (bool)
  ```

  Shows whether the module has been initialized

#### cast

  ```solidity
  function cast(address[] candidates, uint256[] amounts) external payable
  ```

  Allows anyone with vote power to vote on nominated candidates during the Voting period

  caller must use all of their voting power in one go i.e. no partial votes; casts from satellite get broadcast to mothership chain

**Parameters**
* `candidates` (*address[]*) - the candidates to vote for
* `amounts` (*uint256[]*) - the amount of votes for each candidate

#### withdrawVote

  ```solidity
  function withdrawVote() external payable
  ```

  Allows to withdraw a casted vote on the current network

#### getCurrentPeriod

  ```solidity
  function getCurrentPeriod() external view returns (uint256)
  ```

  Returns the current period type: Administration, Nomination, Voting, Evaluation

#### getEpochSchedule

  ```solidity
  function getEpochSchedule() external view returns (struct Epoch.Data epoch)
  ```

  Shows the current epoch schedule dates

#### getElectionSettings

  ```solidity
  function getElectionSettings() external view returns (struct ElectionSettings.Data settings)
  ```

  Shows the settings for the current election

#### getNextElectionSettings

  ```solidity
  function getNextElectionSettings() external view returns (struct ElectionSettings.Data settings)
  ```

  Shows the settings for the next election

#### getEpochIndex

  ```solidity
  function getEpochIndex() external view returns (uint256)
  ```

  Returns the index of the current epoch. The first epoch's index is 1

#### _recvDismissMembers

  ```solidity
  function _recvDismissMembers(address[] membersToDismiss, uint256 epochIndex) external
  ```

  Burn the council tokens from the given members; receiving end of members dismissal via Wormhole

#### _recvTweakEpochSchedule

  ```solidity
  function _recvTweakEpochSchedule(uint256 epochIndex, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate) external
  ```

  Tweak the epoch dates to the given ones, without validation because we assume that it was started from mothership

#### _recvResolve

  ```solidity
  function _recvResolve(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address[] councilMembers) external
  ```

  Burn current epoch council tokens and assign new ones, setup epoch dates. Receiving end of epoch resolution via Wormhole.

#### ElectionModuleInitialized

  ```solidity
  event ElectionModuleInitialized()
  ```

#### EpochStarted

  ```solidity
  event EpochStarted(uint256 epochId)
  ```

#### EpochScheduleUpdated

  ```solidity
  event EpochScheduleUpdated(uint64 epochId, uint64 startDate, uint64 endDate)
  ```

#### EmergencyElectionStarted

  ```solidity
  event EmergencyElectionStarted(uint256 epochId)
  ```

#### CandidateNominated

  ```solidity
  event CandidateNominated(address candidate, uint256 epochId)
  ```

#### NominationWithdrawn

  ```solidity
  event NominationWithdrawn(address candidate, uint256 epochId)
  ```

#### VoteRecorded

  ```solidity
  event VoteRecorded(address voter, uint256 chainId, uint256 epochId, uint256 votingPower, address[] candidates)
  ```

#### VoteWithdrawn

  ```solidity
  event VoteWithdrawn(address voter, uint256 chainId, uint256 epochId)
  ```

#### ElectionBatchEvaluated

  ```solidity
  event ElectionBatchEvaluated(uint256 epochId, uint256 numEvaluatedBallots, uint256 totalBallots)
  ```

#### ElectionEvaluated

  ```solidity
  event ElectionEvaluated(uint256 epochId, uint256 ballotCount)
  ```

#### CouncilMembersDismissed

  ```solidity
  event CouncilMembersDismissed(address[] dismissedMembers, uint256 epochId)
  ```

#### InitializedSatellite

  ```solidity
  event InitializedSatellite(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate, address[] councilMembers)
  ```

#### EpochSetup

  ```solidity
  event EpochSetup(uint256 epochIndex, uint64 epochStartDate, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate)
  ```

#### EpochScheduleTweaked

  ```solidity
  event EpochScheduleTweaked(uint256 epochIndex, uint64 nominationPeriodStartDate, uint64 votingPeriodStartDate, uint64 epochEndDate)
  ```

#### VoteCastSent

  ```solidity
  event VoteCastSent(address sender, address[] candidates, uint256[] amounts)
  ```

#### VoteWithdrawnSent

  ```solidity
  event VoteWithdrawnSent(address sender)
  ```

### MathUtil

#### sqrt

  ```solidity
  function sqrt(uint256 x) internal pure returns (uint256 z)
  ```

## Oracle Manager

### Node Module

#### registerNode

  ```solidity
  function registerNode(enum NodeDefinition.NodeType nodeType, bytes parameters, bytes32[] parents) external returns (bytes32 nodeId)
  ```

  Registers a node

**Parameters**
* `nodeType` (*enum NodeDefinition.NodeType*) - The nodeType assigned to this node.
* `parameters` (*bytes*) - The parameters assigned to this node.
* `parents` (*bytes32[]*) - The parents assigned to this node.

**Returns**
* `nodeId` (*bytes32*) - The id of the registered node.
#### getNodeId

  ```solidity
  function getNodeId(enum NodeDefinition.NodeType nodeType, bytes parameters, bytes32[] parents) external pure returns (bytes32 nodeId)
  ```

  Returns the ID of a node, whether or not it has been registered.

**Parameters**
* `nodeType` (*enum NodeDefinition.NodeType*) - The nodeType assigned to this node.
* `parameters` (*bytes*) - The parameters assigned to this node.
* `parents` (*bytes32[]*) - The parents assigned to this node.

**Returns**
* `nodeId` (*bytes32*) - The id of the node.
#### getNode

  ```solidity
  function getNode(bytes32 nodeId) external pure returns (struct NodeDefinition.Data node)
  ```

  Returns a node's definition (type, parameters, and parents)

**Parameters**
* `nodeId` (*bytes32*) - The node ID

**Returns**
* `node` (*struct NodeDefinition.Data*) - The node's definition data
#### process

  ```solidity
  function process(bytes32 nodeId) external view returns (struct NodeOutput.Data node)
  ```

  Returns a node current output data

**Parameters**
* `nodeId` (*bytes32*) - The node ID

**Returns**
* `node` (*struct NodeOutput.Data*) - The node's output data
#### processWithRuntime

  ```solidity
  function processWithRuntime(bytes32 nodeId, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data node)
  ```

  Returns a node current output data

**Parameters**
* `nodeId` (*bytes32*) - The node ID
* `runtimeKeys` (*bytes32[]*) - Keys corresponding to runtime values which could be used by the node graph
* `runtimeValues` (*bytes32[]*) - The values used by the node graph

**Returns**
* `node` (*struct NodeOutput.Data*) - The node's output data
#### processManyWithRuntime

  ```solidity
  function processManyWithRuntime(bytes32[] nodeIds, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data[] nodes)
  ```

  Returns node current output data for many nodes at the same time, aggregating errors (if any)

**Parameters**
* `nodeIds` (*bytes32[]*) - The node ID
* `runtimeKeys` (*bytes32[]*) - Keys corresponding to runtime values which could be used by the node graph. The same keys are used for all nodes
* `runtimeValues` (*bytes32[]*) - The values used by the node graph. The same values are used for all nodes

**Returns**
* `nodes` (*struct NodeOutput.Data[]*) - The output data for all the nodes
#### processManyWithManyRuntime

  ```solidity
  function processManyWithManyRuntime(bytes32[] nodeIds, bytes32[][] runtimeKeys, bytes32[][] runtimeValues) external view returns (struct NodeOutput.Data[] nodes)
  ```

  Same as `processManyWithRuntime`, but allows for different runtime for each oracle call.

**Parameters**
* `nodeIds` (*bytes32[]*) - The node ID
* `runtimeKeys` (*bytes32[][]*) - Keys corresponding to runtime values which could be used by the node graph.
* `runtimeValues` (*bytes32[][]*) - The values used by the node graph.

**Returns**
* `nodes` (*struct NodeOutput.Data[]*) - The output data for all the nodes

#### NodeRegistered

  ```solidity
  event NodeRegistered(bytes32 nodeId, enum NodeDefinition.NodeType nodeType, bytes parameters, bytes32[] parents)
  ```

  Emitted when `registerNode` is called.

**Parameters**
* `nodeId` (*bytes32*) - The id of the registered node.
* `nodeType` (*enum NodeDefinition.NodeType*) - The nodeType assigned to this node.
* `parameters` (*bytes*) - The parameters assigned to this node.
* `parents` (*bytes32[]*) - The parents assigned to this node.

### ChainlinkNode

#### process

  ```solidity
  function process(bytes parameters) internal view returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### getTwapPrice

  ```solidity
  function getTwapPrice(contract IAggregatorV3Interface chainlink, uint80 latestRoundId, int256 latestPrice, uint256 twapTimeInterval) internal view returns (int256 price)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal view returns (bool valid)
  ```

### ConstantNode

#### process

  ```solidity
  function process(bytes parameters) internal view returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal pure returns (bool valid)
  ```

### ExternalNode

#### process

  ```solidity
  function process(struct NodeOutput.Data[] prices, bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) internal view returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal returns (bool valid)
  ```

### PriceDeviationCircuitBreakerNode

#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters) internal pure returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### abs

  ```solidity
  function abs(int256 x) private pure returns (int256 result)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal pure returns (bool valid)
  ```

### ReducerNode

#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters) internal pure returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### median

  ```solidity
  function median(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data medianPrice)
  ```

#### mean

  ```solidity
  function mean(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data meanPrice)
  ```

#### recent

  ```solidity
  function recent(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data recentPrice)
  ```

#### max

  ```solidity
  function max(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data maxPrice)
  ```

#### min

  ```solidity
  function min(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data minPrice)
  ```

#### mul

  ```solidity
  function mul(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data mulPrice)
  ```

#### div

  ```solidity
  function div(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data divPrice)
  ```

#### mulDecimal

  ```solidity
  function mulDecimal(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data mulPrice)
  ```

#### divDecimal

  ```solidity
  function divDecimal(struct NodeOutput.Data[] parentNodeOutputs) internal pure returns (struct NodeOutput.Data divPrice)
  ```

#### quickSort

  ```solidity
  function quickSort(struct NodeOutput.Data[] arr, int256 left, int256 right) internal pure
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal pure returns (bool valid)
  ```

### StalenessCircuitBreakerNode

#### process

  ```solidity
  function process(struct NodeDefinition.Data nodeDefinition, bytes32[] runtimeKeys, bytes32[] runtimeValues) internal view returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal pure returns (bool valid)
  ```

### UniswapNode

#### process

  ```solidity
  function process(bytes parameters) internal view returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### getQuoteAtTick

  ```solidity
  function getQuoteAtTick(int24 tick, uint256 baseAmount, address baseToken, address quoteToken) internal pure returns (uint256 quoteAmount)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal view returns (bool valid)
  ```

### PythNode

#### process

  ```solidity
  function process(bytes parameters) internal view returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal view returns (bool valid)
  ```

### PythOffchainLookupNode

#### process

  ```solidity
  function process(bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) internal pure returns (struct NodeOutput.Data nodeOutput, bytes possibleError)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) internal pure returns (bool valid)
  ```

# Auxiliary Packages

### ArbGasPriceOracle

#### constructor

  ```solidity
  constructor(address _arbGasInfoPrecompileAddress) public
  ```

  construct the ArbGasPriceOracle contract

**Parameters**
* `_arbGasInfoPrecompileAddress` (*address*) - the address of the ArbGasInfo precompile

#### process

  ```solidity
  function process(struct NodeOutput.Data[], bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data nodeOutput)
  ```

  process the cost of execution in ETH

**Parameters**
* `` (*struct NodeOutput.Data[]*) - 
* `parameters` (*bytes*) - the parameters for the cost of execution calculation
* `runtimeKeys` (*bytes32[]*) - the runtime keys for the cost of execution calculation
* `runtimeValues` (*bytes32[]*) - the runtime values for the cost of execution calculation

**Returns**
* `nodeOutput` (*struct NodeOutput.Data*) - the cost of execution in ETH and timestamp when the cost was calculated (other fields are not used in this implementation)
#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external view returns (bool valid)
  ```

  verify the validity of the external node and its functionality

**Parameters**
* `nodeDefinition` (*struct NodeDefinition.Data*) - the node definition to verify

**Returns**
* `valid` (*bool*) - true if the external node is valid, false otherwise
#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) external pure returns (bool)
  ```

  check if the contract supports the given interface

**Parameters**
* `interfaceId` (*bytes4*) - the interface ID to check

**Returns**
* `[0]` (*bool*) - true if the contract supports the given interface, false otherwise
#### getCostOfExecutionEth

  ```solidity
  function getCostOfExecutionEth(struct ArbGasPriceOracle.RuntimeParams runtimeParams) internal view returns (uint256 costOfExecutionGrossEth)
  ```

  calculate and return the cost of execution in ETH

  gas costs are 2-dimensional: L1 and L2 resources
     - L1 resources include calldata
     - L2 resources include computation
total fee charged to a transaction is the L2 basefee,
multiplied by the sum of the L2 gas used plus the L1 calldata charge

**Parameters**
* `runtimeParams` (*struct ArbGasPriceOracle.RuntimeParams*) - the runtime parameters for the cost of execution calculation

**Returns**
* `costOfExecutionGrossEth` (*uint256*) - the cost of execution in ETH
#### getGasUnits

  ```solidity
  function getGasUnits(struct ArbGasPriceOracle.RuntimeParams runtimeParams) internal pure returns (uint256 gasUnitsL1, uint256 gasUnitsL2)
  ```

  get the gas units consumed on L1 and L2 for the given execution kind

**Parameters**
* `runtimeParams` (*struct ArbGasPriceOracle.RuntimeParams*) - the runtime parameters for the cost of execution calculation

**Returns**
* `gasUnitsL1` (*uint256*) - the gas units consumed on L1
* `gasUnitsL2` (*uint256*) - the gas units consumed on L2
#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external returns (bool)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### ArbGasInfo

#### getPricesInWeiWithAggregator

  ```solidity
  function getPricesInWeiWithAggregator(address aggregator) external view returns (uint256, uint256, uint256, uint256, uint256, uint256)
  ```

  Get gas prices for a provided aggregator

**Returns**
* `[0]` (*uint256*) - return gas prices in wei        (            per L2 tx,            per L1 calldata byte            per storage allocation,            per ArbGas base,            per ArbGas congestion,            per ArbGas total        )
* `[1]` (*uint256*) - 
* `[2]` (*uint256*) - 
* `[3]` (*uint256*) - 
* `[4]` (*uint256*) - 
* `[5]` (*uint256*) - 
#### getPricesInWei

  ```solidity
  function getPricesInWei() external view returns (uint256, uint256, uint256, uint256, uint256, uint256)
  ```

  Get gas prices. Uses the caller's preferred aggregator, or the default if
the caller doesn't have a preferred one.

**Returns**
* `[0]` (*uint256*) - return gas prices in wei        (            per L2 tx,            per L1 calldata byte            per storage allocation,            per ArbGas base,            per ArbGas congestion,            per ArbGas total        )
* `[1]` (*uint256*) - 
* `[2]` (*uint256*) - 
* `[3]` (*uint256*) - 
* `[4]` (*uint256*) - 
* `[5]` (*uint256*) - 
#### getPricesInArbGasWithAggregator

  ```solidity
  function getPricesInArbGasWithAggregator(address aggregator) external view returns (uint256, uint256, uint256)
  ```

  Get prices in ArbGas for the supplied aggregator

**Returns**
* `[0]` (*uint256*) - (per L2 tx, per L1 calldata byte, per storage allocation)
* `[1]` (*uint256*) - 
* `[2]` (*uint256*) - 
#### getPricesInArbGas

  ```solidity
  function getPricesInArbGas() external view returns (uint256, uint256, uint256)
  ```

  Get prices in ArbGas. Assumes the callers preferred validator, or the default
if caller doesn't have a preferred one.

**Returns**
* `[0]` (*uint256*) - (per L2 tx, per L1 calldata byte, per storage allocation)
* `[1]` (*uint256*) - 
* `[2]` (*uint256*) - 
#### getGasAccountingParams

  ```solidity
  function getGasAccountingParams() external view returns (uint256, uint256, uint256)
  ```

  Get the gas accounting parameters. `gasPoolMax` is always zero, as the exponential
pricing model has no such notion.

**Returns**
* `[0]` (*uint256*) - (speedLimitPerSecond, gasPoolMax, maxTxGasLimit)
* `[1]` (*uint256*) - 
* `[2]` (*uint256*) - 
#### getMinimumGasPrice

  ```solidity
  function getMinimumGasPrice() external view returns (uint256)
  ```

  Get the minimum gas price needed for a tx to succeed

#### getL1BaseFeeEstimate

  ```solidity
  function getL1BaseFeeEstimate() external view returns (uint256)
  ```

  Get ArbOS's estimate of the L1 basefee in wei

#### getL1BaseFeeEstimateInertia

  ```solidity
  function getL1BaseFeeEstimateInertia() external view returns (uint64)
  ```

  Get how slowly ArbOS updates its estimate of the L1 basefee

#### getL1RewardRate

  ```solidity
  function getL1RewardRate() external view returns (uint64)
  ```

  Get the L1 pricer reward rate, in wei per unit
Available in ArbOS version 11

#### getL1RewardRecipient

  ```solidity
  function getL1RewardRecipient() external view returns (address)
  ```

  Get the L1 pricer reward recipient
Available in ArbOS version 11

#### getL1GasPriceEstimate

  ```solidity
  function getL1GasPriceEstimate() external view returns (uint256)
  ```

  Deprecated -- Same as getL1BaseFeeEstimate()

#### getCurrentTxL1GasFees

  ```solidity
  function getCurrentTxL1GasFees() external view returns (uint256)
  ```

  Get L1 gas fees paid by the current transaction

#### getGasBacklog

  ```solidity
  function getGasBacklog() external view returns (uint64)
  ```

  Get the backlogged amount of gas burnt in excess of the speed limit

#### getPricingInertia

  ```solidity
  function getPricingInertia() external view returns (uint64)
  ```

  Get how slowly ArbOS updates the L2 basefee in response to backlogged gas

#### getGasBacklogTolerance

  ```solidity
  function getGasBacklogTolerance() external view returns (uint64)
  ```

  Get the forgivable amount of backlogged gas ArbOS will ignore when raising the basefee

#### getL1PricingSurplus

  ```solidity
  function getL1PricingSurplus() external view returns (int256)
  ```

  Returns the surplus of funds for L1 batch posting payments (may be negative).

#### getPerBatchGasCharge

  ```solidity
  function getPerBatchGasCharge() external view returns (int64)
  ```

  Returns the base charge (in L1 gas) attributed to each data batch in the calldata pricer

#### getAmortizedCostCapBips

  ```solidity
  function getAmortizedCostCapBips() external view returns (uint64)
  ```

  Returns the cost amortization cap in basis points

#### getL1FeesAvailable

  ```solidity
  function getL1FeesAvailable() external view returns (uint256)
  ```

  Returns the available funds from L1 fees

#### getL1PricingEquilibrationUnits

  ```solidity
  function getL1PricingEquilibrationUnits() external view returns (uint256)
  ```

  Returns the equilibration units parameter for L1 price adjustment algorithm
Available in ArbOS version 20

#### getLastL1PricingUpdateTime

  ```solidity
  function getLastL1PricingUpdateTime() external view returns (uint64)
  ```

  Returns the last time the L1 calldata pricer was updated.
Available in ArbOS version 20

#### getL1PricingFundsDueForRewards

  ```solidity
  function getL1PricingFundsDueForRewards() external view returns (uint256)
  ```

  Returns the amount of L1 calldata payments due for rewards (per the L1 reward rate)
Available in ArbOS version 20

#### getL1PricingUnitsSinceUpdate

  ```solidity
  function getL1PricingUnitsSinceUpdate() external view returns (uint64)
  ```

  Returns the amount of L1 calldata posted since the last update.
Available in ArbOS version 20

#### getLastL1PricingSurplus

  ```solidity
  function getLastL1PricingSurplus() external view returns (int256)
  ```

  Returns the L1 pricing surplus as of the last update (may be negative).
Available in ArbOS version 20

### BuybackSnx

#### constructor

  ```solidity
  constructor(uint256 _premium, uint256 _snxFeeShare, address _oracleManager, bytes32 _snxNodeId, address _snxToken, address _usdToken) public
  ```

#### processBuyback

  ```solidity
  function processBuyback(uint256 snxAmount) external
  ```

#### quoteFees

  ```solidity
  function quoteFees(uint128 marketId, uint256 feeAmount, address sender) external view returns (uint256)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) public view virtual returns (bool)
  ```

#### quoteFees

  ```solidity
  function quoteFees(uint128 marketId, uint256 feeAmount, address transactor) external returns (uint256 feeAmountToCollect)
  ```

  .This function is called by the spot market proxy to get the fee amount to be collected.

  .The quoted fee amount is then transferred directly to the fee collector.

**Parameters**
* `marketId` (*uint128*) - .synth market id value
* `feeAmount` (*uint256*) - .max fee amount that can be collected
* `transactor` (*address*) - .the trader the fee was collected from

**Returns**
* `feeAmountToCollect` (*uint256*) - .quoted fee amount
#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

#### BuybackProcessed

  ```solidity
  event BuybackProcessed(address buyer, uint256 snx, uint256 usd)
  ```

### OwnedFeeCollector

#### constructor

  ```solidity
  constructor(address _owner, address _feeShareRecipient, uint256 _feeShare, address _feeToken) public
  ```

#### quoteFees

  ```solidity
  function quoteFees(uint128 marketId, uint256 feeAmount, address sender) external view returns (uint256)
  ```

#### claimFees

  ```solidity
  function claimFees() external
  ```

#### setFeeShare

  ```solidity
  function setFeeShare(uint256 _newFeeShare) external
  ```

#### setFeeShareRecipient

  ```solidity
  function setFeeShareRecipient(address _newFeeShareRecipient) external
  ```

#### acceptFeeShareRecipient

  ```solidity
  function acceptFeeShareRecipient() external
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) public view virtual returns (bool)
  ```

#### constructor

  ```solidity
  constructor(address initialOwner) public
  ```

#### acceptOwnership

  ```solidity
  function acceptOwnership() public
  ```

  Allows a nominated address to accept ownership of the contract.

  Reverts if the caller is not nominated.

#### nominateNewOwner

  ```solidity
  function nominateNewOwner(address newNominatedOwner) public
  ```

  Allows the current owner to nominate a new owner.

  The nominated owner will have to call `acceptOwnership` in a separate transaction in order to finalize the action and become the new contract owner.

**Parameters**
* `newNominatedOwner` (*address*) - The address that is to become nominated.

#### renounceNomination

  ```solidity
  function renounceNomination() external
  ```

  Allows a nominated owner to reject the nomination.

#### owner

  ```solidity
  function owner() external view returns (address)
  ```

  Returns the current owner of the contract.

#### nominatedOwner

  ```solidity
  function nominatedOwner() external view returns (address)
  ```

  Returns the current nominated owner of the contract.

  Only one address can be nominated at a time.

#### acceptOwnership

  ```solidity
  function acceptOwnership() external
  ```

  Allows a nominated address to accept ownership of the contract.

  Reverts if the caller is not nominated.

#### nominateNewOwner

  ```solidity
  function nominateNewOwner(address newNominatedOwner) external
  ```

  Allows the current owner to nominate a new owner.

  The nominated owner will have to call `acceptOwnership` in a separate transaction in order to finalize the action and become the new contract owner.

**Parameters**
* `newNominatedOwner` (*address*) - The address that is to become nominated.

#### renounceNomination

  ```solidity
  function renounceNomination() external
  ```

  Allows a nominated owner to reject the nomination.

#### owner

  ```solidity
  function owner() external view returns (address)
  ```

  Returns the current owner of the contract.

#### nominatedOwner

  ```solidity
  function nominatedOwner() external view returns (address)
  ```

  Returns the current nominated owner of the contract.

  Only one address can be nominated at a time.

#### quoteFees

  ```solidity
  function quoteFees(uint128 marketId, uint256 feeAmount, address transactor) external returns (uint256 feeAmountToCollect)
  ```

  .This function is called by the spot market proxy to get the fee amount to be collected.

  .The quoted fee amount is then transferred directly to the fee collector.

**Parameters**
* `marketId` (*uint128*) - .synth market id value
* `feeAmount` (*uint256*) - .max fee amount that can be collected
* `transactor` (*address*) - .the trader the fee was collected from

**Returns**
* `feeAmountToCollect` (*uint256*) - .quoted fee amount
#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

#### OwnerNominated

  ```solidity
  event OwnerNominated(address newOwner)
  ```

  Emitted when an address has been nominated.

**Parameters**
* `newOwner` (*address*) - The address that has been nominated.

#### OwnerChanged

  ```solidity
  event OwnerChanged(address oldOwner, address newOwner)
  ```

  Emitted when the owner of the contract has changed.

**Parameters**
* `oldOwner` (*address*) - The previous owner of the contract.
* `newOwner` (*address*) - The new owner of the contract.

### ERC4626ToAssetsRatioOracle

#### constructor

  ```solidity
  constructor(address _vaultAddress) public
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[], bytes, bytes32[], bytes32[]) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external view returns (bool valid)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) external pure returns (bool)
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external returns (bool)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### IERC20

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the value of tokens in existence.

#### balanceOf

  ```solidity
  function balanceOf(address account) external view returns (uint256)
  ```

  Returns the value of tokens owned by `account`.

#### transfer

  ```solidity
  function transfer(address to, uint256 value) external returns (bool)
  ```

  Moves a `value` amount of tokens from the caller's account to `to`.

Returns a boolean value indicating whether the operation succeeded.

Emits a {Transfer} event.

#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns the remaining number of tokens that `spender` will be
allowed to spend on behalf of `owner` through {transferFrom}. This is
zero by default.

This value changes when {approve} or {transferFrom} are called.

#### approve

  ```solidity
  function approve(address spender, uint256 value) external returns (bool)
  ```

  Sets a `value` amount of tokens as the allowance of `spender` over the
caller's tokens.

Returns a boolean value indicating whether the operation succeeded.

IMPORTANT: Beware that changing an allowance with this method brings the risk
that someone may use both the old and the new allowance by unfortunate
transaction ordering. One possible solution to mitigate this race
condition is to first reduce the spender's allowance to 0 and set the
desired value afterwards:
https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729

Emits an {Approval} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 value) external returns (bool)
  ```

  Moves a `value` amount of tokens from `from` to `to` using the
allowance mechanism. `value` is then deducted from the caller's
allowance.

Returns a boolean value indicating whether the operation succeeded.

Emits a {Transfer} event.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 value)
  ```

  Emitted when `value` tokens are moved from one account (`from`) to
another (`to`).

Note that `value` may be zero.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 value)
  ```

  Emitted when the allowance of a `spender` for an `owner` is set by
a call to {approve}. `value` is the new allowance.

### IERC20Metadata

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Returns the name of the token.

#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Returns the symbol of the token.

#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Returns the decimals places of the token.

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the value of tokens in existence.

#### balanceOf

  ```solidity
  function balanceOf(address account) external view returns (uint256)
  ```

  Returns the value of tokens owned by `account`.

#### transfer

  ```solidity
  function transfer(address to, uint256 value) external returns (bool)
  ```

  Moves a `value` amount of tokens from the caller's account to `to`.

Returns a boolean value indicating whether the operation succeeded.

Emits a {Transfer} event.

#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns the remaining number of tokens that `spender` will be
allowed to spend on behalf of `owner` through {transferFrom}. This is
zero by default.

This value changes when {approve} or {transferFrom} are called.

#### approve

  ```solidity
  function approve(address spender, uint256 value) external returns (bool)
  ```

  Sets a `value` amount of tokens as the allowance of `spender` over the
caller's tokens.

Returns a boolean value indicating whether the operation succeeded.

IMPORTANT: Beware that changing an allowance with this method brings the risk
that someone may use both the old and the new allowance by unfortunate
transaction ordering. One possible solution to mitigate this race
condition is to first reduce the spender's allowance to 0 and set the
desired value afterwards:
https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729

Emits an {Approval} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 value) external returns (bool)
  ```

  Moves a `value` amount of tokens from `from` to `to` using the
allowance mechanism. `value` is then deducted from the caller's
allowance.

Returns a boolean value indicating whether the operation succeeded.

Emits a {Transfer} event.

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 value)
  ```

  Emitted when `value` tokens are moved from one account (`from`) to
another (`to`).

Note that `value` may be zero.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 value)
  ```

  Emitted when the allowance of a `spender` for an `owner` is set by
a call to {approve}. `value` is the new allowance.

### IERC4626

#### asset

  ```solidity
  function asset() external view returns (address assetTokenAddress)
  ```

  Returns the address of the underlying token used for the Vault for accounting, depositing, and withdrawing.

- MUST be an ERC-20 token contract.
- MUST NOT revert.

#### totalAssets

  ```solidity
  function totalAssets() external view returns (uint256 totalManagedAssets)
  ```

  Returns the total amount of the underlying asset that is “managed” by Vault.

- SHOULD include any compounding that occurs from yield.
- MUST be inclusive of any fees that are charged against assets in the Vault.
- MUST NOT revert.

#### convertToShares

  ```solidity
  function convertToShares(uint256 assets) external view returns (uint256 shares)
  ```

  Returns the amount of shares that the Vault would exchange for the amount of assets provided, in an ideal
scenario where all the conditions are met.

- MUST NOT be inclusive of any fees that are charged against assets in the Vault.
- MUST NOT show any variations depending on the caller.
- MUST NOT reflect slippage or other on-chain conditions, when performing the actual exchange.
- MUST NOT revert.

NOTE: This calculation MAY NOT reflect the “per-user” price-per-share, and instead should reflect the
“average-user’s” price-per-share, meaning what the average user should expect to see when exchanging to and
from.

#### convertToAssets

  ```solidity
  function convertToAssets(uint256 shares) external view returns (uint256 assets)
  ```

  Returns the amount of assets that the Vault would exchange for the amount of shares provided, in an ideal
scenario where all the conditions are met.

- MUST NOT be inclusive of any fees that are charged against assets in the Vault.
- MUST NOT show any variations depending on the caller.
- MUST NOT reflect slippage or other on-chain conditions, when performing the actual exchange.
- MUST NOT revert.

NOTE: This calculation MAY NOT reflect the “per-user” price-per-share, and instead should reflect the
“average-user’s” price-per-share, meaning what the average user should expect to see when exchanging to and
from.

#### maxDeposit

  ```solidity
  function maxDeposit(address receiver) external view returns (uint256 maxAssets)
  ```

  Returns the maximum amount of the underlying asset that can be deposited into the Vault for the receiver,
through a deposit call.

- MUST return a limited value if receiver is subject to some deposit limit.
- MUST return 2 ** 256 - 1 if there is no limit on the maximum amount of assets that may be deposited.
- MUST NOT revert.

#### previewDeposit

  ```solidity
  function previewDeposit(uint256 assets) external view returns (uint256 shares)
  ```

  Allows an on-chain or off-chain user to simulate the effects of their deposit at the current block, given
current on-chain conditions.

- MUST return as close to and no more than the exact amount of Vault shares that would be minted in a deposit
  call in the same transaction. I.e. deposit should return the same or more shares as previewDeposit if called
  in the same transaction.
- MUST NOT account for deposit limits like those returned from maxDeposit and should always act as though the
  deposit would be accepted, regardless if the user has enough tokens approved, etc.
- MUST be inclusive of deposit fees. Integrators should be aware of the existence of deposit fees.
- MUST NOT revert.

NOTE: any unfavorable discrepancy between convertToShares and previewDeposit SHOULD be considered slippage in
share price or some other type of condition, meaning the depositor will lose assets by depositing.

#### deposit

  ```solidity
  function deposit(uint256 assets, address receiver) external returns (uint256 shares)
  ```

  Mints shares Vault shares to receiver by depositing exactly amount of underlying tokens.

- MUST emit the Deposit event.
- MAY support an additional flow in which the underlying tokens are owned by the Vault contract before the
  deposit execution, and are accounted for during deposit.
- MUST revert if all of assets cannot be deposited (due to deposit limit being reached, slippage, the user not
  approving enough underlying tokens to the Vault contract, etc).

NOTE: most implementations will require pre-approval of the Vault with the Vault’s underlying asset token.

#### maxMint

  ```solidity
  function maxMint(address receiver) external view returns (uint256 maxShares)
  ```

  Returns the maximum amount of the Vault shares that can be minted for the receiver, through a mint call.
- MUST return a limited value if receiver is subject to some mint limit.
- MUST return 2 ** 256 - 1 if there is no limit on the maximum amount of shares that may be minted.
- MUST NOT revert.

#### previewMint

  ```solidity
  function previewMint(uint256 shares) external view returns (uint256 assets)
  ```

  Allows an on-chain or off-chain user to simulate the effects of their mint at the current block, given
current on-chain conditions.

- MUST return as close to and no fewer than the exact amount of assets that would be deposited in a mint call
  in the same transaction. I.e. mint should return the same or fewer assets as previewMint if called in the
  same transaction.
- MUST NOT account for mint limits like those returned from maxMint and should always act as though the mint
  would be accepted, regardless if the user has enough tokens approved, etc.
- MUST be inclusive of deposit fees. Integrators should be aware of the existence of deposit fees.
- MUST NOT revert.

NOTE: any unfavorable discrepancy between convertToAssets and previewMint SHOULD be considered slippage in
share price or some other type of condition, meaning the depositor will lose assets by minting.

#### mint

  ```solidity
  function mint(uint256 shares, address receiver) external returns (uint256 assets)
  ```

  Mints exactly shares Vault shares to receiver by depositing amount of underlying tokens.

- MUST emit the Deposit event.
- MAY support an additional flow in which the underlying tokens are owned by the Vault contract before the mint
  execution, and are accounted for during mint.
- MUST revert if all of shares cannot be minted (due to deposit limit being reached, slippage, the user not
  approving enough underlying tokens to the Vault contract, etc).

NOTE: most implementations will require pre-approval of the Vault with the Vault’s underlying asset token.

#### maxWithdraw

  ```solidity
  function maxWithdraw(address owner) external view returns (uint256 maxAssets)
  ```

  Returns the maximum amount of the underlying asset that can be withdrawn from the owner balance in the
Vault, through a withdraw call.

- MUST return a limited value if owner is subject to some withdrawal limit or timelock.
- MUST NOT revert.

#### previewWithdraw

  ```solidity
  function previewWithdraw(uint256 assets) external view returns (uint256 shares)
  ```

  Allows an on-chain or off-chain user to simulate the effects of their withdrawal at the current block,
given current on-chain conditions.

- MUST return as close to and no fewer than the exact amount of Vault shares that would be burned in a withdraw
  call in the same transaction. I.e. withdraw should return the same or fewer shares as previewWithdraw if
  called
  in the same transaction.
- MUST NOT account for withdrawal limits like those returned from maxWithdraw and should always act as though
  the withdrawal would be accepted, regardless if the user has enough shares, etc.
- MUST be inclusive of withdrawal fees. Integrators should be aware of the existence of withdrawal fees.
- MUST NOT revert.

NOTE: any unfavorable discrepancy between convertToShares and previewWithdraw SHOULD be considered slippage in
share price or some other type of condition, meaning the depositor will lose assets by depositing.

#### withdraw

  ```solidity
  function withdraw(uint256 assets, address receiver, address owner) external returns (uint256 shares)
  ```

  Burns shares from owner and sends exactly assets of underlying tokens to receiver.

- MUST emit the Withdraw event.
- MAY support an additional flow in which the underlying tokens are owned by the Vault contract before the
  withdraw execution, and are accounted for during withdraw.
- MUST revert if all of assets cannot be withdrawn (due to withdrawal limit being reached, slippage, the owner
  not having enough shares, etc).

Note that some implementations will require pre-requesting to the Vault before a withdrawal may be performed.
Those methods should be performed separately.

#### maxRedeem

  ```solidity
  function maxRedeem(address owner) external view returns (uint256 maxShares)
  ```

  Returns the maximum amount of Vault shares that can be redeemed from the owner balance in the Vault,
through a redeem call.

- MUST return a limited value if owner is subject to some withdrawal limit or timelock.
- MUST return balanceOf(owner) if owner is not subject to any withdrawal limit or timelock.
- MUST NOT revert.

#### previewRedeem

  ```solidity
  function previewRedeem(uint256 shares) external view returns (uint256 assets)
  ```

  Allows an on-chain or off-chain user to simulate the effects of their redeemption at the current block,
given current on-chain conditions.

- MUST return as close to and no more than the exact amount of assets that would be withdrawn in a redeem call
  in the same transaction. I.e. redeem should return the same or more assets as previewRedeem if called in the
  same transaction.
- MUST NOT account for redemption limits like those returned from maxRedeem and should always act as though the
  redemption would be accepted, regardless if the user has enough shares, etc.
- MUST be inclusive of withdrawal fees. Integrators should be aware of the existence of withdrawal fees.
- MUST NOT revert.

NOTE: any unfavorable discrepancy between convertToAssets and previewRedeem SHOULD be considered slippage in
share price or some other type of condition, meaning the depositor will lose assets by redeeming.

#### redeem

  ```solidity
  function redeem(uint256 shares, address receiver, address owner) external returns (uint256 assets)
  ```

  Burns exactly shares from owner and sends assets of underlying tokens to receiver.

- MUST emit the Withdraw event.
- MAY support an additional flow in which the underlying tokens are owned by the Vault contract before the
  redeem execution, and are accounted for during redeem.
- MUST revert if all of shares cannot be redeemed (due to withdrawal limit being reached, slippage, the owner
  not having enough shares, etc).

NOTE: some implementations will require pre-requesting to the Vault before a withdrawal may be performed.
Those methods should be performed separately.

#### name

  ```solidity
  function name() external view returns (string)
  ```

  Returns the name of the token.

#### symbol

  ```solidity
  function symbol() external view returns (string)
  ```

  Returns the symbol of the token.

#### decimals

  ```solidity
  function decimals() external view returns (uint8)
  ```

  Returns the decimals places of the token.

#### totalSupply

  ```solidity
  function totalSupply() external view returns (uint256)
  ```

  Returns the value of tokens in existence.

#### balanceOf

  ```solidity
  function balanceOf(address account) external view returns (uint256)
  ```

  Returns the value of tokens owned by `account`.

#### transfer

  ```solidity
  function transfer(address to, uint256 value) external returns (bool)
  ```

  Moves a `value` amount of tokens from the caller's account to `to`.

Returns a boolean value indicating whether the operation succeeded.

Emits a {Transfer} event.

#### allowance

  ```solidity
  function allowance(address owner, address spender) external view returns (uint256)
  ```

  Returns the remaining number of tokens that `spender` will be
allowed to spend on behalf of `owner` through {transferFrom}. This is
zero by default.

This value changes when {approve} or {transferFrom} are called.

#### approve

  ```solidity
  function approve(address spender, uint256 value) external returns (bool)
  ```

  Sets a `value` amount of tokens as the allowance of `spender` over the
caller's tokens.

Returns a boolean value indicating whether the operation succeeded.

IMPORTANT: Beware that changing an allowance with this method brings the risk
that someone may use both the old and the new allowance by unfortunate
transaction ordering. One possible solution to mitigate this race
condition is to first reduce the spender's allowance to 0 and set the
desired value afterwards:
https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729

Emits an {Approval} event.

#### transferFrom

  ```solidity
  function transferFrom(address from, address to, uint256 value) external returns (bool)
  ```

  Moves a `value` amount of tokens from `from` to `to` using the
allowance mechanism. `value` is then deducted from the caller's
allowance.

Returns a boolean value indicating whether the operation succeeded.

Emits a {Transfer} event.

#### Deposit

  ```solidity
  event Deposit(address sender, address owner, uint256 assets, uint256 shares)
  ```

#### Withdraw

  ```solidity
  event Withdraw(address sender, address receiver, address owner, uint256 assets, uint256 shares)
  ```

#### Transfer

  ```solidity
  event Transfer(address from, address to, uint256 value)
  ```

  Emitted when `value` tokens are moved from one account (`from`) to
another (`to`).

Note that `value` may be zero.

#### Approval

  ```solidity
  event Approval(address owner, address spender, uint256 value)
  ```

  Emitted when the allowance of a `spender` for an `owner` is set by
a call to {approve}. `value` is the new allowance.

### OpGasPriceOracle

#### constructor

  ```solidity
  constructor(address _ovmGasPriceOracleAddress) public
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[], bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data nodeOutput)
  ```

#### getCostOfExecutionEth

  ```solidity
  function getCostOfExecutionEth(struct OpGasPriceOracle.RuntimeParams runtimeParams) internal view returns (uint256 costOfExecutionGrossEth)
  ```

#### getGasUnits

  ```solidity
  function getGasUnits(struct OpGasPriceOracle.RuntimeParams runtimeParams) internal pure returns (uint256 gasUnitsL1, uint256 gasUnitsL2, uint256 unsignedTxSize)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external view returns (bool valid)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) external pure returns (bool)
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external returns (bool)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### IOVM_GasPriceOracle_legacy

#### DECIMALS

  ```solidity
  function DECIMALS() external pure returns (uint256)
  ```

  Number of decimals used in the scalar.

#### getL1Fee

  ```solidity
  function getL1Fee(bytes _data) external view returns (uint256)
  ```

  Computes the L1 portion of the fee based on the size of the rlp encoded input
        transaction, the current L1 base fee, and the various dynamic parameters.

**Parameters**
* `_data` (*bytes*) - Unsigned fully RLP-encoded transaction to get the L1 fee for.

**Returns**
* `[0]` (*uint256*) - L1 fee that should be paid for the tx
#### gasPrice

  ```solidity
  function gasPrice() external view returns (uint256)
  ```

  Retrieves the current gas price (base fee).

**Returns**
* `[0]` (*uint256*) - Current L2 gas price (base fee).
#### baseFee

  ```solidity
  function baseFee() external view returns (uint256)
  ```

  Retrieves the current base fee.

**Returns**
* `[0]` (*uint256*) - Current L2 base fee.
#### overhead

  ```solidity
  function overhead() external view returns (uint256)
  ```

  Retrieves the current fee overhead.

**Returns**
* `[0]` (*uint256*) - Current fee overhead.
#### scalar

  ```solidity
  function scalar() external view returns (uint256)
  ```

  Retrieves the current fee scalar.

**Returns**
* `[0]` (*uint256*) - Current fee scalar.
#### l1BaseFee

  ```solidity
  function l1BaseFee() external view returns (uint256)
  ```

  Retrieves the latest known L1 base fee.

**Returns**
* `[0]` (*uint256*) - Latest known L1 base fee.
#### decimals

  ```solidity
  function decimals() external pure returns (uint256)
  ```

  @custom:legacy
Retrieves the number of decimals used in the scalar.

**Returns**
* `[0]` (*uint256*) - Number of decimals used in the scalar.
#### getL1GasUsed

  ```solidity
  function getL1GasUsed(bytes _data) external view returns (uint256)
  ```

  Computes the amount of L1 gas used for a transaction. Adds the overhead which
        represents the per-transaction gas overhead of posting the transaction and state
        roots to L1. Adds 68 bytes of padding to account for the fact that the input does
        not have a signature.

**Parameters**
* `_data` (*bytes*) - Unsigned fully RLP-encoded transaction to get the L1 gas for.

**Returns**
* `[0]` (*uint256*) - Amount of L1 gas used to publish the transaction.

### IOVM_GasPriceOracle

#### DECIMALS

  ```solidity
  function DECIMALS() external pure returns (uint256)
  ```

  Number of decimals used in the scalar.

#### getL1Fee

  ```solidity
  function getL1Fee(bytes _data) external view returns (uint256)
  ```

  Computes the L1 portion of the fee based on the size of the rlp encoded input
        transaction, the current L1 base fee, and the various dynamic parameters.

**Parameters**
* `_data` (*bytes*) - Unsigned fully RLP-encoded transaction to get the L1 fee for.

**Returns**
* `[0]` (*uint256*) - L1 fee that should be paid for the tx
#### gasPrice

  ```solidity
  function gasPrice() external view returns (uint256)
  ```

  Retrieves the current gas price (base fee).

**Returns**
* `[0]` (*uint256*) - Current L2 gas price (base fee).
#### baseFee

  ```solidity
  function baseFee() external view returns (uint256)
  ```

  Retrieves the current base fee.

**Returns**
* `[0]` (*uint256*) - Current L2 base fee.
#### overhead

  ```solidity
  function overhead() external view returns (uint256)
  ```

  Retrieves the current fee overhead.
deprecated

**Returns**
* `[0]` (*uint256*) - Current fee overhead.
#### scalar

  ```solidity
  function scalar() external view returns (uint256)
  ```

  Retrieves the current fee scalar.
deprecated

**Returns**
* `[0]` (*uint256*) - Current fee scalar.
#### l1BaseFee

  ```solidity
  function l1BaseFee() external view returns (uint256)
  ```

  Retrieves the latest known L1 base fee.

**Returns**
* `[0]` (*uint256*) - Latest known L1 base fee.
#### decimals

  ```solidity
  function decimals() external pure returns (uint256)
  ```

  @custom:legacy
Retrieves the number of decimals used in the scalar.

**Returns**
* `[0]` (*uint256*) - Number of decimals used in the scalar.
#### getL1GasUsed

  ```solidity
  function getL1GasUsed(bytes _data) external view returns (uint256)
  ```

  Computes the amount of L1 gas used for a transaction. Adds the overhead which
        represents the per-transaction gas overhead of posting the transaction and state
        roots to L1. Adds 68 bytes of padding to account for the fact that the input does
        not have a signature.

**Parameters**
* `_data` (*bytes*) - Unsigned fully RLP-encoded transaction to get the L1 gas for.

**Returns**
* `[0]` (*uint256*) - Amount of L1 gas used to publish the transaction.
#### setEcotone

  ```solidity
  function setEcotone() external
  ```

  Set chain to be Ecotone chain (callable by depositor account)

#### isEcotone

  ```solidity
  function isEcotone() external view returns (bool)
  ```

  Indicates whether the network has gone through the Ecotone upgrade.

#### version

  ```solidity
  function version() external view returns (string)
  ```

  Semantic version.

#### blobBaseFee

  ```solidity
  function blobBaseFee() external view returns (uint256)
  ```

  Retrieves the current blob base fee.

**Returns**
* `[0]` (*uint256*) - Current blob base fee.
#### baseFeeScalar

  ```solidity
  function baseFeeScalar() external view returns (uint32)
  ```

  Retrieves the current base fee scalar.

**Returns**
* `[0]` (*uint32*) - Current base fee scalar.
#### blobBaseFeeScalar

  ```solidity
  function blobBaseFeeScalar() external view returns (uint32)
  ```

  Retrieves the current blob base fee scalar.

**Returns**
* `[0]` (*uint32*) - Current blob base fee scalar.

### IOVM_GasPriceOracle

#### version

  ```solidity
  function version() external pure returns (string)
  ```

#### isEcotone

  ```solidity
  function isEcotone() external view returns (bool)
  ```

#### isFjord

  ```solidity
  function isFjord() external view returns (bool)
  ```

#### DECIMALS

  ```solidity
  function DECIMALS() external pure returns (uint256)
  ```

#### getL1Fee

  ```solidity
  function getL1Fee(bytes _data) external view returns (uint256)
  ```

  Computes the L1 portion of the fee based on the size of the rlp encoded input
        transaction, the current L1 base fee, and the various dynamic parameters.

**Parameters**
* `_data` (*bytes*) - Unsigned fully RLP-encoded transaction to get the L1 fee for.

**Returns**
* `[0]` (*uint256*) - L1 fee that should be paid for the tx
#### getL1FeeUpperBound

  ```solidity
  function getL1FeeUpperBound(uint256 _unsignedTxSize) external view returns (uint256)
  ```

  returns an upper bound for the L1 fee for a given transaction size.
It is provided for callers who wish to estimate L1 transaction costs in the
write path, and is much more gas efficient than `getL1Fee`.
It assumes the worst case of fastlz upper-bound which covers %99.99 txs.

**Parameters**
* `_unsignedTxSize` (*uint256*) - Unsigned fully RLP-encoded transaction size to get the L1 fee for.

**Returns**
* `[0]` (*uint256*) - L1 estimated upper-bound fee that should be paid for the tx
#### setEcotone

  ```solidity
  function setEcotone() external
  ```

  Set chain to be Ecotone chain (callable by depositor account)

#### setFjord

  ```solidity
  function setFjord() external
  ```

  Set chain to be Fjord chain (callable by depositor account)

#### gasPrice

  ```solidity
  function gasPrice() external view returns (uint256)
  ```

  Retrieves the current gas price (base fee).

**Returns**
* `[0]` (*uint256*) - Current L2 gas price (base fee).
#### baseFee

  ```solidity
  function baseFee() external view returns (uint256)
  ```

  Retrieves the current base fee.

**Returns**
* `[0]` (*uint256*) - Current L2 base fee.
#### overhead

  ```solidity
  function overhead() external view returns (uint256)
  ```

  @custom:legacy
Retrieves the current fee overhead.

**Returns**
* `[0]` (*uint256*) - Current fee overhead.
#### scalar

  ```solidity
  function scalar() external view returns (uint256)
  ```

  @custom:legacy
Retrieves the current fee scalar.

**Returns**
* `[0]` (*uint256*) - Current fee scalar.
#### l1BaseFee

  ```solidity
  function l1BaseFee() external view returns (uint256)
  ```

  Retrieves the latest known L1 base fee.

**Returns**
* `[0]` (*uint256*) - Latest known L1 base fee.
#### blobBaseFee

  ```solidity
  function blobBaseFee() external view returns (uint256)
  ```

  Retrieves the current blob base fee.

**Returns**
* `[0]` (*uint256*) - Current blob base fee.
#### baseFeeScalar

  ```solidity
  function baseFeeScalar() external view returns (uint32)
  ```

  Retrieves the current base fee scalar.

**Returns**
* `[0]` (*uint32*) - Current base fee scalar.
#### blobBaseFeeScalar

  ```solidity
  function blobBaseFeeScalar() external view returns (uint32)
  ```

  Retrieves the current blob base fee scalar.

**Returns**
* `[0]` (*uint32*) - Current blob base fee scalar.
#### decimals

  ```solidity
  function decimals() external pure returns (uint256)
  ```

  @custom:legacy
Retrieves the number of decimals used in the scalar.

**Returns**
* `[0]` (*uint256*) - Number of decimals used in the scalar.
#### getL1GasUsed

  ```solidity
  function getL1GasUsed(bytes _data) external view returns (uint256)
  ```

  Computes the amount of L1 gas used for a transaction. Adds 68 bytes
        of padding to account for the fact that the input does not have a signature.

**Parameters**
* `_data` (*bytes*) - Unsigned fully RLP-encoded transaction to get the L1 gas for.

**Returns**
* `[0]` (*uint256*) - Amount of L1 gas used to publish the transaction.

### PythERC7412Wrapper

#### constructor

  ```solidity
  constructor(address _pythAddress) public
  ```

#### _getImplementation

  ```solidity
  function _getImplementation() internal view returns (address)
  ```

#### oracleId

  ```solidity
  function oracleId() external pure returns (bytes32)
  ```

#### getBenchmarkPrice

  ```solidity
  function getBenchmarkPrice(bytes32 priceId, uint64 requestedTime) external view returns (int256)
  ```

#### getLatestPrice

  ```solidity
  function getLatestPrice(bytes32 priceId, uint256 stalenessTolerance) external view returns (int256)
  ```

#### fulfillOracleQuery

  ```solidity
  function fulfillOracleQuery(bytes signedOffchainData) external payable
  ```

#### _isFeeRequired

  ```solidity
  function _isFeeRequired(bytes reason) private pure returns (bool)
  ```

#### _getScaledPrice

  ```solidity
  function _getScaledPrice(int64 price, int32 expo) private pure returns (int256)
  ```

  gets scaled price. Borrowed from PythNode.sol.

#### fallback

  ```solidity
  fallback() external payable
  ```

#### receive

  ```solidity
  receive() external payable
  ```

#### _forward

  ```solidity
  function _forward() internal
  ```

#### _getImplementation

  ```solidity
  function _getImplementation() internal view virtual returns (address)
  ```

#### oracleId

  ```solidity
  function oracleId() external view returns (bytes32 oracleId)
  ```

#### fulfillOracleQuery

  ```solidity
  function fulfillOracleQuery(bytes signedOffchainData) external payable
  ```

### IERC7412

#### oracleId

  ```solidity
  function oracleId() external view returns (bytes32 oracleId)
  ```

#### fulfillOracleQuery

  ```solidity
  function fulfillOracleQuery(bytes signedOffchainData) external payable
  ```

### SpotMarketOracle

#### constructor

  ```solidity
  constructor(address _spotMarketAddress) public
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[], bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data nodeOutput)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external view returns (bool valid)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) external pure returns (bool)
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external returns (bool)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### ISpotMarketSystem

#### setSynthetix

  ```solidity
  function setSynthetix(contract ISynthetixSystem synthetix) external
  ```

  Sets the v3 synthetix core system.

  Pulls in the USDToken and oracle manager from the synthetix core system and sets those appropriately.

**Parameters**
* `synthetix` (*contract ISynthetixSystem*) - synthetix v3 core system address

#### setSynthImplementation

  ```solidity
  function setSynthImplementation(address synthImplementation) external
  ```

  When a new synth is created, this is the erc20 implementation that is used.

**Parameters**
* `synthImplementation` (*address*) - erc20 implementation address

#### createSynth

  ```solidity
  function createSynth(string tokenName, string tokenSymbol, address synthOwner) external returns (uint128 synthMarketId)
  ```

  Creates a new synth market with synthetix v3 core system via market manager

  The synth is created using the initial synth implementation and creates a proxy for future upgrades of the synth implementation.
Sets up the market owner who can update configuration for the synth.

**Parameters**
* `tokenName` (*string*) - name of synth (i.e Synthetix ETH)
* `tokenSymbol` (*string*) - symbol of synth (i.e snxETH)
* `synthOwner` (*address*) - owner of the market that's created.

**Returns**
* `synthMarketId` (*uint128*) - id of the synth market that was created
#### getSynth

  ```solidity
  function getSynth(uint128 marketId) external view returns (address synthAddress)
  ```

  Get the proxy address of the synth for the provided marketId

  Uses associated systems module to retrieve the token address.

**Parameters**
* `marketId` (*uint128*) - id of the market

**Returns**
* `synthAddress` (*address*) - address of the proxy for the synth
#### getSynthImpl

  ```solidity
  function getSynthImpl(uint128 marketId) external view returns (address implAddress)
  ```

  Get the implementation address of the synth for the provided marketId.
This address should not be used directly--use `getSynth` instead

  Uses associated systems module to retrieve the token address.

**Parameters**
* `marketId` (*uint128*) - id of the market

**Returns**
* `implAddress` (*address*) - address of the proxy for the synth
#### updatePriceData

  ```solidity
  function updatePriceData(uint128 marketId, bytes32 buyFeedId, bytes32 sellFeedId, uint256 strictPriceStalenessTolerance) external
  ```

  Update the price data for a given market.

  Only the market owner can call this function.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `buyFeedId` (*bytes32*) - the oracle manager buy feed node id
* `sellFeedId` (*bytes32*) - the oracle manager sell feed node id
* `strictPriceStalenessTolerance` (*uint256*) - configurable price staleness tolerance used for transacting

#### getPriceData

  ```solidity
  function getPriceData(uint128 marketId) external view returns (bytes32 buyFeedId, bytes32 sellFeedId, uint256 strictPriceStalenessTolerance)
  ```

  Gets the price data for a given market.

  Only the market owner can call this function.

**Parameters**
* `marketId` (*uint128*) - id of the market

**Returns**
* `buyFeedId` (*bytes32*) - the oracle manager buy feed node id
* `sellFeedId` (*bytes32*) - the oracle manager sell feed node id
* `strictPriceStalenessTolerance` (*uint256*) - configurable price staleness tolerance used for transacting
#### upgradeSynthImpl

  ```solidity
  function upgradeSynthImpl(uint128 marketId) external
  ```

  upgrades the synth implementation to the current implementation for the specified market.
Anyone who is willing and able to spend the gas can call this method.

  The synth implementation is upgraded via the proxy.

**Parameters**
* `marketId` (*uint128*) - id of the market

#### setDecayRate

  ```solidity
  function setDecayRate(uint128 marketId, uint256 rate) external
  ```

  Allows market to adjust decay rate of the synth

**Parameters**
* `marketId` (*uint128*) - the market to update the synth decay rate for
* `rate` (*uint256*) - APY to decay of the synth to decay by, as a 18 decimal ratio

#### nominateMarketOwner

  ```solidity
  function nominateMarketOwner(uint128 synthMarketId, address newNominatedOwner) external
  ```

  Allows the current market owner to nominate a new owner.

  The nominated owner will have to call `acceptOwnership` in a separate transaction in order to finalize the action and become the new contract owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value
* `newNominatedOwner` (*address*) - The address that is to become nominated.

#### acceptMarketOwnership

  ```solidity
  function acceptMarketOwnership(uint128 synthMarketId) external
  ```

  Allows a nominated address to accept ownership of the market.

  Reverts if the caller is not nominated.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### renounceMarketNomination

  ```solidity
  function renounceMarketNomination(uint128 synthMarketId) external
  ```

  Allows a nominated address to renounce ownership of the market.

  Reverts if the caller is not nominated.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### renounceMarketOwnership

  ```solidity
  function renounceMarketOwnership(uint128 synthMarketId) external
  ```

  Allows the market owner to renounce his ownership.

  Reverts if the caller is not the owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### getMarketOwner

  ```solidity
  function getMarketOwner(uint128 synthMarketId) external view returns (address)
  ```

  Returns market owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### getNominatedMarketOwner

  ```solidity
  function getNominatedMarketOwner(uint128 synthMarketId) external view returns (address)
  ```

  Returns nominated market owner.

**Parameters**
* `synthMarketId` (*uint128*) - synth market id value

#### indexPrice

  ```solidity
  function indexPrice(uint128 marketId, uint128 transactionType, enum Price.Tolerance priceTolerance) external view returns (uint256 price)
  ```

  Get current price based on type of transaction and tolerance

**Parameters**
* `marketId` (*uint128*) - synth market id value
* `transactionType` (*uint128*) - type of txn
* `priceTolerance` (*enum Price.Tolerance*) - staleness tolerance to use for price

**Returns**
* `price` (*uint256*) - current price of the synth
#### name

  ```solidity
  function name(uint128 marketId) external view returns (string)
  ```

  returns a human-readable name for a given market

#### reportedDebt

  ```solidity
  function reportedDebt(uint128 marketId) external view returns (uint256)
  ```

  returns amount of USD that the market would try to mint if everything was withdrawn

#### minimumCredit

  ```solidity
  function minimumCredit(uint128 marketId) external view returns (uint256)
  ```

  prevents reduction of available credit capacity by specifying this amount, for which withdrawals will be disallowed

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.
#### buyExactIn

  ```solidity
  function buyExactIn(uint128 synthMarketId, uint256 amountUsd, uint256 minAmountReceived, address referrer) external returns (uint256 synthAmount, struct OrderFees.Data fees)
  ```

  Initiates a buy trade returning synth for the specified amountUsd.

  Transfers the specified amountUsd, collects fees through configured fee collector, returns synth to the trader.
Leftover fees not collected get deposited into the market manager to improve market PnL.
Uses the buyFeedId configured for the market.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market used for the trade.
* `amountUsd` (*uint256*) - Amount of snxUSD trader is providing allowance for the trade.
* `minAmountReceived` (*uint256*) - Min Amount of synth is expected the trader to receive otherwise the transaction will revert.
* `referrer` (*address*) - Optional address of the referrer, for fee share

**Returns**
* `synthAmount` (*uint256*) - Synth received on the trade based on amount provided by trader.
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
#### buy

  ```solidity
  function buy(uint128 marketId, uint256 usdAmount, uint256 minAmountReceived, address referrer) external returns (uint256 synthAmount, struct OrderFees.Data fees)
  ```

  alias for buyExactIn

**Parameters**
* `marketId` (*uint128*) - (see buyExactIn)
* `usdAmount` (*uint256*) - (see buyExactIn)
* `minAmountReceived` (*uint256*) - (see buyExactIn)
* `referrer` (*address*) - (see buyExactIn)

**Returns**
* `synthAmount` (*uint256*) - (see buyExactIn)
* `fees` (*struct OrderFees.Data*) - (see buyExactIn)
#### buyExactOut

  ```solidity
  function buyExactOut(uint128 synthMarketId, uint256 synthAmount, uint256 maxUsdAmount, address referrer) external returns (uint256 usdAmountCharged, struct OrderFees.Data fees)
  ```

  user provides the synth amount they'd like to buy, and the function charges the USD amount which includes fees

  the inverse of buyExactIn

**Parameters**
* `synthMarketId` (*uint128*) - market id value
* `synthAmount` (*uint256*) - the amount of synth the trader wants to buy
* `maxUsdAmount` (*uint256*) - max amount the trader is willing to pay for the specified synth
* `referrer` (*address*) - optional address of the referrer, for fee share

**Returns**
* `usdAmountCharged` (*uint256*) - amount of USD charged for the trade
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction
#### quoteBuyExactIn

  ```solidity
  function quoteBuyExactIn(uint128 synthMarketId, uint256 usdAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 synthAmount, struct OrderFees.Data fees)
  ```

  quote for buyExactIn.  same parameters and return values as buyExactIn

**Parameters**
* `synthMarketId` (*uint128*) - market id value
* `usdAmount` (*uint256*) - amount of USD to use for the trade
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `synthAmount` (*uint256*) - return amount of synth given the USD amount - fees
* `fees` (*struct OrderFees.Data*) - breakdown of all the quoted fees for the buy txn
#### quoteBuyExactOut

  ```solidity
  function quoteBuyExactOut(uint128 synthMarketId, uint256 synthAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 usdAmountCharged, struct OrderFees.Data)
  ```

  quote for buyExactOut.  same parameters and return values as buyExactOut

**Parameters**
* `synthMarketId` (*uint128*) - market id value
* `synthAmount` (*uint256*) - amount of synth requested
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `usdAmountCharged` (*uint256*) - USD amount charged for the synth requested - fees
* `[1]` (*struct OrderFees.Data*) - fees  breakdown of all the quoted fees for the buy txn
#### sellExactIn

  ```solidity
  function sellExactIn(uint128 synthMarketId, uint256 sellAmount, uint256 minAmountReceived, address referrer) external returns (uint256 returnAmount, struct OrderFees.Data fees)
  ```

  Initiates a sell trade returning snxUSD for the specified amount of synth (sellAmount)

  Transfers the specified synth, collects fees through configured fee collector, returns snxUSD to the trader.
Leftover fees not collected get deposited into the market manager to improve market PnL.

**Parameters**
* `synthMarketId` (*uint128*) - Id of the market used for the trade.
* `sellAmount` (*uint256*) - Amount of synth provided by trader for trade into snxUSD.
* `minAmountReceived` (*uint256*) - Min Amount of snxUSD trader expects to receive for the trade
* `referrer` (*address*) - Optional address of the referrer, for fee share

**Returns**
* `returnAmount` (*uint256*) - Amount of snxUSD returned to user
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction.
#### sellExactOut

  ```solidity
  function sellExactOut(uint128 marketId, uint256 usdAmount, uint256 maxSynthAmount, address referrer) external returns (uint256 synthToBurn, struct OrderFees.Data fees)
  ```

  initiates a trade where trader specifies USD amount they'd like to receive

  the inverse of sellExactIn

**Parameters**
* `marketId` (*uint128*) - synth market id
* `usdAmount` (*uint256*) - amount of USD trader wants to receive
* `maxSynthAmount` (*uint256*) - max amount of synth trader is willing to use to receive the specified USD amount
* `referrer` (*address*) - optional address of the referrer, for fee share

**Returns**
* `synthToBurn` (*uint256*) - amount of synth charged for the specified usd amount
* `fees` (*struct OrderFees.Data*) - breakdown of all the fees incurred for the transaction
#### sell

  ```solidity
  function sell(uint128 marketId, uint256 synthAmount, uint256 minUsdAmount, address referrer) external returns (uint256 usdAmountReceived, struct OrderFees.Data fees)
  ```

  alias for sellExactIn

**Parameters**
* `marketId` (*uint128*) - (see sellExactIn)
* `synthAmount` (*uint256*) - (see sellExactIn)
* `minUsdAmount` (*uint256*) - (see sellExactIn)
* `referrer` (*address*) - (see sellExactIn)

**Returns**
* `usdAmountReceived` (*uint256*) - (see sellExactIn)
* `fees` (*struct OrderFees.Data*) - (see sellExactIn)
#### quoteSellExactIn

  ```solidity
  function quoteSellExactIn(uint128 marketId, uint256 synthAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 returnAmount, struct OrderFees.Data fees)
  ```

  quote for sellExactIn

  returns expected USD amount trader would receive for the specified synth amount

**Parameters**
* `marketId` (*uint128*) - synth market id
* `synthAmount` (*uint256*) - synth amount trader is providing for the trade
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `returnAmount` (*uint256*) - amount of USD expected back
* `fees` (*struct OrderFees.Data*) - breakdown of all the quoted fees for the txn
#### quoteSellExactOut

  ```solidity
  function quoteSellExactOut(uint128 marketId, uint256 usdAmount, enum Price.Tolerance stalenessTolerance) external view returns (uint256 synthToBurn, struct OrderFees.Data fees)
  ```

  quote for sellExactOut

  returns expected synth amount expected from trader for the requested USD amount

**Parameters**
* `marketId` (*uint128*) - synth market id
* `usdAmount` (*uint256*) - USD amount trader wants to receive
* `stalenessTolerance` (*enum Price.Tolerance*) - this enum determines what staleness tolerance to use

**Returns**
* `synthToBurn` (*uint256*) - amount of synth expected from trader
* `fees` (*struct OrderFees.Data*) - breakdown of all the quoted fees for the txn
#### getMarketSkew

  ```solidity
  function getMarketSkew(uint128 marketId) external view returns (int256 marketSkew)
  ```

  gets the current market skew

**Parameters**
* `marketId` (*uint128*) - synth market id

**Returns**
* `marketSkew` (*int256*) - the skew

#### SynthetixSystemSet

  ```solidity
  event SynthetixSystemSet(address synthetix, address usdTokenAddress, address oracleManager)
  ```

  Gets fired when the synthetix is set

**Parameters**
* `synthetix` (*address*) - address of the synthetix core contract
* `usdTokenAddress` (*address*) - address of the USDToken contract
* `oracleManager` (*address*) - address of the Oracle Manager contract

#### SynthImplementationSet

  ```solidity
  event SynthImplementationSet(address synthImplementation)
  ```

  Gets fired when the synth implementation is set

**Parameters**
* `synthImplementation` (*address*) - address of the synth implementation

#### SynthRegistered

  ```solidity
  event SynthRegistered(uint256 synthMarketId, address synthTokenAddress)
  ```

  Gets fired when the synth is registered as a market.

**Parameters**
* `synthMarketId` (*uint256*) - Id of the synth market that was created
* `synthTokenAddress` (*address*) - address of the newly created synth token

#### SynthImplementationUpgraded

  ```solidity
  event SynthImplementationUpgraded(uint256 synthMarketId, address proxy, address implementation)
  ```

  Gets fired when the synth's implementation is updated on the corresponding proxy.

**Parameters**
* `synthMarketId` (*uint256*) - 
* `proxy` (*address*) - the synth proxy servicing the latest implementation
* `implementation` (*address*) - the latest implementation of the synth

#### SynthPriceDataUpdated

  ```solidity
  event SynthPriceDataUpdated(uint256 synthMarketId, bytes32 buyFeedId, bytes32 sellFeedId, uint256 strictStalenessTolerance)
  ```

  Gets fired when the market's price feeds are updated, compatible with oracle manager

**Parameters**
* `synthMarketId` (*uint256*) - 
* `buyFeedId` (*bytes32*) - the oracle manager feed id for the buy price
* `sellFeedId` (*bytes32*) - the oracle manager feed id for the sell price
* `strictStalenessTolerance` (*uint256*) - 

#### DecayRateUpdated

  ```solidity
  event DecayRateUpdated(uint128 marketId, uint256 rate)
  ```

  Gets fired when the market's price feeds are updated, compatible with oracle manager

**Parameters**
* `marketId` (*uint128*) - Id of the synth market
* `rate` (*uint256*) - the new decay rate (1e16 means 1% decay per year)

#### MarketOwnerNominated

  ```solidity
  event MarketOwnerNominated(uint128 marketId, address newOwner)
  ```

  Emitted when an address has been nominated.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `newOwner` (*address*) - The address that has been nominated.

#### MarketNominationRenounced

  ```solidity
  event MarketNominationRenounced(uint128 marketId, address nominee)
  ```

  Emitted when market nominee renounces nomination.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `nominee` (*address*) - The address that has been nominated.

#### MarketOwnerChanged

  ```solidity
  event MarketOwnerChanged(uint128 marketId, address oldOwner, address newOwner)
  ```

  Emitted when the owner of the market has changed.

**Parameters**
* `marketId` (*uint128*) - id of the market
* `oldOwner` (*address*) - The previous owner of the market.
* `newOwner` (*address*) - The new owner of the market.

#### SynthBought

  ```solidity
  event SynthBought(uint256 synthMarketId, uint256 synthReturned, struct OrderFees.Data fees, uint256 collectedFees, address referrer, uint256 price)
  ```

  Gets fired when buy trade is complete

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market used for the trade.
* `synthReturned` (*uint256*) - Synth received on the trade based on amount provided by trader.
* `fees` (*struct OrderFees.Data*) - breakdown of all fees incurred for transaction.
* `collectedFees` (*uint256*) - Fees collected by the configured FeeCollector for the market (rest of the fees are deposited to market manager).
* `referrer` (*address*) - Optional address of the referrer, for fee share
* `price` (*uint256*) - 

#### SynthSold

  ```solidity
  event SynthSold(uint256 synthMarketId, uint256 amountReturned, struct OrderFees.Data fees, uint256 collectedFees, address referrer, uint256 price)
  ```

  Gets fired when sell trade is complete

**Parameters**
* `synthMarketId` (*uint256*) - Id of the market used for the trade.
* `amountReturned` (*uint256*) - Amount of snxUSD returned to user based on synth provided by trader.
* `fees` (*struct OrderFees.Data*) - breakdown of all fees incurred for transaction.
* `collectedFees` (*uint256*) - Fees collected by the configured FeeCollector for the market (rest of the fees are deposited to market manager).
* `referrer` (*address*) - Optional address of the referrer, for fee share
* `price` (*uint256*) - 

### WstEthToStEthRatioOracle

#### constructor

  ```solidity
  constructor(address _lidoWstEthAddress) public
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[], bytes, bytes32[], bytes32[]) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external view returns (bool valid)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceId) external pure returns (bool)
  ```

#### process

  ```solidity
  function process(struct NodeOutput.Data[] parentNodeOutputs, bytes parameters, bytes32[] runtimeKeys, bytes32[] runtimeValues) external view returns (struct NodeOutput.Data)
  ```

#### isValid

  ```solidity
  function isValid(struct NodeDefinition.Data nodeDefinition) external returns (bool)
  ```

#### supportsInterface

  ```solidity
  function supportsInterface(bytes4 interfaceID) external view returns (bool)
  ```

  Determines if the contract in question supports the specified interface.

**Parameters**
* `interfaceID` (*bytes4*) - XOR of all selectors in the contract.

**Returns**
* `[0]` (*bool*) - True if the contract supports the specified interface.

### IWstETH

#### getStETHByWstETH

  ```solidity
  function getStETHByWstETH(uint256 _wstETHAmount) external view returns (uint256)
  ```

  Get amount of stETH for a given amount of wstETH

**Parameters**
* `_wstETHAmount` (*uint256*) - amount of wstETH

**Returns**
* `[0]` (*uint256*) - Amount of stETH for a given wstETH amount

