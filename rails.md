## 新規Railsプロジェクト作成
rails new [プロジェクト名] -d [データベース名]
## モデル生成
rails g model [モデル名]
## コントローラー生成
rails g controller [コントローラー名]
## RSpecテスト実行
gem 'rspec-rails', '~> 4.0.0'
bundle
rails g rspec:install
--format documentation .rspecに追記テストコードの結果を可視化
rails g rspec:model user user部分はモデル名
bundle exec rspec spec/models/user_spec.rb user_spec.rbはファイル名
## factory_bot
gem 'factory_bot_rails'
bundle
spec/mkdir factories/mk users.rb users部分はモデル名s
FactoryBot.define do
  factory :user do
    nickname              {Faker::Name.initials(number: 2)}
    email                 {Faker::Internet.free_email}
    password              {Faker::Internet.password(min_length: 6)}
    password_confirmation {password}
  end
end
## faker
gem 'faker'
bundle

## Pryコマンド集
binding.pry
user.errors.full_messages user部分はmodel名に合わせる
exit
## オブジェクトのメソッドを表示
methods
## オブジェクトのインスタンス変数を表示
instance_variables
## オブジェクトの詳細情報を表示
show-doc [オブジェクト名]
## オブジェクトのソースコードを表示
show-source [オブジェクト名]
