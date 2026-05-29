# Git Commit Skill

Current version: `0.1.0`

Use this skill to create repository-compliant git commits from staged changes.

This file is intended for LLM tools and other automation. For human-readable explanations and examples, see `git/committing-code-guide.md`.

## Usage
```
/commit
```

## Behavior
1. Analyze staged changes with `git diff --staged`
2. Stop if nothing is staged or the staged changes mix unrelated work
3. Generate a Conventional Commit subject in imperative mood
4. Add a body only when the reason, tradeoff, migration, or behavior change is not obvious
5. Put issue and pull request references in footers such as `Refs: #123` or `Closes: #456`
6. Mark breaking changes with `!` in the header or a `BREAKING CHANGE:` footer
7. Prefer a specific type over `chore` whenever one applies
8. Create the commit with proper formatting

## Commit Format
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Keep blank lines between the subject, body, and footers.

## Types
- feat: New feature
- fix: Bug fix
- docs: Documentation changes
- test: Tests and test data
- refactor: Code refactoring
- perf: Performance improvements
- style: Formatting-only changes
- build: Build system, dependency, or packaging changes
- ci: Continuous integration configuration
- chore: Routine maintenance that fits no better type
- revert: Reverting a previous commit

Prefer a specific type over `chore` whenever one applies.

## Repository Rules
- Keep each commit focused on one logical change.
- Do not stage unrelated edits.
- Use SSH signing when verified signatures are required.
- Prefer a follow-up commit over rewriting shared history.

## Footer Examples
```
Refs: #123
Closes: #456
Fixes: #789
Resolves: #101
```

## Example Output
```
feat(auth): add password reset functionality

- Add forgot password form
- Implement email verification flow
- Add password reset endpoint
```

## Changelog

| Version | Date       | Notes            |
|---------|------------|------------------|
| 0.1.0   | 2026-05-29 | Initial version. |
