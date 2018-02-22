# Key Concepts Summary

### Peer to Peer networked database of nodes
* New nodes can join the network by simply installing the wallet client and downloading the ledger of transactions
* There is no need to authenticate
* However, the size of the database is huge 
* So you can create an account and store your wallet on a website running a remote node (e.g. exchanges like Coinbase) 
* Browser plugins like Metamask let you connect your wallet to such a remote node
* If you lose your wallet, or someone steals it, you lose your balance and access to transactions

### Ledger
* Series of ordered blocks chained with one another containing lists of ordered transactions
* The integrity and validity of those blocks is maintained by a series of cryptographic algorithms

### Transaction Finality
* Once a block is established, it becomes increasingly costly to change a transaction in the past. 
* Even if you do, you have recompute the block in which the transaction is stored, and each subsequent block. 
* The cost of this operation increases exponentially. 
* One mining network would need to have 51% of the power of the entire mining network in order to be faster than the rest of the network to create fraudulent transcations

### Consensus Algorithm
* Not all nodes need to take part in the consensus algorithm. Only nodes that are part of the mining process.
* Most popular type is called proof of work algorithm
* The higher your computing power or hash rate, the more likely it is to solve the consensus puzzle
* Doesn't require any central node, and avoids the race conditions of one or more nodes solving the puzzle at the same time
* Proof of work has scalability problems, and uses too much power
* Alternatives such as proof of state are being researched codenamed Casper

### Crypto-currency
* Need a mechanism to incentivize miners 
* Any currency needs 6 properties:  
  * Durable: Transaction Finality of the ledger
  * Portable: Can easily move from wallet to wallet
  * Acceptability: Trust in all the other five properties, and the ability to exchange cryptocurrency for fiat currency via an exchange
  * Limited Supply: Only way to mint currency is through the consensus algorithm
