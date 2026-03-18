---
name: wireframe-mockup
description: "Generate black-and-white structural wireframe mockups using a specific dashed-border, monospace, grayscale design system. Use when the user asks to create a wireframe, mockup, wireframe page, structural mockup, low-fidelity prototype, wireframe layout, or mentions 'wireframe', 'mockup', 'wireframe mockup', 'structural mockup'. Produces self-contained React + Tailwind CSS wireframe pages with placeholder images, dashed borders, and a diagonal watermark."
version: 1.0.1
license: MIT
metadata:
  author: Qubernetic
  version: "1.0.1"
---

# Wireframe Mockup Generator

Generate black-and-white structural wireframe mockups in a consistent, technical design language. Every wireframe uses the same visual system: Roboto Mono monospace font, dashed borders, grayscale-only palette, X-pattern image placeholders, square corners, and a diagonal "STRUCTURAL MOCKUP — NOT FINAL DESIGN" watermark.

## When This Skill Applies

- User asks to create a wireframe, mockup, or low-fidelity prototype
- User mentions "wireframe", "mockup", "wireframe mockup", "structural mockup"
- User wants a structural layout preview of a website or web application
- User asks for a black-and-white page layout

## Tech Stack

- **React** (functional components, TypeScript)
- **Tailwind CSS** (utility-first, custom CSS variables)
- **Single font:** Roboto Mono (monospace)
- **No external icon libraries** — only placeholder X symbols
- **No external images** — only PlaceholderBox components

---

## Design Language Rules (CRITICAL)

### Rule 1: Grayscale Only

NO colors. Zero saturation. Only these values:

| Token | HSL | Hex | Use |
|-------|-----|-----|-----|
| `--background` | `0 0% 100%` | `#FFFFFF` | Page background |
| `--foreground` | `0 0% 20%` | `#333333` | Primary text, headings |
| `--secondary` | `0 0% 96%` | `#F5F5F5` | Alternating section background |
| `--muted-foreground` | `0 0% 40%` | `#666666` | Secondary text |
| `--border` | `0 0% 88%` | `#E0E0E0` | Default border |
| `--wire-border` | `0 0% 60%` | `#999999` | Dashed borders |
| `--wire-placeholder` | `0 0% 88%` | `#E0E0E0` | Placeholder box background |
| `--wire-text-secondary` | `0 0% 40%` | `#666666` | Descriptions, labels |
| `--wire-footer-bg` | `0 0% 20%` | `#333333` | Footer background |
| `--wire-footer-fg` | `0 0% 88%` | `#E0E0E0` | Footer text |

### Rule 2: Dashed Borders Everywhere

The core visual element. Never use solid borders.

```css
.dashed-border {
  border: 1px dashed hsl(var(--wire-border));
}
```

Applied to: cards, buttons, form inputs, icon placeholders, nav/footer dividers.

For structural dividers use Tailwind: `border-b border-dashed border-wire-border`

### Rule 3: No Rounded Corners

`--radius: 0px` — all elements are square-cornered.

### Rule 4: Monospace Typography Only

Single font: `'Roboto Mono', monospace` applied via `font-mono` on the root element.

| Class | Size | Use |
|-------|------|-----|
| `text-3xl` | 30px | Hero heading (desktop) |
| `text-2xl` | 24px | Hero heading (tablet) |
| `text-xl` | 20px | Hero heading (mobile) |
| `text-lg` | 18px | Section headings (H2) |
| `text-sm` | 14px | Stat values, navbar logo |
| `text-xs` | 12px | Body text, links, buttons, descriptions |
| `text-[11px]` | 11px | Card descriptions |
| `text-[10px]` | 10px | Form labels, icon labels |

**Weights:** `font-bold` (700) for headings/logo, `font-medium` (500) for buttons, default (400) for body.

**Transforms:** All headings and nav links use `uppercase`. Nav links add `tracking-wider`.

### Rule 5: No Real Images or Icons

