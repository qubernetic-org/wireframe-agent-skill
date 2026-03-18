<div align="center">

# Wireframe Mockup — Claude Code Skill

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-7c3aed.svg)](https://claude.ai/code)
[![React](https://img.shields.io/badge/React-TypeScript-61dafb.svg?logo=react&logoColor=white)](https://react.dev)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-v3-06b6d4.svg?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)

A Claude Code skill that generates black-and-white structural wireframe mockups in a consistent, technical design language — grayscale palette, dashed borders, monospace typography, and X-pattern placeholders.

[Installation](#installation) · [Usage](#usage) · [What It Produces](#what-it-produces) · [Design Language](#design-language) · [Contributing](CONTRIBUTING.md)

</div>

---

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
> Build a structural mockup for a dashboard with sidebar navigation
> Make a wireframe mockup for an e-commerce homepage
> Design a low-fidelity prototype for a blog layout
```

Or invoke directly:

```
/wireframe-mockup
```

## What It Produces

Every generated wireframe is a **self-contained React + Tailwind CSS page** ready to drop into any Vite project.

| Rule | Description |
|------|-------------|
| **Grayscale only** | Zero saturation — 10 CSS variables, all `0 0%` hue/saturation |
| **Dashed borders** | Every structural element uses `1px dashed` — never solid |
| **Monospace typography** | Roboto Mono at 8 size tiers, single font throughout |
| **X-pattern placeholders** | Gray boxes with diagonal X for images, `✕` squares for icons |
| **Bracket notation** | `[LOGO]`, `[CTA]`, `[image]` — no real content |
| **Diagonal watermark** | "STRUCTURAL MOCKUP — NOT FINAL DESIGN" at 8% opacity |
| **Square corners** | `border-radius: 0px` on all elements |
| **Responsive** | Mobile-first with `sm:` / `md:` / `lg:` breakpoints |

## Component Library

The skill includes **11 reusable component templates**:

```
Watermark        — Fixed diagonal overlay text
Navbar           — Sticky nav with mobile hamburger menu
Footer           — 4-column responsive footer
PlaceholderBox   — X-pattern image replacement (5 size presets)
ProductCard      — Icon + title + description
StatCard         — Large number + label
ServiceCard      — Image + text + CTA button
IconLabel        — Centered icon + text pair
FormField        — Label + dashed input box
Button           — 4 size variants, bracket text
Breadcrumb       — Hierarchical page navigation
```

## Design Language

The complete visual system is documented in [DESIGN-LANGUAGE.md](DESIGN-LANGUAGE.md) — 21 sections covering:

| Area | What's defined |
|------|----------------|
| **Color palette** | 10 grayscale CSS variables with HSL/Hex values |
| **Typography** | Font sizes, weights, transforms, line heights |
| **Dashed borders** | CSS class + 9 application points |
| **Placeholders** | PlaceholderBox CSS, React component, 5 sizing patterns |
| **Watermark** | Fixed overlay with responsive `clamp()` sizing |
| **Buttons** | Single style, 4 size variants |
| **Forms** | Input, textarea, layout, submit patterns |
| **Cards** | Product, stat, service, icon+label |
| **Layout** | Container, section structure, background alternation |
| **Grid** | 7 responsive configurations + asymmetric 60/40 split |
| **Spacing** | Section and element spacing tokens |
| **Breakpoints** | 4 tiers with responsive patterns |
| **Tailwind config** | Full `tailwind.config.ts` — copy-pasteable |
| **Base CSS** | Full `index.css` with custom properties — copy-pasteable |

## Files

| File | Description |
|------|-------------|
| `SKILL.md` | The Claude Code skill definition — **install this** |
| `DESIGN-LANGUAGE.md` | Exhaustive design language reference (21 sections) |
| `CHANGELOG.md` | Version history ([Keep a Changelog](https://keepachangelog.com/) format) |
| `CONTRIBUTING.md` | Contribution guidelines and design constraint checklist |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

[MIT](LICENSE) © [Qubernetic](https://github.com/qubernetic-org)
