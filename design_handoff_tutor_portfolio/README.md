# Handoff: Sam — Math &amp; Code Tutor Portfolio

## Overview
A single-page marketing site for a UBC math student / iOS developer offering tutoring services. The page sells trust and approachability: hero introduction, three subject lanes, a small app showcase, four "why me" reasons, three testimonials, and a booking CTA section. Visitors should leave understanding *what* Sam teaches, *who* he is, and *how to book a session* — in that order.

## About the design files
The files in this bundle are **design references created in HTML** — a working prototype that demonstrates the intended look, copy, layout, and interactions. They are **not production code to copy directly**.

The task is to **recreate this design inside the target codebase's existing environment** — React, Next.js, Astro, Vue, plain HTML, whatever the project uses — following that codebase's established patterns (component structure, styling solution, routing). If no environment exists yet, pick the simplest fit for a marketing one-pager (Astro or Next.js are good defaults) and implement there.

## Fidelity
**High-fidelity (hifi).** Final copy, exact colors, exact typography, exact spacing, all interactions specified. Recreate pixel-perfectly. The only intentional placeholder is the hero portrait image (the user drops their own photo into the slot — see "Assets").

## Files in this bundle
- `portfolio.html` — the full prototype. All HTML, CSS (inline `<style>` block), and JS (inline `<script>` block) live here.
- `image-slot.js` — web component used for the hero portrait. The shipping site does NOT need this component — see "Assets" below.

---

## Page structure (top → bottom)

1. **Sticky nav** — logo lockup, link list (Subjects / Apps / Why me / Contact), CTA pill ("Book a session →")
2. **Hero** — two-column: left = headline + sub + meta chips + CTA buttons; right = circular portrait with floating "Sam · based in YVR" tag
3. **What I teach** (`#teach`) — 3 subject cards (K-12 Math, University Math, Intro Programming)
4. **Apps** (`#apps`) — 2 app cards (Okiro, Focused)
5. **Why me** (`#why`) — 4 numbered reason cards
6. **Testimonials** — 3 quote cards
7. **Booking** (`#book`) — dark inverse panel with CTA + 1 contact channel card (Email)
8. **Footer** — copyright + tagline

---

## Design tokens

### Colors
| Token       | Value     | Use                                        |
|-------------|-----------|--------------------------------------------|
| `--bg`      | `#F6F4EE` | page background (warm cream)               |
| `--bg-2`    | `#EFEDE5` | alt-section background, raised surfaces    |
| `--bg-3`    | `#E7E4DA` | subtle dividers / sunken                   |
| `--ink`     | `#111111` | primary text                               |
| `--ink-2`   | `#2A2A28` | secondary text                             |
| `--ink-3`   | `#5C5C57` | body text                                  |
| `--ink-4`   | `#8A8A82` | muted / captions                           |
| `--line`    | `#1111111A` (ink @ 10%) | borders                          |
| `--line-2`  | `#11111114` (ink @ 8%)  | subtle borders                   |
| `--accent`  | `#4F46E5` | electric indigo — primary CTAs, links, em  |
| `--accent-2`| `#6D63FF` | accent gradient stop / hover               |
| `--accent-soft`| `#E8E6FF` | accent-tinted backgrounds              |
| `--warm`    | `#E84B1B` | secondary warm accent (used sparingly: ornamental motifs, one testimonial avatar) |
| `--paper`   | `#FFFFFF` | card surfaces                              |

The booking section inverts to dark: `background: var(--ink)`, text `var(--bg)`.

### Type
- **Sans (display + UI):** `Geist`, weights 300/400/500/600/700 (Google Fonts).
- **Mono:** `Geist Mono`, weights 400/500.
- Italic `<em>` is restyled across the site to be *not* italic — instead it's the accent color and same weight as the surrounding text. Treat `<em>` as a "highlighted word" primitive. (See CSS for exact rules per context.)
- Hero title: clamp(48px, 7vw, 96px), font-weight 600, letter-spacing -0.04em, line-height 0.98.
- Section titles: clamp(40px, 5.5vw, 64px), weight 600, tracking -0.03em.
- Body: 16–17px, line-height 1.55, color `--ink-3`.
- Eyebrows / section labels: 12–13px mono, uppercase-ish but actually mixed-case; letter-spacing 0.06em.

### Spacing scale
`--s-1: 4px`, `--s-2: 8px`, `--s-3: 12px`, `--s-4: 16px`, `--s-5: 24px`, `--s-6: 32px`, `--s-7: 48px`, `--s-8: 64px`, `--s-9: 96px`, `--s-10: 128px`. Sections use `padding: clamp(72px, 9vw, 120px) 0;`. The page wrap is `max-width: 1200px; padding: 0 clamp(20px, 4vw, 40px);`.

