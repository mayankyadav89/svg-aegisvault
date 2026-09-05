# Threat Model (Phase 0)

## Trust boundaries

| Boundary | Trusted data | Untrusted data | Attacker capability | Validation requirement | Replay risk | Manipulation risk |
|---|---|---|---|---|---|---|
| User | Intent confirmations | UI clicks/context | Social engineering | explicit intent display + confirmation | Medium | High |
| Authenticator | Private key operations | Metadata from client | Cloned/emulated device | verify assertion semantics/signCount | Medium | Medium |
| Operating system | Platform APIs | App-level data | Malware/hooking | integrity hardening assumptions | Medium | High |
| Browser | WebAuthn API behavior | dApp content/origin | XSS/phishing | strict origin checks | High | High |
| Frontend | Build artifacts | runtime env inputs | Supply-chain/content injection | integrity + CSP + minimal privileges | Medium | High |
| Backend | Stored credential records | network/client inputs | API abuse/server compromise | strict assertion verification | High | High |
| RPC provider | Chain query transport | returned RPC results | stale/malicious response | multi-source verification | Medium | Medium |
| Bundler | UserOp inclusion semantics | mempool behavior | censorship/reordering | simulation + redundancy | Medium | Medium |
| EntryPoint | ERC-4337 validation logic | account/paymaster logic | griefing via edge UserOps | strict validateUserOp invariants | Medium | Medium |
| Smart account | contract code + storage | calldata/userOps | logic bugs/replay | nonce/domain/op-hash checks | High | High |
| Blockchain | consensus-finalized history | pending assumptions | reorg/latency effects | confirmation/finality strategy | Medium | Medium |

## Threat list

| Threat | Precondition | Impact | Likelihood | Mitigation | Residual risk | Status |
|---|---|---|---|---|---|---|
| Compromised passkey device | Device compromise | Unauthorized signing | Medium | Multi-credential recovery and revocation | Medium | OPEN |
| Phishing / origin confusion | User approves on malicious origin | Account takeover | High | enforce origin and RP ID validation | Medium | OPEN |
| Challenge replay | Challenge reuse | Assertion replay | Medium | one-time challenge + short expiry | Low-Med | OPEN |
| Signature replay | Missing nonce/domain binding | Unauthorized operations | High | account/UserOp nonce + domain separation | Medium | OPEN |
| Cross-chain replay | chain not bound | Wrong-chain execution | Medium | include chain+EntryPoint in signed domain | Low-Med | OPEN |
| Invalid curve/signature edge cases | parser mismatch | bypass/DoS | Medium | strict DER/range parsing and tests | Medium | OPEN |
| Bundler manipulation | adversarial bundler | griefing/ordering abuse | Medium | multi-bundler failover and limits | Medium | OPEN |
| RPC compromise | malicious/stale node | wrong decisions | Medium | cross-check providers | Medium | OPEN |
| Frontend compromise | XSS/supply-chain | malicious signing prompts | High | frontend hardening | Medium-High | OPEN |
| Backend compromise | server breach | policy bypass | High | least privilege + monitoring | Medium-High | OPEN |
