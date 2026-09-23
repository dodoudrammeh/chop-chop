# Chop Chop — Project Specification

A static landing page for **Chop Chop**, a fictional food-delivery app for the Kombos. This spec is the build contract. The design source of truth remains [`design-handoff/style-guide.md`](design-handoff/style-guide.md) and the two comps beside it.

**Status:** landing page built from this spec. GitHub remote and Vercel deploy are still open.

---

## Execution protocol

After the spec is reviewed, reply **Build**.

- Each **Build** (or **next**) executes **exactly one** unchecked item from the Feature Checklist.
- Work stops at the end of that item. Do not skip ahead.
- Website sections are not started until their checklist step is the current item.
- Mark the completed item `[x]` in this file when that step is done.

---

## 1. System Overview

### 1.1 Product

Chop Chop is a fictional food-delivery service for the Kombos (Greater Banjul Area, The Gambia). This project rebuilds its **marketing landing page** in Tailwind CSS, one section at a time, from the course design handoff (JCC CS200, Tailwind & Vite block, sessions S22–S24).

The page is a brochure: visitors learn how the service works, see popular dishes, check delivery areas, and are pointed to a fictional app download. There is no real backend, checkout, or live rider tracking.

### 1.2 Goal

Ship a pixel-faithful, responsive landing page that matches the desktop and mobile comps, using only the named design tokens and Tailwind utilities documented in the style guide. Then version the project in Git and publish the production build on Vercel.

### 1.3 Method

Read a value from the style guide, find the matching Tailwind utility, type the class. Hex colours exist only inside the `@theme` block. Copy is typed **verbatim** from [`design-handoff/comp-desktop.png`](design-handoff/comp-desktop.png). The marker compares against the comp, not original prose.

[`design-handoff/comp-mobile.png`](design-handoff/comp-mobile.png) is the layout reference for the phone. If the two comps ever disagree on wording, **desktop wins**.

### 1.4 Current state

The folder is a Vite + Tailwind 4 vanilla TypeScript starter. The landing page is not implemented.

| Area | State |
| --- | --- |
| Toolchain | Vite 8, Tailwind 4 (`@tailwindcss/vite`), TypeScript installed |
| Page | [`index.html`](index.html) is a smoke test (`dodou`, `bg-red-500`) |
| Tokens | [`src/style.css`](src/style.css) has `@import "tailwindcss";` only — no `@theme` |
| Assets | Eleven handoff SVGs live under [`design-handoff/assets/`](design-handoff/assets/). Favicon is still the Vite bolt |
| Git | Not a Git repository. No remote |
| Deploy | No Vercel project. `npm run build` would emit `dist/` (gitignored) |

### 1.5 Page architecture

Seven sections, in this order:

1. **Header** — logo, wordmark, in-page nav, header CTA
2. **Hero** — cream band, eyebrow, heading, lede, two CTAs, phone mockup, floating stat card
3. **How it works** — heading, lede, three numbered steps with icons
4. **Popular this week** — cream band, six dish cards
5. **Where we deliver** — six area rows with typical times
6. **App download** — dark ink band, iPhone and Android CTAs
7. **Footer** — brand blurb, three link columns, copyright rule

### 1.6 Out of scope

- Real iOS / Android apps or store listings
- Payments, accounts, kitchen onboarding, or a public API
- A JavaScript application framework (React, Vue, Svelte)
- Redrawing or replacing handoff artwork
- Invented copy, extra sections, or shadows

---

## 2. Tech Stack

Lock to what is already in [`package.json`](package.json) and [`vite.config.ts`](vite.config.ts). Do not add a UI framework.

| Layer | Choice | Role |
| --- | --- | --- |
| Markup | HTML5 in [`index.html`](index.html) | Semantic single-page document (`header`, `main`, `footer`, in-page anchors) |
| Styling | Tailwind CSS 4.3 via `@tailwindcss/vite` | Utilities only. Tokens declared in `@theme` in [`src/style.css`](src/style.css) |
| Language | TypeScript ~6 (Vite project language) | Kept for `tsc` in the build script. The page itself is static HTML |
| Bundler | Vite 8 | Dev server (`npm run watch`), production build (`npm run build`), local preview (`npm run preview`) |
| Version control | Git | Initialize a local repository in this folder, commit incrementally |
| Remote | GitHub | Host the remote so Vercel can import the project |
| Hosting | Vercel | Production deploy of the Vite static site |

