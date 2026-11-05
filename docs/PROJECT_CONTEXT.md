# Project Context — SPACE SHOOTER ODYSSEY

## 1. Purpose and product definition

SPACE SHOOTER ODYSSEY is an original full-stack browser arcade shooter and gamified rewards experience. It is intended to combine responsive 2D combat, structured campaign progression, a player fleet and upgrade economy, engagement systems, and carefully verified optional rewarded advertisements.

The uploaded VELoop Rewards assignment defines the product objective and mandatory quality bar. The user's supplied app flow defines the intended navigation modules and additional dashboard/reward/admin presentation. The selected stack is React + Vite + JavaScript, Phaser 3, CSS3, Java + Spring Boot, REST, Spring Security + JWT, PostgreSQL (Supabase), Spring Data JPA/Hibernate, Maven, Postman, Git/GitHub, Vercel and Render.

## 2. Product goals

1. Deliver actual playable combat, not a static visual prototype.
2. Deliver five original sectors, at least 50 data-driven playable missions and at least five boss encounters.
3. Provide five differentiated ship classes and meaningful upgrade attributes.
4. Implement eight power-ups with real effects, durations, cooldowns/uses and stacking rules.
5. Persist player profile, progress, mission history, ship state, inventory, wallet and engagement claims.
6. Operate a controlled economy with auditable, atomic and idempotent transactions.
7. Offer optional rewarded ads at meaningful moments without interrupting core combat.
8. Provide admin-only economy controls, audit and analytics.
9. Support responsive desktop and mobile play and persisted audio preferences.

## 3. Audience and roles

### Player

Can register, authenticate, complete onboarding, play eligible missions, upgrade owned ships, acquire/use power-ups, claim eligible rewards, review history and manage preferences.

### Administrator

Uses a separate protected branch. Can inspect economy/ad activity, audit transactions, manage approved economy settings and view metrics. Admin role enforcement is server-side.

## 4. Functional scope

### Authentication and onboarding

- Registration, login, logout and current-user retrieval.
- JWT-backed authentication with Spring Security.
- Protected player routes and role-protected admin routes.
- First-time onboarding to establish player profile, starter ship and initial progression state.
- Password hashing and server-side input validation.

### Dashboard

Display level/XP progress, selected ship, Credits, Energy Cores, eligible VELoop Reward Coins, primary Play/Continue action, campaign/sector shortcut, hangar, power-up collection, daily missions/rewards, achievements, leaderboard, reward centre and settings.

Dashboard values must come from persisted API data or be explicitly marked as demo data.

### Campaign and missions

Sectors: Orion Frontier, Crimson Nebula, Frozen Expanse, Rift Territory and Void Citadel. Missions support locked, available, completed and replay states. Preparation selects an eligible ship and reviews objectives. Gameplay supports movement/firing, enemy waves, pickups, power-ups, bosses, objective tracking, pause/resume/restart/abandon. Outcome includes result, score/statistics, stars, standard rewards, optional ad bonuses and next-mission eligibility.

Mission definitions are data-driven, not one hardcoded React page per mission. Each definition supports waves, enemy composition, spawn configuration, objective, boss, difficulty, modifiers, completion rules, rewards, star criteria and unlock requirements.

### Failure and revive

On defeat, show Mission Failed and the choices Watch Ad & Revive, Restart Mission or Return to Hangar. Revive is limited (example default: one per mission), tied to a valid checkpoint and game session, and granted only after trusted ad verification and backend eligibility checks.

### Fleet and upgrades

At least five ship classes. Hangar shows owned/locked ships, attributes, unlock conditions and selection. Upgrade attributes: weapon damage, firing rate, health, movement speed, shield capacity, special-ability cooldown and relevant projectile characteristics. Purchases must use server-controlled pricing and atomic currency deduction.

### Power-ups and inventory

Required: Shield Pulse, Rapid Fire, Spread Shot, Homing Missiles, EMP Blast, Repair Drone, Overdrive and Emergency Warp. Inventory must expose effects, remaining uses and cooldowns. Configuration centralizes duration, cooldown, max uses, unlock/acquisition, cost, ad eligibility and stacking behavior.

### Wallet and engagement

Wallet tracks Credits, Energy Cores, XP and separate VELoop Reward Coins. XP is progression, not spendable currency. Include wallet and reward history, daily missions, login streak, achievements, mission streaks, supply drops, limited-time event and leaderboard. All claims are server validated and duplicate protected.

### Rewarded ads

Placements: revive, double score, double Credits, extra shield/power-up, additional mission reward and daily bonus. Opportunity state: OFFERED, REQUESTED, AD_STARTED, AD_COMPLETED, VERIFYING, VERIFIED, GRANTED, REJECTED or EXPIRED. A provider adapter isolates the selected ad network; local simulated adapter is clearly labelled and not production verification.

### Profile and history

Persist profile, statistics, mission history, best scores, selected/unlocked ships, upgrades, wallet, inventory, achievements and progress.

### Settings and help

