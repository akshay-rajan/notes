# Solana

Solana is a high-performance blockchain that can support thousands of nodes and 50,000 transactions per second. 
It is designed to be a fast, secure, and scalable platform for decentralized applications and crypto projects.

Solana uses a unique combination of technologies to achieve its high performance, including a **proof-of-stake** consensus mechanism, a novel architecture called the Tower BFT, and a system of parallel processing called Gulf Stream.

Solana's native token, **SOL**, is used to pay for transactions on the network and to secure the blockchain through staking. 

*Client-side development* involves building applications that interact with on-chain solana programs.
This is done using **TypeScript**. 
*Onchain program development* is creating custom apps that run on the blockchain, using the **Rust** language.

### Terminology

- Keypair: A matching pair of public key and secret key.
- Public key: An **address that points to an account** on the Solana network.
- Secret key: Used to verify the **authority over an account**.
- Asymmetric cryptography: Also called public key cryptography, in which each participant possess a pair of keys.
- Encryption (Asymmetric): If encrypted with the public key, only the secret key can be used to read it.
- Signature (Asymmetrics): If encrypted with a secret key, the authenticity of the signature can be verified using the public key.
- SOL: Solana's native token. 
- Lamport: 1 billionth of a SOL.
- Transactions: A set of instructions that invoke solana programs. All modifications to onchain data happen through transactions.
- SPL Tokens: All other tokens (fungible or non-fungible) on the Solana blockchain, except the native token SOL.
- Wallets: Applications that store the secret key and secure transaction signing. e.g. *Phantom Wallet*
- PDAs: 32 byte strings store accounts that are designed to be controlled by a specific program.

## On-chain Development

Each solana cluster, `mainnet-beta`, `testnet`, `devnet` or `localnet` is effectively a single computer with a globally synchronized state.
`devnet` is where we test our application, whereas `testnet` is for validators.

Solana programs are most commonly written in Rust, typically with the **Anchor** Framework.
The framework handle common tasks like redirecting incoming instructions to the right instruction handler, deserializing data for incoming transactions, verifying accounts etc.

Each program is associated with an address, typically created during `anchor init`.
It's stored in the `target/deploy` directory.

**Instruction handlers** are crucial components of smart contracts which how the program should respond to specific instructions. 
Instruction handlers are like HTTP route handlers, and incoming transactions are like HTTP requests.
But instead of returning data, the handlers write their data to accounts on Solana.
Programs can transfer SOL, which will end up in user wallet addresses.
Programs store data as key-value pairs in Program-Derived Addresses (PDAs).

Native / Non-Anchor development requires manual serialization & deserialization of data, which is the process of converting, the data into a format that is easily stored or transmitted, and back.
Solana uses the BORSH serializer.

**Transactions** are made up of an array of instructions.
Every transaction contains
- An array of every account it intends to read or write
- One or more instructions
- A recent blockhash
- One or more signatures

`@solana/web3.js` simplifies this to just instructions and signatures.
Every **Instruction** contains
- The program ID of the intended program
- An array of accounts involved
- Instruction data

The instructions in a transaction are processed *Atomically*.

## Anchor

Initialize a project:
```sh
anchor init demo
```
Build the project:
```sh
cd demo
anchor build 
```
This would store the program keypair in `target/deploy`.
> If the build fails, it's due to Anchor using an older version of rust (run `cargo-build-sbf --version`). 
> To fix this, upgrade to a newer version of solana tools and rerun `build`.
>```sh
> solana-install init 1.18.18
>```
To obtain the public key, which is also included in the `programs/demo/src/lib.rs` file, run:
```sh
anchor keys list
```
Update the following part in the Anchor.toml file for deployment to the `devnet`:
```toml
[provider]
cluster = "Devnet"
```
Now deploy the project:
```sh
anchor deploy
```
> This may fail due to insufficient balance. Hence, obtain free SOL using `solana airdrop 2` and then try again.

> Run `solana address` to get the user account address, and `solana balance [address]` for viewing the amount of SOL in the account.

The following command deploys after running tests located in `/tests/demo.ts`:
```sh
anchor test
```

---
- [SolDev](https://soldev.app/)
- [Solana Cookbook](https://solanacookbook.com/)
- [Documentation](https://docs.solana.com/)
- [Anchor](https://www.anchor-lang.com/docs/high-level-overview)