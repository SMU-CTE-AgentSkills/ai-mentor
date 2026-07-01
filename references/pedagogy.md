# Pedagogical Framework Reference

This file documents the principles to apply when writing the chatbot's system prompt. Use it to make deliberate, justified instructional choices — not generic "helpful assistant" defaults.

---

## 1. Socratic Questioning — With Judgement

The Socratic approach guides students to construct understanding through questioning rather than direct instruction. It is the default for higher-order learning, but it is not appropriate in every moment. Apply it selectively.

### When to use Socratic questioning
Use it when the student is working within or just above their current understanding — where guided effort leads to genuine insight:
- Applying a concept to a new situation
- Analysing relationships between ideas
- Evaluating claims or justifying positions
- Reflecting on their own reasoning
- Consolidating something they've been introduced to

### When to give direct answers instead
Do not use Socratic questioning for:
- **Recall and definition**: If a student needs a factual definition or basic term to proceed, give it. Withholding it creates friction without learning benefit.
- **Prerequisite gaps**: If a student lacks foundational knowledge required for the current task, fill the gap directly, then continue.
- **Factual clarification**: If a student is confused about something stated in the material, clarify it directly.
- **Basic orientation**: At the opening of a session, when a student needs to know what the chatbot does or how to engage, explain clearly.
- **Genuine confusion blocking progress**: If a student is stuck and not making progress through questioning, explain and then use a follow-up question to check understanding.

The test: ask whether a Socratic question here helps the student *think harder* or just *wait longer*. If the latter, explain.


### Core Socratic patterns (when appropriate)

**Elicitation** — Draw out prior knowledge before introducing content
> "What do you already know about X?"
> "How would you explain this to someone unfamiliar with the topic?"

**Elaboration** — Press for depth and precision
> "What exactly do you mean by [term they used]?"
> "Can you say more about that?"

**Contradiction** — Surface inconsistencies and probe flawed definitions
> "You said X, but earlier you mentioned Y — how do you reconcile those?"
> "How are you defining [term]? Does that definition hold in this case?"
> "If we accept that, doesn't it also mean [reductio]?"

**Hypothesis** — Invite explanatory proposals
> "What do you think might explain this pattern?"

**Consequence** — Explore implications
> "If that's true, what would follow from it?"

**Transfer** — Probe whether understanding generalises
> "How would that apply in [different context]?"

**Reflection** — Summarise and consolidate before progressing
> "So what you're saying is... — is that a fair summary?"
> "What's the core claim you're making here?"

**Meta-inquiry** — Invite the student to examine the reasoning process itself
> "What do you think I'm trying to get you to see with these questions?"
> "What would it take to actually resolve this question?"

---

## 2. Productive Confusion and Productive Failure

### Productive vs. unproductive confusion

Confusion is not inherently bad. *Productive confusion* occurs when a student is actively grappling with a problem that is within reach — their struggle is activating and differentiating knowledge. *Unproductive confusion* occurs when a student lacks the prerequisite knowledge or orientation to engage meaningfully, and continued struggle leads only to frustration and disengagement.

**Signals of productive confusion**: The student is attempting an answer, asking clarifying questions, or showing partial understanding.

**Signals of unproductive confusion**: The student is disengaged, giving non-answers, repeating the same error without variation, or expressing significant frustration.

When confusion is productive, maintain it — ask a reframing question or draw attention to a relevant feature, but do not resolve it immediately. When confusion is unproductive, intervene with direct instruction and then return to guided questioning once orientation is restored.

### Productive failure

Productive failure involves two phases:

1. **Generation and exploration**: Before introducing a canonical solution or explanation, have the student attempt to generate their own. Even incorrect attempts activate and differentiate prior knowledge, creating better conditions for learning when the correct explanation follows. Ask the student to attempt a problem or formulate an explanation *before* you provide one.

2. **Consolidation**: After the student has attempted generation (correctly or not), provide the accurate explanation or worked solution. Connect it explicitly to what the student tried — highlight what was on the right track and where it diverged.

Operationally: pose the problem first, invite an attempt, then teach from the attempt.

---

## 3. Zone of Proximal Development (ZPD)

The ZPD is the gap between what a student can do independently and what they can do with support. Effective tutoring operates in this space — not below it (too easy, no learning) and not above it (too hard, no traction).

**Calibrate to the ZPD by:**
- Assessing what the student already knows before pushing further
- Adjusting the complexity and length of Socratic leaps based on the student's responses
- Reducing scaffolding as the student demonstrates competence
- Recognising when a student has exceeded their ZPD and providing more direct support before resuming questioning

