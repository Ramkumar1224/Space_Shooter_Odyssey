# Design System — SPACE SHOOTER ODYSSEY

## 1. Design direction

**Visual direction:** premium sci-fi arcade interface. The assignment describes original 3D sci-fi artwork, deep-blue nebula environments, metallic materials, cyan and violet energy accents, luminous asteroids, stars and cinematic lighting. Treat this as the visual foundation, not a copied reference-game skin.

The PDF does **not** specify exact hex values or a component library. The palette and component tokens below are an implementation proposal derived from its deep-blue/cyan/violet art direction. Validate contrast and tune values during UI implementation.

## 2. Experience principles

1. **Combat clarity first:** enemy projectiles, player health, boss telegraphs and objectives must remain readable.
2. **Strong hierarchy:** primary action (Play/Continue, Start Mission, Claim) stands out; secondary navigation is quieter.
3. **Game-like, not a poster:** home screen combines animated cosmic background and ship hero artwork with real interactive dashboard controls.
4. **Consistent economy display:** Credits, Energy Cores, XP and VELoop Reward Coins use distinct labels/icons and never imply interchangeable value.
5. **Reward transparency:** show base reward, optional ad bonus, limits/eligibility and clear decline action.
6. **Responsive by design:** dashboard and hangar adapt to narrow screens; gameplay controls remain reachable.
7. **Original assets:** do not use the reference game's logos, ships, enemies, layouts, audio or screenshots.

## 3. Color tokens (proposed)

| Token | Hex | Intended use |
|---|---|---|
| `--space-950` | `#070B18` | Main app background |
| `--space-900` | `#0B1024` | Deep panel/background |
| `--space-800` | `#121B35` | Elevated cards |
| `--space-700` | `#1B2A4A` | Borders/secondary surfaces |
| `--nebula-blue` | `#2457A6` | Main blue accent |
| `--energy-cyan` | `#43D9F2` | Primary interactive accent |
| `--plasma-violet` | `#9A7BFF` | Secondary accent / rare effects |
| `--ion-magenta` | `#D66BFF` | Event / special accent |
| `--success` | `#55D6A2` | Completed / success |
| `--warning` | `#FFBE62` | Caution / limited resource |
| `--danger` | `#FF647C` | Damage / destructive action |
| `--text-primary` | `#F4F7FF` | Main text |
| `--text-secondary` | `#AAB6D0` | Secondary text |
| `--text-muted` | `#71809F` | Disabled/helper text |
| `--border-subtle` | `#283653` | Quiet borders |

Use dark backgrounds with restrained luminous accents. Do not apply cyan/violet glow to every surface; preserve accent meaning and avoid visual noise. Check WCAG contrast for text and controls, especially muted labels over dark panels.

## 4. Typography usage

Font families are not prescribed by the assignment. See `TYPOGRAPHY_FONT_SPECIFICATIONS.md` for proposed families, hierarchy, weights and loading rules.

- Display face: game title, sector title, boss/mission callouts.
- UI sans: navigation, body, form labels, buttons and help.
- Numeric/tabular style: wallet balances, XP, timers, score and stats.
- Use uppercase selectively for compact sci-fi labels; body copy remains sentence case.
- Avoid overly wide tracking in long paragraphs.

## 5. Layout and spacing

Use a 4px base spacing unit. Suggested scale:

| Token | Value |
|---|---:|
| `space-1` | 4px |
| `space-2` | 8px |
| `space-3` | 12px |
| `space-4` | 16px |
| `space-5` | 20px |
| `space-6` | 24px |
| `space-8` | 32px |
| `space-10` | 40px |
| `space-12` | 48px |
| `space-16` | 64px |

Use a centered content container with a practical maximum width (proposed 1440px), fluid side padding and responsive grid. Keep critical wallet/player status visible without forcing every feature onto the first viewport.

## 6. Shape, border and elevation

- Cards: 12–16px radius.
- Buttons and inputs: 8–12px radius.
- Pill status indicators: fully rounded.
- Borders: 1px subtle border; stronger accent border only for selected/focused states.
- Elevation: layered dark surfaces and restrained shadow; avoid excessive neon glow.
- Dialogs: clear title, concise explanation, one primary action and explicit secondary/close action.

## 7. Core components

### Navigation and shell
- Persistent game identity and primary navigation.
- Player summary/wallet strip in dashboard contexts.
- Active route has a visible state, not color alone.
- Admin navigation is separate and only rendered for authorized admins.

### Buttons
- Primary: high-contrast cyan/blue treatment; used for the main next action.
- Secondary: dark surface with visible border.
- Tertiary: text/quiet action.
- Destructive: danger treatment and confirmation for irreversible actions.
- Disabled: reduced emphasis plus explanatory reason where useful.
- Loading state prevents duplicate submission.

