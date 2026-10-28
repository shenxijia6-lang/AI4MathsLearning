# AI4MathsLearning

[简体中文](README.md) | English

> **Tools for accelerating mathematics learning in the age of AI.**

AI assistants can already read alongside you, answer questions and check proofs. But being able to answer is not the same as helping you learn faster. A generic answer can be correct and still unhelpful: it skips the exact step you were stuck on, or hands you the conclusion before you had a chance to find it yourself.

This repository collects tools you can install directly into an AI assistant (Claude, Codex and others): skills, prompts and workflows. Each one targets a specific bottleneck in learning mathematics, such as not seeing why a definition is what it is, not being able to follow a proof, or not knowing whether your own proof is right, and adjusts how the AI responds so that it actually shortens the time it takes to learn.

Every tool can be installed and used on its own, and each comes in both Chinese and English.

## Contents

| Name | Type | What it does |
| --- | --- | --- |
| [motivated-math](skills/motivated-math/SKILL.en.md) ([中文](skills/motivated-math/SKILL.md)) | Skill | Explains graduate-level mathematics and above: recovers the motivation behind definitions, makes theorems guessable and believable, and shows how each step of a proof could have been found |

More tools will be added over time.

---

## motivated-math

### The bottleneck it addresses

Textbooks are written in the order definition → theorem → proof. That is the order of **verification**. Learners usually get stuck because they cannot see the order of **discovery**: what problem forced this definition? Why should this theorem be true? How would anyone think of that auxiliary function in the proof? Without that, all that's left is memorization, which is slow and doesn't carry over to new problems.

### What it does

It has the AI explain mathematics in the **order of discovery**:

```text
Problem → naive attempt → failure / counterexample → revision → concepts and conjectures emerge → proof → review and compression
```

The goal is for every step to feel **forced and natural**. Ideally, halfway through you can guess what comes next.

It has three modules:

- **The archaeology of definitions**: what problem the definition solves; why the most naive definition fails; what breaks when each condition is removed in turn; a typical example, an edge case and a near-miss nonexample; several equivalent perspectives.
- **Making theorems "obvious"**: first a heuristic reason the statement should hold (simplest cases, dimension counting, linearization, physical analogies, …), then an audit of the assumptions, and where the theorem sits: what it generalizes and what it is a special case of.
- **The archaeology of proofs**: strategy before tactics; key steps told as "we want X → the natural attempt is Y → it gets stuck at Z → so we introduce W"; auxiliary objects are **derived**, not announced; and a closing review that compresses the proof into a sentence or two you could say out loud.

A few hard rules:

- No pulling rabbits out of hats. Every new object has to come from somewhere; where a step really does take inspiration, it says so ("this step is the real idea").
- Heuristic arguments are labeled **[Heuristic]** and rigorous ones **[Proof]**, and the two are never mixed up.
- No invented history. A "this is how it could logically have been discovered" rational reconstruction is labeled as such.

Two interaction modes:

- **Explanation Mode** (default): a full explanation of a concept, theorem or proof.
- **Discovery Mode**: switched on when you say something like "let me think it through myself" or "don't tell me directly". The AI gives one hint at a time, from a question that suggests a direction up to the key idea, and gives the full argument only at the end. If you propose a wrong conjecture, it gives an example where the conjecture fails so you can fix it yourself.

### What using it looks like

Once installed, just ask. The AI will use the skill when it fits:

- "Why are normal subgroups defined this way?"
- "Why is compactness defined with open covers rather than with sequences?"
- "How would someone come up with the proof of the Hahn–Banach theorem?"
- "Don't tell me the answer. Help me find the proof of Cantor's theorem myself."

You can also call it by name (see "How to invoke" for each platform below).

---

## Installation

The skill folder contains two files:

```text
skills/motivated-math/
├── SKILL.md       # Chinese (default)
└── SKILL.en.md    # English
```

