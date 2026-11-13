# Solar Guardian

**A health companion for astronauts on long missions: each astronaut checks their own health and gets clear guidance, while an onboard AI watches the whole crew, the cabin and the Sun, and acts when Earth is too far away to help.**

Built for the **NASA Space Apps Challenge 2026**, challenge *"Create Health Monitoring Software for Astronauts on Space Missions"*, Vilnius local event. Team **Solar Guardian**.

> **Simulated mission, real data where it matters.** The crew and ship are simulated, using real reference scales. Space weather can come **live from NOAA's GOES satellites**, a **real May 2024 solar storm** is replayed with timing from **NASA DONKI**, and the **heart sensor measures a real person** through the camera.

---

## Contents

1. [The problem](#1-the-problem)
2. [What Solar Guardian does](#2-what-solar-guardian-does)
3. [How it answers the challenge](#3-how-it-answers-the-challenge)
4. [Quick start](#4-quick-start)
5. [Astronaut health: the astronaut's own view](#5-astronaut-health-the-astronauts-own-view)
6. [Mission control: tour of the interface](#6-mission-control-tour-of-the-interface)
7. [Mission scenarios](#7-mission-scenarios)
8. [Real data: NOAA live Sun and NASA DONKI storm replay](#8-real-data-noaa-live-sun-and-nasa-donki-storm-replay)
9. [How Guardian thinks](#9-how-guardian-thinks)
10. [Live heart sensor: measuring a real person](#10-live-heart-sensor-measuring-a-real-person)
11. [Evidence: how we know the measurement is correct](#11-evidence-how-we-know-the-measurement-is-correct)
12. [Security: tamper-proof medical ledger](#12-security-tamper-proof-medical-ledger)
13. [Science and reference values](#13-science-and-reference-values)
14. [Honest limitations](#14-honest-limitations)
15. [Roadmap](#15-roadmap)
16. [Technical overview](#16-technical-overview)
17. [Use of AI tools](#17-use-of-ai-tools)
18. [References](#18-references)
19. [Team and license](#19-team-and-license)

---

## 1. The problem

NASA's Human Research Program names **five hazards of human spaceflight**: space radiation, isolation and confinement, distance from Earth, gravity fields, and hostile closed environments. Over a long mission they can lead to bone loss, cardiovascular changes, immune changes, vision changes, poor sleep and behavioral health problems.

On the way to Mars a radio signal needs **14 min 32 s** to reach Earth one way, so a question and its answer take **29 minutes**; during a solar conjunction the link can be lost for about two weeks. Astronauts therefore carry much of the responsibility for spotting health changes in themselves, and some dangers move faster than Earth can answer:

- A **solar particle event** can deliver a large radiation dose. The flare's X-rays arrive in about 8 minutes; the energetic protons follow minutes to hours later. That gap is the only warning window.
- A **silent arrhythmia** (atrial fibrillation) can go unnoticed until the next scheduled check.
- A **failing CO₂ scrubber** slowly degrades the whole crew's thinking, and looks like four separate medical problems.

## 2. What Solar Guardian does

Two views, switched in the header: **Astronaut health** for the individual astronaut, and **Mission control** for the crew, the ship and the Sun.

| Capability | What it means |
|---|---|
| **Self-assessment ("Astronaut health")** | A daily check-in (blood pressure, heart rate, blood sugar, temperature, sleep, mood, teamwork, symptoms), a clickable 3D anatomy model (skin, skeleton, organs, vessels) that glows by status, and for every body system: readings, why it matters in space, what to do, and when to involve the flight surgeon. |
| **Routine and motivation** | A daily plan with reminders from the mission clock, XP, streaks and badges. |
| **Space-weather-aware radiation protection** | Detects a flare while it is still rising, forecasts every astronaut's dose per module, aborts spacewalks and sends the crew to the water-walled storm shelter before the protons arrive. |
| **Real space weather** | Live NOAA GOES proton and X-ray data, and a replay of the real May 2024 storm with NASA DONKI timing. |
| **Personal-baseline anomaly detection** | Compares each astronaut with their *own* normal, learned over 142 mission days. Expected changes (a heart-rate rise during a spacewalk) are not flagged. |
| **Multi-crew fusion** | When all crew drift at the same time in the same direction, Guardian concludes the cause is the cabin (CO₂), not four bodies, and fixes the cause. |
| **ECG arrhythmia detection** | Finds a hidden atrial fibrillation from beat-to-beat irregularity and alerts the flight surgeon. |
| **Dose-aware mission planning** | Tracks each career dose against NASA's 600 mSv limit and reassigns spacewalks before anyone would exceed it. |
| **Earth light-delay autonomy** | Decides onboard, queues decisions and flagged check-ins for Mission Control, and keeps working when the link is lost. A human can switch autonomy off and approve each action. |
| **3D habitat** | An ISS-style station in Mars orbit with animated astronauts in realistic spacesuits, the water-walled shelter and radiation particles. |
| **Hazards adding up** | Following NASA's note that the five hazards "can feed off one another", Guardian warns when they combine (for example poor sleep + high CO₂). |
| **Live heart sensor** | Measures a real person's heart rate with the camera: fingertip or contactless from the face. |
| **Tamper-proof medical ledger** | Every decision is written into a SHA-256 hash chain; editing any past record is detected. |
| **Voice and alarm tones** | Critical events trigger an alarm and a spoken alert. |

## 3. How it answers the challenge

| Challenge text | Where it is in Solar Guardian |
|---|---|
| A visual tool that helps astronauts **assess their own health** | **Astronaut health** tab: daily check-in, 3D anatomy model, status per body system |
| Provide **guidance on treatments and health improvements** | Body system cards: *What you can do* |
| Input by **keyboard, mouse clicks or camera images** | Check-in form, clickable body and plan, **camera heart rate** (fingertip or face) |
| Indicators such as **blood pressure, heart rate, blood sugar, body temperature, sleep hours, mood** | All six are in the check-in, each colour-rated |
| **When might a result warrant attention** from the crew or flight surgeons on the ground? | *Involve the flight surgeon* box per system; flagged check-ins are queued to Earth with the real light-time delay |
| A **human figure where each part is clickable** | 3D anatomy model with labels and leader lines: brain, eyes, lungs, heart, blood and liver, skeleton, radiation dosimeter |
| **Prompt astronauts to take measurements** as part of the routine | Today's plan and reminders driven by the mission clock |
| **Gamification** | XP, levels, check-in streaks, badges |
| **Dynamic charts** of indicators over time | 14-day trends; live ECG and vital-sign trends |
| **Colour coding** at a glance | Green / amber / red everywhere |
| **Simple instructions and explanations** | *Why it matters in space* and plain-language advice on every card |
| Different environments (spacecraft, station, base) | A deep-space habitat on a Mars-distance mission |
| Use **NASA HRP** and space-agency resources (all challenge resources were read and used) | Five-hazards panel, "hazards adding up" warnings, balance, cabin noise, lighting and microbes from the NASA HRP hazards page; exercise sessions and nutrition from NASA's video on the space radiation hazard page; CSA facts, Earth benefits and ISS experiment links on every body system card |

## 4. Quick start

No installation and no build step: it is a single HTML file.

1. Download the repository (green **Code** button, then **Download ZIP**) and unzip it.
2. Open **`index.html`** in **Google Chrome** or **Microsoft Edge** (needed for the camera, 3D and voice). An internet connection enables the 3D views and real data; without it the app falls back to 2D and simulated space weather.
3. Click **"▶ Run 60-second pitch demo"**, or open **Astronaut health** and press **Fill example**, then **Save check-in**.

Live version (GitHub Pages, available when the repository is public): https://dilaramammadzada2008.github.io/solar-guardian/

**Before every presentation:** press **↺ Reset mission**, switch **Voice: ON** with a real click (browsers only allow sound after a click), and enter your NASA API key with **⚙** in the Sun panel (see section 8).

## 5. Astronaut health: the astronaut's own view

Choose the astronaut at the top. The bar shows **XP and level**, the **check-in streak** and **exercise days this week**.

**My body · tap a part.** A 3D anatomy model in x-ray style: translucent skin, a skeleton (skull, spine, 12 pairs of ribs, pelvis, limb bones), organs (brain, eyes, lungs with trachea and bronchi, a heart that beats at the astronaut's heart rate with the aorta and vena cava, liver, spleen, stomach, intestines, kidneys, bladder) and blood vessels (red arteries, blue veins). Organs keep their natural colours; a system that needs attention glows amber and one that needs action pulses red. Labels with leader lines (Brain, Eyes, Lungs, Heart, Blood & liver, Skeleton, Dosimeter) show each system's status and can be clicked, as can the organs themselves. Layer buttons show or hide **Skin, Skeleton, Organs, Vessels**. Drag to turn, scroll to zoom, double-click to reset. It is a stylised teaching model, not a medical-grade atlas.

| Part | System | What is rated |
|---|---|---|
| Heart | Heart & circulation | Heart rate, blood pressure, rhythm (from Guardian's ECG) |
| Brain | Brain, mood & sleep | Mood, sleep hours, teamwork, cognition test, headache |
| Eyes | Eyes & vision | Blurred vision (possible SANS sign), weekly vision check |
| Lungs | Lungs & cabin environment | Blood oxygen, cabin CO₂, noise, lighting schedule, microbe swab, temperature and pressure |
| Blood vessels & liver | Blood sugar & immunity | Fasting blood sugar, temperature |
| Skeleton | Bones, muscles & balance | Exercise today, estimated bone loss without exercise, balance (nausea = possible space motion sickness), back pain |
| Chest dosimeter | Radiation exposure | Career dose, projected end-of-mission dose, dose rate now |

**Body system card.** For the selected part: colour-rated readings, the related spaceflight hazard, *Why it matters in space* (with facts from NASA HRP and the Canadian Space Agency, such as anemia, cataracts, insulin resistance, slower reflexes, and bone loss of up to 1.5% a month in space compared with about 1% a year for adults over 50), *What you can do*, *On Earth this helps* (osteoporosis, balance problems in seniors, cardiovascular disorders, type 2 diabetes), *Related space research on the ISS* (CSA experiments such as Vascular Aging, CARDIOBREATH, C-STARS, Wayfinding, SANSORI, SANSORI-2, SPARK, TBone2, AstroFit, HomeBase), a red box *Involve the flight surgeon* with the thresholds that need medical attention, and links to the sources.

**Daily check-in.** Blood pressure (mmHg), heart rate (bpm; **📷** measures it with the camera), fasting blood sugar (mg/dL), body temperature (°C), sleep last night (hours), mood (five faces), teamwork today (1–5) and symptoms (headache, blurred vision, back pain, nausea). Saving rates every value and gives +50 XP. A red result is **sent to the flight surgeons on Earth** (logged by Guardian and queued with the 14 min 32 s light-time delay); amber results point to the body parts to open. **Fill example** enters sample values for demos.

**Today's plan.** Morning check-in (ticked automatically); the three ISS-style exercise sessions shown in NASA's video (treadmill with harness, cycle ergometer, resistance device; two of three count as exercise done); planned meals with fresh greens; 2.5 L of water; weekly vision check; 15 min with family or crew; an 8-hour sleep window. Each gives XP. Reminders appear from the mission clock (morning check-in due, exercise not logged, sleep window). **Badges:** 7-day streak, Bone guardian (exercise 5 of 7 days), Sleep champion (7-day average ≥ 7 h), Storm-ready (sheltered during a storm), Level 3.

**My trends · last 14 days.** Sleep, systolic blood pressure, blood sugar and mood, each point coloured by status. Earlier days are a simulated sample history; today is the astronaut's own entry.

**5 hazards of human spaceflight.** Live status for radiation (career dose, dose rate), isolation and confinement (mood, sleep, teamwork), distance from Earth (link delay, autonomy), gravity fields (exercise, balance) and hostile closed environment (cabin CO₂, noise, lighting), linked to NASA HRP.

**Hazards adding up.** NASA notes that the five hazards "can feed off one another". When they combine for the selected astronaut, an amber box appears above the hazards and Guardian logs a warning: poor sleep + high cabin CO₂ (postpone safety-critical tasks), radiation storm + spacewalk (get into the shelter), Earth link lost + low mood, little sleep + team tension, no exercise + balance problems, little sleep + radiation storm.

## 6. Mission control: tour of the interface

**Header.** Mission clock (day 142 of 500), Earth link delay (14m 32s, or *LOST · AUTONOMOUS*), space weather (flare class and NOAA S-level), total radiation dose averted, simulation speed (1×, 5×, 20×), **Autonomy** and **Voice** switches.

**Sun · space weather.** Animated Sun, **[Simulated] / [Live · NOAA]** switch and **⚙** for the NASA API key. X-ray flare class, proton flux ≥10 MeV, NOAA radiation storm level, solar wind, and a log-scale proton chart with the S1 threshold (10 pfu) dashed. Status chip: *QUIET*, *SEP INBOUND · T-countdown*, *RADIATION STORM S1–S4*, or *LIVE · QUIET / STORM*.

**Cabin environment.** CO₂ (green below 3,000 ppm, amber above, red above 4,000), O₂, pressure, temperature, active CO₂ scrubber and its efficiency.

**Deep-space habitat · live radiation map** (**3D** or **2D**). An ISS-style station in orbit around Mars (consistent with the 14 min 32 s light time): white semi-transparent modules with crew quarters (HAB), laboratory (LAB), the **storm shelter** with a 20 g/cm² water wall, airlock and the EVA worksite outside, each with its live dose rate; large gold solar wings on a truss, white radiators, an antenna and the two **ECLSS CO₂ scrubbers** (*STANDBY*, *ACTIVE*, pulsing red *FAULT*, *OFFLINE · INSPECT*). The four astronauts wear realistic spacesuits (gold sun visor, helmet lights, life-support backpack, chest control module, and stripes in their crew colour, as real NASA suits use stripes to tell astronauts apart): they walk between modules, float on a tether during a spacewalk, and show a ring when selected (pulsing red on ALERT). Violet galactic cosmic rays pass through everything; during a storm amber solar protons stream from the Sun and stop at the water wall, and module floors turn red with dose. Drag to rotate, scroll to zoom, click an astronaut to open their telemetry, double-click to reset. Without WebGL or internet the 2D map is shown.

**Physiological telemetry.** For the selected astronaut: live ECG (lead II, 25 mm/s), heart rate, SpO₂, HRV and dose-rate trends against the personal baseline, and the context (rest, moving, EVA exertion, irregular rhythm).

**Crew digital twins.** One card per astronaut with seven signals (HR, SpO₂, HRV, temperature, respiration, cognition, radiation dose), Guardian risk ring (NOMINAL, WATCH, ALERT) and career-dose bar with the projected end-of-mission dose. A fifth **Guest (live)** card appears when a real person is measured.

**Bottom row.** *Guardian AI · decision log* (AUTO tags or approval buttons), *Autonomous triage* (title, confidence, evidence, actions, Earth reply time), *Tamper-proof medical ledger* (**Verify chain**, **Simulate tampering**) and *Earth uplink queue* to MCC Houston (*in transit*, *received*, *held · no link*).

## 7. Mission scenarios

Each button injects an event. **Guardian is not told about it**; it has to detect the event from its sensors.

| Button | What happens | What Guardian does |
|---|---|---|
| **▶ Run 60-second pitch demo** | EVA → solar storm → CO₂ fault → arrhythmia in sequence. | Everything below, automatically. |
| **☀ Solar particle event (X-class flare)** | A flare erupts; protons arrive about 25 simulated minutes later and peak around NOAA S3. | Forecasts dose per module (HAB 21.0, shelter 3.8, EVA 67 mSv), aborts the EVA if ingress is faster than proton arrival, orders the shelter protocol, counts the dose averted, gives *ALL CLEAR* below S1. |
| **🛰 Replay real storm — May 2024 (NASA DONKI)** | Loads the real event, shows a "Gannon storm" background card, then replays it with the real warning window (5 h 14 min). | Same protocol; reports how early it sheltered the crew before the real proton onset. |
| **⛑ Start EVA — Aylin** | Aylin goes outside; her heart rate rises. | Context-aware thresholds, so no false alarm. Refuses an EVA during a storm. |
| **♥ Hidden cardiac arrhythmia — Jonas** | Jonas develops atrial fibrillation he does not feel. | Detects irregular beat-to-beat intervals, raises an ALERT, alerts the flight surgeon. |
| **≋ CO₂ scrubber degradation** | The active scrubber drops to 52% efficiency; CO₂ rises. | Sees 4/4 crew drifting together, names the cabin as the root cause, switches scrubber. Works repeatedly (B → A → B). |
| **♥ Live heart sensor — guest** | Opens the camera sensor. | Measures a real person and adds them as a live crew card. |
| **⌁ Cut Earth link** | Simulates solar conjunction. | Keeps working; messages wait as *held · no link*. |
| **↺ Reset mission** | Restarts everything. | |

Tip: show the CO₂ scenario at **1×** speed so the red *FAULT* state is visible before Guardian switches.

## 8. Real data: NOAA live Sun and NASA DONKI storm replay

### Live space weather (NOAA SWPC / GOES)

**Live · NOAA** reads, every 5 minutes and without a key:

- `https://services.swpc.noaa.gov/json/goes/primary/integral-protons-1-day.json`: proton flux ≥10 MeV (pfu)
- `https://services.swpc.noaa.gov/json/goes/primary/xrays-1-day.json`: X-ray flux 0.1–0.8 nm (W/m²), converted to the flare class

The panel shows today's real values, the satellite and the update time, and the proton chart shows the last 24 hours. The real flux drives the dose model: if a real radiation storm (≥ 10 pfu) is happening, Guardian applies the shelter protocol. If the feed cannot be reached, the app returns to the simulation and says so.

### Real storm replay (NASA DONKI)

**DONKI** (Space Weather Database Of Notifications, Knowledge, Information) is NASA's space-weather event catalogue, run by the Community Coordinated Modeling Center at NASA Goddard. It records flares, coronal mass ejections, solar energetic particle (SEP) events and geomagnetic storms, and links related events.

The replay calls `https://api.nasa.gov/DONKI/SEP?startDate=2024-05-08&endDate=2024-05-20`, takes the first SEP event and its linked flare: **flare 9 May 2024 08:45 UTC, proton onset 13:59 UTC, a real warning window of 5 h 14 min**. Our storm runs with that timing, the triage shows the real window, and at proton onset Guardian logs how early it ordered the shelter. **Event timing is real NASA data; the proton intensity curve is modelled.** (On 13 November 2026 the DONKI flare endpoint returned 404, so the flare is taken from the SEP event's linked activities.)

**Background card shown before the replay** (facts checked against NOAA SWPC, NASA CCMC and Hayakawa et al. 2025): the strongest geomagnetic storm in over 20 years, **G5 (extreme)** on 10–11 May 2024 and the first G5 since the Halloween storms of October 2003; source sunspot region **AR 13664** with 12 X-class flares between 8 and 15 May; auroras across Europe; named the **"Gannon storm"** in memory of space weather physicist **Dr Jennifer Gannon**, who died on 2 May 2024. The storm starts when **▶ Start replay** is pressed.

**NASA API key.** Get a free personal key at api.nasa.gov and enter it with **⚙** in the Sun panel. It is stored only in that browser (localStorage) and never written into the code. Without a key the shared `DEMO_KEY` is used, which is rate-limited per IP address (at a hackathon many teams share one network).

## 9. How Guardian thinks

Guardian is the decision engine inside the app. It is deliberately **explainable**: rules and statistics whose reasoning can be shown to a flight surgeon, rather than a black box.

**Personal baselines.** For heart rate, SpO₂ and HRV each astronaut has a running mean and variance (exponentially weighted). Every new value becomes a z-score against that person's own normal. The baseline does **not** learn during an EVA, an arrhythmia, or when a value is already abnormal (|z| ≥ 3), so anomalies cannot become the new normal.

**Risk fusion.** Each astronaut's risk score (0–100) combines heart-rate deviation (ignored during expected exertion), low SpO₂ (< 94%), a detected arrhythmia, current radiation dose rate, a projected career dose above 600 mSv and reduced cognition. Score ≥ 28 is **WATCH**, ≥ 55 is **ALERT**.

**Multi-crew fusion.** If cabin CO₂ exceeds 3,900 ppm and at least 3 of 4 crew show heart-rate deviation or reduced cognition at the same time, Guardian reports one environmental root cause instead of separate medical alarms.

**Arrhythmia.** An RR-interval irregularity index above 0.12 (personal baseline 0.03), at rest and outside an EVA, is reported as suspected atrial fibrillation.

**Radiation.** Dose rate per module = solar proton rate × module shielding factor + galactic background. The storm shelter lets through about 18% of the HAB's solar proton dose (about **5.5× lower**); the EVA worksite gets 3.2× the HAB dose. Career dose is projected to the end of the 500-day mission at 0.9 mSv/day.

**Self check-ins.** Every saved check-in is logged; a check-in with a red value is logged as a warning, written to the ledger and queued for flight surgeons on Earth.

**Autonomy.** With *Autonomy: ON* Guardian executes protocols itself (AUTO tag). With *Autonomy: OFF* it recommends and waits for the crew to press the action button. Every event goes to the decision log and the ledger; warnings, critical events and decisions are also queued for Mission Control.

**Confidence values** in the triage panel (91%, 87%, 94%) are fixed per scenario in this prototype to illustrate the concept. In a real system they would be calibrated on validation data.

## 10. Live heart sensor: measuring a real person

The crew is simulated; the live heart sensor is not. It measures the person in front of the camera, from **♥ Live heart sensor — guest** in Mission control or **📷** in the Astronaut health check-in.

### Principle: photoplethysmography (PPG)

Every heartbeat pushes a wave of blood into the skin. More blood absorbs more light, so the skin's colour changes very slightly with each beat, too little for the eye, but measurable by a camera at 30 frames per second. Hospital pulse oximeters and smartwatches use the same principle.

### Two modes

| | **Fingertip** | **Face · contactless (rPPG)** |
|---|---|---|
| How | Fingertip covers the camera; light shines through the tissue (phone flashlight, or a light behind the finger on a laptop). | Camera looks at the face; forehead and both cheeks are measured. |
| Signal | Mean **red** value of the fingertip. Strong signal. | Mean **red, green, blue** of the skin regions, combined with the **POS** algorithm (Wang et al., 2017), which cancels brightness changes that affect all colours equally. Weaker signal. |
| Typical time to first reading | 6–10 s | 10–15 s |
| HRV | Rough estimate (marked ≈) | Not shown |

### Processing pipeline

1. **One number per frame.** The video is reduced to the average colour of the measured region; no image is stored or sent.
2. **Uniform resampling** to 30 Hz over a 12 s (fingertip) or 15 s (face) window.
3. **Band-pass filter** to the heart-rate range (0.5–4 Hz for fingertip, 0.6–3.3 Hz for face), applied forwards and backwards so the wave is not shifted in time.
4. **Method 1, spectrum:** the strongest rhythm between 40 and 200 bpm (180 for face), with a **harmonic check**: if half or a third of the peak rate also carries real power, the lower rate is taken as the heart rate.
5. **Method 2, beat peaks:** individual beats are found in the time domain (with sub-frame precision); the median beat-to-beat interval gives a second heart rate.
6. **Agreement:** a reading counts only if both methods agree within 10 bpm and the signal-to-noise ratio is high enough.
7. **Stability:** a number is displayed only when the last 3–4 accepted readings lie within 8 bpm of each other.
8. **Quality checks:** finger not covering / too dark / too bright; face not in the oval / too dark / moving. When a check fails the app tells the user what to do instead of guessing.

### Using it

1. Click **♥ Live heart sensor — guest** (or **📷** in the check-in) and allow the camera.
2. Choose **Fingertip** or **Face · contactless**.
3. Hold still. When a stable number appears, click **Add to crew** (or close the window: the check-in takes the reading).
4. A **Guest (live)** card shows the real heart rate, signal quality and a Guardian comment (normal resting range 50–100 bpm). Vitals that are not measured show *not measured*.

**Privacy by design:** camera frames are processed in the browser, reduced to a few numbers per frame and discarded. Nothing is stored or transmitted.

Standalone test pages: `pulse-test.html` (fingertip) and `face-test.html` (face).

## 11. Evidence: how we know the measurement is correct

### 11.1 Algorithm verification with known signals

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

### 11.2 Human validation protocol

1. **Reference:** a fingertip pulse oximeter or smartwatch, or a manual count of the pulse at the wrist for 30 seconds × 2.
2. **Resting:** measure seated after 2 minutes of rest; compare app and reference.
3. **Changing heart rate:** 20–30 squats, measure immediately, then every minute during recovery. The app must follow the rise and the fall.
4. **Several people**, different lighting, both modes.
5. **Report** the mean difference and the largest difference.

### 11.3 Human test results

| # | Person | Condition | Mode | App (bpm) | Reference (bpm) | Reference type | Difference |
|---|---|---|---|---|---|---|---|
| 1 | | resting | fingertip | | | | |
| 2 | | after squats | fingertip | | | | |
| 3 | | resting | face | | | | |
| 4 | | | | | | | |

*To be completed by the team before submission; only real measurements go in this table.*

### 11.4 What the app does when it is not sure

It shows no number. A heart rate appears only when two independent methods agree and the reading is stable; otherwise the user sees *"Signal noisy"* or a specific instruction. In medicine a wrong number is worse than no number.

## 12. Security: tamper-proof medical ledger

Medical records made by an autonomous system must be trustworthy afterwards: if an AI made a decision, it must be provable that nobody changed it later.

- Every log entry, including self check-ins, becomes a **block**: `index | time | text | hash of the previous block`.
- The block's **SHA-256** hash is computed with the browser's Web Crypto API.
- Each block stores the previous block's hash, forming a **chain** back to the genesis block.
- **Verify chain** recomputes every hash. **Simulate tampering** silently edits an old record; verification then reports *"✗ tampered at block #N"* and Guardian logs a ledger integrity violation.
- The same decisions are queued to Mission Control, so Earth holds an independent copy.

**Known limit and next step:** someone with full control of the system could recompute every hash. Real deployments add **digital signatures** on each block and **anchoring** block hashes on Earth through the uplink. Medical data should also be **encrypted** at rest and in transit, with **role-based access** (the flight surgeon sees full data, the commander sees fit / not fit).

## 13. Science and reference values

### Mission and space environment

| Item | Value used | Basis |
|---|---|---|
| Earth–Mars light time (scenario) | 14 min 32 s one way, 29 min 04 s round trip | Typical value; real range is about 3–22 minutes |
| Career radiation limit | 600 mSv | NASA-STD-3001 career effective dose limit |
| Galactic cosmic ray background | 0.9 mSv/day | Simplified value for a shielded habitat; for comparison, Curiosity's RAD measured about 1.8 mSv/day during its cruise to Mars (Zeitlin et al., 2013) |
| Radiation storm scale | S1 ≥ 10, S2 ≥ 100, S3 ≥ 1,000, S4 ≥ 10,000 pfu (≥10 MeV protons) | NOAA Space Weather Scales |
| Flare classes | A, B, C, M, X, each 10× stronger (0.1–0.8 nm X-ray flux) | NOAA / GOES classification |
| Storm shelter | 20 g/cm² water wall | Hydrogen-rich materials such as water are effective against solar protons |
| Cabin CO₂ | Reference ~2,600 ppm long-term; app thresholds 3,000 and 4,000 ppm | Values used in the scenario to illustrate long-duration cabin limits |
| Bone loss without exercise | About 1–1.5% per month in weight-bearing bones; ISS crews exercise about 2 h/day | NASA Human Research Program |
| Vision changes | SANS (spaceflight-associated neuro-ocular syndrome) | NASA Human Research Program risks |

### Self check-in ranges (general adult references, simplified, for illustration only)

| Indicator | Green | Amber | Red | Basis |
|---|---|---|---|---|
| Blood pressure (mmHg) | below 120/80 | 120–139 / 80–89, or below 90/60 | 140/90 or higher | Simplified from American Heart Association categories |
| Fasting blood sugar (mg/dL) | 70–99 | 54–69 or 100–125 | below 54 or 126 and above | American Diabetes Association criteria |
| Body temperature (°C) | 35.5–37.2 | 37.3–37.9 | 38.0 and above, or below 35.5 | Common clinical fever threshold 38 °C |
| Sleep (hours) | 7–9 | 6–7, or over 9 | below 6 | Adult sleep recommendation of 7 or more hours |
| Resting heart rate (bpm) | 50–100 | below 50 or 101–120 | above 120 | Standard adult resting range |
| Mood (1–5) | 4–5 | 3 | 1–2 | Self-rated scale used in the app |
| HRV metric | RMSSD | | | ESC/NASPE Task Force HRV standards (1996) |

## 14. Honest limitations

- **Simulated crew and ship.** Crew vitals, ECGs, cabin air and the ship are simulated. Space weather is simulated unless **Live · NOAA** is on. In the DONKI replay only the event timing is real; proton intensity is modelled.
- **Sample history.** In Astronaut health, the 13 days before today are a simulated sample; only today's check-in is entered by the user. Check-ins are kept in memory and reset on reload.
- **Not medical advice.** Reference ranges are general adult values, simplified for illustration; a real system would use each astronaut's medical baseline and flight-surgeon protocols.
- **Prototype decision logic.** Guardian uses explainable rules and statistics, not a trained machine-learning model. Confidence values are fixed per scenario.
- **Live sensor is a demonstration, not a medical device.** Motion, poor or flickering light, cold fingers and camera auto-exposure reduce accuracy; HRV from a 30 fps camera is a rough estimate; arrhythmias cannot be reliably detected this way.
- **Internet needed for 3D and real data.** three.js loads from a CDN; NOAA and NASA data are fetched online. Offline, the app falls back to 2D and the simulation.
- **Simulated cabin extras.** Cabin noise and the microbe swab result are simulated; lighting follows the mission clock.
- **Stylised anatomy.** The 3D body is a simplified teaching model built from shapes, not a medical-grade anatomy atlas.
- **Ledger** is a hash chain without signatures (see section 12).
- **Fictional crew.** Names and personal data are invented.

## 15. Roadmap

1. **Full real storm curves:** GOES archive proton data for complete historical replays, not only DONKI timing.
2. **Certified wearables:** chest-strap ECG, blood-pressure cuff and glucose meter over Bluetooth, similar in spirit to wearable systems tested on the ISS such as the Canadian Space Agency's Astroskin.
3. **Personal medical baselines** for each astronaut instead of general reference ranges, set with flight surgeons.
4. **Trained, validated models** for anomaly detection, with calibrated confidence.
5. **Cryptography:** signed ledger blocks, encrypted records, role-based access.
6. **Mission Control view** that receives decisions and check-ins with the real light-time delay.
7. **Ask Guardian:** crew can ask "why am I in the shelter?" and get a spoken, evidence-based answer.

## 16. Technical overview

- **One file**, `index.html`: HTML, CSS and plain JavaScript, no framework, no build step, no backend.
- **3D:** three.js r128 (from cdnjs) with WebGL for the habitat (procedural Mars texture, fresnel atmosphere) and the anatomy model (fresnel x-ray skin shader, layered meshes, HTML labels with SVG leader lines); automatic 2D fallback.
- **Rendering:** SVG for the 2D map, Canvas for the Sun, ECG, trends and pulse waves.
- **Data:** `fetch` to NOAA SWPC JSON feeds and NASA DONKI (api.nasa.gov); the NASA key is kept only in the browser's localStorage.
- **Browser APIs:** Web Crypto (SHA-256), MediaDevices / getUserMedia (camera), Web Audio (alarm tones), Speech Synthesis (voice alerts).
- **Testing hooks:** `index.html?pulsesim=72` runs the live sensor with a synthetic pulse; `pulse-test.html?sim=1&hr=72` and `face-test.html?sim=1&hr=72` test each pipeline without a camera.

| File | Purpose |
|---|---|
| `index.html` | The Solar Guardian app |
| `pulse-test.html` | Standalone fingertip sensor test page |
| `face-test.html` | Standalone contactless (face) sensor test page |
| `README.md` | This document |
| `LICENSE` | MIT license |

## 17. Use of AI tools

As required by the NASA Space Apps rules, we disclose that AI tools were used during development. We used **Claude (Anthropic)** as an AI coding assistant to help write and debug code, to research the scientific background, and to draft documentation. The concept, design decisions, testing and presentation are the team's own; every value and claim in this document was checked against the code and the cited sources.

## 18. References

1. NASA Human Research Program. The 5 Hazards of Human Spaceflight. https://www.nasa.gov/hrp/hazards/
2. NASA Human Research Program. Risks of Human Spaceflight. https://www.nasa.gov/hrp/risks/
3. NASA Human Research Program. Ongoing HRP Research in Space. https://www.nasa.gov/hrp/ongoing-hrp-research/
4. Canadian Space Agency (2026). Monitoring radiation for astronaut health. https://www.asc-csa.gc.ca/eng/news/articles/2026/2026-02-26-monitoring-radiation-astronaut-health.asp
4a. Canadian Space Agency. Why do we conduct science experiments in space? https://www.asc-csa.gc.ca/eng/iss/science/why-do-we-conduct-science-experiments-in-space.asp
4b. Canadian Space Agency (2017). How does space affect the human body? (infographic). https://www.asc-csa.gc.ca/eng/multimedia/search/image/8056
4c. Canadian Space Agency. Canadian experiments on the Station. https://www.asc-csa.gc.ca/eng/iss/science/experiments.asp
4d. NASA. What Are the Dangers of Going to Space? We Asked a NASA Expert (video, on the NASA HRP space radiation hazard page). https://www.nasa.gov/hrp/hazard-space-radiation/
5. NASA CCMC. DONKI: Space Weather Database Of Notifications, Knowledge, Information (via https://api.nasa.gov).
6. NOAA Space Weather Prediction Center. GOES proton and X-ray JSON products (https://services.swpc.noaa.gov/json/goes/primary/), NOAA Space Weather Scales, and news on the May 2024 G5 storm and Active Region 13664.
7. Hayakawa, H., et al. (2025). The Solar and Geomagnetic Storms in 2024 May: A Flash Data Report. *The Astrophysical Journal*.
8. Hertzman, A. B. (1937). Photoelectric plethysmography of the fingers and toes in man. *Proceedings of the Society for Experimental Biology and Medicine*.
9. Verkruysse, W., Svaasand, L. O., & Nelson, J. S. (2008). Remote plethysmographic imaging using ambient light. *Optics Express*, 16(26).
10. Wang, W., den Brinker, A. C., Stuijk, S., & de Haan, G. (2017). Algorithmic principles of remote PPG. *IEEE Transactions on Biomedical Engineering*, 64(7).
11. Task Force of the European Society of Cardiology and the North American Society of Pacing and Electrophysiology (1996). Heart rate variability: standards of measurement, physiological interpretation and clinical use. *Circulation*, 93(5).
12. NASA. NASA-STD-3001, NASA Space Flight Human-System Standard, Volume 1: Crew Health.
13. Zeitlin, C., et al. (2013). Measurements of energetic particle radiation in transit to Mars on the Mars Science Laboratory. *Science*, 340(6136).
14. American Heart Association. Understanding blood pressure readings (blood pressure categories).
15. American Diabetes Association. Standards of Care in Diabetes: diagnosis and classification (fasting glucose and hypoglycemia levels).
16. NIST. FIPS 180-4, Secure Hash Standard (SHA-256).
17. Canadian Space Agency. Astroskin: bio-monitoring garment used on the International Space Station.

## 19. Team and license

**Team Solar Guardian**, NASA Space Apps Challenge 2026, Vilnius

- Dilara Mammadzada
- Sayadulla Mammadzada

Released under the [MIT License](LICENSE).
