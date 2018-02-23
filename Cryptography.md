##  Hashing Function

* Takes an arbitrary amount of data as input and ouputs as a number
* Can be used to check whether data has been tempered with
* If you send some data and it's hash, I can rehash the data and compare it to the hash and to make sure data hasn't been modified
* It is possible to have collisions (two inputs produce the same ouput) but unlikely

### Properties
* Defined range: No matter the size of the input, you'll get the same sized output back
* Deterministic: The same input will always give the same output
* Discontinuous: The slightest change in input will give you completely different outputs
* Uniform: For the any given set of inputs, the corresponding outputs should be distributed as evenly as possible 
* Non-invertible: Can't go from outputs to inputs

### Usage
* Used for chaining blocks together
  * The header of block N contains the hash of the content of block N-1
  * If you change anything in block N-1 (which will change it's hash), you'd have to change it's hash in block N
  * Since the header of block N changes, it's hash changes as well so N+1 will also need to change, and so on
* Recalculating a hash is pretty quick. However we add a constraint to the hash
  * Each hash must have a certain number of leading zeros i.e. the difficulty target
  * Each block has a 32-bit field called nonce 
  * Miners need to try different values of the nonce to get a hash with the required number of leading zeros
  * Because hashing functions in the blockchain are discontinuous, it can take a lot of attempts to get such a hash
  * Hence the presentation of the block with such a hash value constitutes **proof of work**
  * The work (adjusting the nonce) is costly and time-consuming, but verification is super easy (NP Problem)

## Asymmetric Cryptography
Takes a pair of related keys to transform readable data into unreadable and vice versa 

### General Use
* Public Key Encryption Algorithm takes an encryption key and some data as input
* Produces some obfuscated output
* To recover the original message you need the key associated with the key used to do the encryption
* We use the private key to deduce it's public key, but the process is not reversible. 
* You can't use the public key to get back the private key

### Digital Signature
To prove that a message comes from you:
* Hash the message (the transaction) using a defined length hash
* Encrypt the hash using your private key
* Send the message, your public key and this encrypted hash (also called digital signature or the wallet address)
* The recepient extracts the public key from the message and signature
* And compares it to the public key sent as input to make sure they're identical
* Its also able to verify that the message sent is correct by hashing the message and comparing it to the decrypted signature

### RSA Cryptography
* Blockchain uses the Elliptic-curve (ECDSA) cryptography rather than the standard RSA encryption
* ECDSA makes it possible to achieve higher levels of security with smaller keys than RSA
* RSA uses original message, encrypted hash and public key as inputs (same as ECDSA)
* Uses the public key to decrypt the hash
* It then hashes the message, and compares that to the decrypted hash to make sure they are identical

## Merkle Trees
Also known as hash tree
* Say a block has 8 transations. You created 8 hashes from them (H1-H8)
* You subsequently calculate H12 from hash 1 and hash 2, H34, H56 and H78, followed by: H1234 and H4567, followed the roothash (H12345678)
* To verify transaction 5, you just need H6 (you can calculate H5), H78 (you can calculate H56), and H1234. 
* The miner doesn't have to wait for all transactions before it can 
* The blockchain only stores the root hashes
