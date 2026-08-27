> ### ⚠️ Design specification — not implemented
>
> **This repository contains a design document only. There is no source code here.**
>
> Everything below describes an intended architecture. Any performance figure, benchmark,
> latency target, throughput number or Sharpe ratio in this document is a **design target
> that has never been measured**, not a result. Installation and usage instructions
> describe files that do not exist in this repository.
>
> It is published as a specification and planning artefact. For systems that are actually
> built and tested, see
> **[prediction-market-algorithmic-trading](https://github.com/pranay123-stack/prediction-market-algorithmic-trading)**.

---

# Prediction Market Projects

A comprehensive collection of decentralized prediction market implementations — from binary outcome markets and AMM-based pricing to conditional tokens, oracle resolution, and advanced market mechanisms. Built to understand the $3.69B+ prediction market ecosystem at the smart contract level.

---

## Table of Contents

- [Overview](#overview)
- [Why Prediction Markets?](#why-prediction-markets)
- [Prediction Market Ecosystem](#prediction-market-ecosystem)
- [Tech Stack](#tech-stack)
- [Projects](#projects)
  - [Core Market Mechanics](#core-market-mechanics)
  - [AMM & Pricing Models](#amm--pricing-models)
  - [Oracle & Resolution Systems](#oracle--resolution-systems)
  - [Advanced Market Types](#advanced-market-types)
  - [Market Infrastructure](#market-infrastructure)
  - [Full-Stack Prediction Platforms](#full-stack-prediction-platforms)
- [How Prediction Markets Work](#how-prediction-markets-work)
- [Architecture Diagrams](#architecture-diagrams)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Testing](#testing)
- [Market Mathematics](#market-mathematics)
- [Security](#security)
- [Deployment](#deployment)
- [Key Concepts](#key-concepts)
- [Top Prediction Market Tokens](#top-prediction-market-tokens)
- [Resources](#resources)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

Prediction markets turn opinions into prices. When people bet real money on outcomes, market prices become probability estimates — often more accurate than polls, pundits, or models. This repository implements the full stack of on-chain prediction market infrastructure.

**What you'll build:**

- Binary and multi-outcome markets with automated pricing
- Conditional token frameworks (ERC-1155 based outcome tokens)
- AMM pricing models — LMSR, CPMM, constant-sum
- Oracle and resolution systems — Chainlink, UMA, reality.eth, DAO voting
- Order book markets for deep liquidity and price discovery
- Combinatorial and parimutuel market structures
- Full-stack prediction platforms with real-time UIs
- Market maker bots and arbitrage strategies

---

## Why Prediction Markets?

Prediction markets are one of the most compelling use cases for blockchain technology:

- **Information Aggregation** — Markets distill dispersed knowledge into probability estimates
- **Censorship Resistance** — No central authority can shut down or manipulate markets
- **Transparent Resolution** — Outcomes verified by decentralized oracles, not opaque judges
- **Capital Efficiency** — Conditional tokens, leverage, and AMMs maximize market depth
- **Real-World Impact** — Elections, sports, crypto prices, science, geopolitics — everything is a market
- **Growing Ecosystem** — $3.69B market cap with protocols like Polymarket leading mainstream adoption

---

## Prediction Market Ecosystem

```
┌─────────────────────────────────────────────────────────────────────────┐
│                   PREDICTION MARKET ECOSYSTEM                          │
│                                                                         │
│  ┌───────────────────┐  ┌───────────────────┐  ┌────────────────────┐  │
│  │  Market Platforms   │  │  Conditional Token │  │  Oracle / Resolution│ │
│  │                     │  │  Frameworks         │  │                    │  │
│  │ • Polymarket       │  │                     │  │ • UMA (Optimistic) │  │
│  │ • Azuro            │  │ • Gnosis CTF        │  │ • Chainlink        │  │
│  │ • Overtime Markets │  │ • Polymarket CTF    │  │ • reality.eth      │  │
│  │ • Hedgehog         │  │ • ERC-1155 Outcomes │  │ • API3             │  │
│  │ • Drift (Perps)    │  │                     │  │ • DAO Vote         │  │
│  └───────────────────┘  └───────────────────┘  └────────────────────┘  │
│                                                                         │
│  ┌───────────────────┐  ┌───────────────────┐  ┌────────────────────┐  │
│  │  Pricing / AMMs    │  │  Order Books       │  │  Analytics / Data  │  │
│  │                     │  │                     │  │                    │  │
│  │ • LMSR             │  │ • CLOB (on-chain)  │  │ • Market dashboards│  │
│  │ • CPMM             │  │ • Hybrid (off/on)  │  │ • Probability feeds│  │
│  │ • Constant Sum     │  │ • RFQ systems      │  │ • Historical data  │  │
│  │ • Dynamic spread   │  │                     │  │ • Leaderboards     │  │
│  └───────────────────┘  └───────────────────┘  └────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Layer                | Technology                                               |
| -------------------- | -------------------------------------------------------- |
| Smart Contracts      | Solidity 0.8.x                                           |
| Frameworks           | Foundry, Hardhat                                         |
| Token Standards      | ERC-1155 (Conditional Tokens), ERC-20, ERC-4626          |
| Pricing Libraries    | PRBMath, Solmate, ABDKMath64x64                          |
| Oracles              | Chainlink, UMA Optimistic Oracle, reality.eth            |
| Automation           | Chainlink Automation, Gelato                             |
| Frontend             | Next.js, React, wagmi, viem, TradingView Lightweight     |
| Real-Time Data       | WebSocket, The Graph, Alchemy Webhooks                   |
| Indexing             | The Graph subgraphs, Ponder                              |
| Networks             | Polygon, Arbitrum, Base, Ethereum, Gnosis Chain          |

---

## Projects

### Core Market Mechanics

| #  | Project                                | Description                                                              | Key Concepts                             |
| -- | -------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| 01 | **Binary Outcome Market**              | Simple yes/no market — buy outcome tokens, redeem on resolution          | Outcome tokens, minting, redemption      |
| 02 | **Multi-Outcome Market**               | Markets with 3+ outcomes (e.g., election with multiple candidates)       | Outcome sets, probability normalization  |
| 03 | **Conditional Token Framework**        | ERC-1155 based conditional tokens that split collateral into outcomes    | CTF, position splitting/merging          |
| 04 | **Market Factory**                     | Deploy new prediction markets permissionlessly with configurable params  | Factory pattern, CREATE2, market registry|
| 05 | **Collateral Vault**                   | Manages deposits, mints outcome tokens, handles redemptions on settle   | Vault accounting, share math, ERC-4626   |

### AMM & Pricing Models

| #  | Project                                | Description                                                              | Key Concepts                             |
| -- | -------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| 06 | **LMSR Market Maker**                  | Logarithmic Market Scoring Rule — Hanson's automated market maker        | LMSR cost function, liquidity parameter  |
| 07 | **CPMM for Prediction Markets**        | Constant Product AMM adapted for binary outcomes (Polymarket-style)      | x*y=k invariant, outcome token pools     |
| 08 | **Constant Sum Market Maker**          | Fixed-price market maker for markets near resolution                     | Linear pricing, bounded markets          |
| 09 | **Dynamic Spread AMM**                 | AMM with spread that adjusts based on volatility and time to resolution  | Adaptive fees, implied volatility        |
| 10 | **Hybrid Order Book + AMM**            | Limit orders backed by AMM liquidity as fallback                         | CLOB, passive liquidity, best execution  |

### Oracle & Resolution Systems

| #  | Project                                | Description                                                              | Key Concepts                             |
| -- | -------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| 11 | **Chainlink Data Feed Resolution**     | Resolve markets using Chainlink price feeds (e.g., "BTC above $100K?")  | Price feed, staleness checks, thresholds |
| 12 | **UMA Optimistic Oracle Resolution**   | Dispute-based resolution — assert outcome, challenge window, DVM vote    | Optimistic oracle, disputes, bonds       |
| 13 | **Reality.eth Resolution**             | Community-answered questions with escalating bonds for disputed outcomes  | Question/answer, bond escalation         |
| 14 | **DAO Governance Resolution**          | Market outcomes decided by token-weighted governance vote                 | Proposal, quorum, vote counting          |
| 15 | **Multi-Source Oracle Aggregator**     | Combine multiple oracles for robust resolution with fallback logic       | Aggregation, median, circuit breakers    |

### Advanced Market Types

| #  | Project                                | Description                                                              | Key Concepts                             |
| -- | -------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| 16 | **Combinatorial Markets**              | Bet on combinations of outcomes (e.g., "Team A wins AND player scores") | Conditional on conditional, joint events |
| 17 | **Scalar / Range Markets**             | Bet on where a value falls within a range (e.g., temperature, price)    | Linear payoff, range bounds, settlement  |
| 18 | **Parimutuel Betting Pool**            | Fixed pool — all bets collected, winners split proportionally            | Pool math, odds at close, no house edge  |
| 19 | **Perpetual Prediction Market**        | Continuous market that never resolves — funding rate tracks probability  | Funding rate, mark price, rolling expiry |
| 20 | **Futarchy Governance**                | Use prediction markets to make DAO decisions — bet on policy outcomes   | Decision markets, conditional value      |

### Market Infrastructure

| #  | Project                                | Description                                                              | Key Concepts                             |
| -- | -------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| 21 | **Market Maker Bot**                   | Automated bot that provides liquidity and earns spread                   | Quoting, inventory risk, hedging         |
| 22 | **Arbitrage Bot (Cross-Market)**       | Detect and exploit price differences across prediction platforms         | Cross-platform arb, atomic execution     |
| 23 | **Prediction Market Indexer**          | Subgraph that indexes all market events for fast frontend queries        | The Graph, event parsing, entity mapping |
| 24 | **Probability Feed Oracle**            | Publish market-derived probabilities on-chain for other protocols to use | Oracle pattern, TWAP probability         |
| 25 | **Fee & Treasury System**              | Protocol fee collection, distribution to stakers, and buyback mechanism  | Fee routing, staking rewards, governance |

### Full-Stack Prediction Platforms

| #  | Project                                | Description                                                              | Key Concepts                             |
| -- | -------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| 26 | **Sports Betting Platform**            | Bet on live sports — match winner, over/under, prop bets with oracles   | Live odds, event scheduling, settlement  |
| 27 | **Election / Politics Market**         | Multi-candidate election markets with real-time probability dashboards  | Multi-outcome, media feeds, visualization|
| 28 | **Crypto Price Prediction**            | Will ETH be above $X by date Y? Binary markets on crypto asset prices   | Price oracles, time-based resolution     |
| 29 | **AI / Science Prediction Market**     | Markets on AI milestones, scientific discoveries, tech events            | Long-duration markets, expert resolution |
| 30 | **Personal Prediction Tracker**        | Create private markets, track your calibration, Brier score dashboard   | Calibration, Brier score, track record   |

---

## How Prediction Markets Work

### Lifecycle of a Prediction Market

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  CREATE   │───►│  TRADE    │───►│  RESOLVE  │───►│  SETTLE   │───►│  REDEEM   │
│           │    │           │    │           │    │           │    │           │
│ Define    │    │ Buy/sell  │    │ Oracle    │    │ Winning   │    │ Winners   │
│ question  │    │ outcome   │    │ reports   │    │ outcome   │    │ redeem    │
│ Set params│    │ tokens    │    │ result    │    │ determined│    │ collateral│
│ Seed      │    │ via AMM   │    │           │    │           │    │           │
│ liquidity │    │ or CLOB   │    │ Dispute?  │    │ Losers    │    │ $1/share  │
│           │    │           │    │ Escalate  │    │ get $0    │    │ for YES   │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
```

### How Outcome Tokens Work

```
                        ┌────────────────────┐
                        │  User deposits $1   │
                        │  (USDC collateral)  │
                        └─────────┬──────────┘
                                  │
                                  ▼
                        ┌────────────────────┐
                        │  Conditional Token  │
                        │  Framework (CTF)    │
                        │                    │
                        │  Splits $1 into:   │
                        └────┬──────────┬────┘
                             │          │
                    ┌────────▼──┐  ┌────▼────────┐
                    │  1 YES     │  │  1 NO        │
                    │  Token     │  │  Token       │
                    │            │  │              │
                    │ Worth $1   │  │ Worth $1     │
                    │ if YES     │  │ if NO        │
                    │ Worth $0   │  │ Worth $0     │
                    │ if NO      │  │ if YES       │
                    └────────────┘  └──────────────┘

  Prices MUST sum to $1:   YES @ $0.65  +  NO @ $0.35  =  $1.00
  This means:              65% implied probability of YES outcome

  TRADING:
  ┌─────────────────────────────────────────────────────────┐
  │  Alice thinks YES is underpriced                        │
  │  → Buys 100 YES tokens @ $0.65 = pays $65              │
  │  → If YES wins: redeems 100 × $1 = $100 (profit: $35)  │
  │  → If NO wins:  tokens worth $0 (loss: $65)             │
  │                                                         │
  │  Bob thinks NO is underpriced                           │
  │  → Buys 200 NO tokens @ $0.35 = pays $70               │
  │  → If NO wins:  redeems 200 × $1 = $200 (profit: $130) │
  │  → If YES wins: tokens worth $0 (loss: $70)             │
  └─────────────────────────────────────────────────────────┘

  MERGE (reverse of split):
  1 YES + 1 NO → redeem $1 collateral (anytime, regardless of outcome)
```

### Multi-Outcome Market Example

```
  "Who will win the 2028 Presidential Election?"

  ┌─────────────┬─────────┬──────────────────┐
  │  Outcome     │  Price   │  Implied Prob.   │
  ├─────────────┼─────────┼──────────────────┤
  │  Candidate A │  $0.42  │  42%             │
  │  Candidate B │  $0.35  │  35%             │
  │  Candidate C │  $0.15  │  15%             │
  │  Other       │  $0.08  │   8%             │
  ├─────────────┼─────────┼──────────────────┤
  │  TOTAL       │  $1.00  │ 100%             │
  └─────────────┴─────────┴──────────────────┘

  All outcome token prices must sum to $1.00
  Any deviation = arbitrage opportunity
```

---

## Architecture Diagrams

### Full Platform Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         FRONTEND                                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │
│  │ Market Browse │  │ Trading UI   │  │ Portfolio & History       │  │
│  │ & Discovery   │  │ (Order Entry)│  │ (P&L, positions, claims) │  │
│  └──────┬───────┘  └──────┬───────┘  └────────────┬─────────────┘  │
└─────────┼─────────────────┼───────────────────────┼─────────────────┘
          │                 │                       │
          ▼                 ▼                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│                      SMART CONTRACTS                                 │
│                                                                      │
│  ┌─────────────┐  ┌─────────────┐  ┌────────────┐  ┌─────────────┐ │
│  │ Market       │  │ Conditional  │  │ AMM /      │  │ Resolution  │ │
│  │ Factory      │  │ Token (CTF)  │  │ Order Book │  │ Module      │ │
│  │              │  │              │  │            │  │             │ │
│  │ • Create     │  │ • Split      │  │ • Buy/Sell │  │ • Report    │ │
│  │ • Configure  │  │ • Merge      │  │ • LP add   │  │ • Dispute   │ │
│  │ • Registry   │  │ • Transfer   │  │ • LP remove│  │ • Settle    │ │
│  │ • Fees       │  │ • Redeem     │  │ • Route    │  │ • Payout    │ │
│  └─────────────┘  └─────────────┘  └────────────┘  └──────┬──────┘ │
│                                                            │        │
└────────────────────────────────────────────────────────────┼────────┘
                                                             │
                         ┌───────────────────────────────────┼───┐
                         │          ORACLE LAYER              │   │
                         │                                    ▼   │
                         │  ┌────────────┐  ┌────────────────────┐│
                         │  │ Chainlink   │  │ UMA Optimistic     ││
                         │  │ Data Feeds  │  │ Oracle             ││
                         │  └────────────┘  └────────────────────┘│
                         │  ┌────────────┐  ┌────────────────────┐│
                         │  │ reality.eth│  │ DAO Governance     ││
                         │  │            │  │ Vote               ││
                         │  └────────────┘  └────────────────────┘│
                         └────────────────────────────────────────┘
```

### LMSR Pricing Flow

```
┌──────────────────────────────────────────────────────────────────┐
│                LMSR (Logarithmic Market Scoring Rule)            │
│                                                                  │
│  Cost Function:  C(q) = b × ln(Σ e^(qi/b))                     │
│                                                                  │
│  Where:                                                          │
│    q = vector of outstanding shares per outcome                  │
│    b = liquidity parameter (higher b = less price impact)        │
│                                                                  │
│  Price of outcome i:  p(i) = e^(qi/b) / Σ e^(qj/b)            │
│                                                                  │
│  Example (binary market, b=100):                                 │
│                                                                  │
│  State: YES=150 shares, NO=80 shares                            │
│                                                                  │
│  P(YES) = e^(150/100) / (e^(150/100) + e^(80/100))             │
│         = 4.48 / (4.48 + 2.23)                                  │
│         = 0.668  →  66.8% implied probability                   │
│                                                                  │
│  Cost to buy 10 YES shares:                                      │
│    C(160,80) - C(150,80) = ... ≈ $7.12                          │
│                                                                  │
│  Properties:                                                     │
│  ✓ Prices always sum to $1                                       │
│  ✓ Bounded loss for market maker (≤ b × ln(n))                  │
│  ✓ Prices move smoothly                                          │
│  ✓ Works for any number of outcomes                              │
└──────────────────────────────────────────────────────────────────┘
```

### Optimistic Oracle Resolution (UMA-Style)

```
Asserter              UMA Oracle            Disputer              DVM (Vote)
   │                      │                     │                     │
   ├── assertOutcome ────►│                     │                     │
   │   (bond: $1000)      │                     │                     │
   │                      │── challenge window ─┤                     │
   │                      │   (2 hours)         │                     │
   │                      │                     │                     │
   │              ┌───────┴───────┐              │                     │
   │              │  NO DISPUTE?  │              │                     │
   │              │  → Settled ✓  │              │                     │
   │              │  Bond returned│              │                     │
   │              └───────────────┘              │                     │
   │                      │                     │                     │
   │              ┌───────┴───────┐              │                     │
   │              │  DISPUTED?    │◄── dispute ──┤                     │
   │              │               │  (bond:$1000)│                     │
   │              └───────┬───────┘              │                     │
   │                      │                     │                     │
   │                      ├── escalate to DVM ──────────────────────►│
   │                      │                     │                     │
   │                      │                     │          Token holders
   │                      │                     │          vote on truth
   │                      │                     │                     │
   │                      │◄── DVM result ───────────────────────────┤
   │                      │                     │                     │
   │              ┌───────┴───────┐              │                     │
   │              │ Winner gets   │              │                     │
   │              │ their bond +  │              │                     │
   │              │ loser's bond  │              │                     │
   │              │               │              │                     │
   │              │ Market settled│              │                     │
   │              └───────────────┘              │                     │
```

### Arbitrage Between Markets

```
┌─────────────────────────────────────────────────────────────────────┐
│                CROSS-MARKET ARBITRAGE                                │
│                                                                     │
│  Same event priced differently across platforms:                    │
│                                                                     │
│  Platform A:  "ETH > $5000 by Dec?"   YES @ $0.62                 │
│  Platform B:  "ETH > $5000 by Dec?"   YES @ $0.55                 │
│                                                                     │
│  Arbitrage:                                                         │
│  ┌────────────────────────────────────────────────┐                │
│  │ 1. Buy YES on Platform B @ $0.55               │                │
│  │ 2. Sell YES on Platform A @ $0.62              │                │
│  │ 3. Risk-free profit: $0.07 per share (11.3%)  │                │
│  └────────────────────────────────────────────────┘                │
│                                                                     │
│  Completeness Arbitrage (same platform):                           │
│  ┌────────────────────────────────────────────────┐                │
│  │ If YES @ $0.55 + NO @ $0.40 = $0.95 (< $1.00) │                │
│  │ Buy 1 YES + 1 NO = pay $0.95                   │                │
│  │ Guaranteed redemption = $1.00                   │                │
│  │ Risk-free profit: $0.05 per set (5.3%)         │                │
│  └────────────────────────────────────────────────┘                │
│                                                                     │
│  Overpriced Arbitrage:                                              │
│  ┌────────────────────────────────────────────────┐                │
│  │ If YES @ $0.58 + NO @ $0.47 = $1.05 (> $1.00) │                │
│  │ Mint 1 YES + 1 NO from $1 collateral           │                │
│  │ Sell both: receive $1.05                        │                │
│  │ Risk-free profit: $0.05 per set (5%)           │                │
│  └────────────────────────────────────────────────┘                │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Repository Structure

```
prediction-market-projects/
├── 01-binary-outcome-market/
│   ├── src/
│   │   ├── BinaryMarket.sol
│   │   ├── OutcomeToken.sol
│   │   └── interfaces/
│   ├── test/
│   │   ├── BinaryMarket.t.sol
│   │   ├── fuzz/
│   │   └── invariant/
│   ├── script/
│   │   └── Deploy.s.sol
│   ├── foundry.toml
│   └── README.md
├── 03-conditional-token-framework/
│   ├── src/
│   │   ├── ConditionalTokens.sol
│   │   ├── CTFExchange.sol
│   │   └── libraries/
│   └── README.md
├── 06-lmsr-market-maker/
│   ├── src/
│   │   ├── LMSR.sol
│   │   └── math/
│   │       ├── FixedPointMath.sol
│   │       └── ExpLib.sol
│   ├── test/
│   │   ├── LMSR.t.sol
│   │   └── math/
│   └── README.md
├── 12-uma-optimistic-resolution/
│   ├── src/
│   │   ├── OptimisticResolution.sol
│   │   └── interfaces/
│   │       └── IOptimisticOracle.sol
│   ├── test/
│   │   └── fork/
│   └── README.md
├── 26-sports-betting-platform/
│   ├── contracts/
│   ├── frontend/
│   │   ├── src/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   └── pages/
│   │   └── package.json
│   ├── subgraph/
│   │   ├── schema.graphql
│   │   ├── subgraph.yaml
│   │   └── src/
│   └── README.md
├── lib/                      # Shared Solidity dependencies
│   ├── forge-std/
│   ├── openzeppelin-contracts/
│   ├── solmate/
│   └── prb-math/
├── interfaces/               # Common prediction market interfaces
│   ├── IMarket.sol
│   ├── IConditionalTokens.sol
│   ├── IResolutionModule.sol
│   ├── IMarketMaker.sol
│   └── IOracle.sol
├── libraries/                # Shared math and utility libraries
│   ├── MarketMath.sol        # LMSR, CPMM pricing math
│   ├── OutcomeLib.sol        # Outcome token utilities
│   └── OracleLib.sol         # Oracle validation helpers
└── README.md
```

---

## Getting Started

### Prerequisites

- **Foundry** — `curl -L https://foundry.paradigm.xyz | bash && foundryup`
- **Node.js** >= 18.x (for frontends and subgraphs)
- **Git**
- An RPC provider account ([Alchemy](https://www.alchemy.com/) or [Infura](https://www.infura.io/))

### Quick Start

```bash
# Clone the repository
git clone https://github.com/pranay123-stack/prediction-market-projects.git
cd prediction-market-projects

# Navigate to a project
cd 01-binary-outcome-market

# Install dependencies
forge install

# Build
forge build

# Run tests
forge test -vvv
```

### Environment Setup

```bash
cp .env.example .env
```

```env
# RPC Endpoints
MAINNET_RPC_URL=https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY
POLYGON_RPC_URL=https://polygon-mainnet.g.alchemy.com/v2/YOUR_KEY
ARBITRUM_RPC_URL=https://arb-mainnet.g.alchemy.com/v2/YOUR_KEY
BASE_RPC_URL=https://base-mainnet.g.alchemy.com/v2/YOUR_KEY
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY

# Deployment
PRIVATE_KEY=your_deployer_private_key
ETHERSCAN_API_KEY=your_etherscan_api_key
POLYGONSCAN_API_KEY=your_polygonscan_api_key

# Oracles
UMA_ORACLE_ADDRESS=0x...
CHAINLINK_FEED_ADDRESS=0x...

# The Graph (for indexer projects)
GRAPH_DEPLOY_KEY=your_deploy_key
SUBGRAPH_NAME=your-name/prediction-markets
```

> **Never commit private keys.** All projects include `.gitignore` with `.env` excluded.

---

## Development Workflow

### Foundry Commands

```bash
# Compile
forge build

# Run all tests
forge test

# Run specific test
forge test --match-test testBuyOutcomeTokens -vvvv

# Gas report
forge test --gas-report

# Fork test against live oracles
forge test --fork-url $POLYGON_RPC_URL --match-path "test/fork/*" -vvv

# Watch mode
forge test --watch

# Interact with deployed markets
cast call $MARKET "getPrice(uint256)" 0 --rpc-url $POLYGON_RPC_URL
cast call $MARKET "getPrice(uint256)" 1 --rpc-url $POLYGON_RPC_URL
```

### Frontend Development

```bash
cd frontend
pnpm install
pnpm dev
# Open http://localhost:3000
```

### Subgraph Development

```bash
cd subgraph

# Generate types from schema
graph codegen

# Build subgraph
graph build

# Deploy to hosted service
graph deploy --studio $SUBGRAPH_NAME
```

---

## Testing

### Test Categories

```bash
# Unit Tests — individual functions (pricing, splitting, merging)
forge test --match-path "test/unit/*"

# Integration Tests — full market lifecycle
forge test --match-path "test/integration/*"

# Fuzz Tests — random amounts, edge case discovery
forge test --match-path "test/fuzz/*"

# Invariant Tests — market properties that must always hold
forge test --match-path "test/invariant/*"

# Fork Tests — test against live UMA oracle, Chainlink feeds
forge test --match-path "test/fork/*" --fork-url $POLYGON_RPC_URL

# Math Tests — verify pricing model accuracy
forge test --match-path "test/math/*"
```

### Critical Market Invariants

```solidity
// Outcome token prices must always sum to $1 (normalized)
function invariant_pricesSumToOne() public {
    uint256 totalPrice;
    for (uint i = 0; i < market.outcomeCount(); i++) {
        totalPrice += market.getPrice(i);
    }
    // Allow 0.01% tolerance for rounding
    assertApproxEqRel(totalPrice, 1e18, 0.0001e18);
}

// Collateral locked must equal total outcome tokens outstanding
function invariant_collateralBacked() public {
    uint256 totalMinted = market.totalOutcomeTokensMinted();
    uint256 collateralLocked = collateral.balanceOf(address(market));
    assertEq(collateralLocked, totalMinted);
}

// Split + merge is identity: no value created or destroyed
function invariant_splitMergeIdentity() public {
    uint256 balanceBefore = collateral.balanceOf(user);
    market.split(1e18);   // $1 → 1 YES + 1 NO
    market.merge(1e18);   // 1 YES + 1 NO → $1
    uint256 balanceAfter = collateral.balanceOf(user);
    assertEq(balanceBefore, balanceAfter);
}

// After resolution: winning tokens worth exactly $1, losing worth $0
function invariant_payoutCorrect() public {
    if (market.resolved()) {
        uint256 winningOutcome = market.winningOutcome();
        assertEq(market.getRedemptionValue(winningOutcome), 1e18);
        for (uint i = 0; i < market.outcomeCount(); i++) {
            if (i != winningOutcome) {
                assertEq(market.getRedemptionValue(i), 0);
            }
        }
    }
}

// LMSR: cost function must be monotonically increasing
function invariant_lmsrCostIncreasing() public {
    uint256 cost10 = lmsr.costToBuy(YES, 10e18);
    uint256 cost20 = lmsr.costToBuy(YES, 20e18);
    assertGt(cost20, cost10);
}

// No arbitrage: cannot profit from buying all outcomes and redeeming
function invariant_noFreeArbitrage() public {
    uint256 costAll;
    for (uint i = 0; i < market.outcomeCount(); i++) {
        costAll += market.costToBuy(i, 1e18);
    }
    assertGe(costAll, 1e18); // Must cost at least $1 to buy full set
}
```

---

## Market Mathematics

### Pricing Models Comparison

| Model              | Formula                            | Best For                          | Trade-offs                          |
| ------------------ | ---------------------------------- | --------------------------------- | ----------------------------------- |
| **LMSR**           | C = b × ln(Σ e^(qi/b))           | Multi-outcome, low liquidity      | Bounded loss, complex math          |
| **CPMM**           | x × y = k                         | Binary markets, DeFi native       | Simple, high slippage at extremes   |
| **Constant Sum**   | x + y = k                         | Near-resolution markets           | Fixed price, no price discovery     |
| **Parimutuel**     | Payout = pool / winning bets       | Fixed-pool, events with clear end | Odds change until close             |
| **Order Book**     | Bid/ask matching                   | Deep liquidity, pro traders       | Requires active market makers       |

### LMSR Deep Dive

```
Parameters:
  b = liquidity parameter (higher = less price impact, more subsidy needed)
  q = [q_yes, q_no] = outstanding shares per outcome
  n = number of outcomes

Cost function:
  C(q) = b × ln(e^(q_yes/b) + e^(q_no/b))

Price of YES:
  P(YES) = e^(q_yes/b) / (e^(q_yes/b) + e^(q_no/b))

Maximum loss for market maker:
  Max Loss = b × ln(n)
  For binary market: Max Loss = b × ln(2) ≈ 0.693 × b

Example with b = 100:
  Max loss = 100 × 0.693 = $69.30
  This is the cost of providing liquidity (subsidy)

Choosing b:
  b = 10   → Low liquidity, prices move fast, subsidy ~$6.93
  b = 100  → Medium liquidity, moderate moves, subsidy ~$69.30
  b = 1000 → Deep liquidity, stable prices, subsidy ~$693.00
```

### Brier Score (Forecasting Accuracy)

```
Brier Score = (1/N) × Σ (forecast_i - outcome_i)²

Where:
  forecast_i = predicted probability (0 to 1)
  outcome_i  = actual outcome (0 or 1)
  N          = number of predictions

Perfect score: 0 (predicted exactly right every time)
Worst score:   1 (always maximally wrong)
Random guess:  0.25 (for binary events at 50/50)

Example:
  Prediction: "70% chance of rain"  →  forecast = 0.70
  Outcome: It rained               →  outcome  = 1
  Brier Score = (0.70 - 1)² = 0.09  (good prediction!)

  Prediction: "90% chance of rain"  →  forecast = 0.90
  Outcome: It didn't rain           →  outcome  = 0
  Brier Score = (0.90 - 0)² = 0.81  (bad prediction!)
```

---

## Security

### Prediction Market Attack Vectors

| Attack                           | Description                                                    | Mitigation                                     |
| -------------------------------- | -------------------------------------------------------------- | ---------------------------------------------- |
| **Oracle Manipulation**          | Corrupting the data source that resolves the market             | Multi-oracle, UMA dispute system, TWAP         |
| **Front-Running Resolution**     | Buying winning outcome after seeing oracle tx in mempool        | Commit-reveal resolution, private mempool      |
| **Market Manipulation**          | Whale moves price to influence real-world outcomes (futarchy)   | Position limits, TWAP pricing, time-weighted   |
| **Flash Loan Price Manipulation**| Borrow to move price, trigger dependent contracts               | Block-delayed reads, TWAP, multi-block         |
| **Sybil for Rewards**           | Creating many wallets to farm trader rewards or airdrops        | Min position size, time-weighted participation  |
| **Grief Resolution**            | Repeatedly disputing correct outcomes to delay settlement       | Escalating bonds, dispute cooldowns             |
| **Incomplete Market Attack**    | Outcome not covered by any token (ambiguous question)           | Void/invalid outcome option, careful phrasing   |
| **Collateral Drain**            | Exploiting rounding errors in split/merge to extract value      | Round in protocol's favor, minimum amounts      |
| **Stale Oracle**                | Using outdated price data to resolve time-sensitive markets     | Staleness checks, heartbeat validation          |
| **Sandwich on Outcome Buys**    | Front/back-running large outcome token purchases               | Slippage protection, max price parameter        |

### Security Checklist

- [ ] Oracle resolution has dispute mechanism with bond escalation
- [ ] Outcome token prices verified to sum to 1.0 (no free arbitrage)
- [ ] Split/merge operations preserve total collateral exactly
- [ ] Resolution cannot be front-run (commit-reveal or timelock)
- [ ] Position limits or circuit breakers for manipulation resistance
- [ ] Stale oracle data rejected with configurable heartbeat
- [ ] Reentrancy guards on all token transfer and redemption paths
- [ ] Market can be voided/invalidated for ambiguous outcomes
- [ ] Fee calculations round in protocol's favor
- [ ] Emergency pause and admin withdrawal with timelock

---

## Deployment

### Recommended Networks

| Network          | Chain ID  | Why                                                      | Used By               |
| ---------------- | --------- | -------------------------------------------------------- | --------------------- |
| Polygon          | 137       | Low fees, fast finality, established prediction markets   | Polymarket (bridged)  |
| Arbitrum One     | 42161     | EVM compatible, low fees, growing ecosystem               | Overtime, Thales      |
| Base             | 8453      | Coinbase ecosystem, consumer-friendly, ultra-low fees     | Hedgehog              |
| Gnosis Chain     | 100       | Home of Gnosis CTF, native prediction market infra        | Omen, Gnosis          |
| Ethereum         | 1         | Settlement layer, high-value markets                      | UMA, Augur (legacy)   |
| Sepolia          | 11155111  | Testing                                                   | All                   |

### Deploy a Market

```bash
# 1. Deploy Conditional Token Framework
forge script script/DeployCTF.s.sol \
  --rpc-url $POLYGON_RPC_URL \
  --broadcast --verify

# 2. Deploy Market Factory
forge script script/DeployFactory.s.sol \
  --rpc-url $POLYGON_RPC_URL \
  --broadcast --verify

# 3. Deploy AMM (LMSR or CPMM)
forge script script/DeployAMM.s.sol \
  --rpc-url $POLYGON_RPC_URL \
  --broadcast --verify

# 4. Deploy Resolution Module
forge script script/DeployResolution.s.sol \
  --rpc-url $POLYGON_RPC_URL \
  --broadcast --verify

# 5. Create a market
cast send $FACTORY "createMarket(string,uint256,address,address)" \
  "Will ETH be above 5000 by Dec 2026?" \
  1767225600 \
  $AMM_ADDRESS \
  $RESOLUTION_MODULE \
  --rpc-url $POLYGON_RPC_URL \
  --private-key $PRIVATE_KEY
```

---

## Key Concepts

| Concept                          | Description                                                                 |
| -------------------------------- | --------------------------------------------------------------------------- |
| **Prediction Market**            | Marketplace where participants trade on the probability of future events    |
| **Outcome Token**                | Token representing a specific outcome — worth $1 if correct, $0 if wrong   |
| **Conditional Token (CTF)**      | ERC-1155 token that represents a conditional claim on collateral            |
| **Split**                        | Deposit $1 collateral → receive 1 of each outcome token                    |
| **Merge**                        | Return 1 of each outcome token → receive $1 collateral back                |
| **Resolution**                   | Oracle reports the actual outcome, enabling winner redemption               |
| **LMSR**                         | Logarithmic Market Scoring Rule — AMM with bounded market maker loss       |
| **Implied Probability**          | Market price interpreted as probability (YES @ $0.70 = 70% chance)         |
| **Calibration**                  | How closely predicted probabilities match actual outcome frequencies        |
| **Brier Score**                  | Metric for forecasting accuracy — lower is better (0 = perfect)            |
| **Parimutuel**                   | Betting pool where all bets collected, winners split proportionally         |
| **Futarchy**                     | Governance by prediction market — policies chosen by market forecast        |
| **Completeness**                 | All outcome prices summing to exactly $1.00                                 |
| **Liquidity Parameter (b)**      | LMSR parameter controlling price sensitivity and maximum subsidy            |
| **Dispute / Escalation**         | Challenge mechanism when oracle resolution is contested                     |
| **Optimistic Oracle**            | Assume assertion is correct unless disputed within challenge window          |
| **Combinatorial Market**         | Markets on combinations of independent events                               |
| **Scalar Market**                | Outcome is a numeric range rather than discrete categories                   |

---

## Top Prediction Market Tokens

A snapshot of the prediction market sector powering the ecosystem:

| Token             | Project              | Market Cap Rank | Role in Ecosystem                                        |
| ----------------- | -------------------- | --------------- | -------------------------------------------------------- |
| **MATIC/POL**     | Polygon              | Top 30          | Infrastructure layer for Polymarket and Gnosis markets    |
| **UMA**           | UMA Protocol         | Top 200         | Optimistic Oracle powering dispute-based resolution       |
| **GNO**           | Gnosis               | Top 150         | Gnosis Chain, CTF framework, Omen prediction markets      |
| **AZUR**          | Azuro                | Top 500         | Decentralized sports betting and prediction infrastructure|
| **THALES**        | Thales Market        | Top 600         | Positional markets on Optimism and Arbitrum               |
| **DRIFT**         | Drift Protocol       | Top 300         | Perpetual prediction markets on Solana                    |
| **HEDGEHOG**      | Hedgehog Markets     | Top 800         | Binary prediction markets on Base                         |
| **REP**           | Augur (legacy)       | Top 500         | Pioneer decentralized prediction market (Ethereum)        |

> Market data as of May 2026. Total prediction market sector cap: ~$3.69B.

---

## Resources

### Protocol Documentation

- [Polymarket Docs](https://docs.polymarket.com/) — Leading prediction market platform
- [Gnosis Conditional Token Framework](https://docs.gnosis.io/conditionaltokens/) — Industry-standard CTF
- [UMA Optimistic Oracle](https://docs.uma.xyz/) — Dispute-based truth machine
- [Azuro Protocol](https://docs.azuro.org/) — Sports and event betting infrastructure
- [Omen (Gnosis)](https://omen.eth.limo/) — Decentralized prediction market on Gnosis Chain

### Market Maker Theory

- [Hanson's LMSR Paper](https://mason.gmu.edu/~rhanson/mktscore.pdf) — Original logarithmic scoring rule
- [Othman et al. — Practical LMSR](https://www.cs.cmu.edu/~sandholm/liquidity-sensitive%20automated%20market%20maker.teac.pdf) — Liquidity-sensitive extensions
- [Prediction Market Design (Vitalik)](https://vitalik.eth.limo/) — Futarchy and market design essays

### Development

- [Foundry Book](https://book.getfoundry.sh/)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/)
- [PRBMath](https://github.com/PaulRBerg/prb-math) — Fixed-point math for Solidity
- [The Graph](https://thegraph.com/docs/) — Indexing and querying blockchain data

### Research & Learning

- [Metaculus](https://www.metaculus.com/) — Forecasting platform and calibration training
- [Manifold Markets](https://manifold.markets/) — Play-money prediction markets for learning
- [Superforecasting (Philip Tetlock)](https://en.wikipedia.org/wiki/Superforecasting) — The science of prediction
- [Prediction Markets (Arrow et al.)](https://www.science.org/doi/10.1126/science.1157679) — Academic foundation

### Security

- [Trail of Bits — Building Secure Contracts](https://secure-contracts.com/)
- [Slither](https://github.com/crytic/slither) — Static analysis
- [Echidna](https://github.com/crytic/echidna) — Fuzzing
- [UMA Audit Reports](https://docs.uma.xyz/resources/audit-and-bug-bounty)

---

## Contributing

Contributions are welcome! Whether it's a new market type, pricing model, or resolution mechanism:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-market-type`)
3. Follow the existing project structure
4. Include comprehensive tests (unit + fuzz + invariant)
5. Add a `README.md` with math explanations, architecture, and security analysis
6. Submit a pull request

**High-impact contribution ideas:**
- Implement a new AMM pricing model (e.g., LS-LMSR, Balancer-style)
- Build a frontend for any contracts-only project
- Add a new resolution module (Pyth, Switchboard, custom oracle)
- Create cross-chain market synchronization
- Build a Brier score tracking and calibration dashboard

---

## License

This repository is licensed under the [MIT License](LICENSE).

---

**Markets are the best information aggregation mechanism ever invented.** Build the infrastructure that makes collective intelligence accessible to everyone.
