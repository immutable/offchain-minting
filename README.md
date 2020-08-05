
# Offchain Minting

A proposal for the client-side implementation of offchain minting. 

## v1

The purpose of v1 is to allow us to meet our minting obligations to players. There are two primary state transitions required: minting tokens and burning tokens. 

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
// POST /gateway/burn?txid=1234
{
    "vault_id": "0x..." // ID of the vault
    "signature": { // user must sign
        "r": "",
        "s": ""
    }
}
```

