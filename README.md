
# Offchain Minting

A proposal for the client-side implementation of offchain minting. 

## v1

The purpose of v1 is to allow us to meet our minting obligations to players. There are two primary state transitions required: minting tokens and burning tokens. 

Only certain token types (whether ERC721 or ERC20) should be available to mint - Immutable should not be able to mint CryptoKitties, for example. Preferably, this would be hard-enforced by the proof. 

Immutable should send the following request to mint either an ERC721 or ERC20 token.

```
// POST /mint?txid=1234
{
    "vault_id": "0x...", // ID of the vault to use for this token
    "token_id": "", // ID of the token to store within this vault
    "stark_key": "0x...", // Public key of vault owner
    "amount": 1 // Amount of the token to store in this vault
    "signature": { // Immtuable must sign
        "r": "",
        "s": ""
    }
}
```

Immutable should send the following request to burn either an ERC721 or ERC20 token. 

```
// POST /burn?txid=1234
{
    "vault_id": "0x..." // ID of the vault
    "amount": 100, // amount of the token to burn
    "signature": { // vault owner must sign
        "r": "",
        "s": ""
    }
}
```

Immutable must implement a custom ERC721 contract which will enable the StarkEx contract to mint tokens after a successful withdrawal. This, like traditional withdrawals, will be a two-step process: a user's withdrawal must first be included in a batch, then either the user must send a final transaction to actually mint the token in the contract. 

