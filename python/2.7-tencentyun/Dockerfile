FROM 2.7.18-slim AS builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN sed -i 's/deb.debian.org/mirrors.tencentyun.com/g' /etc/apt/sources.list \
    && sed -i 's/security.debian.org/mirrors.tencentyun.com/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -yq --no-install-recommends gettext git \
    && apt-get install -yq --no-install-recommends default-libmysqlclient-dev \
    && apt-get install -yq --no-install-recommends procps lsof \
    && python -m pip install --no-cache-dir --upgrade pip \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 8000

CMD ["python", "--version"]
