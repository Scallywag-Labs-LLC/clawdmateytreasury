# Security Model

## Overview

Clawdmatey is designed with a **zero-secrets-in-repo** security model. All sensitive credentials are loaded at runtime from secure sources.

## Credential Storage

| Credential | Storage Location | Never In Repo |
|------------|------------------|---------------|
| Private keys | 1claw vault API | ✅ |
| API keys | `~/.openclaw/clawdmatey.env` | ✅ |
| Twitter/X auth | `~/.xurl/` | ✅ |
| Bankr config | `~/.clawdbot/` | ✅ |

## How It Works

1. **Private Keys**: Fetched from 1claw vault at runtime via authenticated API call
2. **API Keys**: Loaded from `~/.openclaw/clawdmatey.env` (local file, gitignored)
3. **No hardcoded secrets**: All addresses in config are public contract addresses (safe to share)

## Blocked Contracts

The `blockedContracts` list in `config.json` prevents interaction with known honeypots/scams. This list is checked before every Bankr call.

## Audit Checklist

Before running:
- [ ] `~/.openclaw/clawdmatey.env` exists with valid credentials
- [ ] 1claw vault is configured with wallet private key
- [ ] No `.env` files in repo directory
- [ ] `git status` shows no untracked secret files

## Reporting Issues

If you discover a security vulnerability, please report it privately — do not open a public issue.

## What's Safe to Share

- Contract addresses (these are public on-chain)
- Token symbols and chain IDs
- Portfolio allocation percentages
- Run history (`runs.md`)

## What's NOT Safe

- Private keys
- Seed phrases / mnemonics
- API keys
- Auth tokens
- Wallet balances (operational security)
