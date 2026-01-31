# Production Intelligence Analysis — Vale Malaysia

Production-grade operational analytics for Vale Malaysia’s Import, Export & Blending operations, converting 1 month of AVEVA PI historical data into actionable production, energy, and reliability insights.

---

## Table of contents
- [Overview](#overview)
- [Business objectives](#business-objectives)
- [Data source & format](#data-source--format)
- [Analysis scope](#analysis-scope)
- [Key outputs & deliverables](#key-outputs--deliverables)
- [Examples of KPIs & visualizations](#examples-of-kpis--visualizations)
- [Tools & environment](#tools--environment)
- [Quick start (Colab / Local)](#quick-start-colab--local)
- [Integration & operationalization](#integration--operationalization)
- [Confidentiality & data handling](#confidentiality--data-handling)
- [Project value & scalability](#project-value--scalability)
- [Intended audience](#intended-audience)
- [Contributing & contact](#contributing--contact)
- [Disclaimer & license](#disclaimer--license)

---

## Overview
This project analyzes one month of AVEVA PI System CSV exports from Vale Malaysia’s import, export and blending processes (including conveyor motor current). The goal is to turn raw operational signals into reliable production, energy and reliability insights that support daily operations, maintenance planning, and management decisions.

This is a production-grade analytics effort (designed to integrate with dashboards and operational systems), not an academic exercise or demo.

## Business objectives
- Stabilize production throughput and improve utilization
- Identify and quantify downtime and idle running
- Detect energy waste from motors running without load
- Surface early signs of mechanical or process inefficiencies
- Enable data-driven decisions using existing PI data (no new sensors)

## Data source & format
- Source: AVEVA PI System CSV exports (1 month)
- Typical tags:
  - Import / Export / Blending throughput (TPH)
  - Conveyor motor current (A)
  - Belt speed and runtime indicators
  - Timestamps at operational sampling intervals
- Confidential note: Raw PI data is not included in this repository.
- Suggested CSV schema (adapt as needed):
  - timestamp (ISO 8601)
  - tag_name (optional; wide format preferred with named columns per tag)
  - throughput_tph
  - motor_current_a
  - belt_speed_m_s
  - runtime_flag (0/1)
- Provide a README/manifest for any raw CSVs describing tag mapping and PI point names.

## Analysis scope
1. Data validation
   - Timestamp consistency, sampling intervals
   - Missing values, flatlines, sensor dropouts
   - Distinguish between shutdown, idle, and running
2. Operational state classification
   - Per-timestamp classification: Running, Idle (motor on, low/no tonnage), Shutdown
3. Production performance
   - Hourly/daily throughput, import vs export balance
   - Blending stability, utilization, downtime, idle durations
4. Motor current & energy analysis
   - Correlate motor current with throughput
   - Detect high-current / low-tonnage events (no-load running)
   - Estimate energy waste
5. Early warning & diagnostics
   - Rolling statistics, deviation detection
   - Explainable models to estimate expected throughput
   - Flags for abnormal operating behavior

## Key outputs & deliverables
- Quantified production losses (time and tonnage)
- Identified energy waste periods and estimated energy loss
- Patterns of operational inefficiency and high-risk events
- Early-warning indicators for maintenance and operations
- Artifacts delivered:
  - Jupyter/Colab notebooks with analysis pipelines
  - Processed CSVs and summary tables
  - Visualization assets (plots, PNGs)
  - Dashboard-ready metrics (Power BI / PI Vision / KPI exports)
  - Short executive slide deck (optional)

## Examples of KPIs & visualizations
- Daily throughput vs plan (TPH)
- Production utilization (%)
- Idle-running hours and tonnage lost
- Energy efficiency indicators (kWh/tonne or proxy from motor current)
- Timelines of high-current/low-tonnage events with annotations
- Rolling deviation charts and anomaly flags

## Tools & environment
- Python 3.8+
- Key libraries: pandas, numpy, matplotlib / seaborn, scikit-learn
- Optional: statsmodels, xgboost (if advancing models)
- Execution targets:
  - Google Colab (lightweight, shareable)
  - Local Python environment or company compute environment

## Quick start (Colab / Local)
1. Open the notebook in Google Colab (recommended for transparency and reproducibility).
2. Install dependencies:
   - pip install -r requirements.txt
3. Place CSV exports into the data/ directory (or mount Google Drive in Colab).
4. Edit configuration (data/tag mapping) in config.yaml or notebook header.
5. Run the pipeline cells in order:
   - data validation -> preprocessing -> state classification -> KPI aggregation -> diagnostics & visualizations
6. Export summary tables for dashboard ingestion (CSV/JSON).

(If you want, I can generate a ready-to-run Colab notebook and a `requirements.txt`.)

## Integration & operationalization
- Outputs structured for ingestion into:
  - Power BI dashboards
  - PI Vision (summary tags / snapshots)
  - KPI systems and maintenance platforms
- Recommended productionization steps:
  - Schedule periodic runs (e.g., daily/shift) in a controlled compute environment
  - Push summary metrics back into PI or a metrics store for dashboarding
  - Add alerting for abnormal events (email / MES / maintenance ticketing)

## Confidentiality & data handling
- Raw PI data must remain on-site or within approved secure storage.
- This repo omits raw PI exports by design. Use local/secure data mounts or a secure pipeline to process PI CSVs.
- Include a data manifest that maps PI point names to analysis tags; treat that manifest as sensitive if it contains site-specific tagging.

## Project value & scalability
- No new sensors required; uses existing PI data
- Low-cost, high-impact: quick wins in utilization, energy and reliability
- Scales to:
  - Predictive maintenance / AI Technical Inspector
  - Energy optimization and ESG reporting
  - Multi-site rollouts using the same pipelines and configuration templates

## Intended audience
- Production managers
- Operations engineers
- Reliability & maintenance teams
- Digital transformation & analytics teams
- Executive management

## Contributing & contact
- To contribute: open issues or PRs with proposed changes to notebooks, config templates, or docs.
- For site-specific onboarding, reach out to the project owner or analytics lead with details on PI tag mappings and secure data access procedures.

## Disclaimer & license
- This project is for analytical and decision-support purposes. Operational actions should be validated by site engineers and follow standard operating procedures.
- Add appropriate license file (e.g., MIT) depending on your organization’s policy.

---

## Author
Industrial Automation & Data Analytics Engineer — specializing in mining operations, production intelligence, and reliability analytics.
