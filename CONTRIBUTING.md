# Contributing

Changes go through pull requests, which are squash-merged into `main`. The PR title
becomes the commit message, so it and every commit in the PR must be a
[Conventional Commit](https://www.conventionalcommits.org/) (checked by the `commits`
workflow; `cz commit` writes one for you).

## Releases

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
