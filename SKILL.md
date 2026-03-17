---
name: skill-scaffolder
description: >
  Generates complete, ready-to-install OpenClaw skills from a plain-English description.
  Use this skill whenever a user wants to build a new skill, automate a workflow into a
  skill, or says things like "I want a skill that...", "can you make a skill for...",
  "build me a tool that...", "I want Claude to always do X when I say Y", or "how do I
  teach Claude to...". Designed especially for non-developers — no coding knowledge
  required. The skill conducts a friendly interview, scaffolds a full SKILL.md with tool
  wrappers and helper scripts, runs a sandbox test, and asks for approval before
  installing. Always trigger this skill for any new skill creation request, even if the
  user's description is vague or rough — the interview process handles the rest.
---

# Skill Scaffolder

Helps anyone — coders and non-coders alike — create a new OpenClaw skill from scratch.
The user describes what they want in plain English; this skill handles the rest:
interview → draft → sandbox test → approval → install.

---

## Guiding Principles

- **No jargon with non-coders.** Detect the user's technical level from their language.
  Never say "YAML frontmatter", "JSON schema", "subprocess", etc. to someone who hasn't
  shown they know those terms. Say "settings block", "a small config file", "runs a
  quick check" instead.
- **One question at a time.** Don't overwhelm. Ask the most important open question, let
  them answer, then move on.
- **Make it feel magical, not technical.** Frame the process as "teaching Claude a new
  habit" rather than "writing a skill file".
- **Always show before installing.** The user must approve the generated files before
  anything is written to their skill folder.

---

## Phase 1 — Friendly Interview

Start with a warm, single opening question. Do NOT dump a form on the user.

**Opening line (adapt to context):**
> "Great! Let's build that skill together. First — in your own words, what should Claude
> *do* when this skill is active? Don't worry about being technical."

Then, through natural back-and-forth, gather answers to these questions. You don't need
to ask them all in order — extract what you can from the conversation and only ask what's
still missing.

| # | What to learn | Example follow-up |
|---|---------------|-------------------|
| 1 | **Core action** — what Claude should do | Already asked in opener |
| 2 | **Trigger words/context** — what the user says to activate it | "What would you typically type to kick this off?" |
| 3 | **Inputs** — what Claude needs to do the job | "Does Claude need a file, a URL, some text, or nothing at all?" |
| 4 | **Output format** — what the user gets back | "Would you like a file saved to your computer, a response in chat, or both?" |
| 5 | **Example** — a concrete 'before and after' | "Can you give me a quick example — what would you give Claude, and what would you want back?" |
| 6 | **Edge cases** — what should NOT happen | "Is there anything this skill should definitely *not* do, or situations it should skip?" |
| 7 | **External tools** (optional) — apps, APIs | "Should this skill ever open a browser, read your email, or talk to any other app?" |

Once you have enough to write a meaningful draft (usually after 4–5 questions), proceed.
Tell the user: *"I think I have enough to write a first draft — let me put that together!"*

Read `references/interview-tips.md` if you need help drawing out answers from a hesitant
or vague user.

---

## Phase 2 — Generate the Skill Package

Based on the interview, generate the following files. Write them to a temp workspace at
`/tmp/scaffolded-skills/<skill-name>/` before showing the user.

### 2a. SKILL.md

Use the template in `assets/skill-template.md`.

Fill in:
- **name**: kebab-case slug of the skill (e.g. `weekly-report-builder`)
- **description**: 3–5 sentences. Start with the core action. Then list trigger phrases
  or contexts. End with a "push" sentence that encourages Claude to use it proactively.
  See `references/description-writing.md` for patterns and anti-patterns.
- **Body sections** (use only what's needed — don't pad):
  - `## What This Skill Does` — one paragraph, plain English
  - `## Step-by-Step Workflow` — numbered steps Claude follows
  - `## Input & Output` — what comes in, what goes out
  - `## Examples` — at least one concrete before/after
  - `## Edge Cases & Guardrails` — what to skip or warn about
  - `## Tool Requirements` *(only if external tools needed)*

