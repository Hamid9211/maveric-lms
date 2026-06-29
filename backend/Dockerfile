# Backend Dockerfile - FastAPI with Uvicorn/Gunicorn
FROM python:3.11-slim AS base
WORKDIR /app

# System deps
RUN apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/*

# Install python deps
FROM base AS builder
COPY requirements.txt ./
RUN python -m pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# Copy application
FROM base
WORKDIR /app
COPY --from=builder /usr/local /usr/local
COPY . ./

EXPOSE 8000

# Start with Gunicorn + Uvicorn workers
CMD ["gunicorn", "-k", "uvicorn.workers.UvicornWorker", "app.main:app", "--bind", "0.0.0.0:8000", "--workers", "1"]
