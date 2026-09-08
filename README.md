# Fortune Foundry

Build a desktop-first browser game called “Hooker & Millions”.

This is a fictional 18+ adult-themed wealth and management game. Keep all characters explicitly 18+ and keep the implementation non-explicit.

ABSOLUTE TECHNICAL REQUIREMENT

This project is FRONTEND ONLY.

Use ONLY:

HTML5

CSS3

Vanilla JavaScript

Local JSON / JavaScript data files

Browser localStorage

Local image, video, and audio assets

DO NOT use or create:

Any backend

Any server

Any database

Any API

Any REST API

Any GraphQL

Any authentication

Any user accounts

Any login system

Any cloud service

Firebase

Supabase

WordPress

PHP

Node.js backend

Express

React

Next.js

Vue

Angular

CMS

External game engine

External data storage

There must be no network dependency for the game logic.

The game must run locally in a browser using its own local files.

PRIMARY GOAL

Build the actual client-side game mechanics, not a fancy website.

Do NOT spend significant effort on visual design.

Create only a simple test UI so the mechanics can be played and verified.

Priority:

Game State → Economy → Time → Businesses → Stocks → Investments → Characters → Properties → Assets → Lifestyle → Events → Save/Load

The game should be modular, expandable, and easy to modify later.

1. CENTRAL GAME STATE

Create one centralized game state object.

It should contain at least:

{
    player: {
        cash: 10000,
        bankBalance: 0,
        reputation: 0,
        lifestyle: "low"
    },

    currentDay: 1,

    ownedCharacters: [],
    ownedBusinesses: [],
    ownedProperties: [],
    ownedAssets: [],

    stockPortfolio: [],
    investments: [],

    activeModifiers: [],
    eventHistory: [],
    transactionHistory: []
}


This state is the single source of truth.

Do not duplicate important values in multiple places.

2. DATA-DRIVEN CONTENT

All game content must be separated from game logic.

Create local data files/modules for:

characters
businesses
stocks
investments
properties
assets
locations
events
lifestyleLevels


The engine must automatically read these data collections.

I should NOT have to modify the game engine whenever I add new content.

3. ADDING NEW CONTENT

Make the system extremely easy to expand.

New character

I should only need:

1. Put an image into assets/characters/
2. Add one character object to the character data file


Example:

{
    id: "char_001",
    name: "Example Character",
    age: 24,
    country: "Example Country",
    category: "Premium",
    tier: 3,
    price: 5000,
    rarity: "Rare",
    image: "assets/characters/char_001.webp",
    unlockRequirement: {
        reputation: 20
    }
}


The game must automatically recognize and display the new entry.

Apply this same architecture to:

Characters

Countries/categories

Businesses

Stocks

Investments

Properties

Luxury assets

Locations

Events

4. CHARACTER ACQUISITION

Create a fictional adult-character catalogue.

Every character must be explicitly 18+.

Each character supports:

id
name
age
country
category
tier
rarity
price
image
unlockRequirement
optionalVideo


Possible states:

locked
available
owned


Purchasing must:

Check the character exists.

Check the character is 18+.

Check unlock requirements.

Check available cash.

Deduct the purchase cost.

Add the character ID to ownedCharacters.

Record the transaction.

Save the game.

Prevent duplicate purchases and invalid spending.

Do NOT implement relationship, romance, or dialogue systems.

5. ECONOMY ENGINE

Create a centralized economy module.

Use functions such as:

addMoney(amount, reason)
removeMoney(amount, reason)
depositMoney(amount)
withdrawMoney(amount)
calculateNetWorth()
recordTransaction()


Important rule:

All financial changes must pass through the economy system.

Never randomly modify:

cash
bankBalance


from unrelated modules.

Track:

Cash

Bank balance

Income

Expenses

Net worth

Transaction history

6. TRANSACTION HISTORY

Every financial transaction must be recorded.

Each transaction should contain:

{
    day: 12,
    type: "business_income",
    amount: 15000,
    description: "Nightclub daily income",
    balanceAfter: 84250
}


Possible transaction types:

business purchase
business income
business expense
character purchase
property purchase
asset purchase
stock buy
stock sell
investment
daily expense
random event


This system is important for debugging and balancing.

