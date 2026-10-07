---
title: Document Authoring
document-id: SYSTEM-GOV-DOCUMENT-AUTHORING
document-type: governance
status: accepted
scope: system
---

# Document Authoring

Read this file when creating, editing, reviewing, or accepting specification documents. Read the [core authoring rules](../SPECIFICATION-AUTHORING-RULES.md) first and follow its routing for any additional concerns.

## System boundaries and canonical names

**DOCUMENT-AUTHORING-RULE-001:** Define canonical component names and scope identifiers in the applicable architecture specification as boundaries are decided, and use them consistently. Use `system` for application-wide material and `cross-component` for obligations spanning identified components. A shorter name may be introduced locally only after its canonical name has been used. Component count, technology, and repository boundaries are project decisions, not prescribed by these rules.

## Repository model

**DOCUMENT-AUTHORING-RULE-002:** Store the governed specification under `spec/`. The `SPECIFICATION-AUTHORING-RULES.md` file at the top of that directory governs it. The root `README.md` presents the project overview based on the user's intent. Root `AGENTS.md` holds general agent instructions. Neither replaces an accepted behavioral specification. Other developer documentation is outside this governance scope unless explicitly included.

**DOCUMENT-AUTHORING-RULE-003:** When component boundaries exist, the architecture specification must identify each component's role, responsibilities, applicable system constraints, and the direction and ownership of public contracts. In a separate component repository, include the context needed to understand that component independently. Statements about another component are informative context and must not define its internal behavior.

**DOCUMENT-AUTHORING-RULE-004:** Each component specification must:

- define its own purpose, scope, responsibilities, and exclusions;
- define the terminology necessary to understand it;
- state its externally observable requirements and applicable system obligations;
- identify dependencies by their public contracts and, for separately released contracts, versions;
- remain understandable without inspecting the implementation; and
- avoid specifying another component's internal design.

When separate component repositories are used, specifications must remain independently understandable using the released contract dependencies they identify, without relying on relative filesystem links or unpublished prose in another repository.

**DOCUMENT-AUTHORING-RULE-005:** Necessary explanatory context may be repeated across repositories for independence, with its canonical owner identified. Repetition does not create a second contract definition. A system constraint applicable to several components must identify separately owned and verifiable component obligations where needed.

## Separation of concerns

**DOCUMENT-AUTHORING-RULE-006:** Each document must have one primary concern and one declared document type. A document must not become authoritative for unrelated concerns merely because it mentions them.

**DOCUMENT-AUTHORING-RULE-007:** The specification separates at least the following concerns:

- system and component architecture;
- feature behavior;
- API contracts;
- data models;
- quality requirements;
- architectural decision rationale;
- domain terminology;
- roadmap and prioritization;
- research and reference material; and
- unresolved work.

**DOCUMENT-AUTHORING-RULE-008:** Architecture documents define structural boundaries, responsibilities, relationships, and governing constraints. They do not contain the complete behavioral specification of individual features or commands. For example, the system architecture may identify a command system, but a command's inputs, preconditions, behavior, errors, and observable results belong in a separate feature specification.

**DOCUMENT-AUTHORING-RULE-009:** A lower-level document must reference applicable higher-level constraints rather than reproducing them as a potentially divergent rule. Brief contextual summaries are allowed when clearly identified as non-canonical summaries.

## Document taxonomy and location

**DOCUMENT-AUTHORING-RULE-010:** Authoritative and supporting material must be organized by concern. Use the following conceptual layout where the relevant material exists:

```text
spec/
  SPECIFICATION-AUTHORING-RULES.md
  CONTEXT.md
  authoring-rules/
  architecture/
  features/
  data-model/
  quality/
  api/
  contracts/
  adr/
  unresolved/
  roadmap/
  research/
```

**DOCUMENT-AUTHORING-RULE-011:** Within `spec/`, create additional files and directories only when they have content. The layout above describes locations for future material, not an initialization checklist. Omit irrelevant directories or add subdirectories when a body of material is too large to navigate as a flat list.

