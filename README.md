# Claw401

Deterministic wallet authentication for autonomous systems.

Claw401 implements the **X401** protocol – an Ed25519 challenge‑response standard designed for AI agents and high‑throughput infrastructure, with **zero private key exposure** and **deterministic verification** across SDKs.

---

### X401 at a glance

- **Deterministic Ed25519 verification**  
  Single, canonical signing format across TypeScript, Python, and Rust.

- **Zero key exposure**  
  Private keys never leave the client. Servers verify signatures only.

- **Replay resistant by design**  
  Nonces are single‑use, TTL‑bounded, and enforced via a replay cache.

- **Agent‑native**  
  Built for autonomous agents and tools – capability attestations, scoped sessions, and verifiable agent identity.

- **Chain‑agnostic core**  
  Solana‑first today, architected for multi‑chain verification.

---

### Install

```bash
# TypeScript
npm i @claw401/sdk

# Python
pip install claw401-sdk

# Rust
cargo add claw401-core

# CLI
cargo install claw401-cli
```

---

### What X401 gives you

#### 1. Challenge–response authentication

Issue a deterministic challenge, have the client sign locally, and verify server‑side without ever touching a private key.

- Canonical JSON payloads with sorted keys
- Explicit domain binding to prevent cross‑origin replay
- Configurable TTL and clock skew tolerance
- One‑time nonces enforced via replay cache

#### 2. Sessions and scoped access

Turn successful verifications into **scoped sessions** your services can rely on:

- Deterministic session IDs (no randomness post‑verification)
- Explicit scopes (e.g. `["read", "write"]`)
- Expiry semantics tuned for production workloads

#### 3. Agent attestations

Give autonomous agents a first‑class identity layer:

- Wallet‑signed capability graphs
- Verifiable agent IDs and versions
- No central registry required – everything is attested and self‑contained

---

### SDKs

#### TypeScript — `@claw401/sdk`

```ts
import { generateChallenge, verifySignature } from "@claw401/sdk";

const challenge = generateChallenge({
  domain: "app.example.com",
  ttl: 300,
});

const ok = await verifySignature({
  challenge,
  signature: sig,
  walletPubkey: pubkey,
});

if (ok.valid) {
  // authenticated wallet
}
```

#### Python — `claw401-sdk`

```python
from claw401 import generate_challenge, verify_signature

challenge = generate_challenge(
    domain="app.example.com",
    ttl=300,
)

result = verify_signature(
    challenge=challenge,
    signature=sig,
    wallet_pubkey=pubkey,
)

if result.valid:
    # authenticated wallet
    ...
```

#### Rust — `claw401-core`

```rust
use claw401_core::auth;

let challenge = auth::generate_challenge("app.example.com", 300)?;
let ok = auth::verify_signature(&challenge, &sig_bytes, &pubkey_bytes)?;

if ok.valid {
    // authenticated wallet
}
```

---

### CLI — `claw401-cli`

For quick inspection and ops workflows:

- Generate and verify challenges
- Issue and validate sessions
- Create and inspect agent attestations

```bash
claw401 help
claw401 challenge issue --domain app.example.com
claw401 challenge verify --file challenge.json --signature <base64> --pubkey <base58>
```

---

### Spec & docs

- Website: [claw401.xyz](https://claw401.xyz)
- Protocol spec: `/protocol` on the site
- Whitepaper: `/whitepaper`
- SDK docs: `/docs` → SDK usage

---

### Status

- TypeScript SDK: **live**
- Python SDK: **live**
- Rust core crate: **live**
- CLI: **live**
- X401 protocol spec: **v0.1**
- Token and on‑chain components: in progress

---

Claw401 is Apache‑2.0 licensed and built for teams who need **predictable, verifiable, and agent‑compatible** authentication primitives – not another opaque auth service.

