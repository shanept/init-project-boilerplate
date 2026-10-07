---
name: init-project-boilerplate
description: Initialize a new coding project's directory structure and foundational documents for AI-assisted, specification-driven development. Use when preparing a new project for specification work before implementation.
---

# Initialize project boilerplate

Prepare a consistent, technology-independent foundation for describing an application before generating its code. This skill completes project initialization; detailed specification and implementation are subsequent work.

## 1. Establish the project directory

Use the directory supplied by the user or the current working directory when it is clearly the intended project root. Ask for the destination only when it is ambiguous.

Read applicable repository instructions and inspect the destination, including hidden files and directories, before making changes. Create the directory if it does not exist.

The destination should be empty. If it contains anything, including Git metadata or files from an earlier initialization, summarize the contents and discuss the user's intended outcome before writing. Clarify whether this is the correct directory and whether they want a different destination, only missing boilerplate added, or particular existing documents updated. A confirmation of the path alone does not settle how existing content should be handled.

Agree which paths may be created or changed and which must be preserved. Inspect the affected existing documents to make that scope concrete. If the user's current instructions already settle these choices, use that authorization without asking them to repeat it. Until the scope is clear, leave the destination unchanged. Apply this process to repeated runs as well; infer neither permission to overwrite nor a requirement to update every file.

## 2. Capture the project intent

Use any explanation the user has already provided. Otherwise, ask for a short description of what the application should do, who it serves, and the problem it solves.

Ask where bugs and implementation issues will be reported and tracked, unless the user has already supplied that information. Capture the tracker or reporting method and its project URL, repository, board, or local file location, as applicable. Include any stated reporting conventions. The user may choose no tracker or explicitly defer the choice; record that answer without selecting a service on their behalf. Include this question with the project-description request when both answers are needed.

Ask focused follow-up questions only when an ambiguity would materially change the initial project description. Record unresolved details as open questions rather than inventing requirements. A technology stack is not required to initialize the project.

Carry forward explicit constraints and decisions, keeping confirmed facts separate from assumptions and open questions.

## 3. Create the foundation

Initialize this structure in the project root:

```text
<project-root>/
├── spec/
│   ├── CONTEXT.md
│   ├── SPECIFICATION-AUTHORING-RULES.md
│   └── authoring-rules/
│       ├── document-authoring.md
│       ├── domain-and-decisions.md
│       ├── data-notation.md
│       ├── contracts-and-releases.md
│       ├── change-workflows.md
│       └── policy-maintenance.md
├── src/
├── .gitignore
├── AGENTS.md
└── README.md
```

Use the following responsibilities when preparing the files:

| Path | Responsibility |
| --- | --- |
| `spec/` | Specification authoring rules and the application requirements, behavior, and acceptance criteria developed during subsequent specification work. |
| `spec/CONTEXT.md` | Canonical domain terminology used by the specifications, maintained as the application's domain becomes clearer. |
| `spec/SPECIFICATION-AUTHORING-RULES.md` | Rules the agent must follow when creating or modifying application specifications. These rules evolve as the application's needs change. |
| `spec/authoring-rules/` | Conditional policy references selected by the core authoring rules for the current task. |
| `src/` | Application source code produced during subsequent implementation work. |
| `.gitignore` | Ignore rules appropriate to the known project environment. Keep rules narrow so project documents and intended source files remain trackable. |
| `AGENTS.md` | Instructions for coding agents working in this project, including where to find project context and specifications, and how to handle missing or conflicting requirements. |
| `README.md` | A project overview generated from the user's input. |

For a fresh project, create the complete structure above. For a non-empty destination, apply only the scope agreed in step 1; preserve everything outside it, including existing source code. Reconcile existing project guidance only where the user has requested an update.

