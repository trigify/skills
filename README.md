# Trigify Skills

Agent skills for working with Trigify — social listening searches, automated workflows, enrichment, X/Twitter management, and more.

## What's included

**trigify-tools** — Expert guidance for all Trigify operations: creating searches with proper Boolean logic, building and testing workflows, enrichment, X/Twitter posting, credit management, and integration health checks.

## Installation

### Claude Code

```bash
claude skill add --from github:trigify/skills
```

### Cursor

Add to `.cursor/rules/trigify.mdc` in your project:

```
---
description: MUST USE for ANY Trigify operation — searches, workflows, enrichment, X/Twitter, or anything involving social listening and workflow automation.
globs:
---

<paste contents of SKILL.md and references/*.md here>
```

Or fetch it directly:

```bash
mkdir -p .cursor/rules
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL.md > .cursor/rules/trigify.mdc
```

### Windsurf

Add to `.windsurfrules` in your project root:

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL.md >> .windsurfrules
```

Or paste the contents of `SKILL.md` into **Windsurf Settings > Rules**.

### GitHub Copilot

Add to `.github/copilot-instructions.md` in your repo:

```bash
mkdir -p .github
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL.md >> .github/copilot-instructions.md
```

### Cline

1. Open VS Code → Cline sidebar → Settings (gear icon)
2. Paste the contents of `SKILL.md` into **Custom Instructions**

Or add to `.clinerules` in your project root:

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL.md >> .clinerules
```

### Aider

Add to `.aider.conf.yml` in your project:

```yaml
read: SKILL.md
```

Then place the file locally:

```bash
curl -sL https://raw.githubusercontent.com/trigify/skills/main/SKILL.md > SKILL.md
```

### Continue

Add to your `.continue/config.yaml`:

```yaml
docs:
  - title: "Trigify Tools"
    startUrl: "https://raw.githubusercontent.com/trigify/skills/main/SKILL.md"
```

### Any other agent

Copy the skill files into whatever custom instructions mechanism your agent supports:

```bash
# Download all skill files
git clone https://github.com/trigify/skills.git trigify-skills

# The key files:
# trigify-skills/SKILL.md              — Main skill prompt
# trigify-skills/references/*.md       — Detailed reference guides
```

Paste the contents of `SKILL.md` into your agent's system prompt or custom instructions. For full coverage, also include the reference files — they contain detailed Boolean query rules and workflow patterns.

## Usage

Once installed, the skill activates automatically when you mention Trigify-related tasks:

- "Create a search for competitor mentions on LinkedIn"
- "Build a workflow to enrich and qualify leads"
- "Test this workflow with real data"
- "Check my credit balance"
- "Post on X"