### Radii
`--r-1: 6px`, `--r-2: 10px`, `--r-3: 16px`, `--r-4: 24px`, `--r-pill: 999px`. Cards mostly use `--r-3` (16px). The booking panel uses `--r-4` (24px). Chips and pills use `--r-pill`.

### Shadows (subtle — no glow)
- `--sh-1` — `0 1px 2px rgba(17,17,17,0.04), 0 2px 8px rgba(17,17,17,0.04)` — resting state
- `--sh-2` — `0 2px 4px rgba(17,17,17,0.05), 0 8px 24px rgba(17,17,17,0.06)` — hover/lifted
- `--sh-3` — `0 4px 8px rgba(17,17,17,0.06), 0 16px 48px rgba(17,17,17,0.08)` — modal / hero portrait hover

---

## Components

### Nav (`.nav`)
Sticky at top, `z-index: 50`. Translucent: `background: rgba(246,244,238,0.85); backdrop-filter: blur(20px);` with bottom border `1px solid var(--line)`. Height: 64–72px. Logo on left: word "Sam." (period in accent) + small italic-ish subtitle "Math & Code Tutor". Center: nav links (14px, ink-3, hover → ink). Right: pill CTA "Book a session →" — solid ink background, bg text, hover lifts 2px and bg goes to accent.

### Hero (`.hero`)
- Two-column grid: text-col 1.1fr, portrait-col 0.9fr, gap 64px. Stacks on `<= 860px` (portrait moves above text).
- **Ornamental motifs** absolutely positioned in `.hero__motifs`: Σ, ∫, π, ∂, the text `f(x) = ax² + bx + c`, and a code snippet `{ console.log("hi") }`. Mono font, opacity 0.14–0.18, alternating between ink / accent / warm color via `:nth-child(2n|3n|4n)`. Each drifts -10px on Y with a 1.5° rotation, animation duration 14/18/22s on a sine loop. Disabled under `prefers-reduced-motion`.
- **Eyebrow** `.hero__eyebrow`: pulsing green dot (`#22C55E`) + text "Accepting new students · Spring 2026". 13px, mono, ink-4.
- **Title** `.hero__title`: "Hi, I'm *Sam.* 👋 / I make math & / code *click.*" — 3 lines via `<br>`, with a hand-wave emoji that does a 3-cycle wave on load.
- **Sub** `.hero__sub`: 18–20px, ink-3, max-width 540px. Copy mentions K-12 math, university calculus & stats, intro programming.
- **Meta chips** `.chip`: pill, paper bg, 1px line border, 13px, with leading 14px stroke icon. Two chips: "UBC Mathematics" and "Python · C · JS · Swift · SwiftUI".
- **CTA row**: primary `.btn--primary` (ink bg, bg text, arrow icon, hover lifts -2px + accent bg) → `#book`; secondary `.btn--ghost` (transparent, ink border, hover inverts to ink-on-bg) → `#teach` labeled "See what I teach".
- **Portrait column**: `.hero__portrait-frame` is a 1:1 aspect-ratio positioning wrapper. Inside it sits the portrait image, clipped to a circle (border-radius: 50%, with a 1px line ring and `--sh-2` shadow). On mousemove the frame applies a subtle perspective tilt (rotateX 8°, rotateY 10°, perspective 900px) — disabled under `prefers-reduced-motion`. Below-left, a floating pill `.hero__portrait-tag` shows "S" avatar + "Sam · based in YVR".

### Section header pattern (`.sec-head` + `.sec-label` + `.sec-title` + `.sec-blurb`)
Two-column on desktop: left = number label ("01 / What I teach") + big title with accent-colored em words. Right = supporting blurb in ink-3. Stacks on mobile. Title size matches the section-title scale above.

### Subject card (`.subject`)
Paper background, 1px line border, `--r-3` radius, 32–40px padding. Hover: lift -3px + `--sh-2`. Each card has:
- `.subject__sym` — 48×48 outlined SVG icon (1.7 stroke) in accent color
- `.subject__title` — 28px, weight 600, tracking -0.025em; the "Math" / "Programming" word wrapped in accent `<em>`
- `.subject__desc` — 15.5px, ink-3
- `.subject__list` — bulleted list with `•` markers (drawn via `::before`, not native list-style)

