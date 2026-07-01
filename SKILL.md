---
name: ai-mentor
description: >
  Designs and builds an AI-powered mentoring chatbot that scaffolds and guides students through specific learning materials, theories, or concepts. Produces either a ready-to-use system prompt instruction document for other AI platforms (ChatGPT Custom GPTs, Gemini Gems, Microsoft Copilot, etc.), a deployable React artifact (on Claude.ai), or a technical specification for building a custom application with tools like Claude Code or Codex.
---

# AI Mentor Skill

This skill produces an AI-powered chatbot that mentors students through specific learning materials using evidence-based pedagogical practices. The output is either a portable instruction document for other platforms, a Claude.ai React artifact, or a technical specification for a custom application.

---

## Phase 1: Intake

Run a focused intake conversation before building anything. Provide options for each question where appropriate.

### Required intake information

**Learning Content**
- What subject, theory, framework, or material should the chatbot cover? Ask the educator to paste key content, readings, or summaries directly — the richer the input, the better the chatbot.
- What are the core learning objectives? What should students be able to *do* or *explain* after interacting with the chatbot?

**Learner Context**
- Who are the students? (Year level, prior knowledge assumed, discipline)
- What is the learning purpose? (Introducing new material, consolidating understanding, applying concepts, exam preparation, or a mix)

