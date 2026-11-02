# ADR-0001: Eisenhower Matrix Skill Design

- **Status:** Accepted
- **Date:** 2026-11-02
- **Deciders:** Hunter

## Context

Hunter wants an AI skill that sorts tasks into an Eisenhower Matrix.
The user gives the skill one or more tasks.
The skill asks questions to find the right quadrant.
The skill then prints the matrix.
The user can add more tasks in later messages.

This ADR records the design decisions made before the repository exists.

## Decisions

### 1. Target platform

The skill targets Claude Skills.
It uses a `SKILL.md` file.

**Alternatives considered:**
- A Claude Code plugin.
- An agent-agnostic markdown prompt.
- A standalone bash tool that calls an LLM API.

### 2. Matrix state

The matrix state lives in the conversation only.
Claude rebuilds the matrix from the chat history each turn.
A local file is a planned later feature.

**Alternatives considered:**
- A local JSON or markdown file.
- A JSON file with a rendered markdown view.
- Sync with an external tracker such as Jira or GitLab.

### 3. Interview logic

The skill asks adaptive questions.
Claude chooses each follow-up question from the earlier answers.
Claude stops when the quadrant is clear.

**Alternatives considered:**
- A fixed script of three or four questions.
- Two fixed questions plus adaptive follow-ups.
- Inference from the task text, with questions only when unsure.

### 4. Handling several tasks at once

Claude first guesses a quadrant for every task.
Claude then asks questions only about the unclear tasks.

**Alternatives considered:**
- Interview one task at a time.
- Ask the same question about every task in one turn.
- Let the user choose the mode.

### 5. Matrix output

The skill prints a markdown 2x2 table.

**Alternatives considered:**
- An ASCII box in a code block.
- Four lists, one per quadrant.
- A configurable format.

### 6. Matrix edits

Version 1 supports these edits:
- Move a task to another quadrant.
- Remove a task or mark it complete.
- Re-interview a task when its circumstances change.

**Alternative considered:**
- Add-only, with no edits.

### 7. Definition of important

The skill uses a generic definition.
Important means a meaningful consequence or a contribution to long-term goals.
Goals are optional.
Claude uses goals only when the user provides them.

**Alternatives considered:**
- Ask for goals once at the start of the session.
- Ask which goal each task serves.

### 8. Definition of urgent

Urgent means that waiting causes harm or lost options.
The due date alone does not decide urgency.

**Alternatives considered:**
- A fixed time window, such as 48 hours.
- Compare the deadline against the estimated effort.
- A window defined by the user.

### 9. Follow-up per quadrant

Claude asks one follow-up question for each quadrant:

| Quadrant | Follow-up |
| --- | --- |
| Do | None |
| Schedule | Ask for a date |
| Delegate | Ask for a person |
| Eliminate | Ask for confirmation |

**Alternatives considered:**
- Print the quadrant only.
- Suggest actions without asking.
- Ask follow-up questions only on request.

### 10. Question interface

The skill uses `AskUserQuestion` popups when the tool exists.
The skill falls back to numbered plain-text options when the tool is missing.

**Alternatives considered:**
- Popups only.
- Plain text only.
- One batched text form.

### 11. Triggering

The skill triggers on the phrase "Eisenhower matrix".
It also triggers on prioritization requests, such as "help me prioritize these tasks".

**Alternatives considered:**
- Trigger on explicit mention only.
- Trigger on any task list.
- Trigger on a slash command only.

### 12. Repository

- The repository holds several skills.
- The first skill lives in `skills/eisenhower-matrix/`.
- The repository is public on GitHub.
- The license is MIT.

**Alternatives considered:**
- A single skill folder at the repository root.
- A plugin marketplace layout.
- A private repository on GitHub or GitLab.

### 13. Testing

Testing is manual in version 1.
The team adds tests after the skill works.

**Alternatives considered:**
- Test prompts in the repository from the start.
- Skill-creator benchmark runs.
- A CI check of the `SKILL.md` frontmatter only.

## Consequences

**Positive:**
- The skill needs no setup and no storage.
- The adaptive interview keeps the question count low.
- The triage step avoids questions about clear tasks.
- The repository can hold more skills later.

**Negative:**
- The matrix disappears when the conversation ends.
- Adaptive questions make results less predictable than a fixed script.
- Broad triggers may fire on unrelated prioritization requests.
- Long task names may break the table layout.
- Manual testing cannot catch behavior changes between model versions.

## Open Items

- Add a local file to store the matrix between sessions.
- Add test prompts with expected quadrants.
- Decide how the table handles long task names.

## Proposed Repository Layout

```
skills-repo/
├── LICENSE
├── README.md
└── skills/
    └── eisenhower-matrix/
        └── SKILL.md
```
