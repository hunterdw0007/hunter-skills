# hunter-skills

A collection of [Claude Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview).

## Skills

| Skill | Description |
| --- | --- |
| [eisenhower-matrix](skills/eisenhower-matrix/SKILL.md) | Sorts tasks into an Eisenhower Matrix through a short adaptive interview. |

## Install

### Claude.ai (web) and Claude Desktop

1. Download the skill's `.zip` (e.g. `eisenhower-matrix.zip`) from the [latest release](https://github.com/hunterdw0007/hunter-skills/releases/latest).
2. In Claude, open **Settings → Capabilities** and make sure **Code execution and file creation** is on.
3. Under **Skills**, click **Upload skill** and choose the `.zip`.

Skills sync to your account, so uploading once on the web also works in the desktop app. To update, upload the new release's zip.

### Claude Code (CLI)

Copy a skill folder into your skills directory, for example:

```sh
cp -r skills/eisenhower-matrix ~/.claude/skills/
```

## Contributing

Commits follow [Conventional Commits](https://www.conventionalcommits.org/) via [commitizen](https://commitizen-tools.github.io/commitizen/):

```sh
cz commit   # write a commit
cz bump     # bump version, update CHANGELOG.md, tag
git push --follow-tags   # the pushed tag triggers a GitHub Release with one zip per skill
```

Design decisions live in `ADR-*.md` files.

## License

MIT
