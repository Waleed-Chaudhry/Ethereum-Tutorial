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
* The itegrity and validity of those blocks is maintained by a series of cryptographic algorithms
* Once a block is established, it becomes increasingly costly to change a transaction in the past. 
* Even if you do, you have recompute the block in which the transaction is stored, and each subsequent block. 
* The cost of this operation increases exponentially  
