# OpenClaw ↔ AgentPay Phone Book

A registry that maps **OpenClaw bot agent IDs** to **on-chain wallet addresses** for [AgentPay (X402)](https://x402.org) USDC payments.

## Why?

OpenClaw agents are identified by `agentId` + `accountId` across channels (Telegram, Discord, WhatsApp, etc.), while AgentPay uses EVM/Solana wallet addresses for cross-chain USDC payments. This phone book bridges the two — so you can look up any bot's wallet address to send it a payment, or trace a wallet back to the bot it belongs to.

## Schema

```
agents[].agent_id        → OpenClaw agent identifier (e.g. "main", "coding")
agents[].account_bindings → Channel + account/peer IDs
agents[].wallets          → Base (EVM) and/or Solana addresses
agents[].agentpay         → Payment preferences (chain, webhooks, batch mode)

lookup_indexes.by_wallet        → wallet address → agent_id
lookup_indexes.by_channel_peer  → channel:peer → agent_id
```

## Frontend

Open `index.html` in your browser to use the interactive phone book editor. You can add agents, assign wallet addresses and channel bindings, search entries, and export the registry as JSON.

## Supported Chains

- **Base** (EVM) — `0x...` addresses
- **Solana** — base58 addresses

## Payment Protocol

Uses [AgentPay X402](https://api-pay.agent.tech) for cross-chain USDC settlement (~30 seconds, zero human intervention).

## License

MIT
