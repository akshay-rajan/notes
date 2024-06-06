# Blockchain

Blockchain is a **decentralized** and **distributed** digital ledger that is used to record transactions across multiple computers or nodes. 

At its core, a blockchain is a chain of blocks, where each block contains a list of transactions. 
These blocks are linked together using cryptographic **hashes**, forming a continuous and immutable record of all transactions. 
This means that once a transaction is recorded on the blockchain, it cannot be altered or deleted.

One of the key features of blockchain is its decentralized nature.
Instead of relying on a central authority like a bank or government, blockchain relies on a network of computers, known as **nodes**, to validate and record transactions. 
This decentralization makes blockchain resistant to censorship and tampering, as there is no single point of failure.

Blockchain also employs **consensus** mechanisms to ensure the integrity of the data.
The most common consensus mechanism used in blockchain is called Proof of Work (PoW), where nodes compete to solve complex mathematical puzzles to validate transactions and add them to the blockchain.
This process requires a significant amount of computational power, making it difficult for malicious actors to manipulate the blockchain.

## How it Works [(Demo)](https://guggero.github.io/blockchain-demo/#!/)

Each block contains the *data*, *nonce* and two hashes: a *Prev* hash, which chains the last block to the current block, and a *Hash* of the current block. 
**Mining** is the process of validating the blocks. Using the nonce, a SHA-256 hash is generated for the block.
By mining, the nonce is adjusted to make the hash valid.
A valid hash could be one that starts with 3 0s.

Using Prev hash, the blocks are linked together. 
If we change data in a single block, it will invalidate every single subsequent block.
Re-mining in most distributed ledgers are almost impossible.

To make the ledger distributed, each person in the blockchain gets the same copy of the blockchain.
Hence, by **distributing**, we can identify if some data in a person's ledger is corrupted by comparing them with the other copies.
Now we have the Distributed Trustless Ledger.

Not only can we store data, but also we can create **Smart Contracts**: storing code inside a blockchain.
This allows for features like automating transactions when a particular condition, like reaching sufficient profit, is met.

# dApps - Decentralized Applications

dApps are the backbone of Web3. 
In this, we can build the technology, release tokens to public or to funds and raise money, and the companies can be run by DAOs (Decentralized Autonomous Organizations) which are users that hold special tokens named Governance Tokens.

*Pseudonimity* refers to how a user can be recognized by their id or username, but the actual identity remains hidden.

Ethereum is the most commonly used blockchain for dApps, but it has certain demerits like very high expense (gas price) on computation. 
The **Internet Computer** is a scalable cloud computer that runs on a blockchain. It can perform fast computations and store data directly on the chain.

# Internet Computer

The goal of the Internet Computer is to reach **Blockchain Singularity**.
The entire base layout of the Web in one single blockchain.

Today's dApps are only partially decentralized. 
Small amount of data is on a secure blockchain, meanwhile majority of the data is stored in Web2 companies like Asure / AWS or relies on Chrome Extensions. 
These companies have authority over these dApps. 
Current blockchains are extremely difficult to be able to host large amount of data or transactions.
The TPS (Transactions Per Second) limits the usage of the applications.

The Dfinity introduced a novel consensus algorithm named *Threshold Relay* which allows the Internet Computer to read much faster.
IC aggregates the computing capacity of a large number of independent data centres and combines them using the `Internet Computer Protocol` into a large decentralized World Computer.
The decentralized computer is organized into **Canisters**, which can run processes and store data.
As a user you can tap into a canister by making an HTTPS request. 
The IC is a group of canisters, where each canister can hold programs and program states through *WebAssembly* Module and *Memory Page*.

We can write code to run web applications in WebAssembly using languages such as Rust, Motoko etc. 
The program states can be stored within the canister, similar to containers (e.g. Docker), but the **program state gets preserved** (runs forever). 
Thus, we don't have to worry about storage and we only have to think about the logic of the program. 

## [Installation and Setup](./Installation+and+Setup+for+Windows.pdf)

1. Install Windows Subsystem for Linux (WSL)

    ```sh
    # Run on powershell as administrator
    wsl --install
    ```

2. Restart the computer.
3. Set up username and password.
4. Make sure WSL is installed properly.

    ```sh
    wsl --list --verbose
    ```

5. Install VSCode.
6. Install `Motoko` language extension from Dfinity.
7. Install WSL extension.
8. Install Homebrew in WSL.
9. Add brew to path by running the commands listed.
    
    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

10. Install homebrew dependencies.

    ```sh
    sudo apt-get install build-essential
    ```

11. Verify installation of brew.

    ```sh
    brew --version
    ```
12. Install Node into WSL

    ```sh
    brew install node@20
    node --version
    ```
    Optionally, run this if another version of node is already installed.
    ```sh
    brew link node@20
    ```

13. Install dfx

    ```sh
    sh -ci "$(curl -fsSL https://internetcomputer.org/install.sh)"
    ```

## Hello 

To create the default 'hello' app, run

```sh
dfx new hello
```

To see the created project in file explorer, run `explorer.exe
.` Now open the project in VS Code.

```sh
cd hello
```
```sh
dfx start
```
```sh
dfx deploy
```
Now the project is deployed to the local network.

## MOTOKO

Motoko is a programming language designed to create Smart Contracts in the Internet Computer.
It has a lot of similarities with other programming languages.

[**Motoko Style Guide**](https://internetcomputer.org/docs/current/motoko/main/reference/style#style) || [**Debug**](https://internetcomputer.org/docs/current/motoko/main/base/Debug/)

    dfx canister call canister_id function_name function_arg1 ...

### [Candid](https://internetcomputer.org/docs/current/tutorials/developer-journey/level-2/2.4-intro-candid/)

**Candid** is an interface description language. It provides an easy way for us to interact with the canisters.

    dfx canister id __Candid_UI

    http://127.0.0.1:4943/?canisterId=<candid_id>&id=<canister_id>

`dfx deploy` wipes the values in the variables stored and resets them to their initial position. (Orthogonal Persistence)

