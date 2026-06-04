---
name: tutorific-study-notes
description: Generate consolidated study notes — summaries, mind maps, flashcards, quick cards
---

# tutorific-study-notes — Generate Consolidated Study Notes

Create focused, student-friendly study notes for a topic, section, or full test preparation.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## Input

When invoked, determine:
1. **Subject** — which subject folder (e.g., `Math/`)
2. **Scope** — specific topic, strand, page range, or "full test prep"
3. **Format** — summary sheet, mind map (text-based), flashcards, or step-by-step guide

If arguments are provided (e.g., `tutorific-study-notes Math "Time" summary`), use those.

## Before Generating

1. Call `get_student()` to load curriculum context and notation conventions.
2. Call `read_patterns({ student, subject })` to understand what needs emphasis.
3. Call `list_page_summaries({ student, subject })` for the requested scope.
4. If scope is "full test prep", call `list_demarcations({ student, subject, status: "active" })` then `read_demarcation()` for test scope.

## Note Generation Rules

### Content Principles
- Notes must be in **student-friendly language** — match the student's grade level.
- Lead with **what the student already knows** (strong areas), then build to weak areas.
- Include the student's **own common mistakes** as "Watch out!" callouts — these are more powerful than generic warnings.
- Every rule or formula must have a **concrete example** worked through step by step.
- Use the **same notation and terminology** as the workbook (from the student's curriculum context).

### What to Include
- Key definitions and rules (in simple language)
- Step-by-step methods for each problem type
- Worked examples (modelled on actual workbook questions)
- "Watch out!" boxes for known error patterns
- Quick-reference tables where useful (e.g., fraction-decimal conversions, time units)
- Practice tips specific to the student's misconceptions

### What NOT to Include
- Content outside the requested scope
- Advanced concepts above grade level
- Generic study advice not tied to specific content

## Output Formats

**IMPORTANT: Always generate BOTH a full summary AND a quick card for every topic.** The summary is for learning; the quick card is for revision. Two files, always.

### Summary Sheet (always generated)
The full learning document with worked examples, Watch out! boxes, and step-by-step methods. Call `save_notes()` after generating.

```markdown
# [Topic] — Study Notes
**Subject:** [Subject] | **Pages:** [X-Y]

## Key Rules
- [Rule 1]: [simple explanation + example]
- [Rule 2]: [simple explanation + example]

## Step-by-Step Methods

### How to [solve this type of problem]
1. [Step]
2. [Step]
3. [Step]
**Example:** [worked through]

## Watch Out!
- [Common mistake from the student's error history + how to avoid it]

## Quick Reference
[Tables, conversion charts, etc.]
```

### Quick Card (always generated alongside the summary)

A one-page, rules-only reference card. No worked examples, no Watch out! boxes — just the key facts, tables, and rules in the most compact form possible. Call `save_notes()` after generating.

The quick card should:
- Fit on a single printed page
- Use tables and shorthand — no full sentences where a table row will do
- Be scannable in under 60 seconds
- End with 3 memorable golden rules for the topic
- Feel like a cheat sheet, not a document

### Mind Map (text-based)
An indented text hierarchy showing how concepts connect. Good for visual learners.

```markdown
# [Topic] — Mind Map

[Central Concept]
├── [Branch 1]
│   ├── [Detail]
│   └── [Detail]
├── [Branch 2]
│   ├── [Detail]
│   └── [Detail]
└── [Branch 3]
    └── [Detail]
```

### Flashcards
Question-answer pairs for self-testing. Call `save_notes()` after generating.

```markdown
# [Topic] — Flashcards

**Q1:** [Question]
**A1:** [Answer]

---

**Q2:** [Question]
**A2:** [Answer]
```

- Include 15-25 cards per topic.
- Mix recall questions with "what would you do if..." application questions.
- Include 3-5 cards specifically targeting known weak areas.

### Step-by-Step Guide
A detailed walkthrough of a single method or problem type. Best for topics where the student has a specific procedural gap.

## Full Test Prep Mode

When scope is "full test prep":
1. Call `list_demarcations({ student, subject, status: "active" })` then `read_demarcation()` to identify all topics.
2. Generate a summary sheet for EACH topic area in the demarcation.
3. Create a master "cheat sheet" that fits on 1-2 pages with the most critical rules and watch-outs.
4. Suggest a study schedule based on priority (most time on Priority 1 weaknesses).
5. Call `save_notes()` for each generated file.

## After Generating

- Call `save_notes()` for each generated note (summary + quick card).
- Suggest running a study session on the weakest topic, or a practice test for reinforcement.

## Student Feedback Loop

After the student reads the notes, ask for quick feedback:

1. **Clarity:** "Was anything confusing or hard to follow? Which bit?"
2. **Length:** "Too long, too short, or about right?"
3. **Usefulness:** "What was the most helpful part? What didn't help?"
4. **Missing:** "Is there anything you still don't understand that wasn't covered?"

Use feedback to:
- Revise the current notes if specific issues are flagged.
- Update the student's patterns via `update_patterns()` with learning style preferences discovered.
- Inform future note generation for this student.
