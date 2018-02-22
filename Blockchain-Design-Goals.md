# Design Goals

### Data Distribution
* Each node in the system has access to all the data.
* One central node can write data, every other node reads from the central node
* If any node (including the central one) goes down, all nodes still have their own copy
* Every node can check the data in the entire system, but it creates privacy issues because each node see how much is owned by a given address
* Therefore you only need to prove that you have access to the address in order to do transaction with coins associated with that address
* Each node keeps track of the last transaction is recorded, and if its disconnects and reconnects it downloads all transactions after that last one

### Decentralization
* In a central system, all you need to do is corrupt the central node to corrupt the entire system
* Much harder to bring down a system if every node can modify the data, but that leads to data consistency issues
* That issue is solved by the consensus algorithm
* For a given transaction, one node is seen as the source of truth. That node changes for each transaction.
* And there isn't a single node assigning the source of truth for each transaction. Therefore this algorithm resides in every node

### Immutability
* You can't change the history. Only append new transactions to it.

## Implementation
* Bitcoin and Ethereum are examples of implementations

### Bitcoin
* Designed for one application - a digital cash system
* Basic element that transactions are keeping track of are UTXO's (Unspent transaction Output)
* They mimic checks in the real world. Once a check is spent, it can't be reused, and the author of the check needs to sign it to prove he's the author
* Any node in the network can create and sign networks, after which they're in a pending state
* Every 10 minutes, there is a competition to decide which node will append which transaction to the ledger 
* The competition happens randomly based on the consensus algorithm 
  * Consensus algorithm creates a complex puzzle which can be solved by any node
  * The node that wins the consensus algorithm, will solve the puzzle
  * It will then have to prove that it did solve it
  * If the solution is found to be correct, the node will decide which transactions get appended to the ledger
  * Transactions are grouped into blocks of transactions
  * This process is called mining
* The winner of the competition gets to include one special transaction in the block that creates an amount of bitcoin and assigns to himself
* The amount is determined by the consensus algorithm. Currently it's 12.5 and gets divided by half every 2 years
* This incentivizes the miners to not jeopardize the very currency their being paid in

### Ehtereum
* Implements the same principles as Bitcoin, but is more generic and has a different implementation
* The block delay is 17s due to a different implementation of the consensus algorithm
* Transactions can have some Turing complete code attached to them that can be executed on any node across the network, which lets you create smart contracts
* Have to pay Ether for every transaction you run on the Ethereum blockchain

## Instances
* Genesis block - first block in the blockchain
* Instantiation: creating the genesis block is passing it on the network of miners
* Instance: Chain of blocks built on top of the genesis block
* Different instances: The Main Net, Test nets, and your private net
* Ether created on one instance can't be spent on another

### Fork
* From a single genesis block, the ledger will start to diverge after a given block.
* Can happen voluntarily or to fix a bug
* After a fork, only currency created on the given chain can be spent on it, and both chains lose value
* In June 2016, an attacker exploited a smart contract, which led to a fork. 
* Ethereum now has two currencies. 
* Ether with the majority with the attacker's transactions removed - ETH and Ethereum classic, ETC

### Tricameral System
* Developers: Write the actual code for the blockchain implementation. Most code is open source
* Users: Use the implementation. Each user has a wallet, all you need to transfer coins to the user's account is the wallet address
* Miners: The higher the processing power (hashrate), the higher your probability to win the consensus algorithm puzzle 
