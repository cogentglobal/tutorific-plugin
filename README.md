# Tutorific — AI Study Companion

Tutorific is an AI-powered study companion that helps students prepare for tests and exams. It uses Socratic questioning — guiding students to discover answers themselves rather than giving answers directly.

## What You Get

| Skill | What it does |
|-------|-------------|
| **Study Session** | Interactive tutoring on any topic — warm-up, concept building, practice, challenge |
| **Generate Test** | Curriculum-aligned practice tests with detailed marking and feedback |
| **Spot Test** | Quick-fire 5–10 question quiz with instant feedback |
| **Study Notes** | Consolidated notes — summaries, quick cards, flashcards |
| **Study Plan** | Day-by-day schedule with teach-me prompts for parents |
| **Exam Planner** | Multi-subject exam calendar balancing workload across subjects |
| **Parent Check** | Honest readiness assessment — verdict, kitchen-table questions, next steps |
| **Process Workbook** | Upload photographed pages for structured summaries and error analysis |
| **Onboard Student** | Set up a new student — interviews, learning style assessment, profile creation |
| **Pause** | Save session state to resume later |
| **Continue** | Resume a paused session from where you left off |

Plus **5 specialist agents** (Claude Code / Cowork): Tutor, Examiner, Noter, Processor, Parent Advisor.

## Prerequisites

- A **paid Claude plan** (Pro, Max, Team, or Enterprise) — plugins require a paid plan
- A **Tutorific account** — the plugin connects to the Tutorific MCP server for student data storage

## Install

### Claude Code (CLI)

```
/plugin marketplace add cogentglobal/tutorific-plugin
```

Then install the plugin:

```
/plugin install tutorific
```

### claude.ai (Desktop / Web)

1. Go to **Settings** → **Plugins**
2. Click **"Add marketplace"**
3. Enter: `cogentglobal/tutorific-plugin`
4. Find **Tutorific** in the plugin list and click **Install**

### Verify

After installing, start a new conversation and try:

> "Help me study for my Math test on fractions"

The Tutorific study session skill should activate automatically.

## How It Works

Tutorific connects to a remote MCP server that stores student data — profiles, error patterns, session history, study materials, and test results. The skills handle the tutoring methodology; the server handles the data.

On first use, the MCP server will prompt you to sign in via your browser (OAuth). After that, your session stays active.

## Updates

When the plugin is updated, pull the latest version:

- **Claude Code:** `/plugin update tutorific`
- **claude.ai:** Updates are pulled automatically when you reload

## Built by

[Collaboration Studio](https://github.com/cogentglobal)
