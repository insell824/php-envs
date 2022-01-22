# PHP with Apatche and MySQL

## 方法

<https://github.com/insell824/php-envs/tree/main/with-database> にある構成を真似てください。
`public` の中のファイルがホストされます。

## 手軽に試す方法

このリポジトリをクローンして実行します。

```bash
$ git clone git@github.com:insell824/php-envs.git sample1
$ cd sample1
$ cd with-database

# 開始
$ docker-compose up -d
```

- Web にアクセス: <http://localhost:8080/>
- データベース管理画面: <http://localhost:8081/>
  - データベースの種類: MySQL
  - サーバ: db:3306
  - ユーザ名: root
  - パスワード: password123456
  - データベース: db1
  - 永続的にログイン: はい

```bash
# 終了（データベースのデータは残ります）
$ docker-compose down
```
