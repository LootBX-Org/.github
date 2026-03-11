# LootBX Platform

LootBX is an interactive live-streaming platform that connects streamers and viewers through a real-time rewards economy. Viewers earn coins by watching, completing quests, and participating in raffles — then spend them in the Reward Shop. Streamers engage their audience by dropping loot live on stream, running giveaways, and building loyal communities.

---

## Platform Overview

The LootBX platform is composed of two client applications sharing a common backend.

| | Web App | Mobile App |
|---|---|---|
| **Audience** | Desktop & browser users | iOS & Android users |
| **Technology** | React + Vite (PWA-capable) | React Native + Expo |
| **Deployment** | GitHub Actions → hosted web | EAS Build → App Store / Play Store |

---

## Core Features

### For Viewers
- **Live Streams** — Browse and watch live streams across categories
- **Loot Drops** — Claim real-time rewards dropped by streamers during live broadcasts
- **Daily Quests & Streaks** — Complete daily tasks to earn bonus coins and maintain streaks
- **Raffle & Roulette** — Enter raffles and spin for prizes using earned coins
- **Reward Shop** — Redeem coins for real prizes, in-game items, and exclusive rewards
- **Leaderboards** — Compete with other viewers for top supporter rankings
- **Inventory** — Track and manage all claimed loot and earned rewards
- **Wallet** — View coin balance, transaction history, and process withdrawals
- **Reels** — Short-form highlight clips from streamers

### For Streamers
- **Streamer Dashboard** — Centralized hub for managing the entire streaming operation
- **Analytics** — Viewer counts, engagement metrics, and performance charts
- **Live Control Room** — Manage stream, drop loot, moderate chat, and monitor activity in real time
- **Stream Setup** — Configure stream title, category, tags, and retrieve stream key
- **Moderation Tools** — Mute users, ban words, and enforce chat standards
- **Live Gifts & Donations** — Receive animated gifts from viewers during broadcasts
- **Events & Giveaways** — Create and manage in-stream reward events
- **Alerts** — Configurable on-screen alerts for follows, subscriptions, and donations
- **OBS Integration** — Browser-source overlays for chat, activity feed, loot drops, and stream preview
- **Reels Studio** — Upload, edit, and manage short-form content

### For Admins
- **Admin Dashboard** — At-a-glance overview of users, streams, shop items, news, and streamer/tier snapshots
- **User Directory** — Browse verified and unverified users with profile preview, inventory, and loot point history
- **Streamer Request Management** — Review, approve, or reject incoming streamer applications
- **Streamer Account Management** — Full lifecycle control: create, edit, suspend, reinstate, and delete streamer accounts
- **Streamer KPI Monitoring** — Track streamer performance against deliverables and KPI targets with exportable reports
- **Tier Management** — Configure tier structures, levels, KPI thresholds, incentives, and assign streamers
- **Live Stream Control** — Monitor live streams, moderate chat in real time, and terminate streams with password confirmation
- **Shop Management** — Create, edit, and manage shop items, pricing, and availability
- **Item Management** — Maintain the master inventory item catalog across the platform
- **Bundle Management** — Create and manage item bundles for shop and inventory use
- **Loot Chest Management** — Define chest types, configure reward payloads, and manage chest lifecycle
- **News Management** — Publish, edit, and manage platform news articles and announcements
- **Admin Account Settings** — Update admin profile, credentials, and security settings

---

## Getting Started

### Web App

```bash
cd lootbx

npm run dev           # Local development
npm run build:prod    # Production build
npm run preview       # Preview the production build locally
```

### Mobile App

```bash
cd lootbx-mobile

npx expo start                   # Start development server
npx expo start --tunnel          # Use if direct connection fails
npx expo start --tunnel --clear  # Clear cache and restart

npx expo run:android             # Build and run on Android
npx expo run:ios                 # Build and run on iOS
```

---

## Project Structure

Each application is a self-contained repository with its own dependencies and configuration.