Read the bundled [core authoring rules](assets/SPECIFICATION-AUTHORING-RULES.md) and copy it to `spec/SPECIFICATION-AUTHORING-RULES.md`. Copy the complete `assets/authoring-rules/` directory to `spec/authoring-rules/`, preserving relative paths and full contents. Copying unchanged references does not require loading them all into context. Follow the core routing table to read only those needed for the documents being generated or changed. If a required bundled file is unavailable, report initialization as incomplete rather than inventing a replacement.

The template's accepted governance status establishes the initial authoring policy when this skill is used; it does not approve application requirements, architecture, or implementation choices.

Read the bundled [agent instructions template](assets/AGENTS.md) and copy it to the project root as `AGENTS.md`. Its relative links are written for that destination. Add project-specific working conventions only when supported by the user's instructions or confirmed decisions, and preserve its pointer to the current project authoring rules. If the template is unavailable, report initialization as incomplete rather than inventing a replacement.

In the generated `AGENTS.md`, replace the issue-tracking setting with the user's answer, including the exact destination and any reporting conventions. If the user chooses no tracker or defers the decision, state that explicitly. Retain the source-control and commit guidance, adapting it to any commit, branch, or review conventions the user has supplied. Recording a tracker does not require creating or configuring one during initialization.

Generate the root `README.md` from the user's project description, confirmed decisions, and constraints. Include the available purpose, intended users, scope, and open project questions, using only sections supported by that information. Distinguish intended capabilities from functionality already implemented. Add useful specification links as their targets are created; setup and usage instructions belong here once they are established and verifiable.

Generate `spec/CONTEXT.md` as the specification's domain glossary using the terminology established by the user's explanation. Follow the core routing for document-authoring and domain rules, including metadata and lifecycle status. If no domain terms have been established, state that without inventing definitions. Link to it from `README.md` and `AGENTS.md`.

Keep specification authoring rules in their governing file, the project overview in `README.md`, domain definitions in `spec/CONTEXT.md`, and general agent working instructions in `AGENTS.md`. Link to the authoritative document instead of repeating its contents. Detailed application requirements belong in `spec/` when they are developed.

Ongoing project-document maintenance is directed by the generated `AGENTS.md`; policy changes follow the core file's pointer to policy maintenance.

Tailor newly created documents to the user's explanation. Describe unknown details explicitly; do not present assumed features, architecture, dependencies, or technology choices as decisions.

For a fresh project, leave `src/` empty and generate only the foundational documents above. Detailed application specifications are subsequent work. Keep framework scaffolding, dependency installation, application code, and Git repository initialization outside this skill's scope unless separately requested.

## 4. Verify and hand off

For a fresh project, verify every path above exists with its expected type and `src/` is empty. For a clarified non-empty destination, verify every agreed creation or update and confirm that preserved files and source code remain unchanged. Judge preserved documents against the agreed scope rather than requiring them to match current templates.

For generated or updated documents, check the following:

- They reflect supplied project intent and confirmed decisions.
- The authoring policy and `AGENTS.md` use the bundled resources with only justified adaptations.
- All local links resolve, including the core policy's conditional references and the pointers from `AGENTS.md`.

When creating or updating `AGENTS.md`, check that it records the user's issue-tracking choice or explicit deferral and contains the applicable commit conventions. An unanswered intake question is not an explicit deferral.

When creating or updating `README.md`, check that it reflects the user's supplied intent, separates planned from implemented capabilities, and contains no invented setup instructions or links to documents that do not yet exist.

When creating or updating `spec/CONTEXT.md`, check that it follows the glossary rules. Generated or updated project overviews and agent instructions must link to it. Report missing links in preserved documents as follow-up work rather than modifying those documents outside the agreed scope.

Report:

- The project directory and the paths created or preserved.
- Any conflicts or missing items that prevent initialization from being complete.
- Any open questions relevant to beginning specification work.

Fresh initialization is complete only when every applicable check above passes. For a non-empty destination, completion means the clarified scope and its checks are satisfied; state any intentionally omitted foundation items so a partial update is not presented as full initialization. Report unresolved conflicts or failed checks as incomplete. A complete foundation establishes readiness for specification work, not readiness for code generation.
