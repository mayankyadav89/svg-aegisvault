# Failure Modes Matrix

This document records security-relevant failure modes identified during Phase 0.

"Expected behavior" refers to the intended protocol/application behavior.
"Actual behavior" must only be marked as empirically verified when the behavior has been executed and observed on the target runtime.

| Component | Failure | Expected behavior | Actual behavior / Evidence | Security impact | Mitigation | Status |
|---|---|---|---|---|---|---|
| P-256 | Invalid `r` | Verification must fail | Specification/implementation indicate failure; Base Sepolia runtime NOT_EXECUTED | Authentication bypass if caller treats failure as success | Validate returndata and treat empty output as failure | PARTIAL |
| P-256 | Invalid `s` | Verification must fail | Specification/implementation indicate failure; Base Sepolia runtime NOT_EXECUTED | Authentication bypass if caller treats failure as success | Validate returndata and treat empty output as failure | PARTIAL |
| P-256 | Off-curve public key | Verification must fail | Specification/implementation reviewed; Base Sepolia runtime NOT_EXECUTED | Authentication bypass / undefined verification assumptions | Reject invalid points and verify runtime behavior | PARTIAL |
| P-256 | Point at infinity | Verification must fail | Specification-level requirement; runtime NOT_EXECUTED | Authentication bypass risk | Reject invalid public keys | PARTIAL |
| P-256 | Non-160-byte calldata | Verification must fail with empty returndata | Specification/implementation indicate empty return; runtime NOT_EXECUTED | Parser confusion / incorrect success handling | Enforce exact 160-byte input and validate returndata | PARTIAL |
| P-256 | Wrong field ordering | Verification must fail | Specification defines fixed field ordering; runtime NOT_EXECUTED | Incorrect signature interpretation | Construct calldata explicitly in canonical order | PARTIAL |
| P-256 | Empty calldata | Verification must fail | Specification/implementation indicate empty return; runtime NOT_EXECUTED | Incorrect caller assumptions | Treat empty returndata as failure | PARTIAL |
| P-256 | Malformed calldata | Verification must fail | Runtime NOT_EXECUTED | Unexpected execution behavior could cause incorrect authentication decisions | Exact-length checks before precompile call | OPEN |
| P-256 | Unexpected return length | Authentication must fail closed | Not runtime tested | Potential authentication bypass if caller accepts malformed output | Require exactly 32-byte successful output and value `1` | OPEN |
| WebAuthn | Origin mismatch | Assertion must be rejected | WebAuthn specification reviewed; end-to-end runtime NOT_EXECUTED | Phishing / origin-confusion attack | Strict origin allowlist and validation | OPEN |
| WebAuthn | RP ID mismatch | Assertion must be rejected | Specification reviewed; end-to-end test NOT_EXECUTED | Credential misuse / phishing risk | Validate RP ID and RP ID hash | OPEN |
| WebAuthn | Challenge mismatch | Assertion must be rejected | Specification reviewed; application implementation not present | Authentication bypass / replay | Bind challenge to server-side authentication request | OPEN |
| WebAuthn | Challenge replay | Replayed challenge must be rejected | Requires application state; not implemented | Replay / account takeover | One-time challenge with expiry and request binding | OPEN |
| WebAuthn | Invalid `clientDataJSON` | Assertion must be rejected | Not implemented | Authentication bypass | Strict parsing and validation | OPEN |
| WebAuthn | Invalid `authenticatorData` | Assertion must be rejected | Not implemented | Authentication bypass | Validate structure, RP ID hash, flags and required fields | OPEN |
| WebAuthn | User Presence requirement not satisfied | Assertion must be rejected when required | Policy not finalized | Unauthorized authentication | Define and enforce UP policy | OPEN |
| WebAuthn | User Verification requirement not satisfied | Assertion must be rejected when required by policy | Policy not finalized | Weaker authentication than intended | Define and enforce UV policy | OPEN |
| WebAuthn | DER signature malformed | Assertion must be rejected | DER parsing not implemented | Signature parser confusion / bypass | Strict DER parser with canonical validation | OPEN |
| WebAuthn | DER signature converted incorrectly to `r/s` | Cryptographic verification must fail closed | Not implemented | Authentication bypass | Dedicated parser + test vectors | OPEN |
| WebAuthn | Credential/public-key mismatch | Assertion must be rejected | Not implemented | Authentication bypass | Bind credential ID to registered public key | OPEN |
| WebAuthn | Sign counter regression | Apply documented clone/replay policy | Policy not finalized | Possible cloned authenticator / replay signal missed | Define signCount handling and recovery policy | OPEN |
| WebAuthn | Unsupported algorithm | Assertion must be rejected | Not implemented | Algorithm confusion | Explicitly allow only intended algorithms, e.g. ES256 | OPEN |
| Smart Account | Missing nonce binding | UserOperation must be rejected | Not implemented | Replay / authorization bypass | Use EntryPoint nonce semantics correctly | OPEN |
| Smart Account | Cross-chain replay | Operation must not be valid on unintended chain/domain | Not implemented | Unauthorized execution | Explicit domain separation and chain/account binding | OPEN |
| Smart Account | Cross-account replay | Signature must not authorize another account | Not implemented | Unauthorized execution | Bind signed data to account address | OPEN |
| Smart Account | Signature-domain mismatch | Signature must be rejected | Not implemented | Authorization bypass | Define canonical signing hash/domain | OPEN |
| EntryPoint | Wrong version | Account validation may fail safely; deployment must match intended interface | Unknown on Base Sepolia | DoS / broken account deployment | Verify exact EntryPoint version | OPEN |
| EntryPoint | Wrong address | Calls must not target an unintended contract | Unknown on Base Sepolia | DoS / potentially dangerous contract interaction | Verify deployment address and code | OPEN |
| EntryPoint | Unexpected bytecode | Deployment must not be trusted | Not verified | Security / compatibility risk | Verify deployed code and version | OPEN |
| EntryPoint | Validation behavior differs from assumptions | UserOperation must fail safely | Not tested | DoS / authorization risk | Test against target EntryPoint | OPEN |
| Bundler | Unsupported UserOperation | Operation should be rejected before execution | Not tested | DoS / availability | Test target bundler compatibility | OPEN |
| Bundler | Simulation mismatch | On-chain execution must not unexpectedly diverge from simulation assumptions | Not tested | DoS / failed operations | Test simulation/execution parity | OPEN |
| Bundler | Malicious or unreliable bundler | Account must remain secure even if bundler is untrusted | Not tested | DoS / censorship / griefing | Treat bundler as untrusted infrastructure | OPEN |
| Paymaster | Incorrect sponsorship assumptions | Operation must fail safely | Paymaster not selected | Unexpected gas/payment behavior | Do not depend on paymaster until verified | OPEN |
| RPC | Stale response | Application must not make security-critical decisions from stale state | Not tested | Incorrect authorization / nonce decisions | Use appropriate block/state validation | OPEN |
| RPC | Malicious RPC response | Application must not trust RPC as an authentication authority | Not tested | Incorrect state interpretation | Cross-check security-critical state where appropriate | OPEN |
| RPC | RPC unavailable | Authentication/transaction flow should fail safely | Base Sepolia RPC unavailable from test environment | Availability / operational risk | Multiple RPC providers and explicit failure handling | OPEN |
| Frontend | Signing malicious or misleading data | User must only sign clearly defined authorization data | Not implemented | Account compromise | Clear signing UX, domain separation, CSP and secure rendering | OPEN |
| Frontend | XSS/injection | Untrusted content must not execute in trusted origin | Not implemented | Credential/session compromise | CSP, output encoding, dependency/security review | OPEN |
| Backend | Challenge generation failure | Authentication request must not proceed with invalid/duplicate challenge | Not implemented | Replay / authentication bypass | Cryptographically secure random challenges with expiry | OPEN |
| Backend | Challenge storage failure | Authentication must fail closed | Not implemented | Replay / authentication bypass | Atomic storage and one-time consumption | OPEN |
| Backend | Challenge-policy bypass | Invalid assertion must be rejected | Not implemented | Account takeover | Centralize and strictly enforce verification policy | OPEN |
| Passkey | Credential loss | Recovery must follow documented policy | Not implemented | Account lockout | Recovery mechanism | OPEN |
| Passkey | Credential clone/device compromise | System should detect or limit suspicious behavior where possible | Depends on signCount and platform behavior | Unauthorized authentication | Sign-count monitoring plus recovery policy | OPEN |
| Replay protection | Reused authentication challenge | Reject reused challenge | Not implemented | Replay / account takeover | One-time challenge + expiry | OPEN |
| Replay protection | Reused UserOperation/signature | Reject according to nonce/domain rules | Not implemented | Unauthorized execution | Correct nonce and signing-domain design | OPEN |
| Replay protection | Cross-chain replay | Reject operation on unintended chain | Not implemented | Unauthorized execution | Chain/domain binding | OPEN |
| Replay protection | Cross-account replay | Reject signature for unintended account | Not implemented | Unauthorized execution | Account binding | OPEN |

## Status definitions

- `CONFIRMED` = supported by authoritative specification or implementation evidence
- `PARTIAL` = specification/implementation evidence exists but target-runtime behavior has not been empirically verified
- `OPEN` = implementation, policy, or runtime verification remains incomplete
- `NOT_EXECUTED` = a planned test could not be run
- `BLOCKING` = unresolved issue that prevents safe Phase 0 completion

## Phase 0 blocking failures

The following remain blocking:

1. Base Sepolia P256VERIFY runtime availability has not been empirically verified.
2. Base Sepolia P256VERIFY runtime semantics have not been empirically verified.
3. Base Sepolia runtime behavior for malformed and invalid inputs has not been empirically verified.
4. Exact ERC-4337 EntryPoint version and deployment remain unverified.
5. Bundler compatibility and simulation behavior remain unverified.
6. Complete WebAuthn assertion validation has not been implemented or tested.
7. Replay-protection policy has not been finalized or tested.
8. Reproducible cryptographic and WebAuthn test execution has not yet been completed.

## Security principle

All authentication and authorization failures must fail closed.

No empty returndata, malformed returndata, unexpected revert behavior, parser error, RPC error, or missing dependency should be interpreted as successful authentication.
