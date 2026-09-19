# READY TO GO — Living PRD

## Product
**READY TO GO — Fight Camp Control Center**

A competition-preparation application for combat-sport athletes. The MVP is focused on Brazilian Jiu-Jitsu (BJJ). Wearables provide data; READY TO GO turns wearable data, weight, and competition context into preparation decisions.

## Product Hypothesis
BJJ competitors preparing for an event need a simple way to understand whether they are ready to compete, whether they will make weight, and what they should do today. Combining competition context, athlete profile, weight trajectory, training, and recovery into one fight-camp experience should make those decisions faster and clearer.

## Primary User
A BJJ competitor who trains regularly, competes in defined age/belt/weight divisions, may use Garmin/WHOOP/Apple Health, and wants actionable preparation guidance rather than another raw fitness dashboard. Initial context: UAE, especially Abu Dhabi and Dubai.

## Core Questions
1. Am I ready to compete?
2. Will I make weight?
3. What should I do today?

## Core Product Model
An **Athlete** can exist without a competition. A **Fight Camp** begins only when the athlete selects/registers for a competition.

`Create / Import Athlete → Complete Athlete Profile → TODAY → optionally Find Competition → Register → Fight Camp`

Competition registration is not mandatory onboarding.

## MVP Scope
### In Scope
- Athlete onboarding
- Wearable connection
- Athlete profile
- Persistent authenticated navigation
- TODAY
- UAE competition discovery
- Competition registration
- Weight Readiness
- Fight Readiness
- Fight-camp state
- Loading, empty, and error states
- Persistent backend for core product data

### Out of Scope
- Tournament administration
- Coach/team dashboards
- Multi-athlete management
- Voice interaction
- Medical diagnosis
- Aggressive dehydration/weight-cut protocols
- Generic fitness coaching
- Full wearable replacement

## Primary Navigation
- TODAY
- WEIGHT
- READINESS
- COMPETITIONS
- PROFILE

Training and Recovery are readiness inputs, not separate top-level destinations.

## Screens

### Homepage / Landing
Value proposition and entry point.
Primary actions: **Create Account** and **Import Athlete Data**.
Core message: **Your fight camp starts here.**

### Athlete Onboarding
Progressive onboarding:
1. Personal identity
2. Wearable connection
3. BJJ profile
4. Current weight
5. Review
6. Profile created

Rules:
- Wearable connection can be skipped.
- DOB should derive age division where possible.
- Sport is fixed to Brazilian Jiu-Jitsu for MVP.
- Target competition weight is not requested during generic onboarding.

### Wearable Connection
Product direction: Garmin, WHOOP, Apple Health.
Current demo source: **Garmin Fenix 7X**.
Wearables provide inputs; READY TO GO provides interpretation and decisions.

### TODAY
Primary decision screen.

Without active competition:
- show athlete identity and wearable context;
- show **No upcoming competition**;
- show **Find a Competition** CTA;
- do not fabricate competition-specific Weight/Fight Readiness.

With active competition:
- competition countdown;
- weight status;
- fight readiness;
- today's recommendation;
- relevant checkpoints.

### WEIGHT
Answers **Will I make weight?**

Inputs: competition/weigh-in date, target weight, current/historical weight, trend, days remaining.

States:
- ON TRACK
- AT RISK
- OFF TRACK

Outputs may include current/target weight, kg remaining, required vs actual trend, projected weigh-in weight, trajectory, checkpoints, and a simple recommendation.

Do not provide dangerous dehydration, diuretic, sauna, starvation, or similar aggressive weight-cut instructions.

### READINESS
Answers **Am I ready to compete?**

READY TO GO uses a transparent competition-readiness model rather than copying Garmin Training Readiness.

Score: 0–100.

Components:
- Recovery
- Training
- Weight
- Competition Prep

States:
- READY
- BUILDING
- AT RISK
- NOT READY

Fight-camp phases:
- BUILD
- PEAK
- TAPER
- COMPETE

Recommendations depend on athlete state and time remaining.

### COMPETITIONS
Discover/select competitions. Initial filters:
- All UAE
- Abu Dhabi
- Dubai

Competition selection is voluntary.

### Competition Registration
1. Select event/date
2. Confirm belt
3. Confirm/verify age division
4. Confirm current weight
5. Select weight category
6. Show consequence
7. Review
8. Confirm registration
9. Start fight camp

Success direction: **You're registered. Your fight camp starts now.**

### PROFILE
Persistent athlete identity.

