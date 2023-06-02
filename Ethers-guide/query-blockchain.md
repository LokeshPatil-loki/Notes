# Prerequisite

- Need access to some provider. Here i am using Infura Provider

# Get Balance of Any Account

```
// Get balance of any etherium account
const address = "0x2b435f60Fb9EA9dFBA1040779207c5AFB6Cf2E19";

const balance = await provider.getBalance(addressOfRandomAccount);
console.log(balance);
```

### Output

`6034034284943745n`

Well this balance is given in WEI.

## Convert Wei to Ether

```
const ethBalance = ethers.formatEther(balance);
console.log(ethBalance, "ETH");
```

### Output

`0.005191908708391125 ETH`

## Convert Ether to Wei

```
const weiBalance = ethers.parseUnits(ethBalance, "ether");
console.log(weiBalance, "WEI");
```

### Output

`5191908708391125n WEI`
