FROM rust:1.58


COPY etc/.bashrc /root/.bashrc
COPY etc/.cargo/ /root/.cargo/

RUN echo 'deb http://mirrors.tencentyun.com/debian bullseye main' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian-security bullseye-security main' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian bullseye-updates main' >> /etc/apt/sources.list \
    && apt update \
    && apt -yq --no-install-recommends install clang \
    && rm -rf /var/lib/apt/lists/*
