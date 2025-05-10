---
icon: user-crown
---

# Usuario

El usuario es una abstraccion

```rust
struct User {
    chain: Chain,
    public_keychains Option<u256>, // this can be a vec!
    
    
}
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
