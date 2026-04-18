# ---- Stage 1: Build ----
FROM python:3.10-slim-bullseye AS builder

WORKDIR /app

COPY requirements.txt .

RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential libpq-dev && \
    pip install --upgrade pip && \
    pip install -r requirements.txt

# ---- Stage 2: Runtime ----
FROM python:3.10-slim-bullseye

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.10 /usr/local/lib/python3.10
COPY --from=builder /usr/local/bin /usr/local/bin

COPY . .

EXPOSE 5153

CMD ["python", "app.py"]
