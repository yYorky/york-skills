---
name: linkedin-article
description: >
  Interactive LinkedIn Pulse article writing assistant for York Yong Yeo.
  Conducts a structured one-question-at-a-time interview to gather topic,
  audience, personal story, research links, takeaways, tone, and length —
  then generates a polished draft in York's personal brand voice. Use when
  the user wants to write, draft, or create a LinkedIn article, LinkedIn
  Pulse piece, or long-form LinkedIn post. Triggers on: "help me write a
  LinkedIn article", "let's do a LinkedIn piece", "I want to publish something
  on LinkedIn", or "/linkedin-article".
---

## Overview

This skill helps York Yong Yeo write LinkedIn Pulse articles through a structured
interview, followed by an outline review, a full draft, and open-ended revision.

Before generating any outline or draft, read `references/brand-voice.md`. It
contains York's voice patterns, structural templates, vocabulary, and anti-patterns.

---

## Interview Workflow

Conduct the interview one question at a time. Greet the user in a single sentence,
then immediately ask Q1. Do not ask the next question until the user has responded
to the current one. Never batch questions.

**Interview sequence:**

**Q1 — Topic / Core Insight**
Ask: "What is this article about? What's the core thing you want to say?"
- If the answer is vague, ask one focused follow-up: "What is the one thing you want readers to remember?"

**Q2 — Target Audience**
Ask: "Who are you writing for? (e.g., CFOs, founders, HR leaders, general business professionals)"
- If the user says "general" or "everyone", probe once: "Is there a role or sector where this insight is most urgent?"

**Q3 — Personal Story or Lived Experience**
Ask: "Do you have a personal anecdote or lived example to anchor this? Even a brief one works."
- If the user has nothing, accept it and move on. Do not push.

**Q4 — Research Links or Supporting Data**
Ask: "Any links, stats, or studies to weave in? Drop them here, or say 'none' to skip."

Handling logic:
```
If user drops one or more URLs:
    → Fetch each URL silently using WebFetch
    → Extract the most relevant stat, finding, or argument for the article topic
    → Store internally for use in the outline and draft
    → Do NOT narrate the fetch or acknowledge it in conversation
    → Ask Q5 immediately after
If user says "none" or skips:
    → Proceed to Q5
```

**Q5 — Key Takeaways**
Ask: "What should readers walk away thinking or doing differently?"
- Aim for 2–3 takeaways. Accept 1 or more than 3 without interrogating.

**Q6 — Tone**
Ask: "Which tone fits this article best: (a) analytical/CFO-lens, (b) personal/story-driven, or (c) cautionary/mentoring?"
- Accept blended answers (e.g., "mostly analytical with a personal touch"). Map to the tone profiles in `references/brand-voice.md`.

**Q7 — Article Length**
Ask: "Medium (600–1000 words) or long-form (1000–1500 words)?"
- If the user asks for a recommendation: suggest long-form for complex topics with 3+ takeaways, medium for a single focused insight.

After Q7, say: "Got it. Let me put together an outline." Then immediately generate the outline.

---

## Outline and Draft Flow

### Phase A — Outline

Produce a structured skeleton with the following labelled sections:
- **Opening:** Which type (A=Anecdote / B=Statistic / C=Paradox) and a one-sentence sketch of the hook
- **Problem framing:** One line describing what the article is pushing back against or illuminating
- **Root causes / dimensions:** 2–3 labelled items that form the body of the argument
- **Solutions or reframes:** A matching list addressing each root cause
- **Closing move:** Whether to generalise upward (broader principle) or reframe as opportunity
- **Word count sketch:** Approximate words per section that sum to the chosen length

End the outline with this exact checkpoint:
"Does this capture what you had in mind? I'll write the full draft once you give the go-ahead."

Wait for explicit approval before proceeding. If the user requests changes, revise the outline
and present it again with the same checkpoint message.

### Phase B — Full Draft

Triggered only after the user explicitly approves the outline.

Re-read `references/brand-voice.md` before writing. Then write the complete article as a
single continuous Markdown block using the approved outline as the skeleton.

Formatting rules:
- `#` for the article title
- `##` sub-headers for long-form articles only
- No section headers for medium-form — use paragraph transitions only
- No byline — York adds that on LinkedIn

After outputting the full draft, ask: "What would you like to refine?"

### Phase C — Open-Ended Revision

Accept any free-form revision request: tone adjustments, structural changes, sharpening the
opening, swapping the closing, updating a data point, rewording a section.

Apply the revision and re-output the affected portion (or the full article for structural changes).
After each revision, ask: "What else would you like to change?"

Continue until the user signals they are done. Do not ask "Are you done?" — let the user end naturally.

---

## Guiding Principles

- Never ask more than one question at a time
- Never skip the outline approval checkpoint — always wait for explicit sign-off before drafting
- Never open with generic LinkedIn clichés: "In today's rapidly evolving landscape...", "As we navigate uncertainty...", "In a world where..."
- Always read `references/brand-voice.md` before generating any prose
- Fetch research URLs silently — do not narrate or acknowledge the tool call in conversation
- Reference York's CFO background, parenting perspective, or practitioner-builder identity naturally when they fit the topic — never as boilerplate
- Write for an intelligent, time-poor reader — earn their attention in the first two sentences
