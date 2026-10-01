# Antigravity Core Skills & Governance Plugin

A clean, standalone repository containing production-grade Google Antigravity agent governance, the 3-Tier Reuse-Before-Build decision engine, and isolated Skeptic red-teaming.

**100% Independent**: Contains zero project-specific or domain-specific code. Ready to be shared, cloned, or synced across any workstation.

---

## What's Included

```text
antigravity-core-skills/
├── plugin.json                                # Antigravity plugin manifest
├── rules/
│   └── AGENTS.md                             # Universal execution invariants
└── skills/
    ├── reuse-before-build/                   # 3-Tier decision engine
    │   ├── SKILL.md                          # (Surgical, Extension, Greenfield)
    │   └── references/
    │       ├── research-and-risk.md          # 3-Archetype Saturation Heuristic
    │       ├── platform-use.md               # Cross-IDE installation guides
    │       └── execution-capsule.md          # Portable delivery capsule standard
    └── skeptic/                              # Cognitive isolation protocol
        └── SKILL.md                          # Epistemic hygiene red-teaming
```

---

## 1. Push to Your Remote Git Repository (One-Time Setup)

Create a private or public repository on GitHub (e.g. `https://github.com/<your-username>/antigravity-core-skills.git`), then run:

```bash
cd antigravity-core-skills
git init
git add .
git commit -m "feat: initial commit of core skills and universal invariants"
git branch -M main
git remote add origin https://github.com/<your-username>/antigravity-core-skills.git
git push -u origin main
```

---

## 2. Auto-Load on ANY Computer (Even if This Computer is Offline)

On any machine where you use Antigravity, you can make these skills auto-load across **all sessions** with a single command:

### Option A: Global Plugin (Recommended)
Cloning into the global plugins directory makes it available across all workspaces automatically:

```bash
git clone https://github.com/<your-username>/antigravity-core-skills.git ~/.gemini/config/plugins/antigravity-core-skills
```

### Option B: Global Skills Directory
Alternatively, clone directly into the skills folder:

```bash
git clone https://github.com/<your-username>/antigravity-core-skills.git ~/.gemini/config/skills/antigravity-core-skills
```

### Option C: Per-Project Auto-Travel (`.agent/`)
In any project repository where you want these skills to travel with the codebase:

```bash
# Add as a git submodule
git submodule add https://github.com/<your-username>/antigravity-core-skills.git .agents/plugins/antigravity-core-skills
```

Once cloned, the skills and universal rules live on that computer's disk and **never depend on your other machine being powered on or connected to the network.**

---

## Core Invariants Enforced

1. **Zero Unsolicited Daemons**: Never start background HTTP servers (Starlette, Flask, FastAPI). Visuals strictly default to standalone HTML artifacts or `open viewer.html`.
2. **Sandbox Discipline**: Commands run in standard sandbox mode (`BypassSandbox: false`). No macOS modal prompts.
3. **Data Batching Governor**: Scrapers and extractors test in bounded batches (10–50 records max).
4. **Non-Destructive Editing**: Existing files are edited via localized `replace_file_content` diffs, preserving external IDE edits (e.g. Cursor).