7. BUSINESS SYSTEM

Create recurring-income businesses.

Business data should support:

id
name
category
purchasePrice
baseIncome
operatingCost
upgradeCost
incomeGrowth
level
unlockRequirement
image


Core loop:

Buy → Operate → Earn → Upgrade → Earn more

Every upgrade should:

cost money

increase income

potentially increase operating costs

increase future upgrade cost

Prevent free or duplicated income.

8. TIME SYSTEM

Create a central:

advanceDay()


function.

When the player advances one day:

Businesses generate income.

Daily expenses are calculated.

Stock prices update.

Investments update.

Random events are evaluated.

Temporary modifiers update.

The game day increases.

The game automatically saves.

Do not scatter daily processing across unrelated files.

9. STOCK MARKET

Create a completely fictional stock market.

Stocks should contain:

id
symbol
companyName
sector
price
volatility
risk
marketSensitivity


Sectors can include:

Technology

Finance

Energy

Real Estate

Retail

Entertainment

Support:

BUY
SELL
HOLD


Track:

sharesOwned
averagePurchasePrice
currentValue
profitLoss


Prevent:

negative shares

selling shares the player does not own

purchases without sufficient money

impossible portfolio values

10. RANDOMIZED STOCK PRICES

The stock market must be unpredictable but controlled.

Do NOT simply use meaningless random price jumps.

Stock movement should consider:

previous price
market condition
sector trend
company-specific movement
volatility
random noise


Conceptually:

newPrice =
previousPrice
+ marketMovement
+ sectorMovement
+ companyMovement
+ volatilityNoise


Different stocks should behave differently.

Low-volatility stocks:

smaller movements and smaller potential losses

High-volatility stocks:

larger movements and larger potential gains/losses

There must be no guaranteed profitable strategy.

11. MARKET CONDITIONS

Create overall market conditions:

Bull Market
Normal Market
Bear Market
Boom
Crash


Market conditions should influence stocks but should NOT make every stock move identically.

12. RANDOM ECONOMIC EVENTS

Create data-driven market events.

Examples:

Technology Boom
Banking Crisis
Energy Shortage
Real Estate Surge
Consumer Spending Drop
Market Panic
Company Breakthrough
Company Scandal


Events may affect:

individual companies

sectors

the entire market

business income

expenses

Each event can define:

probability
duration
affectedStocks
affectedSectors
marketModifier
effects


13. INVESTMENT SYSTEM

Create investments separate from ordinary stocks.

Types:

Safe
Medium Risk
High Risk
Real Estate
Locked-Term


Each investment should define:

minimumCapital
expectedReturn
risk
duration
liquidity


Some investments may lock the player's money for several days.

Returns should have uncertainty.

14. PROPERTY SYSTEM

Create a fully data-driven property system.

Example properties:

Apartment
Luxury Apartment
House
Mansion
Penthouse


Property data:

id
name
category
price
maintenanceCost
lifestyleBonus
reputationBonus
image
unlockRequirement


Purchasing a property must:

deduct money

add ownership

affect relevant player stats

create recurring maintenance costs

15. LIFESTYLE SYSTEM

Create these lifestyle tiers:

Low
Comfortable
Wealthy
Millionaire
Elite


Each lifestyle defines:

minimumNetWorth
dailyMaintenance
reputationBonus
availableCharacters
availableProperties
availableLocations
availableEvents


Higher lifestyle:

unlocks better opportunities

but also:

creates significantly higher recurring costs.

If the player can no longer sustain a lifestyle, implement a sensible downgrade mechanism.

16. LUXURY ASSET SYSTEM

Create a generic asset system.

Examples:

Supercar
Yacht
Private Jet
Jewelry
Luxury Items


Each asset supports:

id
name
price
maintenance
lifestyleBonus
reputationBonus
image


Buying assets changes the appropriate player stats and recurring costs.

17. REPUTATION

Create a numeric reputation system.

Reputation can change due to:

wealth milestones

businesses

lifestyle

luxury assets

investments

major events

Use reputation as an unlock requirement.

18. RANDOM EVENT ENGINE

Build one reusable event system.

Events should be defined in data files.

A generic event can:

give money

remove money

modify reputation

modify expenses

modify business income

modify stock prices

unlock content

