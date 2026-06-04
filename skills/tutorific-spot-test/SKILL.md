---
name: tutorific-spot-test
description: Quick-fire quiz — 5-10 rapid questions with instant feedback
---

# tutorific-spot-test — Quick Fire Quiz

A fast, informal quiz to check if a concept has actually stuck. No setup, no mark sheets — just rapid-fire questions and instant feedback.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When to Use

- Right after reading study notes ("Did that sink in?")
- At the end of a study session as a quick check
- Random revision — "Quiz me on time" or "Quiz me on anything"
- Parent wants a quick 5-minute check before dinner

## Input

When invoked, determine:
1. **Subject** — which subject (default: current working directory)
2. **Topic** — specific topic, or "mix" for random questions across all processed topics
3. **Count** — how many questions (default: 5, max: 10)

If arguments provided (e.g., `tutorific-spot-test Math "24-hour time" 5`), use those.

## Before Starting

1. Call `get_student()` to load curriculum and notation context.
2. Call `read_patterns({ student, subject })` to weight questions towards weak areas.
3. If a topic is specified, call `list_page_summaries({ student, subject })` for question material.

## How It Works

### Rules
- **One question at a time.** Wait for the answer before moving on.
- **Keep it snappy.** No long setups — get to the question fast.
- **Mix difficulty.** Start with 1-2 easy ones to build confidence, then ramp up.
- **Instant feedback.** Unlike a full practice test, give feedback right after each answer — but still ask "how did you get that?" before confirming.
- **No marks or scores.** Just thumbs up/down vibes. At the end, say what went well and what needs more work.
- **If they get one wrong, give one more on the same concept.** Don't move on until they've had a chance to get it right.

### Question Style
- Short, punchy questions. Not word problems (save those for a full practice test).
- "What is 3:45 pm in 24-hour time?"
- "How many minutes in 3/4 of an hour?"
- "How much time from 10:20 to 11:05?"
- "Borrow in time subtraction: you borrow ___?"
- Mix of: fill-in, convert, calculate, true/false, "what's wrong with this?"

### "What's Wrong?" Questions (great for known error patterns)
- Present a WRONG answer (modelled on the student's own past mistakes) and ask them to spot and fix the error.
- "Someone says half past 10 is 10:45. What did they get wrong?"
- "A student calculated 7:45 am in 24-hour time as 19:45. What's the mistake?"

## After the Spot Test

Give a casual summary:
- "Nice — you nailed the 24-hour conversions. Elapsed time across midnight still needs work."
- If 3+ questions wrong on one concept, suggest the user invoke the study session skill for deeper practice.
- Do NOT update patterns for spot tests (too informal). Only update if a genuinely new pattern emerges.
