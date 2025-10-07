# Enterprise-Grade Data Warehouse for Business Intelligence 🚀

This repository showcases a comprehensive, end-to-end data warehousing and analytics solution built from the ground up. It demonstrates the entire data lifecycle, from ingesting raw, disparate data sources to generating actionable business insights. This project is a testament to my skills in **Data Engineering**, **Data Architecture**, and **Data Analytics**.

---

### **Key Features**
* **Scalable Medallion Architecture**: Implemented a robust and scalable Bronze, Silver, and Gold layer architecture to ensure data quality, governance, and traceability across the entire data pipeline.
* **Optimized Star Schema Modeling**: Designed and developed a star schema data model with fact and dimension tables, optimized for high-performance analytical queries and business intelligence applications.
* **Automated ETL Pipelines**: Built efficient and repeatable SQL-based ETL scripts to handle data extraction, transformation, cleansing, and loading, ensuring data is always accurate and up-to-date.
* **Actionable Business Insights**: Developed a suite of SQL-based reports and analytics to uncover key business metrics related to customer behavior, product performance, and sales trends.

---

### **Live Demo / Visuals**

![Data Warehouse Architecture](https://github.com/user-attachments/assets/bc07b98f-7477-4b62-9f21-75f91c9a3ce0)
*(A GIF or a few screenshots of your dashboards or query results would be highly engaging here!)*

---

### **Business Case & Project Objective**

In today's data-driven landscape, businesses need a single source of truth to make informed decisions. This project tackles that challenge head-on by building a centralized data warehouse that consolidates data from disparate ERP and CRM systems.

**The primary objective is to empower business stakeholders with the ability to:**
* Analyze customer behavior to improve marketing and sales strategies.
* Track product performance to optimize inventory and pricing.
* Identify sales trends to forecast future revenue and growth opportunities.

---

### **Tech Stack & Tools**

| Category          | Tool / Technology                                      |
| ----------------- | ------------------------------------------------------ |
| **Database** | SQL Server Express                                     |
| **IDE / Querying**| SQL Server Management Studio (SSMS)                    |
| **Architecture** | Medallion Architecture, Star Schema                    |
| **Version Control**| Git & GitHub                                           |
| **Diagramming** | Draw.io                                                |
| **Documentation** | Notion                                                 |

---

### **Data Architecture Deep Dive**

This project leverages a modern **Medallion Architecture** to progressively refine and transform data, ensuring the highest quality for analytics.

* **Bronze Layer (Raw Ingestion):** This layer serves as the initial landing zone for all source data, providing an unaltered, auditable copy of the raw ERP and CRM files.
* **Silver Layer (Cleansed & Conformed):** Data from the Bronze layer is cleansed, normalized, and integrated. This is where data quality rules are applied to handle missing values, duplicates, and inconsistencies.
* **Gold Layer (Business-Ready & Optimized):** The Silver layer's cleansed data is transformed into a highly optimized star schema, consisting of fact and dimension tables. This is the "single source of truth" for all analytics and reporting.

---
---

## Apache Airflow Setup and Usage

This project utilizes Apache Airflow for orchestrating the data warehouse ETL pipeline. Follow these steps to set up and run Airflow locally using Docker Compose.

### 1. Prerequisites

*   Docker and Docker Compose installed on your system.

### 2. Airflow Setup

Navigate to the `airflow` directory in your terminal:

```bash
cd airflow
```

Build the custom Airflow Docker image and start all the services. This command will:
*   Build a custom Airflow image (from `Dockerfile`) that includes the `apache-airflow-providers-microsoft-mssql` package.
*   Start the PostgreSQL database, Redis, Airflow Webserver, Scheduler, Worker, and Triggerer.
*   Initialize the Airflow database and create the default admin user.

This process might take several minutes the first time it runs.

```bash
docker-compose up -d --build
```

### 3. Accessing the Airflow UI

Once the services are up and running (it might take a minute or two for everything to stabilize), open your web browser and navigate to:

    git clone [https://github.com/your-username/data-warehouse-project.git](https://github.com/your-username/data-warehouse-project.git) 5. Running the DAG

1.  On the Airflow UI homepage, locate the `data_warehouse_pipeline` DAG.
2.  By default, new DAGs are often paused. Click the toggle switch next to the DAG name to **unpause** it.
3.  To manually trigger a run, click the "play" button (Trigger DAG) in the "Actions" column for the `data_warehouse_pipeline` DAG.
4.  You can then click on the DAG name to view its graph, task statuses, and logs.

### 6. Stopping Airflow Services

To stop all Airflow services and clean up the Docker containers (without deleting your PostgreSQL data volume):

```bash
docker-compose down
```

To stop all services and **remove all associated Docker volumes** (including the PostgreSQL database volume, which will delete all Airflow metadata and pipeline data):

```bash
docker-compose down --volumes
```

This is useful for a clean slate if you encounter persistent database-related issues.

### 7. Troubleshooting

*   **`service "airflow-init" didn't complete successfully: exit 1` or `airflow: command not found`**: This usually indicates an issue during the initial setup or a corrupted state. Try a complete reset:
    ```bash
    docker-compose down --volumes --rmi all
    docker-compose up -d --build
    ```
*   **"Broken DAG" in Airflow UI**: Check the Airflow UI for detailed error messages. This often means a Python dependency is missing or there's a syntax error in your DAG file. If you've recently modified `requirements.txt` or `Dockerfile`, ensure you've rebuilt your Docker images.

---

## 📂 Repository Structure

```text
data-warehouse-project/
│
├── datasets/                           # Raw datasets (ERP and CRM data)
│
├── docs/                               # Documentation and diagrams
│   ├── etl.drawio                      # ETL workflow diagrams
│   ├── data_architecture.drawio        # Data warehouse architecture
│   ├── data_catalog.md                 # Dataset catalog with metadata
│   ├── data_flow.drawio                # Data flow diagrams
│   ├── data_models.drawio              # Star schema models
│   ├── naming-conventions.md           # Naming standards for tables & columns
│
├── scripts/                            # SQL scripts for ETL and transformations
│   ├── bronze/                         # Raw data extraction and ingestion
│   ├── silver/                         # Data cleansing and transformations
│   ├── gold/                           # Analytical model creation
│
├── tests/                              # Quality and validation scripts
├── README.md                           # Project overview & instructions
├── LICENSE                             # License information
├── .gitignore                          # Ignore rules for Git
└── requirements.txt                    # Project dependencies

---

### **How to Get Started**

To get this project up and running on your local machine, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/data-warehouse-project.git](https://github.com/your-username/data-warehouse-project.git)
    ```
2.  **Set up the database:**
    * Make sure you have SQL Server Express and SSMS installed.
    * Run the `scripts/init_database.sql` script to create the necessary databases and schemas.
3.  **Run the ETL pipelines:**
    * Execute the SQL scripts in the `scripts/` folder in the following order:
        1.  `bronze/`
        2.  `silver/`
        3.  `gold/`
4.  **Explore the data:**
    * Connect to the database using SSMS and start querying the `gold` layer tables!

---
