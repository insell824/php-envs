# PHP with Apache

Dockerfile を作成する。

`~/Dockerfile`

```Dockerfile
FROM php:8.1.2-apache
RUN apt-get update
RUN docker-php-ext-install pdo_mysql

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
```

コマンドを実行する。

```bash
$ docker pull php:8.1.2-apache
$ docker build -t my_php_apache .
$ docker run --rm --name phpenv1 -v "$PWD":/var/www/html -p 8080:80 my_php_apache
```

テストファイルを作成する。
`~/index.php`

```php
<?php
phpinfo();
```

URL にアクセス。
<http://localhost:8080/>
