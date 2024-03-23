# Starter Learning GETH Private Network | Blockchain

## Table of Contents

1. [Preview](#preview)
2. [Description](#description)
3. [Requirements](#requirements)
4. [How to Use](#how-to-use)
5. [About Creator](#about-creator)

## Preview

<p align="center">
  <img src="https://github.com/ferdyhape/GETH-Blockchain/assets/75787853/c1e495a2-3dec-487d-9f63-32d5b9eacf10" width="75%" height="75%">
</p>

## Description

- This repository is made for learning GETH make a private network in the blockchain.

## Requirements

- [x] [Go Ethereum (GETH)](https://geth.ethereum.org/)

## How to Use

1.  Clone this repository
2.  Create Accounts, Open a split terminal for each node directory and run:
    ```bash
    geth --datadir "./data" account new
    ```
3.  rename password-example.txt for each account to password.txt (in node1 and node2 directory).
4.  (optional) Save public addresses and passwords for each account to info.txt.
5.  Configure the genesis block, open privateblock.json and edit the file as needed.

    ```json
    {
      "config": {
        "chainId": 1234567,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0,
        "eip158Block": 0,
        "byzantiumBlock": 0,
        "constantinopleBlock": 0,
        "petersburgBlock": 0,
        "istanbulBlock": 0,
        "berlinBlock": 0,
        "clique": {
          "period": 5,
          "epoch": 30000
        }
      },
      "difficulty": "1",
      "gasLimit": "8000000",
      "extradata": "0x0000000000000000000000000000000000000000000000000000000000000000{ INITIAL_SIGNER_ADDRESS }0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "alloc": {
        "{ FIRST_NODE_ADDRESS }": {
          "balance": "3000000000000000000000000000000000000"
        },
        "{ SECOND_NODE_ADDRESS }": {
          "balance": "3000000000000000000000000000000000000"
        }
      }
    }
    ```

    - Replace { INITIAL_SIGNER_ADDRESS } with the address of the first node.
    - Replace { FIRST_NODE_ADDRESS } with the address of the first node.
    - Replace { SECOND_NODE_ADDRESS } with the address of the second node.
    - Add more alloc fields as needed.
    - Save the file.

6.  Initialize the genesis block, Open a split terminal for each node directory and run:

    ```bash
    geth --datadir ./data init ../privateblock.json
    ```

7.  Generate the bootnode key, Open a split terminal for the bnode directory and run:
    ```bash
    bootnode -genkey boot.key
    ```
8.  Run the bootnode, Open a split terminal for the bnode directory and run:

    ```bash
    bootnode -nodekey boot.key -verbosity 7 -addr "127.0.0.1:30301"
    ```

9.  (Optional) Store the enode address to info.txt.
10. Run the nodes, Open a terminal for node1 directory and run:

    ```bash
    geth --datadir "./data"  --port 30304 --bootnodes enode://{ YOUR_VALUE } --authrpc.port 8547 --ipcdisable --allow-insecure-unlock  --http --http.corsdomain="https://remix.ethereum.org" --http.api web3,eth,debug,personal,net --networkid { NETWORK_ID } --unlock { ADDRESS_NODE1 } --password { PASSWORD_FILE_NAME_EXTENSION }  --mine --miner.etherbase= { SIGNER_ADDRESS }
    ```

    - Replace { YOUR_VALUE } with the enode address.
    - Replace { NETWORK_ID } with the network id.
    - Replace { ADDRESS_NODE1 } with the address of the first node.
    - Replace { PASSWORD_FILE_NAME_EXTENSION } with the password file name extension.
    - Replace { SIGNER_ADDRESS } with the address of the first node.

11. For the second node, Open a terminal for node2 directory and run:

    ```bash
    geth --datadir "./data"  --port 30306 --bootnodes enode://{ YOUR_VALUE }  -authrpc.port 8546 --networkid { NETWORK_ID } --unlock { ADDRESS_NODE2 } --password { PASSWORD_FILE_WITH_EXTENSION }
    ```

    - Replace { YOUR_VALUE } with the enode address.
    - Replace { NETWORK_ID } with the network id.
    - Replace { ADDRESS_NODE2 } with the address of the second node.
    - Replace { PASSWORD_FILE_WITH_EXTENSION } with the password file name extension.

12. Private network is ready to use.
13. For testing network, test with deploy smart contract in Remix IDE. use "custom - external http provider" with host and port http://127.0.0.1:8545.

### About Creator

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ferdy-hahan-pradana)
[![instagram](https://img.shields.io/badge/instagram-833AB4?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/ferdyhape)
[![github](https://img.shields.io/badge/github-333?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ferdyhape)
