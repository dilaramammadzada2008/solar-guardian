# Solar Guardian

**Autonomous crew health & space-weather AI for deep-space missions.**

Built for the **NASA Space Apps Challenge 2026** — challenge *"Create Health Monitoring Software for Astronauts on Space Missions"* — Vilnius local event.

🚀 **Live demo:** https://dilaramammadzada2008.github.io/solar-guardian/

## Pitch

On a mission to the Moon or Mars, the crew can't wait for Earth to diagnose them: a solar
storm can arrive in minutes, and the signal from Mission Control can lag by tens of minutes
or drop out entirely. Solar Guardian is an onboard health monitor that combines space-weather
forecasting with every crew member's vital signs. It learns each astronaut's personal baseline,
spots anomalies and their environmental causes across the whole crew, and acts on its own:
it sends the crew to the storm shelter, runs triage, and keeps a tamper-proof medical record
that syncs with Earth when the link comes back.

## Key features

- **Space-weather-aware radiation forecasting** — predicts crew radiation dose from solar
  activity and automatically triggers a **storm-shelter protocol** before a solar particle event hits.
- **Personal-baseline anomaly detection** — each astronaut is compared to their own normal
  ranges, not to population averages, so subtle changes are caught early.
- **Multi-crew fusion** — correlates readings across the whole crew to find shared
  environmental root causes (for example rising **CO₂**) instead of treating each alert in isolation.
- **ECG arrhythmia detection** — live ECG analysis flags irregular heart rhythms.
- **SHA-256 tamper-proof medical ledger** — every health event is hash-chained, so the
  medical record can't be silently altered.
- **Earth light-delay autonomy** — models the one-way communication delay (and full blackouts
  such as solar conjunction); the system triages autonomously and queues reports for Mission Control.

## How to run

No build step and no installation: it's a single HTML file.

- Open `index.html` in any modern browser, **or**
- Use the live GitHub Pages version: https://dilaramammadzada2008.github.io/solar-guardian/

## How to demo

Click **"Run 60-second pitch demo"** in the app. It walks through a solar storm, the
shelter protocol, a crew anomaly with its root cause, and autonomous operation during an
Earth-link blackout.

## Note

All telemetry (vital signs, ECG, radiation and space-weather data) is **simulated** for
demonstration purposes. Solar Guardian is a hackathon prototype and not a medical device.

## Team — Solar Guardian

- Dilara Mammadzada
- Sayadulla Mammadzada

## License

[MIT](LICENSE)
