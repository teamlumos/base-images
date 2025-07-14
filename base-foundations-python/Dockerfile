FROM python:3.10.6-slim-bullseye as base-foundations-python

RUN apt-get update && apt-get install --no-install-recommends -y \
    libpq-dev \
    python3-dev \
    build-essential \
    gcc \
    jq \
    curl \
    # Add runtime dependencies for PyICU https://pypi.org/project/PyICU/
    # ICU is used for transliteration support in Lumos Expression Language
    pkg-config \
    libicu-dev \
    # End ICU dependencies
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN ldconfig

# https://docs.python.org/3/using/cmdline.html#envvar-PYTHONUNBUFFERED
# Python env vars
ENV PYTHONUNBUFFERED=1 \
    # https://docs.python.org/3/using/cmdline.html#envvar-PYTHONDONTWRITEBYTECODE
    PYTHONDONTWRITEBYTECODE=1 \
    # Pip env vars (https://pip.pypa.io/en/stable/user_guide/#environment-variables)
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    PIP_REQUESTS_TIMEOUT=180 \
    # Poetry env vars (https://python-poetry.org/docs/configuration/#using-environment-variables)
    POETRY_VERSION=1.5.1 \
    POETRY_NO_INTERACTION=1

RUN \
    python3 -m pip install --no-cache-dir pip==22.3.1 \
    && pip install --no-cache-dir \
    setuptools==68.1.2 \
    virtualenv==20.23.1 \
    "poetry==$POETRY_VERSION" \
    && poetry config virtualenvs.create false
