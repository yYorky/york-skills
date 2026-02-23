![](https://i.logos-download.com/114232/31116-05a1502c46130721c61b3a89eb569886.png/Claude_Logo_2023.png?dl)
# York's Claude Skills Library

A personal library of Claude Code skills for personal productivity and creative work.

## How to use

Skills extend Claude Code with specialised workflows. To use any skill from this library:

**Step 1 — Copy the skill into your project**
```bash
cp -r path/to/york-skills/skill-name /your-project/.claude/skills/
```

The `.claude/skills/` folder should sit at the root of whichever project you are working in. Create it if it does not exist.

**Step 2 — Invoke the skill in Claude Code**

Type `/skill-name` in the Claude Code chat to trigger the skill. For example:
```
/linkedin-article
```

Claude will automatically detect the skill and follow its workflow.

> **Tip:** You can also trigger skills by describing what you want in natural language — Claude will match your request to the right skill based on its description. Invoking by name with `/` is the most reliable method.

> **Note:** The `skill-creator` skill is built into Claude Code natively — you can invoke `/skill-creator` on any machine without copying it first. The copy here is for reference and customisation.

---

## Skills

| Skill | Invoke | What it does |
|-------|--------|--------------|
| Skill Creator | `/skill-creator` | Meta-skill for building new Claude skills. Use when creating or updating skills in this library. |
| LinkedIn Article | `/linkedin-article` | Interview-driven assistant for writing LinkedIn Pulse articles in York's personal brand voice. Asks questions one at a time, researches any links you drop, generates an outline for approval, then writes the full article. |

---

## Related

- [Anthropic official skills repo](https://github.com/anthropics/skills) — source for `skill-creator` and other official skills
- [Claude Code skills documentation](https://code.claude.com/docs/en/skills)
- Private work skills repo — separate private repo (not linked here)