**Analogy-based bridging**: When a student lacks the knowledge to engage with a problem directly, turn it into a learnable example by analogy. Find a domain the student likely knows, construct an analogous problem there, and use the student's reasoning in the familiar domain as a production rule they can transfer back to the target domain. Make the structural mapping explicit.

---

## 4. Scaffolding Sequence

When a student is stuck, apply support in increasing order of directness. Do not jump straight to giving the answer.

1. **Reframe** — Ask a question that draws attention to a relevant aspect the student may have overlooked
2. **Partial answer** — Provide a starting point or constrain the problem, and ask the student to complete it
3. **Full explanation** — Provide the answer with explicit reasoning, then immediately ask the student to paraphrase or apply it
4. **Return ownership** — After any support, ask the student to adapt, apply, critique, or extend what they've been given. The goal is to restore agency, not dependency.

The last step is critical: every time you provide scaffolding, close with a task that hands control back to the student.

---

## 5. Bloom's Taxonomy

Target the appropriate cognitive level for the learning objectives and content. Do not default to recall.

| Level | Verb examples | Chatbot question pattern |
|---|---|---|
| 1. Remember | define, list, name | Give directly — do not Socratise recall |
| 2. Understand | explain, summarise, paraphrase | "In your own words, what does X mean?" |
| 3. Apply | use, solve, demonstrate | "How would X apply in this situation?" |
| 4. Analyse | compare, differentiate, examine | "What's the key difference between X and Y?" |
| 5. Evaluate | justify, critique, argue | "What are the strengths and weaknesses of X?" |
| 6. Create | design, construct, propose | "Using X, how would you approach this problem?" |

For most higher education contexts, target Level 3 and above. For introductory content or students with low prior knowledge, begin at Level 2 and advance.

---

## 6. Self-Explanation

Prompting students to explain their own reasoning is one of the most reliable ways to improve understanding. It surfaces gaps, strengthens connections, and supports accurate self-monitoring.

**Use self-explanation prompts:**
- "Walk me through your reasoning on that."
- "How did you arrive at that answer?"
- "Why does that make sense to you?"
- "What part of that are you least certain about?"

Self-explanation is most effective when students are accurately monitoring their own understanding. Support this by occasionally asking students to rate their confidence or identify their own uncertainty before you give feedback.

---

## 7. Feedback — Three Essential Questions

Effective feedback addresses three questions (Hattie & Timperley):

1. **Where am I going?** (Feed up) — Is the student clear on the goal? Restate the learning objective when a student seems directionless.
2. **How am I going?** (Feed back) — How does the student's current response compare to the goal? Give specific, accurate feedback on what is and isn't working.
3. **Where to next?** (Feed forward) — What should the student do now to close the gap? Give a concrete next step — a question to consider, an aspect to revisit, or a connection to make.

Do not give feedback that only answers question 2. Always close with question 3.

**Wrong-answer handling:**
1. Acknowledge the thinking: "That's a reasonable direction because..."
2. Identify the specific error or gap, not just "that's incorrect"
3. Ask the student to revise with the new information, or pose a reframing question

---

## 8. Questions That Work

Questions should be designed to be answerable — not rhetorical hurdles. A question the student cannot plausibly answer from their current knowledge teaches nothing and erodes confidence.

Principles for effective questions:
- **Ground in the student's last response.** Questions that follow directly from what the student just said feel like dialogue, not interrogation. Pick up a thread from their answer.
- **Draw attention to what they're not yet seeing.** Good questions redirect focus to information or a relationship the student has overlooked, without revealing the answer.
- **One question at a time.** Multi-part questions split attention and dilute effort. Ask one thing.
- **Answerable at the current level.** Calibrate to the ZPD — a question should stretch but not overwhelm.

---

## 9. Cognitive Load

Learning requires working memory, which is limited. Avoid overloading the student.

**Reduce extraneous load:**
- Introduce one concept at a time before connecting them
- Avoid long explanations when a short one will do
- Do not ask questions that require holding too many new ideas simultaneously

**Manage intrinsic load:**
- For complex content, break it into components and sequence from simpler to more integrated
- Check understanding of each component before adding the next

**Use germane load wisely:**
- Elaboration, self-explanation, and application all increase load in productive ways — but only when the student has sufficient working memory available. If a student is already struggling, reduce other demands before adding reflection tasks.

**Signal in the system prompt**: Instruct the chatbot to introduce content incrementally, check understanding before progressing, and avoid multi-concept questions until individual concepts are secure.

---
