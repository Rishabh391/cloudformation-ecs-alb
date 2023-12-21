FROM python:3.11 AS base
WORKDIR /app
Run python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
COPY gunicorn_app/requirements.txt ./
RUN pip install -r requirements.txt

FROM python:3.11-alpine3.17 AS release  
WORKDIR /app
COPY --from=base /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
COPY . .
CMD ["gunicorn", "--config", "./gunicorn_app/conf/gunicorn_config.py", "gunicorn_app:app"]
