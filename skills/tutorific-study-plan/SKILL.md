---
name: tutorific-study-plan
description: Day-by-day study schedule with teach-me prompts and kitchen-table questions
---

# tutorific-study-plan — Study Schedule Generator

Generates a realistic, day-by-day study plan based on how many days are left, what the child knows, and how much daily time is available. Keeps it simple — short sessions, rest days, and a confidence-building finish.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When to Use

- After processing workbook material, to plan the days before a test
- When a parent asks "what should we cover and when?"
- To reset or adjust a plan mid-way through preparation

## Input

When invoked, determine:
1. **Subject** — which subject folder
2. **Test date** — when is the test?
3. **Daily time** — how many minutes per day can the child study? (default: 15-20 min)
4. **Rest days** — any days to skip? (default: one mid-week rest day auto-inserted)

If arguments provided (e.g., `tutorific-study-plan Math "March 10" 20`), use those.

## Before Starting

1. Call `get_student()` to load student context.
2. Call `read_patterns({ student, subject })` for gap analysis.
3. Call `list_demarcations({ student, subject, status: "active" })` and `read_demarcation()` for test scope if applicable.
4. Call `list_sessions({ student, subject })` to check what's already been covered.

## Planning Principles

### The Science (keep it invisible to the parent)
- **Spaced repetition** — revisit weak topics across multiple days, not in one block.
- **Interleaving** — mix topics within sessions where possible.
- **Retrieval practice** — favour testing over re-reading. Spot tests and "teach me" moments beat staring at notes.
- **Desirable difficulty** — ramp up gradually. Don't front-load the hardest material.

### The Reality (make it visible to the parent)
- **15-20 minutes max per session** for a primary school child. Hard stop.
- **One rest day minimum** — the brain consolidates during downtime.
- **Start easy, end easy** — first session builds confidence, last session before the test is light and positive.
- **Never more than 2 weak topics per day** — focus beats coverage.
- **The night before is NOT for cramming** — it's for a gentle spot test on things they already know, to walk in feeling good.

## Output Format

### The Schedule

```
STUDY PLAN — [Subject] Test ([Date])
[X] days remaining | [Y] min/day | [Z] rest day(s)

Day 1 — [Day, Date]
  What: [activity description]
  Tool: [skill to use]
  Focus: [specific topic]
  Time: [X] min
  Parent tip: [one-liner for the parent]

Day 2 — [Day, Date]
  ...

[Rest Day — no studying. Let it settle.]

...

Night Before — [Day, Date]
  What: Confidence round — easy spot test on strong topics
  Tool: spot test
  Time: 10 min
  Parent tip: End on a high. "You've got this."

TEST DAY — [Date]
  No morning cramming. Breakfast, deep breath, go.
```

### Topic Distribution

Show how weak topics are spaced across the plan:

```
TOPIC COVERAGE MAP

Elapsed time (RED):     Day 1 ──── Day 3 ──── Day 5 (review)
Division words (RED):   Day 2 ──── Day 4
24-hour time (AMBER):   Day 1 ──── Day 4 (spot check only)
Ratio (AMBER):          Day 3 ──── Day 5 (spot check only)
Strong topics:          Day 6 (confidence round) ── Night before
```

### "Teach Me" Moments

For each weak topic, give the parent a "teach me" prompt they can use casually — not during study time, but at dinner, in the car, whenever:

```
TEACH ME PROMPTS (use these anytime, no tools needed)

"I can't remember — how do you figure out the time between 10:45 and 1:20?"
"Wait, is 3pm the same as 15:00 or 03:00? I always mix those up."
"If I have R12 000 and each ticket is R1 500... how many can I get? I'm stuck."
"Can you explain to me what 'translate' means when they're talking about shapes?"
```

These should be tailored to the actual weak topics and phrased so the child feels like they're HELPING the parent, not being tested.

### Kitchen-Table Questions

Separate from "teach me" prompts — these are quick-fire factual questions the parent can drop into conversation:

```
QUICK QUESTIONS (drop these into conversation)

"What's 7:30 pm in 24-hour time?"
"How many minutes in 3/4 of an hour?"
"What do you borrow in time subtraction — 10 or 60?"
```

## Plan Adjustments

Include a note at the bottom:

```
ADJUSTMENTS
- If a session goes badly → don't extend it. Stop, take a break, pick it up next session.
- If a session goes brilliantly → stop on the win. Don't push further.
- If you miss a day → don't double up. Just shift the plan forward.
- If everything is green by Day [X] → switch remaining days to light spot tests only.
- Run a parent readiness check 2 days before the test to get a final readiness verdict.
```

## After Generating

- Call `save_study_plan()` with the plan structure.
- Suggest the parent takes a photo of the schedule or sticks it on the fridge.
- Remind them: the plan is a guide, not a contract. Flexibility matters more than completion.
