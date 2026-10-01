---
name: reuse-before-build
description: Find and safely reuse existing products, platform capabilities, agent skills, prompts, plugins, MCP servers, applications, repositories, libraries, APIs, and templates before building software. Operates across 3 real-world tiers: (1) Surgical In-Repo patches, (2) Capability Extension using targeted package/MCP reuse into existing code, and (3) Greenfield Architecture using 3-archetype saturation search and isolated skeptic red-teaming. Enforces zero unsolicited background servers, sandbox discipline, data batching governors (10-50 records), and non-destructive surgical editing.
---

# Reuse before build

Deliver the user's outcome by assembling proven parts before creating new ones.
Run the workflow as one experience with an approval gate between discovery and
execution.

## Triage: The 3 Execution Tiers

Before conducting research or modifying code, classify the task into its real-world tier:

### Tier 1: Surgical In-Repo (Local Patches, Bugfixes, Tests, Styling)
- **Scope**: Localized bug fixes, styling adjustments, adding unit tests, or small logic tweaks in an existing file.
- **Execution**: Single-turn. **Zero external search, zero subagents**.
- **Code Integrity**: NEVER use `write_to_file` on existing non-empty code files. Always inspect `git status` and file lines, then apply localized edits via `replace_file_content` to protect concurrent work in external IDEs (e.g., Cursor).

### Tier 2: Capability Extension (The Missing Middle — Adding Features to Existing Code)
- **Scope**: Adding a capability, parser, connector, or feature to an existing codebase (e.g., adding cookie decoding or session replay to existing scripts).
- **Execution**: Single-turn. **Targeted reuse search only**.
  1. Inspect local workspace and available MCP tools first.
  2. If missing, search top 2–3 PyPI/npm packages or proven libraries.
  3. Integrate the chosen library directly into existing files via `replace_file_content`. Do not invent net-new frameworks, daemon servers, or replace existing domain logic.
- **Data & Loop Governor**: For any data harvesting, scraping, or parsing tests, strictly process in bounded batches (10–50 records max). Never run unbounded loops.

### Tier 3: Greenfield Architecture (Net-New Systems from Scratch)
- **Scope**: Designing or selecting the foundation for a net-new application, service, microservice, or standalone system from scratch.
- **Execution**: Multi-phase discovery with **Architectural Saturation**:
  - Stop searching once **3 distinct architectural archetypes** solving the problem have been identified (e.g., Archetype A: Headless CDP; Archetype B: Reverse-engineered private API; Archetype C: Session replay). Pick the best-maintained candidate from each.
  - Before presenting the final architectural recommendation to the user, automatically spawn an isolated `skeptic` subagent (`TypeName: "self"`, `Role: "Skeptic Red-Teamer"`) in a throwaway context to stress-test assumptions and break convergence bias without bloating the primary conversation transcript.

## Universal Execution Invariants (Enforced Across All Tiers)

1. **Zero Unsolicited Daemons**: Never start background HTTP/WebSocket servers (Starlette, FastAPI, Flask, etc.) unless the user explicitly requested a server or backend daemon. Visuals strictly default to standalone HTML artifacts or opening local files (`open viewer.html`).
2. **Sandbox Non-Negotiable**: Always run in Standard Sandboxed Mode (`BypassSandbox: false`). Never trigger macOS permission modals unless external network access is strictly required.
3. **Cursor & External IDE Concurrency Guard**: Never overwrite rich domain structures, parser tables, or active scripts. Treat existing domain files as collaborative assets. Always use targeted diffs.

## Control scope and cost

Reuse conversation and workspace context. Ask at most three questions, and only
when an answer could change the decision or prevent safe execution. State
constraints once in a compact block and reference them afterward.

Match effort to impact. Compare three to five strong options for small work and
up to ten for material architecture decisions. Do not pad results, repeat
searches, generate an Excel file by default, or build a sample app to validate
this skill.

Stop searching when more results are unlikely to change the recommendation.

## Continue from the current state

Before choosing a phase, classify the user's latest turn and continue from the
furthest completed point:

- Clarification or request for detail: answer from the existing findings. Do
  not restart discovery, repeat unchanged analysis, or present a new decision
  menu.