apply temporary modifiers

Adding a new event should require only a new data entry.

19. ECONOMIC DIFFICULTY

Money generation should NOT be easy.

The intended progression:

Early game

Low income + meaningful expenses + limited opportunities.

Mid game

Multiple income streams + larger investments + higher expenses.

Late game

Huge income potential + huge expenses + large financial risks.

Prevent:

infinite money

guaranteed stock profits

trivial passive income

duplicate purchases

negative-price exploits

free upgrades

impossible investment returns

runaway compounding that breaks the game

The player should need to make financial decisions to become wealthy.

20. LOCAL SAVE SYSTEM

Use localStorage only.

Implement:

saveGame()
loadGame()
resetGame()
exportSave()
importSave()


Save all important state, including:

money
bank
day
reputation
lifestyle
owned characters
owned businesses
owned properties
owned assets
stock portfolio
investments
active modifiers
event history
transaction history


There must be:

NO account system.

NO authentication.

NO cloud save.

NO database.

The save exists only in the user's browser.

21. LOCAL ASSETS

Use local asset paths.

Example:

assets/
├── characters/
├── properties/
├── businesses/
├── locations/
├── videos/
└── audio/


Use placeholder paths initially.

Example:

assets/characters/character-001.webp
assets/properties/property-001.webp
assets/businesses/business-001.webp


I will replace the placeholders later with my own assets.

The code must continue working when those files are replaced.

22. MINIMAL TEST UI

Create only a simple interface for testing.

Example:

Day: 1
Cash: $10,000
Bank: $0
Net Worth: $10,000
Reputation: 0
Lifestyle: Low

[Advance Day]

[Characters]
[Businesses]
[Stocks]
[Investments]
[Properties]
[Assets]
[Events]

[Save]
[Load]
[Reset]

[Debug]


The UI can be ugly.

That is intentional.

Do not spend time on visual polish.

23. DEBUG MODE

Create a development-only debug panel showing:

Day
Cash
Bank
Net Worth
Income
Expenses
Reputation
Lifestyle
Owned Characters
Owned Businesses
Owned Properties
Stock Portfolio
Investments
Active Modifiers
Recent Transactions


Add testing controls:

Advance Day
Add Money
Remove Money
Force Bull Market
Force Bear Market
Force Market Crash
Trigger Random Event
Reset Game


Clearly mark these as DEBUG tools.

24. CODE ORGANIZATION

Keep responsibilities separated.

Suggested structure:

index.html

css/
    style.css

js/
    main.js
    state.js
    economy.js
    time.js
    characters.js
    businesses.js
    stocks.js
    investments.js
    properties.js
    assets.js
    lifestyle.js
    reputation.js
    events.js
    save.js
    debug.js

data/
    characters.js
    businesses.js
    stocks.js
    investments.js
    properties.js
    assets.js
    locations.js
    events.js
    lifestyleLevels.js

assets/
    characters/
    properties/
    businesses/
    locations/
    videos/
    audio/


Use ES modules where useful.

Keep functions small and focused.

Avoid one giant JavaScript file.

Avoid duplicated logic.

25. FINAL HARD REQUIREMENTS

Before finishing, verify:

No backend exists.

No database exists.

No authentication exists.

No API calls exist.

No cloud services exist.

No React/Next.js/framework is used.

No external dependency is required for the game to function.

The game must work entirely from:

HTML + CSS + JavaScript + local data + local assets + localStorage.

Most importantly:

CONTENT EXPANSION MUST BE EASY

I want this workflow:

Add new image
+
Add one data object
+
Refresh
=
New game content automatically appears


This must work for characters, businesses, stocks, investments, properties, assets, locations, and events.

FINAL PRIORITY

Do NOT optimize for beautiful UI.

Optimize for:

CORRECT GAME LOGIC
MODULAR CODE
DATA-DRIVEN CONTENT
RANDOMIZED ECONOMY
DIFFICULT BUT FAIR PROGRESSION
LOCAL SAVE SYSTEM
EASY CONTENT EXPANSION
RELIABLE CLIENT-SIDE OPERATION

Build the frontend-only playable mechanics prototype first. Visual design will be developed separately later.

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/286fbc40-2763-48fc-abc1-e9406d3098c0).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
