# 📊 IFRS 15 Revenue Recognition Data Pipeline (Deloitte Consulting)

## 📌 Project Overview
This project was developed for **Deloitte Consulting** to automate the **daily calculation of recognized revenue and profit** according to **IFRS 15**. The solution is built using **Databricks, PySpark, and Delta Lake** and processes contract, transaction, and employee cost data.

## 🏠 Project Architecture
The project consists of **three data processing layers**:

1️⃣ **Bronze Layer (Raw Data Ingestion)**
   - Reads raw **CSV files** from Azure Data Lake (ADLS).
   - Converts data to **Parquet format** for optimized storage.
   - Moves processed files to the "processed" zone in ADLS.

2️⃣ **Silver Layer (Data Cleaning & Transformation)**
   - Cleans and standardizes data (**removes duplicates, renames columns**).
   - Converts date formats and ensures correct data types.
   - Loads cleaned data into **Delta Tables** for further processing.

3️⃣ **Gold Layer (IFRS 15 Revenue Recognition)**
   - Aggregates contract, transaction, and employee cost data.
   - **Calculates recognized revenue & profit** using the **percentage of completion method**.
   - Exports daily reports to **Azure Blob Storage** in **Excel format**.

## Data Processing Workflow
1. **Contracts, Transactions, and Employee Costs** are loaded from **Azure Blob Storage (CSV format)**.
2. Data is **cleaned, deduplicated, and standardized** before being stored in **Delta Tables**.
3. The **Gold Layer** performs **financial calculations**:
   - 📌 **Cost Incurred Percentage** = (Recognized Costs + Payroll Expenses) / Estimated Costs
   - 📌 **Recognized Revenue** = Contract Amount × Cost Incurred Percentage
   - 📌 **Recognized Profit** = Recognized Revenue - Total Costs
4. The final results are **saved in Delta Tables and exported as daily reports**.

## Technologies Used
- **🔹 PySpark** → Distributed data processing
- **🔹 Databricks** → Cloud-based analytics platform
- **🔹 Delta Lake** → Optimized storage & versioning
- **🔹 Azure Data Lake Storage (ADLS)** → Cloud storage
- **🔹 Pandas & OpenPyxl** → Excel report generation

## How to Run the Project
1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ifrs15-revenue-pipeline.git
   ```
2. **Upload the scripts to Databricks**.
3. **Run the Bronze Layer notebook** to ingest raw data.
4. **Run the Silver Layer notebook** to clean and transform the data.
5. **Run the Gold Layer notebook** to calculate revenue and generate reports.

## 📂 Project Files
| File | Description |
|------|------------|
| `Bronze_layer.py` | Ingests raw CSV data from Azure, converts to Parquet, and moves files. |
| `Silver_layer.py` | Cleans, deduplicates, and standardizes data before loading into Delta Tables. |
| `Gold_layer.py` | Calculates recognized revenue & profit, then exports reports to Azure. |

## 📌 Future Enhancements
🔹 Implement **Apache Airflow** for **pipeline automation**.  
🔹 Optimize **Spark performance** using **Z-Ordering & Caching**.  
🔹 Deploy an **API endpoint** to query recognized revenue in real-time.


