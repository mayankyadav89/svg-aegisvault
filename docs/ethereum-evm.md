# EVM / Precompile Research

## Precompile basics

- Precompiles are executed as native client code at reserved addresses, unlike regular bytecode contracts (CONFIRMED from Base precompile docs and op-geth implementation).

## Relevant call behavior

From op-geth `RunPrecompiledContract`:
- Gas is charged via `RequiredGas(input)`.
- If supplied gas is insufficient, execution returns out-of-gas error.
- Otherwise precompile `Run(input)` is executed.

## P256VERIFY implementation observations (op-geth reference)

- Input length check: exactly 160 bytes; any other length returns empty output (CONFIRMED in code).
- Successful verify returns 32-byte `1`.
- Failed verify returns empty output.
- No revert is produced by this path on invalid signature/input shape (CONFIRMED for this client implementation).

## ABI vs raw bytes

`P256VERIFY` expects raw concatenated 160 bytes, not ABI function-selector encoding (CONFIRMED from RIP/EIP + op-geth implementation).

## Contract vs precompile differences

- Regular contracts: bytecode-defined behavior, ABI-centric interfaces by convention.
- Precompiles: protocol/client-defined behavior, fixed addresses, often raw binary inputs/outputs.