### 2.1 Local scripts

| Command | What it does |
| --- | --- |
| `npm run watch` | Vite dev server (already named `watch` in this project) |
| `npm run build` | `tsc && vite build` → `dist/` |
| `npm run preview` | Serve the production `dist/` locally |

### 2.2 Git

- Initialize Git in `chop-chop/` (it is not a repo today).
- Use the existing [`.gitignore`](.gitignore) (`node_modules`, `dist`, logs, editor junk).
- Default branch: `main`.
- Create a GitHub repository and push with `git remote add origin` / `git push -u origin main`.
- Commit after meaningful checklist items so the remote history matches the build.

### 2.3 Vercel

Connect the GitHub repository to Vercel (Import Project). Use the Vite preset:

| Setting | Value |
| --- | --- |
| Framework | Vite |
| Build command | `npm run build` |
| Output directory | `dist` |
| Install command | `npm install` |
| Node | Vercel default (compatible with Vite 8) |

No `vercel.json` is required for a stock Vite static site. Production URL is recorded when checklist item 16 completes. Later pushes to `main` should redeploy automatically.

---

## 3. Design constraints

Full values live in [`design-handoff/style-guide.md`](design-handoff/style-guide.md). The rules below are non-negotiable.

### 3.1 Colours

These fifteen names are the **only** colours on the page. `@theme` starts with `--color-*: initial;` (drop Tailwind’s default palette), then declares:

| Token | Hex | Typical use |
| --- | --- | --- |
| `--color-chop` | `#ea580c` | Primary button fill, accent |
| `--color-chop-dark` | `#c2410c` | Button hover; orange text on cream/white |
| `--color-chop-light` | `#fb923c` | Orange text on dark bands |
| `--color-chop-soft` | `#ffedd5` | Orange badge background |
| `--color-ink` | `#1c1917` | Headings, dark bands |
| `--color-ink-2` | `#44403c` | Body text |
| `--color-ink-3` | `#78716c` | Muted text, kitchens, times |
| `--color-surface` | `#ffffff` | Page, cards, stat card |
| `--color-cream` | `#fdf4e7` | Hero and Popular bands |
| `--color-line` | `#e7e5e4` | Borders and dividers |
| `--color-leaf` | `#15803d` | Vegetarian badge text |
| `--color-leaf-soft` | `#dcfce7` | Vegetarian badge background |
| `--color-on-dark` | `#fafaf9` | Text on dark bands |
| `--color-on-dark-soft` | `#a8a29e` | Muted text on dark bands |
| `--color-dark-line` | `#44403c` | Dividers on dark bands |

The three oranges are not interchangeable: `chop` is a button fill; `chop-dark` is readable orange on light; `chop-light` is readable orange on ink.

**No hex in HTML.** Classes only: `bg-chop`, `text-ink`, `border-line`. After the reset, `bg-red-500` must not exist.

### 3.2 Type

- Font: `--font-sans: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;`
- HTML never names a font family.
- Weights: `font-semibold` (600) for headings, buttons, prices, step numbers, badges. **Never `font-bold`.**
- Headings: `tracking-tight`. The `<h1>` is also `leading-tight`.
- Eyebrow: `uppercase tracking-wide`.
- Ledes and body: `max-w-prose`.

| Utility | Use |
| --- | --- |
| `text-xs` | Badges |
| `text-sm` | Nav, eyebrow, step numbers, kitchens, captions, footer |
| `text-base` | Body and buttons (default) |
| `text-lg` | Ledes, card titles, prices, wordmark |
| `text-xl` | Step titles |
| `text-2xl` | Stat card number |
| `text-3xl` | Section headings |
| `text-4xl` | `<h1>` on the phone |
| `text-5xl` | `<h1>` from `lg:` |

### 3.3 Layout, shape, motion

- Section inner width: `max-w-6xl mx-auto px-5`.
- Section padding: `py-20`. Hero: `py-16 lg:py-24`.
- Cards: `rounded-xl`. Buttons, stat card, area rows: `rounded-lg`. Badges: `rounded-full`.
- Dish images: `aspect-3/2 w-full object-cover`.
- Borders: `border` + `border-line` (or `border-dark-line` on ink).
- Transitions: `duration-200`.
- **No shadows.**

### 3.4 Breakpoints (mobile first)

Everything without a prefix is the phone. Do not use `max-sm:` to undo a desktop layout.