### 2b. Helper script (if needed)

If the skill involves file transforms, data extraction, API calls, or any deterministic
repeated action, generate a Python helper script inside the **new skill's** scripts folder
(call it `run.py`). Keep it simple.
Add a docstring at the top explaining what it does in plain English.

If no script is needed, skip this file entirely — don't create an empty one.

### 2c. Reference file (if needed)

If the skill has complex domain knowledge (e.g. specific formatting rules, a style guide,
a data schema), write it to the **new skill's** references folder
(call it `domain-knowledge.md`) and reference it from that skill's SKILL.md.
Keep it factual and concise.

### 2d. Sandbox test script

Always generate `scripts/sandbox_test.py`. This script:
1. Imports/references the generated SKILL.md
2. Runs 2–3 lightweight smoke tests against the skill's core actions
3. Prints a simple PASS / FAIL report the user can read without any coding knowledge
4. Does NOT require internet access unless the skill itself needs it

See `references/sandbox-test-patterns.md` for copy-paste test patterns.

---

## Phase 3 — Show the User (Preview Before Install)

Show a friendly, readable summary — NOT raw file contents unless asked.

Use this structure:

```
✅ Here's what I built for you:

📄 The main skill file (SKILL.md)
   Claude will activate this skill when you [trigger summary].
   It will [action summary] and give you [output summary].

🔧 Helper script  ← only if one was created
   A small script that [what it does in plain English].

🧪 Sandbox test
   A quick self-check that makes sure everything works before you install it.

Want me to show you the full files? Or shall I run the sandbox test first?
```

If the user wants to see files, show SKILL.md in a readable code block. Offer to show
helper scripts too. Never show sandbox_test.py to non-technical users unless asked.

---

## Phase 4 — Sandbox Test

Run the sandbox test:

```bash
python /tmp/scaffolded-skills/<skill-name>/scripts/sandbox_test.py
```

Parse the output and present results in plain English:

- If all pass: *"Everything looks good! ✅ All checks passed."*
- If any fail: Show which test failed and why in plain language. Offer to fix it.
  Auto-fix if the issue is minor (missing field, wrong path). Re-run after fixing.
- Never show raw tracebacks to non-technical users. Translate them.

Read `references/sandbox-test-patterns.md` for how to interpret common failures.

---

## Phase 5 — Approval & Install

After a clean sandbox pass, ask:

> "Everything looks great! Should I go ahead and install this skill? Once installed,
> Claude will start using it automatically whenever you [trigger summary]."

If yes, run the install:

```bash
python scripts/install_skill.py --source /tmp/scaffolded-skills/<skill-name>/ --name <skill-name>
```

If the install script is not available (e.g. running in Claude.ai), package the skill
instead:

```bash
python -m scripts.package_skill /tmp/scaffolded-skills/<skill-name>/
```

Then present the `.skill` file to the user and tell them: *"Here's your skill file —
download it and drag it into your OpenClaw skills folder to install."*

After install (or packaging), say:
> "Your **[skill name]** skill is ready! 🎉 Try it by saying: [example trigger phrase]."

---

## Iteration & Updates

If the user asks to change something after the preview or after install:

1. Make the requested change in the temp workspace.
2. Re-run the sandbox test.
3. Show a diff-style summary: *"I changed [X] → [Y]."*
4. Ask for approval again before re-installing.

If the user wants to update an **already-installed** skill:
- Copy it from the installed location to `/tmp/scaffolded-skills/<skill-name>/`
- Make changes there
- Follow the same test → approve → install loop

---

## Reference Files

Read these when needed — don't load all of them upfront:

| File | When to read |
|------|-------------|
| `references/interview-tips.md` | User is vague, hesitant, or giving one-word answers |
| `references/description-writing.md` | Writing the SKILL.md description frontmatter |
| `references/sandbox-test-patterns.md` | Generating or debugging sandbox tests |
| `assets/skill-template.md` | Starting a new SKILL.md from scratch |
