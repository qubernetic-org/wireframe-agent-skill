# Contributing

Thank you for your interest in improving the wireframe mockup skill.

## How to Contribute

1. **Open an issue first** — describe what you want to change and why, before writing code.
2. **Fork the repo** and create a feature branch from `main`.
3. **Make your changes** following the guidelines below.
4. **Open a pull request** against `main`.

## Guidelines

### Design Constraints (non-negotiable)

Every change must preserve the six design invariants:

- **Grayscale only** — zero saturation, all HSL values use `0 0%`
- **Dashed borders only** — never solid borders
- **No rounded corners** — `--radius: 0px`
- **Single font** — Roboto Mono monospace, no other fonts
- **No real images/icons** — only PlaceholderBox (X-pattern) and dashed-border squares with X
- **Bracket notation** for placeholder text: `[LOGO]`, `[CTA]`, `[image]`

### File-Specific Rules

- **SKILL.md** must remain self-contained — it is the installable artifact. Keep it under 700 lines.
- **DESIGN-LANGUAGE.md** is the exhaustive reference. Any new component or pattern must be documented here first.
- **SKILL.md and DESIGN-LANGUAGE.md must stay in sync** — if you change a component in one, update the other.
- All content must be in **English**.

### Testing

Before submitting a PR, test your changes by:

1. Copying the updated `SKILL.md` to `~/.claude/skills/wireframe-mockup/SKILL.md`
2. Starting a new Claude Code session
3. Asking Claude to generate a wireframe and verifying the output follows all design constraints

## Reporting Bugs

If the skill generates output that violates the design language (e.g., uses colors, solid borders, rounded corners), please open an issue with:

- The prompt you used
- What went wrong (screenshot if possible)
- Which design rule was violated

## Code of Conduct

Be respectful. We follow the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).
