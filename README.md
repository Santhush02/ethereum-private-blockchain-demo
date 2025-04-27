# ethereum-private-blockchain-dem

This project demonstrates setting up a private Ethereum blockchain using Geth 1.9.15.

## Requirements 
- Geth 1.9.15 (https://geth.ethereum.org/downloads)
- Linux/ Ubuntu Virtual Machine (2 cores, 4GB RAM)

## Features
- Custom Genesis Block
- Private Network Setup
- Mining Ether on Private Chain
- Managing Accounts (Etherbase, Balances)
- Sending and Confirming Transactions
- Exploring Transaction Pool and Blocks

## Technologies
- Geth (Go-Ethereum)
- Web3.js (inside Geth console)

## Setup Instructions
1. Extract and execute geth binary
        tar -xvzf <downloaded geth binary >

2. Create genesis.json block

3. Initialize private blockchain
        mkdir ~/eth_private_net
        ./geth --datadir ~/eth_private_net init genesis.json

4. Start the private Geth node
        ./geth --datadir ~/eth_private_net \
        --networkid 12345 \
        --http \
        --http.api personal,eth,web3,miner,net,txpool \
        --allow-insecure-unlock \
        --port 30303 \
        --http.port 8545 \
        console

5. Create and manage accounts 
        personal.newAccount()
        personal.newAccount()

6. Set the 1st account as the etherbase to recieve minning awards.
        miner.setEtherbase(eth.accounts[0])

7. Start mining and interact with the blockchain
        miner.start(1)      // "1" defines the no. of minning CPU threads
        miner.stop()

    Monitored block numbers using,
        eth.blockNumber

    Check balance,
        web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")
        web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")

8. Unlock Account and send Ether 
        personal.unlockAccount(eth.coinbase, "<password>", 60)

        eth.sendTransaction({
        from: eth.coinbase,
        to: eth.accounts[1],
        value: web3.toWei(1, "ether")
        })

    Checked pending transactions,
        txpool.status

9. Mine the Transaction into a Block to confirm the transaction 
        miner.start(1)
        miner.stop()       

10. Verify transaction and balances
        web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")
        web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")

    Retrieve full transaction details using hash 
        eth.getTransaction("<your_transaction_hash_here>")

    Retrieve transaction receipt
        eth.getTransactionReceipt("<your_transaction_hash_here>")


## Screenshots
- Mining blocks
- Transaction transfer
- Transaction details using hash

## What I Learned
- How Proof-of-Work mining rewards work
- How to manage accounts and transactions securely
- How Ethereum transactions are structured internally

## Future Improvements
- Deploy a simple smart contract
- Setup multi-node private blockchain