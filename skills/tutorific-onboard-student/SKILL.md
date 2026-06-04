---
name: tutorific-onboard-student
description: Set up a new student — run parent and student interviews, assess learning style, create the student profile. Use when a new family wants to start using Tutorific.
---

# tutorific-onboard-student — Set Up a New Student

Onboard a new student by gathering their profile from TWO separate interviews, assessing their learning style, and creating their account.

**The onboarding has two private interviews:**
1. **Parent Interview** — expectations, observations, concerns (student NOT present)
2. **Student Interview** — how they feel about school, what they like/dislike (parent NOT present)

This separation matters. Parents say things they wouldn't in front of the child. Students open up differently without a parent watching.

## Data Access

This skill uses Tutorific MCP tools for student data. Before starting:

1. Call `get_questionnaire()` to load the interview structure and assessment questions.

All saves go through the corresponding MCP save tools — the skill instructions reference them where needed.

---

## Part 1: Parent Interview (Student NOT Present)

Tell the parent: *"I'd like to chat with you first, without [student] here, so you can be completely honest about what you've observed. Then I'll have a separate chat with [student] to understand things from their side."*

Ask conversationally — don't dump a form. Follow the parent's lead, but cover these areas:

### 1.1 Basics

- **Student's name** — first name
- **Age**
- **Grade/Year**
- **Country**
- **Curriculum** — ask, don't assume. Examples: CAPS (South Africa), Cambridge, IEB, National Curriculum (UK), Common Core (US)
- **School name** (optional — useful for understanding context)

### 1.2 Subjects

- **What subjects are they studying?** — full list
- **Which subjects need the most help?** — prioritise setup
- **Which subjects are they strongest in?** — context for confidence
- **Any upcoming tests or exams?** — capture dates and topics
- **Do they use workbooks? Which ones?** — for material processing later

### 1.3 Parent's Observations (the honest stuff)

These questions are why the parent needs to be alone. Ask open-ended, then probe:

- **"How would you describe [name] as a learner?"** — let them talk freely first
- **"What worries you most about their schoolwork?"** — the real concern, not the polite version
- **"What have you tried that hasn't worked?"** — previous tutors, apps, approaches that failed
- **"What HAS worked, even briefly?"** — any approach that clicked, even once
- **"How do they handle being stuck or confused?"** — give up, get angry, shut down, ask for help, cry, pretend they're fine?
- **"What happens when they get something wrong?"** — how do they react to mistakes?
- **"How long can they focus before quality drops?"** — 5 min, 15 min, 30 min?
- **"Do they show their working, or do everything in their head?"**
- **"Any patterns you've noticed?"** — reads too fast, careless errors, strong verbally but weak on paper, knows the content but freezes in tests, etc.
- **"Anything about how they read questions?"** — skimming, misreading, jumping to answers?

### 1.4 Parent's Expectations

- **"What does success look like to you?"** — specific grades, confidence, independence, less homework battles?
- **"What's your role in their studying currently?"** — do you sit with them, leave them alone, fight about it?
- **"How much time per day is realistic for studying?"** — be honest, not aspirational
- **"Is there anything you want me to know that you wouldn't say in front of [name]?"** — the question that unlocks the real stuff

### 1.5 Additional Context

