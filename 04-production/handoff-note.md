# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

READY TO GO is a competition-preparation control center for Brazilian Jiu-Jitsu athletes. It helps an athlete answer three questions during fight camp: Am I ready to compete? Will I make weight? What should I do today? The prototype covers athlete onboarding, wearable connection, UAE competition discovery, registration, weight and fight-readiness assessment, daily recommendations, and athlete profile management. It now uses authenticated accounts and persistent backend data while preserving the original end-to-end demo journey.

## Architecture (plain language)

- **Frontend:** React 19 + TypeScript on TanStack Start, Vite 8, Tailwind CSS v4, shadcn/Radix UI, and lucide-react. Product code is organised by feature under src/features/ready-to-go/, including landing, onboarding, navigation, today, weight, readiness, competitions, registration, profile, shared components, and data/domain types.
- **Backend / data:** Supabase provides authentication and persistent application data. Each athlete has private account-scoped data including athlete profile, wearable connection, measurements, fight-camp registration, weight targets/checkpoints, readiness assessments, daily recommendations, and competition records. The UAE competition calendar is database-backed. Profile edits, Garmin connect/disconnect state, and registrations persist across reloads. New prototype accounts are seeded with demo data; email confirmation is disabled for instant prototype sign-up.
- **Key flows:** 1. Sign up / sign in → athlete onboarding → wearable connection → profile confirmation → Today.
2. Pre-camp Today → Find a Competition → UAE competition calendar → event detail.
3. Competition registration → confirm belt and age division → current weight → select weight division → confirm registration → first assessment.
4. Active fight camp → Today → Weight → Readiness → Competitions → Profile.
5. Profile edits, wearable connection state, and fight-camp registration persist through the backend.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Core product flow + persistence | solid | End-to-end onboarding, competition registration, authenticated athlete experience, five core screens, Supabase persistence, and account-scoped athlete data are implemented. |
| Wearable + readiness logic | rough | Garmin/WHOOP/Apple Health integrations are still mocked; wearable values and readiness methodology are prototype data/logic rather than production integrations. |

## Risks & assumptions for the team

Real wearable integrations remain the largest technical unknown, including OAuth, API limits, data normalization, and sync behavior. The readiness model and weight projections still require validated production methodology. The prototype is primarily designed around BJJ and a demo athlete/scenario. Health-adjacent data requires appropriate privacy and security controls. Some demo data remains seeded or synthetic, and automated test coverage is not yet established.

## How to run it

```
Run the project through its Lovable hosted environment or local development setup. For local development: install dependencies with npm i, start with npm run dev, and open the local URL printed by Vite. Use npm run build for a production build, npm run preview to preview it, and npm run lint for linting. Supabase must remain configured for authentication and persistent data.
```
