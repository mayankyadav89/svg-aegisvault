# Byte-Level Calldata and Encoding

## P256VERIFY input layout

- Total length: **160 bytes**
- Encoding: raw bytes, fixed-width, big-endian integer fields

| Offset | Length | Field | Meaning |
|---|---:|---|---|
| 0 | 32 | `hash` | message digest |
| 32 | 32 | `r` | ECDSA signature r |
| 64 | 32 | `s` | ECDSA signature s |
| 96 | 32 | `qx` | public key x |
| 128 | 32 | `qy` | public key y |

## Input rules

- No selector/ABI envelope.
- Exactly 160 bytes required.
- Field order is positional; wrong ordering changes semantics.

## WebAuthn-related encoding boundary

- WebAuthn ES256 signature is DER-encoded ASN.1 `Ecdsa-Sig-Value`.
- P256VERIFY needs scalar `r` and `s` fields, so DER parsing is required before call data assembly.
