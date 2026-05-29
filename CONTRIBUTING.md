# Contributing to PolyMomentum

Thank you for helping build open-source Polymarket trading infrastructure.

## How to contribute

| Type | What to do |
|------|------------|
| **Bug reports** | Open an issue with repro steps, logs (redact secrets), and expected vs actual behavior |
| **Feature requests** | Describe the use case, constraints, and what success looks like |
| **Pull requests** | Link an issue when possible; include a concise test plan |

## Development standards

- **Never commit secrets** — private keys, API keys, `.env` files, or wallet addresses tied to real identities.
- **Keep changes focused** — small, reviewable PRs are safer to ship in trading systems.
- **Prefer explicit configuration** over implicit defaults for trading behavior.
- **Document risk controls** — timeouts, max exposure, kill-switch behavior, retry policies, and cooldown semantics.
- **Match existing conventions** — naming, module layout, and config patterns in each repository.

## PR checklist

- [ ] Clear description of the change and motivation
- [ ] Updated docs / README if behavior changes
- [ ] Test plan included (commands run, mocks used, or manual steps)
- [ ] No secrets committed (double-check diffs)
- [ ] Risk implications noted for execution or auth changes

## Scope

We welcome contributions across:

- Trading strategies and rule engines
- CLOB / Gamma integrations and SDK wrappers
- Bot runtime, monitoring, and deployment tooling
- MCP tool surfaces for market data and execution
- Documentation, runbooks, and operational playbooks
