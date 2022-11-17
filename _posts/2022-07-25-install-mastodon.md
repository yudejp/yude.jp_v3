---
layout: post
title: "Mastodon インスタンスを高速に作成する"
---

# 免責 / 注意 事項
* yude はこの記事の内容をあなたが実行した結果の責任を一切負うことができません。自己責任で行ってください。

# 必要なもの
* Cloudflare で管理されている独自ドメイン
* Docker, cloudflared がインストールされているマシン
    * cloudflared のインストール方法については、この記事の最後の方を参照してください。

# 手順
## 1. テンプレートの Git リポジトリをクローンします。
* yude が作成した人のぬくもりのあるテンプレート Git リポジトリをクローンします。
    ```bash
    $ git clone https://github.com/yude/docker-mastodon mastodon
    ```

## 2. Cloudflare に `cloudflared` からログインします。
* まず、不具合を防ぐために事前に Cloudflare のダッシュボードにログインしておきます。
* その後、以下のコマンドを実行すると、Cloudflare の認証ページへの URL が表示されます。
    * 若干処理が長いため、気長に待ってください。
    ```bash
    $ cloudflared login
    ```
* Cloudflare の認証ページでは、あなたが Mastodon を公開する予定のドメインを指定してください。

## 3. Cloudflare の設定を行います。
1. トンネルを定義します。
    ```bash
    $ cloudflared tunnel create mastodon
    ```
    * `mastodon` の部分は英数字で任意に設定できます。
2. ドメインとトンネルを紐付けます。
    ```bash
    $ cloudflared tunnel route dns mastodon mstdn.yude.jp
    ```
    * `mastodon` の部分はステップ 1 で定義したトンネル名を指定してください。
    * `mstdn.yude.jp` の部分は Mastodon を稼働させる予定のドメインを指定してください。 

## 4. Docker コンテナの設定を行います。
クローンしたリポジトリ内にある `docker-compose.yaml` を開き、必要な項目を設定していきます。

* サービス `cloudflared` の `command` の項にある `mastodon` の部分を、ステップ 4.1 で指定したトンネル名に変更してください。\
例のとおりに `mastodon` とした場合は、何もする必要はありません。

## 5. Mastodon の設定を行います。
1. まずは、設定ファイルのテンプレートをダウンロードします。
    ```bash
    $ wget -O .env.production https://raw.githubusercontent.com/mastodon/mastodon/main/.env.production.sample
    ```

2. `.env.production` を開き、必要な項目を設定していきます。
* まずは、設定に使用するコマンドを2つ示します。これらは、両方とも `docker-compose.yaml` が存在するディレクトリで実行してください。
    * コマンド1: `docker compose run --rm web bundle exec rake secret`
    * コマンド2: `docker compose run --rm web bundle exec rake mastodon:webpush:generate_vapid_key`

* 以下が `.env.production` 中の設定項目です。
    * `LOCAL_DOMAIN`: Mastodon を稼働させる予定のドメイン (例: `mstdn.yude.jp`)
    * `REDIS_HOST`: `redis` に変更してください。
    * `DB_HOST`: `db` に変更してください。
    * `ES_ENABLED`: 今回は `false` に変更してください。
    * `SECRET_KEY_BASE`: **コマンド1**を実行して得られた文字列を貼り付けてください。
    * `OTP_SECRET`: **コマンド1**を実行して得られた文字列を貼り付けてください。ただし、`SECRET_KEY_BASE` とは異なる文字列になるようにしてください。(2回生成コマンドを実行してください。)
    * `VAPID_PRIVATE_KEY` & `VAPID_PUBLIC_KEY`: **コマンド2**を実行して得られた文字列を貼り付けてください。コマンドを実行すると、そのまま貼り付けられる形式で結果を得られます。
    <hr>
    
    * 以下の設定項目には、SMTP サーバ (電子メールの送信を担当するサーバ) が必要です。なんらかの手段によって、これを用意してください。
    
        * `SMTP_SERVER`: SMTP サーバのアドレスを指定してください。
        * `SMTP_PORT`: SMTP サーバのポート番号を指定してください。
        * `SMTP_LOGIN`: SMTP サーバのユーザ ID を指定してください。
        * `SMTP_PASSWORD`: SMTP サーバのパスワードを指定してください。
        * `SMTP_FROM_ADDRESS`: サーバーの利用者から、Mastodon インスタンスからのメールに付属するメールアドレスをどのように見せたいかを指定してください。(例: `noreply@yude.jp`)
    
    <hr>
    
    * また、自分しか使用しない場合は、`.env.production` に以下を追記してください。
        ```
        SINGLE_USER_MODE=true
        ```

3. アセットファイルとデータベースを初期化します。
    ```bash
    $ docker compose run --rm web rails db:migrate
    $ docker compose run --rm web rails assets:precompile
    ```

## 6. 起動します。
```
$ docker compose up -d
```
* 起動後、あなたのアカウントをできるだけ早く作成してください。
* 起動したら、以下のコマンドであなたのアカウントを管理者に設定してください。
    ```bash
    $ docker exec -it $(docker compose ps -q web) bin/tootctl accounts modify your_name --role admin
    ```
    * `your_name` にはあなたのスクリーンネームを指定します。(例: `@your_name` と表示されているものを、`your_name` として指定します。)

# 参考: cloudflared をインストールする
* Debian の場合
    1. リポジトリを追加します。
        ```bash
        $ echo "deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/ buster main" | sudo tee /etc/apt/sources.list.d/cloudflare-main.list 
        ```
    2. 公開鍵を追加します。
        ```bash
        $ sudo curl https://pkg.cloudflare.com/cloudflare-main.gpg -o /usr/share/keyrings/cloudflare-main.gpg
        ```
    3. `cloudflared` をインストールします。
        ```bash
        $ sudo apt update; sudo apt -y install cloudflared
        ```
* その他のディストリビューションについては、[こちら](https://pkg.cloudflare.com/) を参照してください。