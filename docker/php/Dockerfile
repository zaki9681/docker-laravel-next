FROM php:8.1-fpm

# Laravelのvite用に解放
EXPOSE 5173

# RUN sed -i '/jessie-updates/d' /etc/apt/sources.list 
# RUNコマンドは、buildしたときに元となるdockerイメージに対して実行する処理を記述する。
# \（バックスラッシュ）を用いて、複数行に分けることが可能。
# パッケージ一覧を更新
RUN apt-get update \
    # zlibはデータの圧縮に関するアルゴリズムをライブラリ化したもの
    # vimをインストール
    # MariaDBデータベースのクライアントアプリケーションである「mysql」を使えるように「mariadb-client」をインストール
    # libzip-devはzip圧縮時に必要となるライブラリ(libzip は、zlib を使用する)
    && apt-get install -y \
        zlib1g-dev \
        mariadb-client \
        vim \
        libzip-dev \
    # docker-php-ext-installはPHPに標準で備わっている拡張パッケージのインストール＆有効化ができるコマンド
    # PDO_MYSQL は、PHP から MySQL データベースへのアクセスを可能にするための PHP Data Objects (PDO) インターフェイス を実装したドライバ。
    && docker-php-ext-install \
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
    && docker-php-ext-install -j$(nproc) gd \
    # gitのインストール
    && apt-get install -y git \
    # xdebugのインストール
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    # cronのインストール
    && apt-get install -y cron \
    # nodeのインストール
    && apt-get install -y nodejs npm && npm install n -g && n 18.9.0
    
# Composerのインストール & パス通す
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