Every image is a PlaceholderBox. Every icon is a dashed-border square with an X.

### Rule 6: Bracket Notation for Placeholder Text

Logo: `[LOGO]`, buttons: `[Request Quote]`, `[Send]`, hamburger: `[☰]`, close: `[✕]`

---

## Core CSS (index.css)

Always include this exact CSS foundation:

```css
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400;500;700&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
    font-family: 'Roboto Mono', monospace;
  }
}

@layer components {
  .dashed-border {
    border: 1px dashed hsl(var(--wire-border));
  }

  .placeholder-box {
    background-color: hsl(var(--wire-placeholder));
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .placeholder-box::before,
  .placeholder-box::after {
    content: '';
    position: absolute;
    background-color: hsl(var(--wire-border));
  }

  .placeholder-box::before {
    width: 141.4%;
    height: 1px;
    transform: rotate(45deg);
  }

  .placeholder-box::after {
    width: 141.4%;
    height: 1px;
    transform: rotate(-45deg);
  }

  .wireframe-watermark {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(-35deg);
    font-size: clamp(1.5rem, 4vw, 3rem);
    font-family: 'Roboto Mono', monospace;
    color: hsl(0 0% 20% / 0.08);
    white-space: nowrap;
    pointer-events: none;
    z-index: 9999;
    letter-spacing: 0.1em;
    font-weight: 700;
  }
}
```

### CSS Variables (in :root)

```css
:root {
  --background: 0 0% 100%;
  --foreground: 0 0% 20%;
  --card: 0 0% 100%;
  --card-foreground: 0 0% 20%;
  --popover: 0 0% 100%;
  --popover-foreground: 0 0% 20%;
  --primary: 0 0% 20%;
  --primary-foreground: 0 0% 100%;
  --secondary: 0 0% 96%;
  --secondary-foreground: 0 0% 20%;
  --muted: 0 0% 96%;
  --muted-foreground: 0 0% 40%;
  --accent: 0 0% 96%;
  --accent-foreground: 0 0% 20%;
  --destructive: 0 0% 40%;
  --destructive-foreground: 0 0% 100%;
  --border: 0 0% 88%;
  --input: 0 0% 88%;
  --ring: 0 0% 20%;
  --radius: 0px;
  --wire-border: 0 0% 60%;
  --wire-placeholder: 0 0% 88%;
  --wire-text-secondary: 0 0% 40%;
  --wire-footer-bg: 0 0% 20%;
  --wire-footer-fg: 0 0% 88%;
}
```

---

## Core Components

### Watermark

Always include as the first child of the root element:

```tsx
function Watermark() {
  return (
    <div className="wireframe-watermark">
      STRUCTURAL MOCKUP — NOT FINAL DESIGN
    </div>
  );
}
```

### PlaceholderBox (Image Placeholder)

Gray rectangle with diagonal X pattern and centered label:

```tsx
function PlaceholderBox({ label = "[image]", className = "" }: { label?: string; className?: string }) {
  return (
    <div className={`placeholder-box ${className}`}>
      <span className="relative z-10 text-[10px] text-wire-secondary bg-wire-placeholder px-1">
        {label}
      </span>
    </div>
  );
}
```

**Common sizes:**

| Context | Classes |
|---------|---------|
| Hero image | `w-full h-64 md:h-80` |
| Map embed | `w-full h-48` |
| Section image | `h-48 md:h-64` |
| Small image | `h-20` to `h-40` |
| Icon | `w-12 h-12` |

### Icon Placeholder (without PlaceholderBox)

Small dashed-border square with X symbol:

```tsx
<div className="dashed-border w-12 h-12 flex items-center justify-center">
  <span className="text-[10px] text-wire-secondary">✕</span>
</div>
```

### Logo Placeholder

```tsx
<span className="font-bold text-sm text-foreground">[LOGO]</span>
```

---

## Layout Components

### Navbar (Sticky)

