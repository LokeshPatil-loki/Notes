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
```
// Web3Provider
// const provider = new ethers.providers.Web3Provider(window.ethereum);

// BrowserProvider
const provider = new ethers.BrowserProvider(window.ethereum);
```
# Signer
A Signer is a class which (usually) in some way directly or indirectly has access to a private key, which can sign messages and transactions to authorize the network to charge your account ether to perform operations.

In a nutshell, Signer allow us to write to blockchain / make changes to blockchain by creating transaction, etc.
```
const signer = await provider.getSigner();

```
