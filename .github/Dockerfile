# Stage 1: Build stage
FROM python:3.9-slim AS builder

WORKDIR /app

# Install dependencies to a local folder
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# Stage 2: Final Runtime stage
FROM python:3.9-slim

WORKDIR /app

# Copy only the installed libraries from the builder
COPY --from=builder /root/.local /root/.local
# Copy your application code
COPY app.py .

# Update PATH so the system can find the installed packages
ENV PATH=/root/.local/bin:$PATH
# Ensure logs are sent straight to the terminal (best for K8s)
ENV PYTHONUNBUFFERED=1

EXPOSE 3000

CMD ["python", "app.py"]