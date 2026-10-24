NYC Taxi Data Engineering Project
An end-to-end data engineering project built with Databricks, PySpark, Delta Lake, and Unity Catalog to process NYC taxi trip data and turn raw files into analytics-ready tables.
Project Overview
The project follows the Medallion Architecture:
- Bronze: Ingests raw Parquet taxi files using Auto Loader and stores them in Delta tables.
- Silver: Cleans and deduplicates trips, derives useful trip metrics, and separates invalid records for data-quality review.
- Gold: Builds fact and dimension tables and business-focused data marts for reporting.
Tech Stack
- Databricks
- Apache Spark / PySpark
- Delta Lake
- Unity Catalog
- Auto Loader
- SQL
Key Features
- Incremental file ingestion with Auto Loader
- Delta tables for reliable data storage
- Trip deduplication using a hashed business key
- Data-quality checks and quarantine handling
- SCD Type 1 and SCD Type 2 dimension logic
- Fact table design for trip-level analysis
- Gold data marts for daily KPIs and hourly demand
- Data-quality validation checks
Data Pipeline
Raw Parquet Files
       |
       v
   Bronze Layer
       |
       v
   Silver Layer
(cleaning & deduplication)
       |
       v
 Gold Fact & Dimensions
       |
       v
   Gold Data Marts
(analytics and reporting)
Repository Structure
File	Purpose
01_setup_unity_catalog.py	Central configuration for catalog, schemas, paths, and table names
02_setup_unity_catalog.py	Creates catalog, schemas, volume, and folders
03_nyc_taxi_bronze_layer.py	Ingests raw taxi data into Bronze using Auto Loader
04_silver_clean.py	Cleans and deduplicates data and handles rejected records
05_dimensions_scd2.py	Creates date, zone, vendor, payment, and rate-code dimensions
06_fact_trips.py	Builds the trip fact table and incremental-load watermark logic
07_gold_marts.py	Creates analytical data marts and KPIs
08_data_quality_checks.py	Runs validation checks on the pipeline output


Note: Some notebook filenames in the ZIP include timestamps. The names above are simplified for readability.
Setup and Run
1. Create or open a Databricks workspace with Unity Catalog enabled.
2. Upload the project notebooks to your workspace.
3. Update catalog, schema, volume, and file paths in 01_setup_unity_catalog.py if needed.
4. Place the source taxi Parquet files in the configured raw trips volume path.
5. Run the notebooks in order, from 01 through 08.
6. Review the resulting Delta tables and Gold marts in Databricks SQL.
Example Analytics
The Gold marts are designed to support questions such as:
- How many trips happen each day or hour?
- What is the total and average trip revenue?
- Which pickup zones have the highest demand?
- How do trip distance, duration, and speed vary?
- What percentage of trips use card payments?
- How much taxi activity is associated with airports?
Data Quality
The project includes checks for duplicate trip keys, missing date keys, orphan zone keys, invalid revenue values, SCD Type 2 validity windows, and non-empty Gold marts.
Notes
- This project is designed to run in Databricks; it is not a standalone local Python application.
- Source datasets are not included in this repository ZIP, so provide your own compatible NYC taxi Parquet files.
- Cloud storage, Unity Catalog permissions, and volume paths must be configured for your workspace.
