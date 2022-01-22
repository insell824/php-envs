# PHP with Apatche and MySQL (phpMyAdmin)

## 方法

<https://github.com/insell824/php-envs/tree/main/with-database-my> にある構成を真似てください。
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

```bash
# 終了（データベースのデータは残ります）
$ docker-compose down
```

`.env` にポート番号を指定すると任意の番号に変更できます。

```ini
PORT=3000
MY_ADMIN_PORT=3030
```
