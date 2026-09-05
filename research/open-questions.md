# Open Questions

## Q-001
- Question: What does live Base Sepolia return for each malformed calldata variant at `0x100`?
- Why it matters: Determines exact failure semantics relied on by smart-account validation logic.
- Evidence: Specs + op-geth code, but no successful runtime calls in this environment.
- Next action: Run scripted `eth_call` test matrix from a network-enabled environment.
- Status: BLOCKING
- Blocking?: YES

## Q-002
- Question: What is current Base Sepolia head block/fork state during verification runs?
- Why it matters: Behavior can vary by upgrade/fork activation.
- Evidence: Base docs list upgrade activations; runtime head not queried.
- Next action: Query `eth_blockNumber`, `eth_config` (if exposed), and fork-dependent behavior.
- Status: BLOCKING
- Blocking?: YES

## Q-003
- Question: Which EntryPoint version/address is currently used by chosen Base Sepolia bundlers?
- Why it matters: UserOperation hashing/validation compatibility.
- Evidence: Generic ERC-4337 + reference implementation docs; no Base-specific runtime proof.
- Next action: Verify against bundler RPC and on-chain code hash.
- Status: BLOCKING
- Blocking?: YES

## Q-004
- Question: Are there Base Sepolia vs Base mainnet differences in P256VERIFY behavior beyond gas?
- Why it matters: Prevent environment-specific integration bugs.
- Evidence: Documentation suggests equivalence; no direct comparative calls executed.
- Next action: Execute identical vectors on both networks and compare returndata.
- Status: NON-BLOCKING
- Blocking?: NO
