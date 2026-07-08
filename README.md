# Bill Swift — SaaS Lead Generation & Revenue Intelligence Pipeline

An end-to-end automated pipeline that takes a webinar registrant from form submission to a scored lead, CRM contact, ML-predicted contract value, and automated email sequence — with zero manual steps.

Built as a full-stack portfolio project simulating a real-world B2B SaaS sales operations workflow for a fictional usage-based billing company.

---

## What It Does

A prospect fills out a webinar registration form. From that single action, the system automatically:

1. **Cleans the data** — title-cases names and standardises input regardless of how it was typed
2. **Scores the lead** — a vectorized 6-factor model rates every lead 0–100 and assigns a tier (Hot / Warm / Cold)
3. **Logs to Excel** — appends the record to a live workbook while preserving the table format for dashboards
4. **Syncs to HubSpot CRM** — creates and associates a Contact and Company, handling duplicates gracefully
5. **Alerts on priority leads** — the same score threshold that flags a lead as Hot in HubSpot also fires a Zapier webhook, posting an instant Slack alert and logging the lead to a dedicated priority-leads Excel file, independent of the general log
6. **Predicts revenue** — a machine learning model estimates the contract value for every new lead
7. **Triggers automation** — HubSpot workflows send confirmation and nurture emails, move the lead through the lifecycle, and create a deal when a meeting is booked
8. **Feeds analytics** — live PivotCharts show leadership which industries and tiers to prioritise

---

## Tech Stack

| Layer | Technologies |
|---|---|
| Frontend | HTML5, CSS3 (glassmorphism UI, micro-interactions) |
| Backend | Python, Flask, Jupyter Notebook |
| Machine Learning | scikit-learn (Random Forest Regressor), pandas, NumPy |
| Data & Reporting | openpyxl, Microsoft Excel (PivotTables, PivotCharts) |
| CRM & Automation | HubSpot CRM API, HubSpot Workflows |
| Alerting & Integration | Zapier (Webhooks + Slack), Slack API |

---

## Pipeline Overview

![Project Pipeline](project_flowchart.png)

---

## Key Features

**Vectorized lead scoring**
Six weighted signals (transaction volume, revenue challenge, billing solution, company size, attribution source, email type) scored in a single NumPy operation — server-side, so scores can't be tampered with from the browser.

**Machine learning revenue prediction**
A Random Forest Regressor trained on 200 historical records predicts contract value for each new lead using one-hot encoded features. Predictions are written directly into the live Excel sheet without overwriting existing values.

**Resilient HubSpot integration**
Contacts and Companies are created via the CRM API with automatic 409-conflict handling — existing records are found and updated instead of failing on duplicates.

**Excel table preservation**
Python rewrites the Excel Table definition on every save, so PivotCharts stay connected and the table range expands automatically as new leads arrive.

**Full lifecycle automation**
Four HubSpot workflows drive the lead journey: registration confirmation, MQL upgrade on engagement, SQL/Opportunity and deal creation on meeting booking, and an instant internal alert for high-scoring leads.

**Priority Lead Alert (Zapier + Slack)**
Leads crossing the same priority threshold as HubSpot's Hot tier trigger a dedicated Zapier webhook, called directly from the Flask backend. This posts a real-time Slack alert — company, score, transaction volume, and primary revenue challenge — and simultaneously logs the lead to a separate priority-leads Excel file, giving the team visibility beyond the CRM itself.

---

## CFO-Ready Analytics

Four PivotCharts turn raw registrations into business intelligence:

- **Where to Invest** — predicted revenue by industry
- **Pipeline Urgency** — predicted revenue by lead tier
- **Lead Distribution** — lead volume by tier
- **Market Reach** — lead volume by industry

---

## Repository Contents

| File | Description |
|------|-------------|
| `billswift-webinar-registration.html` | The registration webpage (frontend) |
| `billswift_registration_server.ipynb` | Flask backend: cleaning, scoring, ML, Excel, HubSpot, Zapier alert |
| `billswift_flowchart.png` | Pipeline architecture diagram (including Priority Lead branch) |
| `Portfolio Project .pdf` | Full visual walkthrough with screenshots |
| `billswift_priority_leads.xlsx` | Auto-generated log of leads that crossed the priority threshold (created on first Priority Lead) |

---

## How to Run

1. Place the notebook and `billswift_testing_dataset.xlsx` in the same folder
2. Open `billswift_registration_server.ipynb` in Jupyter
3. Add your HubSpot Private App token in Step 2
4. Add your Zapier webhook URL in Step 3 (optional — the Priority Lead alert is skipped gracefully if not configured)
5. Run all cells — the Flask server starts and the ML model trains automatically
6. Open the HTML form in a browser and submit a registration
7. Watch the lead flow into Excel and HubSpot in real time — check Slack for an instant alert if the lead scores above the priority threshold

---

## About

SaaS lead generation & revenue intelligence pipeline — Python, Flask, ML, HubSpot CRM, Zapier, Slack
