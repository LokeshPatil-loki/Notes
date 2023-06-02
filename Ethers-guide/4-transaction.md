# Transactions

## Send Transaction

1. Get Access To Provider.
2. Get Access To Signer.
3. Send Transaction using Signer.

_Get Access To Provider_

```
const provider = new ethers.BrowserProvider(window.ethereum);
```

_Get Access To Signer_

```
const signer = await provider.getSigner();
```

_Define transcation_

```
const value = 0.0001;
const tx = {
    to: "0x3408a4AF573F550CF9ceBd37a4eB4562AbfE3d43",
    value: window.ethers.parseEthers(value.toString())
}
```

_Estimate gas for transaction_

```
const estimatedGas = await provider.esitmateGas(tx);
```

_Send Transaction using Signer_

```
const txResult = await signer.sendTransaction(tx);
```

_Wait For Transaction to be completed to get Transaction Recipet_

```
const txReciept = await provider.waitForTransaction(txResult.hash);
```
