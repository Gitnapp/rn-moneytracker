# rn-moneytracker

A mobile expense tracker powered by AI. Log income and spending through natural language chat — the AI parses your message and automatically creates a structured record.

## Features

- **AI-powered logging** — describe a transaction in plain text; DeepSeek parses it into a structured record with title, amount, and date
- **Income & expense tracking** — positive amounts for income, negative for spending
- **Chat interface** — conversational UX for adding records
- **Secure auth** — JWT-based authentication with Supabase on the mobile side
- **Cross-platform** — runs on iOS, Android, and web via Expo

## Architecture

```
rn-moneytracker/
├── mobile/          # Expo React Native app
└── backend/         # Express + TypeScript API
```

| Layer    | Tech                                              |
| -------- | ------------------------------------------------- |
| Mobile   | React Native 0.79, Expo 53, Expo Router           |
| Styling  | NativeWind 4 (Tailwind CSS)                       |
| State    | Zustand                                           |
| Auth     | Supabase Auth + JWT                               |
| Backend  | Express 5, TypeScript                             |
| Database | PostgreSQL via Drizzle ORM                        |
| AI       | DeepSeek Chat (`@ai-sdk/deepseek`, Vercel AI SDK) |

## Getting Started

### Prerequisites

- Node.js 18+
- Yarn
- PostgreSQL database
- [DeepSeek API key](https://platform.deepseek.com/)
- Supabase project (for mobile auth)

### 1. Clone

```bash
git clone https://github.com/Gitnapp/rn-moneytracker.git
cd rn-moneytracker
```

### 2. Start the backend

```bash
cd backend
cp .env.example .env   # fill in your values
yarn install
yarn dev
```

See [`backend/README.md`](./backend/README.md) for full setup.

### 3. Start the mobile app

```bash
cd mobile
cp .env.example .env   # set EXPO_PUBLIC_API_URL
yarn install
yarn start
```

See [`mobile/README.md`](./mobile/README.md) for full setup.

## API Overview

| Method | Endpoint   | Description                                 |
| ------ | ---------- | ------------------------------------------- |
| POST   | `/chat`    | Send a message; AI extracts expense records |
| GET    | `/records` | Fetch records for the authenticated user    |
| POST   | `/records` | Create a record manually                    |

## License

MIT