```tsx
<nav className="sticky top-0 z-50 bg-background border-b border-dashed border-wire-border">
  <div className="container mx-auto flex items-center justify-between py-3 px-4">
    {/* Left: Logo */}
    <span className="font-bold text-sm text-foreground">[LOGO]</span>

    {/* Center: Desktop nav links */}
    <div className="hidden lg:flex items-center gap-6">
      <button className="text-xs uppercase tracking-wider text-wire-secondary">Link</button>
    </div>

    {/* Right: CTA + Mobile hamburger */}
    <button className="hidden lg:block text-xs dashed-border px-3 py-1.5">CTA Text</button>
    <button className="lg:hidden dashed-border min-h-[44px] min-w-[44px] flex items-center justify-center">[☰]</button>
  </div>
</nav>
```

**Mobile menu:** slide-in panel from right, `w-72`, `transition-transform duration-100`, `translate-x-full` (closed) / `translate-x-0` (open).

### Footer (4-Column)

```tsx
<footer className="border-t border-dashed border-wire-border mt-16">
  <div className="container mx-auto px-4 py-10 grid grid-cols-1 md:grid-cols-4 gap-8">
    <div>
      <p className="text-sm font-bold mb-2">[LOGO]</p>
      <p className="text-xs text-wire-secondary">Company description placeholder...</p>
    </div>
    <div>
      <p className="text-xs font-bold uppercase mb-2">Quick Links</p>
      <a className="block text-xs text-wire-secondary py-0.5">Link</a>
    </div>
    <div>
      <p className="text-xs font-bold uppercase mb-2">Products</p>
      <p className="text-xs text-wire-secondary py-0.5">Product name</p>
    </div>
    <div>
      <p className="text-xs font-bold uppercase mb-2">Contact</p>
      <p className="text-xs text-wire-secondary">Address, phone, email</p>
    </div>
  </div>
  <div className="border-t border-dashed border-wire-border py-4 text-center text-xs text-wire-secondary">
    © 2026 Company Name | Privacy | Legal
  </div>
</footer>
```

### Section Structure

Every content section follows this pattern:

```tsx
<section id="section-id" className="py-16">
  {/* Use className="bg-secondary py-16" for alternating gray background */}
  <div className="container mx-auto px-4">
    <h2 className="text-lg font-bold uppercase mb-8">SECTION TITLE</h2>
    {/* Content */}
  </div>
</section>
```

**Background alternation:** White (default) and light gray (`bg-secondary`) alternate between sections.

### Section Heading (Alternative with underline)

```tsx
<h2 className="text-sm font-bold uppercase mb-6 border-b border-dashed border-wire-border pb-2">TITLE</h2>
```

---

## Card Components

### Product Card

```tsx
<div className="dashed-border p-4">
  <div className="w-12 h-12 dashed-border flex items-center justify-center mb-3">
    <span className="text-[10px] text-wire-secondary">✕</span>
  </div>
  <p className="text-xs font-bold mb-1">Product Name</p>
  <p className="text-[11px] text-wire-secondary">Short description</p>
</div>
```

### Stat Card

```tsx
<div className="dashed-border p-4">
  <p className="text-sm font-bold">1998</p>
  <p className="text-xs text-wire-secondary">Foundation Year</p>
</div>
```

### Service Card

```tsx
<div className="dashed-border p-4">
  <PlaceholderBox className="h-24 mb-3" label="[image]" />
  <p className="text-xs font-bold mb-1">Service Name</p>
  <p className="text-xs text-wire-secondary">Lorem ipsum dolor sit amet...</p>
  <button className="dashed-border px-3 py-1 text-xs mt-3">[CTA]</button>
</div>
```

### Icon + Label Card

```tsx
<div className="flex flex-col items-center gap-2">
  <div className="w-12 h-12 dashed-border flex items-center justify-center">
    <span className="text-[10px] text-wire-secondary">✕</span>
  </div>
  <p className="text-xs text-foreground">Label Text</p>
</div>
```

