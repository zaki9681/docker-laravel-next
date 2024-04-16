FROM php:8.2-fpm

RUN apt-get update 
# zlibはデータの圧縮に関するアルゴリズムをライブラリ化したもの
# vimをインストール
# MariaDBデータベースのクライアントアプリケーションである「mysql」を使えるように「mariadb-client」をインストール
# libzip-devはzip圧縮時に必要となるライブラリ(libzip は、zlib を使用する)
RUN apt-get install -y zlib1g-dev mariadb-client vim libzip-dev 
# docker-php-ext-installはPHPに標準で備わっている拡張パッケージのインストール＆有効化ができるコマンド
# PDO_MYSQL は、PHP から MySQL データベースへのアクセスを可能にするための PHP Data Objects (PDO) インターフェイス を実装したドライバ。

##ここからPHP拡張機能のインストール

RUN docker-php-ext-install \
    zip \ 
    pdo_mysql \
    bcmath \
# gdのインストール
&& apt-get install -y \
    libpng-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libwebp-dev \
&& docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp \
&& docker-php-ext-install -j$(nproc) gd 

# gitのインストール
RUN apt-get install -y git 
# xdebugのインストール
RUN pecl install xdebug 
RUN docker-php-ext-enable xdebug 
# nodeのインストール
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get update
RUN apt-get install -y nodejs
RUN apt-get update
# connection timed outにならないようにupdateを挟んでる
#RUN apt-get install -y npm


# Composerのインストール & パス通す
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

