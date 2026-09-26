# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

_The working, shareable link that survives real users._

https://activation-first-path.lovable.app 4.

## Data schema

| Entity | Key fields | Notes |
|---|---|---|
| competition_registrations | user_id, competition_id, weight_division_id, registration_status, registration_weight_kg, result, completed_at | Athlete-owned fight camp record. Supports multiple competitions per athlete and links each camp to its competition and weight division. |
| readiness_assessments | registration_id, assessed_on, overall_score, state, components, evidence | Competition-specific readiness snapshot linked to an athlete's registration/fight camp. |

## Access rules

_Who can see / do what? Where are the auth boundaries?_

Authenticated athletes can access only their own private records. Profiles are scoped to auth.uid(), and athlete-owned measurements, wearable connections, competition registrations, weight targets, readiness assessments, recommendations, results and matches are protected by Row-Level Security and ownership checks. Competitions and weight divisions are shared read-only catalogue data.

## Edge cases hardened

| Case | Before | After |
|---|---|---|
| Empty / first-run state | Hardcoded demo data could appear when real athlete data was missing. | Contextual empty states with clear CTAs; Today offers Find a Competition, incomplete profiles offer Complete Profile, and empty history is handled explicitly. |
| Bad / malicious input | Input validation and cross-table ownership checks were incomplete. | Validated inputs plus RLS ownership checks prevent invalid data and cross-account access. |
| Failure / offline | Backend failures could silently continue or leave the UI without useful feedback. | Loading states, inline errors and Retry actions were added; failed saves preserve or restore persisted state and the authenticated session survives request failures. |

## Stress test results

_What you threw at it, and what held / broke._

Kill Switch: with the network set to Offline, the sign-in request failed gracefully and the UI displayed an inline NetworkError instead of hanging or showing a blank screen. Duplicate registration protection was also verified: duplicate live registrations are blocked by the database uniqueness constraint, preventing duplicate fight camps.
