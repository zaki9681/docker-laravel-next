# 環境構築

## docker desktopのインストール

本プロジェクトの環境構築ではdockerを使用しています。

以下のURLからDocker Desktopをインストールしてください。   
[Docker Desktop](https://www.docker.com/products/docker-desktop/)

## dockerファイルのclone
環境構築のためにまず、dockerファイルをgithubからcloneします。  
dockerプロジェクトを配置したいディレクトリ上で以下のコマンドを叩き
dockerファイルをcloneしてください。

```
git clone https://github.com/ozkoharu/congenial-waddle.git
```
congenial-waddle/docker 直下に srcディレクトリを作成してください。

## srcファイルのclone

congenial-waddle/docker/src上で以下のコマンドを実行

```
git clone https://github.com/ozkoharu/nextRoot.git
```
cloneが完了したら、「nextRoot」フォルダの名前を「next」に変更する。  
再度、congenial-waddle/docker/src上で以下のコマンドを実行


```
git clone https://github.com/ozkoharu/animated-train.git
```

cloneが完了したら、「animated-train」フォルダの名前を「laravel」に変更する。

## dockerコンテナ起動

### DB情報の設定

congenial-waddleディレクトリ上で以下のコマンドでdocker環境ファイルをコピーする。

```
cp .env.example .env
```

.envファイルの以下の項目を設定する。
* DB_NAME
* DB_USER
* DB_PASSWOR
* DB_ROOT_PASSWORD


### laravelの設定
congenial-waddleディレクトリ上で以下のコマンドを実行

```
docker compose run -w /var/www --rm test_laravel composer install
```

(内容:laravelプロジェクト上でcomposer install実行)

```
docker compose run -w /var/www --rm test_laravel npm install
```

```
docker compose run -w /usr/src/app --rm test_node npm install
```

(内容:laravelプロジェクト上でnpm install実行)

.envファイルコピー

```
docker compose run -w /var/www --rm test_laravel cp .env.example .env
```

アプリケーションキーを生成

```
docker compose run -w /var/www --rm test_laravel php artisan key:generate
```

コンテナサービスを起動

```
docker compose up -d
```

## 起動確認

以下のURLにアクセスし、起動確認を行う

* laravel : [laravelトップ](http://localhost:8000)

## Laravel DB設定

Laravelプロジェクトの.envファイルのDB設定を正しく修正する。
※以下の設定を行う。

```
DB_CONNECTION=mysql
DB_HOST= DockerのDBコンテナ名
DB_PORT=3306
DB_DATABASE=DB_NAMEに設定した値
DB_USERNAME=DB_USERに設定した値
DB_PASSWORD=DB_PASSWORDに設定した値
```

### 疎通確認
Laravelプロジェクト上で以下のコマンドを打ち、tinkerを起動する。

```
php artisan tinker
```

以下のSelcet文を打ってエラーが表示されなければ、接続成功

```
DB::select('select 1');
```
