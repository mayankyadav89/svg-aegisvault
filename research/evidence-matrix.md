# Evidence Matrix

| ID | Claim | Status | Evidence | Source | Test | Risk |
| -- | ----- | ------ | -------- | ------ | ---- | ---- |
| E-001 | Base Sepolia chain ID is 84532 (`0x14a34`) | CONFIRMED | Base docs network table + eth_chainId docs | S-006, S-007 | Doc verification | Low |
| E-002 | Base includes P256VERIFY precompile | CONFIRMED | Base precompiles spec entry | S-003 | Doc verification | Med |
| E-003 | P256VERIFY address is `0x100` | CONFIRMED | RIP-7212 + Base precompile docs + op-geth maps | S-001, S-003, S-009 | Doc/code verification | High if wrong |
| E-004 | RIP-7212 calldata is 160-byte fixed tuple | CONFIRMED | RIP-7212 spec input definition | S-001 | Spec verification | High |
| E-005 | Base runtime currently follows same semantics at head | UNKNOWN | No successful RPC calls from environment | S-006 | NOT_EXECUTED | High |
| E-006 | Invalid input length returns empty data | CONFIRMED (op-geth impl) / UNKNOWN (live Base) | `len(input)!=160 => return nil` | S-009 | Code review | Med |
| E-007 | Gas was 3450 in RIP-7212/Fjord and 6900 in Azul/EIP-7951 alignment | CONFIRMED | Base upgrade docs + op-geth params + EIP-7951 | S-002, S-005, S-009 | Doc/code verification | Med |
| E-008 | WebAuthn assertion requires challenge/origin/rpIdHash/flags/signCount checks | CONFIRMED | RP verification algorithm in WebAuthn L3 | S-008 | Spec verification | High |
| E-009 | ES256 assertion signature uses ASN.1 DER Ecdsa-Sig-Value | CONFIRMED | WebAuthn signature format section | S-008 | Spec verification | High |
| E-010 | P256VERIFY alone is insufficient for full WebAuthn validation | CONFIRMED | WebAuthn required checks beyond signature | S-008 | Spec reasoning | High |
| E-011 | ERC-4337 canonical file moved to ethereum/ercs | CONFIRMED | EIP moved notice + ercs file | S-011 | Spec verification | Low |
| E-012 | Base Sepolia EntryPoint deployment for target version | UNKNOWN | No network-specific deployment proof retrieved | S-011, S-012 | NOT_EXECUTED | High |
