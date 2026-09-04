# WebAuthn Verification Boundaries

## Core relationship

- WebAuthn assertion verification is broader than P-256 signature checking (CONFIRMED).
- A valid P-256 signature alone is insufficient to accept a WebAuthn authentication event (CONFIRMED).

## Required RP-side checks (WebAuthn L3)

From the assertion verification algorithm:
- `type == "webauthn.get"`
- challenge matches request challenge (base64url)
- origin matches expected origin
- `rpIdHash` equals SHA-256(expected RP ID)
- UP flag set
- UV flag policy check
- signature verifies over `authenticatorData || SHA-256(clientDataJSON)`
- signCount replay/cloning checks

## Data formats

- `authenticatorData` has binary structure: rpIdHash(32), flags(1), signCount(4), optional trailing fields.
- `signCount` is 32-bit unsigned big-endian.
- `clientDataJSON` exact serialization must be preserved for hashing.

## Signature encoding

For ES256 and ECDSA-based assertion signatures, `sig` MUST be ASN.1 DER `Ecdsa-Sig-Value` (WebAuthn L3 section on signature formats).

## Consequence for on-chain integration

WebAuthn assertion signature generally requires DER parsing/conversion before feeding `(r,s)` to `P256VERIFY` (INFERRED, based on DER requirement vs precompile raw field interface).
