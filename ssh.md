## 秘密鍵ファイルのパーミッションを変更（読み書きのみ）
chmod 600 ファイル名.pem
## 環境変数ファイルを編集（Nanoエディタ）
nano web-variables.env
## 環境変数ファイルから変数をエクスポート
export $(grep -v '^#' web-variables.env | xargs)
## Docker Composeで本番環境用のコンテナをビルド
docker-compose -f docker-compose.production.yml build
## Gitリポジトリからmainブランチをプル
git pull origin main
## カレントディレクトリの表示
pwd
## ディレクトリの移動
cd [ディレクトリ名]
## ディレクトリの作成
mkdir [ディレクトリ名]
## ファイルやディレクトリの一覧表示
ls
ls -l  # 詳細表示
ls -a  # 隠しファイルも表示
## ファイルのコピー
cp [元ファイル] [コピー先]
## ファイルの移動（リネームも兼ねる）
mv [元ファイル] [移動先]
## ファイルの削除
rm [ファイル名]
rm -r [ディレクトリ名]  # ディレクトリを再帰的に削除
## ファイルの内容を表示
cat [ファイル名]
## テキストファイルの編集（viエディタ）
vi [ファイル名]
## プロセスの一覧表示
ps
ps aux  # 詳細表示
## プロセスの終了
kill [プロセスID]
## システムの再起動
sudo reboot
## システムのシャットダウン
sudo shutdown -h now
## システムのアップデート
sudo yum update  # Amazon Linux, CentOS, RHEL
sudo apt update && sudo apt upgrade  # Ubuntu, Debian
## ソフトウェアのインストール
sudo yum install [パッケージ名]  # Amazon Linux, CentOS, RHEL
sudo apt install [パッケージ名]  # Ubuntu, Debian
