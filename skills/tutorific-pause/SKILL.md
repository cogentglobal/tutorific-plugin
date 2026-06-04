---
name: tutorific-pause
description: Save the current study session, test, or activity so it can be resumed later — captures progress, observations, and resume instructions
---

# tutorific-pause — Save Session State for Later

Saves the current study session, test, or activity so it can be resumed in a new conversation.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When to Use

- Student needs to stop mid-session (study session, test, note review)
- Context window is getting large and you want to continue fresh
- Switching subjects or tasks but want to come back later

## What to Capture

Gather the following session state before saving:

### Session State

- **Subject** and **Topic**
- **Session type** (study-session / generate-test / study-notes / spot-test)
- **Started** and **Paused** timestamps
- **Paused by** (student request / context limit / subject switch)
- **Original session goal**

### Progress

- What was covered, which phases completed
- Questions answered, concepts discussed
- Any breakthroughs or "aha" moments
- Current phase of the session flow
- Last question/topic being worked on
- Student's state (confident / struggling / making progress / needs a break)
- What still needs to be covered

### Observations

- New strengths discovered
- New weaknesses discovered
- What explanations/approaches worked
- What didn't work

### Test Progress (if applicable)

- Questions completed (X of Y)
- Score so far
- Answers given with correctness
- Remaining questions

### Resume Instructions

Specific notes for the next session about where to pick up, what to revisit, any setup needed.

## Saving

1. Call `update_session_progress({ student, subject, sessionId, state })` with the full session state.
2. Call `save_session({ student, subject, sessionId, status: "paused" })` to persist.

## After Saving

1. Tell the student what was saved.
2. Give a brief summary: "We covered X, Y, Z. Next time we'll pick up with [specific thing]."
3. If any new patterns were observed, call `update_patterns({ student, subject, findings })` before pausing.
4. Remind the student they can resume with the continue skill.
