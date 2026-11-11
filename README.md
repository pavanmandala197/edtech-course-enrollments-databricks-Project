# 🚀 Online Learning Analytics Platform | Databricks Lakehouse & Lakeflow Pipelines

An end-to-end **Data Engineering and Analytics project** built using **Databricks, Lakeflow Spark Declarative Pipelines, Databricks SQL, and AI/BI Dashboards**.

This project demonstrates how raw and inconsistent EdTech enrollment data can be transformed into clean, reliable, and business-ready insights using the **Medallion Architecture (Bronze, Silver, and Gold)**.

The solution implements an automated data pipeline with data quality validation, duplicate handling, transformation, business aggregations, reconciliation checks, and interactive executive dashboards.

---

## 📌 Project Overview

The Online Learning Analytics Platform analyzes synthetic course enrollment data to help business stakeholders understand learner engagement, course performance, revenue trends, and acquisition channel effectiveness.

**Key Objectives:**
- Build an end-to-end Lakehouse data engineering pipeline.
- Implement Bronze, Silver, and Gold data layers.
- Clean, standardize, and validate raw enrollment data.
- Implement data quality expectations and rejected-record handling.
- Create business-level aggregations using Databricks SQL.
- Perform automated data reconciliation and auditing.
- Develop executive dashboards for business reporting.

---

## 🏛️ Architecture & Data Flow

The project follows the **Medallion Architecture**, where data passes through three progressive layers of refinement.

```text
       RAW CSV DATA
   (Unity Catalog Volume)
              |
              ▼
      BRONZE LAYER
   Raw Data Ingestion
   Metadata & Lineage
              |
              ▼
      SILVER LAYER
   Data Cleaning & Validation
       /           \
      ▼             ▼
 Clean Records   Rejected Records
      |             |
      ▼             ▼
      GOLD LAYER
 Business Aggregations
 Revenue & Performance
      |
      ▼
 DATABRICKS AI/BI DASHBOARDS
 Executive Reporting & Insights
```

### Architecture Layers

| Layer | Purpose |
|---|---|
| Bronze | Raw data ingestion and metadata tracking |
| Silver | Data cleaning, standardization, and quality validation |
| Silver Rejected | Stores records that fail data quality rules |
| Gold | Business aggregations and analytical summaries |
| Dashboard | Executive reporting and business insights |

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Data Engineering | Databricks Lakeflow Spark Declarative Pipelines |
| Data Processing | Databricks SQL |
| Storage | Delta Lake |
| Data Governance | Unity Catalog |
| Data Ingestion | Unity Catalog Volumes |
| Architecture | Medallion Architecture |
| Data Quality | Declarative Expectations |
| Data Visualization | Databricks AI/BI Dashboards |
| Programming Language | SQL |

---

## 📂 Repository Structure

```text
Online-Learning-Analytics-Platform/
│
├── README.md
│
├── pipeline_sql_code.sql
│
├── datasets/
│   └── course_enrollments_raw.csv
│
└── screenshots/
    ├── pipeline_graph.png
    ├── reconciliation_check.png
    └── dashboard_overview.png
```

---

## ⚙️ Pipeline Implementation

### 1. Bronze Layer – Raw Data Ingestion

**Table:** `bronze_course_enrollments`

The Bronze layer ingests raw CSV enrollment records from a Unity Catalog Volume into a streaming table.

**Key Operations:**
- Reads raw CSV files without modifying original business values.
- Captures source file information using `source_file`.
- Adds ingestion timestamps using `loaded_at`.
- Maintains data lineage and traceability.
- Preserves raw data for downstream processing.

**Objective:** Maintain a reliable raw data foundation for further transformations.

### 2. Silver Layer – Data Cleaning & Quality Validation

The Silver layer transforms raw data into clean and standardized records.

**Key Transformations:**

**Data Deduplication**
- Identifies and removes duplicate enrollment records.
- Uses `SELECT DISTINCT` and enrollment-level deduplication logic.

**Text Standardization**
- Uses `TRIM()` to remove unwanted whitespace.
- Uses `INITCAP()` to standardize categorical values.
- Uses `LOWER()` to normalize email addresses.

**Missing Value Handling**
- Uses `COALESCE()` to replace missing city and category values with `'Unknown'`.
- Calculates missing `price_paid` values using `list_price - discount_amount`.

**Data Quality Validation**
- Validates progress percentages between 0 and 100.
- Identifies negative prices and invalid business metrics.
- Uses declarative expectations to enforce data quality rules.
- Separates invalid records into `silver_enrollments_rejected`.

