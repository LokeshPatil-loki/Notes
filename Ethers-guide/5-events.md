# Events


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

