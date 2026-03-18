# Wireframe Design Language Specification

> Reference document for creating black-and-white structural wireframe mockups.
> Goal: wireframe any web project in this visual language, without Lovable or any other tool.

---

## 1. Core Principles

- **Grayscale only** — no colors, no brand elements
- **Dashed borders** everywhere — the core visual element of the wireframe
- **Monospace typography** (Roboto Mono) — technical, sketch-like feel
- **Square corners** — `border-radius: 0px` on all elements
- **Placeholders** for images, icons, logos — X-pattern gray boxes, `[text]` labels
- **Diagonal watermark** — "STRUCTURAL MOCKUP — NOT FINAL DESIGN" across the entire page
- **No hover effects, shadows, gradients, or animations** (except mobile menu slide)
- **Mobile-first** responsive approach

---

## 2. Color Palette

All colors in HSL format, defined as CSS custom properties. **Strictly 0% saturation (grayscale).**

### Primary Colors

| Variable | HSL | Hex | Usage |
|----------|-----|-----|-------|
| `--background` | `0 0% 100%` | `#FFFFFF` | Page background, section background |
| `--foreground` | `0 0% 20%` | `#333333` | Primary text, headings |
| `--secondary` | `0 0% 96%` | `#F5F5F5` | Alternating section background |
| `--muted-foreground` | `0 0% 40%` | `#666666` | Secondary text |
| `--border` | `0 0% 88%` | `#E0E0E0` | Default border color |
| `--wire-border` | `0 0% 60%` | `#999999` | Dashed borders |
| `--wire-placeholder` | `0 0% 88%` | `#E0E0E0` | Placeholder box background |
| `--wire-text-secondary` | `0 0% 40%` | `#666666` | Descriptions, labels |
| `--wire-footer-bg` | `0 0% 20%` | `#333333` | Footer background |
| `--wire-footer-fg` | `0 0% 88%` | `#E0E0E0` | Footer text |

### Full CSS Variable Definition

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

## 3. Typography

### Font

- **Single font for the entire page:** `'Roboto Mono', monospace`
- Google Fonts import: `wght@400;500;700`
- Tailwind config: `fontFamily: { mono: ['"Roboto Mono"', 'monospace'] }`
- Applied to body: `font-mono` class

### Font Sizes

| Tailwind class | Size | Usage |
|----------------|------|-------|
| `text-3xl` | 1.875rem (30px) | Hero heading (desktop) |
| `text-2xl` | 1.5rem (24px) | Hero heading (tablet) |
| `text-xl` | 1.25rem (20px) | Hero heading (mobile) |
| `text-lg` | 1.125rem (18px) | Section headings (H2) |
| `text-sm` | 0.875rem (14px) | Section subheadings, stat values, navbar logo |
| `text-xs` | 0.75rem (12px) | Body text, links, buttons, descriptions |
| `text-[11px]` | 11px | Product descriptions (within cards) |
| `text-[10px]` | 10px | Form labels, icon labels |

### Font Weights

| Tailwind class | Weight | Usage |
|----------------|--------|-------|
| `font-bold` | 700 | Headings, logo, stat values, card titles |
| `font-semibold` | 600 | Badge text |
| `font-medium` | 500 | Buttons, active links |
| (default) | 400 | Body text, descriptions |

### Text Formatting

- **Headings:** `uppercase` + `font-bold`
- **Nav links:** `uppercase` + `tracking-wider`
- **Footer copyright:** `tracking-widest`
- **Line height:** `leading-tight` (headings), `leading-relaxed` (body text)

---

## 4. Dashed Border System

This is the foundational visual element of the entire wireframe design language. A custom CSS class:

```css
.dashed-border {
  border: 1px dashed hsl(var(--wire-border));
}
```

### Application Points

| Element | Tailwind classes |
|---------|-----------------|
| Navbar bottom edge | `border-b border-dashed border-wire-border` |
| Section dividers | `border-b border-dashed border-wire-border pb-2` |
| Cards | `dashed-border p-4` |
| Buttons | `dashed-border px-4 py-2 text-xs` |
| Form inputs | `dashed-border w-full h-9` |
| Textarea | `dashed-border w-full h-24` |
| Icon placeholders | `dashed-border w-12 h-12 flex items-center justify-center` |
| Footer top edge | `border-t border-dashed border-wire-border` |
| Mobile menu left edge | `border-l border-dashed border-wire-border` |

---

## 5. Placeholder System

### Image Placeholder (PlaceholderBox)

Gray rectangle with diagonal X-pattern and centered text label.

```css
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
```

### PlaceholderBox React Component

