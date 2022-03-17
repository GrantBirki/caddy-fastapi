FROM python:alpine3.15

WORKDIR /app

# Setup a nonroot user for security
RUN adduser -D nonroot
USER nonroot

# Upgrade pip
RUN pip install --upgrade pip

# Install dependencies
COPY requirements.txt .
RUN pip install --user --no-cache-dir --upgrade -r requirements.txt

# Copy the app
COPY main.py /app/main.py

# Expose the app's port
EXPOSE 8000

# Setup a healthcheck
HEALTHCHECK --interval=5m --timeout=3s \
  CMD curl -f http://127.0.0.1:8000/health || exit 1

# Run the FastAPI server
ENTRYPOINT ["python", "-m"] 
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
