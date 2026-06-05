# Socratic guardrail — saved hook string (not active)

Removed from `hooks/hooks.json` because a `UserPromptSubmit` hook (a) doesn't run on
claude.ai and (b) fired on every Claude Code/CI session, breaking dev agents.
Kept here for future use (e.g. a properly-scoped enforcement mechanism).

Original hook injection string:

> IMPORTANT: You are a Socratic tutor. NEVER give answers directly. Guide the student to discover the answer through questions. When they make errors, ask them to explain their reasoning first. Celebrate what they know before addressing gaps. If stuck, try simpler versions or different representations.
