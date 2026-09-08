# Hooker & Millions — frontend-only playable game

## Goal
Build a desktop-first browser game called “Hooker & Millions”: a fictional 18+ adult-themed wealth and management game with non-explicit content. Keep characters clearly fictional adults aged 18+, and implement the character catalogue as an acquisition/collection system only—no explicit sexual content, romance, relationships, or dialogue.

The existing TanStack Start/React shell stays in place because it is the supported project runtime, but the game itself remains frontend-only: browser-side TypeScript/JavaScript modules, local data, local media paths, and localStorage. No backend, database, authentication, account system, API, cloud service, or server-side game logic will be added.

## Core player experience
- Start with limited cash and progress through jobs, businesses, investments, stocks, properties, and luxury assets.
- Use a dedicated Purchase/Acquire screen to browse, filter, compare, unlock, and acquire fictional adult characters.
- Advance days to run the full economy loop, make risk/reward decisions, increase lifestyle and reputation, and work toward wealth.
- Save, load, export, import, or reset the game entirely in the local browser.

## Implementation plan

### 1. Central state and data-driven content
- Create one central game state containing cash, bank balance, net worth, reputation, lifestyle, current day, owned IDs, stock portfolio, investments, active modifiers, transaction history, event history, and daily income/expense summaries.
- Create separate local data modules for characters, countries, categories, businesses, stocks, investments, properties, assets, locations, events, and lifestyle levels.
- Keep UI rendering generic: adding one data object and a local asset path makes new content appear without changing engine or card code.
- Add placeholder paths under `public/assets/characters`, `businesses`, `properties`, `locations`, `videos`, and `audio`; do not generate final artwork.

### 2. Economy and progression engine
- Route every cash and bank change through a centralized economy module with validation, transaction recording, balance-after values, income/expense totals, deposits, withdrawals, and net-worth calculation.
- Implement jobs as small reliable income sources, plus businesses, investments, the stock market, properties, and luxury assets as progressively larger and riskier wealth systems.
- Implement business purchase, recurring income, operating costs, upgrades, escalating costs, unlock requirements, and duplicate/invalid-spend protection.
- Implement properties and assets with purchase costs, maintenance, lifestyle bonuses, reputation bonuses, ownership checks, and recurring obligations.
- Implement reputation changes from wealth milestones, lifestyle, businesses, investments, assets, and events.
- Implement Low, Comfortable, Wealthy, Millionaire, and Elite lifestyles with net-worth/access requirements, daily maintenance, reputation effects, unlock lists, and sensible downgrades when unsustainable.

### 3. Time, stock market, investments, and events
- Make one `advanceDay()` pipeline responsible for business income, all expenses, investment updates, stock movement, random events, temporary modifier expiry, lifestyle sustainability, day increment, and automatic save.
- Add fictional stocks across Technology, Finance, Energy, Real Estate, Retail, and Entertainment with volatility, risk, and market sensitivity.
- Track shares, average purchase price, current value, and profit/loss; support buy, sell, and hold while preventing negative shares, selling unowned shares, invalid prices, and insufficient funds.
- Model Bull, Normal, Bear, Boom, and Crash market conditions. Price changes combine prior price, market, sector, company, volatility, and bounded random noise so stocks differ and no guaranteed profit pattern exists.
- Add Safe, Medium Risk, High Risk, Real Estate, and Locked-Term investments with minimum capital, uncertain returns, risk, duration, liquidity, and locked funds where applicable.
- Add a reusable data-driven event resolver affecting money, business income/expenses, stocks, sectors, investments, reputation, unlocks, and temporary modifiers. Include market boom/crash, sector shocks, company success/scandal, energy shortage, banking crisis, and real-estate events.

### 4. Character acquisition catalogue
- Ensure every character is 18+ and supports name, age, country, category, tier, rarity, price, image, availability, unlock requirements, optional non-explicit description, and optional local video.
- Support locked, available, and owned states with checks for existence, age, requirements, cash, duplicates, and safe transaction recording.
- Build the Purchase/Acquire screen with search, country/category/tier/price/rarity filters, price/tier/stat sorting, placeholder image, requirements, price, and owned/locked/available status.
- Keep character mechanics strictly catalogue-based; do not add relationship, romance, dialogue, or explicit systems.

### 5. Local save and debug tools
- Implement `saveGame()`, `loadGame()`, `resetGame()`, `exportSave()`, and `importSave()` using localStorage and browser file APIs, with validation and safe recovery from malformed data.
- Persist all important state: money, bank, day, reputation, lifestyle, ownership, portfolio, investments, modifiers, events, and transactions.
- Add a clearly marked DEBUG area with advance day, add/remove money, force Bull/Bear/Crash, trigger event, reset, and full current-state inspection.

### 6. Styled playable screens
- Replace the blank home screen with a working game shell and separate views for Dashboard, Purchase/Acquisition, Businesses, Stock Market, Investments, Properties, Assets, Events, Transactions, and Save.
- Prioritize mechanics and clarity while applying the requested distinctive luxury aesthetic: deep glittery pink/deep magenta, burgundy, black, dark purple, silver/white highlights, subtle particles, glowing borders, glass panels, shadows, gradients, hover animation, and smooth transitions.
- Keep the experience desktop-first with a usable smaller-screen fallback; avoid a generic SaaS dashboard and do not turn the page into a static marketing mockup.

## Verification
- Confirm the blank placeholder is removed and the main game is playable from `/`.
- Exercise purchases, upgrades, stock buy/sell, locked investments, day advancement, events, lifestyle changes, duplicate protection, and save/load/export/import/reset.
- Check browser console/runtime/build diagnostics and verify that the game introduces no backend, database, auth, API, cloud, external image, or network dependency.
- Verify new data entries render automatically and all content uses local asset paths.
