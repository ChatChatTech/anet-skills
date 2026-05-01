# anet-skills

A small, opinionated set of agent skills curated by the AgentNetwork team for stress-testing plans and aligning shared language before you ship.

## Quickstart · 一键安装

```bash
npx skills@latest add ChatChatTech/anet-skills
```

Pick the skills you want and the coding agents you want to install them on (Claude Code, GitHub Copilot, Cursor, Codex, Gemini CLI, OpenCode, Warp, … 50+ supported).

Optional flags:

```bash
# install everything to all detected agents, no prompts
npx skills@latest add ChatChatTech/anet-skills --all

# install to a specific agent, globally
npx skills@latest add ChatChatTech/anet-skills -a claude-code -g -y

# just list what's available
npx skills@latest add ChatChatTech/anet-skills --list
```

The CLI behind it is the open-source [vercel-labs/skills](https://github.com/vercel-labs/skills) ([spec](https://agentskills.io/)).

## Skills · 技能列表

| Skill | 中文名 | What it does · 做什么 |
|---|---|---|
| [anet-intent-grill](./skills/anet-intent-grill/SKILL.md) | 意图烤问 | Distill the real **intent** behind a plan — walk down each branch of the decision tree and resolve dependencies one by one. 在动手 build 之前把模糊的"想做这个"蒸馏成 leaf-level 的明确 intent。 |
| [anet-lexicon-sync](./skills/anet-lexicon-sync/SKILL.md) | 词表同步 | Synchronise the working **lexicon** for the current task — hunt down vague / overloaded / conflicting terms, lock each to a canonical definition, and pin the resolved vocabulary inline into `CONTEXT.md` + ADRs. 把本次任务里模棱两可、同名异义的词全部拍死。 |

Both skills are written in **English + Chinese mixed style**, work with any LLM, and are not coupled to AgentNetwork itself — use them on any project.

## How it works · 实现方式

This repo follows the [Agent Skills](https://agentskills.io/) spec:

- Each skill lives under `skills/<skill-name>/SKILL.md` with YAML frontmatter (`name`, `description`).
- A `.claude-plugin/plugin.json` manifest at the repo root tells the `skills` CLI which folders to pick up.
- That's it — no build step, no npm publish, no install scripts.

## Develop · 修改与贡献

Edit any `skills/<name>/SKILL.md`, push to `main`, and downstream users get the update via:

```bash
npx skills@latest update
```

To add a new skill:

1. `mkdir -p skills/<name> && cd skills/<name>`
2. Create `SKILL.md` with `name` + `description` frontmatter.
3. Append the path to `.claude-plugin/plugin.json`.
4. Add a row to the table above.

## License

MIT
