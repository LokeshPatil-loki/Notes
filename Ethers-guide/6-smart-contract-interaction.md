# Interacting with Smart Contracts

## Prerequisite

- Access to _Provider_
- Access to _Signer_
- Contract Address
- Contract ABI

## ABI

- ABIs are application binary interfaces.
- They define the methods and variables that are available in a smart contract and which we can use to interact with that smart contract.

## _Define contract_

```
const contractAddress = "0x6B175474E89094C44Da98b954EedeAC495271d0F";
```

## _Define ABI_

```
const abi = [

    // Some details about the token

    "function name() view returns (string)",
    "function symbol() view returns (string)",

    /// Get the account balance
    "function balanceOf(address) view returns (uint)",

    // Send some of your tokens to someone else
    "function transfer(address to, uint amount)",

    // An event triggered whenever anyone transfers to someone else
    "event Transfer (address indexed from, address indexed to, uint amount)"
]
```

# Reading from Smart Contract

## _Create provider_

```
const provider = new ethers.BrowserProvider(window.ethereum);
```

## _Create contract Object_

```
const contract = new ethers.Contract(contractAddress, abi, provider);
```

Now we can use this contract object to read data from smart contract.

Let's call function defined in Contract ABI read data from contract

## _Read name of Contract_

```
const name = await contract.name();
console.log(name);
```

Output: </br> `Dai Stablecoin`

## _Read Symbol_

```
const symbol = await contract.symbol();
console.log(symbol);
```

Output: </br> `DAI`

## _Get DAI Token Balance of an Account_

```
const balance = await contract.balanceOf("0xa55a05324732419df0880a65cb086764bd953f41");
console.log(ethers.formatUnits(balance, 18));
```

DAI has 18 number of decimal places for each token<br><br>
Output: </br>
`912.0`

# Write to Smart Contract

For writing to contract Signer is used

## _Create provider_

```
const provider = new ethers.BrowserProvider(window.ethereum);
```

## _Create provider_

```
const signer = await provider.getSigner();
```

## _Create contract Object_

```
const contract = new ethers.Contract(contractAddress, abi, signer);
```

Now we can use this contract object to write data to smart contract.

## _Call Transfer_

```
const address = "0x3660C697EfdB9E8594470733059141f951Df7450";
const value = 3;

const tx = await contract.transfer(address,value);
```

## _Call functions which are marked payable_

Sending eth to paybale functions

Support signture of payble function is:
</br>
`function store(string message) external payable`

_Calling store_

```
let message = "Interesting Stuff";
let options = {value: ethers.parseEther("0.00403")};
await contract.store(message, options)

```

## _Listen for contract events_

```
let event = "Transfer";
let callback = (from, to, amount) => {
    console.log(from, to, amount);
}
contract.on(event,callback);
```
