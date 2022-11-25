# Hello World Alchemy

Following [the official tutorial in the Alchemy GitHub](https://github.com/alchemyplatform/alchemy-docs/tree/master/tutorials/hello-world-smart-contract). This tutorial is not available on the official docs website but only on GitHub.

## Using Alchemy

1. Alcemny and Metamask setup
2. Initialize a project
3. Write a contract in _contracts_
4. Connect Alchemy and Metamask to the project
5. $ `truffle compile`
6. $ Add a Deployment Script _2_deploy_contracts.js_ in _migrations_
7. $ `truffle migrate --network goerli`

### Alchemy and Metamask setup

1. Create an app in Alchemy
2. Switch Metamask to Goerli (or wherever the app is)
3. Add ether from a faucet
4. Test connection by checking the balance in _Alchemy Composer_

### Initialize a project

1. Create a folder for the project
2. $ `npm init -y`
3. $ `npm i -g truffle`
4. $ `truffle init`
5. $ `npm install @truffle/hdwallet-provider`

### Connect Alchemy and Metamask to the project

1. **IMPORTANT** Create a _.gitignore_ and add _.env_
2. `npm i dotenv`
3. Add a _.env_ file using the format given below
4. Provide `your-api-key` and `"your-metamask-seed-phrase"` in _.env_
5. Configure `HDWalletProvider` in _truffle_config.js_

## Files

### _.env_

```toml
API_URL = "https://eth-ropsten.alchemyapi.io/v2/your-api-key"
MNEMONIC = "your-metamask-seed-phrase"
```

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
    compilers: {
      solc: {
        version: '0.8.0',
      },
    },
  },
}
```

### _2_deploy_contracts.js_

```js
const HelloWorld = artifacts.require('HelloWorld')
const initMessage = 'Hello world!'

module.exports = function (deployer) {
  deployer.deploy(HelloWorld, initMessage)
}
```