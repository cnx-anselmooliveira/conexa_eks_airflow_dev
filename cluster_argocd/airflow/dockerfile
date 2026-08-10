FROM apache/airflow:3.2.2

ARG AIRFLOW_VERSION=3.2.2
ARG PYTHON_VERSION=3.12

USER root
ENV TZ=America/Sao_Paulo

# só instala dependências de sistema necessárias pra compilar, remove depois
COPY --chown=airflow:airflow requirements.txt /opt/airflow/requirements.txt
COPY --from=ghcr.io/astral-sh/uv:latest /uv /usr/local/bin/uv

ENV CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

RUN uv pip install --no-cache \
    --constraint "${CONSTRAINT_URL}" \
    --system \
    -r /opt/airflow/requirements.txt

USER airflow