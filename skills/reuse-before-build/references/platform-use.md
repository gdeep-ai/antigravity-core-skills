# Platform use

Verify current behavior from official documentation before changing these
instructions.

## Codex local installation

Unzip the portable package. Place its `reuse-before-build` folder at:

`~/.agents/skills/reuse-before-build/`

Confirm that `SKILL.md` is directly inside that folder. Restart Codex only if
the skill does not appear automatically. In Codex CLI or the IDE extension,
select the skill with `$reuse-before-build` or through `/skills`.

Official documentation:
https://learn.chatgpt.com/docs/build-skills

## Cursor

For local use, Cursor scans `~/.agents/skills/`, so the same folder placement as
Codex works on that machine. Invoke the discovered skill from the slash menu.
This location remains local and is not copied to Cursor Cloud Agents. Cursor
only syncs personal cloud skills from `~/.cursor/skills/` when skill sync is
enabled.

Official documentation:
https://cursor.com/docs/skills

## Antigravity IDE

For global use across Antigravity IDE workspaces, place the folder at:

`~/.gemini/config/skills/reuse-before-build/`

For workspace-only use, place it at:

`<workspace-root>/.agents/skills/reuse-before-build/`

Mention the skill by name or invoke `/reuse-before-build` to force its use.

Official documentation:
https://antigravity.google/docs/skills/

## Antigravity CLI

Current Antigravity CLI documentation describes standalone global skills as
individual Markdown files. It does not establish that a multi-file Agent Skills
folder will load its referenced scripts and supporting files. Do not claim that
this ZIP is directly installable as a standalone Antigravity CLI skill.

For Antigravity CLI, package and validate this skill as a plugin with the skill
folder under the plugin's `skills/` directory, or use Antigravity IDE instead.
Verify the current CLI documentation and complete a clean-environment test
before claiming CLI support.

Official documentation:
https://www.antigravity.google/docs/cli/plugins

## Hermes

For native global installation, place the folder at:

`~/.hermes/skills/reuse-before-build/`

Hermes can alternatively scan `~/.agents/skills/` when that directory is listed
under `skills.external_dirs` in `~/.hermes/config.yaml`. Once discovered,
invoke `/reuse-before-build`.

Official documentation:
https://hermes-agent.nousresearch.com/docs/user-guide/features/skills

## ZIP attachments

A ZIP is the transport package, not a universal one-click installer. When a
system accepts file attachments, attach the ZIP and instruct the agent to read
the top-level `SKILL.md` and install the enclosed folder in its supported skill
directory. Otherwise unzip it into the platform-specific location above.

Do not claim direct ZIP installation unless the current platform documentation
explicitly supports it.

Standalone local skills are supported by Codex desktop, Codex CLI, and the
Codex IDE extension. For reusable distribution through ChatGPT web or mobile,
or for a package that also bundles connectors, create an Agent Plugin instead
of presenting this ZIP as a universal installer.
