FROM python:3.10.6-slim-buster as base-foundations-python

# https://docs.python.org/3/using/cmdline.html#envvar-PYTHONUNBUFFERED
# Python env vars
ENV PYTHONUNBUFFERED=1 \
    # https://docs.python.org/3/using/cmdline.html#envvar-PYTHONDONTWRITEBYTECODE
    PYTHONDONTWRITEBYTECODE=1 \
    # Pip env vars (https://pip.pypa.io/en/stable/user_guide/#environment-variables)
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    # Poetry env vars (https://python-poetry.org/docs/configuration/#using-environment-variables)
    POETRY_VERSION=1.4.0  \
    POETRY_NO_INTERACTION=1

RUN pip install --no-cache-dir "poetry==$POETRY_VERSION"
RUN poetry config virtualenvs.create false

RUN apt-get update && apt-get install --no-install-recommends -y \
    libpq-dev \ 
    gcc \
    jq \ 
    curl
# RUN apt-get clean && apt-get autoclean && apt-get autoremove
