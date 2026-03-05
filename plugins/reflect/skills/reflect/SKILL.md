---
name: reflect
description: Use at the end of a session to reflect on what happened. Reviews the conversation, interviews the user about what went well or poorly, then suggests improvements to existing skills, CLAUDE.md, and new skills that would be useful.
---

# Reflect

End-of-session retrospective that turns experience into lasting improvements.

## Invocation

### `/reflect`

No arguments needed. This skill works from the current conversation context.

## Phase 1: Session Review

Look back over the conversation and build a summary:

1. **What was attempted** - List the main tasks and goals from the session
2. **What was accomplished** - Which tasks succeeded, what was the outcome
3. **What struggled** - Where did things get stuck, take multiple attempts, or go wrong
4. **Patterns noticed** - Recurring friction, tool usage patterns, communication gaps

Present this summary to the user concisely (bullet points, not paragraphs).

## Phase 2: Interview

Ask the user focused questions to surface insights you can't see from the transcript alone. Ask 2-4 questions, not more. Adapt based on what happened in the session. Examples:

- "What felt slow or frustrating?"
- "Was there anything I did that you'd want done differently next time?"
- "Were there points where I misunderstood what you wanted?"
- "Is there anything you had to repeat or correct multiple times?"
- "Did the end result match what you had in mind?"

Wait for the user's responses before proceeding to Phase 3. Do not skip this step.

## Phase 3: Suggestions

Based on the session review and user feedback, produce concrete suggestions in three categories:

### Existing skill improvements

For each installed skill that was used or relevant during the session, suggest specific changes. Reference the skill by name and describe what to change and why. Only suggest changes backed by evidence from this session.

### CLAUDE.md improvements

Suggest additions or changes to the project's CLAUDE.md (or ~/.claude/CLAUDE.md) that would prevent problems seen in this session. These should be durable preferences or conventions, not one-off instructions. Examples:
- "Add: always run tests before committing"
- "Add: prefer X pattern over Y in this codebase"
- "Remove/update: rule Z caused friction because..."

### New skill ideas

Propose new skills that would have helped during this session. For each:
- **Name**: short slug
- **What it does**: one sentence
- **Why**: what problem from this session it would solve

Only propose skills that address real friction from the session, not hypothetical needs.

## Output Format

After the interview, present suggestions as a clear list under each category. If a category has no suggestions, say so explicitly rather than forcing something.

Ask the user which suggestions (if any) they'd like to implement right now. If they choose any, make the changes immediately.

## Guidelines

- Be honest, not diplomatic. If something went wrong because of a mistake, say so plainly.
- Keep the interview conversational, not like a survey.
- Suggestions should be specific and actionable, not vague ("improve error handling" is bad; "add a retry with backoff when the GitHub API returns 429" is good).
- Don't suggest changes you aren't confident about. Fewer good suggestions beat many mediocre ones.
