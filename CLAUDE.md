# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code **skill** (SKILL.md) that generates black-and-white structural wireframe mockups using React + Tailwind CSS. The skill defines a strict design language: Roboto Mono monospace font, dashed borders, grayscale-only palette, X-pattern image placeholders, square corners, and a diagonal watermark ("STRUCTURAL MOCKUP — NOT FINAL DESIGN").

This is not a runnable application — it's a single `SKILL.md` file that instructs Claude Code how to generate wireframe pages on demand.

## Architecture

- **SKILL.md** — The entire skill definition. Contains frontmatter metadata (name, description, version) followed by the complete design system specification: CSS variables, Tailwind config, component templates, layout patterns, grid system, spacing tokens, and forbidden elements.
- Output targets **Vite + React + TypeScript + Tailwind CSS** projects. Generated wireframes are self-contained and can be dropped into any such project.

## Key Design Constraints

When modifying the skill, preserve these invariants:

- **Grayscale only** — zero saturation, all HSL values use `0 0%` hue/saturation
- **Dashed borders only** — never solid borders
- **No rounded corners** — `--radius: 0px`
- **Single font** — Roboto Mono monospace, no other fonts
- **No real images/icons** — only `PlaceholderBox` (X-pattern) and dashed-border squares with ✕
- **Bracket notation** for placeholder text: `[LOGO]`, `[CTA]`, `[☰]`

## Editing the Skill

The SKILL.md follows Claude Code skill format:
- YAML frontmatter (`name`, `description`, `version`, `metadata`)
- Markdown body with code blocks as component templates
- The `description` field in frontmatter controls when Claude Code triggers the skill — keep trigger keywords updated if scope changes
