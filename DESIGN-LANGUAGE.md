# SQ Trade — Wireframe Design Language Specification

> Referencia dokumentum fekete-fehér szerkezeti wireframe mockupok készítéséhez.
> Cél: bármilyen webes projektet ebben a vizuális nyelvben lehessen wireframe-elni, Lovable nélkül is.

---

## 1. Alapelvek

- **Kizárólag szürkeárnyalatos** — semmi szín, semmi brand elem
- **Szaggatott vonalú (dashed) keretek** mindenhol — ez a wireframe vizuális alapeleme
- **Monospace tipográfia** (Roboto Mono) — technikai, vázlatos hatás
- **Szögletes sarkok** — `border-radius: 0px` minden elemen
- **Placeholder-ek** képek, ikonok, logó helyett — X-mintás szürke dobozok, `[szöveges]` címkék
- **Átlós vízjel** — "SZERKEZETI MOCKUP — NEM VÉGLEGES DESIGN" az egész oldalon
- **Nincs hover effekt, árnyék, gradiens, animáció** (kivéve mobil menü slide)
- **Mobile-first** reszponzív megközelítés

---

## 2. Színpaletta

Minden szín HSL formátumban, CSS custom property-ként definiálva. **Kizárólag 0% szaturáció (szürkeárnyalat).**

### Elsődleges színek

| Változó | HSL | Hex | Használat |
|---------|-----|-----|-----------|
| `--background` | `0 0% 100%` | `#FFFFFF` | Oldal háttér, szekció háttér |
| `--foreground` | `0 0% 20%` | `#333333` | Elsődleges szöveg, címsorok |
| `--secondary` | `0 0% 96%` | `#F5F5F5` | Váltakozó szekció háttér |
| `--muted-foreground` | `0 0% 40%` | `#666666` | Másodlagos szöveg |
| `--border` | `0 0% 88%` | `#E0E0E0` | Alap keret szín |
| `--wire-border` | `0 0% 60%` | `#999999` | Szaggatott keretek |
| `--wire-placeholder` | `0 0% 88%` | `#E0E0E0` | Placeholder doboz háttér |
| `--wire-text-secondary` | `0 0% 40%` | `#666666` | Leírások, címkék |
| `--wire-footer-bg` | `0 0% 20%` | `#333333` | Footer háttér |
| `--wire-footer-fg` | `0 0% 88%` | `#E0E0E0` | Footer szöveg |

### Teljes CSS változó definíció

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

## 3. Tipográfia

### Betűtípus

- **Egyetlen font az egész oldalon:** `'Roboto Mono', monospace`
- Google Fonts import: `wght@400;500;700`
- Tailwind config: `fontFamily: { mono: ['"Roboto Mono"', 'monospace'] }`
- Body-ra alkalmazva: `font-mono` class

### Betűméretek

| Tailwind class | Méret | Használat |
|----------------|-------|-----------|
| `text-3xl` | 1.875rem (30px) | Hero főcím (desktop) |
| `text-2xl` | 1.5rem (24px) | Hero főcím (tablet) |
| `text-xl` | 1.25rem (20px) | Hero főcím (mobil) |
| `text-lg` | 1.125rem (18px) | Szekció címsorok (H2) |
| `text-sm` | 0.875rem (14px) | Szekció alcímek, stat értékek, navbar logo |
| `text-xs` | 0.75rem (12px) | Fő szövegtörzs, linkek, gombok, leírások |
| `text-[11px]` | 11px | Termék leírások (kártyákon belül) |
| `text-[10px]` | 10px | Form labelek, ikon labelek |

### Betűsúlyok

| Tailwind class | Súly | Használat |
|----------------|------|-----------|
| `font-bold` | 700 | Címsorok, logo, stat értékek, kártya címek |
| `font-semibold` | 600 | Badge szöveg |
| `font-medium` | 500 | Gombok, aktív linkek |
| (default) | 400 | Szövegtörzs, leírások |

### Szövegformázás

- **Címsorok:** `uppercase` + `font-bold`
- **Navigációs linkek:** `uppercase` + `tracking-wider`
- **Footer copyright:** `tracking-widest`
- **Sorok közötti távolság:** `leading-tight` (címsorok), `leading-relaxed` (szövegtörzs)

---

## 4. Szaggatott keret rendszer (Dashed Border)

Ez az egész wireframe design nyelv alapeleme. Egy egyedi CSS osztály:

```css
.dashed-border {
  border: 1px dashed hsl(var(--wire-border));
}
```

### Alkalmazási helyek

| Elem | Tailwind osztályok |
|------|-------------------|
| Navbar alsó él | `border-b border-dashed border-wire-border` |
| Szekció elválasztók | `border-b border-dashed border-wire-border pb-2` |
| Kártyák | `dashed-border p-4` |
| Gombok | `dashed-border px-4 py-2 text-xs` |
| Form inputok | `dashed-border w-full h-9` |
| Textarea | `dashed-border w-full h-24` |
| Ikon placeholder-ek | `dashed-border w-12 h-12 flex items-center justify-center` |
| Footer felső él | `border-t border-dashed border-wire-border` |
| Mobil menü bal él | `border-l border-dashed border-wire-border` |

---

## 5. Placeholder rendszer

### Kép placeholder (PlaceholderBox)

Szürke téglalap, átlós X-mintával és középre igazított szöveges címkével.

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

### PlaceholderBox React komponens

```tsx
interface PlaceholderBoxProps {
  label?: string;      // Alapértelmezett: "[kép]"
  className?: string;  // Tailwind méretezéshez
}

function PlaceholderBox({ label = "[kép]", className = "" }: PlaceholderBoxProps) {
  return (
    <div className={`placeholder-box ${className}`}>
      <span className="relative z-10 text-[10px] text-wire-secondary bg-wire-placeholder px-1">
        {label}
      </span>
    </div>
  );
}
```

### Méretezési minták

| Kontextus | Classes | Méret |
|-----------|---------|-------|
| Hero kép | `w-full h-64 md:h-80` | Teljes szélesség, 16rem/20rem magas |
| Térkép | `w-full h-48` | Teljes szélesség, 12rem magas |
| Szekció kép | `h-48 md:h-64` | 12rem/16rem magas |
| Kis kép | `h-20` – `h-40` | 5rem – 10rem magas |
| Ikon placeholder | `w-12 h-12` | 3rem × 3rem négyzet |

### Ikon placeholder (PlaceholderBox nélkül)

Kis szaggatott keretű doboz X szimbólummal:

```tsx
<div className="dashed-border w-12 h-12 flex items-center justify-center">
  <span className="text-[10px] text-wire-secondary">✕</span>
</div>
```

### Logó placeholder

```tsx
<span className="font-bold text-sm text-foreground">[LOGO]</span>
```

Mindig szögletes zárójelben, félkövér, sima szöveg — sosem grafika.

---

## 6. Vízjel (Watermark)

Fix pozíciójú, átlós szöveg az egész oldalon:

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

### Paraméterek

| Tulajdonság | Érték | Megjegyzés |
|-------------|-------|------------|
| Pozíció | `fixed`, középre igazítva | Mindig a viewport közepén |
| Forgatás | `-35deg` | Átlós, bal felülről jobb alulra |
| Betűméret | `clamp(1.5rem, 4vw, 3rem)` | Reszponzív, 24px–48px |
| Szín | `hsl(0 0% 20% / 0.08)` | Sötétszürke, 8% átlátszóság |
| Z-index | `9999` | Minden felett, de `pointer-events: none` |
| Szöveg | `SZERKEZETI MOCKUP — NEM VÉGLEGES DESIGN` | |

### React komponens

```tsx
function Watermark() {
  return (
    <div className="wireframe-watermark">
      SZERKEZETI MOCKUP — NEM VÉGLEGES DESIGN
    </div>
  );
}
```

---

## 7. Gomb stílusok

### Egyetlen gomb variáns

Nincs elsődleges/másodlagos megkülönböztetés. Minden gomb ugyanúgy néz ki:

```tsx
<button className="dashed-border px-4 py-2 text-xs text-foreground">
  [Gomb szöveg]
</button>
```

### Méret variációk

| Variáns | Classes | Használat |
|---------|---------|-----------|
| Normál | `dashed-border px-4 py-2 text-xs` | CTA, form submit |
| Kicsi | `dashed-border px-3 py-1.5 text-xs` | Navbar CTA |
| Kompakt | `dashed-border px-2 py-1 text-xs` | Szűrők, badge-ek |
| Ikon gomb | `dashed-border min-h-[44px] min-w-[44px] flex items-center justify-center` | Hamburger menü |

### Gomb szöveg konvenció

Szögletes zárójelben: `[Ajánlatot kérek]`, `[Küldés]`, `[☰]`, `[✕]`

---

## 8. Form elemek

### Input mező

```tsx
<div>
  <label className="text-[10px] uppercase text-wire-secondary block mb-1">
    Mező név
  </label>
  <div className="dashed-border w-full h-9" />
</div>
```

- Magasság: `h-9` (2.25rem / 36px)
- Szélesség: `w-full`
- Keret: `.dashed-border`
- Label: 10px, uppercase, szürke, block, `mb-1` spacing

### Textarea

```tsx
<div>
  <label className="text-[10px] uppercase text-wire-secondary block mb-1">
    Üzenet
  </label>
  <div className="dashed-border w-full h-24" />
</div>
```

- Magasság: `h-24` (6rem / 96px)

### Form elrendezés

```tsx
<div className="space-y-3">
  {/* Input mezők vertikálisan, 0.75rem gap */}
</div>
```

### Submit gomb

```tsx
<button className="dashed-border px-4 py-2 text-xs text-foreground">
  [Küldés]
</button>
```

---

## 9. Kártya komponensek

### Termék kártya

```tsx
<div className="dashed-border p-4">
  <div className="w-12 h-12 dashed-border flex items-center justify-center mb-3">
    <span className="text-[10px] text-wire-secondary">✕</span>
  </div>
  <p className="text-xs font-bold mb-1">Termék neve</p>
  <p className="text-[11px] text-wire-secondary">Rövid leírás</p>
</div>
```

### Stat kártya

```tsx
<div className="dashed-border p-4">
  <p className="text-sm font-bold">1998</p>
  <p className="text-xs text-wire-secondary">Alapítás éve</p>
</div>
```

### Szolgáltatás kártya (complex wireframe)

```tsx
<div className="dashed-border p-4">
  <PlaceholderBox className="h-24 mb-3" label="[kép]" />
  <p className="text-xs font-bold mb-1">Szolgáltatás neve</p>
  <p className="text-xs text-wire-secondary">Lorem ipsum dolor sit amet...</p>
  <button className="dashed-border px-3 py-1 text-xs mt-3">[Ajánlatot kérek]</button>
</div>
```

### Ikon + Label kártya (fenntarthatóság)

```tsx
<div className="flex flex-col items-center gap-2">
  <div className="w-12 h-12 dashed-border flex items-center justify-center">
    <span className="text-[10px] text-wire-secondary">✕</span>
  </div>
  <p className="text-xs text-foreground">Napenergia</p>
</div>
```

---

## 10. Layout rendszer

### Container

```tsx
<div className="container mx-auto px-4">
```

- Max-width: `1400px` (Tailwind config: `screens: { "2xl": "1400px" }`)
- Centering: `mx-auto`
- Padding: `2rem` (config) + `px-4` (1rem, override)

### Szekció struktúra

Minden szekció azonos mintát követ:

```tsx
<section id="szekció-név" className="py-16">
  {/* VAGY: className="bg-secondary py-16" váltakozó háttérhez */}
  <div className="container mx-auto px-4">
    <h2 className="text-lg font-bold uppercase mb-8">SZEKCIÓ CÍM</h2>
    {/* Tartalom */}
  </div>
</section>
```

### Szekció háttér váltakozás

- Fehér (`bg-background`): Hero, Termékek, Kapcsolat
- Világosszürke (`bg-secondary`): Rólunk, Fenntarthatóság
- Sötétszürke: csak Footer (`--wire-footer-bg`)

### Szekció címsor

```tsx
<h2 className="text-lg font-bold uppercase mb-8">CÍM</h2>
```

Alternatív stílus alávonással (complex wireframe):

```tsx
<h2 className="text-sm font-bold uppercase mb-6 border-b border-dashed border-wire-border pb-2">CÍM</h2>
```

---

## 11. Grid rendszer

### Tipikus grid konfigurációk

| Tartalom | Mobile | Tablet | Desktop | Gap |
|----------|--------|--------|---------|-----|
| Termék kártyák (8db) | `grid-cols-1` | `sm:grid-cols-2` | `lg:grid-cols-4` | `gap-4` |
| Stat kártyák (3db) | `grid-cols-1` | `sm:grid-cols-3` | — | `gap-4` |
| Fenntarthatóság (3db) | `grid-cols-1` | `sm:grid-cols-3` | — | `gap-6` |
| Hero (kép + szöveg) | `grid-cols-1` | — | `lg:grid-cols-5` (3+2) | `gap-8` |
| Kapcsolat (form + info) | `grid-cols-1` | — | `lg:grid-cols-2` | `gap-8` |
| Footer (4 oszlop) | `grid-cols-1` | `md:grid-cols-4` | — | `gap-8` |
| Megoldás kártyák (6db) | `grid-cols-1` | `sm:grid-cols-2` | `lg:grid-cols-3` | `gap-4` |

### Aszimmetrikus grid (60/40 felosztás)

```tsx
<div className="grid grid-cols-1 lg:grid-cols-5 gap-8">
  <div className="lg:col-span-3">{/* 60% - szöveg */}</div>
  <div className="lg:col-span-2">{/* 40% - kép/stat */}</div>
</div>
```

---

## 12. Reszponzív breakpointok

### Tailwind breakpointok

| Prefix | Min-width | Eszköz |
|--------|-----------|--------|
| (default) | 0px | Mobil |
| `sm:` | 640px | Kis tablet |
| `md:` | 768px | Tablet |
| `lg:` | 1024px | Desktop |

### Reszponzív minták

**Navigáció:**
- Mobil: hamburger gomb (`lg:hidden`), slide-in menü
- Desktop: inline linkek (`hidden lg:flex`)

**Grid-ek:**
- Mobil: 1 oszlop
- Tablet: 2–3 oszlop
- Desktop: 3–4 oszlop

**Szövegméretek:**
- Hero cím: `text-xl md:text-2xl lg:text-3xl`
- Kép magasság: `h-64 md:h-80`

---

## 13. Navbar

### Struktúra

```tsx
<nav className="sticky top-0 z-50 bg-background border-b border-dashed border-wire-border">
  <div className="container mx-auto flex items-center justify-between py-3 px-4">
    {/* Bal: Logo */}
    <span className="font-bold text-sm text-foreground">[LOGO]</span>

    {/* Közép: Desktop nav linkek */}
    <div className="hidden lg:flex items-center gap-6">
      <button className="text-xs uppercase tracking-wider text-wire-secondary">
        Link
      </button>
    </div>

    {/* Jobb: CTA + Mobil hamburger */}
    <button className="hidden lg:block text-xs dashed-border px-3 py-1.5">
      Ajánlatot kérek
    </button>
    <button className="lg:hidden dashed-border min-h-[44px] min-w-[44px] flex items-center justify-center">
      [☰]
    </button>
  </div>
</nav>
```

### Mobil menü

```tsx
<div className={`lg:hidden fixed top-[49px] right-0 h-[calc(100vh-49px)] w-72
  bg-background border-l border-dashed border-wire-border z-50
  transition-transform duration-100
  ${open ? "translate-x-0" : "translate-x-full"}`}>
  <div className="p-4 overflow-y-auto">
    {/* Linkek: text-xs uppercase tracking-wider */}
    {/* CTA gomb: dashed-border w-full mt-4 */}
  </div>
</div>

{/* Overlay a menü mögött */}
<div className="lg:hidden fixed inset-0 top-[49px] z-40" onClick={close} />
```

---

## 14. Footer

### Struktúra

```tsx
<footer className="border-t border-dashed border-wire-border mt-16">
  <div className="container mx-auto px-4 py-10 grid grid-cols-1 md:grid-cols-4 gap-8">

    {/* 1. oszlop: Logo + leírás */}
    <div>
      <p className="text-sm font-bold mb-2">[LOGO]</p>
      <p className="text-xs text-wire-secondary">Cég leírás placeholder...</p>
    </div>

    {/* 2. oszlop: Gyors linkek */}
    <div>
      <p className="text-xs font-bold uppercase mb-2">Gyors linkek</p>
      <a className="block text-xs text-wire-secondary py-0.5">Link</a>
    </div>

    {/* 3. oszlop: Termékek */}
    <div>
      <p className="text-xs font-bold uppercase mb-2">Termékeink</p>
      <p className="text-xs text-wire-secondary py-0.5">Termék név</p>
    </div>

    {/* 4. oszlop: Kapcsolat */}
    <div>
      <p className="text-xs font-bold uppercase mb-2">Kapcsolat</p>
      <p className="text-xs text-wire-secondary">Cím, telefon, email</p>
    </div>
  </div>

  {/* Alsó sáv */}
  <div className="border-t border-dashed border-wire-border py-4 text-center text-xs text-wire-secondary">
    © 2026 SQ Trade Kft. | Adatvédelem | Impresszum
  </div>
</footer>
```

---

## 15. Spacing rendszer

### Szekciók közötti térköz

| Kontextus | Tailwind | Méret |
|-----------|----------|-------|
| Szekció padding (vertikális) | `py-16` | 4rem (64px) |
| Szekció cím alatt | `mb-8` | 2rem (32px) |
| Footer feletti margin | `mt-16` | 4rem (64px) |
| Footer belső padding | `py-10` | 2.5rem (40px) |

### Elemek közötti térköz

| Kontextus | Tailwind | Méret |
|-----------|----------|-------|
| Kártya belső padding | `p-4` | 1rem (16px) |
| Ikon kártya alatti rés | `mb-3` | 0.75rem (12px) |
| Cím + leírás között | `mb-1` | 0.25rem (4px) |
| Form mezők között | `space-y-3` | 0.75rem (12px) |
| Grid gap (kártyák) | `gap-4` | 1rem (16px) |
| Grid gap (szekció blokkok) | `gap-8` | 2rem (32px) |
| Footer link sorközöke | `py-0.5` | 0.125rem (2px) |

---

## 16. Accessibility

### Minimum méret

- Érintési célpont: `min-h-[44px] min-w-[44px]` minden kattintható elemen
- Hamburger gomb: `min-h-[44px] min-w-[44px]`

### Focus állapot

```tsx
focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2
```

### Szemantikus HTML

- `<nav>` — navigáció
- `<section>` — tartalmi szekciók `id` attribútummal
- `<footer>` — lábléc
- `aria-label="breadcrumb"` — kenyérmorzsák

---

## 17. Teljes Tailwind konfiguráció

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

## 18. Teljes CSS alap (index.css)

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

## 19. Oldalstruktúra sablon

### Egyoldalas (onepager)

```tsx
<div className="min-h-screen font-mono">
  <Watermark />
  <Navbar />
  <HeroSection />        {/* #hero */}
  <AboutSection />       {/* #rolunk — bg-secondary */}
  <ProductsSection />    {/* #termekek */}
  <SustainabilitySection /> {/* #fenntarthatosag — bg-secondary */}
  <ContactSection />     {/* #kapcsolat */}
  <Footer />
</div>
```

### Többoldalas (complex)

```tsx
{/* Minden oldal: */}
<div className="min-h-screen font-mono">
  <Watermark />
  <Navbar />
  <div className="container mx-auto px-4 py-8">
    {/* Breadcrumb */}
    <div className="text-xs text-wire-secondary mb-6">
      Főoldal &gt; Szekció &gt; <span className="text-foreground">Aktuális oldal</span>
    </div>
    <h1 className="text-lg font-bold uppercase mb-6">OLDAL CÍM</h1>
    {/* Tartalom */}
  </div>
  <Footer />
</div>
```

---

## 20. Komponens katalógus — összefoglaló

| Komponens | Fő osztályok | Leírás |
|-----------|-------------|--------|
| `Watermark` | `.wireframe-watermark` | Fix átlós vízjel szöveg |
| `Navbar` | `sticky top-0 z-50 border-b border-dashed` | Ragadós navigáció |
| `Footer` | `border-t border-dashed mt-16` | 4 oszlopos lábléc |
| `PlaceholderBox` | `.placeholder-box` + méret class | X-mintás kép placeholder |
| `ProductCard` | `dashed-border p-4` + ikon + szöveg | Termék kártya |
| `StatCard` | `dashed-border p-4` + nagy szám + label | Statisztika kártya |
| `IconLabel` | `flex flex-col items-center gap-2` + ikon | Ikon + szöveg páros |
| `FormField` | label (`text-[10px]`) + `dashed-border h-9` | Form input |
| `Button` | `dashed-border px-4 py-2 text-xs` | Univerzális gomb |
| `SectionHeading` | `text-lg font-bold uppercase mb-8` | Szekció címsor |
| `Breadcrumb` | `text-xs text-wire-secondary mb-6` | Kenyérmorzsa navigáció |

---

## 21. NEM szabad (tiltólista)

- Színek (kék, zöld, piros, bármi ami nem szürkeárnyalat)
- Valódi képek, fotók, illusztrációk
- Valódi ikonok (Lucide, FontAwesome, stb.) — csak placeholder X
- Lekerekített sarkok (`border-radius > 0`)
- Árnyékok (`box-shadow`, `shadow-*`)
- Gradiensek (`bg-gradient-*`)
- Hover háttérszín-váltás
- Animációk (kivéve mobil menü slide)
- Különböző betűtípusok (csak Roboto Mono)
- Folyamatos vonalú (`solid`) keretek — csak `dashed`
