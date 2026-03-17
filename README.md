# 🧰 Skill Scaffolder — OpenClaw

> **Describe what you want in plain English. Get a fully built skill. No coding needed.**

The Skill Scaffolder is an [OpenClaw](https://github.com/openclaw) skill that generates
other skills. It interviews you, writes the files, tests them in a sandbox, and installs
only when you say so.

---

## What It Does

1. **Interview** — You describe what you want. The scaffolder asks a few friendly
   follow-up questions (no jargon, no forms).
2. **Generate** — It writes a complete skill package: `SKILL.md`, optional helper
   scripts, and reference files.
3. **Sandbox test** — It runs automatic checks to make sure the skill is correctly
   structured and working.
4. **Approval** — It shows you a plain-English summary and asks before installing
   anything.
5. **Install** — One click (or one "yes") and your new skill is live.

---

## Who It's For

Designed specifically for **non-developers** — no knowledge of YAML, Python, or the
OpenClaw skill format required. If you can describe a workflow in a sentence, the
scaffolder can build a skill for it.

---

## File Structure

```
skill-scaffolder/
├── SKILL.md                          ← Main skill (Claude reads this)
├── scripts/
│   ├── sandbox_test.py               ← Auto-detects & validates generated skills
│   └── install_skill.py              ← Copies skills into OpenClaw's skills folder
├── references/
│   ├── interview-tips.md             ← How to handle vague or hesitant users
│   ├── description-writing.md        ← Patterns for strong skill descriptions
│   └── sandbox-test-patterns.md      ← Copy-paste test templates
├── assets/
│   └── skill-template.md             ← Blank SKILL.md template
└── evals/
    └── evals.json                    ← Test cases for the scaffolder itself
```

---

## Quick Start

### Install the skill

```bash
# From your OpenClaw skills directory:
git clone https://github.com/YOUR_USERNAME/skill-scaffolder
# Or download the .skill file and drag it into your skills folder
```

### Use it

Just describe what you want to Claude:

> *"I want a skill that summarizes my emails every morning."*
> *"Make me a skill for writing project status updates."*
> *"I want Claude to always format my CSV data as a table."*

The scaffolder takes it from there.

---

## Running the Sandbox Test Manually

```bash
# Test a skill you've already scaffolded:
python skill-scaffolder/scripts/sandbox_test.py --skill-dir /path/to/your/skill

# Test the scaffolder itself:
python skill-scaffolder/scripts/sandbox_test.py --skill-dir skill-scaffolder/
```

---

## Installing a Skill Manually

```bash
python skill-scaffolder/scripts/install_skill.py \
  --source /tmp/scaffolded-skills/my-skill/ \
  --name my-skill
```

Options:
- `--skills-dir /custom/path` — Override the default OpenClaw skills directory
- `--force` — Overwrite an existing skill without prompting

---

## Contributing

Pull requests welcome! If you build a skill using the scaffolder and want to share it,
open a PR or link it in the [Discussions](../../discussions) tab.

Areas where contributions are especially welcome:
- More sandbox test patterns (`references/sandbox-test-patterns.md`)
- More example skills in `evals/evals.json`
- Translations of the interview flow for non-English speakers
- Windows path handling improvements in `install_skill.py`

---

## License

MIT — free to use, fork, and build on.
