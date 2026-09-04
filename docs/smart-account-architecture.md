# Conceptual Smart-Account Architecture (Hypothesis)

## Hypothesized flow

User → Browser/Client → Passkey/WebAuthn → Assertion parsing/validation → P-256 verify path → Smart-account signature authorization → ERC-4337 UserOperation → Bundler → EntryPoint → AegisVault account → Base

## Per-step trust/validation model

| Component | Receives | Produces | Trusts | Must verify | Potentially malicious |
|---|---|---|---|---|---|
| Browser/client | dApp action request | WebAuthn request | WebAuthn API | origin/rp configuration | dApp/script context |
| Authenticator | challenge + rp context | assertion signature + authData | local UV/UP mechanisms | internal user intent | compromised device state |
| Backend/RP | clientDataJSON/authData/signature | verification decision | stored credential metadata | challenge/origin/rpIdHash/flags/signCount/signature | client payloads |
| On-chain precompile | hash,r,s,qx,qy | 32-byte success or empty failure | EVM precompile semantics | only tuple validity | calldata sender |
| Smart account | userOp and validated signature material | authorize/reject operation | EntryPoint invocation rules | nonce/domain/op-hash/account authorization | bundler/caller inputs |
| Bundler | userOps | bundle tx | local simulation | policy + simulation consistency | mempool peers |
| EntryPoint | bundle call | execution + accounting | account/paymaster code | ERC-4337 rules | account/paymaster bugs |

## Replay protection model (intended)

1. Off-chain WebAuthn challenge should be one-time and short-lived.
2. On-chain authorization should bind chain ID, EntryPoint, account, nonce, and operation hash.
3. Backend should detect signCount anomalies and enforce challenge invalidation.