- New or changed constraint: identify which claims and candidates it affects,
  verify only those items, and update the recommendation only when warranted.
- Approval or option selection: preserve the selected scope. If post-delivery
  recommendation QA is pending, complete it and resolve any defects before
  continuing to the execution capsule.
- Request to implement: continue to execution only when the target and prior
  approval are clear.
- Explicit restart, materially different goal, invalidated evidence, or stale
  decisive facts: return to the earliest affected phase and explain why.

Preserve prior constraints, evidence, exclusions, and decisions. Do not treat
questions such as "anything else?", "is there nothing to build?", or requests
for more detail as authorization to repeat the full search. Do not reproduce a
supporting reference in the user-facing answer unless the user asks for it.

## Phase 1: understand the build

If a codebase exists, inspect its relevant architecture, dependencies, existing
capabilities, tests, and current changes before searching. Do not scan unrelated
directories.

Classify the product stage:

- Early: prioritize speed, reversibility, and replaceable components.
- Mid-build: prioritize compatibility, migrations, observability, and support.
- Final: prioritize security, licensing, reliability, performance, and access.
- Existing product: minimize disruption and reuse its established patterns.

Deconstruct the requested outcome into:

- Base structure: common mechanics that should usually be reused.
- Novel elements: differentiating behavior worth building.
- Constraints: environment, budget, privacy, license, maintenance, and risk.
- Acceptance criteria: observable proof that the outcome works.

## Phase 2: find what exists

Read [research-and-risk.md](references/research-and-risk.md) before material
research.

Search the current open web and relevant connected sources for:

1. Finished commercial or free products usable as-is.
2. Native operating-system or platform capabilities.
3. Third-party agent skills, agents, prompts, plugins, and workflows.
4. MCP servers and other supported integrations.
5. Maintained open-source applications and repositories.
6. Libraries, SDKs, APIs, templates, and reusable components.
7. Combinations of two to four items when no single option meets the goal.

Search current skill catalogs and community-created skills, not only installed
skills. Search complete products even when the user initially asks for code.
Use primary sources for decisive claims.

Apply an identity and handoff evidence gate before relying on any candidate:

- Name and link every claimed product, connector, skill, plugin, MCP server,
  repository, library, or API. Never refer to an "existing connector" or
  similar capability without a verified identity and source.
- Verify every material handoff in a proposed chain from both sides when
  practical, including supported formats, metadata, permissions, storage or
  placeholder behavior, version compatibility, and round-trip limitations.
- Distinguish a product feature from an agent-accessible operation. A feature
  visible to a human is not proof that an agent can invoke it reliably.
- Label an unverified capability as unknown. Do not use it to justify the
  recommendation, a no-build conclusion, or an execution step.
- Correct earlier findings explicitly when new evidence disproves them.

Do not execute candidate code during discovery.

## Phase 3: compare and decide

Create an in-chat table that maps each candidate or combination to:

- the exact requirement it solves;
- its component type and source URL;
- its disposition as include, exclude, or defer, with the evidence-backed reason;
- what remains missing;
- its language or stack when relevant;
- license and practical commercial-use implications;
- maintenance and adoption evidence;
- security, privacy, cost, and lock-in risks;
- integration effort and confidence.

Treat stars, forks, downloads, and recency as evidence, not conclusions.
Fact-check the provisional winner and any near-perfect exclusion a second time.

For Tier 3 Greenfield Architecture decisions, commission an isolated `skeptic` subagent
via `invoke_subagent` (`TypeName: "self"`, `Role: "Skeptic Red-Teamer"`) before presenting the
decision. Supply the raw requirements, constraints, and proposed candidate table without leading
the witness. The Skeptic stress-tests assumptions, runs the inverse test, and reports back in a
throwaway context, keeping the primary conversation transcript lean. Adjudicate any critical
findings. For Tier 1 and Tier 2 tasks, do NOT spawn subagents; keep execution direct, single-turn,
and token-efficient.

For combinations, define each component's role, sequence, handoff, adapter,
compatibility, failure boundary, and remaining custom work. Reject a combination
when its glue and maintenance burden exceed its reuse value.

Present three paths when credible:

- A: use or configure an existing solution;
- B: fork, extend, or combine selected components;
- C: build the smallest missing layer or, only when justified, build new.

