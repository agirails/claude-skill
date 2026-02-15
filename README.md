# agirails-agent-payments

**Give your AI agent a wallet. Let it earn and pay USDC — settled on-chain, gasless, in under 2 seconds.**

AGIRAILS is the open settlement layer for AI agents on Base L2. This Claude Code skill gives you interactive onboarding: it asks your preferences, generates production-ready agent code, and verifies your setup. Zero to first transaction in 5 minutes.

## Why This Exists

AI agents need to pay each other. Not with API keys and invoices — with real money, real escrow, real dispute resolution. AGIRAILS handles the hard parts:

| What you get | How it works |
|---|---|
| **Gasless transactions** | Gas sponsored — your agent never needs ETH |
| **USDC settlement** | Real stablecoin, not tokens. $1 = $1. On Base L2. |
| **Encrypted wallet** | Auto-generated keystore (AES-128-CTR, chmod 600, gitignored). No keys in code, ever. |
| **Two payment modes** | ACTP escrow for complex jobs. x402 instant for API calls. Same SDK. |
| **On-chain identity** | ERC-8004 portable identity + reputation. Follows your agent across marketplaces. |
| **10,000 test USDC** | `actp init` in mock mode — start building immediately. Testnet: 1,000 USDC minted gaslessly during registration. |
| **1% transparent fee** | `max(amount * 1%, $0.05)`. Same on both payment paths. No subscriptions. |

## ACTP or x402? Pick the Right Payment Mode

```
Need time to do the work?  →  ACTP (escrow)
  Lock USDC → work → deliver → dispute window → settle
  Think: hiring a contractor

Instant API call?  →  x402 (instant)
  Pay → get response. One step. No escrow. No disputes.
  Think: buying from a vending machine
```

Both modes are in the same SDK. Your agent can use both simultaneously.

## What the Skill Does

When triggered, Claude walks through a **7-step interactive onboarding**:

1. Asks what you want (earn, pay, or both)
2. Asks agent name, network, wallet setup, capabilities, pricing
3. Shows a summary and waits for your explicit "yes"
4. Installs `@agirails/sdk` (TypeScript) or `agirails` (Python)
5. Generates customized agent code from your answers
6. Runs verification (`actp balance`, `actp config show`)
7. Launches your agent

This isn't a reference doc you have to read — it's an onboarding agent that does the work.

## Quickest Path

```bash
# Earn USDC
npx actp init --mode mock
npx actp init --scaffold --intent earn --service code-review --price 5
npx ts-node agent.ts

# Pay another agent
npx actp init --mode mock
npx actp init --scaffold --intent pay --service code-review --price 5
npx ts-node agent.ts
```

Three commands. Mock mode. No keys, no gas, no config. Then graduate to testnet → mainnet when ready.

## Install

### Via aitmpl CLI

```bash
npx claude-code-templates@latest --skill agirails-agent-payments
```

### Manual

```bash
mkdir -p .claude/skills/agirails-agent-payments
curl -sL https://raw.githubusercontent.com/agirails/claude-skill/main/SKILL.md \
  -o .claude/skills/agirails-agent-payments/SKILL.md
```

## What's Inside the Skill

- **Interactive onboarding protocol** — 10 questions with conditional logic, not a wall of text
- **Code templates** — Level 0 (one-liner), Level 1 (Agent class), SOUL pattern (earn + pay)
- **Full ACTP state machine** — 8 states, valid transitions, escrow lifecycle
- **Contract addresses** — Base Sepolia (testnet) + Base Mainnet (production), all 8 contracts
- **Adapter routing** — ACTP (default), x402 (register), ERC-8004 (configure)
- **Anti-patterns** — 4 critical mistakes with wrong/right code examples
- **Sharp edges** — 8 severity-rated issues that will bite you in production
- **24 CLI commands** — full `actp` reference
- **Troubleshooting** — 14 common problems with fixes
- **Pricing model** — cost + margin with auto-negotiation via QUOTED state

## Networks

| | Mock | Testnet (Base Sepolia) | Mainnet (Base) |
|---|---|---|---|
| **Cost to start** | Free | Free (1,000 USDC minted during registration) | Real USDC |
| **Gas** | Simulated | Sponsored (paymaster) or ETH | Sponsored (paymaster) or ETH |
| **USDC** | 10,000 auto-minted | 1,000 minted gaslessly on registration | bridge.base.org |
| **Escrow** | `request()` auto-releases; `client.pay()` manual | Manual `release()` | Manual `release()` |
| **Tx limit** | None | None | $1,000 |

## Trigger Keywords

`agirails`, `ACTP`, `agent payment`, `x402`, `agent escrow`, `@agirails/sdk`, `actp init`, `ERC-8004`, `agent identity`, `agent economy`, `USDC agent`, `provide service`, `request service`

## Links

- [SDK (npm)](https://www.npmjs.com/package/@agirails/sdk) | [SDK (pip)](https://pypi.org/project/agirails/)
- [GitHub](https://github.com/agirails) | [Docs](https://docs.agirails.io) | [Examples](https://github.com/agirails/sdk-js/tree/main/examples)
- Security: security@agirails.io

## License

Apache-2.0
