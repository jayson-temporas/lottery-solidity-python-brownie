# Smart Contract Lottery

A Solidity Smart contract where players can enter a lottery for 50$ worth of ETH determine by Chainlink Price Feed.

At the end of the game, the contract owner will draw one winner using Chainlink VRF (Verifiable Random Function) and the prize pool will be transfer to his address.

## Prerequisites

Please install or have installed the following:

- [nodejs and npm](https://nodejs.org/en/download/)
- [python](https://www.python.org/downloads/)
- [brownie](https://eth-brownie.readthedocs.io/en/stable/install.html)

### Install the dependencies

```
pip install -r requirements.txt
```

## Env variables

Create .env file from .env-local 

```
cp .env-local .env
```

PRIVATE_KEY - your eth private key, get it on metamask/ganache

WEB3_INFURA_PROJECT_ID - create a project in Infura then get the project id
[https://infura.io](https://infura.io)

ETHERSCAN_TOKEN -  get api key on etherscan.io to programatically verified your smart contract upon deploying on testnet and mainnet
[https://etherscan.io](https://etherscan.io)


## Local Development

For local testing [install ganache-cli](https://www.npmjs.com/package/ganache-cli)

```bash
npm install -g ganache-cli
```

All the scripts are designed to work locally or on a testnet. You can add a ganache-cli or ganache UI chain like so: 
```
brownie networks add Ethereum ganache host=http://localhost:8545 chainid=1337
```
And update the brownie config accordingly. There is a `deploy_mocks` script that will launch and deploy mock Oracles, VRFCoordinators, Link Tokens, and Price Feeds on a Local Blockchain. 


## Deploy to a testnet / Scripts

```
brownie run scripts/1_deploy_lottery.py
brownie run scripts/2_start_lottery.py
brownie run scripts/3_enter_lottery.py
brownie run scripts/4_end_lottery.py
```
This will deploy your lottery, fund it with LINK, start your lottery, you'll enter it, and then end your lottery. You can also work with the console to do these. 

You can deploy and work with a local network by deploying mocks. 

## Testing

There are 2 types of tests in this project. 

- unit tests, which run on a local blockchain.
- integration tests, which run on a testnet

To run the unit tests:
```
brownie test
```
integration tests:
```
brownie test --network <network>
```

For more information on effective testing with Chainlink, check out [Testing Smart Contracts](https://blog.chain.link/testing-chainlink-smart-contracts/)

Tests are really robust here! They work for local development and testnets. There are a few key differences between the testnets and the local networks. We utilize mocks so we can work with fake oracles on our testnets. 

### To test development / local
```bash
brownie test
```
### To test mainnet-fork
This will test the same way as local testing, but you will need a connection to a mainnet blockchain (like with the infura environment variable.)
```bash
brownie test --network mainnet-fork
```
### To test a testnet
Kovan and Rinkeby are currently supported
```bash
brownie test --network kovan
```

## Adding additional Chains

If the blockchain is EVM Compatible, adding new chains can be accomplished by something like:

```
brownie networks add Ethereum binance-smart-chain host=https://bsc-dataseed1.binance.org chainid=56
```
or, for a fork: 

```
brownie networks add development binance-fork cmd=ganache-cli host=http://127.0.0.1 fork=https://bsc-dataseed1.binance.org accounts=10 mnemonic=brownie port=8545
```

## License

This project is licensed under the [MIT license](LICENSE).
