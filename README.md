# JS-blockchain
A BlockChain is a data structure that stores unites called blocks each block contains a set of transactions or records, a timestep, and cryptographic hash of the previous block

A hash means: is the process of converting any input text, numbers, files into a unique fixed size string

SHA-256: Modren cryptography, blockchain

basic explaination is that a blockchain is more like a tree of blocks that includes multiple chains for blocks pointing at their parent block. The pointing happens through hashes which are calculated based upon the data inside the block (hash of the parent, transaction data and other important stuff)

through pointing through hashes we can enforce a specific order of blocks because of that you cant just take a block in the middle of the chain and change its data
``` java script 
const SHA256 = require('crypto-js/sha256');
```
this imports the![Status](https://img.shields.io/badge/SHA256-yellow)  hash function from the crypto-js library its used to generate a unique hash for each block based on its contents
``` java script 
class Block {
    constructor(index, timestamp, data, previousHash = '') {
        this.index = index;
        this.timestamp = timestamp;
        this.data = data;
        this.previousHash = previousHash;
        this.hash = this.calculateHash();
    }

    calculateHash() {
        return SHA256(this.index + this.previousHash + this.timestamp + JSON.stringify(this.data)).toString();
    }
}
```
index: position of the block in the chain.

timestamp: when the block was created.

data: Transaction or payload.

previousHash: Hash of the previous block (used to link blocks).

Hash: The current block's hash, calculated using calculateHash().

calculateHash(): combines all block properties into a string and hashes it and ensures that any change in block data will result in a different hash
