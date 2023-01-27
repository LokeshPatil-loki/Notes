[ABI]: ## "This contains schema of our smart contract, it represents all the events, functions, public variable smart contract expose"
# Prerequisits
1. Deploy a contract on a Test Network
2. Copy **[ABI]** from Remix IDE
3. Inside react clients **src** directory. Create **abi.json**
4. Paste ABI code inside **abi.json**
5. Install ethers package as dependency for react client <br>
```npm install ethers```

# Steps
### Required imports
  ```
  import {ethers} from "ethers"
  import abi from "./abi.json
  ```

### Create a Provider <br>
```
const provider = new ethers.providers.Web3Provider(window.etherium);
```

### Create a instance of a contract <br>
  ```
  const contractAddress = "xxxxxxxxxxxxxxxxxxxxxxxxx";
  const contract = new ethers.Contract(contractAddress, abi, provider);
  ```

### Access a function that our smart contract provides<br>
  ```
  await contract.functionName()
  ```

### Get currently logged in user as signer
  ```
  await provider.send("eth_requestAccounts",[]);
  const signer = await provider.getSigner();
  ```
### Get address of logged in user (signer)
  ```
  const signerAddress = await signer.getAddress();
  ```
### Get balance of logged in user (Signer)
  ```
  const balance = await contract.balanceOf(signerAddress);
  ```
### Listen for events
  ```
  contract.on("EventName",(attr1,attr2,attrN) => {
    // Do something
  })
  ```