## FourMeme(four.meme) BNB Bundler & Volume bot (BNB Chain)

FourMeme(four.meme) BNB Bundler & Volume bot is a modular, CLI-driven trading toolkit tailored for the Four.meme ecosystem on BNB Chain. It includes specialized modules for mirroring wallets, batching routes, and simulating/measuring volume — all powered directly on-chain with no third‑party market data services.

## Contact

If you have any question or need help, contact here: [Telegram](https://t.me/satscorder) | [Twitter](https://x.com/satcorder33)

## Modules at a glance
- **Bundler**: Execute predefined swap routes (e.g., `WBNB → TOKEN`) with timing controls; designed to extend toward multicalls.
- **Volume Bot**: Programmatic buy/sell loops at a set cadence for liquidity/organic activity testing.
- **Notifications**: Optional Telegram alerts for major lifecycle events.
- **Risk Controls**: Allow/deny lists, max spend ceilings, and basic MEV‑aware settings.

## How it works

### Bundler flow
- Read a sequence of routes from config → execute each respecting slippage/deadline settings → suitable base for multicall-style extensions.

### Volume Bot flow
- Loop on an interval → small buys → approve when needed → partial or full sells → repeat with built‑in rate limiting.

## Getting started

### Prerequisites
- Node.js 18.17 or newer
- A BNB Chain RPC endpoint
- A funded wallet private key

### Install dependencies
```bash
npm install
```

### Environment setup
Copy `env.example` to `.env` and populate the required values. PancakeV2/WBNB mainnet defaults are provided. To enable Telegram notifications (optional), add:
```
TELEGRAM_BOT_TOKEN=123:ABC
TELEGRAM_CHAT_ID=123456789
```

### Sample configurations
You can start from the provided examples and tailor them to your needs:
- `config.sniper.example.json`
- `config.copy.example.json`
- `config.bundle.example.json`
- `config.volume.example.json`

## Build and run
```bash
npm run build
# Sniper (dry-run recommended first)
node dist/index.js sniper -c config.sniper.example.json --dry-run

# Copy-trader
node dist/index.js copy -c config.copy.example.json

# Bundler
node dist/index.js bundle -c config.bundle.example.json

# Volume bot
node dist/index.js volume -c config.volume.example.json
```

Tip: All commands accept standard Node/CLI flags and module‑specific options (see inline `--help`).

## Configuration and safety tips
- Start in dry‑run mode; scale notional size gradually.
- Maintain deny lists and confirm token/router addresses before enabling live trades.
- For fast markets, sniper slippage of 3–8% (300–800 bips) is common; test first.
- For copy‑trading, set both per‑trade caps and a daily max exposure.

## Security best practices
- Never commit secrets or private keys.
- Use a dedicated hot wallet for experimentation.
- Double‑check token and router contract addresses.
- Prefer dry‑run first, then small sizes in production.
