# QSense Factory

Privacy-first, distributed edge-AI predictive maintenance and safety system for MSME manufacturers — built for the Snapdragon Multiverse Hackathon.

Legacy machinery can't afford cloud subscriptions or send proprietary process data off-site. QSense Factory runs entirely on-premises across three devices that form a **closed loop**, not a one-way pipeline:

```
Detect  ──►  Alert  ──►  Diagnose  ──►  Resolve
  │                                        │
  └────────────── baseline reset ◄─────────┘
```

| Stage | Device | Submodule | What it does |
|---|---|---|---|
| **Detect** | Arduino UNO Q | [`Node`](./Node) | Magnetically-attached sensor continuously monitors motor vibration offline and flags anomalies with a local TinyML model. |
| **Alert** | Snapdragon Copilot+ PC | [`Web`](./Web) | Runs NPU-accelerated PPE (safety gear) compliance detection on a live camera feed, hosts the MQTT broker, logs events, and serves the admin dashboard. |
| **Diagnose → Resolve** | Technician's mobile device | [`App`](./App) | Receives alerts and runs a local vision-language model to turn a photo of the machine into repair guidance. |

When the technician resolves an issue on their phone, that signal flows back through the PC to clear the dashboard and reset the Arduino's vibration baseline — completing the cycle. No step in this loop requires an internet connection.

## Repository layout

This repo is a thin wrapper around three independent projects, each pinned as a git submodule tracking its own `main` branch:

- **`App/`** — [QSense-App](https://github.com/VibeCheck-Q/QSense-App): Kotlin Multiplatform Android app (mobile diagnose/resolve client)
- **`Node/`** — [QSense-Node](https://github.com/VibeCheck-Q/QSense-Node): Arduino UNO Q firmware + Python backend + dashboard (vibration detection)
- **`Web/`** — [QSense-Web](https://github.com/VibeCheck-Q/QSense-Web): FastAPI hub + MQTT broker + React dashboard (PPE detection, alerting, orchestration)

Each submodule has its own README with full setup and architecture details — start there once you know which piece you're working on.

## Getting started

Clone with submodules in one step:

```bash
git clone --recurse-submodules git@github.com:VibeCheck-Q/QSense.git
```

If you've already cloned without that flag:

```bash
git submodule update --init --recursive
```

Pull in the latest commit from each submodule's tracked branch:

```bash
git submodule update --remote
```

## License

Each submodule carries its own license — see the respective repo for details.
