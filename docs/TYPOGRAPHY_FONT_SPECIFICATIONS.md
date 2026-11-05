# Typography & Font Specifications — SPACE SHOOTER ODYSSEY

## 1. Status and source boundary

The VELoop Rewards assignment specifies a premium sci-fi visual direction (deep-blue nebula, metallic materials, cyan/violet energy accents) but **does not name any font family, font file, font size, weight or line-height**. The type system below is therefore a recommended implementation specification, not a claim about an existing design asset. Confirm font licences and actual availability before shipping.

## 2. Recommended font pairing

| Role | Recommended family | Fallback stack | Use |
|---|---|---|---|
| Display / game headings | **Orbitron** | `Arial, sans-serif` | Game title, sector names, mission headings, boss labels |
| UI / body | **Inter** | `system-ui, -apple-system, "Segoe UI", sans-serif` | Navigation, forms, paragraphs, cards, help |
| Numeric / telemetry | **Inter** with tabular figures | `ui-monospace, SFMono-Regular, Consolas, monospace` | Score, timers, wallet balances, stats |

Why this pairing: Orbitron supplies a restrained futuristic display voice; Inter remains highly legible for dense dashboard and game information. Do not use the display face for long body copy. If Orbitron is too stylized at small sizes, use Inter for all UI headings and reserve Orbitron for the title and large display labels.

## 3. Font loading

Preferred approach: self-host licensed WOFF2 assets in `client/public/assets/fonts/` to reduce third-party runtime dependency and control caching. Verify the exact licence and include its notice in the repository.

Suggested file organization:

```text
client/public/assets/fonts/
├── orbitron/
│   ├── orbitron-600.woff2
│   └── orbitron-700.woff2
└── inter/
    ├── inter-400.woff2
    ├── inter-500.woff2
    ├── inter-600.woff2
    └── inter-700.woff2
```

The filenames are illustrative. Use actual downloaded font filenames and only the weights included in the chosen font package.

```css
@font-face {
  font-family: "Orbitron";
  src: url("/assets/fonts/orbitron/orbitron-600.woff2") format("woff2");
  font-style: normal;
  font-weight: 600;
  font-display: swap;
}

@font-face {
  font-family: "Orbitron";
  src: url("/assets/fonts/orbitron/orbitron-700.woff2") format("woff2");
  font-style: normal;
  font-weight: 700;
  font-display: swap;
}

@font-face {
  font-family: "Inter";
  src: url("/assets/fonts/inter/inter-400.woff2") format("woff2");
  font-style: normal;
  font-weight: 400;
  font-display: swap;
}

@font-face {
  font-family: "Inter";
  src: url("/assets/fonts/inter/inter-500.woff2") format("woff2");
  font-style: normal;
  font-weight: 500;
  font-display: swap;
}

@font-face {
  font-family: "Inter";
  src: url("/assets/fonts/inter/inter-600.woff2") format("woff2");
  font-style: normal;
  font-weight: 600;
  font-display: swap;
}

@font-face {
  font-family: "Inter";
  src: url("/assets/fonts/inter/inter-700.woff2") format("woff2");
  font-style: normal;
  font-weight: 700;
  font-display: swap;
}
```

Use `font-display: swap`. Preload only the most important above-the-fold regular UI and display weights; do not preload every font file. If using a variable font, define its supported weight range correctly.

## 4. Type scale (proposed)

Use `rem` so browser zoom and user font settings remain effective.

| Token | Desktop size | Mobile size | Weight | Line height | Usage |
|---|---:|---:|---:|---:|---|
| `display-xl` | 48px | 36px | 700 | 1.1 | Landing/game title |
| `display-lg` | 36px | 30px | 700 | 1.15 | Sector / major page heading |
| `heading-1` | 28px | 24px | 700 | 1.2 | Page section |
| `heading-2` | 22px | 20px | 600 | 1.25 | Card/dialog heading |
| `heading-3` | 18px | 18px | 600 | 1.3 | Subsection |
| `body-lg` | 18px | 17px | 400 | 1.55 | Intro / key explanatory copy |
| `body` | 16px | 16px | 400 | 1.5 | Standard UI/body |
| `body-sm` | 14px | 14px | 400 | 1.45 | Secondary card copy |
| `label` | 12px | 12px | 600 | 1.35 | Compact metadata |
| `overline` | 11px | 11px | 600 | 1.3 | Sector/status labels |
| `numeric-lg` | 24px | 22px | 700 | 1.15 | Wallet/score values |

Do not use 11–12px for essential instructions, critical economy details or error messages. On mobile, keep touch-target labels readable.

## 5. Weight and letter spacing

- 400: body text and descriptions.
- 500: navigation, form values and secondary buttons.
- 600: card titles, labels and primary controls.
- 700: page headings, major numbers and title.
- Orbitron: 600/700 for large headings only.
- Body tracking: normal (`0`).
- Display tracking: approximately `0.02em` to `0.06em`, depending on size.
- Overline tracking: `0.08em` to `0.12em`; avoid extended tracking in long words or small mobile widths.

## 6. Numeric and currency typography

Use tabular numerals to prevent dashboard layout shifting as values update:

```css
.numeric,
.wallet-value,
.score-value,
.timer-value {
  font-variant-numeric: tabular-nums lining-nums;
}
```

Always display the currency name or recognizable icon with a text label. Do not rely on color alone to distinguish Credits, Energy Cores and VELoop Reward Coins. XP should be labelled as progression rather than wallet currency.

## 7. CSS typography tokens

```css
:root {
  --font-display: "Orbitron", "Arial", sans-serif;
  --font-ui: "Inter", system-ui, -apple-system, "Segoe UI", sans-serif;

  --text-display-xl: 3rem;
  --text-display-lg: 2.25rem;
  --text-h1: 1.75rem;
  --text-h2: 1.375rem;
  --text-h3: 1.125rem;
  --text-body-lg: 1.125rem;
  --text-body: 1rem;
  --text-body-sm: 0.875rem;
  --text-label: 0.75rem;
  --text-overline: 0.6875rem;

  --line-display: 1.1;
  --line-heading: 1.2;
  --line-body: 1.5;
}

body {
  font-family: var(--font-ui);
  font-size: var(--text-body);
  line-height: var(--line-body);
}

h1, h2, .display-heading {
  font-family: var(--font-display);
  font-weight: 700;
  line-height: var(--line-heading);
}
```

## 8. Accessibility and localization

- Maintain adequate text/background contrast; validate actual rendered combinations.
- Do not communicate status only through type weight, color or uppercase.
- Support browser zoom and text resizing without clipping dialogs or HUD labels.
- Avoid long all-caps passages; screen readers and readability both benefit from sentence case.
- Ensure fallback fonts do not break layout if web fonts fail.
- Test names, currency labels and longer translated strings before locking widths.
- Keep line length comfortable for help/documentation copy; use shorter lines for dense dashboard panels.

## 9. Verification checklist

- [ ] Font files and licences are present in repository.
- [ ] All referenced font URLs resolve in Vite production build.
- [ ] Fallback stacks render acceptably with fonts blocked.
- [ ] Display font is limited to display use.
- [ ] Wallet, score, XP and timer values use tabular numerals.
- [ ] Mobile type remains readable at 320px viewport.
- [ ] Focus, error, disabled and selected states remain legible.
- [ ] Zoom/reflow does not clip text or controls.
