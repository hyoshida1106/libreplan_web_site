---
layout: post
title: "Windowsにインストール"
date: 2014-08-12 21:31:50 +0900
comments: true
categories: 導入編
---
LibrePlanの動作プラットフォームとしてはLinuxが指定されていますが，
Javaアプリである以上，Linux以外でも動作可能なはずです。

ということで，MacにつづいてWinodowsでも動作を確認してみました。
詳しい動作確認はしていませんが，開発環境としては十分使えそうです。

##プラットフォームについて

インストールに使用したのはWindows 7 64bitです。
32bitでは確認していませんが，おそらく問題ないでしょう。 

Windows 8については，ちょっと分かりません。

##動作環境について

Linux(Unix)が標準プラットフォームですから，一番手っ取り早いのは
cygwinなどUnixエミュレーション環境を使う方法だと思いますが，
他のWindowツールやJavaとの整合性を考えて，
今回はあえて標準的な環境で試してみることにしました。

###Java, git

この２つについては，インストール情報がたくさんありますので省略します。  
gitクライアントは，今回はmsysgitを使用しました。

msysgit → http://msysgit.github.io/

###Maven

Apacheのサイトから直接入手します。

maven → http://maven.apache.org/download.html


###Python

これも配布サイトから標準パッケージで入手します。 
こんなところは，Windowsはやっぱり便利ですね。

python → http://www.python.jp/download/

###docutils

easy_installを取得してインストールすることにしました。  
まずeasy_installのスクリプトファイルを取得します。

easy_install → https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py

pythonを使ってインストールします。

    > python ez_setup.py

pythonのインストールディレクトリにeasy_install.exeが取得されているはずですので，
それを使ってdouutilを取得します。

    > (python install dir)¥Scripts¥easy_install.exe docutils

###gettext

これも配布サイトから標準パッケージをもらいます。

gettext → http://gnuwin32.sourceforge.net/downlinks/gettext-bin-zip.php

###postgresql

これも標準パッケージで大丈夫です。
mysqlを使用する方は，以下の手順についてはこちらの説明を参考に読み換えてください。

postgresql → http://www.enterprisedb.com/products-services-training/pgdownload#windows

###make

これは他に適当なものがなかったので，minw32に頼ることにしました。こちらで取得できます。

make → http://gnuwin32.sourceforge.net/packages/make.htm

###cutycapt

Linux用のパッケージですが，Windowsバイナリもちゃんとありました。 取得してインストールしておきます。

cutypart → http://cutycapt.sourceforge.net/

##ソースの取得，インストール，実行

ツールが準備できてしまえば，後は同じです。

    > git clone http://github.com/Igalia/libreplan.git 
    > cd libreplan
    > mvn -DskipTests clean install

それが終わればJettyの起動です。

    > cd libreplan-webapp
    > mvm -DskipTests jetty:run

LibrePlanのURLである http://localhost:8080/libreplan-webapp/ をアクセスしてみてください。
