---
name: git-commit-message
description: Generate a conventional git commit title and description on demand. Use when the user wants to commit changes and needs a well-formatted commit message. Analyzes staged changes, diffs, or a plain-language description of what changed to produce a title and body following Conventional Commits spec.
---

The user wants a git commit message. They will either provide:
- The output of `git diff --staged` or `git diff`
- A plain-language description of what they changed
- Both

Your job is to produce a **commit title** and **commit description** that are clear, concise, and follow the Conventional Commits spec.

## How to Get the Diff

If the user hasn't provided a diff, instruct them to run:

```bash
git diff --staged
```

Or if nothing is staged yet:

```bash
git diff
```

Then paste the output back to you.

## Commit Title Rules

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <short summary>
```

**Types:**
- `feat` – new feature
- `fix` – bug fix
- `refactor` – code change that neither fixes a bug nor adds a feature
- `chore` – maintenance, dependencies, tooling
- `docs` – documentation only
- `test` – adding or updating tests
- `style` – formatting, whitespace (no logic change)
- `perf` – performance improvement
- `ci` – CI/CD changes

**Title rules:**
- Max **72 characters**
- Lowercase after the colon
- No period at the end
- Imperative mood ("add support for X", not "added support for X")
- Be specific — avoid vague titles like `fix: update stuff`

## Commit Description Rules

- Wrap lines at **72 characters**
- Blank line between title and body
- Explain **what** changed and **why**, not how
- Use bullet points if there are multiple distinct changes
- Note any breaking changes with `BREAKING CHANGE:` at the end if applicable
- Keep it skimmable — someone reviewing the git log should understand the change in 10 seconds

## Output Format

Always output exactly this structure, ready to copy-paste:

```
<type>(<scope>): <summary>

<body describing what changed and why>
```

If there are multiple logical changes bundled together, note that and suggest whether the user should consider splitting into multiple commits.

## Example Output

```
feat(auth): add JWT refresh token rotation

Implements automatic refresh token rotation on each use to reduce
the window of exposure if a token is compromised.

- Refresh tokens are now single-use and immediately invalidated
- New token is returned in the response alongside the access token
- Old behavior preserved behind LEGACY_AUTH feature flag for rollout
```

## Tone

Be direct. Don't pad the description. If the change is small, the description can be one sentence. Match the verbosity to the complexity of the change.
