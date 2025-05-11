# 🚖 Uber Data Analytics: An End-To-End Data Engineering Journey

This project showcases the complete lifecycle of a data engineering solution, analyzing Uber-like ride-hailing data. I transformed raw data into actionable insights, leveraging cloud technologies and modern data stack tools.

## Project Overview

The core objective was to build a robust data pipeline. This pipeline ingests raw ride data, transforms it using dimensional modeling principles, and loads it into a data warehouse. Finally, an analytical dashboard visualizes key performance indicators.

---

## 🛠️ Key Technologies & Concepts

*   **Cloud Platform:** Google Cloud Platform (GCP)
    *   Google Cloud Storage (GCS): Data Lake for raw and processed files.
    *   Compute Engine (VM): Hosting for our pipeline tool.
    *   BigQuery: Scalable Data Warehouse.
    *   Looker Studio (formerly Data Studio): Business Intelligence and Visualization.
*   **Data Pipeline Orchestration:** Mage (Open-Source)
*   **Data Transformation:** Python (Pandas)
*   **Data Modeling:** Dimensional Modeling (Fact & Dimension Tables)
*   **Database Querying:** SQL

---

## 📈 The Technical Process: A Step-by-Step Breakdown

Our journey involved several critical phases:

### 1. Conceptual Data Modeling

I began by defining the analytical requirements. This led to designing a dimensional model.
*   **Fact Tables:** Captured quantitative transactional data (e.g., fare amounts, trip durations).
*   **Dimension Tables:** Provided context to facts (e.g., date/time details, passenger counts, location info, payment types).
*   Tools like Lucidchart Ire used for initial schema visualization.


![Conceptual Data Model](images\data_model.jpeg)
*Image: A sketch or diagram of the initial fact and dimension table relationships.*

This iterative process established primary and foreign key relationships crucial for data integrity and efficient querying.

### 2. Data Ingestion & Transformation with Python

Raw CSV data, mimicking Uber's dataset, was ingested.
*   Pandas library in Python was pivotal for this stage.
*   Key transformations included:
    *   Parsing and engineering date/time features (e.g., extracting hour, day of Iek).
    *   Creating surrogate keys for dimension tables.
    *   Handling duplicates and ensuring data consistency.
    *   Mapping IDs to descriptive names (e.g., `rate_code_id` to `Rate Code Name`).
*   Multiple dataframes Ire programmatically generated: one for each dimension and one for the central fact table.
*   Joins based on keys linked these dataframes, forming a cohesive model.

### 3. GCP Infrastructure Setup

I provisioned the necessary GCP services:
*   **Google Cloud Storage (GCS):** A bucket was created to store the transformed data files before loading them into the warehouse. Public URL access was configured for Mage.
*   **Compute Engine:** A Virtual Machine instance was launched.
    *   The Python environment was configured on the VM.
    *   Mage was installed via PIP.
*   **Firewall Rules:** A GCP firewall rule was established to allow inbound traffic on port `6789`, enabling access to the Mage UI from a browser.


![GCP Firewall Rule](images\firewallgcp.png)
*Image: Screenshot of the GCP firewall rule setup.*

### 4. Building the ETL Pipeline with Mage

Mage orchestrated the data flow from source to destination.
*   A new Mage project was initialized (`mage start project_name`).
*   The pipeline consisted of distinct blocks:
    *   **Data Loader:** Configured to read data from the GCS public URL.
    *   **Transformer:** Embedded the Python transformation logic developed earlier. This block outputted multiple dataframes (fact and dimensions).
    *   **Data Exporter:** Loaded the transformed dataframes into BigQuery.
*   Mage's UI facilitated pipeline design and execution monitoring.


![Mage Pipeline UI](images\magegcp.png)
*Image: Screenshot of the Mage UI depicting the pipeline's data flow.*

### 5. Data Warehousing in BigQuery

The transformed data landed in Google BigQuery.
*   **Credentials:** A GCP Service Account was created with necessary permissions (BigQuery Data Editor, etc.). A JSON key was generated and its contents Ire securely configured in Mage's `io_config.yaml` file for authentication.
*   **Schema:** Datasets and tables (fact and dimensions) Ire created in BigQuery, mirroring our dimensional model.
*   Data was passed as dictionaries of dataframes from the Mage transformer to the BigQuery exporter.

### 6. Data Analysis with SQL

With data warehoused, I performed SQL queries in BigQuery for initial analysis.
*   Joined fact and dimension tables to derive insights.
*   Example queries:
    *   Average fare amount by vendor.
    *   Total trips per pickup location.
    *   Average tip amount by payment type.
*   An **analytical layer** (a consolidated view or table) was created by joining relevant tables and selecting key columns, optimizing for dashboard performance.

### 7. Visualization with Looker Studio

The final step involved creating an interactive dashboard.
*   Looker Studio was connected to our BigQuery analytical layer.
*   The dashboard featured:
    *   Key metrics (Total Revenue, Average Trip Distance).
    *   Charts (e.g., revenue by payment type, trips by hour).
    *   Map visualizations for pickup/dropoff locations.
    *   Interactive filters (Vendor ID, Rate Code, Payment Type).
*   This provided a user-friendly interface for exploring data and uncovering business insights.


![Looker Studio Dashboard](images\Uber_Dashboard.jpg)
*Image: A screenshot of the final, insightful dashboard created in Looker Studio.*

---

## 🌟 Key Skills Demonstrated

*   **Data Modeling:** Designing and implementing dimensional models (Star Schema).
*   **ETL Development:** Building robust data pipelines using Python (Pandas) and Mage.
*   **Cloud Engineering (GCP):** Provisioning and managing GCS, Compute Engine, BigQuery.
*   **Data Warehousing:** Structuring data in BigQuery for analytical querying.
*   **SQL:** Advanced querying for data analysis and aggregation.
*   **Business Intelligence & Visualization:** Creating insightful dashboards with Looker Studio.
*   **Problem Solving:** Iteratively refining code and configurations.

---
