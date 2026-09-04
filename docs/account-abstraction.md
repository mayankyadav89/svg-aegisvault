# ERC-4337 Research

## Specification status

- EIP-4337 file in `ethereum/EIPs` is marked `status: Moved` (CONFIRMED).
- Current spec source is `ethereum/ercs` `ERCS/erc-4337.md` (CONFIRMED).
- ERC-4337 status in moved spec file: `Final` (CONFIRMED in ercs file metadata).

## Core model

- `UserOperation` objects are sent via an alt mempool.
- Bundlers submit `handleOps` to `EntryPoint`.
- Smart accounts validate signatures/nonces in `validateUserOp` flows.
- Paymasters may sponsor gas with additional validation paths.

## EntryPoint deployment

- `eth-infinitism/account-abstraction` README states EntryPoint v0.8 is deployed at `0x4337084d9e255ff0702461cf8895ce9e3b5ff108` on most networks.
- Base Sepolia-specific deployment verification from this environment: **UNKNOWN** (no successful RPC / no Base-specific deployment registry found in retrieved sources).

## Practical implication for AegisVault Phase 0

Do not hardcode EntryPoint or bundler assumptions without network-specific verification evidence.
