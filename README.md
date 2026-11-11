🚀 Online Learning Analytics Platform | Databricks Lakehouse & Lakeflow Pipelines

An end-to-end data engineering pipeline and analytics solution built in Databricks using Lakeflow Spark Declarative Pipelines (Delta Live Tables) and Medallion Architecture (Bronze, Silver, Gold). This project transforms raw, messy EdTech export data into trusted, business-ready insights and executive dashboards.

🏛️ Architecture & Data Flow

The project follows a robust multi-hop Medallion Architecture, ensuring progressive data refinement, auditability, and data quality enforcement across layers:

[ Raw CSV (Unity Catalog Volume) ]
               │
               ▼
   [ Bronze Table ] (Raw Ingestion & Metadata Capture)
               │
       ┌───────┴───────┐
       ▼               ▼
[ Silver Clean ]  [ Silver Rejected ] (Data Quality Enforcement)
       │
       ▼
   [ Gold Tables ] (Business Aggregations & Reconciliation)
       │
       ▼
[ Databricks AI/BI Dashboard ] (Executive Reporting)


📂 Repository Structure

├── README.md                          # Project documentation & architecture overview
├── pipeline_sql_code.sql              # Complete Lakeflow declarative pipeline script (Bronze -> Silver -> Gold)
├── datasets/                          # Sample raw export file
│   └── course_enrollments_raw.csv     # 1,283 rows of synthetic EdTech enrollment data
└── screenshots/                       # Visual proof of pipeline DAG, data quality, and dashboard pages
    ├── pipeline_graph.png
    ├── reconciliation_check.png
    └── dashboard_overview.png


🛠️ Tech Stack & Skills Demonstrated

Data Engineering Framework: Databricks Lakeflow Spark Declarative Pipelines / Delta Live Tables (DLT)

Storage & Governance: Unity Catalog Volumes & Schemas

Data Transformation & Modeling: Databricks SQL, Medallion Architecture (Bronze, Silver, Gold)

Data Quality & Auditing: Declarative expectations (EXPECT ... ON VIOLATION DROP ROW), audit logging, and automated row reconciliation

Business Intelligence: Databricks AI/BI Dashboards (KPI counters, monthly trend lines, category distribution charts)

📊 Pipeline Stages & Transformation Logic

1. Bronze Layer (Raw Ingestion)

Purpose: Ingests raw CSV exports from a Unity Catalog Volume into an incremental streaming table (bronze_course_enrollments) without altering source values.

Enhancements: Appends source_file metadata and loaded_at timestamps for complete lineage tracking.

2. Silver Layer (Clean & Validate)

Purpose: Standardizes data quality through four robust cleaning steps:

Deduplication: Removes duplicate records via SELECT DISTINCT on enrollment_id.

Text Standardization: Applies INITCAP and TRIM on categorical fields, and LOWER for email normalization.

Imputation: Uses COALESCE to handle missing city/category values ('Unknown') and computes missing price_paid values (list_price - discount_amount).

Data Quality Constraints: Drops and isolates records with impossible metrics (e.g., progress_pct < 0 or > 100, negative prices) into silver_enrollments_rejected.

Enrichment: Categorizes learner progress dynamically using CASE WHEN into 'Completed', 'In Progress', or 'Not Started'.

3. Gold Layer (Business Aggregations & Reconciliation)

Pre-calculates executive summary views to satisfy key business requirements:

gold_monthly_enrollments: Tracks monthly revenue, active learners, and completion rates.

gold_category_summary: Compares revenue and completion performance across course categories.

gold_course_summary: Evaluates individual course ratings, hours watched, and revenue.

gold_channel_summary: Analyzes acquisition channels (Website, Mobile App, Referral, Social Media).

gold_data_quality: Automated reconciliation audit confirming $\text{Bronze Rows} = \text{Clean Rows} + \text{Rejected Rows} + \text{Duplicates Removed}$.

📈 Executive Dashboard Highlights

Built using Databricks AI/BI Dashboards, the reporting layer delivers 3 core pages:

Overview: High-level KPI cards (Total Enrollments: 1,241, Revenue: ₹27.21L, Completions: 349, Hours Watched: 16,856), monthly revenue trends, and category breakdowns.

Courses & Channels: Deep-dive tables for top-performing courses, completion rates, and acquisition channel efficiency.

Data Quality & Governance: Full transparency on data hygiene, tracking email normalization impact (identifying 61 double-counted users) and 100% reconciliation verification.

💡 Key Project Insights & Review Takeaways

Why Medallion Architecture? Separates concerns so raw data is never lost (Bronze), data errors are safely quarantined and audited (Silver), and clean business logic is fast to query (Gold).

The Email Normalization Impact: Fixing case sensitivity and trailing whitespaces in user emails corrected duplicate user inflation across 61 records, ensuring accurate unique learner metrics.

Robust Reconciliation: Proven mathematical equality across input ingestion and final downstream tables ensures complete audit confidence for business stakeholders.
