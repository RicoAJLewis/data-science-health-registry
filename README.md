# data-science-health-registry
Health Registry Data Cleaning &amp; Profiling  This repository contains a cleaned and validated dataset of healthcare facilities, complete with preprocessing scripts, profiling reports, and documentation. It is designed to support public health analytics, knowledge graph construction, and retrieval-augmented generation (RAG) applications.
# 🏥 Cleaned Health Registry Dataset

This dataset contains structured, cleaned, and validated information on healthcare facilities. It serves as a trusted foundation for analytics, visualization, and downstream applications such as knowledge graphs and retrieval-augmented generation (RAG).

# Link To My Loom Video
https://www.loom.com/share/a9e3e81639c14d56962b894d263d20dd
---

## ⚙️ How to Reproduce

To run the cleaning and profiling process:

1. Clone the repo:
   ```bash
   git clone https://github.com/your-username/health-registry-cleaning.git
   cd health-registry-cleaning

2. ## on windows terminal
   1.	python -m venv .venv
   2.	Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   3.	.venv\Scripts\activate
   4.	py -0 # if you have more than one version
   5.	py -3.11 -m venv .venv
   6.	.venv\Scripts\activate
   7.	python –version #to confirm the version
   8.	pip install -r requirements.txt

3. ## open the notebook On our IDE (mine was VS code)
   Navigate to notebooks/health_registry_eda_clean.ipynb.

   Go to Kernel > Restart & Run All.

   Confirm no errors appear in output.


## 📊 Dataset Overview

- **Total Records**: 569
- **Columns**: 11 (normalized and typed)
- **Format**: CSV (UTF-8 encoded)
- **Last Updated**: 04-06-2025

---

## 🧹 Cleaning Summary

| Field                  | Cleaning Actions                                                                 |
|------------------------|----------------------------------------------------------------------------------|
| `Facility Id`          | Regenerated using hash logic to ensure uniqueness                               |
| `Facility Name`        | Removed emojis, newlines, parentheticals; expanded abbreviations                |
| `Facility Type`        | Normalized known values (e.g., "CHC" → "Community Health Center")               |
| `Bed Capacity`         | Converted text like "ten beds" to integers; missing values replaced with `0`    |
| `Region`               | Fuzzy-matched to 11 Barbados parishes; corrected inverted or misspelled entries |
| `Licence Issue Date`   | Standardized to `DD-MM-YYYY`; swapped if after inspection date                  |
| `Inspection Date`      | Standardized to `DD-MM-YYYY`; handled multiple formats                          |
| `Gps Location`         | Parsed to separate `Latitude` and `Longitude` columns (float64)                |
| `Remarks`              | Normalized category; blanks or NaNs replaced with `-`                           |

---

## 🧾 Final Schema

| Column              | Type       |
|---------------------|------------|
| `Facility Id`       | `string`   |
| `Facility Name`     | `string`   |
| `Facility Type`     | `category` |
| `Bed Capacity`      | `int64`    |
| `Region`            | `category` |
| `Licence Issue Date`| `datetime` |
| `Inspection Date`   | `datetime` |
| `Latitude`          | `float64`  |
| `Longitude`         | `float64`  |
| `Remarks`           | `category` |

---

## 📂 Included Files

| File                             | Description                                       |
|----------------------------------|---------------------------------------------------|
| `cleaned_health_registry.csv`    | Fully cleaned and validated dataset              |
| `missing_data.csv`               | Rows with incomplete or critical missing data    |
| `health_registry_profile.html`   | Sweetviz profiling report                        |
| [Open Profile (Local)](file:///C:/Users/ricoa/Documents/AdminDataScienceIntern/health_registry_profile.html) | Local-only path for report |

---

## 🔍 Use Cases

This dataset supports a range of applications:

- 📊 Health infrastructure analytics and capacity studies  
- 🗺️ GIS mapping of healthcare access and distribution  
- 🧠 Knowledge Graph generation for structured search  
- 🤖 RAG-based chatbot grounding: _"Find hospitals in St. Michael"_  
- 📈 Public health dashboards and alerting systems

---








## Header💡 Assumptions & Decisions

| Area                         | Decision/Assumption                                                                 |
| ---------------------------- | ----------------------------------------------------------------------------------- |
| `Facility Id`                | Original IDs were non-unique, so new IDs were generated based on hash+index         |
| `Facility Type`              | Inferred missing or incorrect types using facility name keywords                    |
| `Region`                     | Fuzzy-matched malformed text against Barbados' 11 parishes                          |
| `Licence & Inspection Dates` | Swapped dates if inspection occurred before license issue (which is invalid)        |
| `Bed Capacity`               | Converted spelled-out numbers and blanks to integer (defaulted blanks to 0)         |
| `GPS Coordinates`            | Normalized to `latitude, longitude` and dropped clearly invalid entries             |
| Missing data                 | All rows with missing critical fields were moved to `missing_data.csv` and excluded |


You can then **add a small `requirements.txt` file** that includes:

txt
pandas
numpy
rapidfuzz
matplotlib
jupyter
pandas-profiling



## 🧠 Knowledge Graph & RAG Context

Each row can serve as a factual triple source. For example:

Facility: "Clark-Cameron Hospital"
Predicate: "is located in"
Object: "St. Peter"
Or RAG queries like:

> _“Which polyclinics were inspected after 2020 in St. James?”_

Can be powered by this dataset directly.

---

## 🧾 License & Notes

- Intended for public health and data science education use.
- Ensure downstream use abides by local data regulations.
