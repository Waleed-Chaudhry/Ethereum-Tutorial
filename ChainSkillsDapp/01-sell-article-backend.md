# Sell Article Backend

### Smart Contract
* Grab the skeleton from github
```
truffle unbox chainskills/chainskills-box
```
* Create ChainList.sol
```solidity
pragma solidity ^0.4.18;

contract ChainList {
  // state variables
  address seller;
  string name;
  string description;
  uint256 price;

  // sell an article
  function sellArticle(string _name, string _description, uint256 _price) public {
    seller = msg.sender;
    // seller is not passed into the contructor
    // It is instead gathered from the "from" object used to call the sell Article function
    name = _name;
    description = _description;
    price = _price;
  }

  // get an article
  function getArticle() public view returns (
    // Function of type view doesn't set contract variables, only views them
    // Function of type pure doesn't view or set contract variables
    // Neither of these two types of functions cost gas
    address _seller,
    string _name,
    string _description,
    uint256 _price
  ) {
      return(seller, name, description, price);
      // We can return several objects in solidity, not just one
  }
}
```

* Create deployment in the file 2_deploy_contracts.js
```solidity
var ChainList = artifacts.require("./ChainList.sol");

module.exports = function(deployer) {
  deployer.deploy(ChainList);
}
```
### Connecting to Ganache
Ganache uses network id 5777 and rpc endpoint 7545 as the default. Truffle develop uses network id 4447 and rpc endpoint 9545.
Both of these are modifiable in Ganache, but neither is in truffle develop. So we'll use Ganache because of this flexibility.  

Ganache also accounts don't need to be unlocked since they're always unlocked.  

* Start ganache
* Deploy the contract to the ganache node:
```
truffle migrate --network ganache
```

* Interact with the contract:
```javascript
truffle console --network ganache
```

* Get balance of an account in Ether:
```javascript
web3.fromWei(web3.eth.getBalance(web3.eth.accounts[0]), "ether").toNumber()
```

* Get instance of the contract:
```javascript
ChainList.deployed().then(function(instance) {app = instance;})
```

* Use app variable to interact with the contract and call functions on it
```javascript
app.sellArticle("iPhone7", "Selling in order to buy iPhone 8", web3.toWei(3, "ether"), {from:web3.eth.accounts[1]})
// from tells you the account that pays for the gas
// Balance account[1] changes
```

### Tests
You can’t fix bugs in our contract once already deployed. You have to deploy a new instance of the contract. Therefore thoroughly testing your contract is very important. We'll focus on JavaScript testing, since Solidity testing is still recent.

* Create a new file ChainListHappyPath.js inside the test directory
```solidity
var ChainList = artifacts.require("./ChainList.sol"); // Same as the deployment script

// test suite
contract('ChainList', function(accounts){
  // function accounts gets a list of accounts of the node we're connected to
  var chainListInstance;
  var seller = accounts[1];
  var articleName = "article 1";
  var articleDescription = "Description for article 1";
  var articlePrice = 10;

  it("should be initialized with empty values", function() {
    // The text is what the console will show
    return ChainList.deployed().then(function(instance) {
      // Same as getting instance from the truffle console
      return instance.getArticle();
    }).then(function(data) {
      // Chain the promise to another function that receives the data of our initial function in object data
      // Can then do assertions on the object data
      assert.equal(data[0], 0x0, "seller must be empty");
      assert.equal(data[1], "", "article name must be empty");
      assert.equal(data[2], "", "article description must be empty");
      assert.equal(data[3].toNumber(), 0, "article price must be zero");
      console.log("data[3]=", data[3]) //Can log the output to the console
    })
  });

  it("should sell an article", function() {
    return ChainList.deployed().then(function(instance) {
      chainListInstance = instance;
      // Here we save the instance of the smart contract
      return chainListInstance.sellArticle(articleName, articleDescription, web3.toWei(articlePrice, "ether"), { from: seller});
    }).then(function() { // sellArticle doesn't actually return anything so no need to pass the data
      return chainListInstance.getArticle();
      // the state of the contract has changed since we called sellArticle on it
    }).then(function(data) {
      assert.equal(data[0], seller, "seller must be " + seller);
      assert.equal(data[1], articleName, "article name must be " + articleName);
      assert.equal(data[2], articleDescription, "article description must be " + articleDescription);
      assert.equal(data[3].toNumber(), web3.toWei(articlePrice, "ether"), "article price must be " + web3.toWei(articlePrice, "ether"));
    });
  });
});
```
* Run the test suite
```javascript
truffle test --network ganache
```

We have to perform the tests on test environments because deploying and running tests costs gas  
Restarting Ganache should reset all the account balances
