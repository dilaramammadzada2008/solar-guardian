# Solar Guardian

**An autonomous onboard medical officer for deep-space crews: it watches the Sun and the astronauts' bodies together, and acts when Earth is too far away to help.**

Built for the **NASA Space Apps Challenge 2026**, challenge *"Create Health Monitoring Software for Astronauts on Space Missions"*, Vilnius local event. Team **Solar Guardian**.

> **Simulated telemetry, real sensing.** All crew, ship and space-weather data in the mission view is simulated, using real reference scales (NASA career dose limit, NOAA storm scale, water shielding). The **live heart sensor** measures a real person through the laptop or phone camera.

---

## Contents

1. [The problem](#1-the-problem)
2. [What Solar Guardian does](#2-what-solar-guardian-does)
3. [Quick start](#3-quick-start)
4. [Tour of the interface](#4-tour-of-the-interface)
5. [Mission scenarios](#5-mission-scenarios)
6. [How Guardian thinks](#6-how-guardian-thinks)
7. [Live heart sensor: measuring a real person](#7-live-heart-sensor-measuring-a-real-person)
8. [Evidence: how we know the measurement is correct](#8-evidence-how-we-know-the-measurement-is-correct)
9. [Security: tamper-proof medical ledger](#9-security-tamper-proof-medical-ledger)
10. [Science and reference values](#10-science-and-reference-values)
11. [Honest limitations](#11-honest-limitations)
12. [Roadmap](#12-roadmap)
13. [Technical overview](#13-technical-overview)
14. [Use of AI tools](#14-use-of-ai-tools)
15. [References](#15-references)
16. [Team and license](#16-team-and-license)

---

## 1. The problem

On the way to Mars a radio signal needs **14 min 32 s** to reach Earth one way, so a question and its answer take **29 minutes**. During a solar conjunction the link can be lost for about two weeks.

Space is dangerous on a much shorter clock:

- A **solar particle event** can deliver a large radiation dose to an unprotected crew. The flare's X-rays arrive in about 8 minutes; the energetic protons follow minutes to hours later. That gap is the only warning window.
- A **silent arrhythmia** (atrial fibrillation) can go unnoticed until the next scheduled check.
- A **failing CO₂ scrubber** slowly degrades the whole crew's thinking, and looks like four separate medical problems.

Today's health dashboards display numbers and wait for a human. On a deep-space mission there may be no one on Earth to answer in time. **The crew needs a system that can understand, decide and act onboard, and explain why.**

## 2. What Solar Guardian does

| Capability | What it means |
|---|---|
| **Space-weather-aware radiation protection** | Detects a flare while it is still rising, forecasts every astronaut's dose per module, aborts spacewalks and sends the crew to the water-walled storm shelter before the protons arrive. |
| **Personal-baseline anomaly detection** | Compares each astronaut with their *own* normal, learned over 142 mission days, not with population averages. Expected changes (a heart-rate rise during a spacewalk) are not flagged. |
| **Multi-crew fusion** | When all crew drift at the same time in the same direction, Guardian concludes the cause is the cabin (CO₂), not four bodies, and fixes the cause. |
| **ECG arrhythmia detection** | Finds a hidden atrial fibrillation from beat-to-beat irregularity on a live ECG trace and alerts the flight surgeon. |
| **Dose-aware mission planning** | Tracks each career dose against NASA's 600 mSv limit and reassigns spacewalks before anyone would exceed it. |
| **Earth light-delay autonomy** | Decides onboard, queues every decision for Mission Control, and keeps working when the link is lost. A human can switch autonomy off and approve each action. |
| **Explainable decisions** | Every decision shows its evidence ("Why Guardian thinks so"), a confidence value and recommended actions. |
| **Tamper-proof medical ledger** | Every decision is written into a SHA-256 hash chain; editing any past record is detected. |
| **Live heart sensor** | Measures a real person's heart rate with the camera: fingertip or contactless from the face. |
| **Voice and alarm tones** | Critical events trigger an alarm and a spoken alert. |

## 3. Quick start

No installation, no build step, no server: it is a single HTML file.

1. Download the repository (green **Code** button, then **Download ZIP**) and unzip it.
2. Open **`index.html`** in **Google Chrome** or **Microsoft Edge** (needed for the camera and voice).
3. Click **"▶ Run 60-second pitch demo"**.

Live version (GitHub Pages, available when the repository is public): https://dilaramammadzada2008.github.io/solar-guardian/

**Before every presentation:** press **↺ Reset mission**, then switch **Voice: ON** with a real click (browsers only allow sound after a user click).

## 4. Tour of the interface

**Header.** Mission clock (day 142 of 500), Earth link delay (14m 32s, or *LOST · AUTONOMOUS*), current space weather (flare class and NOAA S-level), total radiation dose averted, simulation speed (1×, 5×, 20×), **Autonomy** and **Voice** switches.

**Sun · space weather.** Animated Sun (SDO-like, simulated), X-ray flare class (A, B, C, M, X; each class 10× stronger), proton flux ≥10 MeV in pfu, NOAA radiation storm level (S0–S4), solar wind speed, and a log-scale proton chart with the S1 threshold (10 pfu) as a dashed line. Status chip: *QUIET*, *SEP INBOUND · T-countdown*, or *RADIATION STORM S1–S4*.

**Cabin environment.** CO₂ (green below 3,000 ppm, amber above 3,000, red above 4,000), O₂, pressure, temperature, and which CO₂ scrubber is active with its efficiency.

**Deep-space habitat map.** Crew quarters (HAB), laboratory (LAB), the **storm shelter** with a 20 g/cm² water wall, airlock and the EVA worksite outside the hull, each with its live dose rate in mSv/h. Crew members move between modules. Purple streaks are galactic cosmic rays (they pass through everything); during a storm, yellow solar protons fill the map and stop at the water wall. The **ECLSS · CO₂ scrubbers** block shows scrubbers A and B: *STANDBY*, *ACTIVE*, pulsing red *FAULT*, or *OFFLINE · INSPECT*.

**Physiological telemetry.** For the selected astronaut: a live ECG (lead II, 25 mm/s), heart rate, SpO₂, HRV and dose-rate trends against the personal baseline, and the context (rest, moving, EVA exertion, irregular rhythm).

**Crew digital twins.** One card per astronaut with seven signals (HR, SpO₂, HRV, temperature, respiration, cognition, radiation dose), the Guardian risk ring (NOMINAL, WATCH, ALERT), and a career-dose bar with a tick for the projected end-of-mission dose. A fifth **Guest (live)** card appears when a real person is measured.

**Bottom row.** *Guardian AI · decision log* (newest first, with AUTO tags or approval buttons), *Autonomous triage* (title, confidence, evidence, recommended actions, Earth reply time), *Tamper-proof medical ledger* (blocks with hashes, **Verify chain**, **Simulate tampering**) and *Earth uplink queue* to MCC Houston (*in transit*, *received*, *held · no link*).

## 5. Mission scenarios

Each button injects an event. **Guardian is not told about it**; it has to detect the event from its sensors.

| Button | What happens | What Guardian does |
|---|---|---|
| **▶ Run 60-second pitch demo** | Runs EVA → solar storm → CO₂ fault → arrhythmia in sequence. | Everything below, automatically. |
| **☀ Solar particle event (X-class flare)** | A flare erupts; protons arrive about 25 simulated minutes later and peak around NOAA S3. | Forecasts dose per module (in the demo: HAB 21.0, shelter 3.8, EVA 67 mSv), aborts the EVA if ingress is faster than proton arrival, orders the shelter protocol, counts the dose averted, gives *ALL CLEAR* when flux falls below S1. |
| **⛑ Start EVA — Aylin** | Aylin goes outside; her heart rate rises. | Switches to context-aware thresholds, so no false alarm. Refuses an EVA during a storm. |
| **♥ Hidden cardiac arrhythmia — Jonas** | Jonas develops atrial fibrillation he does not feel. | Detects irregular beat-to-beat intervals, raises an ALERT, alerts the flight surgeon with evidence and actions. |
| **≋ CO₂ scrubber degradation** | The active scrubber drops to 52% efficiency; CO₂ rises. | Sees 4/4 crew drifting together, names the cabin as the root cause, switches to the backup scrubber and flags the faulty one for inspection. Works repeatedly (B → A → B). |
| **♥ Live heart sensor — guest** | Opens the camera sensor. | Measures a real person and adds them as a live crew card. |
| **⌁ Cut Earth link** | Simulates solar conjunction. | Keeps working; messages wait as *held · no link* until the link returns. |
| **↺ Reset mission** | Restarts everything. | |

Tip: show the CO₂ scenario at **1×** speed so the red *FAULT* state is visible before Guardian switches.

## 6. How Guardian thinks

Guardian is the decision engine inside the app. It is deliberately **explainable**: rules and statistics whose reasoning can be shown to a flight surgeon, rather than a black box.

**Personal baselines.** For heart rate, SpO₂ and HRV each astronaut has a running mean and variance (exponentially weighted). Every new value becomes a z-score against that person's own normal. The baseline does **not** learn during an EVA, an arrhythmia, or when a value is already abnormal (|z| ≥ 3), so anomalies cannot become the new normal.

**Risk fusion.** Each astronaut's risk score (0–100) combines heart-rate deviation (ignored during expected exertion), low SpO₂ (< 94%), a detected arrhythmia, current radiation dose rate, a projected career dose above 600 mSv and reduced cognition. Score ≥ 28 is **WATCH**, ≥ 55 is **ALERT**.

**Multi-crew fusion.** If cabin CO₂ exceeds 3,900 ppm and at least 3 of 4 crew show heart-rate deviation or reduced cognition at the same time, Guardian reports one environmental root cause instead of separate medical alarms.

**Arrhythmia.** An RR-interval irregularity index above 0.12 (personal baseline 0.03), at rest and outside an EVA, is reported as suspected atrial fibrillation.

**Radiation.** Dose rate per module = solar proton rate × module shielding factor + galactic background. The storm shelter lets through about 18% of the HAB's solar proton dose (about **5.5× lower**); the EVA worksite gets 3.2× the HAB dose. Career dose is projected to the end of the 500-day mission at 0.9 mSv/day.

**Autonomy.** With *Autonomy: ON* Guardian executes protocols itself (AUTO tag). With *Autonomy: OFF* it recommends and waits for the crew to press the action button. Every event goes to the decision log and the ledger; warnings, critical events and decisions are also queued for Mission Control.

**Confidence values** shown in the triage panel (91%, 87%, 94%) are fixed per scenario in this prototype to illustrate the concept. In a real system they would be calibrated on validation data.

## 7. Live heart sensor: measuring a real person

Everything in the mission view is simulated. The live heart sensor is not: it measures the person in front of the camera.

### Principle: photoplethysmography (PPG)

Every heartbeat pushes a wave of blood into the skin. More blood absorbs more light, so the skin's colour changes very slightly with each beat, too little for the eye, but measurable by a camera at 30 frames per second. Hospital pulse oximeters and smartwatches use the same principle.

### Two modes

| |  **Fingertip** |  **Face · contactless (rPPG)** |
|---|---|---|
| How | Fingertip covers the camera; light shines through the tissue (phone flashlight, or a light behind the finger on a laptop). | Camera looks at the face; forehead and both cheeks are measured. |
| Signal | Mean **red** value of the fingertip. Strong signal. | Mean **red, green, blue** of the skin regions, combined with the **POS** algorithm (Wang et al., 2017), which cancels brightness changes that affect all colours equally. Weaker signal. |
| Typical time to first reading | 6–10 s | 10–15 s |
| HRV | Rough estimate (marked ≈) | Not shown |

### Processing pipeline

1. **One number per frame.** The video is reduced to the average colour of the measured region; no image is stored or sent.
2. **Uniform resampling** to 30 Hz over a 12 s (fingertip) or 15 s (face) window.
3. **Band-pass filter** to the heart-rate range (0.5–4 Hz for fingertip, 0.6–3.3 Hz for face), applied forwards and backwards so the wave is not shifted in time.
4. **Method 1, spectrum:** the strongest rhythm between 40 and 200 bpm (180 for face), with a **harmonic check**: a pulse wave has strong harmonics, so if half or a third of the peak rate also carries real power, the lower rate is taken as the heart rate.
5. **Method 2, beat peaks:** individual beats are found in the time domain (with sub-frame precision); the median beat-to-beat interval gives a second heart rate.
6. **Agreement:** a reading counts only if both methods agree within 10 bpm and the signal-to-noise ratio is high enough.
7. **Stability:** a number is displayed only when the last 3–4 accepted readings lie within 8 bpm of each other.
8. **Quality checks:** finger not covering / too dark / too bright; face not in the oval / too dark / moving. When a check fails the app tells the user what to do instead of guessing.

### Using it in the app

1. Click **♥ Live heart sensor — guest**, allow the camera.
2. Choose **Fingertip** or **Face · contactless**.
3. Hold still. When a stable number appears, click **Add to crew**.
4. A **Guest (live)** card shows the real heart rate, signal quality and a Guardian comment (normal resting range 50–100 bpm); Guardian logs the measurement and, with voice on, announces it. Vitals that are not measured (SpO₂, temperature, respiration) show *not measured*.

**Privacy by design:** camera frames are processed in the browser, reduced to a few numbers per frame and discarded. Nothing is stored or transmitted.

Standalone test pages: `pulse-test.html` (fingertip) and `face-test.html` (face).

## 8. Evidence: how we know the measurement is correct

### 8.1 Algorithm verification with known signals

We fed the pipeline synthetic pulse signals with a known heart rate, including a dicrotic notch (the small second bump of a real pulse wave), random noise, slow baseline drift and, for the face mode, lighting changes **6× stronger than the pulse itself**. Run with `pulse-test.html?sim=1&hr=72` and `face-test.html?sim=1&hr=72`.

| True heart rate (bpm) | Fingertip result | Face (contactless) result |
|---|---|---|
| 42 | 42 | — |
| 48 | 48 | 48 |
| 54 | 54 | — |
| 60 | — | 60 |
| 62 | 62 | — |
| 72 | 72 | 72 |
| 88 | — | 88 |
| 95 | 95 | — |
| 110 | — | 110 |
| 128 | 128 | — |
| 140 | — | 140 |
| 160 | 160 | — |
| 190 | 190 | — |

Every tested rate was recovered within **±1 bpm**. Testing also exposed and fixed two real failure modes: at low heart rates the spectrum locked onto a harmonic (48 bpm read as 144), and the dicrotic notch was counted as an extra beat (54 bpm read as 82). The harmonic check and the adaptive minimum beat spacing were added for these cases.

This proves the **signal processing** is correct. It does not by itself prove accuracy on people, which is why we also test on humans.

### 8.2 Human validation protocol

1. **Reference:** a fingertip pulse oximeter or smartwatch, or a manual count of the pulse at the wrist for 30 seconds × 2.
2. **Resting:** measure seated after 2 minutes of rest; compare app and reference.
3. **Changing heart rate:** 20–30 squats, measure immediately, then every minute during recovery. The app must follow the rise and the fall. This shows it tracks the heart, not a random number.
4. **Several people**, different lighting, both modes.
5. **Report** the mean difference and the largest difference.

### 8.3 Human test results

| # | Person | Condition | Mode | App (bpm) | Reference (bpm) | Reference type | Difference |
|---|---|---|---|---|---|---|---|
| 1 | | resting | fingertip | | | | |
| 2 | | after squats | fingertip | | | | |
| 3 | | resting | face | | | | |
| 4 | | | | | | | |

*To be completed by the team before submission; only real measurements go in this table.*

### 8.4 What the app does when it is not sure

It shows no number. A heart rate appears only when two independent methods agree and the reading is stable; otherwise the user sees *"Signal noisy"* or a specific instruction. Refusing to guess is a design choice: in medicine a wrong number is worse than no number.

## 9. Security: tamper-proof medical ledger

Medical records made by an autonomous system must be trustworthy afterwards: if an AI made a decision, it must be provable that nobody changed it later.

- Every log entry becomes a **block**: `index | time | text | hash of the previous block`.
- The block's **SHA-256** hash is computed with the browser's Web Crypto API.
- Each block stores the previous block's hash, forming a **chain** back to the genesis block.
- **Verify chain** recomputes every hash. **Simulate tampering** silently edits an old record; verification then reports *"✗ tampered at block #N"* and Guardian logs a ledger integrity violation.
- The same decisions are queued to Mission Control, so Earth holds an independent copy.

**Known limit and next step:** someone with full control of the system could recompute every hash. Real deployments add **digital signatures** on each block (keys outside the attacker's reach) and **anchoring** block hashes on Earth through the uplink. Medical data should also be **encrypted** at rest and in transit, with **role-based access** (the flight surgeon sees full data, the commander sees fit / not fit).

## 10. Science and reference values

| Item | Value used | Basis |
|---|---|---|
| Earth–Mars light time (scenario) | 14 min 32 s one way, 29 min 04 s round trip | Typical value; real range is about 3–22 minutes depending on orbital positions |
| Career radiation limit | 600 mSv | NASA-STD-3001 career effective dose limit |
| Galactic cosmic ray background | 0.9 mSv/day | Simplified value for a shielded habitat; for comparison, Curiosity's RAD instrument measured about 1.8 mSv/day during its cruise to Mars (Zeitlin et al., 2013) |
| Radiation storm scale | S1 ≥ 10, S2 ≥ 100, S3 ≥ 1,000, S4 ≥ 10,000 pfu (≥10 MeV protons) | NOAA Space Weather Scales |
| Flare classes | A, B, C, M, X, each 10× stronger | NOAA / GOES X-ray classification |
| Storm shelter | 20 g/cm² water wall | Hydrogen-rich materials such as water are effective against solar protons |
| Cabin CO₂ | Reference ~2,600 ppm long-term; app thresholds 3,000 (elevated) and 4,000 ppm (high) | Values used in the scenario for illustration of long-duration cabin limits |
| Normal resting heart rate | 50–100 bpm | Standard adult resting range |
| HRV metric | RMSSD | ESC/NASPE Task Force HRV standards (1996) |
| Atrial fibrillation | Irregularly irregular RR intervals, absent P waves | Standard ECG criteria |

## 11. Honest limitations

- **Simulated mission data.** Crew vitals, ECGs, cabin air, radiation and space weather are simulated. There is no live NASA data feed in this version.
- **Prototype decision logic.** Guardian uses explainable rules and statistics, not a trained machine-learning model. Confidence values are fixed per scenario.
- **Live sensor is a demonstration, not a medical device.** Motion, poor or flickering light, cold fingers and camera auto-exposure reduce accuracy; HRV from a 30 fps camera is a rough estimate; arrhythmias cannot be reliably detected this way.
- **Ledger** is a hash chain without signatures (see section 9).
- **Fictional crew.** Names and personal data are invented.

## 12. Roadmap

1. **Real space weather:** NASA DONKI events and NOAA GOES proton and X-ray data, including replaying a real storm (for example May 2024).
2. **Certified wearables:** chest-strap ECG and smartwatch data over Bluetooth (standard Heart Rate profile), similar in spirit to wearable systems tested on the ISS such as the Canadian Space Agency's Astroskin.
3. **Trained, validated models** for anomaly detection, with calibrated confidence.
4. **Cryptography:** signed ledger blocks, encrypted records, role-based access for the flight surgeon and commander.
5. **Mission Control view** that receives decisions with the real light-time delay.
6. **Ask Guardian:** crew can ask "why am I in the shelter?" and get a spoken, evidence-based answer.

## 13. Technical overview

- **One self-contained file**, `index.html`: HTML, CSS and plain JavaScript, no framework, no build step, no backend. Works offline (fonts fall back to system fonts without internet).
- **Rendering:** SVG for the habitat map, Canvas for the Sun, ECG, trends and pulse waves.
- **Browser APIs:** Web Crypto (SHA-256), MediaDevices / getUserMedia (camera), Web Audio (alarm tones), Speech Synthesis (voice alerts).
- **Testing hooks:** `index.html?pulsesim=72` runs the live sensor with a synthetic pulse; `pulse-test.html?sim=1&hr=72` and `face-test.html?sim=1&hr=72` test each pipeline without a camera.

| File | Purpose |
|---|---|
| `index.html` | The Solar Guardian app |
| `pulse-test.html` | Standalone fingertip sensor test page |
| `face-test.html` | Standalone contactless (face) sensor test page |
| `README.md` | This document |
| `LICENSE` | MIT license |

## 14. Use of AI tools

As required by the NASA Space Apps rules, we disclose that AI tools were used during development. We used **Claude (Anthropic)** as an AI coding assistant to help write and debug code, to research the scientific background, and to draft documentation. The concept, design decisions, testing and presentation are the team's own; every value and claim in this document was checked against the code and the cited sources.

## 15. References

1. Hertzman, A. B. (1937). Photoelectric plethysmography of the fingers and toes in man. *Proceedings of the Society for Experimental Biology and Medicine*.
2. Verkruysse, W., Svaasand, L. O., & Nelson, J. S. (2008). Remote plethysmographic imaging using ambient light. *Optics Express*, 16(26).
3. Wang, W., den Brinker, A. C., Stuijk, S., & de Haan, G. (2017). Algorithmic principles of remote PPG. *IEEE Transactions on Biomedical Engineering*, 64(7).
4. Task Force of the European Society of Cardiology and the North American Society of Pacing and Electrophysiology (1996). Heart rate variability: standards of measurement, physiological interpretation and clinical use. *Circulation*, 93(5).
5. NASA. NASA-STD-3001, NASA Space Flight Human-System Standard, Volume 1: Crew Health (career space permissible exposure limit for radiation).
6. NOAA Space Weather Prediction Center. NOAA Space Weather Scales (Solar Radiation Storms, S1–S5).
7. NIST. FIPS 180-4, Secure Hash Standard (SHA-256).
8. Canadian Space Agency. Astroskin: bio-monitoring garment used on the International Space Station.
9. Zeitlin, C., et al. (2013). Measurements of energetic particle radiation in transit to Mars on the Mars Science Laboratory. *Science*, 340(6136).

## 16. Team and license

**Team Solar Guardian**, NASA Space Apps Challenge 2026, Vilnius

- Dilara Mammadzada
- Sayadulla Mammadzada

Released under the [MIT License](LICENSE).
