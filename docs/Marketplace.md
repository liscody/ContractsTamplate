# Solidity API

## Marketplace

Will contains all the business logic sale and purchase of tokens.

_uses ReentrancyGuard for security_

### nftContract

```solidity
address nftContract
```

ERC721 contract address

### platformFeeInBNB

```solidity
uint256 platformFeeInBNB
```

platform fee for BNB in percentage (using 2 decimals: 10000 = 100)

### platformFeeInGWG

```solidity
uint256 platformFeeInGWG
```

platform fee for GWGin percentage (using 2 decimals: 10000 = 100)

### feeDestination

```solidity
address payable feeDestination
```

fee destination contract address

### MarketItem

```solidity
struct MarketItem {
  uint256 price;
  address currency;
  bool forSale;
}
```

### idToMarketItem

```solidity
mapping(uint256 => struct Marketplace.MarketItem) idToMarketItem
```

Mapping from token ID to Market Item

### tokenOwner

```solidity
mapping(uint256 => address) tokenOwner
```

Mapping from token ID to token owner address

### approvedTokens

```solidity
mapping(address => bool) approvedTokens
```

Mapping from ERC20 address to approved tokens

### BNBFeeChanged

```solidity
event BNBFeeChanged(address account, uint256 newFee, uint256 oldFee)
```

### GWGFeeChanged

```solidity
event GWGFeeChanged(address account, uint256 newFee, uint256 oldFee)
```

### TokenOnSale

```solidity
event TokenOnSale(address owner, uint256 tokenId, uint256 price, address currency)
```

### SalePriceChanged

```solidity
event SalePriceChanged(uint256 tokenId, uint256 price)
```

### TokenNotOnSale

```solidity
event TokenNotOnSale(uint256 tokenId)
```

### TokenBought

```solidity
event TokenBought(uint256 tokenId, address buyer, address currency, uint256 price, uint256 fee, uint256 royalty)
```

### onlyTokenOwner

```solidity
modifier onlyTokenOwner(uint256 tokenId)
```

_Allows only tokens that belong to the owner_

### onlyNonContracts

```solidity
modifier onlyNonContracts()
```

_Allows only for Externally-owned accounts (EOAs)_

### constructor

```solidity
constructor(address _nft, address _token, address payable _feeDestination, uint256 _feeBNB, uint256 _feeGWG) public
```

_Initializes the contract_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _nft | address | ERC721 contract address |
| _token | address | allowed token contract address |
| _feeDestination | address payable | fee destination contract address |
| _feeBNB | uint256 | initial platform fee in BNB |
| _feeGWG | uint256 | initial platform fee in GWG |

### updateAssetAddress

```solidity
function updateAssetAddress(address nft) public
```

update new asset address

_Caller must be contract owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| nft | address | ERC721 contract address |

### updateFee

```solidity
function updateFee(uint256 feeGWG, uint256 feeBNB) public
```

update platform fee

_Caller must be contract owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| feeGWG | uint256 | platform fee for GWG in percentage (using 2 decimals: 10000 = 100) |
| feeBNB | uint256 | platform fee for BNB in percentage (using 2 decimals: 10000 = 100) |

### updateFeeDestination

```solidity
function updateFeeDestination(address payable _feeDestination) public
```

update fee destination

_Caller must be contract owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _feeDestination | address payable | fee destination contract address |

### addApprovedToken

```solidity
function addApprovedToken(address _contractAddress) external
```

Adds an approved contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _contractAddress | address | the address of the contract to be added |

### deleteApprovedToken

```solidity
function deleteApprovedToken(address _contractAddress) external
```

Delete an approved contract

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| _contractAddress | address | the address of the contract to be deleted |

### putTokenForSale

```solidity
function putTokenForSale(uint256 tokenId, uint256 price, address currency) public
```

put NFT for sale

_lock NFT on marketplace contract_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenId | uint256 | the NFT identifier |
| price | uint256 | set NFT price |
| currency | address | set NFT currency address |

### updateTokenPrice

```solidity
function updateTokenPrice(uint256 tokenId, uint256 _price) public
```

update token price

_caller must be token owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenId | uint256 | the NFT identifier |
| _price | uint256 | set new price |

### removeTokenFromSale

```solidity
function removeTokenFromSale(uint256 tokenId) public
```

remove token from sale

_caller must be token owner. Unlock NFT from the marketplace_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenId | uint256 | the NFT identifier |

### buyToken

```solidity
function buyToken(uint256 tokenId) public payable
```

function to buy token

_can buy for allowed ERC20 or native currency. Send fee and royalty_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenId | uint256 | the NFT identifier |

### onERC721Received

```solidity
function onERC721Received(address, address, uint256, bytes) public virtual returns (bytes4)
```

_Whenever an {IERC721} `tokenId` token is transferred to this
contract via {IERC721-safeTransferFrom} by `operator` from `from`,
this function is called_

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| [0] | bytes4 | its Solidity selector to confirm the token transfer. |

### recoverTokens

```solidity
function recoverTokens(address tokenAddress, uint256 tokenAmount) external
```

It allows the admins to get tokens sent to the contract

_Only callable by owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenAddress | address |  |
| tokenAmount | uint256 |  |

### withdraw

```solidity
function withdraw() external
```

It allows the admins to get collected coins

_Only callable by owner_

### recoverAsset

```solidity
function recoverAsset(address tokenAddress, uint256 tokenId) external
```

It allows the admins to get NFT sent to the contract, if there will be any issue with contract

_Only callable by owner_

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| tokenAddress | address |  |
| tokenId | uint256 | to withdraw |

