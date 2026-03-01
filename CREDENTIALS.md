# Credentials Reference — Not4Sale Ecosystem

> **Purpose**: Pointers to where credentials live. NO SECRETS ARE STORED IN THIS FILE.
> **Last Updated**: 2026-02-27

---

## GitHub

- **Organization**: linczyc-MLX
- **Token management**: GitHub Settings → Developer settings → Personal access tokens (fine-grained)
- **N4S token scope**: N4S repo read/write, Actions
- **Claude-memory token scope**: claude-memory repo read/write
- **Superpowers token scope**: Superpowers repo read-only

## IONOS

- **Hosting panel**: https://my.ionos.com
- **GitHub Secrets** (set in N4S repo → Settings → Secrets):
  - `IONOS_API_KEY` — IONOS deployment
  - `IONOS_SSH_KEY` — IONOS SSH access
  - `FTP_PASSWORD` — FTP deployment to website.not-4.sale
  - `DB_PASSWORD` — MariaDB/MySQL password
  - `REACT_APP_RAPIDAPI_KEY` — RapidAPI key for KYM live property data

## VPS (74.208.250.22)

- **SSH**: root@74.208.250.22 (key-based auth)
- **PostgreSQL**: Local on VPS, password in environment files
- **PM2 processes**: n4s-rfq-api, luxebrief, parker-api, mlx-consulting, mailflow, prompt-architect
- **SSH key**: `~/.ssh/parker_vps` (ed25519, added 2026-03-01)
- **Environment files**: `.env` in each service directory on VPS

## RapidAPI

- **Account**: Linked to Michael's email
- **Key**: Stored as GitHub Secret `REACT_APP_RAPIDAPI_KEY`
- **Used by**: KYM module for live property listings

## AI Services

- **Anthropic (Claude)**: API key on VPS for Parker Phase 2
- **OpenAI**: API key in Luxebrief .env for Whisper transcription + GPT report generation

## Luxebrief Admin

- **Admin panel**: /admin route
- **Default token**: configurable via `ADMIN_TOKEN` env var on VPS

---

## Rules

1. **Never commit secrets to any repo.** Use GitHub Secrets, .env files on VPS, or environment variables.
2. **Tokens are repo-scoped.** A token for N4S may not work for claude-memory or Superpowers.
3. **If a clone fails with auth error**, the token likely needs regeneration or the scope needs expanding.
4. **Michael provides tokens at session start** when needed. Don't hardcode them in memory files.

---

*This file tells you WHERE to find credentials, not WHAT they are.*