**DOCUMENT-AUTHORING-RULE-012:** The `data-model/` directory contains common logical types, structures, invariants, and relationships. Common types must be divided among focused documents according to what they describe rather than collected into one universal type file. For example, identifiers and measurement types may belong in separate documents when they concern different domain concepts.

**DOCUMENT-AUTHORING-RULE-013:** A type used by only one feature, command, or operation belongs in that feature's specification. A type used across multiple concerns belongs in the most narrowly scoped common data-model document that can own it without duplication. A type crossing an API boundary is canonically owned by the providing component's API contract.

Document types and their purposes are:

| `document-type` | Purpose | Normative? |
| --- | --- | --- |
| `governance` | Rules for maintaining the specification | Yes, within its stated governance scope |
| `architecture` | System or component structure, boundaries, and constraints | Yes when accepted |
| `feature-specification` | Observable behavior of a feature, workflow, or command | Yes when accepted |
| `api-contract` | Public operations, messages, types, errors, and compatibility rules | Yes when accepted |
| `data-model` | Defined concepts, structures, invariants, and relationships | Yes when accepted |
| `quality-requirements` | Testable non-functional requirements | Yes when accepted |
| `glossary` | Canonical domain vocabulary | Yes when accepted, for terminology only |
| `unresolved-design` | A specification question requiring a human decision | No |
| `roadmap` | Priority, sequencing, and delivery intent | No |
| `research` | Evidence, experiments, alternatives, and background material | No |

