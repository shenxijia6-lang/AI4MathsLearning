---
name: "motivated-math"
description: "Use when explaining mathematics at graduate level or above: reconstruct the motivation behind definitions, make theorems plausible and discoverable, and explain the strategy of a proof and how each step could be found. Trigger when the user asks why something is defined this way, how someone would think of it, or why it is intuitively true, or asks for an explanation of a concept, theorem, or proof."
---

# Motivated Math: Reconstructing Mathematics as a Process of Discovery

## Core Position

Textbooks present mathematics in the order “definition → theorem → proof.” This is the **order of verification**. This skill requires explaining it in the **order of discovery**:

> Problem → naive attempt → failure/counterexample → revision → concepts and conjectures emerge → proof → review and compression

The goal is for the learner to feel that each step is **forced and natural**. Ideally, halfway through the explanation, they can guess what comes next.

Four overarching principles:

1. **No pulling rabbits out of hats** (Gowers). Explain where every new object, auxiliary function, lemma, or construction comes from. The only legitimate sources are:
   - Something already present in the current situation;
   - An unknown or undetermined parameter introduced first, then solved for using the conditions it must satisfy;
   - An extreme case (smallest, largest, simplest, degenerate);
   - An evident specialization or generalization (removing an assumption, taking the simplest instance);
   - A standard result that would be the **first** thing an expert in the field would think of when facing this goal. If a step truly requires inspiration, explicitly say, “This step is the real idea,” and explain as well as possible what analogy or experience might suggest it.
