# skills

A small collection of reusable [Agent Skills](https://agentskills.io/specification) — procedural knowledge that AI coding agents can discover and apply. Each skill is portable across skills-compatible agents (Claude Code, GitHub Copilot CLI, and others).

## Skills

| Skill | What it does |
|-------|--------------|
| [`catchup`](skills/catchup/SKILL.md) | Returns to an existing session and summarizes where things left off, key decisions, and what's next. Trigger with `/catchup` or "catch me up". |
| [`to-options`](skills/to-options/SKILL.md) | Turns the questions a grilling couldn't settle into one HTML page that shows each answer side by side, for the people who decide. Trigger with `/to-options` after a grilling session. |

## Installation

Install with the [`skills`](https://www.npmjs.com/package/skills) CLI:

```bash
# Add all skills from this repo
npx skills@latest add kylehoehns/skills

# Or pick a single skill
npx skills@latest add kylehoehns/skills --skill catchup
```

Add `--global` to install at the user level instead of the current project, and `--agent '*'` to install for every supported agent. Run `npx skills@latest add --help` for all options.

You can also install the whole repository as a plugin in Claude Code or Copilot by pointing to `kylehoehns/skills`.

## Layout

```
skills/
  <skill-name>/
    SKILL.md          # required: frontmatter (name, description) + instructions
    resources/        # optional: supporting scripts or data
```

## Creating a skill

Each skill is a folder with a `SKILL.md` whose frontmatter has a `name` and a `description`. Write the `description` as triggering conditions ("Use when…") so agents know when to reach for it. See the [Agent Skills specification](https://agentskills.io/specification) for the full format.

## License

[MIT](LICENSE)
