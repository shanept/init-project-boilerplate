# Agent Working Instructions

This project uses specification-driven development. Establish the intended behavior in the specification before generating or changing the application code that implements it.

## 1. Establish context

Read [README.md](README.md) for the project's purpose, scope, confirmed decisions, and open questions. Inspect the relevant files and any working-tree changes before editing; preserve work unrelated to the task.

For specification or implementation work, read the [core Specification Authoring Rules](spec/SPECIFICATION-AUTHORING-RULES.md) and [domain context](spec/CONTEXT.md). Use the core routing table to load only the conditional policy files needed for the current task, revisiting it when the scope changes. Then locate the relevant specifications, contracts, and decision records. Check document status and use stable document and requirement identifiers to identify the behavior being addressed.

Read additional `AGENTS.md` files applicable to the directories being changed. Discover build, test, and formatting commands from the project's maintained configuration when those tools exist.

## 2. Use each document for its intended purpose

| Location | Purpose |
| --- | --- |
| `AGENTS.md` | Agent workflow and project working conventions. |
| `README.md` | Project overview based on the user's intent, maintained as specifications and implementation evolve. |
| `spec/CONTEXT.md` | Canonical domain terminology for the specifications, maintained under the glossary rules. |
| `spec/SPECIFICATION-AUTHORING-RULES.md` | Core authority, lifecycle, and conflict rules, plus conditional policy routing. |
| `spec/authoring-rules/` | Detailed policy loaded for the concerns selected by the core routing table. |
| Other documents in `spec/` | Requirements, architecture, public contracts, terminology, rationale, and unresolved specification work, according to their declared type and status. |
| `src/` | Application implementation. |

Keep authoritative information in its owning document and reference it elsewhere. Project summaries, research, examples, and existing code do not independently establish accepted product behavior. Follow the authoring rules for document lifecycle, requirement identifiers, ownership, conflict resolution, and coordinated changes rather than redefining those policies here.

## 3. Establish readiness before implementation

For the requested scope, identify the accepted requirements, observable outcomes, relevant failure behavior, and applicable constraints before implementing them. Readiness applies to the work being undertaken; unrelated specifications may remain unfinished.

When the requested behavior is new or insufficiently specified, develop or update its owning specification first. Use the user's explicit decisions and any delegated decision authority already provided. Resolve missing decisions through the authoring rules' unresolved-work process; continue independent work while an answer is pending. Ask only for decisions or authorization that remain outstanding.

An initialized directory is ready for specification work. The presence of `src/` or an accepted authoring-policy document does not establish application requirements or select a technology stack. Introduce framework scaffolding and dependencies when implementation is requested and the applicable technology choices are established within the task's authority.

## 4. Implement and verify the requested change

Make implementation choices within accepted behavior and constraints. When a choice would establish new product behavior, architecture, or contract semantics, handle it as a specification decision under the authoring rules.

Keep affected specifications, contracts, implementation, and tests synchronized using the authoring rules' change process. For reported bugs, use its bug-classification guidance to distinguish an implementation defect from a missing or incorrect requirement. If sources disagree, follow its conflict-resolution process before continuing dependent work.

Derive verification from the affected requirements and their acceptance criteria. Exercise relevant success cases, failure behavior, and boundary conditions; run the applicable checks available in the repository. Report checks that could not run and the resulting uncertainty. For specification-only work, verify the applicable authoring and acceptance criteria without treating structural checks as approval of product decisions.

## 5. Issue reporting and tracking

**Issue tracking:** Not yet selected.

Use the reporting destination and conventions recorded above for bugs and implementation work. When working from an existing issue, read its relevant context and connect the work to applicable specification and requirement identifiers. Issue discussions provide context; changes to intended behavior still follow the specification change process.

When reporting a bug is part of the task, include the affected feature, reproduction steps, expected and observed behavior, relevant environment details, and known specification references. Use an existing issue for the same defect when appropriate.

Keep unresolved specification decisions in the locations defined by the Specification Authoring Rules. If issue tracking is unset or deliberately unused, report implementation findings in the task handoff; obtain a destination when durable issue creation is needed.

## 6. Source control and commits

Follow the user's instructions and established project workflow for when to commit, which branch to use, and how changes are reviewed and published. Apply the following conventions when committing:

- Use short, imperative commit subjects, such as `Add fare validation rules` or `Fix empty search results`. Describe the change directly; use a body when its reason, consequences, or migration details need explanation.
- Keep each commit focused on one coherent change. Include the specifications, implementation, and tests needed for that change together; keep unrelated changes in separate commits.
- Review the staged diff before committing. Stage only the intended files or hunks, preserving unrelated working-tree and staged changes.
- Run the checks appropriate to the change before committing. Explain any failed or unavailable verification in the handoff.
- Reference relevant issue identifiers using the selected tracker's conventions. Use automatic issue-closing references only when the commit resolves the issue and the project workflow calls for them.
- Preserve existing history by default. Amend, rebase, or otherwise rewrite history only when covered by the user's instructions or established workflow. A local commit does not itself authorize pushing or publishing it.

## 7. Maintain guidance and hand off

You are responsible for writing and maintaining the root `README.md`. Its audience is human readers: prospective users, contributors, and maintainers. Lead with what the application does, who it serves, and how to get started when those steps are established. Use plain language, explain unfamiliar project terms, and include concrete usage examples and verified setup commands where useful. Choose sections that help readers understand and use the project at its current stage. Keep agent operating instructions in `AGENTS.md` and detailed requirements in `spec/`, linking to them when relevant to the reader.

Update the README when specification or implementation changes affect its description of the project's purpose, scope, decisions, capabilities, or setup and usage. Distinguish planned behavior from implemented functionality, resolve or revise affected open questions, and keep links current. Link to the issue-tracking guidance in this file rather than duplicating it.

When domain definitions change, follow the core routing to the domain and change-workflow rules and update `spec/CONTEXT.md` accordingly.

Update this file when project working conventions change. Keep executable commands in their maintained configuration. For changes to the authoring policy, follow its policy-maintenance route. Preserve project-specific guidance when refreshing boilerplate unless the user explicitly requests changes to it.

Conclude with the outcome, affected specifications or requirement identifiers where relevant, verification performed, and any unresolved work. Distinguish implemented behavior from proposed behavior and unverified assumptions. Completion means the requested scope is handled and its verification results and remaining limitations are explicit.
