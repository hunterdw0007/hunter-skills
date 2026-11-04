---
name: eisenhower-matrix
description: Sorts tasks into an Eisenhower Matrix (Do, Schedule, Delegate, Eliminate) by guessing each task's quadrant and asking short adaptive questions only about unclear tasks, then prints the matrix as a markdown 2x2 table, one per area of life (e.g. Work, Home) when the tasks span several. Supports adding tasks later, moving, removing, completing, and re-interviewing tasks. Use when the user mentions an "Eisenhower matrix" or asks for help prioritizing tasks, e.g. "help me prioritize these tasks" or "what should I work on first".
---

# Eisenhower Matrix

Sort the user's tasks into four quadrants and keep the matrix up to date across the conversation.

## Definitions

Use these definitions. Do not swap in your own.

- **Important**: the task has a meaningful consequence, or it contributes to long-term goals. Use the user's goals only if they have stated them. Never ask the user for their goals.
- **Urgent**: waiting causes harm or lost options. A due date alone does not make a task urgent. A deadline next month for a one-hour task is not urgent; a window that closes tomorrow is.

Judge every task against its own consequences, never against the other tasks.
Never move a task to a lower quadrant to make room for another.

Routine upkeep (chores, exercise, errands, health) is at least Schedule unless the user says it doesn't matter.

| | Urgent | Not urgent |
| --- | --- | --- |
| **Important** | Do | Schedule |
| **Not important** | Delegate | Eliminate |

## State

The matrix lives only in this conversation. There is no file.
Each turn, rebuild the matrix from the chat history: start from the last printed matrix, then apply every change since.
Keep each task's wording short and stable so it can be matched across turns.

## Workflow

### 1. Triage

When the user gives one or more tasks:

1. Tag every task with an area of life, such as Work, Home or Health.
   Pick the areas from the tasks themselves, not from a fixed list.
   If a task's area is unclear, add one question about it to the interview batch. Do not ask in a separate round.
2. Guess a quadrant for every task from its text and any context the user gave.
3. Mark each guess as **clear** or **unclear**.
   A guess is clear only when both urgency and importance are obvious.
4. Place clear tasks straight away. Do not ask about them.

### 2. Interview the unclear tasks

For each unclear task, ask adaptive questions:

- Ask only about the axis that is unclear (urgency, importance, or both).
- Choose each next question based on the earlier answers.
- Stop as soon as the quadrant is clear. Usually one or two questions are enough.
- Batch questions for several tasks into one turn when you can.

Good questions target the definitions, for example:

- "What happens if this waits a week?" (urgency)
- "Does a chance or option disappear if you don't act soon?" (urgency)
- "What is the consequence if this never gets done?" (importance)
- "Does this move a goal you care about forward?" (importance, only if goals were mentioned)

### 3. Quadrant follow-up

After a task lands in a quadrant, ask one follow-up:

| Quadrant | Follow-up |
| --- | --- |
| Do | None |
| Schedule | Ask for a date |
| Delegate | Ask who to give it to |
| Eliminate | Ask the user to confirm dropping it |

Record the answer next to the task, e.g. `Write report (Fri 14 Nov)` or `Book venue → Sam`.
If the user declines to confirm an Eliminate task, re-interview it.
The user may skip a follow-up; then leave the task without a note.

### 4. Print the matrix

After every change, print the full matrix as a markdown 2x2 table:

```markdown
| | **Urgent** | **Not urgent** |
| --- | --- | --- |
| **Important** | **Do:** Fix prod outage · File taxes | **Schedule:** Write report (Fri 14 Nov) · Plan Q1 goals (1 Dec) |
| **Not important** | **Delegate:** Book venue → Sam | **Eliminate:** — |
```

- Keep each cell on one line. Separate tasks with ` · `.
- Never use HTML such as `<br>`. Many renderers, including terminals, show it as literal text.
- Write `—` after the quadrant name in an empty quadrant.
- Keep task names short. Shorten long names to a few words.
- If all tasks share one area, print one table with no heading.
- If tasks span several areas, print one table per area, each under a heading such as `### Work`.
- Below the last table, list completed tasks as `Done: task, task` when any exist.

## Asking questions

If the `AskUserQuestion` tool is available, use it for interview questions and follow-ups.
Give 2–4 concrete options per question, e.g. for "What happens if this waits a week?":
"Real harm or a missed chance", "Some inconvenience", "Nothing much".

If the tool is not available, ask in plain text with numbered options:

```
**Taxes** — what happens if this waits a week?
1. Real harm or a missed chance
2. Some inconvenience
3. Nothing much
```

The user may answer with a number or in their own words.

## Later turns

The user can keep working on the matrix in later messages:

- **Add tasks**: run triage (including the area) and the interview for the new tasks only.
- **Move a task to another area**: keep its quadrant, put it under the area the user names, and reprint.
- **Move a task**: put it in the quadrant the user names, run that quadrant's follow-up, and reprint.
- **Remove a task**: drop it from the matrix and reprint.
- **Complete a task**: move it to the `Done` line and reprint.
- **Re-interview a task** (the user says its situation changed): run the interview again for that task only, then place it and reprint.

Never re-ask about tasks that are already placed unless the user asks.