```
lootbx/
├── lootbx/          → Web application
└── lootbx-mobile/   → Mobile application
```

### Web App (`lootbx/`)

| Area | Purpose |
|---|---|
| `src/pages/` | All user-facing, streamer-facing, and admin-facing screens |
| `src/pages/streamer/` | Streamer dashboard — analytics, control room, moderation, studio |
| `src/pages/admin/` | Admin dashboard — user directory, streamer management, shop, items, tiers, news |
| `src/components/` | Shared UI components used across pages |
| `src/lib/api/` | All API communication with the backend |
| `src/store/` | Global application state (Zustand) |
| `src/hooks/` | Reusable logic and data-fetching hooks |
| `src/routes/` | Route definitions and access control |
| `public/` | Static assets, PWA manifest, splash screens |
| `.github/workflows/` | Automated deployment pipelines |

### Mobile App (`lootbx-mobile/`)

| Area | Purpose |
|---|---|
| `app/` | All screens, organized by Expo Router file-based routing |
| `app/(tabs)/` | Main bottom navigation — Home, Discover, Search, Streams, Profile |
| `app/(streaming)/` | Live stream viewing experience |
| `components/` | Shared UI components |
| `api/` | All API communication with the backend |
| `store/` | Global application state (Zustand) |
| `hooks/` | Reusable logic and data-fetching hooks |
| `services/` | Push notification handling |
| `android/` `ios/` | Native platform projects |

---

## Access Control

LootBX has four user roles, each with different levels of access.

| Role | Access |
|---|---|
| **Guest** | Browse homepage, view public streamer profiles, watch streams |
| **User** | Full viewer experience — quests, rewards, shop, wallet, inventory |
| **Streamer** | Everything above, plus the full streamer dashboard at `/streamer` |
| **Admin** | Platform management — user directory, streamer approvals, KPI monitoring, shop/item/bundle/chest management, live stream control, news publishing, and tier configuration at `/admin` |

OBS browser-source overlay pages are fully public and require no authentication — they are accessed directly by streaming software using the streamer's username.

---

## Infrastructure & Deployment

- **Real-time** — Both applications connect to a shared WebSocket server (Socket.IO) for live chat, loot drops, gift animations, viewer counts, and notifications
- **Video Delivery** — Web uses HLS streaming; mobile uses Amazon IVS for low-latency broadcast playback
- **Authentication** — JWT-based, with email verification and reCAPTCHA on sign-up
- **Encryption** — API requests are encrypted; see [Encryption Guide](lootbx/ENCRYPTION_USAGE_GUIDE.md)
- **Web Deployment** — Automated via GitHub Actions for staging and production environments
- **Mobile Deployment** — Managed builds and OTA updates via Expo Application Services (EAS)
- **PWA** — The web app is installable on desktop and mobile browsers, including iOS

---

## Documentation

| Document | Description |
|---|---|
| [PWA Guide](lootbx/PWA_README.md) | Installing and testing the web app as a PWA |
| [iOS PWA Guide](lootbx/iOS_PWA_GUIDE.md) | PWA installation instructions for iOS users |
| [Encryption Guide](lootbx/ENCRYPTION_USAGE_GUIDE.md) | How API request encryption works |
| [Encryption Keys Setup](lootbx/ENCRYPTION_KEYS_SETUP.md) | Generating and configuring encryption keys |
| [reCAPTCHA Setup](lootbx/RECAPTCHA_SETUP.md) | Configuring reCAPTCHA v3 for sign-up protection |
| [Socket Rate Limiting](lootbx/SOCKET_RATE_LIMITING_FIX.md) | WebSocket performance and rate limiting notes |
| [Admin Features](ADMIN_FEATURES.md) | Full list of admin dashboard features and capabilities |
| [Mobile Dev Guide](lootbx-mobile/DEV_INSTRUCTIONS) | Quick-reference commands for mobile development |
