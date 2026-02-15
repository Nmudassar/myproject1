<<<<<<< HEAD
Overview
========

Welcome to Astronomer! This project was generated after you ran 'astro dev init' using the Astronomer CLI. This readme describes the contents of the project, as well as how to run Apache Airflow on your local machine.

Project Contents
================

Your Astro project contains the following files and folders:

- dags: This folder contains the Python files for your Airflow DAGs. By default, this directory includes one example DAG:
    - `example_astronauts`: This DAG shows a simple ETL pipeline example that queries the list of astronauts currently in space from the Open Notify API and prints a statement for each astronaut. The DAG uses the TaskFlow API to define tasks in Python, and dynamic task mapping to dynamically print a statement for each astronaut. For more on how this DAG works, see our [Getting started tutorial](https://www.astronomer.io/docs/learn/get-started-with-airflow).
- Dockerfile: This file contains a versioned Astro Runtime Docker image that provides a differentiated Airflow experience. If you want to execute other commands or overrides at runtime, specify them here.
- include: This folder contains any additional files that you want to include as part of your project. It is empty by default.
- packages.txt: Install OS-level packages needed for your project by adding them to this file. It is empty by default.
- requirements.txt: Install Python packages needed for your project by adding them to this file. It is empty by default.
- plugins: Add custom or community plugins for your project to this file. It is empty by default.
- airflow_settings.yaml: Use this local-only file to specify Airflow Connections, Variables, and Pools instead of entering them in the Airflow UI as you develop DAGs in this project.

Deploy Your Project Locally
===========================

Start Airflow on your local machine by running 'astro dev start'.

This command will spin up five Docker containers on your machine, each for a different Airflow component:

- Postgres: Airflow's Metadata Database
- Scheduler: The Airflow component responsible for monitoring and triggering tasks
- DAG Processor: The Airflow component responsible for parsing DAGs
- API Server: The Airflow component responsible for serving the Airflow UI and API
- Triggerer: The Airflow component responsible for triggering deferred tasks

When all five containers are ready the command will open the browser to the Airflow UI at http://localhost:8080/. You should also be able to access your Postgres Database at 'localhost:5432/postgres' with username 'postgres' and password 'postgres'.

Note: If you already have either of the above ports allocated, you can either [stop your existing Docker containers or change the port](https://www.astronomer.io/docs/astro/cli/troubleshoot-locally#ports-are-not-available-for-my-local-airflow-webserver).

Deploy Your Project to Astronomer
=================================

If you have an Astronomer account, pushing code to a Deployment on Astronomer is simple. For deploying instructions, refer to Astronomer documentation: https://www.astronomer.io/docs/astro/deploy-code/

Contact
=======

The Astronomer CLI is maintained with love by the Astronomer team. To report a bug or suggest a change, reach out to our support.
=======
# myproject1
Real-Time Stock Market Data Pipeline using Apache Airflow, Spark, Docker, and MinIO

---

# Real-Time Stock Market Data Pipeline using Apache Airflow, Spark, Docker, and MinIO

## Project Summary

Designed and implemented a production-grade data pipeline that automatically extracts stock market data from Yahoo Finance, processes it using Apache Spark, and stores structured output in MinIO object storage. The pipeline is fully orchestrated using Apache Airflow and executed inside Docker containers.

This project demonstrates end-to-end Data Engineering workflow orchestration, distributed processing, containerization, and scalable architecture.

---

## Business Problem

Financial and analytics systems require reliable, automated pipelines to ingest and transform stock market data for reporting, analytics, and decision-making.

Without orchestration tools, teams face:

* Manual data collection
* Lack of automation
* No monitoring or scheduling
* Poor scalability
* Data processing delays
* High operational overhead

---

## Solution

Built an automated ETL pipeline using Airflow and Spark that:

* Automatically extracts stock market data via API
* Stores raw data in object storage (MinIO)
* Processes and transforms data using Apache Spark
* Outputs clean, structured CSV files
* Runs on scheduled workflows
* Executes distributed processing using Docker and Spark

---

## Architecture Overview

```
                 Yahoo Finance API
                        │
                        ▼
              Airflow Sensor Task
          (Check API availability)
                        │
                        ▼
             Airflow Extract Task
                (PythonOperator)
                        │
                        ▼
               MinIO Object Storage
                  (Raw JSON)
                        │
                        ▼
          Airflow DockerOperator
                (Spark Job)
                        │
                        ▼
               Apache Spark Cluster
             (Data Transformation)
                        │
                        ▼
               MinIO Object Storage
                 (Formatted CSV)
                        │
                        ▼
              Ready for Analytics
```

---

## Tech Stack

### Orchestration

* Apache Airflow
* Astro CLI

### Data Processing

* Apache Spark
* PySpark

### Storage

* MinIO (S3-compatible object storage)

### Containerization

* Docker
* DockerOperator (Airflow)

### Programming Language

* Python

### Infrastructure & Tools

* Docker Desktop
* Linux
* Airflow Connections & XCom

### APIs

* Yahoo Finance API

---

## Key Features

* Fully automated pipeline using Airflow DAG
* Distributed data transformation using Spark
* Containerized execution using Docker
* Object storage integration using MinIO
* Dynamic task communication using XCom
* Fault-tolerant workflow execution
* Production-ready architecture

---

## Airflow DAG Workflow

```
is_api_available
      │
      ▼
get_stock_prices
      │
      ▼
store_prices (MinIO)
      │
      ▼
format_prices (Spark Docker Container)
      │
      ▼
get_formatted_csv
```

---

## Data Processing Flow

### Raw Data (MinIO)

```
stock-market/AAPL/prices.json
```

### Processed Output

```
stock-market/AAPL/prices.json/formatted_prices/
```

Contains:

* timestamp
* open price
* close price
* high price
* low price
* volume
* formatted date

---

## Spark Transformation Tasks

* Read JSON from MinIO
* Explode nested arrays
* Transform into structured dataset
* Convert timestamp to date format
* Write formatted CSV to MinIO

---

## Project Structure

```
stock-market-pipeline/
│
├── dags/
│   └── stock_market.py
│
├── include/
│   └── stock_market/
│       └── tasks.py
│
├── spark/
│   └── stock_transform.py
│
├── Dockerfile
├── requirements.txt
└── README.md
```

---

## How to Run the Project

### Start Airflow

```
astro dev start
```

---

### Run DAG

```
astro dev run dags test stock_market 2025-01-01
```

---

### Access Airflow UI

```
http://localhost:8080
```

Username:

```
airflow
```

Password:

```
******
```

---

## Skills Demonstrated

This project demonstrates strong skills in:

* Data Engineering
* Apache Airflow orchestration
* Apache Spark distributed processing
* Docker containerization
* ETL pipeline design
* Object storage integration
* Workflow automation
* Cloud-native pipeline architecture

---

## Real-World Engineering Concepts Used

* DAG orchestration
* Distributed computing
* Container-based execution
* ETL pipeline architecture
* Fault-tolerant workflows
* Scalable data processing
* Data transformation using Spark

---

## Performance & Scalability

The pipeline is designed to scale horizontally by:

* Running Spark jobs on distributed clusters
* Adding Airflow workers
* Scaling object storage
* Deploying on Kubernetes

---

## Future Improvements

* Deploy on Kubernetes using KubernetesExecutor
* Add monitoring with Grafana and Prometheus
* Add alerting with Slack integration
* Add CI/CD pipeline
* Deploy to AWS using S3 and EKS

---

## Author

Nadia
Junior Cloud Engineer | Data Engineer

Certifications:

* AWS Solutions Architect
* Certified Kubernetes Administrator (CKA)
* Terraform Associate

>>>>>>> 963e6827706fbeef555ad3b3ecc6750033139bd0
