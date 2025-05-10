---
icon: user-crown
---

# Usuario

El usuario es una abstraccion



### ✨ About the Name: `/api/user/`

Yes. It's _fancy_, mnemonic, and future-proof. I’d maybe document:

* `/api/user/<address>` — raw BTC or ETH address
* `/api/user/<pubkey>` — raw BTC compressed pubkey (33 bytes, hex)
* `/api/user/<ens>` — will resolve via `ethers.js` or `web3.js` (optional in v1)









```rust
struct User {
    chain: Chain,
    public_keychains Option<u256>, // this can be a vec!
    
    
}

// response for request to api/user/bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh
{
  "address": "bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh",
  "type": "bitcoin",
  "first_seen": "2022-04-10T15:33:00Z",
  "last_seen": "2025-05-10T10:14:00Z",
  "total_received_btc": "0.81234567",
  "total_sent_btc": "0.41234567",
  "balance_btc": "0.40000000",
  "tx_count": 34,
  "pubkeys": [
    {
      "pubkey": "03abcdef123...",
      "revealed_in_tx": "f83bc4..."
    }
  ],
  "history": [
    {
      "txid": "abc123...",
      "timestamp": "2024-03-02T13:00:00Z",
      "direction": "in",
      "amount_btc": "0.05"
    },
    ...
  ],
  "known_tags": ["Binance", "Whale Alert"]
}

GET /api/user/ # where identifier can be anything, auto-resolved
GET /api/user/type:ens/sigiloso.eth
GET /api/user/type:pubkey/03abc...
```



🧠 Design Overview: `/api/user/<ANY_IDENTIFIER>`

#### ✅ Supported Inputs:

You can design this endpoint to accept multiple identity types:

* **Bitcoin address** (`bc1...`, `1...`, `3...`)
* **Ethereum address** (`0x...`)
* **Public keys** (for BTC, only once revealed via spend)
* **ENS name** (`sigiloso.eth`)
* **Other identifiers** (in future: NEAR, Solana, etc.)

A good first move: normalize the identifier and redirect internally to the corresponding type resolver (BTC address → BTC profile view).
