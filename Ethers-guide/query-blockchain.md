# Prerequisite

- Need access to some provider. Here i am using Infura Provider

<details>

<summary>

# Get Balance of Any Account

</summary>

```
// Get balance of any etherium account
const address = "0x2b435f60Fb9EA9dFBA1040779207c5AFB6Cf2E19";

const balance = await provider.getBalance(addressOfRandomAccount);
console.log(balance);
```

Output

`6034034284943745n`

Well this balance is given in WEI.

## Convert Wei to Ether

```
const ethBalance = ethers.formatEther(balance);
console.log(ethBalance, "ETH");
```

Output

`0.005191908708391125 ETH`

## Convert Ether to Wei

```
const weiBalance = ethers.parseUnits(ethBalance, "ether");
console.log(weiBalance, "WEI");
```

Output

`5191908708391125n WEI`

</details>

<details>

<summary>

# Get Block Information

</summary>

## Current Block Number

```
const blockNumber = await provider.getBlockNumber();
console.log(blockNumber);
```

Output

`17391287`

## Block Information

Pass any valid blockNumber

```
const block = await provider.getBlock(blockNumber);
console.log(block);
```

<details>
<summary>Output</summary>

```
Block {
  provider: InfuraProvider {
    projectId: '171ecb351bb048379b9042a835fb20ad',
    projectSecret: null
  },
  number: 17391303,
  hash: '0x45775f7596b68544491a017b5163e4c7056d37c7fddd43f35972b3b9bfc79b2b',
  timestamp: 1685687543,
  parentHash: '0x350e4a2bb5d86ded37fcbab02150cf65ec312d44cac599791df3a71bbb183e41',
  nonce: '0x0000000000000000',
  difficulty: 0n,
  gasLimit: 30000000n,
  gasUsed: 10334495n,
  miner: '0x0035Fc5208eF989c28d47e552E92b0C507D2B318',
  extraData: '0x',
  baseFeePerGas: 27766033178n
}
```

</details>

## Get Transcation hashes from that block

```
const txHashListOfBlock = block.transactions;
console.log(txHashListOfBlock);
```

<details>

<summary>Output</summary>

```
[
  '0x7aeee1904781768984c88ea0b5f299be48bcde9545ac13d20c406dec8937bbb0',
  '0x1ebdef32127b56be6ca76816ce462998165c0ace90e66f58f3378dce12034f7f',
  '0xe5dcbef54cbd706496530f8c6b4099d3ef3ca3e56e31ba3173c11819cc039eb8',
  '0xa4aecf01d80a893602bceca5774355541425215e622ec25290ed9151fb83f772',
  ... 150 more items
]
```

</details>

## Get Detailed Transaction for selected transaction hash

```
const selectedTxHash = txHashListOfBlock[0];
const transaction = await block.getTransaction(selectedTxHash);
console.log(transaction);
```

<details>
<summary>Output</summary>

```
TransactionResponse {
  provider: InfuraProvider {
    projectId: '171ecb351bb048379b9042a835fb20ad',
    projectSecret: null
  },
  blockNumber: 17391407,
  blockHash: '0x5b62796581efc04e64d666d19954e5959c2b36d8a9917121820d688f56e71e9a',
  index: undefined,
  hash: '0xe46cf69bfed73d113aaea6eb04258175a49cb85f0cef9c8ecd223ec3daa87a9c',
  type: 2,
  to: '0xEf1c6E67703c7BD7107eed8303Fbe6EC2554BF6B',
  from: '0x17314050828F8FE66D00DC703977563320694C6d',
  nonce: 53,
  gasLimit: 241585n,
  gasPrice: 37141495041n,
  maxPriorityFeePerGas: 100000000n,
  maxFeePerGas: 45206215195n,
  data: '0x3593564c000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000647998d300000000000000000000000000000000000000000000000000000000000000030a080c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001e000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000160000000000000000000000000c00e94cb662c3520282e6f5717214004a7f26888000000000000000000000000ffffffffffffffffffffffffffffffffffffffff0000000000000000000000000000000000000000000000000000000064a11ec00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000ef1c6e67703c7bd7107eed8303fbe6ec2554bf6b00000000000000000000000000000000000000000000000000000000647998c800000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000000000000000000000000000000000000000004198016cd78d402572a717369d25be0a024d086b4f662f61b97b01ff60d1ad85f419bdea48f55c9112018e1e7ce75b19a2883c9f0bb2a27d7303b6c5e6e1c2bbc21b000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000270801d946c94000a0000000000000000000000000000000000000000000000000b82cd698a09db9900000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002000000000000000000000000c00e94cb662c3520282e6f5717214004a7f26888000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000b82cd698a09db99',
  value: 0n,
  chainId: 1n,
  signature: Signature { r: "0xf0af93a518859383151ee21c8f93135c577d4fddafb32de618c4e05fa5a8d658", s: "0x77fa66bdbc483615a918801cb4685ab62c74dc8ef92e34137376c3796388d571", yParity: 1, networkV: null },
  accessList: []
}
```

</details>

</details>

<details>
<summary>

# Events

</summary>

## Filter

When a Contract creates a log, it can include up to 4 pieces of data to be indexed by. The indexed data is hashed and included in a Bloom Filter, which is a data structure that allows for efficient filtering.

So, a filter may correspondingly have up to 4 topic-sets, where each topic-set refers to a condition that must match the indexed log topic in that position (i.e. each condition is AND-ed together).

If a topic-set is null, a log topic in that position is not filtered at all and any value matches.

If a topic-set is a single topic, a log topic in that position must match that topic.

If a topic-set is an array of topics, a log topic in that position must match any one of the topics (i.e. the topic in this position are OR-ed).

This may sound complicated at first, but is more easily understood with some examples.

![image](https://github.com/LokeshPatil-loki/Notes/assets/69594258/722553ce-d50b-46cf-ae43-9c14b080af50)

<pre>ERC-20:
Transfer(address indexed src, address indexed dst, uint val)

-------------------^
----------------------------------------^

Notice that only _src_ and _dst_ are _indexed_, so ONLY they
qualify for filtering.

Also, note that in Solidity an Event uses the first topic to
identify the Event name; for Transfer this will be:
id("Transfer(address,address,uint256)")

Other Notes:

- A topic must be 32 bytes; so shorter types must be padded
</pre>

```
// List all token transfers  *from*  myAddress
filter = {
    address: tokenAddress,
    topics: [
        utils.id("Transfer(address,address,uint256)"),
        hexZeroPad(myAddress, 32)
    ]
};

// List all token transfers  *to*  myAddress:
filter = {
    address: tokenAddress,
    topics: [
        utils.id("Transfer(address,address,uint256)"),
        null,
        hexZeroPad(myAddress, 32)
    ]
};

// List all token transfers  *to*  myAddress or myOtherAddress:
filter = {
    address: tokenAddress,
    topics: [
        utils.id("Transfer(address,address,uint256)"),
        null,
        [
            hexZeroPad(myAddress, 32),
            hexZeroPad(myOtherAddress, 32),
        ]
    ]
};

```

## Listen For Event

```
const filter = {
    address: "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
    topics: [ethers.id("Transfer(address,address,uint256)")]
};

provider.on(filter, (Log) => {
    console.log(Log);
});
```

## Stop Listening for Event

```
provider.off(filter);
```

</details>
