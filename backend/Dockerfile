FROM python:3.11-alpine
MAINTAINER ujwal.pachghare
WORKDIR /usr/bin/app
ENV PIP_NO_CACHE_DIR=1
RUN rm -rf /var/lib/apt/lists/*
COPY ./dependencies.txt .
RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r dependencies.txt
COPY . .
RUN python manage.py collectstatic --no-input
RUN python manage.py migrate
EXPOSE 8000
CMD ["gunicorn","backend.wsgi:application","--bind","0.0.0.0:8000","--reload"]
