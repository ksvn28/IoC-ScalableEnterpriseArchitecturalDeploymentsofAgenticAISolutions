# System Architecture — AgentOps Console

**Author:** Shree Vekka Narayanee K | **Roll No:** 2023103620  
**Deployed Link:** https://picture-perfect-render-61.lovable.app

---

## Overview
AgentOps Console is a React single-page application styled as a Space Mission Control interface. It provides a unified enterprise dashboard for monitoring, orchestrating, and securing AI agents deployed across distributed environments.

## Architecture Layers

```
┌──────────────────────────────────────────────────────┐
│                    CLIENT LAYER                      │
│     React + TypeScript SPA  |  Vite Build Tool       │
├──────────────────────────────────────────────────────┤
│                  PRESENTATION LAYER                  │
│  Space-themed UI  |  Orbitron Font  |  Star Field BG │
│  Recharts (line/area)  |  Tailwind CSS Design Tokens │
├──────────────────────────────────────────────────────┤
│                  COMPONENT LAYER                     │
│  Sidebar Nav      │  KPI Instrument Cards            │
│  Kanban Board     │  Orbital Events Feed             │
│  Agent Table      │  Log Viewer + Search             │
│  Deployment Timeline  │  Security Event Table        │
├──────────────────────────────────────────────────────┤
│                    DATA LAYER                        │
│     Static TypeScript mock data fixtures             │
│     Simulated real-time log + event streaming        │
├──────────────────────────────────────────────────────┤
│                 DEPLOYMENT LAYER                     │
│        Lovable CDN  —  Global Edge Network           │
│     HTTPS  |  picture-perfect-render-61.lovable.app  │
└──────────────────────────────────────────────────────┘
```

## Pages & Trust Boundaries

| Page | Access Level | Function |
|---|---|---|
| Overview | All users | Fleet-wide KPIs, 7-day activity chart, Orbital events feed |
| Agents | Operator+ | Agent registry, status monitoring, uptime tracking |
| Workflows | Operator+ | Kanban task orchestration (Queued → Running → Review → Done) |
| Security | Admin only | Auth events, severity-tagged alerts, open incident table |
| Deployments | DevOps+ | Rocket-sequence pipeline (Dev → Staging → Canary → Production) |
| Logs & Traces | Operator+ | Full-text searchable, color-coded by severity level |

## Integrations
- **Recharts** — time-series line chart with Tasks and Errors overlay
- **React Router v6** — client-side navigation between all 6 pages
- **Tailwind CSS** — design token system, dark/space theme
- **Google Fonts** — Orbitron + Space Mono for mission-control typography
