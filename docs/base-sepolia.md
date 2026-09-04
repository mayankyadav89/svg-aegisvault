# Base Sepolia Research

## Network identity

- Network: Base Sepolia testnet (CONFIRMED, Base docs)
- Chain ID: `84532` / `0x14a34` (CONFIRMED)
- Documented RPC endpoint: `https://sepolia.base.org` (CONFIRMED)
- EVM compatibility: documented as standard EVM-compatible (CONFIRMED)

## Upgrade and mechanism context

- Fjord introduced `P256VERIFY` on Base (CONFIRMED).
- Base docs state `P256VERIFY` remains at `0x100` and gas became `6900` in Azul (CONFIRMED).

## A–Z verification answers (Phase 0)

| Item | Answer | Status |
|---|---|---|
| A | Base Sepolia support for RIP-7212/P-256 mechanism is documented by Base | INFERRED runtime / CONFIRMED docs |
| B | Mechanism is `P256VERIFY` | CONFIRMED |
| C | Type is protocol precompile (native EVM implementation) | CONFIRMED |
| D | Address is `0x0000000000000000000000000000000000000100` | CONFIRMED |
| E | Address is specified in RIP/Base docs; live-node confirmation here | UNKNOWN |
| F | Calldata fields: `hash,r,s,qx,qy` | CONFIRMED |
| G | Input length is exactly 160 bytes | CONFIRMED |
| H | 32-byte digest, r, s, pubkey x, pubkey y | CONFIRMED |
| I | Big-endian integer encoding | CONFIRMED |
| J | Raw concatenated bytes, not ABI function selector call | CONFIRMED |
| K | Success return data is 32-byte word with value 1 | CONFIRMED |
| L | Success length 32 bytes; failure length 0 bytes | CONFIRMED |
| M | Success means signature verification passed | CONFIRMED |
| N | Failure means invalid signature or invalid input; empty returndata | CONFIRMED |
| O | Malformed calldata behavior on live Base Sepolia | UNKNOWN (NOT_EXECUTED) |
| P | Empty calldata behavior on live Base Sepolia | UNKNOWN (NOT_EXECUTED) |
| Q | Too-short calldata on live Base Sepolia | UNKNOWN (NOT_EXECUTED) |
| R | Too-long calldata on live Base Sepolia | UNKNOWN (NOT_EXECUTED) |
| S | Invalid public key expected to fail with empty returndata | CONFIRMED spec/impl, UNKNOWN live |
| T | Invalid curve coordinates expected to fail | CONFIRMED spec/impl, UNKNOWN live |
| U | Invalid r/s expected to fail | CONFIRMED spec/impl, UNKNOWN live |
| V | Invalid signature expected to fail | CONFIRMED spec/impl, UNKNOWN live |
| W | Incorrect digest expected to fail | CONFIRMED spec/impl, UNKNOWN live |
| X | Gas: RIP-7212 historical 3450; Base post-Azul documented 6900 | CONFIRMED docs/impl |
| Y | Live Base Sepolia vs specification exact match | UNKNOWN (NOT_EXECUTED) |
| Z | Differences across Base Sepolia/Base mainnet/Ethereum include rollout timing and gas evolution (3450→6900); exact runtime parity now | PARTIAL / UNKNOWN |

## Empirical verification attempts

No successful live RPC calls were executed from this environment.

Evidence: `curl` to `https://sepolia.base.org` and alternate public RPC endpoints failed with `Could not resolve host`.
