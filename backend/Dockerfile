FROM python:3.10-slim

# Install system dependencies required for OpenCV and mediapipe
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx \
    libglib2.0-0 \
    libsm6 \
    libxrender1 \
    libxext6 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy requirements and install Python dependencies
COPY requirements.txt .

# Install dependencies in a specific order to avoid conflicts
RUN pip install --no-cache-dir werkzeug==2.0.3
RUN pip install --no-cache-dir flask==2.0.1
RUN pip install --no-cache-dir gunicorn==20.1.0
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Set environment variables
ENV PORT=8080

# Run the application with Gunicorn
CMD exec gunicorn --bind 0.0.0.0:$PORT --workers 1 --threads 8 --timeout 0 app:app
