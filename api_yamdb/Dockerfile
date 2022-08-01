FROM python:3.7-slim
WORKDIR /app
COPY ./api_yamdb/requirements.txt .
RUN pip3 install -r requirements.txt --no-cache-dir
COPY . .
WORKDIR /app/api_yamdb/
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "api_yamdb.wsgi:application"]