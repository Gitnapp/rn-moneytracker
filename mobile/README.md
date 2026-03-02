# mobile

React Native client for rn-moneytracker, built with Expo.

## Tech Stack

- **Expo 53** with Expo Router (file-based routing)
- **React Native 0.79** (new architecture enabled)
- **NativeWind 4** — Tailwind CSS for React Native
- **Zustand** — lightweight state management
- **Supabase JS** — authentication
- **Vercel AI SDK** — streaming AI responses
- **Zod** — runtime schema validation

## Project Structure

```
mobile/
├── app/
│   ├── (tabs)/
│   │   ├── index.tsx      # Home — expense feed
│   │   ├── explore.tsx    # AI chat interface
│   │   └── profile.tsx    # User profile
│   ├── Auth.tsx           # Login / signup screen
│   └── _layout.tsx        # Root layout
├── components/
│   ├── RecordCard.tsx     # Expense/income list item
│   └── ...                # Shared UI components
├── hooks/                 # Custom React hooks
├── lib/                   # Supabase client, utilities
└── constants/             # Theme tokens, config
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

| Variable               | Description                        |
| ---------------------- | ---------------------------------- |
| `EXPO_PUBLIC_API_URL`  | Base URL of the backend API        |

Supabase credentials are configured inside `lib/supabase.ts`.

### 3. Run the app

```bash
# Start Expo dev server
yarn start

# Platform-specific
yarn ios
yarn android
yarn web
```

Scan the QR code with **Expo Go** or run in a simulator/emulator.

## Scripts

| Command               | Description                        |
| --------------------- | ---------------------------------- |
| `yarn start`          | Start the Expo dev server          |
| `yarn ios`            | Open in iOS simulator              |
| `yarn android`        | Open in Android emulator           |
| `yarn web`            | Open in browser                    |
| `yarn lint`           | Run ESLint                         |
| `yarn reset-project`  | Reset to blank app scaffold        |
