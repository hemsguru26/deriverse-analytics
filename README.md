# Deriverse Analytics Terminal

> Bloomberg Terminal for DeFi Traders — built on Solana

A trading analytics and journal dashboard for the Deriverse DEX ecosystem. Supports spot, perpetual, and options trading with performance insights, AI coaching, and behavioral pattern detection.

---

## Demo

Open `deriverse-dashboard.html` directly in any modern browser. No installation required.

---

## Features

- Equity curve and drawdown chart
- Win/loss metrics — win rate, profit factor, expectancy, avg win/loss
- Long vs short split with directional PnL
- PnL heatmap calendar (90 days)
- Performance by hour of day and day of week
- Trade duration histogram
- Scatter plot — trade size vs PnL
- Volume by symbol and cumulative fee analysis
- Monte Carlo simulation — 100 forward equity projections
- Risk score (0–100) with behavioral alerts
- Revenge trading and overtrading detection
- AI Coach insights panel
- Trade journal with CSV export
- 90-day mock dataset with 187 trades (demo mode, no wallet required)

---

## Project Structure

```
deriverse/
├── deriverse-dashboard.html    # Main dashboard (open this)
├── src/
│   ├── app/
│   │   └── api/
│   │       ├── trades/route.ts
│   │       ├── analytics/route.ts
│   │       ├── journal/route.ts
│   │       ├── export/route.ts
│   │       └── auth/route.ts
│   ├── lib/
│   │   ├── analytics.ts        # Core calculation engine
│   │   ├── prisma.ts
│   │   ├── auth.ts
│   │   └── rateLimit.ts
│   └── hooks/
│       ├── useTrades.ts
│       ├── useWallet.ts
│       └── useAnalytics.ts
├── prisma/
│   ├── schema.prisma
│   └── seed.ts
├── scripts/
│   └── mockData.ts             # 90-day mock dataset
└── README.md
```

---

## Full Stack Setup (optional)

If you want to run the full Next.js app with a real database:

```bash
npm install
cp .env.example .env.local
npx prisma migrate dev
npx prisma db seed
npm run dev
```

Visit `http://localhost:3000?demo=true`

---

## Environment Variables

```env
DATABASE_URL="postgresql://user:pass@localhost:5432/deriverse"
NEXT_PUBLIC_RPC_URL="https://api.mainnet-beta.solana.com"
NEXT_PUBLIC_DEMO_MODE="true"
JWT_SECRET="your-secret-here"
RATE_LIMIT_PER_MINUTE=100
```

---

## Tech Stack

- Next.js 14 (App Router) + TypeScript
- TailwindCSS + ShadCN UI
- Recharts + custom Canvas charts
- Framer Motion
- Prisma ORM + PostgreSQL
- Solana web3.js + Phantom wallet adapter
- Zod validation + SWR data fetching

---

## Database Models

| Model | Description |
|-------|-------------|
| User | Wallet-based account |
| Trade | Individual trade records |
| Position | Open positions |
| Fee | Fee breakdown per trade |
| Symbol | Trading pairs with market type |
| StrategyTag | User-defined strategy labels |
| JournalNote | Trade annotations and screenshots |
| PerformanceSnapshot | Daily equity snapshots |

---

## API Routes

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/trades?wallet=&demo=true` | Fetch trades |
| POST | `/api/trades` | Record new trade |
| GET | `/api/analytics?wallet=&period=30` | Aggregated stats |
| GET | `/api/journal?wallet=` | Fetch journal notes |
| POST | `/api/journal` | Create journal entry |
| PATCH | `/api/journal/:id` | Update note |
| POST | `/api/auth/verify` | Verify wallet signature |
| GET | `/api/export?wallet=&format=csv` | Export trade data |

---

## Security

- Wallet signature verification only (no private key storage)
- Rate limiting: 100 requests/minute per wallet
- Zod input validation on all API routes
- Secrets managed via `.env.local`

---

## Seed Script

```bash
npx prisma db seed
# Creates: 1 demo wallet, 187 trades over 90 days
# Symbols: SOL-PERP, BTC-PERP, ETH-PERP, SOL-USDC, JUP-PERP, SOL-CALL
```

---

## Key Dependencies

```json
{
  "next": "14.x",
  "typescript": "5.x",
  "@prisma/client": "5.x",
  "recharts": "2.x",
  "framer-motion": "11.x",
  "@solana/web3.js": "1.x",
  "@solana/wallet-adapter-react": "0.x",
  "zod": "3.x",
  "swr": "2.x",
  "date-fns": "3.x"
}
```
