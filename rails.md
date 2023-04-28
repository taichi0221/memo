## 新規Railsプロジェクト作成
rails new [プロジェクト名] -d [データベース名]
## サーバー起動
rails s
## データベース作成
rails db:create
## マイグレーション
rails db:migrate
## モデル生成
rails g model [モデル名]
## コントローラー生成
rails g controller [コントローラー名]
## コンソール起動
rails c
## RSpecテスト実行
bundle exec rspec
## RSpecテスト実行 (特定のファイル)
bundle exec rspec [ファイルパス]
## RSpecテスト実行 (特定の行)
bundle exec rspec [ファイルパス]:[行番号]

# Pryコマンド集
## ブレークポイントを設定 (コードに挿入)
binding.pry
## Pryのセッションから抜ける
exit
## 変数やメソッドの情報を表示
ls
## オブジェクトのメソッドを表示
methods
## オブジェクトのインスタンス変数を表示
instance_variables
## オブジェクトの詳細情報を表示
show-doc [オブジェクト名]
## オブジェクトのソースコードを表示
show-source [オブジェクト名]
