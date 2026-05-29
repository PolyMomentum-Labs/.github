# Security Policy

## Reporting a vulnerability

If you believe you've found a security issue — credential leakage risk, signing/auth bugs, unsafe order execution behavior, or dependency vulnerabilities — **do not** open a public issue.

Send a private report to the maintainers:

- **Email:** security@polymomentum.org *(preferred)*

Include:

- Impact and affected component / repository
- Steps to reproduce
- Proof-of-concept if available (redact all secrets)
- Suggested fix or mitigation if you have one

We aim to acknowledge reports within **72 hours** and will coordinate disclosure responsibly.

## Scope

Security reports are especially important for:

| Area | Examples |
|------|----------|
| **Wallet & auth** | Key derivation, credential handling, signature type mismatches |
| **Order execution** | Unintended orders, stuck loops, unsafe retries, missing cooldowns |
| **Dependencies** | Packages that could lead to RCE or secret exfiltration |
| **Configuration** | Defaults that could cause unintended live trading |

## Safe disclosure

- Do not test against other users' accounts or wallets.
- Do not perform actions that could affect live markets beyond your own test environment.
- Redact private keys, API secrets, and funder addresses in all communications.
