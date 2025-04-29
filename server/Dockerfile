# 1. Add a base image
FROM python:3.12.0-slim-bookworm

# 2. Set environment variables for performance
ENV PYTHONBUFFERED 1
ENV PYTHONWRITEBYTECODE 1
ENV APP=/app

# 3. Install and update Python dependencies
# (via requirements.txt)
WORKDIR $APP
COPY requirements.txt $APP
RUN pip install --upgrade pip && pip install -r requirements.txt

# 4. Copy the rest of the app files
COPY . $APP

# 5. Expose port (Django usually runs on 8000)
EXPOSE 8000

# 6. Make entrypoint executable and run it
RUN chmod +x /app/entrypoint.sh

# Entrypoint shell script to handle migrations
ENTRYPOINT ["/bin/bash", "/app/entrypoint.sh"]

# Start the Gunicorn server
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]
