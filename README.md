# Git Commit Message — Claude Code Skill

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) custom skill that generates clear, consistent commit messages following the [Conventional Commits](https://www.conventionalcommits.org/) specification.

Type `/git-commit-message` in Claude Code, provide a diff or describe your changes, and get a ready-to-use commit message.

## Example

Given a diff, the skill produces output like:

```
feat(auth): add JWT refresh token rotation

Implements automatic refresh token rotation on each use to reduce
the window of exposure if a token is compromised.

- Refresh tokens are now single-use and immediately invalidated
- New token is returned in the response alongside the access token
- Old behavior preserved behind LEGACY_AUTH feature flag for rollout
```

## Installation

Claude Code discovers skills from a `skills/` directory containing a named subfolder with a `SKILL.md` file. You can install at two scopes:

### Personal (available in all your projects)

```bash
# Clone the repo
git clone https://github.com/robsheppard/Claude-Skill-Git-Commit-Message.git

# Copy into your personal skills directory
mkdir -p ~/.claude/skills/git-commit-message
cp Claude-Skill-Git-Commit-Message/SKILL.md ~/.claude/skills/git-commit-message/SKILL.md
```

### Project-level (available only in a specific project)

From your project root:

```bash
mkdir -p .claude/skills/git-commit-message
cp /path/to/SKILL.md .claude/skills/git-commit-message/SKILL.md
```

You can commit the `.claude/skills/` directory to share the skill with your team.

Start a new Claude Code session to pick up the skill.

## Usage

Once installed, invoke the skill in any Claude Code session:

```
/git-commit-message
```

You can provide input in three ways:

- **Paste a diff** — run `git diff --staged` (or `git diff`) and paste the output
- **Describe your changes** — explain what you changed in plain language
- **Both** — provide a diff and additional context

The skill will return a formatted commit message you can copy-paste directly into your commit.

## What It Does

- Generates a title in `<type>(<scope>): <summary>` format
- Picks the appropriate type: `feat`, `fix`, `refactor`, `chore`, `docs`, `test`, `style`, `perf`, `ci`
- Keeps titles under 72 characters, imperative mood, lowercase after the colon
- Writes a body explaining **what** changed and **why**
- Uses bullet points for multi-part changes
- Flags breaking changes with a `BREAKING CHANGE:` footer
- Suggests splitting when multiple unrelated changes are bundled together

## Customization

To tailor the skill to your project's conventions, fork this repo and edit `SKILL.md`. The file has two parts:

- **YAML frontmatter** (between `---` delimiters) — the `name` field sets the slash command and `description` controls when Claude auto-suggests the skill
- **Markdown body** — the prompt that defines commit message rules, format, and tone

For example, you could add your team's custom commit types, enforce a specific scope list, or change the line-wrap width.

## License

[MIT](LICENSE)
