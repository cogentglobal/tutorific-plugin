---
name: tutorific-exam-planner
description: Multi-subject exam preparation calendar balancing workload across subjects
---

# tutorific-exam-planner — Multi-Subject Exam Preparation

Generates a coordinated study plan across multiple subjects for an exam period. Balances workload, respects exam dates, and ensures adequate coverage of all subjects.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When to Use

- At the start of an exam period (2-4 weeks before first exam)
- When demarcation booklet has been processed into subject folders
- When parent asks "how do we prepare for all these exams?"

## Input

1. **Student** — which student repo
2. **Exam period** — start and end dates (or "June exams", "November exams")
3. **Daily time** — total study minutes available per day (default: 45-60 min)
4. **Priority subjects** — any subjects to weight more heavily (optional)

## Before Starting

1. Call `get_student()` to load the student's full subject list and curriculum context.
2. For each subject in scope, call `list_demarcations({ student, subject, status: "active" })` then `read_demarcation()` for exam scope.
3. For each subject, call `read_patterns({ student, subject })` for known gaps.
4. Count days until each exam. Identify rest days, holidays, revision days.

## Planning Principles

### Time Allocation
- **More time for harder subjects** — weight by difficulty AND days until exam
- **Diminishing returns** — no subject gets more than 40% of total daily time
- **Minimum viable coverage** — every subject gets at least 2 sessions before its exam
- **Buffer time** — leave 20% unscheduled for catch-up or extra practice

### Sequencing
- **Proximity rule** — intensity increases as exam approaches
- **Interleaving** — mix subjects within a day (max 2 subjects per day)
- **No cramming** — nothing new the day before an exam
- **Rest before clusters** — if 2+ exams in 2 days, rest day before the cluster

### Session Design
- **15-20 min per subject** for younger students
- **25-30 min per subject** for older students
- **Switch subjects** after each session to maintain freshness
- **End on strength** — last session of the day should be something they're good at

## Output Format

### Master Calendar

```
EXAM PREP CALENDAR — [Exam Period]
[Student] | [X] subjects | [Y] days | [Z] min/day

Week 1: Foundation
─────────────────────────────────
Mon [Date]
  AM: [Subject 1] — [topic] (20 min)
  PM: [Subject 2] — [topic] (20 min)
  
Tue [Date]
  AM: [Subject 3] — [topic] (20 min)
  PM: [Subject 1] — [topic] (20 min)

[REST DAY — brain consolidation]

...

Week 2: Intensify
─────────────────────────────────
...

Week 3: Final Push
─────────────────────────────────
[Date] — EXAM: [Subject]
  Morning: Light confidence round only
  
[Date]
  Focus: [Next exam subject]
...
```

### Subject Coverage Matrix

Show how each subject is distributed:

```
COVERAGE MATRIX

Subject          | Sessions | Focus Areas           | Exam Date
─────────────────|──────────|───────────────────────|──────────
Mathematics      | 8        | Algebra, Fractions    | Jun 1
Natural Sciences | 6        | Electricity, Atoms    | Jun 5
English HL       | 7        | Poetry, Literature    | Jun 9, 17
EMS              | 4        | Economic cycle        | Jun 8
Geography        | 5        | Maps, Climate         | Jun 19
...
```

### Daily Breakdown Format

For each day, provide:

```
[Day] [Date] — [X] days to [next exam]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Session 1 (AM): [Subject]
  What: [specific activity]
  Tool: [skill name]
  Focus: [topic from demarcation]
  Time: [X] min

Session 2 (PM): [Subject]
  What: [specific activity]
  Tool: [skill name]
  Focus: [topic from demarcation]
  Time: [X] min

Parent tip: [one actionable tip]
Kitchen-table question: "[casual question to ask at dinner]"
```

### Exam Day Protocols

```
EXAM DAY PROTOCOLS

[Subject] — [Date]
  Night before: Confidence round on strong topics only (10 min max)
  Morning: No studying. Breakfast, check equipment, deep breaths.
  After exam: Brief debrief, then switch focus to next exam.
```

## Adjustments Section

```
ADJUSTMENTS

If behind schedule:
  → Don't double up. Cut lowest-priority topics, not rest days.
  
If ahead of schedule:
  → Add spot tests, not new content. Reinforce, don't expand.

If a session goes badly:
  → Stop. Take a break. Try a different approach next session.
  
If everything is clicking:
  → Reduce intensity. Over-preparation breeds anxiety.

Emergency triage (if running out of time):
  1. Focus on high-mark sections first
  2. Know something about everything > everything about something
  3. Past papers > notes > textbook
```

## After Generating

1. Call `save_study_plan()` with the master plan.
2. Suggest creating individual subject plans for subjects that need more detailed breakdowns.
3. Suggest printing the calendar for the fridge.
4. Set up check-in points: "Run a parent readiness check for each subject 2 days before its exam."

## Example Invocation

Ask the user for their student name, exam period, and available study time. For example: "Plan Beau's June 2026 exams with 60 minutes of study time per day."
