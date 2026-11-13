# Risk-Tiered Code Review

An [Agent Skills](https://agentskills.io/specification) package that reviews code by blast radius, checks evidence against the reviewed revision, and reports merge and launch readiness separately.

## Install

Run this command from the project where you want to use the skill.

```sh
npx skills add tranvuongduy2003/rtacr
```

The Skills CLI requires Node.js and installs to your project by default. Select the agents you use, or pass `-a` with agent names such as `codex`, `claude-code`, `cursor`, `antigravity`, and `opencode`. Add `-g` for a user-wide install. [Skills CLI documentation](https://github.com/vercel-labs/skills#install-a-skill)

For a local checkout, pass its path to `npx skills add`. For a manual install, copy the entire [`risk-tiered-code-review/`](.agents/skills/risk-tiered-code-review/) directory into the appropriate location in the target project.

| Agent | Project skill directory |
| --- | --- |
| [Codex](https://learn.chatgpt.com/docs/build-skills), [Cursor](https://cursor.com/docs/skills), [Antigravity](https://antigravity.google/docs/skills), [OpenCode](https://opencode.ai/docs/skills/) | `.agents/skills/` |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/` |

If a client does not discover the skill after installation, start a fresh session in the target repository.

## Use

Select `risk-tiered-code-review` in the client or ask for a risk-tiered review of a specific PR, commit range, or local change. Include a spec or acceptance criteria if available. Request launch readiness explicitly when reviewing a release candidate.

The workflow draws on John Kim’s [How I Review AI Code](https://www.youtube.com/watch?v=b2QkhmQ0sT0).
