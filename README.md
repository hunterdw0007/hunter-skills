# hunter-skills

A collection of [Claude Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview).

## Skills

| Skill | Description |
| --- | --- |
| [eisenhower-matrix](skills/eisenhower-matrix/SKILL.md) | Sorts tasks into an Eisenhower Matrix through a short adaptive interview. |

## Install

### Claude.ai (web) and Claude Desktop

1. Download the skill's `.zip` (e.g. [`eisenhower-matrix.zip`](https://github.com/hunterdw0007/hunter-skills/releases/latest/download/eisenhower-matrix.zip)) from the [latest release](https://github.com/hunterdw0007/hunter-skills/releases/latest). Don't use the release's "Source code (zip)": Claude rejects it because `SKILL.md` is nested too deep.
2. In Claude, open **Settings → Capabilities** and make sure **Code execution and file creation** is on.
3. Under **Skills**, click **Upload skill** and choose the `.zip`.

Skills sync to your account, so uploading once on the web also works in the desktop app. To update, upload the new release's zip.

### Claude Code (CLI)

Copy a skill folder into your skills directory, for example:

```sh
cp -r skills/eisenhower-matrix ~/.claude/skills/
```

### Codex

Codex reads the same `SKILL.md` format. Copy a skill folder into your Codex skills directory:

```sh
cp -r skills/eisenhower-matrix ~/.agents/skills/
```

Older Codex versions read `~/.codex/skills/` instead. To install a skill for one project only, copy it into `.agents/skills/` in that repo.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT
