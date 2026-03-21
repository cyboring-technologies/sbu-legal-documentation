
---
id: "BRANDING_LANDING"
title: "Landing Page Visual Identity and UX Standards"
type: "UX, Branding & Visual Design"
version: "v1.0.1"
last_updated: "2026-02-19"
status: "Approved"
---

# Landing Page Visual Identity and UX Standards

**Context:** *Specifies the visual identity and UI standards for the landing page. It details the "Institutional Greyscale" color palette, typography (Inter/IBM Plex Sans), and component specifications.*


This document outlines the visual identity, design tokens, and UI components used in the Documentos.legal marketing website. The system is built using **Tailwind CSS** with comprehensive dark mode support and internationalization (i18n).

---

## 1. Project Identity

### Brand Name
**Documentos.legal** - Infraestructura Legal Automatizada

### Tagline
"Infraestructura legal confiable, mínima y eficiente. Automatización de documentos sin fricción visual ni cognitiva."

### Domain
- **Production:** `https://documentos.legal`
- **Locales:** English (`/en`) and Spanish (`/es`)

### Business Context
This is the corporate landing site for Documentos.legal, a legal automation SaaS platform. The site serves as the marketing hub showcasing legal document automation services across Central America.

---

## 2. Typography

The typography system uses Google Fonts with optimized loading via `next/font` to prevent Cumulative Layout Shift (CLS).

| Role | Font Family | Variable | Weights | Usage |
| :--- | :--- | :--- | :--- | :--- |
| **Primary Sans** | **Inter** | `var(--font-inter)` | Variable (100-900) | Body text, UI elements, general content, navigation. |
| **Logo / Headings** | **IBM Plex Sans** | `var(--font-plex)` | 400, 600, 700 | Brand logo, major section headers, emphasized headings. |

### Implementation
```typescript
// src/app/(landing)/layout.tsx
const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});

const plexSans = IBM_Plex_Sans({
  subsets: ['latin'],
  weight: ['400', '600', '700'],
  display: 'swap',
  variable: '--font-plex',
});
```

### Tailwind Configuration
- `font-sans`: Uses `var(--font-inter)` for body text
- `font-logo`: Uses `var(--font-plex)` for headings and branding

---

## 3. Color System

The color system is based on an **Institutional Greyscale** foundation with a distinct **Blue-Grey Accent**. It supports both Light and Dark modes natively via CSS variables and HSL color values.

### Theme Philosophy
- **Light Mode:** High contrast, clean white backgrounds (`#FFFFFF`), dark grey text (`#0F0F0F`).
- **Dark Mode:** Deep "Soft Black" backgrounds (`#0F0F0F`), stark white text (`#FFFFFF`), slightly lighter card backgrounds for depth.

### Color Palette

| Token | Light Mode (HSL) | Hex | Dark Mode (HSL) | Hex | Usage |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Background** | `0 0% 100%` | `#FFFFFF` | `0 0% 6%` | `#0F0F0F` | Main page background. |
| **Foreground** | `0 0% 6%` | `#0F0F0F` | `0 0% 100%` | `#FFFFFF` | Primary text color. |
| **Primary** | `204 32% 27%` | `#2F4A5C` | `204 32% 27%` | `#2F4A5C` | Brand accent, primary CTAs (Institutional Blue-Grey). |
| **Primary-Fg** | `0 0% 100%` | `#FFFFFF` | `0 0% 100%` | `#FFFFFF` | Text on primary elements. |
| **Secondary** | `0 0% 96%` | `#F4F4F4` | `0 0% 11%` | `#1C1C1C` | Secondary backgrounds, subtle contrasts. |
| **Secondary-Fg** | `0 0% 23%` | `#3A3A3A` | `0 0% 100%` | `#FFFFFF` | Text on secondary elements. |
| **Card** | `0 0% 93%` | `#ECECEC` | `0 0% 9%` | `#171717` | Cards, panels (Dark mode: lighter than BG for depth). |
| **Card-Fg** | `0 0% 6%` | `#0F0F0F` | `0 0% 100%` | `#FFFFFF` | Text on cards. |
| **Muted** | `0 0% 96%` | `#F4F4F4` | `0 0% 15%` | `#262626` | Muted backgrounds. |
| **Muted-Fg** | `0 0% 42%` | `#6B6B6B` | `0 0% 60%` | `#999999` | Muted text, descriptions. |
| **Border** | `0 0% 84%` | `#D6D6D6` | `0 0% 16%` | `#292929` | Hairlines, dividers, input borders. |
| **Input** | `0 0% 84%` | `#D6D6D6` | `0 0% 16%` | `#292929` | Input field borders. |
| **Ring** | `204 32% 27%` | `#2F4A5C` | `204 32% 27%` | `#2F4A5C` | Focus ring color. |
| **Accent** | `204 32% 27%` | `#2F4A5C` | `204 32% 27%` | `#2F4A5C` | Accent elements. |
| **Destructive** | `359 58% 39%` | `#9E2A2B` | `359 58% 39%` | `#9E2A2B` | Errors, delete actions, warnings. |
| **Destructive-Fg** | `0 0% 100%` | `#FFFFFF` | `0 0% 100%` | `#FFFFFF` | Text on destructive elements. |

### CSS Variables Location
All color tokens are defined in `src/app/(landing)/global.css` using CSS custom properties.

---

## 4. UI Elements & Design Tokens

### Border Radius
The system uses a variable radius `var(--radius)` defaulting to **0.5rem (8px)**.

| Utility | Value | Usage |
| :--- | :--- | :--- |
| `rounded-lg` | `var(--radius)` (8px) | Primary buttons, cards, major containers. |
| `rounded-md` | `calc(var(--radius) - 2px)` (6px) | Secondary elements, inputs. |
| `rounded-sm` | `calc(var(--radius) - 4px)` (4px) | Small elements, badges. |
| `rounded-full` | `9999px` | Pills, chips, avatar containers. |

### Focus States
Accessible focus rings are implemented globally for keyboard navigation:
- **Style:** `outline: 2px solid hsl(0 0% 42%)` (Muted grey)
- **Offset:** `2px`
- **Border Radius:** `4px`

```css
/* src/app/(landing)/global.css */
*:focus-visible {
  outline: 2px solid hsl(0 0% 42%);
  outline-offset: 2px;
  border-radius: 4px;
}
```

### Background Patterns
A custom grid pattern is used for visual texture and depth.

**Utility:** `.bg-grid-pattern`

**Implementation:**
- **Light Mode:** 5% opacity black grid lines
- **Dark Mode:** 5% opacity white grid lines
- **Grid Size:** 40px × 40px
- **Usage:** Hero sections, feature backgrounds

```css
.bg-grid-pattern {
  background-image:
    linear-gradient(to right, rgba(0, 0, 0, 0.05) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(0, 0, 0, 0.05) 1px, transparent 1px);
  background-size: 40px 40px;
}

.dark .bg-grid-pattern {
  background-image:
    linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
}
```

### Smooth Scrolling
```css
html {
  scroll-behavior: smooth;
}
```

### Transitions
Body transitions for theme switching:
```css
body {
  @apply bg-background text-foreground transition-colors duration-300 ease-in-out;
}
```

---

## 5. Components

### Buttons (`CTAButton` & `CTAButton2`)

Two primary button components manage call-to-action hierarchies, located in `src/components/CTAButtons.tsx`.

#### CTAButton (Primary/Marketing Actions)
**Purpose:** High-priority conversions, primary user actions.

**Features:**
- Rounded-lg corners
- Font-medium weight
- Smooth transitions on all properties
- Optional `ArrowRight` icon that slides on hover
- Focus ring with offset
- Supports `onClick` handlers and `Link` navigation
- External link support (`target`, `rel`)

#### CTA Type Architecture (v1.1)
The `ctaType` prop (Types `cta-1` | `cta-2` | `cta-3` | `cta-4`) strictly governs the component's underlying behavior and routing logic, independently of its visual `variant`.

| CTA Type | Behavior | Link Type | Special Logic |
| :--- | :--- | :--- | :--- |
| `cta-1` | **Engine Entry** | External Anchor | Dynamically builds the Engine URL based on current locale and theme. Always opens in `_blank`. |
| `cta-2` | **Security Modal** | Button | **Hardcoded Trigger:** Intercepts clicks to open the `SecurityModal`. Prevents default navigation even if `href` is provided. |
| `cta-3` | **Standard Link** | `Link` / Anchor | Default navigational link. Uses provided `href`. Supports internal `next-intl` routing. **Auto-detects** `mailto:` and `tel:` to use standard `<a>` tags. |
| `cta-4` | **Alt Link** | `Link` / Anchor | Similar to `cta-3`, used for secondary links. **Auto-detects** `mailto:` and `tel:` to use standard `<a>` tags. |

**CRITICAL:** Never use `cta-2` for a button that is intended to navigate to a page (like `/blog` or WhatsApp). Use `cta-3` or `cta-4` for all navigational links.

**Example (Navigational Link):**
```tsx
<CTAButton
  href="/blog"
  variant="secondary"
  size="md"
  ctaType="cta-3"
>
  Visitar Blog
</CTAButton>
```

**Example (Security Modal Trigger):**
```tsx
<CTAButton
  href="#"
  variant="secondary"
  size="md"
  ctaType="cta-2"
>
  Ver protocolos de seguridad
</CTAButton>
```

#### CTAButton2 (Secondary/Navigational Actions)
**Purpose:** Secondary navigation, exploratory actions.

**Features:**
- Rounded-lg corners
- Font-medium weight
- Always includes `ChevronRight` icon that slides on hover
- Group hover effects
- Focus ring support

**Variants:**

| Variant | Visual Style | Use Case |
| :--- | :--- | :--- |
| `outline` | Solid **White** background (`#FFFFFF`), 2px border. Hover changes border/text to **Primary** color. | Secondary CTAs, outlined actions. |
| `ghost` | No border/background initially. Hover adds subtle accent background and primary text. | Tertiary actions, minimal emphasis. |

**Sizes:** Same as `CTAButton` (sm, md, lg).

**Example:**
```tsx
<CTAButton2
  href="/learn-more"
  variant="outline"
  size="md"
>
  Learn More
</CTAButton2>
```

### Hero Component

**Location:** `src/components/Hero.tsx`

**Purpose:** Primary landing section with headline, description, CTAs, and optional interactive elements.

**Features:**
- Grid pattern background
- Responsive typography scaling
- HTML content support via `HtmlContent` component
- Optional "smart chips" for document type selection
- Primary and secondary CTA support
- Trust signals (Founders Grant, Incinerator Protocol)
- Customizable background variants

**Props:**
- `title`: Main headline (supports HTML)
- `subtitle`: Badge text above title
- `description`: Supporting paragraph
- `primaryCTA`: Main action button
- `secondaryCTA`: Optional secondary action
- `chips`: Optional interactive document type selectors
- `prompt`: Text above chips
- `foundersGrant`: Trust signal text
- `incineratorProtocol`: Additional trust signal
- `backgroundVariant`: Visual style options

**Smart Chips:**
Recent update ensures chips use `bg-background` to match hero section background in both light and dark modes, preventing grid pattern visibility through transparent chips.

### Institutional Authority Signal
A microcopy bridge between the Hero and the Features section, designed to project technical authority and legal-tech positioning.

**Specifications:**
- **Translation Key:** `branding.authoritySignal`
- **Component:** Inline `div` with `font-mono` typography.
- **Styling:** `text-xs tracking-widest uppercase text-muted-foreground`.
- **Background:** `bg-muted/20` with a 1px bottom border.
- **Localization:**
    - **ES:** "Motor de Tecnología Legal"
    - **EN:** "Legal Technology Engine"
- **Purpose:** Contextual SEO density and cognitive framing of the system as an "engine".

### Header Component

**Location:** `src/components/Header.tsx`

**Features:**
- Responsive navigation
- Language toggle (EN/ES)
- Theme toggle (Light/Dark)
- Mobile menu support
- Sticky positioning
- Internationalized navigation links

### Footer Component

**Location:** `src/components/Footer.tsx`

**Features:**
- Multi-column layout
- Social media links
- Legal page links (Privacy, Terms)
- Newsletter signup
- Copyright information
- Responsive grid layout

### Layout Components

**Location:** `src/components/Layout.tsx`

Wrapper component combining Header and Footer for consistent page structure.

### Theme Provider

**Location:** `src/components/providers/ThemeProvider.tsx`

**Features:**
- `next-themes` integration
- System theme detection
- Theme persistence via localStorage
- Hydration-safe theme script
- Class-based theme switching

---

## 6. Internationalization (i18n)

### Implementation
**Library:** `next-intl` v4.5.5

**Supported Locales:**
- English (`en`)
- Spanish (`es`)

### Structure
```
src/
├── app/
│   ├── (landing)/         # Landing site route group
│   │   ├── global.css     # Landing-specific styles
│   │   ├── layout.tsx     # Root layout with fonts
│   │   ├── [locale]/      # Locale-based routing
│   │   │   ├── layout.tsx # Locale layout with NextIntlClientProvider
│   │   │   ├── page.tsx   # Home page
│   │   │   ├── about-us/
│   │   │   ├── contact/
│   │   │   ├── our-services/
│   │   │   ├── prices/
│   │   │   ├── questions-and-answers/
│   │   │   ├── privacy/
│   │   │   └── terms/
│   └── (sovereign)/       # Sovereign app route group (separate app)
├── i18n/
│   └── navigation.ts      # Internationalized Link and routing
└── messages/
    ├── en.json            # English translations
    └── es.json            # Spanish translations
```

