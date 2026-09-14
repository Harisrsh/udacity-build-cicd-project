FROM python:3.10-slim

RUN adduser --uid 1000 --disabled-password --gecos "" app

RUN apt-get update && apt-get install -y \
    libpcre2-dev \
    build-essential \
    gcc \
    linux-headers-amd64 \
    libffi-dev \
    openssl \
    && rm -rf /var/lib/apt/lists/* \
    && pip install pipenv

RUN mkdir -p /var/www/app && mkdir /app

WORKDIR /app

COPY Pipfile* /app/

RUN cd /app && pipenv install --system --deploy

COPY . /app

EXPOSE 5000

USER app

CMD ["uwsgi", "--http", "0.0.0.0:5000", "--wsgi-file", "app.py", "--callable", "app"]ript-name --mount /=app:app