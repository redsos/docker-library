FROM node:16-slim AS base
WORKDIR /app

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true

COPY package.json yarn.lock ./
RUN yarn --frozen-lockfile

# node_modules
FROM node:16-slim AS node_modules
WORKDIR /modules

COPY --from=base /app ./
RUN yarn install --non-interactive --frozen-lockfile --production

# Production
FROM node:16-slim
WORKDIR /app

RUN apt-get update \
    && apt-get install -y chromium-driver fonts-freefont-ttf \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*


ENV NODE_ENV production
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true
ENV CHROMIUM_PATH /usr/bin/chromium

# Google & Adobe 免费字体 https://noto-website-2.storage.googleapis.com/pkgs/NotoSansCJKsc-hinted.zip
COPY fonts/*.otf /usr/share/fonts/

COPY package.json yarn.lock ./
COPY --from=node_modules /modules/node_modules ./node_modules
