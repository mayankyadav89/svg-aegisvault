# Sources

## S-001
- Title: RIP-7212: Precompile for secp256r1 Curve Support
- Author/Org: ethereum/RIPs
- URL: https://github.com/ethereum/RIPs/blob/master/RIPS/rip-7212.md
- Source type: Primary specification
- Relevant section: Specification, Precompiled Contract Specification, Gas
- Claim supported: Address 0x100, 160-byte input, success/failure return semantics, 3450 gas
- Confidence: High
- Access date: 2026-09-04
- Notes: Status marked Final.

## S-002
- Title: EIP-7951: Precompile for secp256r1 Curve Support
- Author/Org: ethereum/EIPs
- URL: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-7951.md
- Source type: Primary specification
- Relevant section: Input validation, output, gas
- Claim supported: 6900 gas, exact input-length rule, empty return on failure
- Confidence: High
- Access date: 2026-09-04
- Notes: Final; states security fixes relative to RIP-7212.

## S-003
- Title: Base Protocol Precompiles
- Author/Org: base/docs
- URL: https://github.com/base/docs/blob/master/docs/specifications/base-protocol/execution/precompiles.mdx
- Source type: Official network docs
- Relevant section: P256VERIFY table and address
- Claim supported: Base P256 precompile address and gas (Azul update)
- Confidence: High
- Access date: 2026-09-04
- Notes: Explicit Base-specific statement.

## S-004
- Title: Base Upgrades — Fjord Overview
- Author/Org: base/docs
- URL: https://github.com/base/docs/blob/master/docs/upgrades/fjord/overview.mdx
- Source type: Official network docs
- Relevant section: Execution Layer changes
- Claim supported: Fjord introduced RIP-7212 precompile; Sepolia activation timestamp
- Confidence: High
- Access date: 2026-09-04

## S-005
- Title: Base Upgrades — Azul Execution Engine
- Author/Org: base/docs
- URL: https://github.com/base/docs/blob/master/docs/upgrades/azul/exec-engine.mdx
- Source type: Official network docs
- Relevant section: secp256r1 precompile gas cost; eth_config notes
- Claim supported: Base gas moved from 3450 to 6900
- Confidence: High
- Access date: 2026-09-04

## S-006
- Title: Connect to Base
- Author/Org: base/docs
- URL: https://github.com/base/docs/blob/master/docs/get-started/connect-to-base.mdx
- Source type: Official network docs
- Relevant section: Network details table
- Claim supported: Base Sepolia chain ID 84532 and RPC URL
- Confidence: High
- Access date: 2026-09-04

## S-007
- Title: Base JSON-RPC eth_chainId
- Author/Org: base/docs
- URL: https://github.com/base/docs/blob/master/docs/base-chain/api-reference/ethereum-json-rpc-api/eth_chainId.mdx
- Source type: Official network docs
- Relevant section: Returns
- Claim supported: `0x14a34` for Base Sepolia
- Confidence: High
- Access date: 2026-09-04

## S-008
- Title: Web Authentication: Level 3 (spec source)
- Author/Org: W3C WebAuthn WG
- URL: https://github.com/w3c/webauthn/blob/main/index.bs
- Source type: Primary specification source
- Relevant section: authData layout; RP assertion verification; signature formats
- Claim supported: rpIdHash/flags/signCount formats, challenge/origin validation, signature verification inputs, DER signature requirement for ES256 assertion signatures
- Confidence: High
- Access date: 2026-09-04

## S-009
- Title: op-geth P256 precompile implementation
- Author/Org: ethereum-optimism/op-geth
- URL: https://github.com/ethereum-optimism/op-geth/blob/7da4560d1fb3045286b70a8dc23360d2626543f2/core/vm/contracts.go
- Source type: Reference implementation
- Relevant section: p256Verify Run/RequiredGas
- Claim supported: exact length check, return behavior, gas constants path
- Confidence: High
- Access date: 2026-09-04

## S-010
- Title: op-geth secp256r1 verifier
- Author/Org: ethereum-optimism/op-geth
- URL: https://github.com/ethereum-optimism/op-geth/blob/7da4560d1fb3045286b70a8dc23360d2626543f2/crypto/secp256r1/verifier.go
- Source type: Reference implementation
- Relevant section: Verify function
- Claim supported: on-curve check + ECDSA verify behavior
- Confidence: High
- Access date: 2026-09-04

## S-011
- Title: ERC-4337 (moved canonical file)
- Author/Org: ethereum/ercs
- URL: https://github.com/ethereum/ercs/blob/master/ERCS/erc-4337.md
- Source type: Primary specification
- Relevant section: Abstract, terminology, validation/bundler model
- Claim supported: UserOperation/EntryPoint/bundler/paymaster model
- Confidence: High
- Access date: 2026-09-04

## S-012
- Title: account-abstraction reference implementation README
- Author/Org: eth-infinitism/account-abstraction
- URL: https://github.com/eth-infinitism/account-abstraction/blob/develop/README.md
- Source type: Official implementation docs
- Relevant section: EntryPoint deployment note
- Claim supported: v0.8 EntryPoint address claim used by that project
- Confidence: Medium
- Access date: 2026-09-04
- Notes: Not sufficient alone for Base Sepolia deployment confirmation.