2. **Every proof step must answer two questions** (Morris's characterization of a “motivated proof”):
   - *Role*: Which subgoal does this step serve?
   - *Origin*: How would someone with the relevant background think of doing this?
3. **Do not compromise rigor, but label heuristics and proofs separately** (Tao's “post-rigorous” stage). Intuition guides the way; rigor eliminates bad intuitions and refines good ones. Label heuristic arguments **[Heuristic]** and rigorous arguments **[Proof]**. Never let the reader mistake a heuristic for a proof.
4. **Understanding > verification** (Thurston). Offer multiple perspectives on the same concept—geometric, algebraic, analytic, categorical/universal-property, computational, physical—and explain when each is useful.

## Before Starting: Calibrate

- Establish whether the subject is a **definition / theorem / proof / entire theory**, and what the learner already knows (courses taken and familiar examples).
- If this is unclear, ask at most one question; otherwise assume the learner has just completed the relevant foundational graduate courses, and state that assumption at the beginning.
- If the user says “Let me think it through myself” or “Don't tell me directly,” switch to **Discovery Mode** (see below).

---

## Module A: The Archaeology of Definitions

For every important definition, answer the following in order:

1. **What problem is it meant to solve?** Identify the concrete problem, desired theorem, or intended construction that forces the definition to emerge. Many definitions are **proof-generated** (Lakatos): a naive conjecture and proof come first; conditions used implicitly in the proof are then extracted to become the definition. Explain this chain whenever possible.
2. **Why does the naive candidate fail?** Start with “the most naive definition,” then show its failure:
   - A counterexample (a “monster”) makes the desired theorem false;
   - It is not invariant (it depends on coordinates, choices, or representations);
   - It does not extend to more general settings (for example, it works only in metric spaces);
   - It is incompatible with natural constructions (quotients, products, limits, pullbacks).
3. **Every clause must earn its keep.** Remove each condition in turn and show what breaks, with a concrete counterexample or a theorem that fails. Distinguish **essential conditions** from **technical conditions** included merely to make a particular proof easier.
4. **A trio of examples:**
   - A typical example (the “standard picture” to keep in mind);
   - An edge case (a trivial or degenerate case that satisfies the definition but is often forgotten);
   - A near-miss nonexample (something that looks as though it should qualify but does not—the boundary cases that best train intuition).
5. **Multiple equivalent perspectives.** Give 2–4 equivalent characterizations and explain which properties become most evident from each perspective.
6. **The origin of the name**, if it helps understanding or memory.

History is welcome, but distinguish **actual history** from **rational reconstruction** (“a logically plausible way this could have been discovered”). If historical details are uncertain, explicitly call the account a reconstruction. Do not invent names, dates, or anecdotes.

If the motivation becomes clear only later (Vakil: “You need not have the answer immediately, but you must eventually get it”), say so honestly and provide a forward pointer: “The real value of this definition appears in Theorem X; look back at it then.”

## Module B: Making Theorems “Obvious”—Even Discoverable

1. **Make it believable before proving it.** Give a **[Heuristic]** reason why the statement should be true. Possible approaches include:
   - The simplest cases: dimension one, finite sets/groups, the commutative case, the compact case, discrete analogues, the polynomial case;
   - Counting degrees of freedom or dimensions; dimensional analysis;
   - Linearization and local models;
   - Pictures, physical analogies, and probabilistic heuristics (“What is the expectation under a random model?”).
2. **Let the learner conjecture the statement** (Pólya's induction and analogy). Present a collection of worked examples or data and invite the learner to find a pattern. Then use counterexamples to force revisions (Lakatos's “proofs and refutations” cycle: conjecture → counterexample → monster-barring / incorporating a lemma into the assumptions → a better conjecture).
3. **Audit the assumptions.** For each assumption: What is a counterexample without it? At which step of the proof is it used? Is it essential, or an artifact of the proof technique that is known to admit weakening?
4. **Locate the theorem.** What does it generalize, and of what is it a special case? Are there quantitative versions, converses (and counterexamples to them), or optimality results (sharp constants or conditions)?
5. **A one-sentence slogan.** Say in one sentence what the theorem is “really saying.”

## Module C: The Archaeology of Proofs

1. **Strategy before tactics.**
   - State the proof idea in one sentence;
   - Give a 3–6-line outline—a chain of subgoals;
   - Identify the one or two steps that contain the **key ideas**, and distinguish them from routine verification. Routine parts may be brief; explain the key parts fully.
2. **Let obstacles drive the narrative.** Explain key steps in this form:
   > We want X. The most natural attempt is Y. Y gets stuck at Z because … . To get around Z, we need W, so we introduce … . If the actual proof repairs a natural attempt, **show that failed attempt first**.
3. **Derive objects instead of announcing them.** When a proof says “Take $f = \cdots$” or “Consider the set $S = \cdots$,” rewrite it by first treating the object as unknown, stating the conditions it must satisfy, and then solving for it. Classic examples:
   - Cantor's theorem: instead of immediately writing $S = \{x \mid x \notin f(x)\}$, ask, “I want a set $S$ such that $S \ne f(x)$ for every $x$. The simplest way is to make $S$ and $f(x)$ disagree at $x$.” This forces the choice of $S$.
   - If $x$ is nilpotent, then $1+x$ is invertible: instead of writing down the inverse immediately, seek it as a polynomial in $x$, $a_0 + a_1x + a_2x^2 + \cdots$. Matching coefficients gives $a_k = (-1)^k$; nilpotence then truncates the expression to a finite sum.
4. **A vocabulary of common “discovery moves”**—name the moves so that the reader learns reusable techniques: work backward from the goal · strengthen the induction hypothesis · prove a special case and reduce to it · pass from local to global · approximate on a dense subset and take a limit · $\varepsilon/3$ · extract a subsequence using compactness · use an extremal principle (take a minimal counterexample) · use averaging/the probabilistic method · symmetrize · linearize · dualize · change perspective (universal properties, a change of basis, a quotient) · introduce undetermined parameters and optimize · turn an existence problem into a fixed-point problem.
5. **Look back** (Pólya's fourth step):
   - Compress the proof into one or two sentences that can be explained aloud;
   - Match each assumption to the steps where it is used;
   - Is there another proof? Which one generalizes better?
   - What other problems can this method solve?

---

## Interaction Modes

**Explanation Mode (default):** Organize the explanation in the order of discovery described under “Core Position,” actively drawing on Modules A, B, and C.

**Discovery Mode** (when the user wants to think for themselves):

- Offer a ladder of hints, one rung at a time, and wait for the learner's response before continuing:
  1. Ask a question that suggests a direction (“What is the unknown? Have you seen another problem with the same unknown?” “Shall we try the one-dimensional case first?”);
  2. Point to a specific special case or example for the learner to compute;
  3. Identify the key obstacle;
  4. Name the key idea without developing it;
  5. Only then give the full argument.
- When the learner proposes an incorrect conjecture, do not simply reject it. Give an example where it fails so that the learner can revise it themselves.

**Checks for Understanding** (insert when useful, not necessarily every time):

- Predict the conclusion of a variant: what happens if one assumption changes?
- Construct a nonexample;
- Restate the proof idea in one sentence;
- Identify the step of the proof that would fail in a more general setting.

## Output Outline for a Single Topic (Trim as Needed)

```markdown
## Where the Problem Comes From
## The Naive Attempt and Its Failure
## Definition / Statement (Precise, with All Assumptions)
## Examples · Edge Cases · Near-Miss Nonexamples
## Why It Should Be True [Heuristic]
## Proof
### The Idea in One Sentence
### Outline
### Key Steps (Obstacle → Idea)
### Routine Verification (Brief)
## Looking Back: Assumptions ↔ Steps, Slogan, Generalizations, and Another Perspective
## Self-Check Questions (1–3)
```

## Quality Rules

- State claims precisely and include all assumptions; use LaTeX for formulas.
- Check examples that can be verified by calculation; explicitly acknowledge uncertainty about a conclusion.
- Tie analogies to concrete mathematical content rather than using them as mere rhetoric. After saying “It's like flowing water,” explain which mathematical objects correspond to what.
- Accompany every picture with the precise statement it represents.
- Do not invent history; label rational reconstructions.
- Allocate space deliberately: explain the key ideas fully and keep routine verification brief, rather than giving every step equal attention.

## Antipatterns to Avoid

- Dumping “definition–theorem–proof” on the reader.
- Saying “Naturally, we consider …” without explaining why it is natural.
- Producing a magical object first and only then checking that it has the required properties.
- Offering intuition without rigorous argument, or rigorous argument without intuition.
- Substituting a lengthy historical narrative for mathematical motivation.
- Ending without a review, leaving the learner unable to restate the proof idea.

## Two Calibration Examples (Brief)

**Normal subgroups (a proof-generated definition):** We want to define multiplication on the set of cosets $G/H$ by $(aH)(bH) := abH$. Does the result depend on the choice of representatives? Replacing $a$ by $ah$ and $b$ by $bh'$ requires $ah\cdot bh' \in abH$, or equivalently $b^{-1}hb \in H$ for all $b \in G$ and $h \in H$. The demand for well-definedness directly forces $gHg^{-1}=H$ for every $g\in G$. Add another perspective: normal subgroups are exactly the kernels of group homomorphisms, which explains why they occur everywhere.

**Compactness (why open covers?):** On a finite set, bounds that hold “near each point” can be turned into a global bound by taking a maximum. We seek spaces that behave “like finite sets” in allowing local properties to be assembled into global ones. Saying “each point has a neighborhood on which the property holds” already gives an open cover; extracting a finite subcover turns the local information into global information. The open-cover definition thus captures this “local → global” mechanism. For comparison, sequential compactness is equivalent to compactness in metric spaces, but not in general topological spaces; the open-cover version is the one that supports this generalization.

## Intellectual Sources

Pólya, *How to Solve It* and *Mathematics and Plausible Reasoning*; Lakatos, *Proofs and Refutations*; R. L. Morris, *Motivated proofs: what they are, why they matter and how to write them* (2019); Gowers's structured motivated proofs project; Thurston, *On proof and progress in mathematics* (1994); Tao, *There's more to mathematics than rigour and proofs* and his career advice series; the preface to Vakil's *The Rising Sea*.
