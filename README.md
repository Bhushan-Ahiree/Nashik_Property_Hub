# Nashik Property Hub — PropTech Data Platform

> Real-time property market intelligence for Pune & Nashik.  
> Production backend engineered with FastAPI · Celery · Redis · Docker · MongoDB.

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Docker Network                      │
│                                                      │
│  ┌──────────┐    ┌──────────┐    ┌───────────────┐  │
│  │  FastAPI  │───▶│  Redis   │───▶│ Celery Worker │  │
│  │  (API)   │    │ (Broker) │    │ (Analytics)   │  │
│  └──────────┘    └──────────┘    └───────────────┘  │
│        │                                 │           │
│        ▼                                 ▼           │
│  ┌──────────┐                    ┌──────────────┐   │
│  │  Motor   │                    │   Scraping   │   │
│  │(MongoDB) │                    │   Engine     │   │
│  └──────────┘                    └──────────────┘   │
└─────────────────────────────────────────────────────┘
```

## Tech Stack

| Layer | Technology |
|-------|------------|
| API | FastAPI (async) |
| Task Queue | Celery + Redis broker |
| Database | MongoDB via Motor (async driver) |
| Validation | Pydantic v2 schemas |
| Containerisation | Docker multi-container network |
| Scraping | Beautiful Soup 4 |

## Key Engineering Decisions

- **Idempotent ingestion** — Every property record passes through a deduplication engine before write. Guarantees zero data corruption across all ingestion stages regardless of scrape frequency.
- **Async-first** — FastAPI + Motor means zero blocking I/O on the primary API. Heavy compute (market analytics, trend aggregation) is offloaded to Celery workers via Redis broker.
- **Decoupled services** — Each container runs a single responsibility. The scraping engine, API server, and analytics workers are fully isolated — one service failing doesn't cascade.

## What It Tracks

- Property prices across Pune and Nashik micro-markets
- Area-level trend data for investor-facing analytics
- Automated ingestion from multiple real estate sources

## Status

- 🟢 Live in production
- 📍 Covering Pune & Nashik real estate markets
- 📸 @nashik_propertyhub — 5,000+ followers

## Author

**Bhushan Ahire** — Backend Python Developer
- [LinkedIn](https://www.linkedin.com/in/bhushan-ahiree/)
- bhushan.ahire.dev@gmail.com
