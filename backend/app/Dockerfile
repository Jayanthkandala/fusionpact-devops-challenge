# Use a slim Python image
FROM python:3.9-slim

WORKDIR /app

# Install system dependencies for psycopg2 and gcloud CLI
# Note: Cloud SQL Proxy setup is for the final deployment phase (Cloud Run sidecar)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential libpq-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app/ /app/app/

EXPOSE 8080

# Command to run the application
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "app.main:app"]
