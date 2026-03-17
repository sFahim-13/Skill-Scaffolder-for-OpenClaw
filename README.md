# 🛠️ Skill Scaffolder for OpenClaw
### Build custom AI skills in plain English — works with Claude, GPT-4o, and other LLMs — no coding required

---

> **What this does:** You describe what you want your AI to do. The Skill Scaffolder builds it — writes the files, tests them, and installs the skill — all from a normal conversation. Works with Claude, GPT-4o, and other capable LLMs connected to OpenClaw. No code, no config files, no technical knowledge needed.

---

## Table of Contents

1. [What is a "Skill"?](#1-what-is-a-skill)
2. [What You Need](#2-what-you-need)
3. [Installation — Adding This Skill to OpenClaw](#3-installation--adding-this-skill-to-openclaw)
4. [How to Use It](#4-how-to-use-it)
5. [A Full Walkthrough Example](#5-a-full-walkthrough-example)
6. [What Happens Behind the Scenes](#6-what-happens-behind-the-scenes)
7. [Updating or Changing a Skill](#7-updating-or-changing-a-skill)
8. [Ideas to Get You Started](#8-ideas-to-get-you-started)
9. [Troubleshooting](#9-troubleshooting)

---

## 1. What is a "Skill"?

OpenClaw lets you give your AI custom **skills** — persistent instructions that change how it behaves for specific tasks. This works with any LLM you have connected to OpenClaw: Claude, GPT-4o, Gemini, and others.

Think of it like this:

| Without a skill | With a skill |
|----------------|-------------|
| You explain what you want every single time | Your AI already knows — just ask |
| AI gives a generic response | AI follows your exact format and preferences |
| You copy-paste the same prompt repeatedly | One sentence and it does it perfectly |

**Examples of skills people build:**
- "Every time I paste meeting notes, make a clean action-item list with owners and deadlines"
- "When I ask for a LinkedIn post, keep it under 200 words and use my professional-but-human tone"
- "Whenever I share a PDF, give me: 3 key points, the most important quote, and what I should do next"
- "Always format my to-do list with priority levels and estimated time"

The **Skill Scaffolder** is a skill that builds other skills. You describe what you want in plain English, and it does the rest.

> ⚠️ **Note on LLM choice:** This skill works best with a capable, instruction-following model. See [Section 2](#2-what-you-need) for the recommended models.

---

## 2. What You Need

| Requirement | Details |
|------------|---------|
| **OpenClaw** | Installed on your computer ([openclaw.ai](https://openclaw.ai)) |
| **An LLM connected to OpenClaw** | See recommended models below |
| **This skill installed** | Follow Section 3 below |
| **Coding knowledge** | ❌ Not needed |
| **Technical knowledge** | ❌ Not needed |

### Recommended LLMs

This skill asks your AI to hold a conversation, write structured files, run checks, and fix its own mistakes. That requires a minimum capable model.

| LLM | Works? | Notes |
|-----|--------|-------|
| **Claude 3.5 / 3.7 (Sonnet or Opus)** | ✅ Best | Designed for this kind of task |
| **GPT-4o** | ✅ Great | Fully compatible |
| **GPT-4 Turbo** | ✅ Good | Works well |
| **Gemini 1.5 Pro / 2.0** | ✅ Good | Works well |
| **GPT-3.5 / GPT-4o mini** | ⚠️ Hit or miss | May skip steps or produce incomplete files |
| **Small local models** | ❌ Not recommended | Likely to fail silently |

**Bottom line:** If your model can write a well-structured document and follow multi-step instructions, it will work. If you're unsure, use Claude or GPT-4o.

---

## 3. Installation — Adding This Skill to OpenClaw

You only do this **once**. After that, the Skill Scaffolder is always available.

### Option A — Install from the ZIP file *(easiest)*

1. Go to the [**Releases**](../../releases) page of this repository
2. Download `skill-scaffolder.zip`
3. Unzip it on your computer:
   - **Windows:** Right-click the file → "Extract All"
   - **Mac:** Double-click the file
4. Open **OpenClaw** on your computer
5. Go to **Settings** → **Skills** → **"Install from folder"**
6. Select the unzipped `skill-scaffolder` folder
7. Click **Install**

You should see "Skill Scaffolder" appear in your skills list. ✅

---

### Option B — Install directly from GitHub

1. Open **OpenClaw**
2. Go to **Settings** → **Skills** → **"Install from GitHub"**
3. Paste this URL:
   ```
   https://github.com/sFahim-13/Skill-Scaffolder-for-OpenClaw
   ```
4. Click **Install**

---

### Confirming the install worked

Open a new conversation in OpenClaw and type:

> *"What skills do you have available?"*

You should see **Skill Scaffolder** in the list.

---

## 4. How to Use It

Using the Skill Scaffolder is just a normal conversation. No commands, no special syntax.

**Just describe what you want:**

> *"I want a skill that takes my messy daily notes and organizes them into categories."*

> *"Can you build me a skill for writing cold outreach emails?"*

> *"I want my AI to always summarize YouTube transcripts in 5 bullet points."*

> *"Make a skill that formats my expenses into a clean table."*

That's it. The Skill Scaffolder will take over from there.

---

### What happens next (the 5-step process)

```
You describe what you want
        ↓
Your AI asks 2–4 friendly questions to understand exactly what you need
        ↓
Your AI builds the skill files and shows you a plain-English summary
        ↓
Your AI runs a quick automatic test to check everything is working
        ↓
Your AI asks for your approval — then installs only when you say yes
```

**You stay in control the whole time.** Nothing is installed without your permission.

---

## 5. A Full Walkthrough Example

Here's exactly what a real session looks like, from start to finish.

---

**You:**
> *"I want a skill that takes my grocery list and sorts it by store section — produce, dairy, snacks, etc."*

---

**Skill Scaffolder:**
> *"Love it — let's build that! Just a couple of quick questions so I get it right:*
> *1. Do you usually type your list directly into the chat, or would you upload a file?*
> *2. Would you like it to suggest quantities, or just organize what you give it?"*

---

**You:**
> *"I just type it in chat. No quantities needed, just organize it."*

---

**Skill Scaffolder:**
> *"Perfect, I have everything I need! Here's what I built:*
>
> *📄 **Grocery Organizer Skill***
> *This skill will activate whenever you paste or type a grocery list.*
> *It will sort your items into sections (Produce, Dairy, Meat, Snacks, Pantry, etc.)*
> *and return a clean organized list — nothing else.*
>
> *🧪 Want me to run a quick check to make sure everything looks good before installing?"*

---

**You:**
> *"Yes, run the test."*

---

**Skill Scaffolder:**
> *"✅ All checks passed! The skill is correctly structured and ready to go.*
>
> *Should I go ahead and install it? Once installed, just type or paste any grocery list and it will automatically organize it for you."*

---

**You:**
> *"Yes, install it!"*

---

**Skill Scaffolder:**
> *"🎉 Your **Grocery Organizer** skill is installed!*
> *Try it right now — just paste a grocery list."*

---

**You:**
> *"milk, chips, apples, chicken breast, cheddar cheese, bananas, olive oil, oreos, salmon"*

---

**Your AI (now using your new skill):**
> **🥬 Produce**
> - Apples
> - Bananas
>
> **🥩 Meat & Seafood**
> - Chicken breast
> - Salmon
>
> **🧀 Dairy**
> - Milk
> - Cheddar cheese
>
> **🛒 Pantry**
> - Olive oil
>
> **🍪 Snacks**
> - Chips
> - Oreos

---

That's the whole experience. One conversation. No code touched.

---

## 6. What Happens Behind the Scenes

You don't need to know this to use the skill — but if you're curious:

When the Skill Scaffolder builds your skill, it creates a small folder with these files:

```
your-skill-name/
├── SKILL.md          ← The main instruction file your AI reads
├── scripts/          ← Helper code (only if your skill needs it)
└── references/       ← Extra context your AI refers to (only if needed)
```

The most important file is **SKILL.md** — it's a plain text file that tells your AI exactly what to do, when to do it, and how to format the result. You never need to open or edit it manually. But if you're curious, it looks like a simple document written in plain language.

The **sandbox test** checks that:
- The file structure is correct
- All required sections are present
- No broken references exist
- No unfilled placeholder text remains

If any check fails, the Skill Scaffolder fixes it automatically and re-runs the test before offering to install.

---

## 7. Updating or Changing a Skill

**Want to tweak a skill after installing it?** Just ask:

> *"Update my Grocery Organizer skill — I want it to also add an emoji next to each section header."*

> *"Change my LinkedIn Post skill to keep posts under 150 words instead of 200."*

> *"My Meeting Notes skill is good but I also want it to flag any decisions that were made."*

The Skill Scaffolder will:
1. Load your existing skill
2. Make the change you described
3. Run the test again
4. Show you what changed
5. Ask for approval before updating

---

## 8. Ideas to Get You Started

Not sure what skill to build first? Here are some popular ones:

**For work:**
- Weekly status report formatter
- Email reply drafts (formal / casual / decline)
- Meeting agenda builder from bullet points
- Job description analyzer ("what skills does this role actually need?")

**For writing:**
- Blog post outline from a topic
- Proofreader that preserves your voice
- Social media post variations (Twitter, LinkedIn, Instagram)
- Cover letter customizer

**For personal life:**
- Recipe scaler ("make this for 2 people instead of 4")
- Travel packing list by destination and duration
- Habit tracker summary from daily notes
- Book/movie recommendation explainer

**For learning:**
- Explain any concept at different levels ("explain like I'm 10 / like I'm an expert")
- Flashcard generator from any text
- Quiz maker from notes or documents

---

## 9. Troubleshooting

**The skill installed but my AI isn't using it automatically**

Make sure you're using trigger phrases that match what the skill is designed for. Try asking:
> *"What are the trigger phrases for my [skill name] skill?"*

If the skill still doesn't activate, try uninstalling and reinstalling it.

---

**The sandbox test failed**

This is normal — it means the Skill Scaffolder caught a problem before it affected you. Just tell it:
> *"Fix the test failure and try again."*

It will diagnose and repair the issue automatically.

---

**I described something but the skill doesn't do exactly what I wanted**

Skills can always be refined. After seeing the first version, tell it what's off:
> *"This is close, but I want the output to be shorter / in a table / include X / skip Y."*

The Skill Scaffolder is designed for iteration — your first description doesn't have to be perfect.

---

**I want to delete a skill**

In OpenClaw: **Settings → Skills → [skill name] → Remove**

---

**The skill scaffolder skipped steps or gave incomplete output**

This usually means the LLM you're using isn't powerful enough to follow all the instructions reliably. Try switching to a stronger model (Claude Sonnet, GPT-4o, or Gemini 1.5 Pro) and run the same request again.

---

**Something went wrong and I'm not sure what**

Open an [Issue](../../issues) on this GitHub page and describe what happened. Include:
- What you asked for
- Which LLM you were using
- What the Skill Scaffolder did
- What you expected instead

---

## Contributing

If you build a skill using this scaffolder and want to share it with others, feel free to open a Pull Request or post it in [Discussions](../../discussions).

Improvements to the scaffolder itself — better interview questions, more test patterns, bug fixes — are very welcome.

---

## License

MIT — free to use, share, and build on.
