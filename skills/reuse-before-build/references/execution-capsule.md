# Execution capsule standard

Use this reference only after the user approves an option.

## Purpose

Create one ZIP that another capable agent can read and execute without needing
the original conversation. The package must preserve the decision, evidence,
sequence, safeguards, tests, and resumable state.

## Required structure

Create a project-specific directory with:

- START_HERE.md
- MANIFEST.json
- PROJECT.md
- SOLUTION.md
- RUN.md
- TESTS_AND_ROLLBACK.md
- SKEPTIC_REVIEW.md
- runners/<target-system>.md

Add patches/, adapters/, licenses/, fixtures/, or evidence/ only when the
approved plan requires them. Do not add decorative documentation.

## File responsibilities

### START_HERE.md

State the reading order, the approved option, the current checkpoint, and the
single natural-language command that continues execution. Tell the runner not
to infer missing facts or change the approved components silently.

### MANIFEST.json

Use valid JSON with these fields:

- schema_version: use "1.0".
- package_type: use "reuse-execution-capsule".
- project_name: use the real project name.
- project_stage: early, mid-build, final, or existing-product.
- approved_option: A, B, or C.
- approved_at: ISO 8601 date or timestamp.
- target_systems: lower-case runner names.
- components: one object per selected product, skill, MCP server, repository,
  library, API, template, or native capability.
- status: phase, checkpoint, and next_action.

Each component object must include:

- name
- type
- source_url
- version_or_ref
- license
- role
- risk_status

Use an official documentation URL for a product or native capability. For code,
use the canonical repository and the exact evaluated release or commit.

### PROJECT.md

Record the outcome, current architecture when relevant, product stage, base
structure, novel elements, constraints, acceptance criteria, and explicit
out-of-scope work.

### SOLUTION.md

Record the approved architecture, component roles, sequence, data and control
handoffs, adapters, compatibility findings, licenses, risks, mitigations,
rejected alternatives, and unresolved questions.

### RUN.md

Give the system-independent execution order. Include preconditions, checkpoints,
stop conditions, expected outputs, and the rule that scope or component changes
require renewed approval.

### TESTS_AND_ROLLBACK.md

Define component tests, handoff tests, combined acceptance tests, regression
checks, proportionate security checks, rollback steps, and the evidence required
for pass, revise, or reject.

### SKEPTIC_REVIEW.md

Record the independent reviewer's prioritized findings with severity, evidence,
impact, remediation, and acceptance checks. For each finding, record the primary
agent's adjudication and remediation evidence. State whether an independent
closure pass was required and, when required, its result. Include the final
include, exclude, or defer disposition and evidence-backed reason for every
candidate considered in the decision table.

### runners/<target-system>.md

Generate one file for each target system. Use its current official syntax and
capabilities. State:

- how to resolve and confirm the target project;
- which capsule files to read and in what order;
- the exact approved sources and sequence;
- permissions and prohibited actions;
- commands or tool actions supported by that system;
- checkpoints, tests, rollback, and completion report;
- the natural-language continuation command.

Do not hardcode a model. Select a current model at runtime based on available
access, quality, cost, privacy, and task risk.

## No-placeholder rule

Before packaging:

- replace every template token with a verified value;
- use exact URLs and evaluated versions;
- use exact source paths only when inspected;
- mark genuine unknowns explicitly and state whether they block execution;
- never invent the target project path.

The packager rejects common unresolved placeholder patterns.

## Third-party code

Do not include third-party source by default. Record the pinned source and
integrity evidence so the runner retrieves the evaluated version. Include source
only when offline execution requires it and redistribution is permitted. Include
all required notices when bundling or modifying licensed work.

## Portable skill placement

The reusable skill itself follows the open Agent Skills folder format.

For user-wide local use with Codex or Cursor, place the unzipped
`reuse-before-build` folder under `~/.agents/skills/`. Other hosts use different
global locations: Antigravity IDE uses `~/.gemini/config/skills/`, and Hermes
uses `~/.hermes/skills/`. Direct installation of this multi-file skill in
Antigravity CLI is unverified; use a validated plugin package for that CLI.
Read [platform-use.md](platform-use.md) for current paths, invocation, and
cloud-distribution limits.

A project-specific execution capsule is not installed as a global skill. Attach
it to the target agent when file attachments are supported, or unzip it into a
clearly named staging folder inside the intended project. The runner begins with
START_HERE.md.