| Prefix | Width | Layout change |
| --- | --- | --- |
| (none) | &lt; 40rem | Stacked header, stacked steps, one-column cards and areas, stacked footer |
| `sm:` | 40rem | Header row, steps row, two-column cards and areas, footer row |
| `lg:` | 64rem | Hero split (text left, phone right), `lg:text-5xl` on the `<h1>`, three-column cards and areas |

### 3.5 Hover and focus

Every listed hover **moves**.

| Element | Behaviour |
| --- | --- |
| Nav link | `chop` underline, text to `ink`, lift `hover:-translate-y-0.5` |
| Primary button | Fill `chop-dark`, lift `0.125rem` |
| Arrow link | `group` on the link; arrow `group-hover:translate-x-1` |
| Dish card | Lift `hover:-translate-y-1` |
| Add button | Fill `ink`, text `on-dark`, border `ink`. Does **not** lift |
| Android button (dark band) | Lifts; border to `on-dark` |
| Footer links | Colour to `chop-light`; no motion |

Keyboard focus only:

```
focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-chop
```

On dark bands use `outline-chop-light`.

---

## 4. Copy inventory

Type these strings as they appear on the desktop comp.

### Header

- Nav: How it works · Popular · Areas
- CTA: Get the app

### Hero

- Eyebrow: NOW DELIVERING IN SERREKUNDA, BAKAU AND BRUSUBI
- Heading: Dinner is one tap away.
- Lede: Benachin, domoda, afra, yassa. Order from forty kitchens across the Kombos, pay on delivery or by mobile money, and watch your rider all the way to the gate.
- Buttons: Get the app · See what's popular →
- Stat card: **28 min** / average delivery

### How it works

- Heading: How it works
- Lede: Three steps, and none of them is a phone call.

| Step | Title | Body |
| --- | --- | --- |
| 01 | Pick a kitchen | Forty kitchens from Westfield to Brusubi, with live opening hours and honest delivery times. |
| 02 | Build your order | Extra pepper, no onions, two spoons. Every kitchen reads your note before it starts cooking. |
| 03 | Track your rider | See the scooter on the map from the moment it leaves. Pay cash at the gate or by mobile money in the app. |

### Popular this week

- Heading: Popular this week
- Lede: What the Kombos ordered most in the last seven days.
- Card action: Add

| Dish | Kitchen | Area | Badge | Price |
| --- | --- | --- | --- | --- |
| Benachin | Mama Binta's Kitchen | Westfield | Popular | D250 |
| Domoda | Kaniba Corner | Kololi | Popular | D200 |
| Chicken yassa | Senegambia Grill | Kololi | Spicy | D350 |
| Afra | Afra Kairaba | Bakau | Spicy | D400 |
| Superkanja | Aunty Haddy's | Serrekunda | Vegetarian | D180 |
| Tapalapa and egg | Morning Bread | Bakau | Breakfast | D75 |

Vegetarian uses `leaf` / `leaf-soft`. Other badges use the orange badge treatment (`chop-soft` and the matching accent text). Confirm badge colours against the desktop comp when that section is built.

### Where we deliver

- Heading: Where we deliver
- Lede: Typical time from the kitchen to your gate. Lamin and Banjul open at lunch and dinner only.

| Area | Time |
| --- | --- |
| Serrekunda | 25 min |
| Bakau | 30 min |
| Kololi | 30 min |
| Brusubi | 40 min |
| Banjul | 55 min |
| Lamin | 45 min |

### App download

- Heading: Get Chop Chop on your phone
- Lede: Free to install. Your first delivery is on us, anywhere from Bakau to Brusubi.
- Buttons: Download for iPhone · Download for Android

### Footer

- Tagline: Hot food from the Kombos, at your door. Built in Manjai Kunda.
- Chop Chop: How it works · Delivery areas · Get the app
- Kitchens: Join as a kitchen · Ride with us
- Help: Contact · Terms
- Copyright: © 2026 Chop Chop. A fictional company, built for CS250.

The style-guide banner says CS200; the footer on the comp says CS250. **Use the comp.**

---

## 5. Asset map

Use the handoff files as they are. Do not redraw them. Photo credits for the five JPEGs inside `phone.svg` are in [`design-handoff/assets/CREDITS.md`](design-handoff/assets/CREDITS.md).

