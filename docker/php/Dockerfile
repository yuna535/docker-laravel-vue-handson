FROM php:7.4.1-fpm

# COPY php.ini
# PHPの設定ファイルをDockerコンテナ内にコピー
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

# Composer install
# マルチステージビルド
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

# install Node.js
# マルチステージビルド
COPY --from=node:10.22 /usr/local/bin /usr/local/bin
COPY --from=node:10.22 /usr/local/lib /usr/local/lib

# apt-getというパッケージ管理ツールを使用
# apt-getを更新後、PHP拡張モジュールをインストール
RUN apt-get update && \
    apt-get -y install \
    git \
    zip \
    unzip \
    vim \
    && docker-php-ext-install pdo_mysql bcmath

# コンテナに入った時の作業ディレクトリを指定
WORKDIR /var/www/html

# Composer：パッケージ管理ツールであり、Laravelをインストールするために必要
# npm：パッケージ管理ツールであり、Vue.jsをインストールするために必要