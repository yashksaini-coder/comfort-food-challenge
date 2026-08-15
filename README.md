# Gravy Theory — three chickens, one base

An interactive field guide to North Indian gravy, arguing one thing: **butter chicken and chicken
curry are not different recipes.** They are the same onion–tomato masala, stopped at different
moments and finished in different directions. Chilli chicken never touches it at all.

Built for the [DEV Frontend Challenge — Comfort Food Edition](https://dev.to/challenges/frontend-2026-07-29)
(*Perfect Landing* prompt).

**[→ Live demo](https://yashksaini-coder.github.io/comfort-food-challenge/)**

---

## The constraint

One HTML file. **Zero image requests.**

Every pan, thali, katori, roti, chilli, spice tin and ingredient on the page is drawn in CSS
gradients and inline SVG. There is no build step, no framework, no bundler, no icon font, no CDN,
and no tracking. The only external request is Google Fonts.

```
index.html    ~146 KB    everything
```

Open it in a browser. That's the whole setup.

## What's in it

| Section | What it does |
|---|---|
| **The base** | A dial that cooks the masala from raw to done. The gravy colour interpolates in OKLCH; six ingredients light up as you pass their stage. |
| **The split** | Three dishes, tabbed, each showing what it adds on top of the shared base. |
| **The fork** | The signature scene. One pan splits into two along drawn curves while a wok slides in from the right and *stops short* — it never joins. |
| **The clock** | Where each dish spends its time. Butter chicken is the only one needing two burners. |
| **Green chilli** | Heat plotted against aroma on a log scale. The Indian green chilli sits where nothing else does. |
| **The dabba** | Seven tins, seven jobs — and what breaks when each is missing. |
| **Tonight** | Three questions. It's a constraint problem, not a taste problem. |

## Technique notes

A few things worth pointing at:

- **Food is three optical layers, not one gradient.** An opaque pigmented base, a *wide, blurry,
  coloured* subsurface glow, and a *small, hard, warm-white* specular glint. Collapsing the last
  two into one soft blob is what makes CSS food read as a pie chart.
- **One light source** (upper right, `--lx: 78%; --ly: 18%`) for every highlight and shadow on the
  page. Mismatched light direction is the biggest tell that something was drawn rather than lit.
- **Four SVG filters**, defined once and reused: a turbulence displacement for ragged gravy edges,
  a goo filter so cream dollops fuse instead of stacking, a thresholded-noise char for tandoori
  blistering, and a static wisp displacement for steam. None of them animate their own
  parameters — that regenerates Perlin noise on the CPU every frame.
- **Registered custom properties** (`@property --f`, `--gravy`) so the dial's colour ramp actually
  interpolates instead of stepping.
- **An 18-symbol ingredient sprite** instanced with `<use>`, sized from one 48×48 box so everything
  sits on the same optical scale.

## Accessibility

- WCAG 2.1 AA contrast verified across every text/background pair, in both the default and
  "dim the lights" palettes.
- The chilli scatter and the masala dabba are **radio groups**, not sets of toggle buttons — one
  tab stop each, arrow-key navigation, selection follows focus.
- A **Pause motion** control in the masthead stops every looping animation (WCAG 2.2.2), and
  `prefers-reduced-motion` is honoured including animation *delays*.
- Every section carries an accessible name for landmark navigation.
- **Fully readable with JavaScript switched off** — the tabs become stacked panels and the two
  interactive charts fall back to static lists. Nothing is hidden behind JS.

## Licence

[MIT](LICENSE).