```tsx
interface PlaceholderBoxProps {
  label?: string;      // Default: "[image]"
  className?: string;  // For Tailwind sizing
}

function PlaceholderBox({ label = "[image]", className = "" }: PlaceholderBoxProps) {
  return (
    <div className={`placeholder-box ${className}`}>
      <span className="relative z-10 text-[10px] text-wire-secondary bg-wire-placeholder px-1">
        {label}
      </span>
    </div>
  );
}
```

### Sizing Patterns

| Context | Classes | Size |
|---------|---------|------|
| Hero image | `w-full h-64 md:h-80` | Full width, 16rem/20rem tall |
| Map | `w-full h-48` | Full width, 12rem tall |
| Section image | `h-48 md:h-64` | 12rem/16rem tall |
| Small image | `h-20` – `h-40` | 5rem – 10rem tall |
| Icon placeholder | `w-12 h-12` | 3rem × 3rem square |

### Icon Placeholder (without PlaceholderBox)

Small dashed-border box with X symbol:

```tsx
<div className="dashed-border w-12 h-12 flex items-center justify-center">
  <span className="text-[10px] text-wire-secondary">✕</span>
</div>
```

### Logo Placeholder

```tsx
<span className="font-bold text-sm text-foreground">[LOGO]</span>
```

Always in square brackets, bold, plain text — never a graphic.

---

## 6. Watermark

Fixed-position diagonal text across the entire page:

```css
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
```

### Parameters

| Property | Value | Note |
|----------|-------|------|
| Position | `fixed`, centered | Always at viewport center |
| Rotation | `-35deg` | Diagonal, top-left to bottom-right |
| Font size | `clamp(1.5rem, 4vw, 3rem)` | Responsive, 24px–48px |
| Color | `hsl(0 0% 20% / 0.08)` | Dark gray, 8% opacity |
| Z-index | `9999` | Above everything, but `pointer-events: none` |
| Text | `STRUCTURAL MOCKUP — NOT FINAL DESIGN` | |

### React Component

```tsx
function Watermark() {
  return (
    <div className="wireframe-watermark">
      STRUCTURAL MOCKUP — NOT FINAL DESIGN
    </div>
  );
}
```

---

## 7. Button Styles

### Single Button Variant

No primary/secondary distinction. All buttons look the same:

```tsx
<button className="dashed-border px-4 py-2 text-xs text-foreground">
  [Button Text]
</button>
```

### Size Variations

| Variant | Classes | Usage |
|---------|---------|-------|
| Normal | `dashed-border px-4 py-2 text-xs` | CTA, form submit |
| Small | `dashed-border px-3 py-1.5 text-xs` | Navbar CTA |
| Compact | `dashed-border px-2 py-1 text-xs` | Filters, badges |
| Icon button | `dashed-border min-h-[44px] min-w-[44px] flex items-center justify-center` | Hamburger menu |

### Button Text Convention

In square brackets: `[Request Quote]`, `[Send]`, `[☰]`, `[✕]`

---

## 8. Form Elements

### Input Field

```tsx
<div>
  <label className="text-[10px] uppercase text-wire-secondary block mb-1">
    Field Name
  </label>
  <div className="dashed-border w-full h-9" />
</div>
```

- Height: `h-9` (2.25rem / 36px)
- Width: `w-full`
- Border: `.dashed-border`
- Label: 10px, uppercase, gray, block, `mb-1` spacing

### Textarea

```tsx
<div>
  <label className="text-[10px] uppercase text-wire-secondary block mb-1">
    Message
  </label>
  <div className="dashed-border w-full h-24" />
</div>
```

- Height: `h-24` (6rem / 96px)

### Form Layout

```tsx
<div className="space-y-3">
  {/* Input fields stacked vertically, 0.75rem gap */}
</div>
```

### Submit Button

```tsx
<button className="dashed-border px-4 py-2 text-xs text-foreground">
  [Send]
</button>
```

---

## 9. Card Components

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

### Service Card (complex wireframe)

```tsx
<div className="dashed-border p-4">
  <PlaceholderBox className="h-24 mb-3" label="[image]" />
  <p className="text-xs font-bold mb-1">Service Name</p>
  <p className="text-xs text-wire-secondary">Lorem ipsum dolor sit amet...</p>
  <button className="dashed-border px-3 py-1 text-xs mt-3">[Request Quote]</button>
</div>
```

### Icon + Label Card (sustainability)

```tsx
<div className="flex flex-col items-center gap-2">
  <div className="w-12 h-12 dashed-border flex items-center justify-center">
    <span className="text-[10px] text-wire-secondary">✕</span>
  </div>
  <p className="text-xs text-foreground">Solar Energy</p>
</div>
```

---

## 10. Layout System

### Container

```tsx
<div className="container mx-auto px-4">
```

- Max-width: `1400px` (Tailwind config: `screens: { "2xl": "1400px" }`)
- Centering: `mx-auto`
- Padding: `2rem` (config) + `px-4` (1rem, override)

