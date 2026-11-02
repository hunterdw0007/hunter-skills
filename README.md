# hunter-skills

A collection of [Claude Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview).

## Skills

| Skill | Description |
| --- | --- |
| [eisenhower-matrix](skills/eisenhower-matrix/SKILL.md) | Sorts tasks into an Eisenhower Matrix through a short adaptive interview. |

## Install

Copy a skill folder into your skills directory, for example:

```sh
cp -r skills/eisenhower-matrix ~/.claude/skills/
```

Or zip the folder and upload it in Claude.ai under Settings → Capabilities → Skills.

## Contributing

Commits follow [Conventional Commits](https://www.conventionalcommits.org/) via [commitizen](https://commitizen-tools.github.io/commitizen/):

```sh
cz commit   # write a commit
cz bump     # bump version, update CHANGELOG.md, tag
```

Design decisions live in `ADR-*.md` files.

## License

MIT
