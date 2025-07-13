# Docker上にVue.js開発環境を作る

## 【参考にした資料】

### Vue.jsとDockerで作るフロントエンド　Vue.jsを最速で理解する

https://qiita.com/Brutus/items/f5c380d4e5277f357043


## DockerFile

```Dockerfile
FROM node:lts-alpine

# vue-cliをインストール
RUN apk update && \
    apk add --no-cache npm && \
    npm install --location=global @vue/cli

WORKDIR /app

```



## docker-compose.yml

```yaml
version: '3'

services:
  vue-todo-list:
    build:
      context: "./"
      dockerfile: "Dockerfile"
    ports:
      - 8080:8080
    volumes:
      - ./app:/app
    tty: true        
    stdin_open: true
    environment:
      - NODE_ENV=development

```


<span style="color: #FF6666;">
CLI（コマンドラインインターフェース）でDockerを使う場合は、<b>`tty`</b>と<b>`stdin_open`</b>入れておかないと、コンテナが瞬時にダウンする。
</span>


(参考)　docker-composeのtty, stdin_open

https://qiita.com/s_i_engineer/items/9299e64062d5ba059d40

- tty
    - 仮想端末を配置するコマンド
    - docker run -it {container_name}の -i にあたる設定
    - シェルスクリプトの実行や対話型のCLIツールを使う場合、ttyを有効にすると端末が割り当てられるため、正常に動作するようになる。
    - 有効にすると、コンテナが実行されている間、常に仮想ターミナルがアタッチされる


- stdin_open
    - 標準入力（stdin）をオープン状態する。
    - これにより、ユーザーが標準入力を通じてコンテナに対話的に入力を送ることが可能になる
    - コンテナに接続してコマンドを入力したい場合や、対話的なシェルを利用する場合に有効



## buildとdockcer-compose upしたあとにやること


（参考資料） Docker上にVue.js開発環境を作る

https://qiita.com/taketakekaho/items/8e6d16f29ea198f24d61


```sh
$  docker exec -it docker-vue_hoge sh
(コンテナに入る)
# /app
# cd vue-hoge
# yarn serve
これでvueのサーバ起動となる
```