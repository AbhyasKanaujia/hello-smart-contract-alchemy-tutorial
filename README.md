# Hello World Alchemy

Following [the official tutorial in the Alchemy GitHub](https://github.com/alchemyplatform/alchemy-docs/tree/master/tutorials/hello-world-smart-contract). This tutorial is not available on the official docs website but only on GitHub.

## Using Alchemy

1. [Alchemy and Metamask setup](#alchemy-and-metamask-setup)
2. [Initialize a project](#initialize-a-project)
3. Write a contract in _contracts_ called [_HelloWorld.sol_](#helloworldsol)
4. [Connect Alchemy and Metamask to the project](#connect-alchemy-and-metamask-to-the-project)
5. Compile the contract
    - $ `truffle compile`
6. $ Add a Deployment Script [_2_deploy_contracts.js_](#2_deploy_contractsjs) in _migrations_
7. $ `truffle migrate --network goerli`

[Go Back to steps](#using-alchemy)

Now you have a working contract that is deployed on Alchemy. Next you should make a frontend for this. Follow this tutorial on [creating a frontend for your smart contract](https://github.com/AbhyasKanaujia/hello-world-dapp).

### Alchemy and Metamask setup

1. Signup for an acount on [Alchemy](http://alchemy.com)
2. Create an app in Alchemy
3. Switch Metamask to Goerli (or wherever the app is)
4. Add ether from a faucet
5. Test connection by checking the balance in _Alchemy Composer_

[Go Back to steps](#using-alchemy)


### Initialize a project

1. Create a folder for the project
2. Open the project in VS Code
3. Open ternimal
    - `ctrl + `` (ctrl + backtick)
4. Initialie a project using
    - $ `npm init -y`
5. $ Check if truffle is installed on your system 
    - `npm list -g`
6. If not installed then install
    - $ `npm i -g truffle`
7. Create a new truffle project
    - $ `truffle init`
8. Install wallet provider to connect to Alchemy
    - $ `npm install @truffle/hdwallet-provider`

[Go Back to steps](#using-alchemy)


### Connect Alchemy and Metamask to the project

1. **IMPORTANT** Create a _.gitignore_ and add _.env_
2. `npm i dotenv`
3. Add a [_.env_](#env) file using the format given below
4. Provide `your-api-key` and `"your-metamask-seed-phrase"` in _.env_
5. Configure `HDWalletProvider` in [_truffle_config.js_](#truffle-configjs)

[Go Back to steps](#using-alchemy)


## Files

### _HelloWorld.sol_

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract HelloWorld {
    string public message;

    constructor(string memory _message) {
        message = _message;
    }

    function updateMessasge(string memory _message) public {
        message = _message;
    }
}

```

[Go Back to steps](#using-alchemy)


### _.env_

```toml
API_URL = "https://eth-ropsten.alchemyapi.io/v2/your-api-key"
MNEMONIC = "your-metamask-seed-phrase"
```
[Go Back to steps](#using-alchemy)


### _truffle-config.js_

```js
require('dotenv').config()
const HDWalletProvider = require('@truffle/hdwallet-provider')
const { API_URL, MNEMONIC } = process.env

module.exports = {
  networks: {
    development: {
      host: '127.0.0.1',
      port: 7545,
      network_id: '*',
    },
    goerli: {
      provider: function () {
        return new HDWalletProvider(MNEMONIC, API_URL)
      },
      network_id: 5,
      gas: 4000000, //4M is the max
    },
  },
  compilers: {
    solc: {
      version: '0.8.0',
    },
  },
}
```

[Go Back to steps](#using-alchemy)


### _2_deploy_contracts.js_

```js
const HelloWorld = artifacts.require('HelloWorld')
const initMessage = 'Hello world!'

module.exports = function (deployer) {
  deployer.deploy(HelloWorld, initMessage)
}
```

[Go Back to steps](#using-alchemy)

