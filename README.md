## アプリケーション名
kirokuya2
## アプリケーション内容
体重を記録し、それをカレンダーやグラフなどで分かりやすく表示させる
## URL
https://kirokuya2.herokuapp.com/
## テスト用アカウント
・Basic認証パスワード:2222
・Basic認証ID:admin
・メールアドレス:
・パスワード:
## 利用方法
## 体重記録
1.トップページからユーザー新規登録を行う。
2.体重を記録するボタンから、内容(日付、体重、体脂肪率、【コメント】)を入力し投稿する。
## カレンダーを見る
1.カレンダーを見るボタンから確認することができる。
2.記録した内容(日付、体重、体脂肪率、【コメント】)を確認することができる
## グラフを見る
1.グラフを見るボタンから確認することができる
2.記録した内容(体重、体脂肪率)を確認することができる

## アプリケーションを作成した背景
主に自分のために作成したものである。ダイエットを3日坊主で辞めてしまう課題があった。課題を分析した結果、ダイエットを継続するためのモチベーションが欠如することが原因と考えた。そこで体重や体脂肪率などの記録をカレンダーやグラフなど客観的に分かりやすく表示することで努力を実感することができ、それがモチベの向上に繋がるのではと考えた。(また対戦機能をつけることでさらにライバル意識が生まれ、モチベに繋がるのではと考えている)
## 洗い出した要件
https://docs.google.com/spreadsheets/d/1jhRGuThjbXWG-ASDfgFq5KreM78OzHrDdhq_7XWGYGs/edit#gid=982722306
## 実装した機能についての画像やGIFおよびその説明
https://gyazo.com/d17f016ca716e7774d2f6bd01887ccbb
URLを入力するとこの画面が出てくる。この画面では新規登録とログインをすることが可能である。
https://gyazo.com/7fd39cde87c1d45131361d431ab5e2eb
この画面は新規登録画面である。メールアドレス、パスワード、パスワード再入力、ユーザー名、性別、身長、体重、目標体重を全て入力することで登録することができる。
https://gyazo.com/0f5eeb7c9dc7644cddd95d7abcbbfaca
この画面はログイン画面である。新規登録画面で登録したメールアドレス、パスワードを入力することでログインすることが可能である。
https://gyazo.com/44bbf88f349d77a67380b95ac7383422
この画面はログインした後の画面である。この画面ではログインしたユーザーの体重記録に加え、カレンダー、グラフの確認をすることができる。
https://gyazo.com/1d0862e2c2c2410c09c562346aa9e24f
この画面は記録画面である。詳しくいうと体重、体脂肪率、日付の3つを全て入力することで登録することができる。
https://gyazo.com/acebc4e26678b934da9cecae30ef9a40
この画面はカレンダーの画面である。カレンダーの役割を果たしつつ、その日の体重、体脂肪率、また後々コメント機能を追加する予定である。
https://gyazo.com/ccdd29553156f087d9edd2395511df4d
この画面はグラフの画面である。今まで計測した体重や体脂肪率を折れ線グラフで表示する。(まだ完成していない)
## 実装予定の機能
コメント機能、対戦機能、目標体重の設定及びグラフの線の表示
## データベース設計
https://gyazo.com/b33406c40e272d1ca254033a7b9b4ab5
## 画面遷移図
https://gyazo.com/28dbd0c3736a9e5567bfaf3863356e0b
## 開発環境
・Ruby
・Ruby on Rails
・MySQL
・GitHub
・Heroku
・Visual Studio Code
## 工夫したポイント
私はこのアプリを作る理由として努力が目に見える形で表現できる形で表現されるようなものを自分の手で作りたいと考えたからである。そのため客観的に努力を感じれるように折れ線グラフを導入し、また全体的に内容をパッと見れるようためのカレンダー機能の実装、まだ実装は出来ていないがそこにカロリーや運動内容をメモることができるコメント機能を実装する予定することで更なる実感を得れるであろう。またモチベーションを維持するためにユーザー同士での対戦機能の実装やダイエットする人同士のコミュニケーションする場などを取り入れていきたいと考えている。



## usersテーブル

| name          | string  | option                    |
| ------------- | ------- | ------------------------- |
| nickname      | string  | null: false               |
| encrypted     | string  | null: false               |
| height        | float   | null: false               |
| email         | string  | null: false, unique: true |
| sex_id        | integer | null: false               |
| weight        | float   | null: false               |
| target_weight | float   | null: false               |

has_many :records
has_one :calender

## recordsテーブル

| name                | string    | option                         |
| ------------------- | --------- | ------------------------------ |
| weight              | float     | null: false                    |
| body fat percentage | float     | null: false                    |
| month               | integer   | null: false                    |
| date                | integer   | null: false                    |
| user                | reference | null: false, foreign_key: true |

belong_to :user
has_one :comments

## commentsテーブル

| name      | string    | option                         |
| --------- | --------- | ------------------------------ |
| comment   | text      |                                |
| user_id   | reference | null :false ,foreign_key :true |
| record_id | reference | null :false ,foreign_key :true |

belong_to :record