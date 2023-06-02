# Import Ethers

```
 import { ethers } from "ethers";
```

# Providers

Provides read-only access to the Blockchain and its status.

## Infura Provider

```
// Networks: homestead(Mainnet), sepolia, goerli
const NETWORK = "homestead";
const APIKEY = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX";
const provider = new ethers.InfuraProvider(NETWORK, APIKEY);
```

## JsonRpcProvider

```
const rpcEndpoint = "http://127.0.0.1:8545/"; // Local hardhat node rpc endpoint
const provider = new ethers.JsonRpcProvider(rpcEndpoint);
```

## Web3Provider / BrowserProvider

Connects to Network used by wallet like Metamask or Core

*Request Permission to connected to user accounts*

```
await provider.request({method:"eth_requestAccounts"});
```

```
// Web3Provider
// const provider = new ethers.providers.Web3Provider(window.ethereum);

// BrowserProvider
const provider = new ethers.BrowserProvider(window.ethereum);
```

## Get Block Number

```
const blockNumber = await provider.getBlockNumber();
console.log("BlockNumber:", blockNumber);
```
### Output:
`
BlockNumber: 17390540
`

## Get Block Information
```
const block = await provider.getBlock(blockNumber);
console.log(block);
```
### Output
```
Block {
  provider: InfuraProvider {
    projectId: '171ecb351bb048379b9042a835fb20ad',
    projectSecret: null
  },
  number: 17390540,
  hash: '0xf9bf4a263175e34b0626619c38ae18c6f25c1536bc7afb803a718926a48793f7',
  timestamp: 1685678243,
  parentHash: '0x7df1b4bc43518c838214bbbe1a43d9ade7b1895327606f9e3eb4816966e4254a',
  nonce: '0x0000000000000000',
  difficulty: 0n,
  gasLimit: 30000000n,
  gasUsed: 29981559n,
  miner: '0x95222290DD7278Aa3Ddd389Cc1E1d165CC4BAfe5',
  extraData: '0x6265617665726275696c642e6f7267',
  baseFeePerGas: 27847313757n
}
```
# Signer

A Signer is a class which (usually) in some way directly or indirectly has access to a private key, which can sign messages and transactions to authorize the network to charge your account ether to perform operations.

In a nutshell, Signer allow us to write to blockchain / make changes to blockchain by creating transaction, etc.

```
const signer = await provider.getSigner();
```

## Get Signer Address

```
const address = signer.getAddress();
```
