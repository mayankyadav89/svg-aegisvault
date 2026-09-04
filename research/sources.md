# Sources

This document records the authoritative and implementation-level sources used for Phase 0 verification of AegisVault.

## Source hierarchy

Sources are evaluated in the following order:

1. Ethereum normative specifications (EIP/RIP)
2. Official Base documentation
3. Official WebAuthn/W3C specification
4. Official Ethereum/OP Stack/client implementation code
5. ERC-4337 / Ethereum account-abstraction specifications
6. Secondary sources only when necessary for context

A secondary source must not be treated as authoritative when a primary specification or implementation source is available.

---

## S-001 — RIP-7212: P-256 verification precompile

Title: RIP-7212 — Precompile for secp256r1 Curve Support

Publisher: Ethereum R&D / Ethereum RIPs

URL:
https://github.com/ethereum/RIPs/blob/master/RIPS/rip-7212.md

Used for:

- P256VERIFY precompile definition
- Precompile address `0x0100`
- 160-byte input format
- `hash || r || s || qx || qy`
- 32-byte success output
- Empty output on verification failure
- Historical gas cost of 3450 gas
- P-256/secp256r1 curve requirements
- `r` and `s` bounds
- Public-key point validation

Authority:

Normative protocol specification / historical specification.

Notes:

RIP-7212 is the original specification for the P-256 verification precompile. It is retained as an important compatibility reference, but newer implementations may follow EIP-7951 semantics where applicable.

---

## S-002 — Base protocol upgrade documentation

Publisher: Base

URL:
https://docs.base.org/base-chain/specs/upgrades/

Used for:

- Base network protocol upgrades
- Network-specific fork activation information
- Protocol configuration
- Gas and execution-layer changes
- Determining which Ethereum protocol changes are active on Base

Authority:

Official Base documentation.

Notes:

Network-specific protocol behavior must be established from Base documentation and, where necessary, confirmed against the actual execution client/runtime.

---

## S-003 — Base network / precompile documentation

Publisher: Base

URL:
https://docs.base.org/

Used for:

- Base execution-layer behavior
- Precompile support
- Network-specific protocol assumptions
- Base Sepolia environment information

Authority:

Official Base documentation.

Notes:

A documentation statement that a feature is supported is not by itself equivalent to empirical verification of the current Base Sepolia runtime. Runtime-critical assumptions must be independently tested where possible.

---

## S-004 — Base Sepolia network information

Publisher: Base

URL:
https://docs.base.org/base-chain/api-reference/rpc-overview

Used for:

- Base Sepolia network identification
- Chain ID `84532`
- Standard Base Sepolia RPC endpoint
- JSON-RPC availability and endpoint information

Expected network:

Base Sepolia

Decimal chain ID:

`84532`

Hexadecimal chain ID:

`0x14a34`

Standard RPC endpoint:

`https://sepolia.base.org`

Authority:

Official Base documentation.

---

## S-005 — EIP-7951: P256 verification precompile

Title: EIP-7951 — Precompile for secp256r1 Curve Support

Publisher: Ethereum Improvement Proposals

URL:
https://eips.ethereum.org/EIPS/eip-7951

Used for:

- Current P256VERIFY interface
- Precompile address `0x0100`
- 160-byte input format
- Message hash / r / s / qx / qy ordering
- Success return value
- Failure return value
- Input validation requirements
- Point-at-infinity rejection
- `r` and `s` bounds
- Public-key coordinate bounds
- Gas cost of 6900 gas
- No-revert failure semantics
- Compatibility with RIP-7212 interface

Authority:

Ethereum Improvement Proposal.

Important distinction:

EIP-7951 preserves the RIP-7212 interface while tightening security requirements.

Interface:

`hash(32) || r(32) || s(32) || qx(32) || qy(32)`

Total:

`160 bytes`

Success:

32-byte value equal to `1`

Failure:

empty returndata

Gas:

`6900`

---

## S-006 — Base JSON-RPC documentation

Title: Base RPC Overview

Publisher: Base

URL:
https://docs.base.org/base-chain/api-reference/rpc-overview

Used for:

- Base Sepolia RPC endpoint
- JSON-RPC methods
- `eth_call`
- Network identification
- Runtime verification methodology

Base Sepolia:

`https://sepolia.base.org`

Required runtime checks include:

- `eth_chainId`
- `eth_call`
- block/head queries
- precompile behavior

Authority:

Official Base documentation.

Runtime status:

The documentation establishes the endpoint, but a successful runtime call is still required for empirical verification.

---

## S-007 — Base `eth_chainId` documentation

Title: `eth_chainId`

Publisher: Base

URL:
https://docs.base.org/base-chain/api-reference/ethereum-json-rpc-api/eth_chainId

Used for:

- Chain ID verification
- Base Sepolia expected chain ID

Expected Base Sepolia response:

`0x14a34`

Decimal:

`84532`

Authority:

Official Base documentation.

Verification command:

```text
curl https://sepolia.base.org \
  -X POST \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}'
