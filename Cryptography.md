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
  * The work (adjusting the nonce) is costly and time-consuming, but verification is super easy


  
  
