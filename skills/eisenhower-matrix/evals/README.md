# eisenhower-matrix evals

Test prompts for task categorization. Each case in `evals.json` has a prompt, the expected area and quadrant per task, and behavior checks.

## Run

- **Claude**: run with the `skill-creator` skill's eval workflow, pointing it at this skill.
- **Codex and other agents**: paste each `prompt` into a fresh session with the skill loaded and check the `expectations` by hand.

A case passes when every expectation holds. Questions count as a pass where an expectation allows them.

## Results

Record one row per model run. Case 1 is the acceptance test for #2.

| Date | Model | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
