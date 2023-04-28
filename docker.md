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