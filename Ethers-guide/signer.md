# Signer

A Signer is a class which (usually) in some way directly or indirectly has access to a private key, which can sign messages and transactions to authorize the network to charge your account ether to perform operations.

In a nutshell, Signer allow us to write to blockchain / make changes to blockchain by creating transaction, etc.

```
const signer = await provider.getSigner();
```
we are using BrowserProvider here

## Get Signer Address

```
const address = signer.getAddress();
```
