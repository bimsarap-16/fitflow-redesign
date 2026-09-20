# ADR-001: Adopt React Native + Node.js/Express + Firebase + TensorFlow Lite for the FitFlow Redesign

## 4.2 Architecture Decision Record

| Field | Details |
|---|---|
| **ID / Title** | ADR-001: Adopt React Native + Node.js/Express + Firebase + TensorFlow Lite for the FitFlow Redesign |
| **Status** | Accepted |
| **Date** | 2026.08.30 |
| **Context** | FitFlow needs a redesign covering AI-personalised workouts, social/community features, and nutrition tracking, shipped by a small-to-mid-sized team across iOS, Android, and web, while controlling cost and time-to-market (Labs 1–2 research; this lab's Activities 1–3 comparison). |
| **Decision** | Use React Native for the client (mobile + web), Node.js/Express for the backend API with Socket.io for real-time features, Firebase (Firestore + Realtime Database + Authentication + Cloud Storage) as the primary data/identity/media layer, PostgreSQL as a secondary analytics store, Redis for caching, and TensorFlow Lite for on-device AI personalisation with a cloud model as fallback. |
| **Alternatives considered** | Flutter (close second on the frontend; smaller ecosystem/hiring pool tipped the decision to React Native); Kotlin Multiplatform and native Swift (rejected — do not meet the seamless cross-platform requirement without duplicating UI work); NestJS+PostgreSQL+Auth0 and FastAPI+MongoDB+Cognito (both scored lower on development speed and cost/maintainability for a mid-sized team — Activity 3.3). |
| **Consequences (positive)** | Single primary language (JS/TS) across frontend and backend simplifies hiring and code sharing; Firebase's real-time listeners map directly onto the social/community requirements; TensorFlow Lite keeps AI personalisation working offline and reduces cloud inference cost; matches the stack the case study confirms was actually shipped, so retrospective outcomes (SUS 68→87, 35% retention increase) can be attributed with confidence to design, not a different tech stack. |
| **Consequences (negative / trade-offs)** | Firebase's query limitations mean some reporting needs a secondary PostgreSQL store, adding one more moving part; Firebase is a single-vendor dependency for a large part of the stack, so a future migration off Firebase (if ever needed) would touch most of the backend; HIPAA/GDPR compliance requires deliberate configuration (BAA, data residency, security rules) rather than being automatic. |
| **Revisit if** | The team scales past ~15 backend engineers (NestJS's structure would start to pay off), a proven bottleneck emerges that Node.js cannot handle cost-effectively (becomes worth evaluating), or deep native health/sensor integration becomes a priority (a native Swift/Kotlin module could be added alongside React Native rather than replacing it). |