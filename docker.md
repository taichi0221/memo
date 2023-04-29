# Docker Compose コマンド集
## 設定ファイルを元にコンテナのビルド・起動
docker-compose up -d
## コンテナの停止・削除
docker-compose down
## サービス一覧の表示
docker-compose ps
## コンテナのログを表示
docker-compose logs [サービス名]
## コンテナ内のコマンドを実行
docker-compose exec [サービス名] [コマンド]
## 本番環境用のDocker ComposeでRailsアプリケーションのproductionログをリアルタイム表示
docker-compose -f docker-compose.production.yml exec rails tail -f log/production.log
## Dockerコンテナにインタラクティブシェルで接続
docker exec -it コンテナID bash
## 本番環境用のDocker ComposeでRailsアプリケーションにsass-loader@10を追加
docker-compose -f docker-compose.production.yml exec rails yarn add sass-loader@10
## 本番環境用のDocker ComposeでRailsアプリケーションのWebpackを実行
docker-compose -f docker-compose.production.yml exec rails bin/webpack
## 本番環境用のDocker ComposeでRailsアプリケーションのアセットを事前コンパイル
docker-compose -f docker-compose.production.yml exec rails bundle exec rails assets:precompile

# Docker コマンド集
## イメージのビルド
docker build -t [イメージ名]:[タグ名] [Dockerfileがあるディレクトリ]
## イメージ一覧の表示
docker images
## イメージの削除
docker rmi [イメージ名]:[タグ名] or [イメージID]
## コンテナの作成と起動
docker run -d --name [コンテナ名] -p [ホスト側ポート]:[コンテナ側ポート] [イメージ名]:[タグ名]
## コンテナ一覧の表示 (稼働中)
docker ps
## コンテナ一覧の表示 (すべて)
docker ps -a
## コンテナの停止
docker stop [コンテナ名] or [コンテナID]
## コンテナの起動
docker start [コンテナ名] or [コンテナID]
## コンテナの削除
docker rm [コンテナ名] or [コンテナID]
## コンテナのログを表示
docker logs [コンテナ名] or [コンテナID]
## コンテナ内のコマンドを実行
docker exec -it [コンテナ名] or [コンテナID] [コマンド]
## コンテナ内にシェルで入る
docker exec -it [コンテナ名] or [コンテナID] /bin/bash or /bin/sh
## ボリューム一覧の表示
docker volume ls
## ボリュームの削除
docker volume rm [ボリューム名]
## ネットワーク一覧の表示
docker network ls
## ネットワークの削除
docker network rm [ネットワーク名]
## システム全体のリソース使用状況を表示
docker system df
## 未使用のイメージやコンテナ、ボリューム、ネットワークを削除
docker system prune
