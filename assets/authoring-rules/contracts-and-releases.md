---
title: Contracts and Releases
document-id: SYSTEM-GOV-CONTRACTS-AND-RELEASES
document-type: governance
status: accepted
scope: system
---

# Contracts and Releases

Read this file when working on public contracts, their dependencies, or their releases. Read the [core authoring rules](../SPECIFICATION-AUTHORING-RULES.md) first and follow its routing for any additional concerns.

## Ownership of public contracts

Apply this section when the application exposes or consumes public contracts.

**CONTRACT-RELEASE-RULE-001:** Each public contract is owned by the component that provides it.

**CONTRACT-RELEASE-RULE-002:** Consumers must reference the provider's canonical contract rather than redefine it.

**CONTRACT-RELEASE-RULE-003:** Consumers may contain generated bindings, generated reference material, compatibility notes, and released contract artifacts. Generated or copied material must identify its source and version or revision and must not be edited as if it were canonical.

**CONTRACT-RELEASE-RULE-004:** A repository consuming separately released component contracts must maintain a machine-readable dependency register at `spec/contracts/dependencies.yaml`. Each entry identifies the stable contract identifier, provider, supported contract version, immutable release tag or revision, canonical artifact location, and artifact checksum. Internal contracts developed and released together may be referenced by stable document identifiers without this register.

**CONTRACT-RELEASE-RULE-005:** Metadata referencing a registered contract uses `<CONTRACT-ID>@<VERSION>`, for example `SERVICE-API@1.4.0`. Normative prose may reference stable operation, message, and type identifiers without reproducing their definitions as a competing source of truth.

**CONTRACT-RELEASE-RULE-006:** Verified snapshots, generated reference documentation, or generated bindings stored locally must identify their provider, contract identifier, source version or revision, artifact checksum, and generated or mirrored status. Update them from their canonical source rather than editing them manually.

**CONTRACT-RELEASE-RULE-007:** Where practical, public APIs must have a canonical machine-readable definition. Choose its format to suit the actual boundary and document which concerns it governs.

**CONTRACT-RELEASE-RULE-008:** Normative prose complements machine-readable definitions for behavior they cannot fully express, including lifecycle, invariants, ownership, errors, concurrency, and resource constraints where relevant. Both must describe the same interface and be authoritative for their distinct concerns.

**CONTRACT-RELEASE-RULE-009:** Human-readable API reference material must be generated from or checked against the canonical contract. Disagreement in material derived from the machine-readable definition is a defect; the canonical definition governs that derived material.

**CONTRACT-RELEASE-RULE-010:** Normative cross-repository references must target immutable revisions or released artifacts. A changing default branch must not be a normative dependency.

## Contract dependency validation

**CONTRACT-RELEASE-RULE-011:** When separately released contract dependencies exist, validation must cover dependency-register structure, artifact checksums, contract references, generated-artifact provenance, and required regeneration. Local checks should be deterministic and network-independent; they provide feedback rather than proof of remote release authenticity.

**CONTRACT-RELEASE-RULE-012:** Required CI checks for those dependencies must also verify immutable release provenance, ensure regeneration produces no unexplained changes, assess compatibility, and run applicable contract and integration tests. Define these checks when the contract tooling is introduced; boilerplate initialization does not create hooks, CI, or release automation.

A consumer need not adopt every provider release. Its dependency register records the exact supported release. Release checks verify that the versions intended to ship together are compatible.

## Product and API release versioning

Apply this section when public contracts are released to consumers.

**CONTRACT-RELEASE-RULE-013:** Document the contract's compatibility and versioning policy before release. When semantic versioning is used, major versions permit breaking changes, minor versions add backward-compatible behavior, and patch versions provide compatible corrections. Product, component, and contract versions may be independent; record their supported combinations explicitly.

**CONTRACT-RELEASE-RULE-014:** A released contract must identify the immutable tag or revision containing its exact specification and canonical definition. Consumers must depend on released artifacts rather than the changing default branch.

**CONTRACT-RELEASE-RULE-015:** Provider releases must make the canonical contract, release identifier, artifact checksum, and contract changelog available to consumers. Publish generated reference documentation and bindings when the toolchain supports them; generated bindings do not become canonical merely because they are distributed.

**CONTRACT-RELEASE-RULE-016:** Each released public contract must maintain a human-readable changelog describing additions, compatible changes, deprecations, removals, and breaking changes. Compare the canonical definition with the previous release and assess compatibility under the documented policy before release.

**CONTRACT-RELEASE-RULE-017:** Coordinate changes to providers, affected consumers, generated artifacts, tests, and changelogs. Document migration or coexistence when breaking changes require it. API version negotiation and where versions appear are project-specific contract decisions.

## Operation failure coverage

**CONTRACT-RELEASE-RULE-018:** Before accepting a public operation or adding a validation constraint, review every failure branch against the public error contract and any error registry the project maintains. Record the condition, error classification, effects on state and resources, structured data, and defined delivery mechanism. Include delayed or asynchronous failures where applicable. A branch with no defined mapping remains unresolved work and cannot be accepted as complete. Operation specifications, error definitions, and any applicable registry entries change together; contract checks verify their references and runtime failure behavior once an implementation exists.