AI assistants only read a file named `SKILL.md`. The commands below install the English version by copying `SKILL.en.md` into place as `SKILL.md`. To use the Chinese version instead, see [the end of this section](#using-the-chinese-version).

First, get the repository:

```bash
git clone https://github.com/shenxijia6-lang/AI4MathsLearning.git
cd AI4MathsLearning
```

### Claude

#### Claude on the web, desktop and mobile apps (claude.ai)

1. Open **Settings → Capabilities** and make sure **Code execution and file creation** (called **Create and edit files** in the updated settings layout) is turned on. Skills depend on it.
2. Package the English version as a zip. **The zip must have the `motivated-math/` folder at its root**, not `SKILL.md` directly at the root:

   ```bash
   mkdir -p build/motivated-math
   cp skills/motivated-math/SKILL.en.md build/motivated-math/SKILL.md
   cd build && zip -r motivated-math.zip motivated-math
   ```

3. Open **Customize → Skills**, click **+** → **Create skill** → **Upload a skill**, and upload `motivated-math.zip`.
4. Check that the skill is turned on in your skills list.

> Team / Enterprise plans: an organization owner needs to enable Skills and code execution on the Policy tab of **Organization settings → Plugins & skills**. Owners can also provision the skill for the whole organization from there.

#### Claude Code

Install for yourself, available in every project:

```bash
mkdir -p ~/.claude/skills/motivated-math
cp skills/motivated-math/SKILL.en.md ~/.claude/skills/motivated-math/SKILL.md
```

Or install into a single project (you can commit it to that project's git to share it with your team):

```bash
mkdir -p /path/to/your-project/.claude/skills/motivated-math
cp skills/motivated-math/SKILL.en.md /path/to/your-project/.claude/skills/motivated-math/SKILL.md
```

**How to invoke**: Claude loads the skill automatically when your question matches it. You can also type `/motivated-math` at the start of a message.

**No restart needed**: Claude Code picks up new skills automatically. The one exception: if the `~/.claude/skills` directory was created after the current session started, run `/reload-skills` once.

### Codex

Works with the Codex CLI, the IDE extension and the Codex app.

Install for yourself, available in every project:

```bash
mkdir -p ~/.agents/skills/motivated-math
cp skills/motivated-math/SKILL.en.md ~/.agents/skills/motivated-math/SKILL.md
```

Or install into a single project (under `.agents/skills/` at the project root):

```bash
mkdir -p /path/to/your-project/.agents/skills/motivated-math
cp skills/motivated-math/SKILL.en.md /path/to/your-project/.agents/skills/motivated-math/SKILL.md
```

> Older versions of Codex read skills from `~/.codex/skills/`. If the skill doesn't show up after installing, update Codex first; if you can't, copy it into `~/.codex/skills/motivated-math/` instead.

**How to invoke**: Codex uses the skill automatically when your question matches it. You can also mention it with `$motivated-math`, or pick it from the list with `/skills`.

Codex detects new skills automatically. If it doesn't appear, restart Codex.

### One-command install for Claude Code and Codex (optional)

These options install the folder as it is in the repository, so the **Chinese** `SKILL.md` will be the active one. Follow each with the swap commands below to switch to English.

Inside Codex, with the built-in installer:

```text
$skill-installer install https://github.com/shenxijia6-lang/AI4MathsLearning/tree/main/skills/motivated-math
```

Or, if you have Node.js, with the community tool [skills](https://github.com/vercel-labs/skills) (made by Vercel, not an official Anthropic or OpenAI tool):

```bash
npx skills add shenxijia6-lang/AI4MathsLearning --skill motivated-math -g -a claude-code -a codex
```

`-g` installs into your user directory (global); leave it out to install into the current project. `-a` chooses which tools to install for.

Then switch each installed copy to English. The installed folder already contains `SKILL.en.md`, so run this inside it:

```bash
cd ~/.claude/skills/motivated-math && cp SKILL.en.md SKILL.md   # Claude Code
cd ~/.agents/skills/motivated-math && cp SKILL.en.md SKILL.md   # Codex
```

If an installer put the skill somewhere else (for example `~/.codex/skills/`), run the same `cp SKILL.en.md SKILL.md` in that folder.

### Using the Chinese version

The two versions have the same content in different languages. To use the Chinese one, copy the whole folder instead, which keeps the Chinese `SKILL.md`:

```bash
# Claude Code
cp -r skills/motivated-math ~/.claude/skills/
# Codex
cp -r skills/motivated-math ~/.agents/skills/
# claude.ai: zip the folder as is
cd skills && zip -r motivated-math.zip motivated-math
```

### Updating

```bash
cd AI4MathsLearning
git pull
```

Then run the install commands for your platform again (or rebuild and re-upload the zip).

---

## Where the ideas come from

- G. Pólya, *How to Solve It* and *Mathematics and Plausible Reasoning*
- I. Lakatos, *Proofs and Refutations*
- R. L. Morris, *Motivated proofs: what they are, why they matter and how to write them* (2019)
- T. Gowers's structured motivated proofs project
- W. Thurston, *On proof and progress in mathematics* (1994)
- T. Tao, *There's more to mathematics than rigour and proofs* and his career advice series
- R. Vakil, the preface to *The Rising Sea*

## Feedback and contributions

[Issues](https://github.com/shenxijia6-lang/AI4MathsLearning/issues) and pull requests are welcome, especially:

- cases where the AI, even with this skill, **still** dumps definition–theorem–proof on you (please include your question and its answer);
- examples you thought were explained especially well;
- better calibration examples (short ones where you can see at a glance how the motivation forces the definition).

## License

This repository is licensed under the [MIT License](LICENSE).