Mark one option "Recommended". Explain the decision in plain language for a
builder who is not an engineer. State facts, inferences, assumptions, and
unknowns distinctly.

## Post-delivery recommendation QA

After the recommendations have been delivered to the user, run QA against the
exact user-visible content before treating a selection as approval. Read the
post-delivery QA standard in
[research-and-risk.md](references/research-and-risk.md). Check requirement and
acceptance-criteria coverage, source support, candidate dispositions, handoffs,
risk statements, skeptic remediation, the reuse-first conclusion, clarity, and
the proposed next action. Confirm that broad discovery stayed shallow and that
deep review was limited to close candidates that could affect the decision.

Report pass, revise, or blocked. If QA finds a defect, deliver the corrected
recommendation and rerun only the failed or affected checks. Do not package,
install, execute, or change the project until the delivered recommendation
passes QA. If the user selects an option before QA finishes, preserve the
selection but complete QA before acting on it.

Stop and request approval before packaging, retrieving, installing, executing,
or changing the project.

## Phase 4: produce the execution capsule

After approval, read
[execution-capsule.md](references/execution-capsule.md). Create a
project-specific folder and package it as a ZIP with
scripts/package_capsule.py.

The helper is optional and uses only the Python standard library. Run it with
Python 3.9 or newer. It refuses to overwrite an existing output ZIP unless the
operator explicitly passes `--force`. When Python is unavailable, apply the
same validation rules below and create a ZIP with the platform archive tool,
preserving one project folder at the archive root.

The capsule must contain the complete approved handoff:

- goal, stage, constraints, and acceptance criteria;
- selected components and how they relate;
- exact source URLs and verified versions or commit references;
- licenses, notices, risks, mitigations, and unresolved questions;
- exact integration order, boundaries, and required glue;
- destination-specific runner instructions;
- functional, compatibility, security, and regression tests;
- checkpoints, rollback steps, and resumable status.
- critical self-review findings, risk mitigations, acceptance checks, and closure status.

Use real values. Do not leave generic bracket fields, template tokens, TODOs, or
invented file paths. Include exact source file paths only after verifying them.
If the target project path cannot be known until launch, instruct the runner to
resolve and confirm it rather than fabricate it.

Generate runners only for the systems the user will use. Verify current platform
capabilities and installation rules from official sources. Treat Codex, Cursor,
Antigravity, Hermes, and similar products as environments, not models. Do not
hardcode model availability, plans, prices, or routing. Choose them at runtime
from current evidence and the user's available subscriptions or local models.

Do not bundle third-party source by default. Record pinned sources and integrity
information so the runner retrieves the evaluated code. Bundle source only when
offline execution requires it and redistribution is allowed.

## Phase 5: hand off clearly

Deliver:

1. The project-specific execution ZIP.
2. A short chat summary naming the approved option and first action.
3. Exact instructions for attaching or installing the ZIP in each selected
   environment.
4. One natural-language command the user can issue to continue.

Read [platform-use.md](references/platform-use.md) before giving installation
or invocation instructions.

Do not create extra reports or an Excel workbook unless requested.

## Phase 6: execute when authorized

Treat a request such as the following as authorization to continue:

“Use the approved plan in this capsule. Integrate the selected components into
this codebase, test the result, and recommend the next build steps.”

Before changing code:

1. Resolve and confirm the target project.
2. Inspect current files and version-control status.
3. Reverify component identity, selected version, license, and required notices.
4. Choose the least complex reversible staging method appropriate to the risk.
5. Inspect install hooks and requested permissions before running them.

Implement only the approved option and verified gaps. Keep unrelated work
untouched. Use checkpoints before material changes.

Test each component alone, each handoff, the combined workflow, regressions, and
the acceptance criteria. Use proportionate security tools when available, but
do not claim an audit.

If an expected condition fails, stop at the current checkpoint. Do not silently
substitute another component or expand scope.

Report what was reused, changed, connected, tested, left unresolved, and
recommended next. Update the capsule state so another agent can resume without
reconstructing the work.

## Product and intellectual-property boundary

Use finished products as-is, through supported integrations, or as architectural
and workflow references. Reuse source code only when its license permits the
intended use. Do not copy proprietary code, protected assets, or distinctive
trade dress.
