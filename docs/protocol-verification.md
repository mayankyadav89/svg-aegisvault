# Protocol Verification Plan (Phase 0)

## Scope

Phase 0 verifies assumptions before wallet implementation.

## Classification

- **CONFIRMED**: Supported by specification text and/or reproducible evidence.
- **INFERRED**: Reasonable conclusion, not directly proven on live Base Sepolia from this environment.
- **UNKNOWN**: Insufficient evidence.
- **CONFLICT**: Reliable sources disagree.

## Core verification target

Determine whether Base Sepolia supports secp256r1 (`P256VERIFY`) at EVM level and document exact byte/return semantics.

## Execution summary

1. Repository inspection completed.
2. Base and RIP/EIP/WebAuthn/4337 sources collected.
3. Live Base Sepolia RPC tests attempted but blocked by DNS in this environment.
4. Required research docs and matrices created.

## Roadmap

- Phase 0 — Protocol verification
- Phase 1 — Cryptographic/WebAuthn prototype
- Phase 2 — Minimal smart account
- Phase 3 — ERC-4337 integration
- Phase 4 — Base Sepolia end-to-end testing
- Phase 5 — Adversarial testing and fuzzing
- Phase 6 — Security hardening
- Phase 7 — External security review
- Phase 8 — Production-readiness assessment
