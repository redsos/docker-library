FROM rust:1.61


COPY etc/.bashrc /root/.bashrc
COPY etc/.cargo/ /root/.cargo/


RUN apt update && apt -yq --no-install-recommends install clang \
    && sed -i 's/deb.debian.org/mirrors.tencentyun.com/g' /etc/apt/sources.list \
    && sed -i 's/security.debian.org/mirrors.tencentyun.com/g' /etc/apt/sources.list \
    && rm -rf /var/lib/apt/lists/*
