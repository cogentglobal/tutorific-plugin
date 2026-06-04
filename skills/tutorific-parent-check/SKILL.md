---
name: tutorific-parent-check
description: Honest readiness assessment — verdict, kitchen-table questions, and teach-me prompts
---

# tutorific-parent-check — Parent Readiness Assessment

Helps a parent evaluate whether their child genuinely understands a topic and is ready for a test — not just memorised answers. Produces a clear readiness verdict with specific next steps.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When to Use

- The night before or days before a test
- After a study session to verify understanding stuck
- When a parent wants to know "are we done with this topic or not?"

## Input

When invoked, determine:
1. **Subject** — which subject folder
2. **Scope** — specific topic, or "full test" to check all demarcation topics
3. **Child present?** — is the child here now, or is this a parent-only briefing?

If arguments provided (e.g., `tutorific-parent-check Math "full test"`), use those.

## Before Starting

1. Call `get_student()` to load student context.
2. Call `read_patterns({ student, subject })` for known gaps — this is the primary source.
3. If scope is "full test", call `list_demarcations({ student, subject, status: "active" })` then `read_demarcation()`.
4. Call `list_sessions({ student, subject })` to know what's been covered recently.

## Phase 1: Parent Briefing (Child NOT needed yet)

Give the parent a clear, honest overview:

### Readiness Dashboard

```
TOPIC READINESS — [Subject] Test ([Date])

  Strong (ready):
  [tick] Addition strategies
  [tick] Matchstick patterns
  [tick] Data handling (mode, bar graphs)

  Needs practice (almost there):
  [~] 24-hour time conversion — knows the rule but forgets under pressure
  [~] Transformation vocabulary — can do it, can't name it

  Not ready (gaps remain):
  [x] Elapsed time across boundaries — 18 errors in workbook
  [x] Division word problems — cannot connect multiples to division
  [x] Ratio beyond tables — guesses instead of using multiplier
```

### What to Focus On
- Rank the "not ready" topics by test weight and likelihood of appearing.
- Suggest how much time to spend on each (e.g., "30 min on elapsed time, 15 min on division").
- Flag any topics where the child THINKS they understand but their errors suggest otherwise.

### Parent-Friendly Explanations
- For each weak topic, explain IN PLAIN LANGUAGE what the child gets wrong and why.
- No jargon. "She can count in 1500s but when a question says 'how many tickets can you buy with R10 000', she doesn't realise it's the same thing as dividing."
- Suggest what the parent can ask at home to check understanding (kitchen-table questions).

## Phase 2: Check Questions (Child present)

If the child is available, run a structured check. This is NOT a spot test — it's diagnostic.

### How It Works

1. **Pick 2-3 questions per weak topic.** These should be carefully chosen to expose the specific misconception, not just test recall.
2. **Present one question at a time.**
3. **After each answer, ask the child to EXPLAIN their thinking.** This is the key — correct answers with wrong reasoning are red flags.
4. **Listen for:**
   - Can they explain the METHOD, not just give the answer?
   - Do they use the correct vocabulary?
   - Do they catch their own mistakes when asked to double-check?
   - Are they confident or guessing?
5. **For each topic, rate:**
   - **Green:** Understands the concept AND can explain it. Ready.
   - **Amber:** Gets the right answer sometimes but reasoning is shaky. Needs 1-2 more practice rounds.
   - **Red:** Still making the same errors. Needs a focused study session.

### Question Design for Diagnosis
- Include a "trap" question that targets the exact misconception from the student's known error patterns.
- Include a question that requires EXPLAINING, not just calculating (e.g., "Why do we add 12 for PM times?")
- Include a "what's wrong?" question showing a common error.

## Phase 3: Verdict & Plan

### For the Parent

Deliver a clear verdict:

```
READINESS VERDICT: [READY / ALMOST / NOT YET]

Ready topics: [list]
Almost topics: [list] — suggest [X] more minutes of practice
Not ready topics: [list] — suggest [study session / notes review / practice test]
```

### Recommended Next Steps

Based on the verdict, suggest specific actions:

| Verdict | Action |
|---------|--------|
| Green on everything | "You're good. Maybe a quick spot test the night before for confidence." |
| Some amber | "Run through the quick cards for [topics]. Do a spot test tomorrow to check." |
| Any red | "Sit down for a study session on [topic]. Then a spot test to verify." |

### Kitchen-Table Questions

Give the parent 3-5 simple questions they can ask at home WITHOUT needing this tool:
- "What's 4:30 pm in 24-hour time?"
- "If a movie starts at 6:15 pm and lasts 2 hours 20 minutes, when does it end?"
- "You have R12 000 and tickets cost R1 500 each. How many can you buy?"

These should be conversational, not test-like. The parent can ask over dinner or in the car.

### "Teach Me" Prompts

The most powerful check: ask the child to TEACH the parent. This works because:
- If they can explain it clearly, they truly understand it.
- If they can't, you've found the gap — without it feeling like a test.
- The child feels like the expert, which builds confidence.

Give the parent 2-3 "teach me" prompts per weak topic, phrased so the PARENT sounds confused:

- "I can't remember how elapsed time works — if something starts at 10:45 and ends at 1:20, how do you figure that out? Can you show me?"
- "Wait, is 3 pm the same as 15:00 or 03:00? I always get confused."
- "Someone told me you borrow 10 in time subtraction, same as normal maths. Is that right?"

Rules for "teach me" prompts:
- The parent should sound genuinely curious, not quizzy.
- If the child struggles, the parent should NOT correct them — say "hmm, let's look at your notes together."
- If the child explains it well, react with genuine "oh, that makes sense!" energy.
- These work best OUTSIDE study time — car rides, dinner, walking the dog.

## Phase 4: Follow-Up Work with Child (if time allows)

If red or amber topics remain and the child is still available:

1. **Pick the single highest-priority red topic.**
2. **Switch to tutor mode** — guide the child through a mini study session (10-15 min).
3. **Focus on the specific misconception**, not the whole topic.
4. **End with 2-3 check questions** to see if the mini session moved the needle.
5. **Re-rate:** Did it shift from red to amber or green?

## After the Check

- Call `save_parent_check()` with the verdict, topic ratings, and observations.
- If new insights emerged, call `update_patterns({ student, subject, findings })`.
- Save a brief summary so future sessions know what was covered.
