# OfflineQueue — Smart Offline Content Sync for Android

A personal, offline-first Android app that syncs your YouTube subscriptions and playlists during scheduled windows (e.g. overnight WiFi), so you can browse a fresh, organized feed even with no signal while traveling — without wasting mobile data.

## 🎯 Problem

Traveling often means unreliable or expensive mobile data. Existing apps assume you're always connected. **OfflineQueue** solves this by syncing lightweight metadata (titles, thumbnails, descriptions) during a window you control — like late at night on WiFi — so you always have something fresh to browse offline, with old content automatically cleaned up.

## ✨ Features

- 🔄 **Scheduled background sync** using Android WorkManager — runs only under conditions you set (e.g. WiFi-only, specific time window)
- 📦 **Local-first storage** via Room (SQLite) — your feed works fully offline
- 🧹 **Automatic expiry** — content older than a configurable threshold is purged automatically, keeping storage lean
- 📊 **Data budget controls** — cap how much is synced per session
- 🔐 **OAuth-based login** — signs in with the user's own Google account via the official YouTube Data API v3; no scraping, no third-party credential handling
- 🕒 **Honest sync state** — every screen clearly shows "Last synced: X hours ago" rather than pretending to be live

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose |
| Local storage | Room (SQLite) |
| Background jobs | WorkManager |
| Networking | Retrofit + OkHttp |
| Auth | Google OAuth 2.0 (Sign-In for Android) |
| Image loading/caching | Coil |
| API | YouTube Data API v3 |

## 🏗️ Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  WorkManager     │────▶│  YouTube Data API │────▶│  Room Database  │
│  (scheduled job) │     │  v3 (metadata)    │     │  (local cache)  │
└─────────────────┘     └──────────────────┘     └────────┬────────┘
                                                              │
                                                              ▼
                                                   ┌─────────────────┐
                                                   │  Compose UI      │
                                                   │  (offline feed)  │
                                                   └─────────────────┘
```

## 📋 Project Status

🚧 **In active development** — this is a learning + portfolio project exploring offline-first Android architecture, background scheduling, and working within official platform APIs (as opposed to scraping).

- [x] Project planning & architecture design
- [ ] Google OAuth integration
- [ ] YouTube Data API sync layer
- [ ] Room database schema
- [ ] WorkManager scheduled sync
- [ ] Compose UI for offline feed
- [ ] Auto-expiry job
- [ ] Data budget settings screen

## 🎓 What I Learned Building This

- Working with official OAuth flows and API quotas instead of scraping
- Designing an offline-first architecture (local DB as source of truth, network as a sync layer)
- Android background task scheduling with WorkManager constraints
- Balancing user data budgets against API rate limits

## ⚖️ A Note on Ethics & ToS

This project deliberately uses **only official, sanctioned APIs** (YouTube Data API v3) with proper OAuth consent — no scraping, no bypassing platform restrictions, no impersonating a live connection. It syncs metadata the signed-in user already has access to, on a schedule they control.

## 🚀 Getting Started

```bash
git clone [https://github.com/ManasBhahada/offline-queue.git](https://github.com/ManasBhahada/offline-queue.git)
cd offline-queue
```

1. Create a project in [Google Cloud Console](https://console.cloud.google.com/)
2. Enable the **YouTube Data API v3**
3. Create OAuth 2.0 credentials for an Android app
4. Add your `google-services.json` to the `app/` directory
5. Open in Android Studio and run

## 📄 License

MIT — free to use, modify, and learn from.

---

*Built as a portfolio project exploring offline-first mobile architecture and ethical API usage.*