### Section Structure

Every section follows the same pattern:

```tsx
<section id="section-name" className="py-16">
  {/* OR: className="bg-secondary py-16" for alternating background */}
  <div className="container mx-auto px-4">
    <h2 className="text-lg font-bold uppercase mb-8">SECTION TITLE</h2>
    {/* Content */}
  </div>
</section>
```

### Section Background Alternation

- White (`bg-background`): Hero, Products, Contact
- Light gray (`bg-secondary`): About, Sustainability
- Dark gray: Footer only (`--wire-footer-bg`)

### Section Heading

```tsx
<h2 className="text-lg font-bold uppercase mb-8">TITLE</h2>
```

Alternative style with underline (complex wireframe):

```tsx
<h2 className="text-sm font-bold uppercase mb-6 border-b border-dashed border-wire-border pb-2">TITLE</h2>
```

---

## 11. Grid System

### Typical Grid Configurations

| Content | Mobile | Tablet | Desktop | Gap |
|---------|--------|--------|---------|-----|
| Product cards (8) | `grid-cols-1` | `sm:grid-cols-2` | `lg:grid-cols-4` | `gap-4` |
| Stat cards (3) | `grid-cols-1` | `sm:grid-cols-3` | — | `gap-4` |
| Sustainability (3) | `grid-cols-1` | `sm:grid-cols-3` | — | `gap-6` |
| Hero (image + text) | `grid-cols-1` | — | `lg:grid-cols-5` (3+2) | `gap-8` |
| Contact (form + info) | `grid-cols-1` | — | `lg:grid-cols-2` | `gap-8` |
| Footer (4 columns) | `grid-cols-1` | `md:grid-cols-4` | — | `gap-8` |
| Solution cards (6) | `grid-cols-1` | `sm:grid-cols-2` | `lg:grid-cols-3` | `gap-4` |

### Asymmetric Grid (60/40 Split)

```tsx
<div className="grid grid-cols-1 lg:grid-cols-5 gap-8">
  <div className="lg:col-span-3">{/* 60% — text */}</div>
  <div className="lg:col-span-2">{/* 40% — image/stats */}</div>
</div>
```

---

## 12. Responsive Breakpoints

### Tailwind Breakpoints

| Prefix | Min-width | Device |
|--------|-----------|--------|
| (default) | 0px | Mobile |
| `sm:` | 640px | Small tablet |
| `md:` | 768px | Tablet |
| `lg:` | 1024px | Desktop |

### Responsive Patterns

**Navigation:**
- Mobile: hamburger button (`lg:hidden`), slide-in menu
- Desktop: inline links (`hidden lg:flex`)

**Grids:**
- Mobile: 1 column
- Tablet: 2–3 columns
- Desktop: 3–4 columns

**Font sizes:**
- Hero heading: `text-xl md:text-2xl lg:text-3xl`
- Image height: `h-64 md:h-80`

---

## 13. Navbar

### Structure

```tsx
<nav className="sticky top-0 z-50 bg-background border-b border-dashed border-wire-border">
  <div className="container mx-auto flex items-center justify-between py-3 px-4">
    {/* Left: Logo */}
    <span className="font-bold text-sm text-foreground">[LOGO]</span>

    {/* Center: Desktop nav links */}
    <div className="hidden lg:flex items-center gap-6">
      <button className="text-xs uppercase tracking-wider text-wire-secondary">
        Link
      </button>
    </div>

    {/* Right: CTA + Mobile hamburger */}
    <button className="hidden lg:block text-xs dashed-border px-3 py-1.5">
      Request Quote
    </button>
    <button className="lg:hidden dashed-border min-h-[44px] min-w-[44px] flex items-center justify-center">
      [☰]
    </button>
  </div>
</nav>
```

### Mobile Menu

```tsx
<div className={`lg:hidden fixed top-[49px] right-0 h-[calc(100vh-49px)] w-72
  bg-background border-l border-dashed border-wire-border z-50
  transition-transform duration-100
  ${open ? "translate-x-0" : "translate-x-full"}`}>
  <div className="p-4 overflow-y-auto">
    {/* Links: text-xs uppercase tracking-wider */}
    {/* CTA button: dashed-border w-full mt-4 */}
  </div>
</div>

{/* Overlay behind the menu */}
<div className="lg:hidden fixed inset-0 top-[49px] z-40" onClick={close} />
```

---

## 14. Footer

### Structure