---

## Form Components

### Text Input

```tsx
<div>
  <label className="text-[10px] uppercase text-wire-secondary block mb-1">Field Name</label>
  <div className="dashed-border w-full h-9" />
</div>
```

### Textarea

```tsx
<div>
  <label className="text-[10px] uppercase text-wire-secondary block mb-1">Message</label>
  <div className="dashed-border w-full h-24" />
</div>
```

### Form Layout

```tsx
<div className="space-y-3">
  {/* Stack form fields vertically with 0.75rem gap */}
</div>
```

### Submit Button

```tsx
<button className="dashed-border px-4 py-2 text-xs text-foreground">[Submit]</button>
```

---

## Button Variants

All buttons use the same visual style — only padding varies:

| Variant | Classes | Use |
|---------|---------|-----|
| Normal | `dashed-border px-4 py-2 text-xs` | CTA, form submit |
| Small | `dashed-border px-3 py-1.5 text-xs` | Navbar CTA |
| Compact | `dashed-border px-2 py-1 text-xs` | Filters, badges |
| Icon | `dashed-border min-h-[44px] min-w-[44px] flex items-center justify-center` | Hamburger menu |

Button text always uses bracket notation: `[Button Text]`

---

## Grid System

### Common Grid Configurations

| Content | Mobile | Tablet | Desktop | Gap |
|---------|--------|--------|---------|-----|
| Products (8) | `grid-cols-1` | `sm:grid-cols-2` | `lg:grid-cols-4` | `gap-4` |
| Stats (3) | `grid-cols-1` | `sm:grid-cols-3` | — | `gap-4` |
| Icons (3) | `grid-cols-1` | `sm:grid-cols-3` | — | `gap-6` |
| Hero (text+image) | `grid-cols-1` | — | `lg:grid-cols-5` (3+2) | `gap-8` |
| Contact (info+form) | `grid-cols-1` | — | `lg:grid-cols-2` | `gap-8` |
| Footer (4 cols) | `grid-cols-1` | `md:grid-cols-4` | — | `gap-8` |
| Solutions (6) | `grid-cols-1` | `sm:grid-cols-2` | `lg:grid-cols-3` | `gap-4` |

### Asymmetric Grid (60/40 Split)

```tsx
<div className="grid grid-cols-1 lg:grid-cols-5 gap-8">
  <div className="lg:col-span-3">{/* 60% — text content */}</div>
  <div className="lg:col-span-2">{/* 40% — image/stats */}</div>
</div>
```

---

## Spacing System

### Section Spacing

| Context | Tailwind | Size |
|---------|----------|------|
| Section vertical padding | `py-16` | 4rem (64px) |
| Section heading margin-bottom | `mb-8` | 2rem (32px) |
| Footer top margin | `mt-16` | 4rem (64px) |
| Footer inner padding | `py-10` | 2.5rem (40px) |

### Element Spacing

| Context | Tailwind | Size |
|---------|----------|------|
| Card padding | `p-4` | 1rem (16px) |
| Icon below margin | `mb-3` | 0.75rem (12px) |
| Title to description | `mb-1` | 0.25rem (4px) |
| Form field gap | `space-y-3` | 0.75rem (12px) |
| Card grid gap | `gap-4` | 1rem (16px) |
| Section block gap | `gap-8` | 2rem (32px) |
| Footer link spacing | `py-0.5` | 0.125rem (2px) |

---

## Responsive Breakpoints

| Prefix | Min-width | Device |
|--------|-----------|--------|
| (default) | 0px | Mobile |
| `sm:` | 640px | Small tablet |
| `md:` | 768px | Tablet |
| `lg:` | 1024px | Desktop |

**Navigation:** Mobile shows hamburger (`lg:hidden`), desktop shows inline links (`hidden lg:flex`).

**Grids:** Mobile 1 column, tablet 2-3 columns, desktop 3-4 columns.

