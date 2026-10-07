---
title: Domain Terminology and Decisions
document-id: SYSTEM-GOV-DOMAIN-AND-DECISIONS
document-type: governance
status: accepted
scope: system
---

# Domain Terminology and Decisions

Read this file when defining, changing, reviewing, or accepting domain terminology or architectural decisions. Read the [core authoring rules](../SPECIFICATION-AUTHORING-RULES.md) first and follow its routing for any additional concerns.

## Glossary rules

**DOMAIN-DECISION-RULE-001:** `spec/CONTEXT.md` is the canonical domain glossary. It contains domain terminology rather than behavior, design notes, status reports, or API definitions and evolves as the application's terminology develops. The root `README.md` remains the project overview and references this file instead of duplicating definitions. A term used in only one document may be defined locally until a shared definition is needed.

**DOMAIN-DECISION-RULE-002:** Every glossary entry must define one canonical term, distinguish easily confused terms where necessary, avoid implementation details, and identify synonyms to avoid when inconsistent terminology is a risk.

**DOMAIN-DECISION-RULE-003:** Where separate component repositories exist, each must include the terminology needed to understand its component independently. Repeated definitions must identify their canonical owner and remain compatible across public contract boundaries.

**DOMAIN-DECISION-RULE-004:** Undefined, ambiguous, or conflicting terminology must be resolved before a document depending on it can be accepted.

## Architecture Decision Records

**DOMAIN-DECISION-RULE-005:** Use an ADR only when a decision is all of the following:

- costly to reverse;
- surprising or difficult to understand without its rationale; and
- the result of a meaningful trade-off among alternatives.

**DOMAIN-DECISION-RULE-006:** An ADR records context, considered alternatives, the decision, consequences, and decision status. The accepted behavior or constraint must also appear in the appropriate architecture, feature, or API specification.

**DOMAIN-DECISION-RULE-007:** ADRs belong in `spec/adr/` in the repository that owns the decision. Use a stable identifier such as `ADR-0001`, a descriptive level-one title, and explicit scope and decision status (`proposed`, `accepted`, `rejected`, or `superseded`). Include the sections Context, Alternatives, Decision, and Consequences; identify a replacement when superseded. Cross-component decisions must result in explicit constraints or contract changes in every affected specification; an ADR must not be the only source for required behavior.
