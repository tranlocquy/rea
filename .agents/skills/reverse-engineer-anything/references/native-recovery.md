# Evidence-led native source recovery

Use this workflow when the user requests native source reconstruction or
compiler matching. Ordinary feature investigation does not require compiler
reproduction. This adapts the recovery discipline of REA-PowerPCB without its
PowerPCB paths, compiler assumptions, or project-specific tools.

## Pin the artifact and reuse evidence

Record the caller-selected artifact's path, SHA-256, format, architecture, and
relevant image base. Recheck identity when resuming; a matching filename is
insufficient. Keep primary executables, launchers, and dependent libraries as
separate targets. Preserve installed files and retain derived artifacts under
their own identities. Do not execute a target merely to obtain static facts.

Reuse matching session evidence and exported bundles before repeating analysis.
Retain artifact identity, Evidence IDs, provider/version, operation, addresses,
timestamp, and limitations with each finding. Read the
[native guide](native-and-artifacts.md) for provider capabilities. Ghidra analysis
is ephemeral; Windows P0 admits no database mutations. Attached IDA databases
remain read-only and must never be saved or closed by the agent.

## Recover one bounded function

1. Select a bounded question or a small function with few dependencies. Retain
   instruction bytes and data references before writing a reconstruction.
2. Establish entry, body ranges, callers/callees, calling convention, and
   relevant data. A provider's reported size alone does not prove extent;
   discontiguous ranges, shared tails, padding, and embedded data need explicit
   treatment. Keep file offsets, RVAs, and loaded addresses distinct.
3. Separate observations from inferred identities and layouts. Use RVA-derived
   names until symbols, RTTI, type libraries, or call sites support a name.
   External automation contracts establish interfaces, not implementation.
   Record structure offsets, parameter roles, ABI evidence, and unresolved calls.
4. Write a readable source body in the user's selected language and project
   layout. Keep unsuccessful reconstructions separate from verified source.
   Preserve all proven aliases sharing an address; do not assume identical
   functions have distinct linker bodies.
5. When compiler matching is requested, establish a compiler, linker, flags,
   and dependency profile from corroborating evidence. Do not borrow a reference
   project's settings without verification. Compile and compare instructions,
   relocation targets, constants, strings, jump tables, and referenced data.
   Never mask arbitrary differences or omit relocated bytes merely to pass.
6. Retain the result and exact mismatch or missing evidence. Resolve reference
   identity and extent before adjusting layouts, literals, or instruction shape.
   Keep each completed change reviewable before expanding the scope.

## Record claims and coverage

Keep a project-owned function ledger using an existing format where available.
Each entry needs target SHA-256, RVA/body ranges, name, source, status, identity,
boundary and ABI evidence, verification report, and remaining gaps. These are
project records, not new REA tool fields or a built-in matching verifier.

- `recovered`: evidence-backed source interpretation; compiler equivalence is
  unproven. A decompiler dump or raw-byte lift does not count as readable source
  recovery.
- `behavioral_verified`: passed the retained finite behavioral checks; specify
  inputs, environment, and untested behavior. This does not establish byte equality.
- `byte_exact`: compiled bytes match the proven target extent, including validated
  relocation targets and referenced data. Retain a passing report binding target
  hash, current source hash, compiler profile, RVA/ranges, and actual object bytes.
  A missing compiler profile or stale report cannot support this claim.
- `partial` / `blocked`: retain the attempt and concrete unresolved evidence,
  dependencies, or toolchain requirement.

Count each covered RVA once per target. Separate application and third-party
library coverage, and exclude placeholders and generated dumps. Report measured
bytes and the denominator's provenance; unknown extent means unknown coverage.
Exact individual bodies do not establish a working replacement executable:
linking, symbol ownership, dependencies, and integration need separate evidence.

End each pass with changed coverage, retained evidence/report locations, and
unresolved work. Follow the user's commit and publication instructions; recovery
work alone does not authorize pushing artifacts or publishing vendor files.
