# FitFlow Redesign

## Project Overview

FitFlow is a fitness application redesign project focused on providing a
seamless mobile and web experience with real-time community features,
AI-personalised functionality, secure authentication, and scalable data
management.

This repository contains the supporting documentation and initial project
structure developed for the FitFlow redesign.

## Recommended Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React Native + React Native Web |
| Backend API | Node.js + Express |
| Real-time Communication | Socket.io |
| Primary Database | Firebase Firestore + Realtime Database |
| Secondary/Analytics Database | PostgreSQL |
| Authentication | Firebase Authentication |
| On-device AI | TensorFlow Lite |
| Cloud AI Fallback | Vertex AI / custom FastAPI microservice |
| Caching | Redis |
| Media Storage | Firebase Cloud Storage |
| CI/CD | GitHub Actions |

## Repository Structure

```text
fitflow-redesign/
├── frontend/
├── backend/
├── ai-service/
├── docs/
│   ├── tech-stack-summary.md
│   ├── comparison-matrix.md
│   ├── architecture.png
│   └── adr/
│       └── ADR-001-tech-stack.md
├── .gitignore
└── README.md