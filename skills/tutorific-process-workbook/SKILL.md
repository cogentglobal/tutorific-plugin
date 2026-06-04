---
name: tutorific-process-workbook
description: Process photographed workbook, test, or textbook pages into structured summaries and error analysis — upload photos in chat and get per-page breakdowns with pattern tracking
---

# tutorific-process-workbook — Batch Process Study Materials

Process photographed or scanned workbook/textbook/test pages into structured summaries, error analysis, and study guides.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## When to Use

- Student or parent has photographed pages from a workbook, test paper, or textbook
- Pages are uploaded in the chat as images
- Goal is to extract questions, concepts, student answers, and identify error patterns

## Input

When invoked, determine:
1. **Subject** — which subject are we processing? (e.g., Math, Natural Science, Social Sciences)
2. **Page numbers** — which pages to process (e.g., "pages 1-19" or "all uploaded")
3. **Book/source name** — what workbook or test is this from?

Ask the user to upload page photos directly in the chat. Process each uploaded image using vision.

## Before Processing

1. Call `get_student()` to load curriculum context and notation conventions.
2. Call `read_patterns({ student, subject })` to understand existing error history.
3. Call `list_page_summaries({ student, subject })` to check what has already been processed.

## Processing Each Page

For each uploaded page image, read the photo and extract:

### Page Summary Structure

```markdown
## Page XX — [Topic Title] ([Strand/Section])

**Workbook:** [Book Name] | **Date on page:** [if visible]

---

### Concepts
- List the key concepts/skills being taught or tested

### Key Rules
- Any rules, formulas, or definitions presented on the page

### Questions & Answers

For EACH question on the page:
- State the question
- Provide the correct answer with working/method
- Note the student's written answer (if visible)
- Flag any errors the student made and explain the misconception

### Areas to Focus On
- 3-5 specific study tips based on what this page covers and any errors found
```

**Important extraction rules:**
- Use notation conventions from the student's curriculum context
- Note any student working/scratch work visible on the page
- If teacher marks are visible (ticks, crosses, comments like "YAY"), include those
- Be precise about what the student wrote vs what is correct

## After Each Page

Call `save_page_summary({ student, subject, page, content })` for each processed page.

## After All Pages

1. Call `update_patterns({ student, subject, findings })` with:
   - New errors found (with page references and underlying misconceptions)
   - New strong areas observed
   - Updated topic coverage
   - Re-evaluated study priorities based on error frequency and severity
   - Updated summary statistics

2. Report to the user:
   - How many pages were processed
   - Key errors found (top 3-5)
   - Key strengths observed
   - Updated study priorities
   - Suggest running a study session on the highest-priority weakness

## Handling Special Pages

- **Demarcation/scope pages:** Extract the test date, page ranges, and topic areas. Call `save_demarcation({ student, subject, content })`.
- **Blank or admin pages:** Skip — note that the page was intentionally not processed.
- **Pages with only teacher comments:** Extract the comments and include in the summary.
