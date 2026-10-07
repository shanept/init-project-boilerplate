---
title: Change Workflows
document-id: SYSTEM-GOV-CHANGE-WORKFLOWS
document-type: governance
status: accepted
scope: system
---

# Change Workflows

Read this file when implementing or changing application behavior, changing existing specifications, investigating bugs, or handling unresolved design questions. Read the [core authoring rules](../SPECIFICATION-AUTHORING-RULES.md) first and follow its routing for any additional concerns.

## Unresolved work

**CHANGE-WORKFLOW-RULE-001:** Unresolved design questions, missing decisions, and incomplete specification work are tracked within specification documents, not in the implementation issue tracker. The project's implementation issue tracker, when used, records implementation issues and bugs.

**CHANGE-WORKFLOW-RULE-002:** A question affecting one draft or proposed document must be recorded in that document under an `Unresolved questions` section. A substantial question affecting multiple documents or components must have its own `unresolved-design` document in `spec/unresolved/`.

A question about accepted behavior must be tracked separately in `spec/unresolved/`, referencing the accepted documents. Preserve their status while the decision is pending and pause work that depends on the disputed behavior under [Consistency and precedence](../SPECIFICATION-AUTHORING-RULES.md#consistency-and-precedence).

**CHANGE-WORKFLOW-RULE-003:** Every unresolved question must have a stable identifier using the form `UQ-<SCOPE>-<NUMBER>`, for example `UQ-SYSTEM-001`. It must state:

- the exact question requiring a decision;
- why the decision is required;
- the affected components, documents, requirements, and contracts;
- known constraints;
- alternatives already identified; and
- the consequences of those alternatives where known.

**CHANGE-WORKFLOW-RULE-004:** An unresolved-design document must use `status: proposed`. It is non-authoritative and must not be cited as an accepted behavioral dependency.

**CHANGE-WORKFLOW-RULE-005:** Accepted normative prose must not contain unresolved behavior or imply that a proposed answer has been decided. Markers such as `TODO`, `TBD`, `NEXT`, unchecked task lists, and conversational prompts are not permitted in accepted documents.

**CHANGE-WORKFLOW-RULE-006:** When a human or an explicitly authorized agent resolves a question, the decision must be incorporated into the appropriate specification or ADR. Remove the resolved question from active unresolved work after its decision is incorporated and its history is recoverable, following [Document lifecycle](../SPECIFICATION-AUTHORING-RULES.md#document-lifecycle).

**CHANGE-WORKFLOW-RULE-007:** An accepted document may state a deliberate and bounded omission when the omission itself has been accepted. This is not a substitute for recording an unknown as unresolved work.

## Change rules

**CHANGE-WORKFLOW-RULE-008:** A specification change must:

- identify its owning scope and concern;
- preserve stable identifiers when meaning is unchanged;
- assign new identifiers when behavior changes materially;
- update affected references, diagrams, examples, and generated artifacts;
- update the glossary when canonical terminology changes;
- update public contracts when externally observable behavior changes;
- identify compatibility and migration consequences for contract changes; and
- remove superseded material from the active specification with the archival safeguards in [Document lifecycle](../SPECIFICATION-AUTHORING-RULES.md#document-lifecycle).

**CHANGE-WORKFLOW-RULE-009:** Changes spanning component boundaries must be expressed as coordinated changes to the owning public contract and every affected component specification. Internal details remain in their owning component.

**CHANGE-WORKFLOW-RULE-010:** When a consumer adopts a different contract release, it must update its dependency register, verified local artifacts, generated bindings, affected specifications, implementation, and tests as one coordinated change.

## Bugs and specification corrections

**CHANGE-WORKFLOW-RULE-011:** The project's implementation issue tracker, when used, records reported bugs and implementation defects. A bug record must identify the affected feature or component and, where known, the applicable specification documents and requirement identifiers.

**CHANGE-WORKFLOW-RULE-012:** A permanent specification document must not normally be created for an individual bug. Apply the following classification:

| Finding | Specification action | Implementation action |
| --- | --- | --- |
| Code violates a correct specification | Do not change the intended requirement | Correct the code and add or update regression tests |
| Specification is ambiguous or incomplete | Clarify the owning specification after human approval or a decision within explicitly delegated authority | Update code and tests if the clarification affects them |
| Specification contradicts the intended behavior | Correct the owning specification after human approval or a decision within explicitly delegated authority | Update code and tests to conform |
| Reported bug is actually a requested behavior change | Accept the specification change before implementation | Implement the newly accepted behavior |
| Bug exposes a missing invariant | Add the invariant to the owning specification | Add regression coverage for the invariant |

**CHANGE-WORKFLOW-RULE-013:** The durable result of a bug belongs in the affected component, feature, data-model, architecture, or API specification. The issue records the particular defect and its resolution. An ADR is warranted only when resolving the bug requires a consequential architectural decision meeting [Architecture Decision Records](domain-and-decisions.md#architecture-decision-records)'s criteria.

**CHANGE-WORKFLOW-RULE-014:** An agent must not decide by itself that intended behavior should change merely because the implementation currently behaves differently. That decision requires human confirmation unless the agent has been explicitly authorized to make it.

## Keeping specifications and implementations synchronized

**CHANGE-WORKFLOW-RULE-015:** Keep the project's specification alongside its implementation. Where components have separate repositories, each repository owns its component's specification. Once implementation exists, accepted specifications and implementation at the same revision are expected to describe the same behavior, except for explicitly recorded staged delivery under `CHANGE-WORKFLOW-RULE-016`.

**CHANGE-WORKFLOW-RULE-016:** Once an implementation exists, a change to accepted behavior must update the affected specification, implementation, and tests in one coordinated change. A specification-only behavioral change must not be merged as accepted unless a human explicitly authorizes staged delivery and the outstanding implementation work and affected requirements are recorded in the project's implementation tracking mechanism.

**CHANGE-WORKFLOW-RULE-017:** Unit and integration tests must be organized using the same component, feature, command, or subsystem vocabulary as the specification so that their relationship is evident from repository structure and naming. Specification documents must not contain direct test-file mappings, because those mappings can become stale or misleading.

**CHANGE-WORKFLOW-RULE-018:** An agent beginning work without prior conversational context must:

1. read the applicable authoring rules, glossary, specifications, and ADRs;
2. inspect the working tree and, when Git is available, the relevant diff for uncommitted or proposed specification changes;
3. identify affected features, contracts, implementation areas, and test categories using stable document and requirement identifiers and canonical terminology;
4. treat an unexplained difference between accepted specification and implementation as a defect, not as permission to select either behavior; and
5. elevate behavioral uncertainty to a human under [Consistency and precedence](../SPECIFICATION-AUTHORING-RULES.md#consistency-and-precedence).

Git history detects that a specification changed, but cannot prove that code conforms semantically. Coordinated changes, human review, consistently organized tests, and automated contract validation provide the required control. Changes to the protected default branch should pass repository checks and review before merge.