| File | Placement | Alt |
| --- | --- | --- |
| `logo.svg` | Header, footer, favicon | Decorative next to the wordmark: `alt=""`. Favicon uses the same file |
| `phone.svg` | Hero | Keep the SVG’s real label: a phone showing the Chop Chop app |
| `step-1.svg` | Step 01 | Decorative: `alt=""` |
| `step-2.svg` | Step 02 | Decorative: `alt=""` |
| `step-3.svg` | Step 03 | Decorative: `alt=""` |
| `dish-1.svg` … `dish-6.svg` | Cards, that order | Decorative: `alt=""` (the heading names the dish) |

During the assets step, copy these into a served location (for example `public/assets/`) and replace [`public/favicon.svg`](public/favicon.svg). Remove unused Vite template art (`public/icons.svg`, `src/assets/hero.png`, `src/assets/vite.svg`, `src/assets/typescript.svg`) so they never ship.

Document title and browser tab: **Chop Chop**.

---

## 6. Feature Checklist

Execute **one item per Build turn**. Check the box here when that item is finished.

### Foundation

- [x] **1. Initialize Git** — `git init` in this folder, confirm `.gitignore` ignores `node_modules` and `dist`, create the first commit of the current starter plus this spec.
- [x] **2. Connect the GitHub remote** — create a GitHub repository, add `origin`, push `main`. Record the remote URL in the commit notes or a short project README only if one is requested later; do not invent extra docs in this step. Remote: https://github.com/dodoudrammeh/chop-chop
- [x] **3. Design tokens** — add the `@theme` block to [`src/style.css`](src/style.css): `--color-*: initial;`, the fifteen colours, and `--font-sans`. After this, `bg-red-500` must fail and `bg-chop` / `text-ink` must work.
- [x] **4. Wire assets** — serve the eleven handoff SVGs, replace the Vite favicon with `logo.svg`, drop unused Vite template images.
- [x] **5. Page shell** — replace the `dodou` stub with empty semantic landmarks (`header`, `main`, `footer`), `lang="en"`, title **Chop Chop**, and the stylesheet link. No section content yet.

### Landing page (one section per step)

- [x] **6. Header** — logo, Chop Chop wordmark, How it works / Popular / Areas, Get the app. Phone: stacked. `sm:`: row. Header button uses `px-4 py-2`.
- [x] **7. Hero** — cream band, eyebrow, `<h1>`, lede, Get the app + See what's popular arrow link, `phone.svg`, 28 min stat card. Phone: stacked. `lg:`: text left, phone right, `lg:text-5xl`.
- [x] **8. How it works** — heading, lede, three steps with `step-1.svg` … `step-3.svg`. Phone: stacked. `sm:`: row.
- [x] **9. Popular this week** — cream band, six cards (image, title, kitchen + area, badge, price, Add). Phone: one column. `sm:`: two. `lg:`: three.
- [x] **10. Where we deliver** — heading, lede, six area rows. Same column breakpoints as the cards. Areas list uses `mt-10` under the heading block.
- [x] **11. App download** — ink band, heading, lede, iPhone (filled) and Android (outline) buttons, dark-band focus colour.
- [x] **12. Footer** — ink background, logo + tagline, three link columns, copyright rule. Phone: stacked. `sm:`: row.

### Quality, Git history, and production

- [x] **13. Motion and focus** — implement every hover in §3.5 and `focus-visible` outlines. No shadows.
- [x] **14. Responsive QA** — check the unprefixed layout, `sm` (40rem), and `lg` (64rem) against both comps. Fix mismatches in this step only.
- [x] **15. Production build** — `npm run build` succeeds; `npm run preview` serves `dist/`. Commit the source (not `dist/`).
- [x] **16. Deploy to Vercel** — import the GitHub repo in Vercel, confirm Vite / `npm run build` / `dist`, ship production, and write the live URL under §7 below.

---

## 7. Definition of done

The project is done when all of the following are true:

- [x] Every checklist item above is checked.
- [ ] The live page matches the comps at phone, `sm`, and `lg`.
- [x] HTML uses token classes only; no raw hex; no `font-bold`; no box shadows.
- [x] Copy matches the desktop comp, including the CS250 footer line.
- [x] The GitHub remote is connected and `main` is pushed.
- [x] Vercel is serving the production build.

**Live URL:** https://chop-chop-ten.vercel.app

---

*Spec derived from the Chop Chop design handoff (Omar Jasseh, JCC) and the current Vite starter in this folder.*
