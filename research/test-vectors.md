# Test Vectors

| ID | Description | Network | Chain ID | Target | Input | Expected | Actual | Status | Evidence | Date |
|---|---|---|---:|---|---|---|---|---|---|---|
| TV-001 | `eth_chainId` on Base Sepolia RPC | Base Sepolia | 84532 | RPC endpoint | JSON-RPC `eth_chainId` | `0x14a34` | n/a | NOT_EXECUTED | `curl: Could not resolve host: sepolia.base.org` | 2026-09-04 |
| TV-002 | Valid pubkey + valid signature to `0x100` | Base Sepolia | 84532 | `0x000...0100` | 160-byte `hash||r||s||qx||qy` | 32-byte `0x...01` | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-003 | Valid pubkey + invalid signature | Base Sepolia | 84532 | `0x000...0100` | 160-byte tuple | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-004 | Empty calldata | Base Sepolia | 84532 | `0x000...0100` | `0x` | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-005 | Too-short calldata | Base Sepolia | 84532 | `0x000...0100` | `<160 bytes` | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-006 | Too-long calldata | Base Sepolia | 84532 | `0x000...0100` | `>160 bytes` | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-007 | `r=0` boundary | Base Sepolia | 84532 | `0x000...0100` | 160-byte tuple | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-008 | `s=0` boundary | Base Sepolia | 84532 | `0x000...0100` | 160-byte tuple | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-009 | invalid coordinates/off-curve key | Base Sepolia | 84532 | `0x000...0100` | 160-byte tuple | empty returndata | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
| TV-010 | wrong field ordering | Base Sepolia | 84532 | `0x000...0100` | misordered 160-byte tuple | failure | n/a | NOT_EXECUTED | RPC DNS failure | 2026-09-04 |
