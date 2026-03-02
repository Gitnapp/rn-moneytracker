# backend

Express API for rn-moneytracker. Handles AI-powered expense parsing and record persistence.

## Tech Stack

- **Express 5** — HTTP server
- **TypeScript 5**
- **Drizzle ORM** — type-safe PostgreSQL queries
- **DeepSeek Chat** (`@ai-sdk/deepseek`) — natural language parsing
- **Vercel AI SDK** — `generateText` / `streamText`
- **JSON Web Tokens** — request authentication
- **Zod** — input validation

## Project Structure

```
backend/
├── src/
│   ├── db/
│   │   ├── index.ts        # Drizzle client + query helpers
│   │   └── schema.ts       # Table definitions
│   ├── auth.middleware.ts  # JWT verification
│   ├── chatRoute.ts        # POST /chat — AI parsing endpoint
│   └── recordRoute.ts      # GET/POST /records — CRUD
├── drizzle/                # Migration files
├── drizzle.config.ts
└── index.ts                # App entry point
```

## Database Schema

```ts
records {
  id         serial PRIMARY KEY
  user_id    varchar(255) NOT NULL
  amount     integer      NOT NULL   // negative = expense, positive = income
  title      varchar(255) NOT NULL
  date       timestamp    NOT NULL
  created_at timestamp    DEFAULT now()
}
```

## Setup

### 1. Install dependencies

```bash
yarn install
```

### 2. Configure environment

```bash
cp .env.example .env
```

| Variable           | Description                              |
| ------------------ | ---------------------------------------- |
| `PORT`             | Port to listen on (default: `8000`)      |
| `DATABASE_URL`     | PostgreSQL connection string             |
| `DEEPSEEK_API_KEY` | DeepSeek platform API key                |
| `JWT_SECRET`       | Secret used to sign/verify JWT tokens    |

### 3. Run migrations

```bash
npx drizzle-kit push
```

### 4. Start the server

```bash
# Development (watch mode)
yarn dev

# Production
yarn build && yarn start
```

## API Reference

### `POST /chat`

Requires a valid JWT in the `Authorization` header.

**Request body**

```json
{
  "messages": [{ "role": "user", "content": "bought lunch for 45 yuan" }],
  "user_id": "uuid"
}
```

**Response — record detected**

```json
{
  "text": "",
  "records": { "title": "lunch", "amount": -45, "date": "2025-07-26" }
}
```

**Response — general conversation**

```json
{
  "text": "Sure, anything else you want to track?",
  "records": null
}
```

### `GET /records`

Returns all records for the authenticated user.

### `POST /records`

Creates a record directly (bypasses AI parsing).

## Scripts

| Command      | Description                     |
| ------------ | ------------------------------- |
| `yarn dev`   | Start with nodemon (watch mode) |
| `yarn build` | Compile TypeScript to `dist/`   |
| `yarn start` | Run compiled output             |
