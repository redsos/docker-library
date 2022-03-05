FROM python:3.9-slim AS builder

WORKDIR /app

COPY requirements.txt .
# ADD requirements.txt /app/

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN echo 'deb http://mirrors.tencentyun.com/debian/ bullseye main contrib non-free' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian/ bullseye-updates main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian/ bullseye-backports main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian-security bullseye-security main contrib non-free' >> /etc/apt/sources.list \
    && apt-get update \
    # MySQL
    && apt-get install -yq --no-install-recommends default-libmysqlclient-dev gcc \
    && apt-get install -yq --no-install-recommends gettext wait-for-it git \
    && python -m pip install --upgrade pip -i http://mirrors.tencentyun.com/pypi/simple --trusted-host mirrors.tencentyun.com \
    && pip wheel --no-cache-dir --no-deps --wheel-dir /app/wheels -r requirements.txt -i http://mirrors.tencentyun.com/pypi/simple --trusted-host mirrors.tencentyun.com

# final stage
FROM python:3.9-slim

WORKDIR /data/work

COPY --from=builder /usr/bin/wait-for-it /usr/bin
COPY --from=builder /app/wheels /wheels
COPY --from=builder /app/requirements.txt /

# COPY docker-entrypoint.sh /usr/local/bin/

RUN echo 'deb http://mirrors.tencentyun.com/debian/ bullseye main contrib non-free' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian/ bullseye-updates main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian/ bullseye-backports main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian-security bullseye-security main contrib non-free' >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -yq --no-install-recommends gettext \
    && apt-get install -yq --no-install-recommends default-libmysqlclient-dev \
    # 调试工具
    && apt-get install -yq --no-install-recommends procps lsof \
    && pip install --no-cache /wheels/* \
    && python -m pip install --no-cache-dir --upgrade pip -i http://mirrors.tencentyun.com/pypi/simple --trusted-host mirrors.tencentyun.com \
    && rm -rf /var/lib/apt/lists/*

# RUN ln -s /usr/local/bin/docker-entrypoint.sh /entrypoint.sh

# ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 8000

CMD ["python", "--version"]
