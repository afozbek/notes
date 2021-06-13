---
description: >-
  We will looking at Solidity programming language and its basic features.
  Solidity is a programming language for creating smart contracts on ethereum
  blockchain.
---

# Ethereum Development: Solidity

This article inspired by [\#1 Solidity Tutorial & Ethereum Blockchain Programming Course \| CryptoZombies](https://cryptozombies.io/) Go checkout the tutorials if you are interested.

### Should start with importing it and wrapping it in a contract field

```text
pragma solidity >=0.5.0 <0.6.0;

contract ZombieFactory {

}
```

### uint-int-string-struct

```text
uint count = 5; // cannot be negative
int count  = -5; 
string name  = "Furkan is handsome and also awesome!"

// create a type
struct Name {
	string name;
	uint number;
}
```

### Functions

All functions public by default and accessible by any contracts

```text
// It is a convention that naming variables with underscore to keep them different from global variables
function createZombie(string memory _name, uint _dna) public {
    // todo
} 
```

It is a good practice making your function private by default and making the name starts with underscore\(\_\)

```text
function _createZombie(string memory _name, uint _dna) private {
    // todo
} 
```

### Function Modifiers

```text
string greeting = "Furkan is great";
// 'returns'
function sayHello() public returns (string memory) {
  return greeting;
}

// Since funtion does not change any state in the contract
// We can declare it as a 'view'
function sayHello() public view returns (string memory) {
  return greeting;
}

// If you are not accessing any state fields in function
// You can use 'pure' function declaration
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
```

### Keccak256 and TypeCasting

Ethereum has the hash function `keccak256` built in, which is a version of SHA3. A hash function basically maps an input into a random 256-bit hexadecimal number. A slight change in the input will cause a large change in the hash.

It's useful for many purposes in Ethereum, but for right now we're just going to use it for pseudo-random number generation.

Also important, `keccak256` expects a single parameter of type `bytes`. This means that we have to "pack" any parameters before calling `keccak256`:

```text
//6e91ec6b618bb462a4a6ee5aa2cb0e9cf30f7a052bb467b0ba58b8748c00d2e5
keccak256(abi.encodePacked("aaaab"));
//b1f078126895a1424524de5321b339ab00408010b7cf0e6ed451514981e58aa9
keccak256(abi.encodePacked("aaaac"));
```

Sometimes you need to convert between data types

```text
uint8 a = 5;
uint b = 6;
// throws an error because a * b returns a uint, not uint8:
uint8 c = a * b;
// we have to typecast b as a uint8 to make it work:
uint8 c = a * uint8(b);
```

In the above, a \* b returns a uint, but we were trying to store it as a uint8, which could cause potential problems. By casting it as a uint8, it works and the compiler won't throw an error.

### Events

Events are a way for your contract to communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen.

```text
// declare the event
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public returns (uint) {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
}
```

Your app front-end could then listen for the event. A javascript implementation would look something like:

```text
YourContract.IntegersAdded(function(error, result) {
  // do something with result
})
```

### Addresses

The Ethereum blockchain is made up of _**accounts**_, which you can think of like bank accounts. An account has a balance of _**Ether**_ \(the currency used on the Ethereum blockchain\), and you can send and receive Ether payments to other accounts, just like your bank account can wire transfer money to other bank accounts.

Each account has an `address`, which you can think of like a bank account number. It's a unique identifier that points to that account, and it looks like this: `0xeEBd581f950d4D249989063C18508F32890DFdC3`

We'll get into the nitty gritty of addresses in a later lesson, but for now you only need to understand that an address is owned by a specific user \(or a smart contract\).

* Mappings

`Mappings` are another way of storing organized data in Solidity

```text
// For a financial app, storing a uint that holds the user's account balance:
mapping (address => uint) public accountBalance;
// Or could be used to store / lookup usernames based on userId
mapping (uint => string) userIdToName;
```

A mapping is essentially a key-value store for storing and looking up data. In the first example, the key is an `address` and the value is a `uint`, and in the second example the key is a `uint` and the value a `string`.

### msg.sender

In Solidity, there are certain global variables that are available to all functions. One of these is `msg.sender`, which refers to the `address` of the person \(or smart contract\) who called the current function.

In Solidity, function execution always needs to start with an external caller. A contract will just sit on the blockchain doing nothing until someone calls one of its functions. So there will **always** be a msg.sender.

```text
mapping (address => uint) favoriteNumber;

function setMyNumber(uint _myNumber) public {
  // Update our `favoriteNumber` mapping to store `_myNumber` under `msg.sender`
  favoriteNumber[msg.sender] = _myNumber;
  // ^ The syntax for storing data in a mapping is just like with arrays
}

function whatIsMyNumber() public view returns (uint) {
  // Retrieve the value stored in the sender's address
  // Will be `0` if the sender hasn't called `setMyNumber` yet
  return favoriteNumber[msg.sender];
}
```

### Require

For validating the function we can use require

```text
function sayHiToVitalik(string memory _name) public returns (string memory) {
  // Compares if _name equals "Vitalik". Throws an error and exits if not true.
  // (Side note: Solidity doesn't have native string comparison, so we
  // compare their keccak256 hashes to see if the strings are equal)
  require(keccak256(abi.encodePacked(_name)) == keccak256(abi.encodePacked("Vitalik")));
  // If it's true, proceed with the function:
  return "Hi!";
}
```

### Inheritance

One feature of Solidity that makes this more manageable is contract `inheritance`

```text
contract Doge {
  function catchphrase() public returns (string memory) {
    return "So Wow CryptoDoge";
  }
}

contract BabyDoge is Doge {
  function anotherCatchphrase() public returns (string memory) {
    return "Such Moon BabyDoge";
  }
}
```

### Import

You can import other sol files like we are importing on javascript

```text
import "./zombiefactory.sol";

contract ZombieFeeding is ZombieFactory {

}
```

### Storage

```text
contract SandwichFactory {
  struct Sandwich {
    string name;
    string status;
  }

  Sandwich[] sandwiches;

  function eatSandwich(uint _index) public {
    // Sandwich mySandwich = sandwiches[_index];

    // ^ Seems pretty straightforward, but solidity will give you a warning
    // telling you that you should explicitly declare `storage` or `memory` here.

    // So instead, you should declare with the `storage` keyword, like:
    Sandwich storage mySandwich = sandwiches[_index];
    // ...in which case `mySandwich` is a pointer to `sandwiches[_index]`
    // in storage, and...
    mySandwich.status = "Eaten!";
    // ...this will permanently change `sandwiches[_index]` on the blockchain.

    // If you just want a copy, you can use `memory`:
    Sandwich memory anotherSandwich = sandwiches[_index + 1];
    // ...in which case `anotherSandwich` will simply be a copy of the 
    // data in memory, and...
    anotherSandwich.status = "Eaten!";
    // ...will just modify the temporary variable and have no effect 
    // on `sandwiches[_index + 1]`. But you can do this:
    sandwiches[_index + 1] = anotherSandwich;
    // ...if you want to copy the changes back into blockchain storage.
  }
}
```

### Internal and External

In addition to `public` and `private`, Solidity has two more types of visibility for functions: `internal` and `external`.

`internal` is the same as `private`, except that it's also accessible to contracts that inherit from this contract.

`external` is similar to `public`, except that these functions can ONLY be called outside the contract — they can't be called by other functions inside that contract. We'll talk about why you might want to use `external` vs `public` later.

For declaring `internal` or `external` functions, the syntax is the same as `private` and `public`:

### Interfaces

Interface is like a skeleton of the contract that tells which functions that a contract can have

```text
contract NumberInterface {
  function getNum(address _myAddress) public view returns (uint);
}
```

### Interacting with other Smart contracts

```text
// Contract Address
address ckAddress = 0x06012c8cf97BEaD5deAe237070F9587f8E7A266d;
KittyInterface kittyContract = KittyInterface(ckAddress);
```

### Multiple Assignments

```text
function multipleReturns() internal returns(uint a, uint b, uint c) {
  return (1, 2, 3);
}

function processMultipleReturns() external {
  uint a;
  uint b;
  uint c;
  // This is how you do multiple assignment:
  (a, b, c) = multipleReturns();
}

// Or if we only cared about one of the values:
function getLastReturnValue() external {
  uint c;
  // We can just leave the other fields blank:
  (,,c) = multipleReturns();
}
```

### Ownable Contracts

* Ownable Smart Contract which most dapps use

### Modifiers

A function modifier looks just like a function, but uses the keyword modifier instead of the keyword function. And it can't be called directly like a function can — instead we can attach the modifier's name at the end of a function definition to change that function's behavior.

```text
modifier onlyOwner() {
  require(isOwner());
  _;
}
```

### Gas

Every operation on ethereum network produces gas so that your users pay that gasses in order to use them.

* Put same types near each other
* Struct is more efficient

### Times

Solidity provides some native units for dealing with time.

The variable `now` will return the current unix timestamp of the latest block \(the number of seconds that have passed since January 1st 1970\). The unix time as I write this is `1515527488`.

> Unix time is traditionally stored in a 32-bit number. This will lead to the "Year 2038" problem, when 32-bit unix timestamps will overflow and break a lot of legacy systems. So if we wanted our DApp to keep running 20 years from now, we could use a 64-bit number instead — but our users would have to spend more gas to use our DApp in the meantime. Design decisions!

Solidity also contains the time units `seconds`, `minutes`, `hours`, `days`, `weeks` and `years`. These will convert to a `uint` of the number of seconds in that length of time. So `1 minutes` is `60`, `1 hours` is `3600` \(60 seconds x 60 minutes\), `1 days` is `86400` \(24 hours x 60 minutes x 60 seconds\), etc.

```text
uint lastUpdated;

// Set `lastUpdated` to `now`
function updateTimestamp() public {
  lastUpdated = now;
}

// Will return `true` if 5 minutes have passed since `updateTimestamp` was 
// called, `false` if 5 minutes have not passed
function fiveMinutesHavePassed() public view returns (bool) {
  return (now >= (lastUpdated + 5 minutes));
}
```

### Passing Struct Arguments

You can pass a storage pointer to a struct as an argument to a private or internal function. This is useful, for example, for passing around our Zombie structs between functions.

```text
function _doStuff(Zombie storage _zombie) internal {
  // do stuff with _zombie
}
```

### Saving Gas Using View Functions

`view` functions don't cost any gas when they're called externally by a user.

This is because `view` functions don't actually change anything on the blockchain – they only read the data. So marking a function with `view` tells `web3.js` that it only needs to query your local Ethereum node to run the function, and it doesn't actually have to create a transaction on the blockchain \(which would need to be run on every single node, and cost gas\).

We'll cover setting up web3.js with your own node later. But for now the big takeaway is that you can optimize your DApp's gas usage for your users by using read-only `external view` functions wherever possible.

> Note: If a view function is called internally from another function in the same contract that is not a view function, it will still cost gas. This is because the other function creates a transaction on Ethereum, and will still need to be verified from every node. So view functions are only free when they're called externally.

```text
function getZombiesByOwner(address _owner) external view returns(uint[] memory) {

}
```

### Storage is Expensive

One of the more expensive operations in Solidity is using `storage` — particularly writes.

This is because every time you write or change a piece of data, it’s written permanently to the blockchain. Forever! Thousands of nodes across the world need to store that data on their hard drives, and this amount of data keeps growing over time as the blockchain grows. So there's a cost to doing that.

In order to keep costs down, you want to avoid writing data to storage except when absolutely necessary. Sometimes this involves seemingly inefficient programming logic — like rebuilding an array in `memory` every time a function is called instead of simply saving that array in a variable for quick lookups.

In most programming languages, looping over large data sets is expensive. But in Solidity, this is way cheaper than using `storage` if it's in an `external view` function, since `view` functions don't cost your users any gas. \(And gas costs your users real money!\).

### Declaring Arrays in Memory

You can use the memory keyword with arrays to create a new array inside a function without needing to write anything to storage. The array will only exist until the end of the function call, and this is a lot cheaper gas-wise than updating an array in storage — free if it's a view function called externally.

```text
function getArray() external pure returns(uint[] memory) {
  // Instantiate a new array in memory with a length of 3
  uint[] memory values = new uint[](3);

  // Put some values to it
  values[0] = 1;
  values[1] = 2;
  values[2] = 3;

  return values;
}
```

### Payable Modifier

You can make the function payable like the name suggest.

```text
contract OnlineStore {
  function buySomething() external payable {
    // Check to make sure 0.001 ether was sent to the function call:
    require(msg.value == 0.001 ether);
    // If so, some logic to transfer the digital item to the caller of the function:
    transferThing(msg.sender);
  }
}
```

Here, `msg.value` is a way to see how much Ether was sent to the contract, and `ether` is a built-in unit.

What happens here is that someone would call the function from web3.js \(from the DApp's JavaScript front-end\) as follows:

```text
// Assuming `OnlineStore` points to your contract on Ethereum:
OnlineStore.buySomething({from: web3.eth.defaultAccount, value: web3.utils.toWei(0.001)})
```

If a function is not marked payable and you try to send Ether to it as above, the function will reject your transaction.

### Random Number Generating Problem

* Random Number Problem

keccak256 → returns 32 byte array → 256 bit string

### Tokens on Ethereum

A _**token**_ on Ethereum is basically just a smart contract that follows some common rules — namely it implements a standard set of functions that all other token contracts share, such as `transferFrom(address _from, address _to, uint256 _tokenId)` and `balanceOf(address _owner)`.

Internally the smart contract usually has a mapping, `mapping(address => uint256) balances`, that keeps track of how much balance each address has.

So basically a token is just a contract that keeps track of who owns how much of that token, and some functions so those users can transfer their tokens to other addresses.

### ERC721 Tokens

_**ERC721 tokens**_ are **not** interchangeable since each one is assumed to be unique, and are not divisible. You can only trade them in whole units, and each one has a unique ID. So these are a perfect fit for making our zombies tradeable.

> Note that using a standard like ERC721 has the benefit that we don't have to implement the auction or escrow logic within our contract that determines how players can trade / sell our zombies. If we conform to the spec, someone else could build an exchange platform for crypto-tradable ERC721 assets, and our ERC721 zombies would be usable on that platform. So there are clear benefits to using a token standard instead of rolling your own trading logic.

### Comments

The standard in the Solidity community is to use a format called natspec, which looks like this:

```text
/// @title A contract for basic math operations
/// @author FURKAN OZBEK 💯💯😎💯💯
/// @notice For now, this contract just adds a multiply function
contract Math {
  /// @notice Multiplies 2 numbers together
  /// @param x the first uint.
  /// @param y the second uint.
  /// @return z the product of (x * y)
  /// @dev This function does not currently check for overflows
  function multiply(uint x, uint y) returns (uint z) {
    // This is just a normal comment, and won't get picked up by natspec
    z = x * y;
  }
}
```

### Web3 Providers

* Web3.js is client side library for interacting ethereum smart contracts.
* Ethereum is made up of nodes that all share a copy of the same data. Setting a Web3 Provider in Web3.js tells our code which node we should be talking to handle our reads and writes. It's kind of like setting the URL of the remote web server for your API calls in a traditional web app.
* You could host your own Ethereum node as a provider. However, there's a third-party service that makes your life easier so you don't need to maintain your own Ethereum node in order to provide a DApp for your users — **Infura**

#### Infura

[Infura](https://infura.io/) is a service that maintains a set of Ethereum nodes with a caching layer for fast reads, which you can access for free through their API. Using Infura as a provider, you can reliably send and receive messages to/from the Ethereum blockchain without needing to set up and maintain your own node.

You can set up Web3 to use Infura as your web3 provider as follows:

```text
var web3 = new Web3(new Web3.providers.WebsocketProvider("wss://mainnet.infura.io/ws"));
```

Ethereum \(and blockchains in general\) use a public / private key pair to digitally sign transactions. Think of it like an extremely secure password for a digital signature. That way if I change some data on the blockchain, I can prove via my public key that I was the one who signed it — but since no one knows my private key, no one can forge a transaction for me.

#### Metamask

[Metamask](https://metamask.io/) is a browser extension for Chrome and Firefox that lets users securely manage their Ethereum accounts and private keys, and use these accounts to interact with websites that are using Web3.js. \(If you haven't used it before, you'll definitely want to go and install it — then your browser is Web3 enabled, and you can now interact with any website that communicates with the Ethereum blockchain!\).

_Metamask uses Infura's servers under the hood as a web3 provider, just like we did above — but it also gives the user the option to choose their own web3 provider. So by using Metamask's web3 provider, you're giving the user a choice, and it's one less thing you have to worry about in your app._

### Talking with the Contracts

Web3.js will need 2 things to talk to your contract: **its address and its ABI**.

#### Contract Address

After you finish writing your smart contract, you will compile it and deploy it to Ethereum. We're going to cover **deployment** in the **next lesson**, but since that's quite a different process from writing code, we've decided to go out of order and cover Web3.js first.

After you deploy your contract, it gets a fixed address on Ethereum where it will live forever. If you recall from Lesson 2, the address of the CryptoKitties contract on Ethereum mainnet is `0x06012c8cf97BEaD5deAe237070F9587f8E7A266d`.

You'll need to copy this address after deploying in order to talk to your smart contract.

#### Contract ABI

The other thing Web3.js will need to talk to your contract is its _**ABI**_.

ABI stands for Application Binary Interface. Basically it's a representation of your contracts' methods in JSON format that tells Web3.js how to format function calls in a way your contract will understand.

When you compile your contract to deploy to Ethereum \(which we'll cover in Lesson 7\), the Solidity compiler will give you the ABI, so you'll need to copy and save this in addition to the contract address.

### Calling Contract Functions

Web3.js has two methods we will use to call functions on our contract: **call** and **send**.

#### Call

`call` is used for `view` and `pure` functions. It only runs on the local node, and won't create a transaction on the blockchain.

Review: view and pure functions are read-only and don't change state on the blockchain. They also don't cost any gas, and the user won't be prompted to sign a transaction with MetaMask.

Using Web3.js, you would call a function named myMethod with the parameter 123 as follows:

```text
myContract.methods.myMethod(123).call()
```

#### Send

`send` will create a transaction and change data on the blockchain. You'll need to use send for any functions that aren't `view` or `pure`.

sending a transaction will require the user to pay gas, and will pop up their Metamask to prompt them to sign a transaction. When we use Metamask as our web3 provider, this all happens automatically when we call send\(\), and we don't need to do anything special in our code. Pretty cool!

Using Web3.js, you would send a transaction calling a function named myMethod with the parameter 123 as follows:

```text
myContract.methods.myMethod(123).send()
```