### Cards
- Mission card: sector, sequence, difficulty, status, best result and unlock reason.
- Ship card: artwork, class, ownership/lock, key stats and selected state.
- Power-up card: effect, duration/cooldown and remaining quantity.
- Reward card: source, amount, currency, eligibility and claim state.
- Achievement card: badge, criteria, progress and claim status.

### Data display
- XP bar includes current/next-level values.
- Wallet values show currency label and consistent icon.
- Health/shield indicators are high visibility during combat.
- Boss bar is visually distinct and does not obscure the play area.
- Leaderboard shows rank, display name, score and tie-break context.

### Forms and dialogs
- Labels always visible; validation messages near fields.
- Auth forms return useful errors without leaking account/security details.
- Confirm purchases with item, price, currency and resulting effect.
- Revive dialog shows remaining revive eligibility and a non-ad alternative.

## 8. Screen composition

### Home / player dashboard
- Animated cosmic background with original spaceship hero art.
- Player level and XP progress.
- Selected ship preview.
- Credits, Energy Cores and eligible VELoop Reward Coins shown separately.
- Primary Play/Continue Mission action.
- Campaign/sector shortcut.
- Navigation/cards for Hangar, Power-Ups, Daily Missions, Daily Rewards, Achievements, Leaderboard, Reward Center and Settings.

### Campaign
- Sector selector with distinct original visual identity.
- Mission list with locked/available/completed/replay states.
- Mission preparation with selected ship, objective list and start action.

### Gameplay
- Phaser canvas is the dominant region.
- HUD: health, shield, score, objective progress, wave and boss health.
- Pause and power-up controls remain accessible.
- Do not let particles, screen shake or overlays hide hostile projectiles.

### Result / failure
- Mission result, score/statistics, stars, standard rewards and unlocks.
- Optional ad bonus is separate and clearly optional.
- Failure screen: Watch Ad & Revive (if eligible), Restart, Return to Hangar.

### Hangar and inventory
- Strong ship/power-up artwork; readable stat comparisons.
- Show upgrade level, cost and maximum level.
- Purchase confirmation precedes spending.

### Wallet / reward centre
- Currency balance separated by type.
- Transaction and reward history with source, amount, status and time.
- Distinguish ordinary game currencies from platform-eligible rewards.

### Admin
- Separate layout and authorization.
- Filters for opportunities, verified/completed/failed/rejected ads, reward grants, Credits in/out and user-level audit.
- Analytics charts must be computed from event/ledger data.

## 9. Interaction and motion

Required feedback includes ship movement, firing, impacts, enemy destruction, boss attacks, shield activation, power-up activation, pickup collection, mission completion, reward grants, level-up and ship upgrade/selection.

- Use short purposeful transitions; avoid motion that delays critical actions.
- Boss powerful attacks should be telegraphed.
- Use screen shake/particles sparingly.
- Respect `prefers-reduced-motion`; provide reduced particle/transition intensity.
- Handle focus states and keyboard navigation for menus/dialogs.
- Do not play audio before a user gesture if blocked by browser autoplay policy.

## 10. Responsive behavior (proposed breakpoints)

| Breakpoint | Width | Layout guidance |
|---|---:|---|
| Small mobile | < 480px | Single-column cards; compact resource strip; touch-first |
| Mobile/tablet | 480–767px | Two-column card grids where space permits |
| Tablet/desktop | 768–1199px | Collapsible navigation; 2–3 column dashboard |
| Wide desktop | >= 1200px | Full navigation and multi-column dashboard |

These are suggested CSS breakpoints, not source-mandated values. Test real device sizes and landscape gameplay. Reserve canvas dimensions to avoid layout shifts.

## 11. CSS token starter

```css
:root {
  color-scheme: dark;
  --space-950: #070B18;
  --space-900: #0B1024;
  --space-800: #121B35;
  --space-700: #1B2A4A;
  --nebula-blue: #2457A6;
  --energy-cyan: #43D9F2;
  --plasma-violet: #9A7BFF;
  --ion-magenta: #D66BFF;
  --success: #55D6A2;
  --warning: #FFBE62;
  --danger: #FF647C;
  --text-primary: #F4F7FF;
  --text-secondary: #AAB6D0;
  --text-muted: #71809F;
  --border-subtle: #283653;
  --radius-card: 14px;
  --radius-control: 10px;
  --content-max: 1440px;
}
```

## 12. Asset direction and optimization

Generate original player ships, enemy ships, bosses, sector/planet backgrounds, mission thumbnails, power-up icons and hangar artwork separately from UI. Artwork should not contain generated buttons, labels or interface screenshots. Compress images, prefer WebP/AVIF where appropriate, create mobile/desktop variants, lazy-load noncritical art, reserve dimensions and separate foreground/background layers where animation benefits. Use original or appropriately licensed audio.
