#最小限のDocker＋Laravel環境の構築

user docker
app webapp

#準備作業(コンテナの消去、イメージの消去)
docker ps -aq | xargs docker rm
docker images -aq | xargs docker rmi

#コンテナを立ち上げる(約3分)
docker-compose up -d

#コンテナに入る
docker-compose exec --user=docker app bash

nodejs&npm確認(optional))
node -v
npm -v

#laravelプロジェクトをクリエイト(約7分)
composer create-project laravel/laravel webapp --prefer-dist "5.8.*"

#コンテナを抜ける
exit

#webapp/config/app.phpを修正
'timezone' => 'Asia/Tokyo',

#webapp/.envを修正

DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=sample
DB_USERNAME=user
DB_PASSWORD=password

#Web server設定ファイル(docker/web/default.conf)を修正
root  /var/www/html/webapp/public;

#コンテナを再起動
docker-compose restart

#動作確認
http://localhost:8000/
LaravelStart画面が出ていれば成功

#再びコンテナに入る
docker-compose exec --user=docker app bash
cd webapp

#DB Migration
php artisan migrate
Migration table created successfully.となれば成功
