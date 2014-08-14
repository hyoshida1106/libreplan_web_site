---
layout: post
title: "開発環境のセットアップ"
date: 2014-08-13 16:46:49 +0900
comments: true
categories: 開発編
---
ソースを入手してビルドはできるようになりましたが，
このままでは公開されたソースもエディタなどで眺めるくらいのことしかできません。

ドキュメントの整理が今一つのLiblePlanですが，丹念に探すと，開発環境に関する資料も見つかります。
今回，これに沿ってIDEでのビルド環境を用意しました。

元資料はこちら → http://www.libreplan.org/howto-start-development-with-eclipse.html

IDEはポピュラーなEclipseを使用しています。  
以下の手順はWindowsで行いましたが，Eclipseが動作するプラットフォームならば基本的にはすべて同じはずです。

##Eclipseのインストール

"Java EE"版が必要です。以下のURLから使用するプラットフォーム用を取得してください。

Eclipse → http://www.eclipse.org/downloads/

Eclipseが起動したら，Mavenプラグイン(m2e)を追加します。  
Help > Install New Software から [Add...] を選択して，次のURLを指定してインストールします。

    http://download.eclipse.org/technology/m2e/releases

![develop_1](/images/develop_1.png)

インストールが完了したら，表示される指示に従って再起動します。

##プロジェクトのインポート

GitHubから取得したソースをインポートします。  
Importメニューから Maven > Existing Maven Project を選択してください。

![develop_2](/images/develop_2.png)

"Root Directory"に，取得したソースの位置を指定します。

![develop_3](/images/develop_3.png)

インポートを実行すれば，プロジェクトが３つ生成されています。  
ドキュメントの指示に従って，”libreplan”プロジェクトは閉じておきます。

##プロジェクトの設定

閉じた"libreplan"以外のプロジェクト"ganttzk", "libreplan-business", "libreplan-webapp" の３つに，
Mavenの設定を行います。

プロジェクトエクスプローラでプロジェクトを右クリックして「プロパティ」を表示して，
"Maven Profile"に次の値を設定してください。

    -userguide, -reports

![develop_4](/images/develop_4.png)

##実行設定

メニューから Run > Run Configuration... を選択します。  
"New Launch Configuration"で，次のように設定してください。

    Base Directory: "Browse Workspace..." -> libreplan-webapp
    Goals: jetty:stop jetty:run
    Profiles: -userguide,-reports
    "Update Snapshots"
    "Skip Tests"
    "Resolve Workspace artifacts"

![develop_5](/images/develop_5.png)

##起動

データベースの設定などは，インストール時と同じく設定しておきます。

http://localhost:8080/libreplan-webapp をブラウザで開くと，
ログインメニューが表示されるはずです。