Separate background music, sound effects and master volume controls. Persist supported audio preferences. Provide gameplay instructions/help pages. Handle browser autoplay restrictions and start audio after user interaction.

### Admin and analytics

Admin authentication/authorization, economy configuration, reward limits/ad settings, reward audit, ad metrics, Credits granted/spent, conversion rates and engagement analytics. Metrics must derive from recorded events rather than fabricated counters.

## 5. Non-functional requirements

- **Security:** secure password hashes, JWT verification, role checks, DTO validation, session ownership, rate limits, secrets management.
- **Consistency:** atomic purchases/rewards, unique transaction/event identifiers, no negative balances.
- **Reliability:** persistent progress; refresh must not erase legitimate progress; explicit session/ad state machines.
- **Performance:** Phaser object pooling/collision groups where appropriate; control projectile and spawn rates; optimize assets for lower-powered mobile devices.
- **Responsive UX:** desktop keyboard and mobile touch controls; layouts adapt to viewport.
- **Accessibility:** keyboard focus handling for menus/dialogs; readable contrast; reduced-motion support where appropriate.
- **Maintainability:** centralized config, reusable game entities, data-driven mission content, separation of UI/game/API/business layers.
- **Observability:** structured analytics and audit events with minimal necessary data.

## 6. Architecture decisions

### Frontend

React owns route transitions and application screens. Vite handles development/build. Phaser is mounted within a dedicated React game host component; it owns the real-time canvas, update loop, input, entities, physics/collisions and scene lifecycle. React overlays may render pause, HUD adjuncts, failure, result and revive dialogs using a typed/event-based bridge. Avoid two competing sources of truth for combat state.

Suggested frontend layers:
- `app`: router, route guards, providers
- `pages`: route screens
- `components`: reusable UI
- `game` / `scenes` / `entities`: Phaser runtime
- `data`: content definitions
- `services`: API client, auth and ad adapter
- `config`: title, API and economy display configuration
- `styles`: CSS variables, global styles and component styles

### Backend

Spring Boot exposes versioned REST APIs. Controllers map HTTP requests to validated DTOs; services enforce business rules; repositories encapsulate JPA persistence. Spring Security validates JWT and role access. `@Transactional` boundaries protect multi-row purchases, wallet changes and reward grants. Database uniqueness constraints reinforce idempotency.

### Persistence

PostgreSQL on Supabase is authoritative for user identity, profile, progression, inventory, sessions, wallet ledger, reward/ad state and analytics. Use Flyway or Liquibase migrations (implementation choice) rather than relying on automatic schema mutation in production. See `DATABASE_SCHEMA.md`.

### Deployment

Vercel hosts the Vite frontend; Render hosts the Spring Boot API; Supabase provides PostgreSQL. Use environment variables, HTTPS, explicit CORS origins, production migrations and health checks.

## 7. Important trust boundaries

| Data/action | Authority |
|---|---|
| UI navigation and local display state | React |
| Real-time rendering and immediate combat simulation | Phaser client |
| Player identity and roles | Spring Security/backend |
| Wallet balance and ledger | Backend/PostgreSQL |
| Ship ownership, prices and upgrades | Backend/PostgreSQL |
| Mission unlocks and persistent progress | Backend/PostgreSQL |
| Reward amount, caps and eligibility | Backend/PostgreSQL |
| Ad completion proof | Ad provider's trusted verification path/backend |
| Leaderboard acceptance | Backend validation |
| Admin configuration | Backend with admin role and audit |

Do not trust client-supplied `userId`, balance, price, reward amount, score multiplier, ad completion or unlock status. For browser-simulated combat, validate session, mission rules, duration, score bounds, enemy counts, boss completion and power-up usage. This reduces abuse but is not equivalent to a server-authoritative simulation.

## 8. Product data and content targets

| Content | Target from assignment |
|---|---:|
| Sectors | 5 |
| Playable missions | At least 50 |
| Boss encounters | At least 5 |
| Ship classes | At least 5 |
| Required power-ups | 8 |
| Daily mission templates | At least 3 |
| Achievements | At least 10 |
| Functional limited-time event | At least 1 |

## 9. Out of scope / not assumed

- No exact final UI wireframes, production palette values or font families are prescribed in the PDF.
- No final production reward rates or advertising payout assumptions are supplied.
- VELoop Reward Coins are not automatically cash-equivalent; use actual platform eligibility rules.
- Weekly/monthly leaderboards, procedural missions, cosmetics, offline mode, friend leaderboards, PWA and A/B testing are optional extensions.
- Do not claim that simulated ads are a real ad integration.

## 10. Open implementation decisions

Resolve and record these in the repository before release:
- Exact Java and Spring Boot versions.
- JWT transport and refresh-token strategy.
- Migration tool and naming convention.
- Ad provider and its server-side verification protocol.
- Mission-result integrity strategy for client-simulated combat.
- Final currency prices, caps, cooldowns, time zone and daily reset policy.
- Final UI color values, font assets/licences and responsive breakpoints.
