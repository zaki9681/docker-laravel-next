react-dockerの環境構築編

workingディレクトリを作成します。
```
git clone https://github.com/ozkoharu/congenial-waddle.git

```

```
cd congenial-waddle/docker
```

```
mkdir src
```

```
cd src
```

```
git clone https://github.com/ozkoharu/animated-train.git
```

```
mv .\animated-train\ laravel
```

```
git clone https://github.com/ozkoharu/friendly-octo-tribble.git
```

```
mv .\friendly-octo-tribble\ react
```

```
cd ~/congenial-waddle
```

```
cp .env.example .env
```

```
DB_USER="任意の文字"
DB_PASSWORD="任意の文字"
DB_ROOT_PASSWORD="任意の文字"
```

を書いて保存してください。

```
docker-compose run -w /var/www --rm php composer install
```

```
docker-compose run -w /var/www --rm php npm install
```

```
docker-compose run -w /usr/src/app test_node npm install
```

```
docker-compose run -w /var/www --rm php cp .env.example .env
```

```
docker-compose run -w /var/www --rm php php artisan key:generate
```

```
docker-compose up -d
```

```
docker-compose up ps
```

nginx, php, mariadb, node, phpmyadminのコンテナが表示されていることを確認

http://localhostにアクセスして、Reactの画面が表示されていればＯＫ