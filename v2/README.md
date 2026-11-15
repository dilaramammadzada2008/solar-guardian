# Solar Guardian · Crew Self-Care

**A health app for an astronaut on the way to Mars: the astronaut is not a doctor, and Earth is 11 minutes away.**

NASA Space Apps Challenge 2026 · Vilnius · Challenge: *Create Health Monitoring Software for Astronauts on Space Missions*

| | |
|---|---|
| **Open the app** | `v2/index.html` in Chrome or Edge (see [How to run](#how-to-run)) |
| **Presentation** | [Solar-Guardian-presentation.pdf](presentation/Solar-Guardian-presentation.pdf) · 7 slides · [speaker notes](presentation/speaker-notes.md) |
| **Main user** | The astronaut, a crew member who is not a doctor |

---

## Contents

1. [The problem](#1-the-problem)
2. [The idea in one sentence](#2-the-idea-in-one-sentence)
3. [Who it is for](#3-who-it-is-for)
4. [How it works](#4-how-it-works)
5. [The five tabs](#5-the-five-tabs)
6. [Emergency](#6-emergency)
7. [Built on the real ISS routine](#7-built-on-the-real-iss-routine)
8. [Built on NASA’s plans](#8-built-on-nasas-plans)
9. [Where the data comes from](#9-where-the-data-comes-from)
10. [How to run](#how-to-run)
11. [Demo script](#11-demo-script)
12. [What is real and what is simulated](#12-what-is-real-and-what-is-simulated)
13. [Use of Super Intelligence (SI) tools](#13-use-of-super-intelligence-si-tools)
14. [References](#14-references)

---

## 1. The problem

The challenge video starts with this scene: *halfway to Mars, a crewmate feels a sharp pain in the chest and collapses. What do you do?*

- **On the ISS today** a flight surgeon on Earth talks to the crew within a second. Real cases were handled this way. In 2020 a blood clot was found during a routine ultrasound and treated from Earth for more than 90 days. In January 2026 the Crew-11 crew managed a medical event with doctors guiding them, and the crew returned early.
- **On Mars** a radio signal needs minutes. Today it is **10 min 55 s one way**, read live from NASA’s Deep Space Network, so a question and its answer take about 22 minutes. Medical decisions have to start on board.
- **Astronauts are not doctors.** The challenge asks software to explain how to take each measurement, why it matters, and what to do when something is not normal.

## 2. The idea in one sentence

**The sensor sees *what* changed. The astronaut tells us *why*.**

Spacecraft sensors already measure a lot, but they cannot know the reason behind a change. Solar Guardian asks the astronaut one simple question at the right moment, and turns the numbers plus that reason into a clear next step.

## 3. Who it is for

Mentors asked us: *who is the user, the astronaut or the doctor?* Our answer is **the astronaut**. Their feedback shaped the app:

| Mentor feedback | What we did |
|---|---|
| “Who is the user?” | One user: the astronaut. Everything is written for someone who is not a doctor. |
| “Too complex for an astronaut” | Five simple tabs, one question at a time, one EMERGENCY button. |
| “Not numbers: what happened at that time?” | Plain words on screen; the astronaut adds the reason in one tap. Numbers are hidden unless *Clinical details* is switched on. |
| “NASA already has systems: integrate” | The app measures nothing itself. It is designed to read the devices already on board (Section 9) and follows NASA’s own concept (Section 8). |

## 4. How it works

An example from the demo day:

1. **Onboard devices measure.** The smart shirt records heart rate all day.
2. **Something changes that the crew schedule cannot explain.** At 13:10 the heart rate is 24 bpm above the astronaut’s usual level for 40 minutes, and no exercise was planned.
3. **The app asks one question:** *“What was happening?”* The astronaut taps an answer (physical work, stress, coffee, medication) and says whether they felt unwell.
4. **The answer decides what happens next**, and the rule behind it is always shown:

| Answer | Result | Rule shown |
|---|---|---|
| Coffee or physical work, felt fine | 🟢 **Explained**, no action | Rise explained by activity or intake |
| Stress, felt fine | 🟢 Explained, with a breathing tip | Single episode with a non-medical cause → monitor |
| Stress again later the same day | 🟠 **Follow-up**: check in with the CMO, adjust workload | Two episodes with the same cause in 24 h |
| Any cause, **felt unwell** | 🔴 **See the CMO today**, with buttons: *Tell us what you felt*, *Notify Dr. Ito* | Unexplained heart-rate rise + feeling unwell |

The answer goes into the note for the Crew Medical Officer (CMO), so the doctor gets the number **and** the reason.

Changes that the schedule already explains are not asked about. For example, a high heart rate during the 09:00 exercise session is normal.

## 5. The five tabs

The status line (one sentence, for example *“One change needs your context”*) and the **EMERGENCY** button stay at the top on every tab.

| Tab | What the astronaut does there |
|---|---|
| **Today** | Four plain-word cards (heart, sleep, cabin air, radiation), each with *How to measure* guides. *Needs your input* asks one question at a time. *Coming up* lists today’s reminders. |
| **My body** | A 3D body coloured by today’s data: amber means watch, pulsing red means act now. Tapping an organ shows what happened today, why it matters in space, the data source, and quick *Report* buttons. |
| **Log & messages** | Meals and water, exercise minutes (2.5 h a day, as on the ISS), a **private message** to the flight surgeon or psychologist, and *Report a symptom*. |
| **Health items & report** | Open items followed up as improved / no change / worsened / resolved. One structured report that the astronaut reviews and sends to the CMO or queues for Earth. |
| **Data & sources** | Which onboard device each value comes from, when it last synced, and the NASA documents behind the rules. |

**How to measure** guides (pulse, blood pressure, SpO₂, sleep, cabin CO₂, dosimeter) each answer three questions: *how to measure*, *why it matters*, *what to do if it is not normal*.

**Report a symptom.** Red-flag symptoms (chest pain, palpitations, shortness of breath, strong dizziness) lead to *contact the CMO now*. A headache while cabin CO₂ is high is linked to the cabin, not treated as an illness. The same symptom logged twice within 30 minutes updates one item instead of creating two.

**Cabin pattern.** When 3 of 4 crew show fatigue at the same time and CO₂ is high, the app says *“this may not be about you”* and offers *Notify Commander*. This follows NASA’s own rule: several crew affected at once → check the environment first.

## 6. Emergency

One pulsing **EMERGENCY** button. Pressing it sends an SOS to the CMO and the Commander and queues a message to the flight surgeon on Earth. Then the screen guides a crewmate who is not a doctor, one step per screen:

**“Can the person answer you?”**

- **Yes, awake with chest pain:** stop all activity → help is coming → measure blood pressure, pulse and SpO₂ (with guides) → ask and write down when it started and where it hurts → no medicine without the CMO → stay until the CMO takes over.
- **No, not responding:**
  1. Shout for help and **send someone for the defibrillator (AED)**.
  2. Check breathing for **10 seconds at most**.
  3. **Chest compressions** with an on-screen beat of **110 per minute**, 5–6 cm deep; trained crew add 2 breaths after every 30.
  4. **Use the AED** as soon as it arrives; pause only while it analyses or shocks.
  5. Keep going and **swap every 2 minutes**.

  CPR in weightlessness: alone, the **Evetts-Russomano** method; once the patient is strapped to the medical restraint, the **handstand** method, which is used in the ISS protocol.

**When help arrives**, the astronaut taps **“✓ CMO is here”**.

**A clear ending.** The last step asks *“How did it end?”*, for example *The CMO has taken over* or *The person is breathing again*. A summary then shows a timed list of what happened, what happens next, and when the flight surgeon on Earth will see it. The outcome is saved as a health item.

**Link to Earth (3D).** Next to the steps, a 3D view compares two cases:
- **ISS today:** the flight surgeon connects in under 1 second.
- **Mars:** the alert travels for the live light time and the reply needs as long again, so the app says *“Earth cannot help in time, follow the onboard steps.”*

## 7. Built on the real ISS routine

| On the ISS today | In Solar Guardian, on the way to Mars |
|---|---|
| A flight surgeon at Mission Control guides in real time | The first steps and decisions happen on board; Earth gets the data with a delay |
| Weekly **private medical conference**, a confidential call | A **private message** to the flight surgeon or psychologist, with live arrival and reply times. It is never in the crew report. |
| **2.5 h of exercise** a day on ARED, the T2 treadmill and the CEVIS bike | Two exercise blocks; minutes tracked against 150 |
| **Daily food log** on a tablet, sent to the dietitians weekly | Daily log of meals and water, sent weekly |
| Self-administered **ultrasound**, guided from Earth | Weekly eye-ultrasound reminder |
| Cabin CO₂ and air quality monitored | Cabin air card and the crew-wide CO₂ pattern |
| Preflight tests set each astronaut’s baseline | “Usual” = preflight tests + the last 14 days |

## 8. Built on NASA’s plans

NASA does not have this app. It has published the concept that Solar Guardian follows:

- **NASA ExMC, Clinical Decision Support System Concept of Operations** (HRP-48033, 2022). Crew members log symptoms themselves, follow-up uses *resolved / improved / no change / worsened*, and when several crew are affected the system checks the cabin first.
- **Earth-Independent Medical Operations (EIMO) Concept of Operations** (2025). Medical decisions move gradually from Earth to the spacecraft. The CMO can become the patient, so every crew member must be able to use the system.
- **EIMO Datascope** (2023). One system that combines wearables, environment, exercise data and point-of-care tests.
- **NASA Integrated Medical Model (IMM).** 100 spaceflight medical conditions in three categories. Every health item gets its IMM category, visible under *Clinical details*.
- **CMO-DA** (NASA + Google, 2025). An AI assistant for the CMO. Solar Guardian is not CMO-DA; its report has a machine-readable *Data* view that a tool like it could read.

## 9. Where the data comes from

The app reads these sources; in this prototype their values are simulated.

| Source | Example device | Used for |
|---|---|---|
| Wearable physiology | Smart shirt, like CSA’s **Bio-Monitor** on the ISS | Heart card, heart-rate questions, ECG |
| Point-of-care | Medical kit: blood-pressure cuff, labs | Morning blood pressure |
| Sleep | Wrist actigraph, like the one used on **Artemis II** (NASA ARCHeR study) | Sleep card and question |
| Countermeasures | ARED, T2, CEVIS exercise devices | “Exercise stopped at 70%” question |
| Environment | Cabin atmosphere system + personal CO₂ monitor (tested on the ISS) | Cabin air card, crew-wide pattern |
| Radiation | Personal dosimeter | Radiation card |
| Crew schedule | Planned activities | Deciding which changes need a question |
| **Earth link** | **NASA Deep Space Network, DSN Now feed** | **Live** Earth–Mars light time |

Sync times follow the simulated day; for example, the exercise device shows *waiting* before 09:00 and *09:42* after the session.

## How to run

Chrome or Edge, no installation, no build step.

- **Simple:** open `v2/index.html`. The 3D view and fonts need an internet connection.
- **Recommended:** run a small local server from the repository root, then open `http://localhost:8765/v2/`. For example:

  ```bash
  python -m http.server 8765
  ```

Top-bar controls:
- **SIM** (demo only): drag the slider or press **Play** to move through a simulated day (06:30–22:00); events and questions appear when their time comes.
- **Reset:** starts the day again and clears all answers. Press it before a demo.
- **Clinical details:** shows numbers, ECG and IMM categories for a medical audience. Off by default.

## 11. Demo script

About 90 seconds. Press **Reset** first.

1. **07:05 · Today.** The sleep question appears. Answer *Late work* → explained.
2. **SIM to 14:05.** *Question 1 of 2*: heart rate +24 bpm at 13:10. Answer *Stress* + *No* → explained.
3. **SIM to 16:00.** Cabin pattern, CO₂ high → **Notify Commander**.
4. **SIM to 18:00.** Second heart-rate rise. Answer *Medication taken* + *Yes* → 🔴 *See the CMO today* → press **Tell us what you felt**.
5. **My body** tab: the heart glows red; tap it.
6. **EMERGENCY** → *Not responding* → steps with the 110/min beat → **✓ CMO is here** → *The person is breathing again* → summary.
7. Switch **Link to Earth** between *ISS today* and *Mars*.

## 12. What is real and what is simulated

| Real | Simulated or simplified |
|---|---|
| Live Earth–Mars delay from NASA’s Deep Space Network feed | Health data, crew, schedule and the day |
| SOS sent the moment EMERGENCY is pressed | Device connections (the source names describe the type of system) |
| Every rule visible with its outcome | Limits are general adult values; real ones would be set by flight surgeons |
| CPR guidance from published guidelines | Not a medical device |

- The DSN Now feed is public but not a documented API. If it cannot be reached, the app uses a scenario value (14 min 32 s) and says so.
- There is no AI inside the app. Decisions come from simple, transparent rules.

## 13. Use of Super Intelligence (SI) tools

Space Apps requires every team to describe how SI tools were used (NASA now uses the term *Super Intelligence* instead of *AI*).

| | |
|---|---|
| **Tool** | Claude (Anthropic) |
| **What SI did** | Wrote and debugged the code; found and summarised NASA, CSA and JAXA sources; drafted the English text, this README and the slides |
| **What the team did** | The idea; the design decisions based on mentor feedback (astronaut as the user, tabs, one question at a time, the emergency flow); checked every source; tested the app by hand and reported problems to fix |
| **Inside the app** | No SI. Simple rules that are shown to the user |

## 14. References

- NASA ExMC, *Clinical Decision Support System Concept of Operations*, HRP-48033 (2022). [NTRS 20220017856](https://ntrs.nasa.gov/citations/20220017856)
- Parker, Krihak et al., *Earth-Independent Medical Operations (EIMO) Concept of Operations*, HRP IWS (2025). [NTRS 20250000009](https://ntrs.nasa.gov/citations/20250000009)
- *EIMO Datascope Technical Interchange Meeting* (2023). [NTRS 20240001278](https://ntrs.nasa.gov/citations/20240001278)
- NASA OCHMO, *Integrated Medical Model (IMM) overview*. [nasa.gov](https://www.nasa.gov/nasa-integrated-medical-model-imm-overview/)
- Google Public Sector, *How Google and NASA are testing AI for medical care in space* (8 Aug 2025). [cloud.google.com](https://cloud.google.com/blog/topics/public-sector/how-google-and-nasa-are-testing-ai-for-medical-care-in-space)
- NASA, *The Real Story About Astronaut Health Care in Space* (2024). [nasa.gov](https://www.nasa.gov/missions/station/faq-the-real-story-about-astronaut-health-care-in-space/)
- NASA, *Wearable Tech for Space Station Research* (2024). [nasa.gov](https://www.nasa.gov/missions/station/iss-research/wearable-tech-for-space-station-research/)
- Canadian Space Agency, *Bio-Monitor*. [asc-csa.gc.ca](https://www.asc-csa.gc.ca/eng/sciences/bio-monitor.asp)
- NASA, *ARCHeR: Artemis Research for Crew Health and Readiness*. [nasa.gov](https://www.nasa.gov/reference/archer)
- JAXA, *Medical Operations Team Activities*. [humans-in-space.jaxa.jp](https://humans-in-space.jaxa.jp/en/biz-lab/med-in-space/healthcare/medops/system/)
- Lindsay, Hughes, Caplan, *What the first medical evacuation from the ISS tells us about healthcare in space*, The Conversation (16 Jan 2026). [theconversation.com](https://theconversation.com/what-the-first-medical-evacuation-from-the-international-space-station-tells-us-about-healthcare-in-space-273728)
- NASA, *Deep Space Network: DSN Now*. [eyes.nasa.gov](https://eyes.nasa.gov/dsn/dsn.html)
- European Society of Cardiology, *Cardiac arrest in space: CPR in microgravity* (2025). [escardio.org](https://www.escardio.org/news/press/press-releases/cardiac-arrest-in-space-new-research-shows-that-automatic-chest-compressions-are-more-effective-for-cpr-when-both-rescuer-and-patient-are-floating-in-microgravity/)
