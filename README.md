# PharmaGenDSS

**A Mini Clinical Genomics Decision Support System for Variant-Informed Prescribing**

Bioinfo 203 — Special Project · Sem 2, AY 2025–2026
University of the Philippines Diliman

**Author:** John Marquel P. Revilla — MEng Industrial Engineering (Analytics & Systems Engineering)

---

## Overview

Adverse drug reactions account for roughly 6.5% of adult hospital admissions, and a
large share of that variability is inherited — people metabolize, transport, and
react to drugs differently because of their genes. The science is mature: CPIC and
DPWG between them cover more than a hundred clinically actionable gene–drug pairs.
The gap is at the bedside. The underlying resources (PharmGKB, DrugBank, CPIC, DPWG)
are *descriptive* — they tell a clinician what is known — but none is *prescriptive*
given a specific patient's genetic profile, and none is prescription-aware out of the box.

**PharmaGenDSS** is a proposal and full software-engineering design for a small,
single-tenant, web-accessible decision support system that pulls those four resources
into one citation-backed query layer. A clinician can ask, in one query, *"given this
patient's genetic profile, what should I prescribe?"* and get back a guideline-backed,
citation-traceable answer in under two seconds.

> ⚠️ **Decision support — not diagnostic.** The system consumes a patient genotype; it
> never generates one. Where no genotype is on file it degrades gracefully to a
> *"testing recommended"* advisory and never silently defaults to a wild-type call.

This repository is a **systems-engineering proposal** following Sommerville's (10e)
frameworks. It contains the design artifacts and deliverables — not a running
implementation.

## Scope at a glance

| | |
|---|---|
| **Intended users** | Prescribing clinician · Clinical pharmacist · Bioinformatics curator · PGx researcher |
| **Driving queries** | Variant-driven · Drug-driven · Gene-driven |
| **Data sources** | PharmGKB · DrugBank · CPIC · DPWG |
| **Methodology** | Agile, with a DevOps complement |
| **Architecture** | Layered + Repository pattern, with a pipe-and-filter sub-architecture for the curator data refresh |
| **Requirements** | 12 functional requirements · 3 categories of non-functional requirements |
| **Models** | Contextual · Structural · Behavioral (use case, sequence, state, activity) |
| **Deployment** | Docker Compose, single-tenant |
| **Licensing** | Role-based redaction layer honoring PharmGKB CC-BY-SA share-alike and DrugBank academic-license boundaries |

## Proposed technology stack

| Layer | Choice |
|-------|--------|
| Frontend | React + TypeScript + TanStack Query |
| API | FastAPI (Python 3.12), auto-generated OpenAPI docs |
| ORM | SQLAlchemy 2 + Alembic |
| Database | PostgreSQL 16 (JSONB for flexible annotation fields) |
| Auth | OAuth2 password flow → JWT, bcrypt |
| ETL | Python (pandas, lxml), scheduled via GitHub Actions / cron |
| Containers | Docker Compose (web · api · db) |
| CI | GitHub Actions (pytest, ruff, mypy) |

## Repository contents

### Deliverables

| File | Description |
|------|-------------|
| `[Bioinfo203] Final Project-Written Report_Revilla.pdf` | Final written report (ACM proceedings format) |
| `PharmaGenDSS_Proposal Deck.pdf` | Oral presentation slide deck |
| `[Bioinfo203] Special Project_Oral Report_Revilla.mp4` | 20-minute oral report recording |

## Report outline

1. Project Background
2. Requirements Engineering and System Model
3. System Architecture and Design
4. Implementation Details
5. References

## References

The data sources and clinical resources underlying this proposal:

1. PharmGKB — https://www.pharmgkb.org
2. DrugBank — https://go.drugbank.com
3. CPIC (Clinical Pharmacogenetics Implementation Consortium) — https://cpicpgx.org
4. DPWG (Dutch Pharmacogenetics Working Group) — https://www.knmp.nl
5. HL7 FHIR Genomics Implementation Guide — https://hl7.org/fhir/uv/genomics-reporting

## License

The project design and source code are proposed for release under the **MIT License**.
Derived PharmGKB data inherits **CC-BY-SA**; DrugBank fields are gated by user role to
comply with its academic license.

---

*Academic coursework. PharmaGenDSS is a design proposal — it is decision support, not a
diagnostic tool, and is not intended for clinical use.*
