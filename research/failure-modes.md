# Failure Modes Matrix

| Component | Failure | Expected behavior | Actual behavior | Security impact | Mitigation | Status |
|---|---|---|---|---|---|---|
| P-256 | Invalid `r/s` | Fail verification | Spec/code indicate empty return | Auth bypass risk if mis-handled by caller | Treat empty return as failure only | PARTIAL |
| RIP-7212 | Non-160-byte calldata | Empty return | Spec/code indicate empty return | Parser confusion risk | Strict length checks before call | PARTIAL |
| WebAuthn | Origin mismatch | Reject assertion | Spec-defined reject path | Phishing risk | strict origin allowlist | OPEN |
| WebAuthn | Challenge replay | Reject assertion | Requires RP state | Replay risk | one-time challenge + expiry | OPEN |
| Smart Account | Missing nonce binding | Reject op | Not implemented yet | replay/authorization bypass | nonce + domain separation | OPEN |
| EntryPoint | Wrong version/address assumption | Validation mismatch/revert | Unknown on Base Sepolia | DoS / invalid signing domain | verify deployment + codehash | OPEN |
| Bundler | Malicious inclusion/simulation behavior | Robust handling | Not tested | griefing/DoS | multi-bundler strategy | OPEN |
| RPC | Dishonest/stale response | Detect mismatch | Not tested | bad decisions | multi-provider checks | OPEN |
| Frontend | XSS/injection | Prevent signing malicious data | Not implemented | account compromise | CSP/SRI/review | OPEN |
| Backend | Challenge policy bypass | Reject invalid assertion | Not implemented | replay/account takeover | hardening + auditing | OPEN |
| Passkey | Credential clone/device compromise | Risk-aware handling | Depends on signCount policies | unauthorized auth | signCount monitoring + recovery | OPEN |
| Nonce/replay protection | Cross-chain/account replay | Reject | Not implemented | unauthorized tx | chain/account/userOp binding | OPEN |
