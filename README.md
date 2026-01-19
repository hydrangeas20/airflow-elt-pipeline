# 🚀 e2e-elt-pipeline-airflow — Airflow ELT Pipeline (NASA API → PostgreSQL)

This repository implements a production style ELT pipeline orchestrated with Apache Airflow. The pipeline extracts JSON data from an external REST API (NASA APOD – Astronomy Picture of the Day), performs lightweight transformation, and loads curated records into a PostgreSQL database. The workflow is containerized using Docker for reproducibility across environments.

## 🌍 Overview

This project demonstrates how to build a production-style data engineering workflow with:

- Workflow orchestration using Apache Airflow DAGs

- Automated scheduling and monitoring via the Airflow UI

- REST API extraction using Airflow HTTP operators

- JSON transformation using Python TaskFlow tasks

- Database loading into PostgreSQL using Airflow Hooks/Operators

- Containerized services using Docker (Airflow + Postgres)

### 🛰️ Problem Context: API-Based Data Ingestion

Many modern data pipelines rely on ingesting data from external APIs (e.g., analytics, telemetry, finance, observability, public datasets). These sources often deliver information as JSON responses, which must be extracted, cleaned, validated, and stored for downstream analysis.

This project simulates a real-world ingestion pipeline where Airflow is used to:

- Fetch structured API data on a schedule

- Process/standardize JSON fields

- Persist records into a relational database for reporting and querying

### 📡 Dataset / Data Source

This pipeline extracts data from:

NASA APOD API (Astronomy Picture of the Day)

Each daily API response contains structured metadata, including:

```bash
title
explanation
url
date
media_type
```

The pipeline stores these fields in PostgreSQL for historical querying and analysis.

### ✨ Key Features

#### 🧩 Airflow DAG Orchestration

- DAG-based pipeline execution with task dependencies

- Scheduled execution (daily pipeline runs)

<b>Airflow UI support for:</b>

- Run history

- Task status monitoring

- Logs and troubleshooting

#### 🌐 API Extraction (HTTP Operator)

- Uses Airflow’s SimpleHttpOperator to fetch JSON payloads

- Handles API integration in a reusable Airflow pattern

#### 🔄 Transformation (TaskFlow API)

- Transforms raw JSON into a cleaned structured object

- Extracts relevant fields and enforces formatting consistency

#### 🗄️ Load into PostgreSQL (Hook + Operator)

- Uses PostgresHook / PostgresOperator to interact with PostgreSQL

- Creates the target table automatically if it doesn’t exist

- Loads transformed records into structured relational storage

### 🐳 Dockerized Services

- Airflow and PostgreSQL run as isolated services through Docker

- Environment is reproducible across machines

- Database persistence supported through Docker volumes

### 🧱 Pipeline Stages

The ELT pipeline consists of three core stages:

<b>1) Extract</b>

Calls NASA’s APOD API via HTTP GET request

Returns metadata in JSON format

<b>2) Transform </b>

Parses JSON payload

Selects fields needed for storage

Normalizes values into a database-ready record

<b>3) Load </b>

Creates table if missing

Inserts transformed record into PostgreSQL

### 🧠 Tech Stack

Language: Python

Orchestration: Apache Airflow

Database: PostgreSQL

API Integration: REST APIs / JSON

Operators/Hooks: SimpleHttpOperator, TaskFlow API, PostgresHook

Containerization: Docker + Docker Compose

### 📁 Repository Structure

```bash
e2e-elt-pipeline-airflow/
│
├── dags/
│   └── etl.py               # Airflow DAG (Extract → Transform → Load)
│
├── docker-compose.yml       # Docker services (Postgres + pipeline environment)
├── requirements.txt         # Python dependencies
└── README.md
```

### 📋 Setup & Usage

1. Start services (Docker)
   docker compose up -d

2. Open Airflow UI
   http://localhost:8080

3. Trigger the DAG

Enable the DAG in Airflow

Trigger a manual run OR allow schedule to execute automatically

### ⚙️ Workflow Architecture Summary

This project demonstrates a practical pipeline architecture commonly used in production environments:

API ingestion layer (HTTP extraction)

Transform layer (Python TaskFlow)

Storage layer (Postgres load)

Orchestration + monitoring layer (Airflow)
