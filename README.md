# Airflow Local Setup (Docker Compose)

This guide explains how to start the Airflow stack locally using Docker
Compose.

The setup includes: - PostgreSQL (Airflow metadata database) - Airflow
services (API server, scheduler, dag processor, triggerer) -
Initialization container (`airflow-init`) that prepares the database

------------------------------------------------------------------------

## 1. Prerequisites

Install:

-   Docker
-   Docker Compose

Verify:

    docker --version
    docker compose version

------------------------------------------------------------------------

## 2. Environment Configuration

Create `.env`:

    POSTGRES_HOST=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=123456
    POSTGRES_PORT=5432

    AIRFLOW_DB=airflow_meta
    WAREHOUSE_DB=warehouse

    AIRFLOW_UID=1000

    AIRFLOW_ADMIN_USERNAME=admin
    AIRFLOW_ADMIN_PASSWORD=admin
    AIRFLOW_ADMIN_FIRSTNAME=Admin
    AIRFLOW_ADMIN_LASTNAME=User
    AIRFLOW_ADMIN_ROLE=Admin
    AIRFLOW_ADMIN_EMAIL=admin@example.com

------------------------------------------------------------------------

## 3. Initialize Airflow Database

Run:

    docker compose run airflow-init

This will:

-   connect to PostgreSQL
-   create Airflow metadata tables
-   run migrations

------------------------------------------------------------------------

## 4. Start Airflow

    docker compose up

Services started:

-   postgres
-   airflow-apiserver
-   airflow-scheduler
-   airflow-dag-processor
-   airflow-triggerer

------------------------------------------------------------------------

## 5. Access UI

Open:

    http://localhost:8080

Login:

    admin / admin

------------------------------------------------------------------------

## 6. Logs

    docker compose logs -f

Specific service:

    docker compose logs -f airflow-scheduler

------------------------------------------------------------------------

## 7. Stop

    docker compose down

------------------------------------------------------------------------

## 8. Reset

    docker compose down -v
    docker compose run airflow-init
    docker compose up

------------------------------------------------------------------------

## Startup Flow

    1. docker compose run airflow-init
    2. docker compose up
# elt_dbt
