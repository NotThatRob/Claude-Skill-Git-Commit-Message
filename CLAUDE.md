# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a **Claude Code custom skill** (`SKILL.md`) that generates git commit messages following the [Conventional Commits](https://www.conventionalcommits.org/) specification. It is not a traditional codebase — the entire deliverable is the `SKILL.md` prompt file.

## Architecture

- **`SKILL.md`** — The skill definition. The YAML frontmatter (`name`, `description`) registers the skill with Claude Code. The markdown body is the prompt that instructs Claude how to generate commit messages from diffs or plain-language descriptions.
- The skill is invoked via `/git-commit-message` in Claude Code.

## Key Conventions in SKILL.md

- Commit titles: Conventional Commits format `<type>(<scope>): <summary>`, max 72 chars, imperative mood, lowercase after colon, no trailing period.
- Commit types: `feat`, `fix`, `refactor`, `chore`, `docs`, `test`, `style`, `perf`, `ci`.
- Commit body: explains **what** and **why** (not how), 72-char line wrap, bullet points for multiple changes, `BREAKING CHANGE:` footer when applicable.

## Editing Guidelines

- When modifying `SKILL.md`, preserve the YAML frontmatter delimiters (`---`) and ensure the `name` and `description` fields remain valid.
- Changes to the prompt body affect how all commit messages are generated, so test with varied diffs (single-file fixes, multi-file features, breaking changes) to verify output quality.
- This is a public repo — keep `README.md` in sync with any changes to skill behavior or installation steps.
