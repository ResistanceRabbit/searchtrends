🧰 Google Trends Workbook Generator
Open Project — Looking for feedback, collaborators, or contributors
📌 Summary

This project aims to build a small web-based tool that allows a user to plan and automatically generate Excel workbooks from Google Trends data. Each workbook will contain multiple sheets (one per selected time range) and multiple regions (one column per region).

The goal is to let a user configure the query in the browser, then produce a structured Excel report without manually repeating the same Google Trends searches.

🎯 Core Use Case

A user wants to compare how often a term (e.g., Charlie Kirk, Project 2025, Ukraine war, J6 pardons) is searched across multiple regions and time windows.

Example:

Search term: “Charlie Kirk”

Time ranges: 1 hour, 1 day, 30 days

Regions: US-DC, Palm Beach, FL, Israel, Philadelphia, Chicago

Expected output:

A workbook (output.xlsx)

Sheet: 1-hour → columns: each region’s trend series

Sheet: 1-day → same structure

Sheet: 30-day → same structure

Optional metadata sheet (search term, run time, region codes)

🏗️ Project Architecture (Proposed)
1. Browser UI (Front-End)

The current UI already supports selecting:

A single search term

Multiple time ranges

Multiple regions

Front-end responsibility:

Build a simple JSON configuration object:

{
  "searchTerm": "Charlie Kirk",
  "timeRanges": ["1h", "1d", "30d"],
  "regions": [
    {"code": "US-DC", "label": "Washington, D.C. Metro"},
    {"code": "IL-CHI", "label": "Chicago, IL"}
  ]
}


Allow the user to download this plan JSON or send it to an API.

✔️ The front-end is ~90% complete. Needs a small JS function to generate plan.json.

2. Backend Logic (Google Trends Fetcher)

Preferred implementation language: Python, using:

pytrends or an equivalent Trends library

pandas for data handling

openpyxl or xlsxwriter for workbook generation

Backend responsibilities:

Load plan.json

For each time range:

For each region:

Fetch “interest over time”

Build workbook:

One sheet per time range

One column per region

Return file or save locally

3. Deployment Strategy

There are two viable workflows:

Option A — Semi-Automated (Simplest)

Front-end generates plan.json

User runs:

python run_trends_plan.py plan.json


Script outputs output.xlsx

Option B — Fully Automated Web App

Front-end POSTs plan to /generate

Backend runs workflow, returns Excel file to user

🧪 Technical Challenges (Where Help Is Welcome)
✔️ 1. Handling Google Trends throttling

Pytrends is unofficial; needs retry/backoff logic.

✔️ 2. Validating region codes

Google region codes vary (US states vs. metro codes vs. countries).

✔️ 3. Sheet layout design

Consistent formatting across 1h/1d/30d time ranges.

✔️ 4. Deployment & hosting

Small Flask/FastAPI server is enough, but deployment is open-ended.

📦 Deliverables (MVP)

plan.json schema

run_trends_plan.py script (local mode MVP)

Excel builder with:

≥3 time ranges

≥3 regions

Automatic sheet generation

Clean column layout

🧑‍💻 Looking For:

Comments on the architecture

Suggestions on the region code system

Help writing/optimizing the data-fetch loop

A contributor who wants to build the backend API

Anyone who wants to take this on as a standalone open-source tool

📎 Contact / Links

steven@clearruleoflaw.org
@fraudfighter.79 on Signal


# searchtrends
Search term history compiler from Google Trends into Spreadsheet