### Static Generation
All locale routes are statically generated at build time:
```typescript
// src/app/(landing)/[locale]/layout.tsx
export function generateStaticParams() {
  return locales.map((locale) => ({ locale }));
}
```

### Navigation
Custom `Link` component from `src/i18n/navigation.ts` automatically handles locale prefixing.

---

## 7. Technical Stack

### Core Framework
- **Framework:** Next.js 14.2.5 (App Router)
- **React:** 18.3.1
- **TypeScript:** 5.5.4

### Styling
- **CSS Framework:** Tailwind CSS 3.4.18
- **PostCSS:** 8.4.39
- **Autoprefixer:** 10.4.19

### Theming & i18n
- **Theme Management:** `next-themes` 0.4.6
- **Internationalization:** `next-intl` 4.5.5

### Icons
- **Icon Library:** `lucide-react` 0.395.0

### Build & Export
- **Output:** Static export (`output: 'export'` in `next.config.js`)
- **Deployment:** Cloudflare Pages, Azure Static Web Apps

### Testing
- **Unit Tests:** Jest 30.2.0 with React Testing Library
- **E2E Tests:** Playwright 1.56.1

### Code Quality
- **Linting:** ESLint 8.57.1 with Next.js config
- **Formatting:** Prettier 3.6.2
- **Commit Linting:** Commitlint with Conventional Commits

---

## 8. File Structure

### Key Files
- `src/app/(landing)/global.css` - Landing site styles and CSS variables
- `src/app/(landing)/layout.tsx` - Root layout with fonts and metadata
- `src/app/(landing)/[locale]/layout.tsx` - Locale-specific layout
- `tailwind.config.ts` - Tailwind configuration
- `next.config.js` - Next.js configuration

### Component Organization
```
src/components/
├── CTAButtons.tsx              # Primary and secondary CTA buttons
├── Hero.tsx                    # Hero section component
├── Header.tsx                  # Site header with navigation
├── Footer.tsx                  # Site footer
├── Layout.tsx                  # Page layout wrapper
├── HtmlContent.tsx             # Safe HTML rendering
├── LanguageToggle.tsx          # Language switcher
├── ThemeProvider.tsx           # Theme management (deprecated location)
├── providers/
│   └── ThemeProvider.tsx       # Theme provider (current)
├── sections/
│   └── HeroSection.tsx         # Alternative hero implementation
└── ui/                         # Reusable UI primitives
```

---

## 9. Design Principles

### Visual Hierarchy
1. **Primary:** Hero CTAs, main navigation, primary headings
2. **Secondary:** Feature cards, secondary navigation, subheadings
3. **Tertiary:** Footer links, metadata, supporting text

### Accessibility
- WCAG 2.1 AA compliant color contrast
- Keyboard navigation support
- Focus indicators on all interactive elements
- Semantic HTML structure
- ARIA labels where appropriate

### Responsive Design
- **Mobile-first approach**
- **Breakpoints:** sm (640px), md (768px), lg (1024px), xl (1280px)
- **Fluid typography:** Scales from mobile to desktop
- **Flexible layouts:** Grid and flexbox for adaptability

### Performance
- **Font optimization:** `next/font` with `display: swap`
- **Static generation:** All pages pre-rendered at build time
- **Minimal JavaScript:** Static export with minimal client-side JS
- **Image optimization:** Next.js Image component (where applicable)

---

## 10. Brand Voice & Messaging

### Tone
- **Professional yet approachable**
- **Technical but clear**
- **Confident without arrogance**
- **Solution-focused**

### Key Messages
- Legal infrastructure automation
- Minimal friction
- Reliable and efficient
- B2B focus
- Regional expertise (Central America)

---

## 11. Maintenance & Updates

### Color Token Updates
Modify `src/app/global.css` in the `:root` and `.dark` selectors.

### Typography Changes
Update font imports in `src/app/layout.tsx` and Tailwind config in `tailwind.config.ts`.

### Component Modifications
All components are in `src/components/` - follow existing patterns for consistency.

### Translation Updates
Edit `src/messages/en.json` and `src/messages/es.json` for content changes.

---

## 12. References

- **Design System:** Based on shadcn/ui principles
- **Color Palette:** Institutional Greyscale + Blue-Grey Accent
- **Typography:** Inter (body) + IBM Plex Sans (display)
- **Icons:** Lucide React
- **Deployment:** Static export to Cloudflare Pages

---

**Last Updated:** February 2026  
**Version:** 1.0.1  
**Maintained by:** Cyboring Technologies
