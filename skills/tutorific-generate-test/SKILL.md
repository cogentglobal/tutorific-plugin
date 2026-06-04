---
name: tutorific-generate-test
description: Generate curriculum-aligned practice tests, then interactively mark and review
---

# tutorific-generate-test — Generate & Mark Practice Tests

Create practice tests from processed material, then interactively guide the student through answering and review their work.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_student({ student: "<name>" })` to load the student's profile, subjects, and curriculum context.
2. Call `read_patterns({ student: "<name>", subject: "<subject>" })` to load known strengths, weaknesses, and error history.

All saves (notes, tests, sessions, patterns) go through the corresponding MCP save tools — the skill instructions reference them where needed.

## Input

When invoked, determine:
1. **Subject** — which subject folder (e.g., `Math/`)
2. **Scope** — specific topics, pages, or "full test" matching a demarcation
3. **Difficulty** — easy (recall), medium (apply), hard (reason/extend), or mixed
4. **Question count** — how many questions (default: 10-15)

If arguments are provided (e.g., `tutorific-generate-test Math "Elapsed Time" medium 10`), use those.

## Before Generating

1. Call `get_student()` to load curriculum context.
2. Call `read_patterns({ student, subject })` to understand known weaknesses — weight questions towards these.
3. If scope is "full test", call `list_demarcations({ student, subject, status: "active" })` then `read_demarcation()` to match the test structure.
4. Call `list_notes({ student, subject })` to find relevant study material for question sourcing.

## Test Generation Rules

### Question Design
- Model questions on the STYLE found in the student's actual workbook — don't invent unfamiliar formats.
- Include a MIX of question types: fill-in, short answer, word problems, multiple choice, draw/describe.
- Weight 60% of questions towards known weak areas, 40% towards strong areas (to build confidence).
- For weak areas, include scaffolded questions: start easy, build to the level where errors typically occur.
- Include at least one question that targets each Priority 1 weakness from the student's known error patterns.
- Ensure questions are grade-appropriate per the student's curriculum context.

### Test Structure
- Group questions by topic/section (matching the workbook or test demarcation structure).
- Number questions clearly.
- Include point values if generating a scored test.
- Provide clear instructions for each section.

### Output Format
Present the test to the student with this structure:

```markdown
# Practice Test — [Topic/Scope]
**Subject:** [Subject] | **Date:** [today] | **Total:** [X] marks

## Section A: [Topic] ([X] marks)
1. [Question] (X)
2. [Question] (X)
...
```

## Interactive Mode (Default)

After generating, run the test interactively:

1. **Present one question at a time** to the student.
2. **Wait for their answer** before proceeding.
3. **Do NOT reveal if the answer is correct immediately.** Instead:
   - Ask "Are you confident in that answer?" or "Can you explain how you got that?"
   - If they're wrong, use Socratic questioning to guide them (follow tutoring rules).
   - Only confirm correctness after they've explained their reasoning.
4. **Track answers** as you go.
5. After the last question, provide a summary.

## Marking & Review

After the test is complete (interactive or written), produce a mark sheet:

```markdown
# Mark Sheet — [Test Name]
**Score:** X / Y ([%])

## Results by Question
| # | Topic | Correct? | Notes |
|---|-------|----------|-------|
| 1 | ...   | Yes/No   | [misconception or praise] |

## Analysis
- **Strengths shown:** [topics]
- **Weaknesses confirmed:** [topics]
- **New issues:** [any new errors not previously tracked]
- **Recommended focus:** [next study priorities]
```

- Call `update_patterns({ student, subject, findings })` with any new findings.
- Call `mark_test()` with scores, answers, strengths, weaknesses, and recommendations.

## Paper Mode

If the student wants to write on paper instead of interactively:
1. Generate the full test and display it for printing.
2. After they're done, ask them to photograph their answers.
3. Read the photo(s) and mark accordingly.
