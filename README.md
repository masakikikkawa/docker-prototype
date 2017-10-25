# docker-laravel prototype

#### ソースの取得
```
$ git clone git@github.com:masakikikkawa/docker-prototype.git

```

#### Dockerコンテナの構築
```
$ docker-compose build
$ docker-compose up -d
```

#### .envファイルの生成
```
# .envファイルはgitにないので自前で作成する
$ cp .env.example .env

```

#### .envファイルの修正
```
# dockerのappコンテナに入る
$ docker-compose exec app /bin/bash

# pingでmysqlコンテナのipを調べる
$ ping mysql
　PING mysql (172.23.0.3): 56 data bytes
　64 bytes from 172.23.0.3: icmp_seq=0 ttl=64 time=0.446 ms
　64 bytes from 172.23.0.3: icmp_seq=1 ttl=64 time=0.191 ms
　64 bytes from 172.23.0.3: icmp_seq=2 ttl=64 time=0.261 ms
　64 bytes from 172.23.0.3: icmp_seq=3 ttl=64 time=0.216 ms

# .envを編集
$ vi .env
DB_HOST=172.18.0.3   #pingで確認したipを記載
DB_DATABASE=prototype_db
DB_USERNAME=root
DB_PASSWORD=password

```

#### DBテーブル生成
```
$ php artisan migrate

```

#### 確認
```
ブラウザで
http://localhost

```

#### 新規登録まで動かす場合
```
# Gmailのアプリパスワードを事前に取得する
https://accounts.google.com/signin/v2/sl/pwd?service=accountsettings&passive=1209600&osid=1&continue=https%3A%2F%2Fmyaccount.google.com%2Fu%2F1%2Fapppasswords%3Frapt%3DAEjHL4OzV7VTuwnBlMudIZUyo0slMrteUt2pchXYUT2-sAg-bfLzpwmP77lQglDqLJSddcSM9ZjIvzJ5qvCGdG_zJkg2o-kW6A&followup=https%3A%2F%2Fmyaccount.google.com%2Fu%2F1%2Fapppasswords%3Frapt%3DAEjHL4OzV7VTuwnBlMudIZUyo0slMrteUt2pchXYUT2-sAg-bfLzpwmP77lQglDqLJSddcSM9ZjIvzJ5qvCGdG_zJkg2o-kW6A&rart=ANgoxccNaZQL5fsCzhtZR8SM_LJO9Fc31sXlwOi4LYyKCTHMJROqn9XYPKetgcgRo1dAgVma7AAATfybdu-Gsb2TTNW2NDjzeA&authuser=1&flowName=GlifWebSignIn&flowEntry=ServiceLogin  

# .envファイルの修正
MAIL_DRIVER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=*******@gmail.com
MAIL_PASSWORD=********
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=*******@gmail.com
MAIL_FROM_NAME=******

```