**Learner Progress Categorization**

Uses SQL `CASE WHEN` statements to classify learners into:

- Completed
- In Progress
- Not Started

**Objective:** Ensure downstream analytics are based on consistent and validated data.

### 3. Gold Layer – Business Aggregations

The Gold layer contains business-ready analytical tables designed for reporting and decision-making.

| Gold Table | Business Purpose |
|---|---|
| `gold_monthly_enrollments` | Monthly enrollment trends, revenue, active learners, and completion rates |
| `gold_category_summary` | Course category performance and revenue comparisons |
| `gold_course_summary` | Individual course performance, ratings, and hours watched |
| `gold_channel_summary` | Acquisition channel analysis and performance |
| `gold_data_quality` | Data quality metrics and reconciliation auditing |

**Objective:** Convert cleaned enrollment data into meaningful business insights.

---

## 📊 Executive Dashboard

Developed using **Databricks AI/BI Dashboards**, the reporting solution contains three major analytical pages.

### 1. Overview Dashboard

Provides a high-level summary of platform performance.

**Key Performance Indicators (KPIs):**

| Metric | Result |
|---|---:|
| Total Enrollments | 1,241 |
| Total Revenue | ₹27.21 L |
| Course Completions | 349 |
| Hours Watched | 16,856 |

**Visualizations:**
- Total enrollment KPI
- Revenue KPI
- Course completion KPI
- Hours watched KPI
- Monthly revenue trends
- Course category distribution

### 2. Courses & Channels Dashboard

Analyzes course performance and learner acquisition.

**Key Insights:**
- Top-performing courses.
- Course-wise revenue comparison.
- Course completion rates.
- Acquisition channel performance.
- Website, Mobile App, Referral, and Social Media analysis.

### 3. Data Quality & Governance Dashboard

Provides transparency into data cleaning and pipeline reliability.

**Key Insights:**
- Raw versus cleaned records.
- Rejected records analysis.
- Duplicate record tracking.
- Email normalization impact.
- Automated row reconciliation.
- Data quality monitoring.

---

## 🔍 Key Business Insights

### 1. Email Normalization Impact

Standardizing email addresses using `LOWER()` and `TRIM()` helped identify duplicate user identities caused by inconsistent capitalization and trailing spaces.

This analysis identified 61 potentially double-counted user records, improving the reliability of unique learner metrics.

### 2. Data Quality Management

Invalid records were identified and separated from clean records instead of allowing poor-quality data to affect business reporting.

### 3. Revenue & Course Performance

Gold-layer aggregations provide visibility into monthly revenue, course performance, category-level comparisons, and acquisition channel effectiveness.

### 4. Automated Data Reconciliation

Implemented reconciliation logic to validate the relationship between ingested and processed records.

**Reconciliation Formula:**

```text
Bronze Records =
Clean Records
+ Rejected Records
+ Duplicate Records Removed
```

The reconciliation check achieved 100% verification for the implemented record accounting logic.

---

## 🚀 Key Skills Demonstrated

Through this project, I gained practical experience in:

- End-to-end Data Engineering workflows.
- Databricks Lakehouse architecture.
- Lakeflow Spark Declarative Pipelines.
- Medallion Architecture implementation.
- Delta Lake and Unity Catalog.
- SQL-based data transformations.
- Data cleaning and preprocessing.
- Data quality expectations and validation.
- Duplicate detection and handling.
- Data lineage and audit tracking.
- Business data modeling and aggregation.
- Executive dashboard development.
- Data reconciliation and reporting.

---

## ▶️ How to Explore This Project

1. Clone or download this repository.
2. Review `pipeline_sql_code.sql` to understand the pipeline implementation.
3. Upload `course_enrollments_raw.csv` into a Unity Catalog Volume in your Databricks workspace.
4. Configure the required catalog, schema, and volume paths.
5. Configure and execute the Lakeflow Spark Declarative Pipeline.
6. Verify Bronze, Silver, Rejected, and Gold tables.
7. Connect Gold-layer tables to Databricks AI/BI Dashboards.
8. Explore the dashboard visualizations and reconciliation results.

**Note:** Update the catalog, schema, and volume paths in the SQL script according to your Databricks environment before execution.

---

## 👨‍💻 Author

**Pavan Mandala**

Data Engineering & Analytics Intern

Interested in Data Engineering, Data Analytics, SQL, Python, Databricks, and Business Intelligence.

---

⭐ If you find this project useful, feel free to explore the repository and share your feedback!
