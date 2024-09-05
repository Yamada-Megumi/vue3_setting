# はじめの手順 新ストール手順
## docker+vue手順メモ

### 事前準備

プロジェクト用にディレクトリを作成
└── frontend/
    ├── app/
    │   └── Dockerfile
    ├── compose.yaml

### Dockerfile

FROM node:lts-alpine

# vue-cliをインストール
RUN apk update && \
    apk add --no-cache npm && \
    npm install --location=global @vue/cli

WORKDIR /app

### compose.yaml
version: '3'

services:
  vue-app:
    build:
      context: "./frontend"
      dockerfile: "Dockerfile"
    ports:
      - 8080:8080
    volumes:
      - ./frontend/app:/app
    tty: true
    environment:
      - NODE_ENV=development


## docker立ち上げ
docker-compose up

### dokcer内にアクセス
このターミナルで追加のコマンドを走らせられないことに注意．別のターミナルを立ち上げ以下のコマンドでアクセスする必要がある

docker-compose exec vue-app sh

### 新規プロジェクト立ち上げ

vue create my-app


### 終了手順

cntl + c


#### shellのみ追加名でsh抜けます

exit

docker-compose stop
docker-compose down


-------
## vueバージョン確認

//　プロジェクトにインストールしているvueのバージョン

npm list vue

// グローバルにインストールしているvueのバージョン

npm list -g vue

------

# vueプロジェクト作成後　起動手順

## docker コンテナ起動

docker-compose up

## ターミナルで

docker-compose exec vue-app sh

ls
cd my-app
yarn serve
の手順で起動してサービスを利用できる

