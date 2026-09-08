# Hooker & Millions — playable local game prototype

## Goal
Build a desktop-first, frontend-only wealth and management game prototype named “Hooker & Millions”. The existing TanStack Start/React shell will remain only as the supported screen host; all game rules, data, persistence, and calculations will live in browser-safe TypeScript modules with no backend, database, authentication, API calls, or cloud dependency.

## Player-facing result
- A simple test dashboard showing day, cash, bank balance, net worth, reputation, lifestyle, income, and expenses.
- Tabs/sections for Characters, Businesses, Stocks, Investments, Properties, Assets, Events, transaction history, and save tools.
- Working purchase, upgrade, deposit/withdraw, buy/sell, investment, day-advance, random-event, save/load/export/import/reset, and debug controls.
- Explicitly adult fictional characters only; no relationship, romance, dialogue, or explicit content systems.
- Placeholder local image paths that remain valid when the user replaces files later.

## Implementation steps
1. **Core state and data contracts**
   - Create one normalized game state with the requested fields plus economy summaries, market condition, and IDs/records needed for purchases and ongoing obligations.
   - Add typed, data-driven collections for characters, businesses, stocks, investments, properties, assets, locations, events, and lifestyle levels.
   - Seed a small but playable catalog that demonstrates locked/available/owned content, recurring costs, varied stock risk, locked-term investments, and lifestyle progression.

2. **Game engine modules**
   - Implement economy functions as the only path for cash and bank changes, including validation, balance-after transaction records, income/expense summaries, and net-worth calculation.
   - Implement character acquisition, business purchase/upgrade/income, property and asset ownership/maintenance, reputation changes, lifestyle unlocks/downgrades, investments, and stock portfolio accounting.
   - Implement one central `advanceDay()` pipeline: recurring business income, operating/maintenance/daily expenses, investment updates, controlled market movement, random events, temporary modifier expiry, lifestyle sustainability, day increment, and automatic save.
   - Implement reusable event resolution and modifier handling from event data, including market/sector/company, business, expense, money, reputation, and unlock effects.

3. **Stocks and difficulty controls**
   - Add fictional market conditions (Bull, Normal, Bear, Boom, Crash) with forced debug overrides.
   - Calculate prices from prior price plus market, sector, company, volatility, and bounded noise components; clamp prices and prevent invalid portfolio values.
   - Enforce all spending, selling, duplicate ownership, non-negative share, upgrade, and investment duration rules.

4. **Local persistence and content expansion**
   - Add localStorage save/load/reset plus JSON export/import with validation and safe fallback to a fresh state.
   - Keep content in separate data modules so adding an image and one object automatically exposes new content without engine changes.
   - Keep asset references local and create placeholder directory conventions under `public/assets/` for characters, properties, businesses, locations, videos, and audio.

5. **Test UI and verification**
   - Replace the blank index screen with a utilitarian desktop-first dashboard and responsive fallback, using the existing design tokens rather than visual polish work.
   - Add clear action feedback and recent transaction/event visibility so mechanics can be checked while playing.
   - Add a marked DEBUG panel for advancing days, money adjustments, market forcing, event triggering, and reset.
   - Add route metadata for the game page and verify the preview, build diagnostics, core interactions, persistence flow, and that no network/backend integration is introduced.

## Technical details
- Keep the TanStack Start route structure and existing React shell; do not introduce another router or a backend.
- Use small browser-safe TypeScript modules under `src/game/` and `src/game/data/`, with the screen consuming a single game-state store/hook.
- Use `localStorage` only for persistence and browser file APIs only for import/export.
- Use no external images, APIs, services, accounts, or runtime network calls for game logic.