**Hero heading:** `text-xl md:text-2xl lg:text-3xl`

---

## Tailwind Configuration

```typescript
// tailwind.config.ts
import type { Config } from "tailwindcss";

export default {
  darkMode: ["class"],
  content: ["./pages/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}", "./app/**/*.{ts,tsx}", "./src/**/*.{ts,tsx}"],
  prefix: "",
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: { "2xl": "1400px" },
    },
    extend: {
      fontFamily: {
        mono: ['"Roboto Mono"', "monospace"],
      },
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: { DEFAULT: "hsl(var(--primary))", foreground: "hsl(var(--primary-foreground))" },
        secondary: { DEFAULT: "hsl(var(--secondary))", foreground: "hsl(var(--secondary-foreground))" },
        destructive: { DEFAULT: "hsl(var(--destructive))", foreground: "hsl(var(--destructive-foreground))" },
        muted: { DEFAULT: "hsl(var(--muted))", foreground: "hsl(var(--muted-foreground))" },
        accent: { DEFAULT: "hsl(var(--accent))", foreground: "hsl(var(--accent-foreground))" },
        card: { DEFAULT: "hsl(var(--card))", foreground: "hsl(var(--card-foreground))" },
        wire: {
          border: "hsl(var(--wire-border))",
          placeholder: "hsl(var(--wire-placeholder))",
          secondary: "hsl(var(--wire-text-secondary))",
          "footer-bg": "hsl(var(--wire-footer-bg))",
          "footer-fg": "hsl(var(--wire-footer-fg))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
} satisfies Config;
```

---

## Page Templates

### Single Page (Onepager)

```tsx
<div className="min-h-screen font-mono">
  <Watermark />
  <Navbar />
  <HeroSection />              {/* #hero */}
  <AboutSection />             {/* #about — bg-secondary */}
  <ProductsSection />          {/* #products */}
  <SustainabilitySection />    {/* #sustainability — bg-secondary */}
  <ContactSection />           {/* #contact */}
  <Footer />
</div>
```

### Multi-Page (with Breadcrumbs)

```tsx
<div className="min-h-screen font-mono">
  <Watermark />
  <Navbar />
  <div className="container mx-auto px-4 py-8">
    <div className="text-xs text-wire-secondary mb-6">
      Home &gt; Section &gt; <span className="text-foreground">Current Page</span>
    </div>
    <h1 className="text-lg font-bold uppercase mb-6">PAGE TITLE</h1>
    {/* Content */}
  </div>
  <Footer />
</div>
```

---

## Accessibility

- Touch targets: `min-h-[44px] min-w-[44px]` on all clickable elements
- Focus: `focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2`
- Semantic HTML: `<nav>`, `<section id="">`, `<footer>`, `aria-label`

---

## Forbidden (NEVER Use)

- Any color with saturation > 0% (no blue, green, red, etc.)
- Real images, photos, illustrations
- Real icons (Lucide, FontAwesome, etc.) — only placeholder X
- Rounded corners (`border-radius > 0`)
- Shadows (`box-shadow`, `shadow-*`)
- Gradients (`bg-gradient-*`)
- Hover background color changes
- Animations (except mobile menu slide)
- Multiple font families (only Roboto Mono)
- Solid borders — only `dashed`

---

## Workflow

When asked to create a wireframe:

1. **Understand the structure** — Ask for or infer the page sections, content blocks, and hierarchy
2. **Set up the foundation** — Create `index.css` with the full CSS variables and component classes, and `tailwind.config.ts`
3. **Build core components** — `Watermark`, `PlaceholderBox`, `Navbar`, `Footer`
4. **Build section components** — One component per section, following the section structure pattern
5. **Assemble the page** — Compose components in the page template
6. **Verify compliance** — Check against the Forbidden list. No colors, no real images, no rounded corners, no solid borders.

Output should be complete, self-contained React + Tailwind CSS files that can be dropped into a Vite project and run immediately.
