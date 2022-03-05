FROM node:16-bullseye

WORKDIR /app

RUN echo 'deb http://mirrors.tencentyun.com/debian/ bullseye main contrib non-free' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian/ bullseye-updates main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian/ bullseye-backports main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.tencentyun.com/debian-security bullseye-security main contrib non-free' >> /etc/apt/sources.list \
    && npm config set registry http://mirrors.cloud.tencent.com/npm/
