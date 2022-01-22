# Docker Commands

「今だけこの環境がほしい」のニーズに応じる Docker コマンド集。

※ マウントしたいディレクトリでコマンドを実行する。

※ shell から出る場合は、 `exit` コマンドを使用する。

※ Alpine Linux を使用している理由: 軽量だから。

## オプションの説明

<https://docs.docker.jp/v19.03/engine/reference/commandline/run.html>

- `--rm`: 一連の処理のあとに自動的に実行中のコンテナを削除する。このオプションがある場合、`exit` コマンドで切断したタイミングでコンテナが削除される。
- `-it`: `-i` と `-t` をあわせたもの。コマンド入力を有効にする。（これがないと実行してもキーボードからコマンドが入力できない）
- `-v`: 外部ボリュームをマウントする。 （構文: `-v {MacやWSLのパス}:{コンテナ内のパス}`）
  "$PWD" を使用することで、実行時に `pwd` コマンドを実行し、現在のディレクトリをマウントすることができる。
- `-u`: コンテナ内で実行するユーザーの設定。 Mac はユーザーの権限を自動で調整してくれるので不要、というより、オプションを付けると自動変換が行われないため、付けてはいけない。 WSL（Linux）は自動変換がおこわなれない。Docker は初期設定で root ユーザーとして実行されてしまう。ボリュームをマウントする際に、ルートユーザーで実行後、コンテナ内からファイルを作成すると、WSL のディレクトリからは WSL のルートユーザーが作成したことになり、通常のユーザーがファイルを編集・削除できなくなる。そのため、`-u 1000` とすることで、一般ユーザーで実行する。1000 は Linux の初期ユーザーに割り当てられるユーザー ID であり、コンテナ内には 1000 のユーザーが唯一ある。（root は 0）
- `-w`: ワーキングディレクトリ。コンテナに入った際の初期パス。（構文 `-w {コンテナ内のパス}`）
- `-p`: ポート共有。（構文: `-p {MacやWSLのポート}:{コンテナ内のポート}`） 例: `-p 3001:3000` とすることで コンテナ内で 3000 ポートでサーバーを起動すると Mac や Windows では、 `http://localhost:3001` のようにアクセスできる。この例のようにポート番号を変換することもできるが、理由がない場合は大抵同じ番号（`-p 3000:3000`）で良い。また、ポートを複数開けたい場合は、 `-p 3000:3000 -p 8080:8080` のように繰り返して記述する。

## PHP

`php` コマンドが使える環境。

[Docker Image List](https://hub.docker.com/_/php?tab=tags&page=1&name=alpine)

```bash
# Mac
$ docker run --rm -it -v "$PWD":/app -w /app php:8.0.15-fpm-alpine sh

# WSL
$ docker run --rm -it -v "$PWD":/app -w /app -u 1000 php:8.0.15-fpm-alpine sh
```

## Laravel の初期ファイル作成

以下のコマンドの場合、実行すると、現在のディレクトリに、 `project1` というディレクトリが作成され、
その中に Laravel プロジェクトファイルが生成される。ディレクトリ名である `project1` を変更したい場合は、引数の最後を任意のディレクトリ名に変更する。

```bash
# Mac
$ docker run --rm -it -v "$PWD":/app composer create-project laravel/laravel project1

# WSL
$ docker run --rm -it -v "$PWD":/app -u 1000 composer create-project laravel/laravel project1
```

[補足] このイメージは、composer イメージである。Laravel の初期ファイルを生成する際には PHP 環境は不要ということである。

## Node.js

`node`、`npm` コマンドが使える環境。

[Docker Image List](https://hub.docker.com/_/node?tab=tags&page=1&name=alpine)

```bash
# Mac
$ docker run --rm -it -v "$PWD":/home/node/app -w /home/node/app node:16.13.2-alpine sh

# WSL
$ docker run --rm -it -v "$PWD":/home/node/app -w /home/node/app -u 1000 node:16.13.2-alpine sh
```

[Node.js Version List](https://nodejs.org/ja/download/releases/)

一般的には、LTS を使用する。

## Node.js ワンライナー

Laravel で `npm install` と `npm run dev` を実行し、js と css のビルドファイルを作成する必要がある場合に活用可能。

```bash
$ docker run --rm -it -v "$PWD":/home/node/app -w /home/node/app -u 1000 node:16.13.2-alpine /bin/sh -c "npm install && npm run dev"
```
