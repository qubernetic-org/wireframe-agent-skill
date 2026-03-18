# Wireframe Mockup — Claude Code Skill

A Claude Code skill that generates black-and-white structural wireframe mockups using a consistent, technical design language: Roboto Mono monospace font, dashed borders, grayscale-only palette, X-pattern image placeholders, and a diagonal watermark.

## Installation

Copy the `SKILL.md` file to your global Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/wireframe-mockup
cp SKILL.md ~/.claude/skills/wireframe-mockup/SKILL.md
```

The skill will be automatically discovered on the next Claude Code session.

## Usage

The skill activates automatically when you mention wireframes or mockups:

```
> Create a wireframe for a SaaS landing page with hero, pricing, and FAQ sections
> Készíts egy wireframe mockupot egy webshop főoldalához
> Build a structural mockup for a dashboard with sidebar navigation
```

Or invoke directly with the slash command:

```
/wireframe-mockup
```

## What It Produces

- **React + Tailwind CSS** wireframe pages
- **Grayscale only** — no colors, no brand elements
- **Dashed borders** on all structural elements
- **Roboto Mono** monospace typography throughout
- **X-pattern placeholders** for images and icons
- **Diagonal watermark**: "SZERKEZETI MOCKUP — NEM VÉGLEGES DESIGN"
- **Responsive** — mobile-first with sm/md/lg breakpoints
- **Square corners** — zero border radius

## Files

| File | Description |
|------|-------------|
| `SKILL.md` | The Claude Code skill definition (install this) |
| `DESIGN-LANGUAGE.md` | Full design language specification with every CSS value, Tailwind class, and component pattern documented |

## Design Language Reference

See [DESIGN-LANGUAGE.md](DESIGN-LANGUAGE.md) for the complete specification including:

- Color palette (10 grayscale CSS variables)
- Typography system (Roboto Mono, 8 size tiers)
- Dashed border system
- PlaceholderBox component (X-pattern image replacement)
- Watermark implementation
- 11 reusable components (Navbar, Footer, Cards, Forms, etc.)
- Grid system (7 configurations)
- Spacing system
- Responsive breakpoints
- Full Tailwind config and CSS — copy-pasteable

## Origin

Extracted from two wireframe reference projects:

- [sq-trade-complex-wireframe](https://github.com/qubernetic-org/sq-trade-complex-wireframe) — multi-page wireframe
- [sq-trade-simple-wireframe](https://github.com/qubernetic-org/sq-trade-simple-wireframe) — single-page wireframe

## License

MIT
