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

### Codex

Codex reads the same `SKILL.md` format. Copy a skill folder into your Codex skills directory:

```sh
cp -r skills/eisenhower-matrix ~/.agents/skills/
```

Older Codex versions read `~/.codex/skills/` instead. To install a skill for one project only, copy it into `.agents/skills/` in that repo.

## Contributing

Changes go through pull requests, which are squash-merged into `main`. The PR title
becomes the commit message, so it and every commit in the PR must be a
[Conventional Commit](https://www.conventionalcommits.org/) (checked by the `commits`
workflow; `cz commit` writes one for you).

### Releases

Every push to `main` whose commits call for a new version is released automatically
(`.github/workflows/release.yml`). [commitizen](https://commitizen-tools.github.io/commitizen/)
(`.cz.toml`) reads the commits since the last release:

| Commits since the last release | Next version, while on 0.x |
| --- | --- |
| any with `!` (or a `BREAKING CHANGE:` footer) | minor: `v0.4.2` → `v0.5.0` |
| `feat` | minor: `v0.4.2` → `v0.5.0` |
| `fix`, `refactor`, `perf` | patch: `v0.4.2` → `v0.4.3` |
| only `docs`, `ci`, `test`, `chore`, `style`, `build` | no release |

A release is a `bump: version X → Y` commit by `github-actions[bot]` that adds the
version's entry to `CHANGELOG.md`, an annotated `vX.Y.Z` tag on it, and a GitHub release
with that entry as its notes and one zip per skill. The current version is the newest tag.

- `CHANGELOG.md` is written only by the release job; editing it in a PR conflicts with the next bump.
- Don't create, move or delete `v*` tags or releases by hand, and don't run `cz bump` yourself.
  To preview what merging would release, run `cz bump --get-next` on an up-to-date `main` with the PR's commits on top.

## License

MIT
