
# **End-to-End COVID Analytics Pipeline**

## **📌 Executive Summary**
This project implements a scalable, enterprise-grade data pipeline on **Microsoft Azure** to process global COVID-19 datasets. It demonstrates a hybrid approach to data engineering—combining **low-code ETL (Azure Data Factory)** with **high-code distributed computing (Azure Databricks/PySpark)** to transform raw ECDC data into actionable BI insights.

---

## **🏗️ Architectural Framework (Medallion Schema)**
The pipeline follows a layered storage strategy within **Azure Data Lake Storage (ADLS) Gen2**:

1.  **Bronze (Raw):** Immutable ingestion of CSV/TSV source data from ECDC and Blob storage.
2.  **Silver (Cleaned):** Normalized schemas, handled nulls, and standardized country codes using **ADF Data Flows**.
3.  **Gold (Curated):** Aggregated metrics and age-group parsing using **PySpark** on **Databricks**, optimized for analytical consumption.

---

## **🛠️ Tech Stack & Orchestration**

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Orchestration** | **Azure Data Factory (ADF)** | Managing control flow and pipeline scheduling. |
| **Compute** | **Azure Databricks (PySpark)** | Complex transformations & population data parsing. |
| **Storage** | **ADLS Gen2** | Scalable Data Lake with hierarchical namespace. |
| **Warehouse** | **Azure SQL Database** | Serving layer for structured analytical queries. |
| **Visualization** | **Power BI** | End-user reporting and trend analysis. |
| **DevOps** | **Git / GitHub** | Version control for logic and notebooks. |

---

## **🔄 Data Engineering Workflow**

### **1. Ingestion & Multi-Source Integration**
*   **Automated Extraction:** Pulled dynamic ECDC datasets (Cases, Deaths, Testing) via HTTP connectors.
*   **Heterogeneous Formats:** Handled both CSV and TSV (Population data) integration into a unified landing zone.

### **2. Transformation & Normalization**
*   **ADF Data Flows:** Performed lookups for country code standardization and pivoted indicators for flattened reporting.
*   **Databricks/PySpark:** Leveraged Spark's distributed engine to parse complex age-group demographics and enrich the data with dimension tables.

### **3. Analytical Serving Layer**
*   Designed a relational schema in **Azure SQL Database** optimized for BI.
*   Implemented partitioned loading of:
    *   *Daily Trends:* Hospital & ICU admissions.
    *   *Weekly Summaries:* Regional testing and positivity rates.

---

## **📈 Business Intelligence & Insights**
The final **Power BI** dashboard provides an interactive interface to explore:
*   **Global Mortality Trends:** Correlation between case spikes and death rates.
*   **Healthcare Capacity:** Real-time visibility into hospital and ICU occupancy levels.
*   **Demographic Slicing:** Filtering by country, date range, and population metrics.

---

## **🚀 Engineering Best Practices**
*   **Security:** Followed a "Secret-less" approach; all credentials managed via environment variables (ready for **Azure Key Vault** integration).
*   **Modularity:** Decoupled compute (Databricks) from orchestration (ADF) for easier maintenance.
*   **Scalability:** Used ADLS Gen2 to ensure the system can handle petabyte-scale datasets if expanded.

---

## **🔮 Roadmap & Future Enhancements**
*   [ ] **CI/CD:** Integrate Azure DevOps for automated deployment.
*   [ ] **Data Quality:** Implement Great Expectations or ADF validation rules.
*   [ ] **Incremental Loading:** Shift from Full Load to Delta Upserts using Change Data Capture (CDC).

