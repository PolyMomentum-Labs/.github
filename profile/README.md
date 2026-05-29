<div align="center">

# PolyMomentum

**Production-grade prediction market trading infrastructure for Polymarket**

[GitHub Organization](https://github.com/PolyMomentum) · [Documentation](#documentation) · [Quickstart](#quickstart)

</div>

---

**PolyMomentum** builds trader-oriented systems for Polymarket — combining quantitative strategy design, automated CLOB execution, and composable tooling for short-horizon and event-driven markets.

This organization profile is the entry point for the **PolyMomentum** GitHub org. Implementation code, bots, and libraries live in sibling repositories below.

---

## What We Build

| Layer | Purpose |
|-------|---------|
| **Trading Logic** | Rule-driven strategies, edge frameworks, and risk controls for prediction markets |
| **Execution Bots** | Polymarket CLOB bots with position management, retries, cooldowns, and circuit breakers |
| **Market Data** | Gamma / CLOB integrations, price polling, market metadata, and analytics pipelines |
| **Operator Tooling** | Config validators, runbooks, health checks, and production hardening utilities |
| **MCP Tooling** *(planned)* | Standardized tool surfaces for market data, order management, and portfolio state |

---

## Documentation

| Section | Description |
|---------|-------------|
| [Getting Started](#quickstart) | Organization overview, prerequisites, and first steps |
| [Architecture](#architecture) | System design, data flow, and component boundaries |
| [Polymarket Integration](#polymarket-integration) | CLOB V2, authentication, market data, and order lifecycle |
| [Trading Logic](#trading-logic) | Strategy taxonomy, configuration, and operational controls |
| [Trading Bots](#trading-bots) | Bot runtime, execution pipeline, and operational playbooks |
| [Security](#security) | Key management, risk controls, and production hardening |
| [Contributing](#contributing) | How to contribute strategies, bots, and tooling |

---

## Repository Map

Current and planned repositories under **PolyMomentum**:

```
PolyMomentum/
├── .github                          ← Organization profile (you are here)
├── polymarket-btc-arbitrage-bot     ← BTC Up/Down 5m/15m CLOB execution bot
├── pm-polymarket-sdk                ← Typed wrappers around CLOB V2 + Gamma API
├── polymarket-copytrading-bot       ← Shared strategy engine, risk, and backtesting
├── pm-bot-runtime                   ← Production bot orchestration and deployment
├── pm-mcp-server                    ← MCP tools for market data and execution
└── pm-market-scanner                ← Market discovery, alerts, and opportunity surfacing
```

Repository names are indicative. See individual repo READMEs for current status.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│  Strategy layer (trade.toml / shared engine)                     │
│  Entry gates · exits · risk limits · cooldowns                   │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  Market data (Gamma + CLOB)                                      │
│  Slug resolution · UP/DOWN quotes · market metadata              │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  Execution (CLOB V2)                                             │
│  L1 auth → API credentials → L2 orders · balances · retries      │
└─────────────────────────────────────────────────────────────────┘
```

---

## Polymarket Integration

| Area | Details |
|------|---------|
| **CLOB** | `@polymarket/clob-client-v2` for authenticated order placement and balance queries |
| **Auth** | L1 wallet signing → derive/create API key → L2 authenticated client |
| **Markets** | Gamma API for slug resolution, token IDs, and market metadata |
| **Windows** | Short-horizon Up/Down markets (5m, 15m, and configurable periods) |
| **Orders** | Market-style FAK execution with transient retry policy and entry cooldowns |

---

## Trading Logic

| Strategy type | Description |
|---------------|-------------|
| **Rule-driven** | Transparent, config-file strategies with auditable entry/exit logic |
| **Short-horizon** | BTC / ETH / SOL / XRP Up/Down windows (5m, 15m, and beyond) |
| **Risk-aware** | Position limits, cooldowns after failed entries, and operator kill-switch workflows |
| **Multi-process** | One market window per process; run 5m and 15m instances independently |

---

## Trading Bots

| Bot | Status | Description |
|-----|--------|-------------|
| [`orderbook-backend`](https://github.com/PolyMomentum/orderbook-backend) | **Active** | TypeScript CLOB bot for Polymarket BTC Up/Down 5m/15m markets — config-driven `trade_1` / `trade_2` strategies, quote polling, and market-style execution |

**Operational model:** one configured market window per process. Run separate instances for 5m and 15m when operating multiple horizons in parallel.

---

## Design Principles

- **Deterministic execution, transparent research** — Strategies are explicit and config-driven; bots execute only validated, rule-based signals.
- **Safety-first operations** — Real capital, real risk. Cooldowns, retries, kill-switch workflows, and clear operator logs are first-class.
- **Production over backtest** — Slippage, latency, rate limits, and capital constraints are design inputs, not afterthoughts.
- **Composable modules** — Shared SDK, core engine, and MCP tooling so each bot stays focused and reusable.
- **MCP-ready tooling** *(planned)* — Capabilities exposed to agents and automation as typed, auditable tool surfaces.

---

## Quickstart

### Prerequisites

- **Node.js ≥ 20.6**
- **Polygon wallet** with Polymarket-compatible setup (private key + funder / proxy address)
- **USDC** balance sized for experimental `trade_usd` settings

### Run the flagship bot

```bash
git clone https://github.com/PolyMomentum/polymarket-btc-5min-15min-arbitrage-trading-bot.git
cd orderbook-backend
npm install
cp .env.example .env   # fill in POLYMARKET_PRIVATE_KEY and POLYMARKET_FUNDER_ADDRESS
# edit trade.toml — set market_period to "5" or "15", choose strategy
npm run dev
```

See the [polymarket-btc-5min-15min-arbitrage-trading-bot README](https://github.com/PolyMomentum/polymarket-btc-5min-15min-arbitrage-trading-bot) for full configuration, runbooks, and troubleshooting.

---

## Quick Links

- [Polymarket CLOB Documentation](https://docs.polymarket.com/)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)
- [Contributing](./CONTRIBUTING.md)
- [Security Policy](./SECURITY.md)

---

## Security

- **Never commit secrets** — private keys, API credentials, or `.env` files.
- **Dedicated wallets** — fund only what you can afford to lose; use isolated trading accounts.
- **Kill-switch procedure** — stop the process, verify open orders, re-check balances.
- Report vulnerabilities privately via [SECURITY.md](./SECURITY.md).

---

## Contributing

We welcome issues and pull requests for strategies, bots, SDK improvements, and tooling.

1. Open an issue describing the use case or bug.
2. Fork the relevant repository and keep changes focused.
3. Include a test plan and confirm no secrets in the diff.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for full guidelines.

---

## License

Software in each repository is licensed individually — check each repo's `LICENSE` or `package.json`. Organization documentation in this profile repository is provided for reference; use all trading software at your own risk.

---

<div align="center">

**Nothing here is financial advice.** Trading prediction markets involves significant risk, including total loss.  
Comply with applicable laws and [Polymarket Terms of Service](https://polymarket.com/tos).

</div>
