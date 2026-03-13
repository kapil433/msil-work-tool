# MSIL Work Tool — Pillar 3A

> **Personal OS**: Blog → Automation → **Projects** → Research

Production-grade analytics dashboard for automotive industry work. Built on FastAPI + Streamlit, powered by Vahan registration data.

## Modules

| Module | Description | Status |
|---|---|---|
| **Vahan Dashboard** | Registration trends by OEM, segment, state, fuel type | In Progress |
| **CAFE Norms Tracker** | Fleet average CO2 vs regulatory targets, OEM-wise | Planned |
| **TCO Calculator** | Total Cost of Ownership comparison across fuel types | Exists (TCO-Calculator repo) |
| **OEM Market Share** | State-wise and segment-wise market share over time | Planned |
| **EV Transition Monitor** | EV penetration by state, charging infra correlation | Planned |

## Tech Stack

```
Backend:  FastAPI + PostgreSQL
Frontend: Streamlit (dashboard) / Dash (advanced charts)
Data:     Vahan registration extracts (monthly)
Auth:     JWT-based (even for personal use — production-ready)
Deploy:   AWS EC2 or Railway.app
CI/CD:    GitHub Actions → test → lint → deploy on push to main
```

## Project Structure

```
msil-work-tool/
├── api/
│   ├── main.py              ← FastAPI app entry point
│   ├── routers/
│   │   ├── vahan.py         ← Registration data endpoints
│   │   ├── cafe.py          ← CAFE norms endpoints
│   │   └── tco.py           ← TCO calculator endpoints
│   └── models/
│       ├── vahan.py         ← Pydantic models
│       └── db.py            ← SQLAlchemy models
├── dashboard/
│   ├── app.py               ← Streamlit main app
│   ├── pages/
│   │   ├── 1_Vahan.py
│   │   ├── 2_CAFE.py
│   │   └── 3_TCO.py
│   └── components/
├── data/
│   ├── ingestion/           ← ETL scripts for Vahan data
│   └── migrations/          ← Alembic DB migrations
├── tests/
├── .github/
│   └── workflows/
│       └── ci.yml           ← GitHub Actions CI/CD
├── pyproject.toml           ← Pinned dependencies
├── Dockerfile
└── README.md
```

## Data Flow

```
Vahan Portal (manual extract)
    ↓
data/ingestion/load_vahan.py  (ETL: CSV → PostgreSQL)
    ↓
PostgreSQL (structured, versioned)
    ↓
FastAPI (data layer, computation)
    ↓
Streamlit Dashboard (visualization)
```

## Production Standards

- [ ] `pyproject.toml` with pinned deps
- [ ] PostgreSQL (not CSV files) as data store
- [ ] Alembic migrations for schema versioning
- [ ] GitHub Actions CI: pytest + ruff lint on every push
- [ ] JWT auth (even for personal access)
- [ ] Dockerfile for containerized deployment
- [ ] Comprehensive test coverage

## Part of the Four-Pillar System

```
Pillar 1: personal-blog
Pillar 2: social-automation
Pillar 3A: msil-work-tool (this repo)
Pillar 3B: commercialize-analytics
Pillar 3C: complexity-lab
Pillar 4:  research-platform
```
