# Committing Code Skill Options

This note captures options for turning `git/committing-code-skill.md` into reusable guidance for Claude, Copilot, Codex, OpenCode, and similar coding agents.

## 1. Best Default: Make One Portable Agent Skill

Convert `git/committing-code-skill.md` into a real `SKILL.md` package with YAML frontmatter:

```text
commit/
`-- SKILL.md
```

```md
---
name: commit
description: Create repository-compliant Conventional Commit messages from staged git changes. Use when preparing commits.
---

# Git Commit Skill
...
```

This is the cleanest path because Agent Skills are a portable format: a folder with `SKILL.md`, required `name` and `description`, plus optional scripts, references, and assets. Codex, Copilot, and OpenCode support this style, and Claude Code supports the same basic `SKILL.md` pattern.

## 2. Use Per-Tool Install Locations

Copy the same skill package to each tool's preferred folder:

| Tool | Project Location | Personal Location |
|---|---|---|
| Claude Code | `.claude/skills/commit/SKILL.md` | `~/.claude/skills/commit/SKILL.md` |
| Codex | `.agents/skills/commit/SKILL.md` | `~/.agents/skills/commit/SKILL.md` |
| Copilot / VS Code | `.github/skills/commit/SKILL.md`, `.claude/skills/...`, or `.agents/skills/...` | `~/.copilot/skills/commit/SKILL.md`, `~/.agents/skills/...` |
| OpenCode | `.opencode/skills/commit/SKILL.md`, `.agents/skills/...`, or `.claude/skills/...` | `~/.config/opencode/skills/commit/SKILL.md`, `~/.agents/skills/...` |

## 3. Use `.agents/skills` As The Shared Repo Target

For this repo, the most portable single checked-in target is probably:

```text
.agents/skills/commit/SKILL.md
```

Codex, Copilot, and OpenCode support `.agents/skills`. Claude Code does not list `.agents/skills` as its native project skill path, so if Claude Code is important, mirror it to:

```text
.claude/skills/commit/SKILL.md
```

## 4. Use Instruction Files Instead Of Skills

If you want commit rules to be always-on rather than invoked as a task, use instruction files:

```text
AGENTS.md
.github/copilot-instructions.md
CLAUDE.md
opencode.json
```

This is better for "always follow these commit conventions." A skill is better for "when I ask you to commit, run this workflow."

For Copilot specifically, `.github/prompts/commit.prompt.md` is another option when you want a slash-command style prompt rather than a full skill.

## Recommendation

Keep `git/committing-code-skill.md` as the source, generate a canonical `.agents/skills/commit/SKILL.md`, and mirror that to `.claude/skills/commit/SKILL.md` only if you actively use Claude Code.

## Sources

- Codex skills: https://developers.openai.com/codex/skills
- Claude Code skills: https://code.claude.com/docs/en/skills
- Copilot Agent Skills: https://code.visualstudio.com/docs/copilot/customization/agent-skills
- Copilot custom instructions: https://code.visualstudio.com/docs/copilot/customization/custom-instructions
- Copilot prompt files: https://code.visualstudio.com/docs/copilot/customization/prompt-files
- OpenCode skills: https://opencode.ai/docs/skills/
- OpenCode rules: https://opencode.ai/docs/rules/
- Agent Skills overview: https://agentskills.io/
