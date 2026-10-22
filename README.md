# NASA Space Apps 2026 — MODIS & VIIRS Hotspot Harmonization

> NASA Space Apps Challenge 2026 project: a web-based exploration tool for harmonizing and comparing NASA FIRMS active-fire hotspot detections from MODIS and VIIRS.

## Project Overview

This project explores historical active-fire hotspot detections from NASA FIRMS and provides a practical way to compare MODIS and VIIRS observations over the same area and time period.

The MVP is designed around a simple scientific rule: **a hotspot detection is an observation, not necessarily an individual fire**. MODIS and VIIRS detections are therefore kept separate and are never simply added together. Any anomaly-style view is descriptive of historical activity and must not be presented as a prediction or early-warning system.

## MVP Goals

The MVP should allow a user to:

1. Select a study region/area and date range.
2. Explore aggregated active-fire detections on a map.
3. Review daily, monthly, and yearly activity patterns.
4. Compare MODIS and VIIRS detection counts and standardized metrics.
5. Understand the data sources, methodology, limitations, and known data gaps.
6. Continue demonstrating the core experience through an offline/local fallback if hosted services are unavailable.

### Out of Scope for the MVP

- Real-time operational fire monitoring.
- Fire prediction or early-warning claims.
- Treating each hotspot as a unique fire.
- Adding MODIS and VIIRS counts together as a single fire count.
- Complex machine-learning forecasting when historical coverage does not support it.
- Features that are not required for the core challenge demonstration.

## Workstreams

The project is divided into four technical workstreams plus cross-cutting coordination/documentation:

| Workstream | Primary responsibility | Main dependency |
|---|---|---|
| **Data** | NASA FIRMS access, raw-file preservation, cleaning rules, validation, summaries | Starts first |
| **Backend** | ASP.NET Core API, SQL Server schema/importer, aggregation, endpoints | Data definitions + API contract |
| **Frontend** | React/TypeScript UI, map, calendars, comparison views, methods page | API contract; can start with mocks |
| **AI / Anomaly** | Historical coverage assessment and reproducible anomaly/percentile analysis | Validated historical data |

## Recommended Execution Order

```text
PHASE 1 — FOUNDATION

Coordination / Scope
        │
        ├───────────────┐
        ▼               ▼
      DATA          BACKEND
        │               │
        ▼               ▼
   Data Quality     API Contract
        │               │
        └───────┬───────┘
                ▼
        Frontend Mock Integration

PHASE 2 — PARALLEL BUILD

DATA ───────────────► Backend Importer / Database ─────► API
  │                                                        │
  └──────────────► AI / Anomaly Analysis                   │
                                                           ▼
FRONTEND (mock data) ───────────────────────────────► Live Integration

PHASE 3 — INTEGRATION

API + validated data + anomaly decision
                 │
                 ▼
       Map + Calendar + Comparison
                 │
                 ▼
        Methods / Limitations

PHASE 4 — RELEASE

E2E QA → deployment → offline fallback → demo rehearsal → submission
```

### Parallel-work rule

Frontend does **not** need to wait for the production database. It can build screens and interactions against stable mock JSON once the API contract is agreed.

Data work should start as early as possible because the quality and historical coverage of the source data determine what can safely be shown by Backend and AI/Anomaly.

AI/Anomaly work can prepare its environment and inspect coverage early, but final anomaly analysis must use validated metrics. If the historical series is insufficient, the team should fall back to descriptive historical percentiles or omit anomaly labels rather than inventing a predictive model.

## Timeline

| Target | Focus |
|---|---|
| **Oct 22–25, 2026** | Scope, study region, data inspection, API contract, anomaly feasibility |
| **Oct 26–Nov 1** | Importer/database, frontend mock UI, data validation, anomaly baseline |
| **Nov 2–8** | API integration, comparison views, methods page, testing, feature freeze |
| **Nov 9–13** | Stabilization, deployment, fallback verification, rehearsal, integrated MVP |
| **Nov 14–15** | Presentation and final submission |

## Architecture

```text
NASA FIRMS files
      │
      ▼
Data validation / cleaning
      │
      ▼
SQL Server
      │
      ▼
ASP.NET Core Web API
      │
      ├──────────────► Aggregations / comparison metrics
      │
      └──────────────► Optional anomaly / percentile results
      │
      ▼
React + TypeScript frontend
      │
      ├── Map Explorer
      ├── Activity Calendar
      ├── MODIS vs VIIRS Comparison
      └── Methods & Limitations
```

## Technology Stack

### Backend

- ASP.NET Core Web API
- C#
- SQL Server
- REST/JSON API
- Automated API/data tests

### Frontend

- React
- TypeScript
- Interactive map visualization
- Responsive web UI

### Data

- NASA FIRMS active-fire hotspot data
- MODIS
- VIIRS
- Reproducible cleaning and aggregation pipeline

### AI / Analysis

- Python may be used for exploratory/reproducible analysis.
- Historical percentiles/baselines are preferred when they are scientifically supportable.
- Any anomaly result must be clearly labeled as descriptive historical analysis, not prediction.

## Data & Scientific Rules

The application must preserve the distinction between **sensor observations** and **fires**.

- Count hotspot detections, not individual fires.
- Keep MODIS and VIIRS counts separate.
- Do not sum MODIS + VIIRS and call the result a fire count.
- Document the selected study region and date range.
- Preserve raw source files where possible for reproducibility.
- Record rejected/invalid rows during import.
- Validate database summaries with an independent recount.
- Report important data gaps and limitations.
- Use consistent definitions and aggregation rules across the comparison views.

## Repository Work Management

The repository's linked GitHub Project is the central execution board.

All implementation work is documented as GitHub Issues and is intentionally **unassigned** at creation time. Issue titles use the workstream name so the backlog can be filtered into:

- Backend
- Frontend
- Data
- AI / Anomaly
- Coordination / QA / Infrastructure

Issue descriptions include dependencies and acceptance criteria so contributors can identify the correct starting point and parallelizable work without relying on tribal knowledge.

### Dependency strategy

- **Start first:** project scope, data access/study region, initial data inspection, backend/frontend foundations.
- **Next:** data definitions + API contract.
- **Parallel:** backend importer/database, frontend mock implementation, data validation, and anomaly feasibility work where dependencies permit.
- **Integration:** API endpoints → live frontend → comparison → methods/limitations.
- **Final:** end-to-end QA → deployment → offline fallback → presentation/submission.

## Release Checkpoints

### Feature freeze — Nov 6

Only bug fixes and critical integration changes should be accepted after the feature freeze.

### Code freeze — Nov 10

No feature additions after code freeze. Only release-blocking fixes should be merged.

### Deployment — Nov 11

Validate the hosted frontend, API, database connectivity, and fallback path.

### Integrated MVP — Nov 13

The complete demonstrable flow should be working, with methodology and limitations clearly documented.

## Project Documentation

The GitHub Issues and linked Project contain the detailed implementation backlog, dependencies, acceptance criteria, and workstream breakdown.

See the repository's **Issues** and linked **Projects** tabs for the current execution state.

## Challenge Focus

This project is being developed for the **NASA Space Apps Challenge 2026**. The application prioritizes scientific transparency, reproducibility, clear sensor comparison, and a reliable demo over unsupported predictive claims.

## License

License and NASA data attribution details will be added with the final release documentation according to the applicable source-data and challenge requirements.
