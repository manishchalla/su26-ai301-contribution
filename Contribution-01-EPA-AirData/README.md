# AI301 Contribution README

**Student:** Manish Challa  
**GitHub:** @manishchalla  
**Course:** AI301 — AI Open Source Capstone, Summer 2026  
**Status:** Contribution #1 Merged

---

# Contribution #1

**Repository:** https://github.com/almanac-data/environment-almanac

**Issue:** #1 – Dataset: EPA AirData (Outdoor Air Quality)

**Pull Request:** Add EPA AirData catalog entry

**Status:** ✅ Merged

---

# Phase I — Issue Selection

## Why I Chose This Issue

I selected this issue because it was a well-scoped beginner-friendly open source contribution that required understanding an existing project instead of simply writing code. The issue involved adding a new public environmental dataset into the project's catalog while following the repository schema, contribution guidelines, validation process, and CI workflow.

This contribution aligns well with my background in Data Engineering because it involves metadata management, schema validation, public datasets, reproducibility, and GitHub collaboration.

---

## Issue Summary

The project maintains a catalog of publicly available environmental datasets.

This issue requested adding the **EPA AirData** dataset into the catalog by creating a new YAML catalog entry.

The required work included:

- Creating a new YAML file
- Filling every required metadata field
- Verifying the official EPA source
- Running validation
- Rebuilding the generated catalog
- Opening a Pull Request

---

## Repository Links

Repository

https://github.com/almanac-data/environment-almanac

Issue

https://github.com/almanac-data/environment-almanac/issues/1

Fork

https://github.com/manishchalla/environment-almanac

---

# Phase II — Understanding the Issue

## Problem Description

The repository catalogs public datasets instead of hosting them.

Each dataset is represented by one YAML file under

```
catalog/
```

The issue requested creating

```
catalog/epa-airdata.yaml
```

following the existing schema.

---

## Expected Result

After completing the issue,

- EPA AirData should appear in the catalog
- Validation should succeed
- catalog.json should be regenerated
- CI should pass
- Pull Request should be mergeable

---

## Existing State

Before my contribution,

EPA AirData did not exist inside the catalog.

---

## Files Affected

```
catalog/epa-airdata.yaml
catalog.json
```

---

# Environment Setup

Operating System

- Windows 11
- WSL2 (Ubuntu)

Repository Setup

```bash
git clone https://github.com/manishchalla/environment-almanac.git

cd environment-almanac

git checkout -b add-epa-airdata
```

---

# Understanding the Repository

Before making any changes I reviewed:

```
CONTRIBUTING.md
```

to understand the contribution workflow.

I also reviewed

```
schema/catalog-entry.schema.json
```

to understand

- required fields
- field descriptions
- validation rules

This prevented guessing values and ensured every field followed the repository schema.

---

# Solution Planning

Instead of creating a YAML file from scratch,

I copied an existing EPA catalog entry

```
catalog/epa-aqs.yaml
```

because it followed the same schema and represented a similar air-quality dataset.

I then replaced every dataset-specific field with verified EPA AirData information.

Nothing was copied without verification.

Every field was checked against

https://www.epa.gov/outdoor-air-quality-data

---

# Implementation

Created

```
catalog/epa-airdata.yaml
```

Final metadata

```yaml
id: epa-airdata
title: EPA AirData
description: EPA AirData provides access to recent and historical outdoor air quality data collected at monitoring stations across the United States, including downloadable datasets, AQI reports, and monitor information.
publisher: U.S. Environmental Protection Agency (EPA)

topics:
- air-quality
- pollutants
- monitoring
- aqi

source:
  canonical_url: https://www.epa.gov/outdoor-air-quality-data
  predecessor_url: null
  doi: null

access:
  method:
  - web
  - api
  - bulk
  auth_required: false
  auth_note: API requires a free key obtained by email registration; bulk pre-generated files are publicly available.
  rate_limit: null

format:
- csv
- json

coverage:
  spatial: United States
  temporal: 1980-present
  cadence: daily

license: public-domain (US Gov work)

attribution: U.S. Environmental Protection Agency, AirData

archive:
  wayback_url: null
  cloud_mirror: null
  mirror: null

status: live

last_checked: '2026-06-30'

checksum: null

notes: null
```

---

# Verification Process

Every field was verified before modification.

Examples

### id

Verified using repository rules.

The filename

```
catalog/epa-airdata.yaml
```

must match

```
id: epa-airdata
```

---

### title

Verified from the official EPA page.

Official page heading

```
AirData: Air Quality Data Collected at Outdoor Monitors Across the US
```

Dataset name

```
EPA AirData
```

---

### description

Written from the official EPA documentation instead of copying another dataset.

---

### source

Verified against

https://www.epa.gov/outdoor-air-quality-data

---

### coverage

Verified by downloading the historical data.

The downloaded dataset contained records beginning in

```
1980
```

therefore

```
temporal: 1980-present
```

was retained.

---

### access

Verified using EPA API documentation.

Confirmed

- Web access
- API access
- Bulk downloads

The repository convention used

```
auth_required: false
```

for free API registration.

---

# Validation

Schema Validation

```bash
python3 scripts/validate.py
```

Output

```
OK — 8 entries valid
```

---

Catalog Generation

```bash
python3 scripts/build_index.py
```

Output

```
wrote catalog.json — 8 entries ({'live': 8})
```

---

Test Suite

```bash
python3 -m pytest
```

Output

```
7 passed
```

---

# Git Workflow

Created feature branch

```bash
git checkout -b add-epa-airdata
```

Staged files

```bash
git add catalog/epa-airdata.yaml catalog.json
```

Commit

```bash
git commit -m "Add EPA AirData catalog entry"
```

Push

```bash
git push -u origin add-epa-airdata
```

---

# Pull Request

PR Title

```
Add EPA AirData catalog entry
```

PR Description

```
Summary

Adds a new catalog entry for EPA AirData.

Changes

- Added catalog/epa-airdata.yaml
- Verified the canonical source URL
- Added dataset metadata following the catalog schema
- Regenerated catalog.json

Validation

- python3 scripts/validate.py
- python3 scripts/build_index.py
- pytest

Closes #1
```

---

# Maintainer Review

The maintainer reviewed the contribution and approved it.

Review comment

> Approved — clean first catalog contribution. EPA AirData URL verified, schema-valid, distinct from the existing AirNow entry (AirData = historical/bulk vs AirNow = real-time AQI), and catalog.json was correctly regenerated. CI green.

The Pull Request was merged into the main branch.

---

# Outcome

Successfully merged into

```
almanac-data/environment-almanac
```

Contribution completed successfully.

---

# Technical Skills Demonstrated

- Reading project documentation
- Understanding JSON Schema
- YAML authoring
- Metadata curation
- Source verification
- Git workflow
- Branch management
- Pull Requests
- Repository validation
- Running automated tests
- Open source collaboration

---

# Lessons Learned

This contribution taught me that successful open source contributions require understanding the repository conventions before making changes.

Rather than assuming field values, I learned to verify each metadata field using the project's schema, official EPA documentation, and existing repository conventions.

Running validation scripts, rebuilding generated artifacts, and executing the project's test suite before opening a Pull Request helped ensure the contribution was accepted without requiring any revisions.
