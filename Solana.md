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

## On-chain Development

Each solana cluster: `mainnet-beta`, `testnet`, `devnet` or `localnet` is effectively a single computer with a globally synchronized state.
Solana programs are most commonly written in Rust, typically with the **Anchor** Framework.
The framework handle common tasks like redirecting incoming instructions to the right instruction handler, deserializing data for incoming transactions, verifying accounts etc.

Each program is associated with an address, typically created during `anchor init`.
It's stored in the `target/deploy` directory.

**Instruction handlers** are crucial components of smart contracts which how the program should respond to specific instructions. 
Instruction handlers are like HTTP route handlers, and incoming transactions are like HTTP requests.
But instead of returning data, the handlers write their data to accounts on Solana.
Programs can transfer SOL, which will end up in user wallet addresses.
Programs store data as key-value pairs in Program-Derived Addresses (PDAs).



