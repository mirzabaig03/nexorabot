# FROM python:3.11-slim

# ENV PYTHONUNBUFFERED=1 \
#     POETRY_VIRTUALENVS_CREATE=false \
#     POETRY_NO_INTERACTION=1 \
#     PYTHONPATH=/app


# RUN apt-get update && apt-get install -y \
#     build-essential \
#     libmagic-dev \
#     libgl1 \
#     libglib2.0-0 \
#     poppler-utils \
#     tesseract-ocr \
#     libreoffice \
#     libreoffice-impress \
#     libreoffice-writer \
#     libreoffice-calc \
#     curl \
#     && rm -rf /var/lib/apt/lists/*

# RUN pip install --no-cache-dir poetry==2.3.2

# WORKDIR /app

# COPY pyproject.toml poetry.lock ./

# RUN poetry install --no-root --only main

# COPY . .

# EXPOSE 8000

# CMD ["uvicorn", "src.server:app", "--host", "0.0.0.0", "--port", "8000"]


# ____________________________________________________________________________________________



FROM python:3.11-slim

# -----------------------------
# Environment variables
# -----------------------------
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    POETRY_VIRTUALENVS_CREATE=false \
    POETRY_NO_INTERACTION=1 \
    PYTHONPATH=/app

# -----------------------------
# System dependencies
# Required for:
# - unstructured
# - OpenCV
# - OCR
# - PDF parsing
# - LibreOffice conversions
# -----------------------------
RUN apt-get update && apt-get install -y \
    build-essential \
    libmagic-dev \
    libgl1 \
    libglib2.0-0 \
    poppler-utils \
    tesseract-ocr \
    libreoffice \
    libreoffice-impress \
    libreoffice-writer \
    libreoffice-calc \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# -----------------------------
# Install Poetry
# -----------------------------
RUN pip install --no-cache-dir poetry==2.3.2

# -----------------------------
# Set working directory
# -----------------------------
WORKDIR /app

# -----------------------------
# Copy dependency files
# (better Docker cache usage)
# -----------------------------
COPY pyproject.toml poetry.lock* ./

# -----------------------------
# Install dependencies
# -----------------------------
RUN poetry install --no-root --only main

# -----------------------------
# Copy application source
# (overwritten by volume in dev)
# -----------------------------
COPY . .

# -----------------------------
# Expose FastAPI port
# -----------------------------
EXPOSE 8000

# -----------------------------
# Start FastAPI
# Compose overrides this command
# -----------------------------
CMD ["uvicorn", "src.server:app", "--host", "0.0.0.0", "--port", "8000"]