---
layout: post
title: "OS Xにインストール"
date: 2014-08-12 21:15:25 +0900
comments: true
categories: 
---
LibrePlanはJavaで開発されていますから，
基本的にJavaが動作するプラットフォームならばインストール可能なはずです。

ならば，ということで，MacOS Xにインストールを試みました。
Macを選択したのは単に自分が使っているからです。
基本的にUnix系OSであれば，必要なツールさえ用意できれば，同じように動作すると思います。

##プラットフォームについて

プラットフォームは Mac OS X 10.9(Marverics)を使用しましたが，
ツールとJVMさえ揃えば，バージョンには影響されないでしょう。 
なお，MarvericsにはJava環境が入っていないので，Oracleのサイトから別途インストールします。

このあたりから → http://www.oracle.com/technetwork/java/javase/downloads/index.html

バージョンとしては，Java 7を選択しておいた方が無難だと思います。

##ツールのインストール

Linuxではaptやyumを使いますが，今回のmacではHomebrewを使用しました。

Homebrew → https://github.com/Homebrew/homebrew/wiki/Installation

Homebrewをインストールすると `brew` というコマンドが使用可能になりますので，
ターミナルを立ち上げて，必要なものを順次インストールしていきます。

###Maven2

    # brew install homebrew/versions/maven2

###PostgreSQL

    # brew install postgresql

Postgresqlをインストールすると，起動方法に関する説明が表示されると思います。
今回は次のようなメッセージがありましたので，これに沿ってpostgresqlを起動しておきます。

    To have launchd start postgresql at login:
    ln -sfv /usr/local/opt/postgresql/*.plist ‾/Library/LaunchAgents
    Then to load postgresql now:
    launchctl load ‾/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
    Or, if you don't want/need launchctl, you can just run:
    postgres -D /usr/local/var/postgres

Python, makeはOS Xに最初からあるので，インストールは不要です。

###Python Docutils

    # pip install docutils - gettext # brew install gettext
    # brew link

gettext CutyCaptはとりあえず省略しました。
機会があればインストールして，手順を追記します。
データベースの初期化操作はLinuxと同じです。

    # psql -d postgres
    CREATE DATABASE libreplandev;
    CREATE DATABASE libreplandevtest; CREATE USER libreplan WITH PASSWORD 'libreplan';
    GRANT ALL PRIVILEGES ON DATABASE libreplandev TO libreplan;
    GRANT ALL PRIVILEGES ON DATABASE libreplandevtest TO libreplan;

##ソースの取得，コンパイル，起動

ここまでできてしまえば，後はLinuxと違う部分はありません。
ソースを取得して，コンパイルします。

    $ git clone http://github.com/Igalia/libreplan.git $ cd libreplan/
    $ mvn -DskipTests clean install

正常に終了すれば，jettyを起動します。

    $ cd libreplan-webapp
    $ mvn jetty:run

これで http://localhost:8080/libreplan-webapp にアクセスすれば，
ログイン画面が拝めるはずです。


