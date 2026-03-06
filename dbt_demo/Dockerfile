FROM python:3.11-slim

WORKDIR /app

COPY . /app

RUN pip install --upgrade pip && pip install dbt-postgres

ENV DBT_PROFILES_DIR=/app/config

CMD ["dbt", "run"]