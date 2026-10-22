# GitHub Project Board — NASA Space Apps 2026

**Project:** https://github.com/users/salmahmed6/projects/5/views/1  
**Repository:** https://github.com/salmahmed6/Harmonization-of-MODIS-and-VIIRS-Hot-Spots  
**Issues:** https://github.com/salmahmed6/Harmonization-of-MODIS-and-VIIRS-Hot-Spots/issues

This guide defines the intended Project V2 setup for the repository backlog. All dates are targets, not claims of completed work.

## Workflow

Use the built-in **Status** field with options: **Backlog → Ready → In progress → Blocked → In review → Done**. Mark an item Done only when its acceptance criteria are met and evidence is available. Keep all issues unassigned until the team agrees ownership.

## Recommended fields

| Field | Type | Values |
|---|---|---|
| Status | Built-in status | Backlog, Ready, In progress, Blocked, In review, Done |
| Workstream | Single select | Backend, Frontend, Data, AI / Anomaly, Coordination, QA, Infrastructure, Release |
| Priority | Single select | P0 — core MVP/blocking; P1 — important/fallback; P2 — optional |
| Phase | Single select | 1 — Foundation; 2 — Parallel Build; 3 — Integration; 4 — Stabilization & Release; 5 — Submission |
| Target date | Date | Use the issue-to-date table below |
| Blocked by | Text | Issue references such as #5 and #7; keep in sync with issue descriptions |

## Views to create

### 1. Execution Board (default)
- Layout: Board; group by Status.
- Filter: repository is `salmahmed6/Harmonization-of-MODIS-and-VIIRS-Hot-Spots`, issues only.
- Sort each column by Priority, then Target date.

### 2. Workstream Backlog
- Layout: Table; group by Workstream.
- Show Title, Status, Priority, Phase, Target date, Assignees, Labels.

### 3. Delivery Roadmap
- Layout: Roadmap (or Table if unavailable); date field Target date; group by Phase.

### 4. Priority Triage
- Layout: Table; group by Priority; filter out Done; sort by Target date.

### 5. Blocked Work
- Layout: Table or Board; filter Status = Blocked.
- Show Title, Workstream, Blocked by, Target date.

## Phases and checkpoints

| Phase | Target window | Exit condition |
|---|---|---|
| 1 — Foundation | Oct 22–25, 2026 | Scope/region, data quality, cleaning rules, API contract v1.0, anomaly feasibility decision |
| 2 — Parallel Build | Oct 26–Nov 1 | Importer/database loaded, summaries independently checked, frontend mock UI, stub deployment tested |
| 3 — Integration | Nov 2–8 | Live map/calendar/comparison/methods flow validated; feature freeze Nov 6 |
| 4 — Stabilization & Release | Nov 9–13 | Code freeze Nov 10, production target Nov 11, fallback/rehearsal complete, MVP target Nov 13 |
| 5 — Submission | Nov 14–15 | Presentation/submission confirmed; fallback ready |

## Dependency and parallel-work plan

**Start first:** #1 scope, region, dates, checkpoints; #2 FIRMS access; #3 backend skeleton; #4 frontend skeleton. After scope is agreed, #2, #3 and #4 can progress in parallel.

**Definition gates:** #5 depends on #2 and inspects real sensor fields/coverage. #7 depends on #5 and defines cleaning/aggregation. #6 depends on #3 and #5 and freezes the API contract. #8 depends on #5 (and #7 when available) and decides whether anomaly analysis is defensible.

**Parallel build:**
- Backend: #9 → #13 → #14 → #15.
- Frontend mock work: #10 and #11 can proceed in parallel after #4 and #6; they do not wait for the database.
- AI/Anomaly: #12 is conditional on #8 and validated metrics; if coverage is insufficient, use percentiles or omit anomaly labels.
- Methods content: #19 can be drafted as data decisions become available.

**Integration and release:** #17 integrates live endpoints and must not wait for optional anomaly work. #18 depends on live data and validated comparison semantics. #16 and #20 are optional and must not block the core MVP. #21 validates end-to-end behavior and scientific language. #22 deployment and #23 fallback can proceed in parallel after a stable integration build. #24 prepares the demo/evidence pack; #25 is the final release gate.

If time runs short, cut optional anomaly labels first, then other optional enhancements. Protect area/date selection, map, calendar, fair MODIS/VIIRS comparison, and the methods/limitations page.

## Issue metadata for Project fields

| Issue | Workstream | Priority | Phase | Target |
|---|---|---|---|---|
| #1 | Coordination | P0 | 1 — Foundation | Oct 22 |
| #2 | Data | P0 | 1 — Foundation | Oct 23 |
| #3 | Backend | P0 | 1 — Foundation | Oct 23 |
| #4 | Frontend | P0 | 1 — Foundation | Oct 23 |
| #5 | Data | P0 | 1 — Foundation | Oct 24 |
| #6 | Backend | P0 | 1 — Foundation | Oct 25 |
| #7 | Data | P0 | 1 — Foundation | Oct 24 |
| #8 | AI / Anomaly | P0 | 1 — Foundation | Oct 24 |
| #9 | Backend | P0 | 2 — Parallel Build | Oct 27 |
| #10 | Frontend | P0 | 2 — Parallel Build | Oct 27 |
| #11 | Frontend | P0 | 2 — Parallel Build | Oct 27 |
| #12 | AI / Anomaly | P2 | 2 — Parallel Build | Oct 31 |
| #13 | Backend | P0 | 2 — Parallel Build | Oct 30 |
| #14 | Data | P0 | 2 — Parallel Build | Oct 31 |
| #15 | Backend | P0 | 3 — Integration | Nov 3 |
| #16 | Backend | P2 | 3 — Integration | Nov 3 |
| #17 | Frontend | P0 | 3 — Integration | Nov 3 |
| #18 | Frontend | P0 | 3 — Integration | Nov 5 |
| #19 | Frontend | P0 | 3 — Integration | Nov 5 |
| #20 | Frontend | P2 | 3 — Integration | Nov 5 |
| #21 | QA | P0 | 3 — Integration | Nov 8 |
| #22 | Infrastructure | P0 | 4 — Stabilization & Release | Nov 11 |
| #23 | Infrastructure | P1 | 4 — Stabilization & Release | Nov 10 |
| #24 | Coordination | P1 | 4 — Stabilization & Release | Nov 13 |
| #25 | Release | P0 | 5 — Submission | Nov 13 |

## Project checklist

- [ ] Add all open repository issues (#1–#25) as project items.
- [ ] Enable auto-add for future open issues from this repository, if available.
- [ ] Configure Workstream, Priority, Phase, Target date, and Blocked by.
- [ ] Create the five views above and populate metadata from the table.
- [ ] Keep every item unassigned.
- [ ] Mark waiting work Blocked rather than silently moving its date.
- [ ] Review on Oct 25, Nov 1, Nov 8, and Nov 12.

## Scientific guardrails

- Count hotspot detections, not individual fires.
- Never add MODIS and VIIRS counts together and call them a fire count.
- Only show anomaly highlights if coverage analysis and validation support them.
- An anomaly is unusual historical activity relative to comparable times of year, not prediction or early warning.
- Document data gaps, attribution, and limitations in the application and presentation.