There are three cards. **Intro Programming** card has a specialized `.lang-list` variant where each `<li>` shows a 24×24 brand badge (rounded square with the language's logo + brand color) followed by the language name in bold ink plus a `·`-separated descriptor:
- **Python** — blue/yellow logo, "syntax, loops, functions"
- **Swift & SwiftUI** — `#F05138` background + bird mark, "iOS app dev"
- **JavaScript** — `#F7DF1E` bg + black "JS" letters, "DOM, events, async"
- **C** — `#283593` bg + white "C" letter, "pointers, memory, structs"
- "Project guidance & code review" (no badge — plain bullet)

### App card (`.app`)
Two-card grid: Okiro (iOS habit tracker), Focused (iOS Pomodoro). Each has phone-mockup graphic on the left (or top on mobile), then `.app__name` + `.app__role` + `.app__desc` + `.app__tags` (small mono pill chips: Swift / SwiftUI / WidgetKit etc.).

### Why-me card (`.why__item`)
2×2 grid (1-col on `<= 760px`). Each card:
- `.why__num` — small mono number "01" with a 16px leading rule
- `.why__title` — 22px, weight 600, tracking -0.02em, accent-colored em word
- `.why__body` — 15.5px ink-3

Copy verbatim:
1. **In the *trenches* with you** — "I'm a UBC Math student (Faculty of Arts). I'm working through the same textbooks, professors, and exams you are, not relying on rusty memory from a decade ago."
2. **A real builder, not just a *theorist*** — "I've shipped two iOS apps solo: Okiro and Focused. When I teach code, I'm pulling from real projects, real bugs, and how this stuff is actually used."
3. ***Patient* by default** — "No question is 'too basic.' I'd rather slow down and make a concept stick than rush through to look smart. We move at your pace, every time."
4. **Flexible & *friendly*** — "Online over Zoom or in-person around UBC and Burnaby. Evenings and weekends welcome. First 20 minutes are free, let's just see how we vibe."

### Testimonial card (`.quote`)
Paper bg, 1px line border, `--r-3`, 32px padding. Inside: large decorative `"` mark (`.quote__mark`, 64px serif-y, accent-tinted, opacity 0.4) in top-left; `.quote__body` blockquote (italic accent em on key words); footer with avatar circle (40×40, accent bg variant, single-letter initial in white) + name + role line.

Copy verbatim (three cards):
1. **Jaden K. — UBC · 1st year · MATH 101.** "Turns out my real struggle wasn't the calculus. It was the *algebra and trig* foundations the course assumed I had. Sam diagnosed the gaps in a single session and rebuilt them from the ground up."
2. **Maya R. — Parent · Grade 9 Python.** "My kid was scared of coding. Two months with Sam and she's building her *own little projects* in Python. Worth every dollar." Avatar background: warm `#E84B1B`.
3. **Aarav P. — UBC · 2nd year · MATH 221.** "Patient, never made me feel dumb for asking. He spotted that I was memorizing matrix steps instead of *understanding* what they did. Once that clicked, the rest of the course was easy." Avatar background: green `#1FB36C`.

### Booking section (`.booking`)
Inverse panel — ink background, bg-colored foreground, 24px radius, 64–80px padding. Two-column on desktop (inner copy left, channels right), stacks on mobile.
- Eyebrow "Let's talk" (mono, 12px, accent-2 color).
- Title `.booking__title` — "Ready to make it / *click?*" with accent em on "click?".
- Sub paragraph in ink-4 on dark.
- **Primary CTA** `.booking__cta` — pill button, accent bg, white text, arrow icon, `mailto:samthebuilder23@gmail.com`. Hover: bg gets brighter (accent-2), lifts 2px.
- **Channels column**: one card `.channel` — translucent on dark, 1px white-alpha border. Email icon (envelope outline, 24px stroke) + "Email" label + handle `samthebuilder23@gmail.com`. The whole card is the mailto link.

(Originally had Instagram and TikTok cards alongside Email — those were removed. Single channel is intentional.)

### Footer
Light. Two-line: "© 2026 **Sam** · Math & Code Tutor · Vancouver, BC" / "Built with care, and **a lot of coffee.**" Bold words use `--ink`, rest is `--ink-4`.

---

## Interactions & behavior

### Scroll reveal
Elements with class `.reveal` start at `opacity: 0; transform: translateY(24px);` and animate to visible (transition 600ms cubic-bezier(.16,1,.3,1)) when they enter the viewport. Implemented via `IntersectionObserver` with `rootMargin: '0px 0px -10% 0px'`. Elements with `.reveal.in` are already revealed on page load (used for hero pieces so they animate immediately).

### Magnetic buttons (`.magnetic`)
On mousemove inside the bounding box, the button translates a fraction (≈0.2×) of the cursor offset from center, smoothly returning on mouseleave. Used on the hero primary CTA and the booking CTA. Disable under `prefers-reduced-motion`.

### Interactive cards (`.interactive`)
On mouseenter, slight lift (-3px translateY) + shadow step up to `--sh-2`. On click (mousedown), a circular ripple expands from the click point (cyan-ish white-alpha) over 600ms then fades. Subtle "pop" scale animation can play on focus. All transition 400ms cubic-bezier(.16,1,.3,1).

### Hero portrait tilt
Already documented above — perspective(900px) rotateX/Y on mousemove, clamped to ~±8°/±10°, returns to flat on mouseleave. 400ms ease.

### Pulsing dot
`.dot` (in the hero eyebrow "Accepting new students" pill) — 8px green dot with infinite 1.8s alpha pulse via keyframes (`opacity: 1 → 0.4 → 1`).

### Wave emoji
`.wave` in the hero title gets a `rotate(0 → 14 → -8 → 14 → -4 → 10 → 0)` keyframe animation lasting 1.6s, runs 3× on load then stops. `transform-origin: 70% 70%`.

### Hero motif drift
Already documented — slow 14–22s sine drift, alternating colors and durations via nth-child to feel organic, not synced.

All animations gate on `@media (prefers-reduced-motion: reduce)` — fall back to static.

---

## Responsive behavior

- Single layout breakpoint family. Most multi-column grids collapse to 1 column around 760–860px. The hero grid stacks at ≤ 860px; the portrait moves above the text and caps at 280px wide.
- Nav links hide on narrow widths; only logo + CTA remain visible (you may want a hamburger / drawer — not yet designed; ask before adding).
- Type scales fluidly via `clamp()` throughout.

---

## Assets

### Hero portrait image (user-supplied)
The HTML prototype uses a custom `<image-slot>` web component (`image-slot.js`) that lets a user drop a photo onto the circle and persists it. **In production, do not ship the image-slot component.** Replace it with a plain `<img>` tag whose `src` is whatever final headshot the user provides. The circle clip, ring, and shadow already live on the parent `.hero__portrait-frame`.

The user is sourcing their own photo. Coordinate with them for the final headshot — square crop, head & shoulders, neutral background ideally.

### Iconography
All icons are inline SVG (Lucide-style: 24×24 viewBox, stroke 1.7–2.2, round caps/joins). No icon font, no external icon library. The inline SVGs can be lifted directly into a React `<svg>` component, or replaced with the codebase's icon library equivalents (lucide-react, heroicons, etc.) if one exists.

### Language brand badges
The Python / Swift / JavaScript / C badges in the Intro Programming list are small inline SVGs with the official brand colors. Re-use them as-is, or swap for `simple-icons` if the codebase already pulls from there.

### Fonts
Geist + Geist Mono from Google Fonts. Loaded via `<link>` in `<head>` with `preconnect` to gstatic. If the codebase uses `next/font` or similar, route through that instead.

### Math/code motif text
The hero "ornaments" (Σ, ∫, π, ∂, `f(x) = ax² + bx + c`, `{ console.log("hi") }`) are plain text spans, not images. Keep as text — they're sized via `font-size` and animated via CSS.

---

## State management

This is a static marketing page. There is **no application state**. Only:
- Scroll position (driven by browser, observed by IntersectionObserver).
- A `localStorage`-persisted image drop on the hero portrait via `image-slot.js` — drop in production once you have the real headshot.

No forms, no data fetching, no auth. The "Book a session" CTAs are `mailto:` links to `samthebuilder23@gmail.com`.

---

## SEO / `<head>`

- Page title: `Sam · Math & Code Tutor`
- Meta description: "Sam, UBC math student and iOS developer offering patient, friendly tutoring in math, statistics, and intro programming. Vancouver, online & in-person."
- `viewport` meta is set to `width=device-width, initial-scale=1.0`.
- No favicon yet (placeholder responsibility).
- Add Open Graph / Twitter card meta with the final headshot when available — not yet in the prototype.

---

## Implementation notes for the developer

1. **`<em>` is not italic.** Across this design, `<em>` is restyled to mean "accent-highlighted word" — same weight, indigo color, non-italic. Either keep this convention with a global rule, or replace `<em>` with a `<span class="hl">` primitive in your component library. Be consistent.
2. **Inline `<style>` is for the prototype only.** Move tokens into your codebase's CSS variable / Tailwind config / styled-components theme.
3. **No utility-class soup or component framework was used in the prototype** — it's hand-written BEM-ish classes (`.subject__title`, `.why__num`, etc.). Re-componentize cleanly when porting.
4. **The `.image-slots.state.json` sidecar in the project root is NOT part of the design** — it's prototype runtime state where the user's dropped image is cached. Ignore.
5. **`portfolio-system-v1.html` was an earlier exploration** and is intentionally not included in this handoff — `portfolio.html` is the canonical design.
