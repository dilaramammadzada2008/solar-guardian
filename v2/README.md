# Solar Guardian v2 · Crew Self-Care

The crew-facing self-care front end of an onboard **clinical decision support system (CDSS)**. It was rebuilt after mentor feedback at NASA Space Apps Challenge 2026 (Vilnius). The first version is still in the repository root.

## Design basis: what NASA is already planning

NASA does not have this as a finished app. NASA's Human Research Program, **Exploration Medical Capability (ExMC)** element, has published the concept that v2 follows:

- **ExMC Clinical Decision Support System Concept of Operations**, HRP-48033 (2022). [NTRS 20220017856](https://ntrs.nasa.gov/citations/20220017856)
  - Crew members log symptoms themselves, and the system cross-checks them with other data.
  - Follow-up uses the statuses *resolved / improved / no change / worsened*.
  - When several crew show symptoms at the same time, the system checks the cabin atmosphere first and alerts the CMO and the Commander.
  - The system is meant to run on laptop-class hardware and to communicate asynchronously with the ground.
- **Earth-Independent Medical Operations (EIMO) Concept of Operations**, HRP Investigators' Workshop (2025). [NTRS 20250000009](https://ntrs.nasa.gov/citations/20250000009)
  - Medical decisions move gradually from Earth to the spacecraft.
  - It includes a scenario on self-medical management and behavioural health.
  - The CMO can become the patient, so every crew member must be able to use the system.
- **EIMO Datascope Technical Interchange Meeting** (2023). [NTRS 20240001278](https://ntrs.nasa.gov/citations/20240001278)
  - Describes a "system of systems" that combines wearables, environmental controls, countermeasures (exercise) data, behavioural data, point-of-care tests and medical records.

- **NASA Integrated Medical Model (IMM).** [nasa.gov overview](https://www.nasa.gov/nasa-integrated-medical-model-imm-overview/)
  - A probabilistic model of 100 spaceflight medical conditions, used to plan medical kits and to estimate mission medical risk.
  - The conditions are grouped into three categories: environmental, injury/trauma and medical illness.
  - v2 tags every health item with its IMM category, so onboard events can be compared with IMM incidence data.
- **Crew Medical Officer Digital Assistant (CMO-DA).** NASA and Google proof of concept, announced 8 Aug 2025 ([Google Public Sector blog](https://cloud.google.com/blog/topics/public-sector/how-google-and-nasa-are-testing-ai-for-medical-care-in-space)).
  - An AI clinical decision support system that supports the CMO.
  - v2 is not CMO-DA and contains no AI. It collects the crew member's data and context and hands them over in a structured, machine-readable form (**Data** view of the report) that a tool like CMO-DA could read.

## Mentor feedback → v2

| Feedback | v2 |
|---|---|
| Who is the user? Too complex for an astronaut, too much for a doctor | **One user: the crew member.** The CMO receives the crew member's report; that is a separate role. |
| NASA already has systems like this. Integrate with them | **No own measuring.** v2 reads from the data sources in NASA's CDSS concept: wearable physiology, point-of-care kit, sleep sensor, exercise device, cabin atmosphere, dosimeter and crew schedule. |
| Not just numbers. What happened at that time? | **Context requests.** When data deviates from the personal baseline and the crew schedule can't explain it, the crew member is asked what was happening. The answer is stored with the data and goes into the report. |
| No camera measurements | Removed |

## Also from the official challenge brief (Brazilian Space Agency video)

| Brief | v2 |
|---|---|
| "A crewmate feels a sharp pain in the chest and collapses. What should you do?" | **EMERGENCY** button: step-by-step guidance, one step per screen. **Awake with chest pain**: stop activity, help is alerted, measure vital signs, note the answers, no medicine without the CMO. **Not responding**: check breathing (10 s at most), chest compressions with a 110/min beat, AED. Includes CPR methods for weightlessness: Evetts-Russomano alone, handstand once the patient is restrained (DGLRM / ESAM guideline; the ISS protocol uses the handstand method). |
| "Astronauts are not doctors: explain how to take each measurement, why it matters, and what to do when a value is not normal" | **How to measure** guides for pulse, blood pressure, SpO₂, sleep, cabin CO₂ and the dosimeter. |
| "Remind the crew to take measurements" | **Coming up** list with due items. |

## Screen

- **Status bar.** One state with one sentence: NOMINAL, CONTEXT, FOLLOW-UP, CABIN or CONTACT CMO.
- **Four plain-word cards.** Heart, sleep, cabin air and radiation: a word, one sentence, and *How to measure* links. No numbers on the main screen.
- **Clinical details** (switch in the top bar, off by default). Shows the numbers for the medical officer: live vitals with 6-hour trends, a single-lead ECG, IMM categories and the machine-readable report. The astronaut's screen stays simple.
- **Earth reply time, live.** Read from the public feed of NASA's Deep Space Network ([DSN Now](https://eyes.nasa.gov/dsn/dsn.html)). The round-trip light time to the Mars orbiters MRO, Mars Odyssey and TGO is halved, so the delay follows today's real Earth–Mars distance. If the feed cannot be reached, the scenario value (14 min 32 s) is used and labelled as such.
- **Body overview.** A 3D anatomical model (three.js) with skin, skeleton, organs and vessels. Each body system is coloured from today's data: a system that needs watching glows amber, one that needs action pulses red. Tapping a system shows what happened today, why it matters in space, the data source, and quick links to report a symptom there.
- **Context requests.** Each request shows what changed, the evidence, the data source, and structured answers. Every outcome shows the rule that produced it.
- **Timeline.** Crew schedule, heart rate against the personal baseline, cabin CO₂, symptom markers, and whether context has been added.
- **Open health items.** Follow-up with improved / no change / worsened / resolved. "Worsened" or a red flag offers *Notify CMO*.
- **Report a symptom.** Symptom, onset and severity. Red-flag symptoms go to the CMO. A symptom that matches elevated CO₂ is linked to the cabin.
- **Report to medical officer.** A structured note that the crew member reviews, then sends to the CMO or queues for the flight surgeon (arrival time from the live Earth–Mars light time).

## Demo (about 90 s)

Use the **SIM** slider or **Play**. **Reset** restarts the day.

1. **07:05.** Short sleep. Answer *Late work* → explained.
2. **10:00.** Exercise stopped at 70%. Answer *Felt tired* → a fatigue follow-up item opens.
3. **14:05.** Unexplained heart-rate rise. Answer *Stress*, felt unwell *No* → explained.
4. **16:00.** Crew-wide pattern: CO₂ high. Press *Notify Commander* → the backup scrubber comes on. Log *Headache 4/10* → it is linked to the cabin.
5. **18:00.** Second heart-rate rise. Answer *Stress*, felt unwell *Yes* → CONTACT CMO. Then send the report.

## Limitations

- All health data is simulated. Source names describe the type of system (for example CSA's Bio-Monitor smart shirt), not a live connection. Only the Earth–Mars light time is live.
- The DSN Now feed is public but not a documented API; its format may change, so the app falls back to the scenario value.
- The decision rules are simple and transparent. Real thresholds would be set by flight surgeons. This is not a medical device.

## Use of Super Intelligence (SI) tools

Claude (Anthropic) was used to find and summarise the NASA ExMC documents, and to write code and text. The team chose the direction based on mentor feedback and tested the app by hand. See section 17 of the main README.
