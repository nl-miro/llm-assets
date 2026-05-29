# Committing Code

Current version: `0.1.0`

## Status

Accepted.

## Purpose

This guide is written for engineers and other technical personnel committing changes in this repository. It explains the repository's commit conventions in plain language so commits stay readable, reviewable, and consistent.

For LLM and tool-oriented commit instructions, use `git/committing-code-skill.md`.

## Quick Checklist

- Use Conventional Commits.
- Keep each commit focused on one logical change.
- Stage only the files you intend to include.
- Add a body when the reason or tradeoff is not obvious from the subject.
- Put issue and pull request references in footers.
- Use SSH signing when verified signatures are required.

## Commit Message Format

Use Conventional Commits for every commit:

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

The subject line must be concise and written in the imperative mood. Prefer describing the change as an action:

```text
docs: add committing code guide
fix(parser): handle empty input
feat(api): expose asset lookup endpoint
```

### Types

Use these commit types:

| Type       | Use for                                            |
|------------|----------------------------------------------------|
| `feat`     | New user-facing or developer-facing behavior       |
| `fix`      | Bug fixes                                          |
| `docs`     | Documentation-only changes                         |
| `test`     | Tests and test data                                |
| `refactor` | Code changes that preserve behavior                |
| `perf`     | Performance improvements                           |
| `style`    | Formatting-only changes that do not affect meaning |
| `build`    | Build system, dependency, or packaging changes     |
| `ci`       | Continuous integration configuration               |
| `chore`    | Routine maintenance that does not fit another type |
| `revert`   | Reverting a previous commit                        |

Avoid `chore` when another type applies — it is easily overused as a catch-all.

Use an optional scope when it helps locate the change:

```text
docs(git): clarify commit body guidance
fix(importer): skip malformed asset rows
```

### Breaking Changes

Mark breaking changes with either `!` after the type or scope, or a `BREAKING CHANGE:` footer:

```text
feat(api)!: require explicit asset namespace
```

Use a footer when the breaking change needs explanation, or when you prefer not to mark it in the header:

```text
feat(api): require explicit asset namespace

BREAKING CHANGE: Asset IDs must now include a namespace prefix.
```

## Commit Body

Use a commit body when the subject line cannot explain the change clearly. The body should explain why the change was made, important tradeoffs, and anything reviewers or future maintainers need to understand.

Add a body for changes that:

- Touch multiple areas of the repository.
- Change behavior in a way that is not obvious from the diff.
- Introduce a migration, compatibility concern, or follow-up task.

Put issue and pull request references in footers instead of free-form body text so they remain easy to scan and automate. On GitHub and GitLab, `Closes`, `Fixes`, and `Resolves` footers auto-close the referenced issue when the commit lands on the default branch:

```text
Refs: #123
Closes: #456
Fixes: #789
Resolves: #101
```

Keep the subject and body separated by a blank line:

```text
fix(importer): ignore blank asset rows

Blank rows can be produced by spreadsheet exports. Treating them as
invalid records caused otherwise valid imports to fail.
```

## Workflow

Before committing:

1. Review the current state with `git status`.
2. Inspect the diff with `git diff`.
3. Run the relevant tests or checks for the change.
4. Stage only the intended files with `git add <path>`.
5. Confirm staged content with `git diff --cached`.
6. Commit with a Conventional Commit message.

Use `git commit` without `-m` when the commit needs a body. Use `git commit -m "<subject>"` only for small, obvious changes.

## Staging Rules

Keep commits focused. A commit should represent one logical change, even if that change touches several files.

Do not include unrelated edits in the same commit. If the working tree contains unrelated changes, stage paths deliberately instead of using `git add .`.

## Amending Commits

Before pushing, use `git commit --amend` to fix a typo, improve the message, or add a missed file to the latest commit.

After pushing, avoid rewriting shared history unless the branch is yours and collaborators will not be disrupted. Prefer a follow-up commit when others may already have based work on the pushed commit. If you must amend a pushed commit, use `git push --force-with-lease` instead of `--force` to avoid accidentally overwriting others' work.

## Signed Commits

Sign commits with `git commit -S` when the repository requires verified signatures. This repository standardizes on SSH signing:

```text
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
```

To verify SSH signatures locally, configure an allowed signers file:

```text
git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```

To sign all commits by default in this repository, enable commit signing after SSH signing is configured:

```text
git config --local commit.gpgsign true
```

## Examples

Good commit subjects:

```text
docs: add committing code guide
docs(git): document commit workflow
fix: preserve changelog table alignment
refactor(assets): split metadata normalization
test(importer): cover duplicate asset names
```

Avoid vague subjects:

```text
update docs
fix stuff
changes
wip
```

## References

- [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)
- [Git commit documentation](https://git-scm.com/docs/git-commit)
- [GitLab commit guidance](https://docs.gitlab.com/topics/git/commit/)
- [How to Write a Git Commit Message (Chris Beams)](https://chris.beams.io/posts/git-commit/)

## Ideas

- `Use GPG instead of just SSH?`
- `Require DCO sign-offs?`

## Changelog

| Version | Date       | Notes            |
|---------|------------|------------------|
| 0.1.0   | 2026-05-29 | Initial version. |
