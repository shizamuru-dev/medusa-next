# 🪼 Medusa Next

> **Your clean, fast mobile client for BSU schedule.**  
> Powered by BLoC architecture. Zero bloat, instant offline access.

[![Flutter](https://img.shields.io/badge/Flutter-3.27+-02569B.svg?style=flat-square&logo=flutter&logoColor=white)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.13+-0175C2.svg?style=flat-square&logo=dart&logoColor=white)](https://dart.dev)
[![BLoC](https://img.shields.io/badge/State-BLoC-blue.svg?style=flat-square)](https://bloclibrary.dev)
[![Backend](https://img.shields.io/badge/API-Medusa%20Backend-009688.svg?style=flat-square)](https://github.com/shizamuru-dev/medusa-backend)
[![License](https://img.shields.io/badge/license-MIT-green.svg?style=flat-square)](LICENSE)

[🪆 Russian version](README_RUS.md)

---

## 🎯 Overview

**Medusa Next** is the uncompromising spiritual reboot of the original [**Medusa**](https://github.com/bsu-digital-lab/medusa) concept — reclaiming the project from prompt-generated spaghetti, 0-byte controllers, and green salad-leaf logos.

Built around a simple philosophy: **a schedule app should show your schedule**, not DDoS the university's legacy PHP server from a smartphone, burn battery on fireworks shaders, or double as a volunteer desk-moving dispatch system. Powered by **BLoC** and backed by [**Medusa Backend**](https://github.com/shizamuru-dev/medusa-backend), it brings back the original mythological mascot and delivers pure, instant utility.

## 🧬 Why "Next"?

This repository is an ideological return to the roots of the original **Medusa** architecture:
- **Backend-First, Not Client-DDoS**: Heavy HTML parsing, retries, and Redis caching live on the server — not inside a `setState` loop on your phone.
- **Function Over Fireworks**: No confetti overlays, no `--android-skip-build-dependency-validation` hacks, and no mystery bloatware.
- **Actual Medusa**: Named after the Gorgon who birthed *Pegasus* (BSU's LMS) — featuring an actual jellyfish mascot instead of a stock botanical sprout.

## Offline Caching

Schedule states are automatically persisted on disk using `hydrated_bloc`, while user preferences (selected group, theme preset, favorites) are stored locally via `shared_preferences`.

If the network or upstream server is temporarily unavailable, the app immediately renders the last cached schedule snapshot without blocking the UI.

## ✨ Key Features

- ⚡ **Instant Startup**: Zero blocking network calls in `main()` — renders cached data immediately.
- 🧱 **BLoC Architecture**: Strict separation between data layer, business logic, and dumb UI widgets.
- 📅 **Smart Weeks & Subgroups**: Smooth horizontal week navigation and compact subgroup accordions.
- 🏫 **On-Demand Auditoriums**: Tap any classroom to inspect its live weekly occupancy via backend API.
- 💾 **Offline-First**: Automatic state persistence with `hydrated_bloc` for subway/no-signal access.
- 🎨 **Clean Minimalist UI**: 6 curated color themes including true OLED black, with zero heavy shaders or frame drops.

## 🚀 Quick Start

### Prerequisites

- **Flutter SDK**: `3.27+` (Dart `3.13+`)
- **Backend**: A running instance of [Medusa Backend](https://github.com/shizamuru-dev/medusa-backend)

### Local Development

```bash
# 1. Clone the repository
git clone https://github.com/shizamuru-dev/medusa-next
cd medusa-next

# 2. Install dependencies
flutter pub get

# 3. Run the app (pointing to your backend URL)
flutter run --dart-define=API_BASE_URL=http://localhost:8080

```

### Building Release APK

Clean builds out of the box — no tree-shake workarounds or dependency validation bypasses required:

```bash
flutter build apk --release --dart-define=API_BASE_URL=https://medusa.glitched.network

```

## 📡 Backend Integration

Medusa Next acts as a thin, strictly typed client over **Medusa Backend** REST endpoints:

| Method | Endpoint                         | Usage                                              |
|--------|----------------------------------|----------------------------------------------------|
| `GET`  | `/weeks?action=this_week`        | Resolve current, previous, and next academic weeks |
| `GET`  | `/groups/{id}/schedules/current` | Fetch active week schedule for the student's group |
| `GET`  | `/groups/{id}/schedules?week=15` | Load schedule for a specific academic week         |
| `GET`  | `/auditories/{id}/schedules`     | Fetch on-demand classroom schedule                 |

## 🛠️ Development

### Project Structure

```text
lib/
├── core/
│   ├── api/            # Dio HTTP client, base options & error interceptors
│   ├── di/             # Service locator setup (get_it)
│   ├── storage/        # SharedPreferences wrapper (group, theme, favorites)
│   └── theme/          # 6 color schemes & OLED dark theme definitions
├── features/
│   ├── schedule/       # Main group schedule feature
│   │   ├── data/       # Strictly typed models & ScheduleRepository
│   │   ├── bloc/       # ScheduleBloc, Events & Hydrated States
│   │   └── ui/         # Schedule screen, week pager & lesson cards
│   ├── auditory/       # On-demand classroom schedule feature
│   │   ├── data/
│   │   ├── bloc/
│   │   └── ui/
│   └── settings/       # Group selection & theme switcher
│       ├── bloc/
│       └── ui/
└── main.dart           # App entry point, DI & HydratedStorage initialization

```

### Static Analysis & Tests

The project enforces strict type safety (`strict-casts`, `strict-inference`, `strict-raw-types`) in `analysis_options.yaml`:

```bash
# Run static analyzer
flutter analyze

# Run unit & BLoC tests
flutter test

```

## 🛡️ Configuration

Build-time environment variables passed via `--dart-define`:

* **`API_BASE_URL`**: Base URL of your Medusa Backend instance (defaults to `http://10.0.2.2:8080` for Android emulator).
* **`APP_ENV`**: Environment tag (`dev` / `prod`).

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'feat: add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.

---

<div align="center">
  <sub>Made with ❤️ for BSU students</sub>
</div>
