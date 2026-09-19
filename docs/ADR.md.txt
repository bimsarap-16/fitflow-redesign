# ADR-001: 

## Status
Accepted for the redesign prototype 

## Context

FitFlow needs a redesign covering AI-personalised workout plans, social/community features, and nutrition tracking. The redesign must be shipped by a small-to-mid-sized team across iOS, Android, and web, while controlling cost and time-to-market. This decision follows the user research and design work in Labs 1–4, and the technology comparisons carried out in this lab's Activities 1–3.

## Decision

We will use:
- **React Native** for the client (mobile + web via React Native Web)
- **Node.js + Express** for the backend API, with **Socket.io** for real-time features
- **Firebase** (Firestore + Realtime Database + Authentication + Cloud Storage) as the primary data, identity, and media layer
- **PostgreSQL** as a secondary analytics/reporting store
- **Redis** for caching
- **TensorFlow Lite** for on-device AI personalisation, with a cloud-hosted model as fallback
- **GitHub Actions** for CI/CD

## Alternatives Considered

- **Flutter** — close second on the frontend (4.15/5 vs React Native's 4.70/5); smaller ecosystem and hiring pool tipped the decision to React Native.
- **Kotlin Multiplatform** and **native Swift/SwiftUI** — rejected; neither meets the "seamless iOS/Android/web" requirement without duplicating significant UI work.
- **NestJS + PostgreSQL + Auth0** and **FastAPI + MongoDB + Cognito** — both scored lower (3.50/5 and 3.60/5 respectively vs 4.55/5) on development speed and cost/maintainability for a mid-sized team.

## Consequences

### Positive

- A single primary language (JavaScript/TypeScript) across frontend and backend simplifies hiring and code sharing.
- Firebase's real-time listeners map directly onto the social/community requirements without custom WebSocket infrastructure.
- TensorFlow Lite keeps AI personalisation working offline and reduces cloud inference cost.
- This matches the stack the case study confirms was actually shipped, so the retrospective outcomes (SUS rising from 68 to 87, 35% retention increase) can be attributed with confidence to the design work rather than a different technology choice.

### Negative / Trade-offs

- Firestore's query limitations mean some reporting needs a secondary PostgreSQL store, adding one more moving part to operate.
- Firebase is a single-vendor dependency for a large part of the stack; a future migration off Firebase would touch most of the backend.
- HIPAA/GDPR compliance requires deliberate configuration (signed BAA, data residency selection, server-side security rules) rather than being automatic with this stack.

## Revisit If

- The team scales past roughly 15 backend engineers (NestJS's enforced structure would start to pay off).
- A proven bottleneck emerges that Node.js cannot handle cost-effectively (Go becomes worth evaluating).
- Deep native health-sensor integration becomes a priority (a native Swift/Kotlin module could be added alongside React Native rather than replacing it).