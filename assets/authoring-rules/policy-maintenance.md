---
title: Policy Maintenance
document-id: SYSTEM-GOV-POLICY-MAINTENANCE
document-type: governance
status: accepted
scope: system
---

# Policy Maintenance

Read this file when importing or reorganizing specification material, or changing this authoring policy. Read the [core authoring rules](../SPECIFICATION-AUTHORING-RULES.md) first and follow its routing for any additional concerns.

## Incorporating existing material

**POLICY-MAINTENANCE-RULE-001:** When importing or reorganizing existing material, classify every document or coherent section before incorporating it into the active specification. It must be:

- retained and normalized as accepted material;
- retained as draft or proposed material;
- split by concern and placed in the appropriate documents;
- converted to roadmap, research, glossary, ADR, or unresolved specification material; or
- deleted as superseded, contradictory, duplicate, obsolete, or otherwise unnecessary.

**POLICY-MAINTENANCE-RULE-002:** Existing location, filename, formatting, repetition, or apparent completeness does not establish authority. Remove superseded approaches from the active specification after resolving conflicts, using the lifecycle and archival safeguards in [Document lifecycle](../SPECIFICATION-AUTHORING-RULES.md#document-lifecycle).

**POLICY-MAINTENANCE-RULE-003:** Cleanup must preserve unresolved differences long enough to obtain a decision. Conflicting statements must not be merged into a new apparent consensus without review.

## Maintaining these authoring rules

**POLICY-MAINTENANCE-RULE-004:** This policy set is the project's maintained authoring guidance, not an immutable copy of the initialization template. Revisit relevant rules when application needs, specification structure, ownership, or contract practices change. A subsequent boilerplate run must preserve local revisions except where the user explicitly requests their revision or replacement.

**POLICY-MAINTENANCE-RULE-005:** A proposed policy change must identify its reason, affected rule identifiers, affected documents and tooling, and any migration work. Preserve identifiers for clarifications; assign new identifiers for materially changed obligations. Incorporate policy changes under the project's human or explicitly delegated decision authority. Mechanical corrections do not need a new policy decision.

**POLICY-MAINTENANCE-RULE-006:** Update affected specifications with the policy change, or record an explicitly authorized transition and its outstanding work. Changing an authoring rule does not itself decide disputed product behavior or retroactively accept draft specifications.
