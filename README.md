# Airflow-in-Docker-Setup

This repository implements an automated ETL (Extract–Transform–Load) pipeline using Apache Airflow, orchestrated via Docker and backed by an external PostgreSQL database.

**Extract**: Source data is retrieved from a remote files such as (CSV, TXT, PARQUET) endpoint via HTTP request.
**Load**: Data is bulk-loaded into a staging table (employees_temp) using PostgreSQL's COPY protocol, isolating raw data from the production schema.
**Transform**: Records are deduplicated and merged into the production table (employees) via an upsert operation (INSERT, UPDATE), ensuring idempotent execution — repeated runs do not create duplicates.

Orchestration: Task dependencies are defined as a DAG (Directed Acyclic Graph), guaranteeing schema creation precedes loading, and loading precedes transformation. The pipeline runs on a daily schedule with a bounded execution timeout.
Deployment: Airflow runs in Docker for isolation and reproducibility, while PostgreSQL runs independently — reflecting a typical production separation of compute and storage layers.
