---
name: tutorific-continue
description: Resume a previously paused study session, test, or activity from where it left off — restores context and picks up seamlessly
---

# tutorific-continue — Resume a Paused Session

Resume a previously paused study session, test, or activity from where it left off.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When Invoked

1. Call `list_sessions({ student, subject, status: "paused" })` to find paused sessions.
2. If multiple paused sessions exist, show the user a list and ask which one to resume.
3. If a subject or session is specified (e.g., `tutorific-continue Math`), filter to that.

## Resume Steps

1. Call `read_session({ student, subject, sessionId })` to load the full session state.
2. Call `get_student()` to load current curriculum context.
3. Call `read_patterns({ student, subject })` in case patterns were updated since the pause.

## Resuming the Session

1. **Briefly recap** what was covered last time: "Last session we worked on [X]. You were doing well with [Y] but we were still working through [Z]."
2. **Quick warm-up** — ask 1-2 quick questions from the completed section to re-activate knowledge.
3. **Pick up from the current position** — resume exactly where the session left off.
4. **Follow the remaining plan** from the session state.
5. Continue using the same session flow (study-session phases, test questions, etc.).

## For Resumed Tests

- Re-display the next unanswered question (don't re-ask completed ones).
- Keep the running score from the session state.
- At the end, produce the full mark sheet including questions from both sittings.

## After Completion

- Call `save_session({ student, subject, sessionId, status: "completed" })` when the session finishes naturally.
- Call `update_patterns({ student, subject, findings })` with any new findings from the full session.
- Tell the student their overall progress across both sittings.
