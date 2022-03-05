FROM python:3.9-slim AS builder

WORKDIR /app

COPY requirements.txt .
# ADD requirements.txt /app/

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update \
    # MySQL
    && apt-get install -yq --no-install-recommends default-libmysqlclient-dev gcc \
    && apt-get install -yq --no-install-recommends gettext wait-for-it git \
    && python -m pip install --upgrade pip \
    && pip wheel --no-cache-dir --no-deps --wheel-dir /app/wheels -r requirements.txt 

# final stage
FROM python:3.9-slim

WORKDIR /data/work

COPY --from=builder /usr/bin/wait-for-it /usr/bin
COPY --from=builder /app/wheels /wheels
COPY --from=builder /app/requirements.txt /

# COPY docker-entrypoint.sh /usr/local/bin/

RUN apt-get update \
    && apt-get install -yq --no-install-recommends gettext \
    && apt-get install -yq --no-install-recommends default-libmysqlclient-dev \
    && apt-get install -yq --no-install-recommends procps lsof \
    && pip install --no-cache /wheels/* \
    && python -m pip install --no-cache-dir --upgrade pip \
    && rm -rf /var/lib/apt/lists/* \
    && sed -i 's/deb.debian.org/mirrors.tencentyun.com/g' /etc/apt/sources.list \
    && sed -i 's/security.debian.org/mirrors.tencentyun.com/g' /etc/apt/sources.list

# RUN ln -s /usr/local/bin/docker-entrypoint.sh /entrypoint.sh

# ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 8000

CMD ["python", "--version"]
