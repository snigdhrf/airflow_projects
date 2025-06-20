# 🌤️ Weather ETL Pipeline with Apache Airflow

This project implements an **Apache Airflow ETL pipeline** that automatically fetches real-time weather data from the [Open-Meteo API](https://open-meteo.com/), processes it, and loads it into a **PostgreSQL database** on a daily schedule.

---

## 🔧 What It Does

This Airflow DAG (`weather_etl_pipeline`) performs the following steps:

### 1. Extract
- Uses Airflow’s `HttpHook` to connect to the Open-Meteo API.
- Dynamically constructs the API URL using the specified **latitude** and **longitude**.
- Retrieves the current weather data.

### 2. Transform
- Extracts key fields from the API response:
  - `temperature`, `windspeed`, `winddirection`, `weathercode`
- Adds location metadata (`latitude`, `longitude`).

### 3. Load
- Uses Airflow’s `PostgresHook` to connect to a PostgreSQL database.
- Creates a table (`weather_data`) if it doesn’t exist.
- Inserts the transformed weather data into the table.

---

## 📦 Technologies Used

- **Apache Airflow** (2.9+)
- **Airflow Providers**:
  - `apache-airflow-providers-http`
  - `apache-airflow-providers-postgres`
- **PostgreSQL**
- **Docker** (if running via Astro CLI)
- **Open-Meteo API**

---

## 📌 Notes

- This DAG runs on a **daily schedule** (`@daily`).
- Requires Airflow connections:
  - `API_CONN_ID` – an HTTP connection for the Open-Meteo API.
  - `POSTGRES_CONN_ID` – a connection to the target PostgreSQL database.
- Compatible with **Airflow 2.9+** and **Python 3.8–3.11**.

---