# docker-ssl-nginx-proxy
Make SSL using nginx-proxy with Docker

詳細な記事:
  [Docker環境で簡単にSSL化する方法を解説 【失敗しない初心者でもできる方法】](https://it-web-life.com/docker-ssl-nginx-proxy/)

## usage
本リポジトリを`git clone`します。
- `/development` はローカル開発環境用のコードです。SSLの認証局をローカルに設定しています。
- `/production` は本番用のコードです。SSLの認証局を`Let's Encrypt`に設定しています。`example.com`ドメイン部分などを摘便書き換えます。

### Dockerの起動
- cloneしたディレクトリに移動に移動します。ローカル開発なら`/development`以下、本番なら`/production`以下のコードを使います。

  #### Nginxのリバースプロキシを起動する
  - `nginx-proxy`起動
    - `shared`ディレクトリに移動します。
      - `docker-compose up -d nginx-proxy`コマンドを実行します。(`nginx-proxy`サービスを指定して起動)
        - ※`letsencrypt-nginx`も一緒に起動して問題ないですが今回は順番に見ていきます。

  #### WordPressコンテナを起動
  - `wordpress`ディレクトリに移動します。
  - `docker-compose up -d` を実行します。(`wordpress`,`mysql`サービスを起動)
  - WordPressが`localhost`で起動します。
  - `localhost`にアクセスするとWordPressのインストール画面が出るので、適当に設定を済ませて、WordPressが立ち上がる状態にします。

  #### SSL認証のコンテナを起動
  - `letsencrypt-nginx`起動
    - `shared`ディレクトリに移動します。
    - `$ docker-compose up -d letsencrypt-nginx` を実行します。(`letsencrypt-nginx`サービスを指定して起動)
