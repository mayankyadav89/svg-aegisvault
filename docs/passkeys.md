# Passkeys and WebAuthn Relationship

## Terminology mapping

- **Passkeys**: user-facing FIDO credentials, typically multi-device credentials.
- **WebAuthn**: browser/API and server validation model.
- **FIDO2**: broader ecosystem including CTAP and authenticator behavior.
- **P-256 / ES256**: common signing algorithm path used by many passkey credentials.

## Critical separation

`P256VERIFY` checks a cryptographic tuple (`hash,r,s,qx,qy`).

It does **not** by itself prove:
- challenge freshness
- origin validity
- RP ID binding
- credential binding to account identity
- user presence/verification policy compliance

## Signature representation

- WebAuthn ES256 signatures are DER-encoded ASN.1 ECDSA signature values.
- Precompile call expects scalar fields (`r`,`s`) as 32-byte integers.
- Therefore conversion/parsing is required before on-chain precompile use.