**DOCUMENT-AUTHORING-RULE-014:** Architecture Decision Records use the format defined in [Architecture Decision Records](domain-and-decisions.md#architecture-decision-records) rather than the general specification header. They explain why a consequential decision was made; they do not replace the resulting specification.

## Required document metadata

**DOCUMENT-AUTHORING-RULE-015:** Every Markdown document governed by these rules, except ADRs as defined in [Architecture Decision Records](domain-and-decisions.md#architecture-decision-records), must begin with YAML front matter. Example:

```yaml
---
title: Search Records
document-id: SYSTEM-FEATURE-SEARCH
document-type: feature-specification
status: draft
scope: system
---
```

The required fields are:

- `title`: the human-readable title, matching the document's level-one heading.
- **DOCUMENT-AUTHORING-RULE-016:** `document-id`: a stable, unique identifier. It must not change merely because the file is renamed or moved.
- `document-type`: one value defined in the taxonomy in [Document taxonomy and location](#document-taxonomy-and-location).
- `status`: one lifecycle state defined in [Document lifecycle](../SPECIFICATION-AUTHORING-RULES.md#document-lifecycle).
- `scope`: `system`, `cross-component`, or a component scope identifier established under [System boundaries and canonical names](#system-boundaries-and-canonical-names).

**DOCUMENT-AUTHORING-RULE-017:** Use these optional fields only when applicable:

```yaml
decision-refs:
  - ADR-0004
contract-refs:
  - SERVICE-API@1.4.0
supersedes:
  - SYSTEM-FEATURE-LOOKUP
affected-documents:
  - SYSTEM-DATA-RECORD
```

- `decision-refs` identifies ADRs that explain governing decisions.
- `contract-refs` identifies public contracts on which the document depends.
- `supersedes` identifies documents wholly replaced by this document.
- `affected-documents` identifies accepted or proposed documents whose content may change when an unresolved-design document is decided.

**DOCUMENT-AUTHORING-RULE-018:** Ownership and review dates are not required metadata. Document scope establishes the responsible area, and Git history records change dates when available. If the repository is not yet under version control, do not assume that change history is available. Release and compatibility conventions are defined under [Product and API release versioning](contracts-and-releases.md#product-and-api-release-versioning).

## Normative language and requirements

Requirement levels follow [RFC 2119 — Key words for use in RFCs to Indicate Requirement Levels](https://www.rfc-editor.org/info/rfc2119/), as clarified by [RFC 8174 — Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words](https://www.rfc-editor.org/info/rfc8174/); together they form BCP 14. The special keyword meanings apply only to uppercase forms; lowercase words retain their ordinary English meanings. Normative obligations may also be expressed without these keywords.

Use the following keywords consistently:

- **MUST** and **MUST NOT** express mandatory behavior.
- **SHOULD** and **SHOULD NOT** express a strong default from which a documented reason may justify departure.
- **MAY** expresses permitted optional behavior.

**DOCUMENT-AUTHORING-RULE-019:** Uppercase normative keywords must not be used casually in explanatory prose.

**DOCUMENT-AUTHORING-RULE-020:** Every testable product, component, or API requirement must have a stable requirement identifier. Use a readable identifier whose prefix indicates its owning scope and concern, for example:

```text
SYSTEM-SEARCH-001
SYSTEM-RECORD-STATE-003
SYSTEM-API-VALIDATION-002
```

**DOCUMENT-AUTHORING-RULE-021:** A requirement identifier must remain stable when wording is clarified without changing meaning. A materially different requirement receives a new identifier. Deleted identifiers must not be reused.

**DOCUMENT-AUTHORING-RULE-022:** Each normative requirement must be:

- owned by one declared scope (`system` or a component), or explicitly marked cross-component;
- expressed as one independently verifiable obligation;
- precise about inputs, preconditions, behavior, outputs, and failure behavior where applicable;
- free of implementation detail unless that implementation detail is itself an accepted constraint; and
- consistent with its referenced architecture and public contracts.

**DOCUMENT-AUTHORING-RULE-023:** Examples, rationale, diagrams, and notes are non-normative unless a requirement explicitly incorporates them.

## Structure of a specification document

**DOCUMENT-AUTHORING-RULE-024:** A normative specification must contain the sections relevant to its concern. When applicable, use this order:

1. Purpose
2. Scope
3. Out of scope
4. Terminology
5. Preconditions and invariants
6. Requirements or behavior
7. Inputs and outputs
8. Errors and failure behavior
9. Interactions and dependencies
10. Security and privacy considerations
11. Accessibility considerations
12. Performance or resource constraints
13. Acceptance criteria or verification
14. References

**DOCUMENT-AUTHORING-RULE-025:** Irrelevant sections must be omitted rather than filled with placeholders. A required decision that has not been made must be tracked as unresolved work; authors must not invent an answer to complete the template.

## Filenames, headings, and links

**DOCUMENT-AUTHORING-RULE-026:** Except for the fixed `SPECIFICATION-AUTHORING-RULES.md` and `CONTEXT.md` filenames, new authoritative filenames must:

- use lowercase ASCII `kebab-case.md`;
- describe the document's concern;
- avoid emoji, status labels, dates, and words such as `old`, `new`, `final`, or `ticked`; and
- use a numeric prefix only when a maintained reading order is meaningful.

**DOCUMENT-AUTHORING-RULE-027:** Every Markdown document must have exactly one level-one heading, matching its metadata title where title metadata is required. Heading levels must not be skipped.

**DOCUMENT-AUTHORING-RULE-028:** Links within a repository must be relative and must resolve. Links across repositories must target a stable, versioned published artifact or immutable repository revision, not a relative filesystem path or an unversioned branch location. Research links may point to live sources when clearly informative rather than normative.

**DOCUMENT-AUTHORING-RULE-029:** Documents must reference another specification by its title and stable document identifier on first use. Reference canonical requirements by identifier instead of duplicating normative text. Cross-repository context and separately owned obligations follow [Repository model](#repository-model).

## Diagrams, examples, and code

**DOCUMENT-AUTHORING-RULE-030:** Diagrams communicate relationships but are non-normative unless requirements explicitly define the depicted relationship. A diagram must use the same component names and boundaries as the surrounding text.

**DOCUMENT-AUTHORING-RULE-031:** Examples and code samples must be labeled as examples. They must conform to accepted requirements and contracts but do not create requirements that are absent from the normative text.

**DOCUMENT-AUTHORING-RULE-032:** Placeholder signatures, speculative types, and illustrative APIs must not appear indistinguishable from accepted API definitions.
