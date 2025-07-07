FROM node:lts-alpine

# vue-cliをインストール
RUN apk update && \
    apk add --no-cache npm && \
    npm install --location=global @vue/cli

WORKDIR /app

