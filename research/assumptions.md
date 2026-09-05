# Assumptions Register

## A-001
- Assumption: Base Sepolia supports RIP-7212-compatible P-256 verification.
- Status: INFERRED
- Evidence: Base protocol docs + OP implementation references.
- Verification method: `eth_call` to `0x100` on Base Sepolia with known vectors.
- Risk: High
- Blocking?: YES
- Last reviewed: 2026-09-04

## A-002
- Assumption: Target address is `0x0000000000000000000000000000000000000100`.
- Status: CONFIRMED (spec/docs), UNKNOWN (live runtime from this environment)
- Evidence: RIP-7212, Base precompile spec, op-geth mapping.
- Verification method: direct `eth_call` and `eth_config`/client-level inspection.
- Risk: High
- Blocking?: YES
- Last reviewed: 2026-09-04

## A-003
- Assumption: Calldata format is `hash||r||s||qx||qy` exactly 160 bytes.
- Status: CONFIRMED (spec + implementation)
- Evidence: RIP-7212/EIP-7951 and op-geth `Run`.
- Verification method: length-variant call vectors.
- Risk: High
- Blocking?: YES
- Last reviewed: 2026-09-04

## A-004
- Assumption: Failure returns empty bytes (not boolean false/revert) for invalid signatures/inputs.
- Status: CONFIRMED (spec + implementation), UNKNOWN (live runtime verification)
- Evidence: RIP/EIP text, op-geth code.
- Verification method: invalid vectors via `eth_call`.
- Risk: High
- Blocking?: YES
- Last reviewed: 2026-09-04

## A-005
- Assumption: WebAuthn ES256 signature can be directly fed into P256VERIFY.
- Status: WRONG
- Evidence: WebAuthn requires DER Ecdsa-Sig-Value while precompile consumes raw r/s fields.
- Verification method: DER parser/unit vectors.
- Risk: High
- Blocking?: YES
- Last reviewed: 2026-09-04