- **Any learning difficulties or diagnoses?** (ADHD, dyslexia, anxiety, etc.)
- **Any family/social context that affects learning?** (only if volunteered — don't pry)
- **Anything else?**

---

## Part 2: Student Interview (Parent NOT Present)

Tell the student: *"Your [dad/mum] and I had a chat. Now I want to hear from you — just us. There are no wrong answers and I'm not going to tell your parents what you say. I just want to understand how YOU feel about school stuff."*

Keep it light and conversational. Match the student's age and energy. These are NOT test questions.

### 2.1 School Vibe

- **"What's your favourite subject? Why?"**
- **"What subject do you like least? What bugs you about it?"**
- **"If you could change one thing about school, what would it be?"**
- **"Do you feel like your marks show what you actually know?"** — reveals test anxiety vs knowledge gaps

### 2.2 How They Study

- **"When you have a test coming up, what do you normally do to prepare?"** — nothing, re-read, get help, panic?
- **"Do you prefer studying alone or with someone?"**
- **"What makes studying boring? What makes it less boring?"**
- **"If you're stuck on something, what do you do?"** — compare with parent's answer

### 2.3 How They Feel

- **"When you get a question wrong, how does that feel?"** — reveals relationship with mistakes
- **"Is there a subject where you feel like you're actually good at it?"** — find the confidence anchor
- **"What would make you feel more confident going into a test?"**

### 2.4 Fun / Interests

- **"What do you do for fun outside school?"** — useful for analogies and engagement hooks
- **"Do you like games, competition, challenges?"** — reveals if gamification will work
- **"If I could teach you in any way — games, stories, puzzles, challenges, drawing — what sounds the most fun?"**

---

## Part 2.5: Learning Style Assessment (Student Present)

Run this conversational assessment immediately after the student interview, while you still have the student's attention. Frame it as a game, not a test.

Tell the student: *"Last thing — I want to play a quick 'would you rather' game so I know the best way to explain things to you. There are no right or wrong answers — I just want to know what works for YOUR brain."*

Ask each question conversationally. Accept the first honest answer. Aim for 5-8 minutes.

### Section A: How You Take In Information (Learning Modality)

**A1.** *"When you're learning something new, which feels easier — having someone explain it out loud, or reading about it yourself?"*
→ Auditory (explain out loud) / Read-Write (read it myself)

**A2.** *"Would you rather understand something by looking at a diagram or picture, or by writing out the steps?"*
→ Visual (diagram/picture) / Read-Write (writing steps)

**A3.** *"If I'm showing you how to solve a problem, would you rather watch me do it first, or just try it yourself and see what happens?"*
→ Visual/Auditory (watch first) / Kinesthetic (try it first)

### Section B: What Keeps You Going (Mindset & Motivation)

**B1.** *"If you got 4 out of 10 on a test, which thought is closer to what you'd actually think: 'I'm just not good at this subject' — or 'I haven't figured it out yet but I could'?"*
→ Fixed mindset / Growth mindset

**B2.** *"When something is really hard and you keep getting it wrong, do you usually want to keep trying — or does it start to feel pointless?"*
→ High persistence / Low persistence

**B3.** *"What feels better to you — earning a reward (like points, a sticker, a treat) for doing well, or just knowing that you actually got better at something?"*
→ Extrinsic motivation / Intrinsic motivation

**B4.** *"Do you work harder when you're trying to beat someone else, when you're working together with someone, or when you're on your own?"*
→ Competitive / Collaborative / Solo

### Section C: How You Handle Pressure

**C1.** *"When a teacher or parent is watching you work, does it help you focus — or does it make you more nervous?"*
→ Performs well under observation / Pressure-avoidant

**C2.** *"If you get something wrong, would you rather be told immediately so you can fix it, or figure it out yourself first?"*
→ Prefers direct feedback / Prefers self-discovery

**C3.** *"When you're in a real test, do you usually feel pretty calm, a bit nervous but okay, or really anxious?"*
→ Calm / Manageable / High anxiety

### Section D: What Makes Learning Interesting

**D1.** *"Which sounds more fun to you — a game or challenge, a story or real-world example, or just getting to the point quickly?"*
→ Gamification / Narrative / Direct instruction

**D2.** *"Do you like knowing the big picture first ('today we'll learn X so you can do Y') — or do you prefer to just dive in and figure out why later?"*
→ Top-down learner / Bottom-up learner

### Assessment Scoring

Record the dominant profile for each dimension:

| Dimension | Options |
|-----------|---------|
| Learning modality | Visual / Auditory / Read-Write / Kinesthetic (can be mixed) |
| Mindset | Growth / Fixed / Mixed |
| Persistence | High / Moderate / Low |
| Motivation driver | Intrinsic / Extrinsic / Mixed |
| Social style | Competitive / Collaborative / Solo |
| Pressure response | Thrives / Manages / Avoidant |
| Feedback preference | Direct / Self-discovery |
| Test anxiety | Low / Moderate / High |
| Engagement style | Gamification / Narrative / Direct |
| Processing direction | Top-down / Bottom-up |

---

## Part 3: Synthesise and Confirm

After both interviews, synthesise (privately — don't share raw interview notes):

1. **Where do parent and student agree?** — reliable signals
2. **Where do they disagree?** — the interesting gaps (e.g., parent says "she doesn't try" but student says "I do try but I don't understand" = comprehension issue, not effort)
3. **What did the student reveal that the parent doesn't know?** — e.g., test anxiety, feeling stupid
4. **What did the parent reveal that should shape the approach?** — e.g., "we've tried tutors before and she hated it"

### Confirm with Parent

Summarise back to the parent (WITHOUT sharing student's private responses):

```
Student: [Name], Age [X], Grade [X]
Curriculum: [Curriculum], [Country]
Subjects: [list]
Priority subjects: [list]

Key observations:
- [Synthesised trait 1]
- [Synthesised trait 2]
- [Synthesised trait 3]

Session approach:
- [X] min sessions max
- [Approach that will work based on both interviews]
- [What to avoid]

Ready to set up?
```

Wait for confirmation before proceeding.

---

## Part 4: Create the Student Account

After parent confirmation:

1. Call `create_student()` with:
   - Name, age, grade, country, curriculum
   - Subjects list with priority flags
   - Synthesised learning profile
   - Assessment results
   - Session preferences (max duration, approach notes)

2. Call `save_questionnaire_response({ student, responses })` with the interview data (synthesised, not raw).

---

## Part 5: Next Steps

Tell the parent:

1. **Upload materials** — photograph workbook/textbook pages and use the process-workbook skill
2. **Start studying** — use the study session skill for guided practice on any topic
3. **Learning style will evolve** — as sessions happen, patterns and preferences are updated automatically
4. **First session is exploratory** — we'll discover more about how [name] learns by actually working with them

---

## Key Rules

- **Never skip the interviews or the assessment.** The learning style information is what makes the tutor effective.
- **Keep interviews separate.** Parent and student must not hear each other's answers.
- **Run the assessment immediately after the student interview** — same session, while rapport is established.
- **The assessment informs, it doesn't label.** Results are working hypotheses, not permanent traits.
- **Don't share assessment results with the parent in raw form.** Translate to practical implications.
- **Don't share student's private responses with parent.** Synthesise insights, don't quote.
- **Don't assume curriculum.** Always ask.
- **Ask conversationally.** These are conversations, not forms.
