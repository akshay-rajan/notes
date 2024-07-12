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



