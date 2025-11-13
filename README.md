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
        this.nonce=0;
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
```Javascript
mineBlock(difficulty){
        while(this.hash.substring(0, difficulty)!=Array(difficulty+1).join("0")){
            this.nonce++;
            this.hash=this.calculateHash();
    }
    console.log("Block minded: "+this.hash)
        }
```
POW

This method makes sure that each block is mined repeatedly recalculating its hash until it reaches certain difficulty target the higher the difficulty is the more time it takes to mine and find a valid hash and the nonce count how many tries of calculations of hashes it took to reach that requirement for example if the difficulty was 4 we add 1+ because its an array and fill it with zeros comparing it with the hash that also takes the first numbers up to the difficulty which is 4 in this case and it keep recalculating till we get the 0000 
``` Javascript 
class Blockchain {
    constructor() {
        this.chain = [this.createGenesisBlock()];
        this.difficulty=2;
        this.pendingTransactions=[];
        this.miningReward=100;
    }

    createGenesisBlock() {
        return new Block(0, "04/10/2025", "Genesis Block", "0");
    }

    getLatestBlock() {
        return this.chain[this.chain.length - 1];
    }

   minePendingTransactions(miningRewardAddress){
    let block= new block(Date.now()this.pendingTransactions);
    block.mineBlock(this.difficulty);

    console.log('Block successfully mined!');
    this.chain.push(block)

    this.pendingTransactions=[
    new Transaction(null, miningRewardAddress, this.miningReward)
];
  }

createTransaction(transaction){
this.pendingTransactions.push(transaction);
}

getBalanceofAddress(address){

let balance=0;
for(const block of this.chain){
    for(const trans of block.transactions){
        if(trans.fromAddress==address)
            balance-=trans.amount
        if(trans.toAddress=address)
            balance+=trans.amount
    }
 }
return balance;
}

    isChainValid() {
        for (let i = 1; i < this.chain.length; i++) {
            const currentBlock = this.chain[i];
            const previousBlock = this.chain[i - 1];

            if (currentBlock.hash !== currentBlock.calculateHash()) {
                return false;
            }
            if (previousBlock.hash !== previousBlock.calculateHash()) {
                return false;
            }
            if (currentBlock.previousHash !== previousBlock.hash) {
                return false;
            }
        }
        return true;
    }
}
```
createGenesisBlock(): Creates the first block manually (no previous block) a question might come up is why not just initialize it in the constructer? Well then we lose the ability of resuable code and in the case of changing the genesisBlock timestamp or data later, you only need to update one method this avoids hardcoding values directly in the constructor, which can get messy another question is why not declare it outside of the constructor and the class well the issue with that every blockchain would share the same chain any changes done to one chain would effect every chain thats why use this syntax to point towards the one chain we editing that index points at that instance

minePendingTransactions(miningRewardAddress) is responsible for creating a new block with the current timestampt and all pending transactions this.pendingTransactions is an array of Transaction objects waiting to be mined, initiates 

getLatestBlock(): self explanatory gets the latestBlock with a simple array like functions (this.chain[this.chain.length-1]



isChainValid(): Checks for three conditions to ensure the chain is valid which are 
1- check if the current block hash is equal to its caluclated hash 
2- checks for the previous hash is also equal to its calculated hash 
3-lastly check for the link between the blocks

``` Javascript 
let ZaidCoin = new Blockchain();
ZaidCoin.createTransaction(new Transaction('address1','address2',100));
ZaidCoin.createTransaction(new Transaction('address2','address1',50));

console.log('\n Sarting the miner...');
ZaidCoin.minePendingTransactions('zaid-address');

console.log('\n balance of zaid is: ',ZaidCoin.getBalanceOfAddress('zaid-address'))

console.log('\n Sarting the miner again...');
ZaidCoin.minePendingTransactions('zaid-address');

console.log('\n balance of zaid is: ',ZaidCoin.getBalanceOfAddress('zaid-address'))
```
