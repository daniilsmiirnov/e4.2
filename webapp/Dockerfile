FROM python:3.10.9

SHELL ["/bin/bash", "-c"]

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN pip install --upgrade pip

RUN apt update && apt -qy install gcc libjpeg-dev libxslt-dev \
    libpq-dev libmariadb-dev libmariadb-dev-compat gettext cron openssh-client flake8 locales vim

RUN useradd -rms /bin/bash webapp && chmod 777 /opt /run

WORKDIR /webapp

RUN mkdir /webapp/static && mkdir /webapp/media && chown -R webapp:webapp /webapp && chmod 755 /webapp
COPY --chown=webapp:webapp . .

RUN pip install -r requirements.txt

USER webapp

CMD ["gunicorn","-b","0.0.0.0:8000","webapp.wsgi:application"]
