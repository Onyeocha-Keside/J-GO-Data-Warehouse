# JéGO Data Warehouse

## Overview
The JéGO Data Warehouse project is a centralized data infrastructure designed to collect, transform, and store data from various sources across all company products. This initiative serves as the backbone for advanced analytics, reporting, and decision-making.

Currently, the first pipeline has been implemented to ingest **weather data** into a PostgreSQL database for now, marking the initial step in building the broader data ecosystem.

---

## Current Implementation

### Weather Data Pipeline
The first module of the JeGO Data Warehouse focuses on weather data for Lagos, Nigeria. This pipeline uses **Apache Airflow** for orchestration and consists of the following components:

1. **Extract**:
   - Data is fetched from the **Open Meteo API**, capturing real-time weather information for Lagos.
   - Extracted fields include:
     - Latitude and Longitude
     - Temperature
     - Wind Speed
     - Wind Direction
     - Weather Code

2. **Transform**:
   - The raw data is processed into a structured format to align with the database schema.
   - Ensures data consistency and readiness for integration with future modules.

3. **Load**:
   - Transformed data is loaded into a **PostgreSQL** database.
   - A table named `weather_data` is created (if it does not already exist) with the following schema:
     - **latitude**: FLOAT
     - **longitude**: FLOAT
     - **temperature**: FLOAT
     - **windspeed**: FLOAT
     - **winddirection**: FLOAT
     - **weathercode**: INT
     - **timestamp**: TIMESTAMP (default to the current timestamp)

### Technologies Used
- **Apache Airflow**: Orchestrates the ETL process with daily scheduling.
- **PostgreSQL**: Serves as the initial data warehouse for storing weather data.
- **Python**: Implements ETL logic and Airflow tasks.

---

## Scope and Vision

### Broader Vision
The JeGO Data Warehouse aims to integrate data from all products, enabling a unified platform for analytics and reporting. This includes, but is not limited to:
- **Energy Systems**:
  - Voltage Output
  - Inverter Performance
  - Temperature Differentials
  - Degradation Rates
  - Current Output
  - Power Generation (Watts)
  - Energy Production (Kilowatt-Hours)
  - Panel Efficiency Percentage
- **Sales and Marketing**:
  - Product Performance Metrics
  - Customer Behavior Insights
  - Sales Trends Analysis
- **Operational Data**:
  - Logistics and Supply Chain Performance
  - Staff Efficiency Metrics

### Current Focus
- Develop a robust pipeline for **weather data** as a proof of concept.
- Establish a scalable data warehouse architecture.

### Next Steps
1. **Integrate Additional Data Points**:
   - Expand the scope to include operational and product-specific data streams.
2. **Migrate to Cloud Storage**:
   - Transition from PostgreSQL to a cloud-based solution like AWS S3 or Google BigQuery.
3. **Advanced Analytics**:
   - Use the data warehouse as the foundation for dashboards, predictive analytics, and machine learning models.
4. **Real-Time Monitoring**:
   - Enable real-time alerts and triggers for operational insights.

---

## Getting Started

### Local Development
1. **Prerequisites**:
   - Install Docker and Astronomer CLI.
   - Configure Airflow and PostgreSQL connections in `airflow_settings.yaml`.

2. **Run the Project**:
   - Start the local environment:
     ```bash
     astro dev start
     ```
   - Access the Airflow UI at [http://localhost:8080](http://localhost:8080) with:
     - Username: `admin`
     - Password: `admin`

3. **Database Connection**:
   - Default PostgreSQL setup:
     - Host: `localhost`
     - Port: `5432`
     - Database: `postgres`

4. **Test the Pipeline**:
   - Trigger the `weather_etl_pipeline` DAG in the Airflow UI or let it run on its daily schedule.

### Deploying to Production
1. Deploy the pipeline to an Astronomer-managed Airflow environment:
   ```bash
   astro deploy
