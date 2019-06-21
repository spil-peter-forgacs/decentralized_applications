# Private Blockchain setup with geth via cli

This is a simple recreation of documentation of https://www.theschool.ai/courses/decentralized-application/lessons/private-blockchain-setup-screencast/

## Step 1
* install geth

## Step 2
* Create genesis block file

genesis.json
```
{
    "config": {
        "chainid": 1994,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0,
        "byzantiumBlock": 0
    },
    "difficulty": "400",
    "gasLimit": "2000000",
    "alloc": {
        "7b684d27167d208c66584ece7f09d8bc8f86ffff": {
            "balance": "100000000000000000000000"
        },
        "ae13d41d66af28380c7af6d825ab557eb271ffff": {
            "balance": "120000000000000000000000"
        }
    }
}
```

### Config
chainId - this is your chain's identifier, and is used in replay protection.
homesteadBlock, eip155Block, eip158Block, byzantiumBlock - these relate to chain forking and versioning, so in our case lets leave them 0 since we're starting a new blockchain.

### difficulty
This dictates how difficult is to mine a block. Setting this value low (~10-10000) is helpful in a private blockchain as it lets you mine blocks quickly, which equals fast transactions, and plenty of ETH to test with. For comparision, the Ethereum mainnet Genesis file defines a difficulty of 17179869184.

### gasLimit
This is the total amount of gas that can be used in each block. With such a low mining difficulty, block will be moving pretty quickly, but you should still set this value pretty high to avoid hitting the limit and slowing down your network.

### alloc
Here you can allocate ETH to specific addresses. This won't create the account for you, so make sure its an account you already have control of. You will need to add the account to your private chain in order to use it, and to do that you need access to the keystore/utc file. For example, Geth and MyEtherWallet give you access to this file when you create an account, but Metamask and Coinbase do not. The addresses provided are not real addresses, they are just examples. Here we allocate 100,000 and 120,000 ETH repectively.

## Step 3
* Instantiate genesis block

`geth --datadir ./myDataDir init ./genesis.json`

`geth --datadir . init ./genesis.json`

## Step 4
* Start the Ethereum node

`geth --datadir ./myDataDir --networkid 1114 console`

`geth --datadir . --networkid 1111 console`

## Step 5 (working with geth console)
* Create account

`personal.newAccount("<YOUR_PASSPHRASE>")`

* Set default account

`miner.setEtherbase(web3.eth.accounts[0])`

* Start mining

`miner.start()`

* Check balance

`eth.getBalance(eth.coinbase)`

* Stop mining

`miner.stop()`
