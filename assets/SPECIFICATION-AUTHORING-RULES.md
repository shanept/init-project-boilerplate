---
title: Specification Authoring Rules
document-id: SYSTEM-GOV-SPECIFICATION-AUTHORING
document-type: governance
status: accepted
scope: system
---

# Specification Authoring Rules

## Purpose and authority

These rules apply to specification material under `spec/`. Their purpose is to make the specification authoritative, navigable, internally consistent, and testable. Rules concerning public APIs, separate component repositories, or releases apply only when those concerns exist in the project; they do not require introducing them.

**SYSTEM-GOV-RULE-001:** If another specification document conflicts with these authoring rules, these rules govern how that conflict is handled. They do not decide the disputed application behavior. The conflict must be recorded as unresolved and corrected through the specification change process.

## Read rules for the current task

Read this core for specification or implementation work. Load the references below only when their conditions apply; several may apply to one task. Re-evaluate the conditions when the task's scope changes. The linked files are parts of this policy with the same authority within their stated concerns.

| When the task involves… | Read |
| --- | --- |
| Creating, editing, reviewing, or accepting specification documents, including governance documents | [Document authoring](authoring-rules/document-authoring.md) for structure, metadata, requirements, formatting, diagrams, and examples. |
| Defining, changing, reviewing, or accepting domain terminology or architectural decisions | [Domain terminology and decisions](authoring-rules/domain-and-decisions.md). |
| Defining, changing, reviewing, accepting, or implementing logical data types, field semantics, or boundary representations | [Data notation](authoring-rules/data-notation.md). |
| Providing or consuming public contracts, changing contract dependencies, or preparing contract releases | [Contracts and releases](authoring-rules/contracts-and-releases.md). |
| Implementing or changing application behavior, changing existing specifications, investigating bugs, or recording or resolving an unanswered design question | [Change workflows](authoring-rules/change-workflows.md). |
| Importing or reorganizing existing specification material, or changing the authoring policy itself | [Policy maintenance](authoring-rules/policy-maintenance.md). |

All paths written as `spec/...` in this policy are relative to the project root. Rule identifiers are unique across the policy set. Core rules use `SYSTEM-GOV-RULE`; conditional files use subject-specific prefixes and independent three-digit numbering starting at `001`. Refer to rules by their complete identifiers.

## Document lifecycle

**SYSTEM-GOV-RULE-002:** Active documents use one of these states:

- `draft`: incomplete and not ready for a decision;
- `proposed`: coherent and under review, but not authoritative; or
- `accepted`: approved and authoritative within its stated scope.

**SYSTEM-GOV-RULE-003:** Only accepted material defines committed application behavior or architecture. Draft and proposed material must not be presented as an accepted dependency.

**SYSTEM-GOV-RULE-004:** When accepted material is replaced or rejected, the default action is to delete it from the active specification. Before deletion, verify that the removed content is recoverable from version history; otherwise preserve it as explicitly non-authoritative historical material until an archive exists. A superseded document may remain temporarily only when an explicit migration need justifies it; it must be marked `deprecated`, identify its replacement, and be removed when that need ends.

**SYSTEM-GOV-RULE-005:** Historical material may remain in the working tree when required by `SYSTEM-GOV-RULE-004`'s archival safeguard or by explicit exception. It must be marked `historical`, isolated from active specifications, and state that it is non-authoritative. Names such as `OLD`, `legacy`, or `ticked` do not establish lifecycle status.

## Consistency and precedence

**SYSTEM-GOV-RULE-006:** There is no implicit "more specific document wins" rule. Two accepted documents that prescribe incompatible behavior constitute a specification defect.

When documents disagree:

1. **SYSTEM-GOV-RULE-007:** The agent must not silently choose one interpretation.
2. **SYSTEM-GOV-RULE-008:** The agent must identify each conflicting document and requirement or contract identifier.
3. **SYSTEM-GOV-RULE-009:** The agent must explain the conflicting interpretations and their known consequences.
4. **SYSTEM-GOV-RULE-010:** The agent must record the conflict as unresolved specification work under [Unresolved work](authoring-rules/change-workflows.md#unresolved-work).
5. **SYSTEM-GOV-RULE-011:** The agent must stop work whose correctness depends on the answer and elevate the conflict to a human, unless already explicitly authorized to resolve that class of decision. Independent work may continue.
6. **SYSTEM-GOV-RULE-012:** A human, or an agent acting within that human's explicit delegation, must determine the correct interpretation.
7. **SYSTEM-GOV-RULE-013:** After the decision, every affected document must be updated or deleted in the same specification change.

**SYSTEM-GOV-RULE-014:** An agent may correct an unambiguous mechanical defect, such as a broken link or typographical error, without escalation. Choices of product behavior, architecture, API semantics, or requirement precedence require human direction or an explicit delegation covering that decision.

**SYSTEM-GOV-RULE-015:** Within an API, the canonical machine-readable contract governs generated or explanatory API material. This limited precedence rule does not authorize a contract to override accepted product or architecture requirements silently; such disagreement is still a defect.

## Acceptance checklist

**SYSTEM-GOV-RULE-016:** A document may move to `accepted` only when:

- its metadata is complete and valid;
- its concern and owning scope are unambiguous;
- its terminology agrees with the canonical glossary and any applicable local definitions;
- every normative requirement is identified and verifiable;
- normative and informative content are distinguishable;
- it contains no unresolved markers presented as decisions;
- it neither duplicates nor contradicts an accepted source of truth;
- all references resolve;
- its diagrams and examples agree with its requirements;
- relevant public contracts are synchronized;
- it can be understood with only the dependencies permitted by the repository model; and
- acceptance is supported by a human decision or explicit delegated authority; passing this checklist alone does not grant approval.
