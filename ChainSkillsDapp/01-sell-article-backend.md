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
    seller = msg.sender; //seller is not passed into the sell
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

* Create deployment script
```solidity
var Migrations = artifacts.require("./Migrations.sol");

module.exports = function(deployer) {
  deployer.deploy(Migrations);
};
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
```
