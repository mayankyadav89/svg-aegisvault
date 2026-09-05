# Security Considerations (Phase 0)

## Non-marketing status

This project is experimental. No audit or production-readiness claims are made.

## Key considerations

- P-256 verification does not validate WebAuthn origin/challenge context.
- DER parsing bugs can invalidate security assumptions.
- Replay protection needs multi-layer binding (challenge + nonce + domain).
- Bundler/paymaster/EntryPoint assumptions require adversarial testing.
- RPC trust and simulation mismatch can create execution risk.

## Privacy

Avoid unnecessary on-chain publication of passkey-linked identifiers. Public chain data is permanently observable.

## Recovery and upgradeability

Recovery and upgrade mechanisms are deferred to later phases and treated as high-risk boundaries.