```tsx
<footer className="border-t border-dashed border-wire-border mt-16">
  <div className="container mx-auto px-4 py-10 grid grid-cols-1 md:grid-cols-4 gap-8">

    {/* Column 1: Logo + description */}
    <div>
      <p className="text-sm font-bold mb-2">[LOGO]</p>
      <p className="text-xs text-wire-secondary">Company description placeholder...</p>
    </div>

    {/* Column 2: Quick links */}
    <div>
      <p className="text-xs font-bold uppercase mb-2">Quick Links</p>
      <a className="block text-xs text-wire-secondary py-0.5">Link</a>
    </div>

    {/* Column 3: Products */}
    <div>
      <p className="text-xs font-bold uppercase mb-2">Our Products</p>
      <p className="text-xs text-wire-secondary py-0.5">Product name</p>
    </div>

    {/* Column 4: Contact */}
    <div>
      <p className="text-xs font-bold uppercase mb-2">Contact</p>
      <p className="text-xs text-wire-secondary">Address, phone, email</p>
    </div>
  </div>

  {/* Bottom bar */}
  <div className="border-t border-dashed border-wire-border py-4 text-center text-xs text-wire-secondary">
    © 2026 Company Name | Privacy | Legal
  </div>
</footer>
```

---

## 15. Spacing System

### Section Spacing

| Context | Tailwind | Size |
|---------|----------|------|
| Section padding (vertical) | `py-16` | 4rem (64px) |
| Below section heading | `mb-8` | 2rem (32px) |
| Footer top margin | `mt-16` | 4rem (64px) |
| Footer inner padding | `py-10` | 2.5rem (40px) |

### Element Spacing

| Context | Tailwind | Size |
|---------|----------|------|
| Card inner padding | `p-4` | 1rem (16px) |
| Below icon in card | `mb-3` | 0.75rem (12px) |
| Between title and description | `mb-1` | 0.25rem (4px) |
| Between form fields | `space-y-3` | 0.75rem (12px) |
| Grid gap (cards) | `gap-4` | 1rem (16px) |
| Grid gap (section blocks) | `gap-8` | 2rem (32px) |
| Footer link line spacing | `py-0.5` | 0.125rem (2px) |

---

## 16. Accessibility

### Minimum Size

- Touch target: `min-h-[44px] min-w-[44px]` on all clickable elements
- Hamburger button: `min-h-[44px] min-w-[44px]`

### Focus State

```tsx
focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2
```

### Semantic HTML

- `<nav>` — navigation
- `<section>` — content sections with `id` attribute
- `<footer>` — footer
- `aria-label="breadcrumb"` — breadcrumbs

---

## 17. Full Tailwind Configuration

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
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      fontFamily: {
        mono: ['"Roboto Mono"', 'monospace'],
      },
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
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

## 18. Full Base CSS (index.css)

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

---

## 19. Page Structure Templates

### Single Page (onepager)

```tsx
<div className="min-h-screen font-mono">
  <Watermark />
  <Navbar />
  <HeroSection />        {/* #hero */}
  <AboutSection />       {/* #about — bg-secondary */}
  <ProductsSection />    {/* #products */}
  <SustainabilitySection /> {/* #sustainability — bg-secondary */}
  <ContactSection />     {/* #contact */}
  <Footer />
</div>
```

### Multi-Page (complex)

```tsx
{/* Every page: */}
<div className="min-h-screen font-mono">
  <Watermark />
  <Navbar />
  <div className="container mx-auto px-4 py-8">
    {/* Breadcrumb */}
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

## 20. Component Catalog — Summary

| Component | Main classes | Description |
|-----------|-------------|-------------|
| `Watermark` | `.wireframe-watermark` | Fixed diagonal watermark text |
| `Navbar` | `sticky top-0 z-50 border-b border-dashed` | Sticky navigation |
| `Footer` | `border-t border-dashed mt-16` | 4-column footer |
| `PlaceholderBox` | `.placeholder-box` + size class | X-pattern image placeholder |
| `ProductCard` | `dashed-border p-4` + icon + text | Product card |
| `StatCard` | `dashed-border p-4` + large number + label | Statistic card |
| `IconLabel` | `flex flex-col items-center gap-2` + icon | Icon + text pair |
| `FormField` | label (`text-[10px]`) + `dashed-border h-9` | Form input |
| `Button` | `dashed-border px-4 py-2 text-xs` | Universal button |
| `SectionHeading` | `text-lg font-bold uppercase mb-8` | Section heading |
| `Breadcrumb` | `text-xs text-wire-secondary mb-6` | Breadcrumb navigation |

---

## 21. Forbidden (NEVER Use)

- Colors (blue, green, red, anything that is not grayscale)
- Real images, photos, illustrations
- Real icons (Lucide, FontAwesome, etc.) — only placeholder X
- Rounded corners (`border-radius > 0`)
- Shadows (`box-shadow`, `shadow-*`)
- Gradients (`bg-gradient-*`)
- Hover background color changes
- Animations (except mobile menu slide)
- Multiple font families (only Roboto Mono)
- Solid borders — only `dashed`