**Known Difficulties** *(optional — ask if the educator doesn't volunteer this naturally)*
- What do students typically struggle with in this topic? Common questions, recurring misconceptions, or parts of assessments where students consistently do poorly. Use these to shape the chatbot's scaffolding focus and anticipate where students are likely to need more support. It is ok if the instructor is not sure about this.

**Deployment platform** *(it determines the output format)*
- Where will this chatbot be deployed? Options: ChatGPT Custom GPT / Gemini Gem / Microsoft Copilot Studio, Claude.ai (artifact), a custom-built app, or unsure.
- If unsure and you're currently on Claude.ai, default to a Claude artifact and note that a portable instruction document is also available.


### Inferring pedagogical approach
Infer a suitable approach from the learning content and learner context, then confirm it with the educator as part of the intake summary.

Use the following reasoning:

- **Learning purpose** is the primary signal. Introduction to new material → lean explanatory to build orientation before Socratic questioning. Consolidation or application → lean Socratic. Exam preparation → mix of retrieval and feedback.
- **Content type** matters. Conceptual or applied content (theories, frameworks, case analysis) warrants Socratic guidance. Definitional, procedural, or prerequisite content warrants direct instruction.
- **Prior knowledge** shapes scaffolding depth. Lower prior knowledge → more scaffolding, shorter Socratic leaps, more direct support before questioning. Higher prior knowledge → reduce scaffolding sooner, target higher Bloom's levels.
- **Bloom's level targets** follow from the learning objectives. Map each objective to a level and set the chatbot's questioning strategy accordingly (see `references/pedagogy.md`).
- **Checkpoints** should be proportional to session length and content complexity. For short focussed interactions, embed checks naturally in dialogue. For longer or multi-concept sessions, include explicit checkpoints after each major concept.

### Intake output

Summarise your inferred approach and ask the educator to confirm before building:
- Deployment platform and output format
- Subject and core concepts
- Learning objectives (numbered)
- Target learner and context
- Known difficulties or common misconceptions (if provided) and how the chatbot will address them


---

## Phase 2: System Prompt Design

The chatbot's quality depends almost entirely on its system prompt. This phase is the same regardless of deployment platform. Read `references/pedagogy.md` for the full framework before writing.

```
# [Chatbot Name] — AI Tutor Instructions

## Purpose
[One paragraph: what this chatbot does and who it's for]

## Learning Objectives
[Numbered list]

## Knowledge Base
[All subject content, theories, definitions, examples]

## How to Teach
[Full pedagogical behaviour rules as derived from Phase 2:
Socratic / direct decision logic, Socratic patterns (elicitation, elaboration, contradiction,
hypothesis, consequence, transfer, reflection, meta-inquiry), scaffolding sequence,
confusion handling, feedback approach, cognitive load considerations, checkpoint strategy]

## Conversation Flow
[Opening move → prior knowledge probe → content progression → reflection consolidation →
meta-inquiry → closing summary]

## Boundaries
[What the chatbot will and will not do]
```

### System prompt structure

1. **Identity and purpose** — Who the chatbot is and what it's here to do
2. **Learning objectives** — Paste the confirmed objectives verbatim
3. **Content knowledge base** — All educator-provided material: theories, definitions, examples, key distinctions. Be thorough — the chatbot can only teach what's in the prompt.
4. **Pedagogical behaviour rules** — The specific instructional strategy for this chatbot: when to use Socratic questioning vs. direct explanation, how to scaffold, how to handle errors and confusion, how to manage cognitive load, when and how to use checkpoints (derived from `references/pedagogy.md`)
5. **Known difficulties** (include if educator provided them) — Common misconceptions, typical errors, or areas where students struggle. The chatbot should anticipate these, probe for them early, and provide targeted scaffolding when they surface.
6. **Conversation flow** — Opening move, prior knowledge elicitation, content progression, closing
7. **Boundaries** — What the chatbot will and will not do (e.g., "Do not complete assessment tasks for students", "Stay within the scope of [topic]")

Show the educator the system prompt draft and invite refinement before generating the final output.

---

## Phase 3: Build the Output

### Path A — Instruction Document Only (for other platforms)

Produce a structured .md file the educator can paste directly into the platform's system prompt or instructions field. Use `references/instructions-template.md` as the baseline structure, populating each section with the confirmed content from Phase 2.

**Platform-specific setup notes:**
- *ChatGPT Custom GPT*: paste into the "Instructions" field; advise uploading content as a file if the knowledge base is large and suggest conversation starters to guide the user into the intended flow
- *Gemini Gem*: paste into the "Instructions" field; advise uploading content as a file if the knowledge base is large
- *Microsoft Copilot Studio*: provide as the system topic instruction block
- *Generic / unknown*: paste wherever the platform accepts system-level instructions

---
### Path B — Claude.ai: React Artifact

Read `references/artifact-template.md` for the full component template and implementation notes.

**Core requirements:**
- Chat interface with message history (user/assistant bubbles)
- Calls `https://api.anthropic.com/v1/messages` with `claude-sonnet-4-20250514`
- Full conversation history passed on each turn (stateful)
- Loading indicator while awaiting response
- System prompt embedded in the API call — never visible to the student
- Collapsible learning objectives panel
- Quick-action buttons: "Give me a hint", "Check my understanding", "Summarise so far"
- Clean, accessible interface (16px+ font, sufficient contrast, keyboard navigable)
- Graceful error handling

---

### Path C — Custom Application (Claude Code / Codex)

For educators who need a more customised experience — such as integration with institutional systems, custom UI, persistent student data, or features beyond what a chat artifact supports — guide them toward building a standalone application.

**When to recommend Path C:**
- The educator explicitly mentions wanting a custom application
- Requirements exceed what a single-page artifact can deliver (e.g., authentication, database, multi-page flows)
- The chatbot needs to be embedded elsewhere

**What to produce:**
1. The system prompt from Phase 2 (same as Paths A and B)
2. A technical specification document covering:
   - Recommended architecture (e.g., frontend framework, API integration pattern)
   - How the system prompt should be embedded
   - Key features to implement (conversation history, learning objectives display, quick actions)
   - Accessibility requirements
3. Clear instructions for using the spec with Claude Code, Codex, or similar agentic coding tools to scaffold the application

**Note**: This path requires the educator (or a developer) to have access to agentic coding tools and a deployment environment. Confirm this before proceeding. If the educator lacks technical resources, recommend Path A or Path B instead and note that Path C remains an option if development support becomes available.

--- 

## Phase 4: Handoff

1. Briefly explain the pedagogical choices made and why — in plain language
2. **Path A**: suggest deployment options (share artifact link, use as in-class demo, embed if hosted)
3. **Path B**: give exact setup steps for the target platform
4. **Path C**: provide the system prompt and technical spec; explain how to use them with Claude Code, Codex, or similar tools
5. Offer to produce the *other* format — educators often want both a Claude demo tool and a portable version for students
6. Remind them the chatbot's knowledge is bounded by the system prompt — if content changes, the instructions should be updated

---

## Reference files

- `references/pedagogy.md` — Scaffolding framework, Bloom's taxonomy, Socratic judgement, productive failure, ZPD, cognitive load, feedback model, self-explanation, and ownership return. **Read before writing the system prompt.**
- `references/instructions-template.md` — Baseline system prompt structure with pedagogical scaffolding, Socratic patterns, and conversation flow. **Use as the starting point for all system prompts.**
- `references/react-template.md` — React component template with API integration, UI layout, and accessibility notes. **Read for Path A only.**

Path C does not have a separate template — it uses the system prompt from Phase 2 and a bespoke technical specification tailored to the educator's requirements.