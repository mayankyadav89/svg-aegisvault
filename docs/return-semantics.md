# Return and Failure Semantics

## Source basis

- RIP-7212 / EIP-7951 text
- Base precompile docs
- op-geth implementation (`core/vm/contracts.go`, `crypto/secp256r1/verifier.go`)

## Observed/Specified semantics

| Case | Expected behavior | Status |
|---|---|---|
| Valid signature | 32-byte return value `0x...01` | CONFIRMED (spec + code) |
| Invalid signature | empty return data | CONFIRMED (spec + code) |
| Invalid public key | empty return data | CONFIRMED (code path to `false`) |
| Invalid coordinates/off-curve | empty return data | CONFIRMED (code `IsOnCurve`) |
| Invalid `r` / `s` bounds | empty return data | CONFIRMED (ecdsa.Verify semantics + spec requirement) |
| Incorrect digest | empty return data | CONFIRMED (verification fails) |
| Empty calldata | empty return data (length != 160) | CONFIRMED in op-geth implementation |
| Too-short calldata | empty return data | CONFIRMED in op-geth implementation |
| Too-long calldata | empty return data | CONFIRMED in op-geth implementation |
| Malformed calldata length | empty return data | CONFIRMED in op-geth implementation |
| Out of gas | EVM call failure / out-of-gas | CONFIRMED from precompile dispatcher code |

## Important caveat

Live Base Sepolia runtime equivalence for each case is **UNKNOWN** in this environment due failed RPC connectivity.