Core data:
- name
- nationality
- DOB
- academy/club
- belt
- sport
- wearable connection
- competition history/statistics where available

Editable: name, nationality, DOB, academy/club, belt.
Sport: BJJ, fixed for MVP.
Competition history: read-only.
Wearable: manageable.

## Key Flows
### New Athlete
`Homepage → Create Account → Athlete Onboarding → Profile Created → TODAY`

### Import Athlete Data
`Homepage → Import Athlete Data → Select Wearable → Connect → Complete Athlete Profile → TODAY`

### Athlete Without Competition
`TODAY → No Upcoming Competition → Find a Competition`

PROFILE and COMPETITIONS remain accessible without registration.

### Start Fight Camp
`COMPETITIONS → Select Competition → Registration → Confirm → Fight Camp Created → TODAY`

### Active Fight Camp
`TODAY → Weight / Readiness / Competition context → daily decision`

## TODAY Decision Model
During an active camp, prioritize concise guidance such as:
- BJJ intensity
- Strength intensity
- Cardio recommendation
- Recovery priority
- Sleep target
- Weight checkpoint

The goal is decision before raw data.

## Data Sources
Athlete-entered data includes identity, DOB, nationality, academy, belt, current weight, competition, and division.

Wearable inputs may include HRV, sleep, resting HR, stress, Body Battery, activity/training history, training-status signals, VO2 max, and weight where available.

Architecture direction:
`Wearable Adapter → Normalized Athlete Snapshot → READY TO GO Engines → UI`

## Demo Athlete / Prototype Data
Consistent demo athlete:
- Stepan Yuschishin
- Ukraine
- De La Riva Abu Dhabi
- Brazilian Jiu-Jitsu
- Masters 1
- White Belt
- Garmin Fenix 7X

Prototype wearable values include:
- Weight: 92.0 kg
- HRV last night: 53 ms
- HRV weekly average: 55 ms
- Sleep score: 78
- Resting HR: 51 bpm
- VO2 max: ~49

Competition records/scenarios may be synthetic and must not be represented as verified wearable data.

## Example Fight Camp Scenario
Example prototype scenario:
- current weight: 92.0 kg
- target: 88.3 kg
- 19 days remaining
- 3.7 kg remaining
- projected weigh-in: 89.1 kg
- Weight Readiness: AT RISK
- Fight Readiness: 74 / BUILDING

These values demonstrate product behavior, not a real-world weight-cut prescription.

## UX Principles
- Athlete-first, not enterprise-dashboard-first.
- Decision before data.
- Progressive onboarding.
- One clear primary action per step.
- Competition is optional until the athlete starts a fight camp.
- Empty states explain what is unavailable and how to activate it.
- Never fabricate competition-specific insights without a competition.
- Preserve TODAY and PROFILE access after athlete creation.
- Mobile-first with strong desktop support.

## Visual Direction
Premium combat-sports editorial design with strong typography, restrained accents/status colors, and BJJ imagery. Avoid generic wearable dashboards, sci-fi/gaming HUDs, excessive glassmorphism, and toy-like cards.

## Current Prototype Decisions
- BJJ only for MVP.
- Athlete profile exists independently from competition.
- Persistent authenticated navigation.
- TODAY has a no-competition state.
- Weight/Fight Readiness become competition-specific with an active fight camp.
- Garmin is the primary demo wearable.
- Prototype mixes mocked/synthetic data with wearable-derived values.
- Core code has been refactored by feature/screen in the build tool.

## Backend Requirements
Persist:
- authenticated users
- athlete profiles
- wearable connections
- athlete measurements / normalized snapshots
- competitions
- registrations / fight camps
- weight targets/checkpoints
- readiness assessments
- daily recommendations

Authorization must ensure athletes can access only their own private profile/preparation data.

## Success Criteria
An athlete can:
1. create/import and complete a profile;
2. enter TODAY without mandatory competition registration;
3. find/register for a competition;
4. start a fight camp;
5. understand weight status;
6. understand fight readiness;
7. receive a clear recommendation for today.

## Risks and Assumptions
- Wearable APIs expose different metrics and require normalization.
- Some integrations may initially be mocked/partial.
- Competition data may be manually seeded.
- Readiness logic requires future validation.
- Weight projections depend on sufficient recent measurements.
- Demo data is not equivalent to production integration.
- Backend/auth should progressively replace hard-coded state without breaking the demonstrated journey.

## Product Principle
**Wearables give the athlete data. READY TO GO gives the athlete decisions.**
