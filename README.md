# JS-blockchain
A BlockChain is a data structure that stores unites called blocks each block contains a set of transactions or records, a timestep, and cryptographic hash of the previous block

A hash means: is the process of converting any input text, numbers, files into a unique fixed size string

SHA-256: Modren cryptography, blockchain

basic explaination is that a blockchain is more like a tree of blocks that includes multiple chains for blocks pointing at their parent block. The pointing happens through hashes which are calculated based upon the data inside the block (hash of the parent, transaction data and other important stuff)

through pointing through hashes we can enforce a specific order of blocks because of that you cant just take a block in the middle of the chain and change its data
