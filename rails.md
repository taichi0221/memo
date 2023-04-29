## 新規Railsプロジェクト作成
rails new [プロジェクト名] -d [データベース名]
## モデル生成
rails g model [モデル名]
## コントローラー生成
rails g controller [コントローラー名]
## routes.rb
Rails.application.routes.draw do
  devise_for :users
    root to: 'items#index'
    resources :items  do
      resources :buys, only: [:new, :create]
    end
end
## devise
gem 'devise'
bundle
rails g devise:install
rails g devise user
rails g devise:views
## マイグレーションファイル
t.string     :name,         null: false
t.text       :explanation,  null: false
t.references :user,         null: false, foreign_key: true
t.string     :category,     null: false, index: true
t.string     :email,        null: false, unique: true, index: true
-------------------------------------------------------------------
t.integer   数値     金額、回数
t.string    短文     ユーザー名、メールアドレス
t.text      長文     投稿文、説明文
t.boolean   真偽     はい・いいえ、合格・不合格
t.datetime  日時     イベント日時、更新日時
t.date      日付     生年月日、イベント日
t.float     浮動小数点 数値 重量、座標
t.decimal   精度の高い小数点 数値 金額、割合
t.references 外部キー 他のテーブルへの参照

## バリデーションオプション
null: false               # NULLを許可しない
default: ""               # デフォルト値を設定
unique: true              # 一意性を保証する
limit: 255                # 文字列の最大長を制限する
precision: 10, scale: 2   # 小数点以下の桁数を制限する (数値データのみ)
foreign_key: true           # 外部キー制約を適用する
index: true                 # インデックスを作成する　データの検索が高速化する

以下の点に注意して、適切なカラムにインデックスを適用することが重要。
1.検索やソートが頻繁に行われるカラムにインデックスを適用します。
2.外部キーとして使用されるカラムにインデックスを適用します。
3.データ量が多く、検索に時間がかかる可能性があるカラムにインデックスを適用します。
以下のような状況ではインデックスの適用を検討しないか、慎重に検討することが推奨。
1.頻繁にデータが追加・更新されるカラム
2.カラム内のデータの種類が非常に少ない場合（例：真偽値を持つカラム）
3.検索やソートがほとんど行われないカラム
## form_with
<%= form_with model: @question, url: questions_path ,local: true do |f| %>
  <div id ="after_submit" >
    <h2>プロフィール入力</h2>
    <%= f.label :language, 'プログラミング言語' %>
    <%= f.text_field :language, id: "language_input",class: "form-control", placeholder: "得意なプログラミング言語を入力してください" %>
    <%= f.label :framework, 'フレームワーク'%>
    <%= f.text_field :framework, id: "framework_input",class: "form-control", placeholder: "得意なフレームワークを入力してください" %>
    <%= f.label :hobby, '趣味' %>
    <%= f.text_field :hobby, id: "hobby_input", class: "form-control", placeholder: "趣味を入力してください" %> 
    <%= f.label :former_job ,'経験したお仕事（任意）'%>
    <%= f.text_field :former_job, class: "form-control", placeholder: "前職を入力してください" %> 
    <%= f.submit "聞く！", class: "btn btn-primary", id: "submit", style: "display:none;"%>
  </div>
<% end %>

form_with メソッドを使用してフォームを開始。
model: インスタンス変数 url: フォーム送信後のURL local: true Ajaxを無効にし、通常のHTTPリクエストを行う設定。
f.label と f.text_field 各入力フィールドのラベルとテキストフィールドを作成。
id, class, placeholder フォームの見た目や振る舞いをカスタマイズ。
f.submit フォームの送信ボタンを作成。

## link_to
<%= link_to "プロフィール入力", new_question_path, class: 'btn btn-outline-secondary', type: 'button' %>
link_to メソッドを使用
"プロフィール入力" テキストのリンクを作成。
new_question_path リンク先
class: 'btn btn-outline-secondary' CSSクラスを追加。この例では、btn と btn-outline-secondary の2つのクラスが適用され、Bootstrap のスタイルが適用されることで、ボタンの見た目が整えられます。
type: 'button' リンクがボタンとして機能することを明示的に示す目的で使用

## RSpecテスト
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
