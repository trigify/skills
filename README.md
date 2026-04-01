# Trigify Skills

Agent skills for working with Trigify — social listening searches, automated workflows, enrichment, X/Twitter management, and more.

## What's included

**trigify-tools** — Expert guidance for all Trigify operations: creating searches with proper Boolean logic, building and testing workflows, enrichment, X/Twitter posting, credit management, and integration health checks.

**Files:**
- `SKILL.md` — Main skill prompt (references files in `references/`)
- `SKILL-FULL.md` — Bundled version with all references inlined (for single-file agents)
- `references/search-guide.md` — Boolean query rules, platform-specific requirements, keyword strategies
- `references/workflow-patterns.md` — Workflow decision trees, patterns, and testing procedures

## Installation

### Claude Code

Claude Code discovers skills from `.claude/skills/` directories. Clone the full repo:

```bash
git clone https://github.com/trigify/skills.git .claude/skills/trigify
```

To update: `cd .claude/skills/trigify && git pull`

### Cursor

Use `SKILL-FULL.md` which bundles all reference guides into one file:

```bash
mkdir -p .cursor/rules
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md > .cursor/rules/trigify.mdc
```

### Windsurf

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md >> .windsurfrules
```

Or paste the contents of `SKILL-FULL.md` into **Windsurf Settings > Rules**.

### GitHub Copilot

```bash
mkdir -p .github
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md >> .github/copilot-instructions.md
```

### Cline

1. Open VS Code → Cline sidebar → Settings (gear icon)
2. Paste the contents of [`SKILL-FULL.md`](https://github.com/trigify/skills/blob/main/SKILL-FULL.md) into **Custom Instructions**

Or add to `.clinerules` in your project root:

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md >> .clinerules
```

### Aider

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md > SKILL.md
```

Then add to `.aider.conf.yml`:

```yaml
read: SKILL.md
```

### Continue

Add to your `.continue/config.yaml`:

```yaml
docs:
  - title: "Trigify Tools"
    startUrl: "https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md"
```

### Any other agent

Download the bundled skill file and paste into your agent's custom instructions:

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL-FULL.md
```

Or clone the full repo for access to individual files:

```bash
git clone https://github.com/trigify/skills.git trigify-skills
```

## Usage

Once installed, the skill activates automatically when you mention Trigify-related tasks:

- "Create a search for competitor mentions on LinkedIn"
- "Build a workflow to enrich and qualify leads"
- "Test this workflow with real data"
- "Check my credit balance"
- "Post on X"
