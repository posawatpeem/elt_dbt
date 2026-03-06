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

    POSTGRES_HOST=XXX
    POSTGRES_USER=XXX
    POSTGRES_PASSWORD=XXX
    POSTGRES_PORT=5432

    AIRFLOW_DB=XXX
    WAREHOUSE_DB=XXX

    AIRFLOW_UID=XXX

    AIRFLOW_ADMIN_USERNAME=XXX
    AIRFLOW_ADMIN_PASSWORD=XXX
    AIRFLOW_ADMIN_FIRSTNAME=XXX
    AIRFLOW_ADMIN_LASTNAME=XXX
    AIRFLOW_ADMIN_ROLE=XXX
    AIRFLOW_ADMIN_EMAIL=XXX

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
