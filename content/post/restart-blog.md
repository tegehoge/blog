---
date: 2020-12-09T18:12:26+09:00
description: "Hugo + Netlify で爆速構築"
featured_image: "/images/waiwai.jpg"
tags: ["近況", "技術"]
title: "てげほげブログを再開しました！（Hugo + Netlify で爆速構築）"
---

こんにちは！  
てげほげのともえです。

以前存在していたてげほげブログ、いつの間にか消えてしまっていたことをご存知だったでしょうか・・・？  
~~実はサーバーごとお亡くなりに~~諸般の事情により、新しい形で再開することになりました。

改めて、「Web ナイト宮崎」の告知やレポート・近況報告などを載せていこうと思っていますので、よろしくお願いいたします！

このブログの仕組みですが、メンバー同士で話し合ったところ「Hugo + Netlify + GitHub でやったら簡単そう＆楽しそう！」ということになったので、構築してみました🙌

せっかくなので、第１回目のこの記事は、このブログの構築方法の紹介としたいと思います。  
めっちゃ簡単で爆速（調べ物入れても 1.5h ぐらい）公開できました！

以下が全体の流れです。

- [1. Homebrew で Mac に hugo をインストール](#1-homebrew-で-mac-に-hugo-をインストール)
- [2. Hugo のプロジェクトを作る](#2-hugo-のプロジェクトを作る)
  - [テーマを追加](#テーマを追加)
  - [とりあえずデモサイトを構築](#とりあえずデモサイトを構築)
  - [.gitignore](#gitignore)
  - [ドメイン設定](#ドメイン設定)
  - [Netlify の設定を追加](#netlify-の設定を追加)
  - [コンテンツをよしなに編集](#コンテンツをよしなに編集)
- [3. Netlify に登録](#3-netlify-に登録)
- [4. GitHub に push](#4-github-に-push)

## 1. Homebrew で Mac に hugo をインストール

```shell
brew install hugo
```

## 2. Hugo のプロジェクトを作る

```shell
hugo new site tegehoge-blog
```

### テーマを追加

みんなで選んだ「ananke」テーマを追加します。  
テーマは submodule で追加することもできますが、
もしかしたら細かい style を触りたくなるかもしれないと思ってコードをダウンロードしてきました。  
テーマのライセンスを読んで問題ないか確認してください。（このテーマは MIT でした）

```shell
cd themes
git clone git@github.com:theNewDynamic/gohugo-theme-ananke.git
cd gohugo-theme-ananke
rm -rf .git
```

### とりあえずデモサイトを構築

まずは、テーマの中に含まれているデモサイトをそのまま表示してみます。  
予めプロジェクト直下に戻っておきます。

```shell
rm config.toml
cp themes/gohugo-theme-ananke/exampleSite/config.toml \
 themes/gohugo-theme-ananke/exampleSite/content \
 themes/gohugo-theme-ananke/exampleSite/static ./ # 上書きしていいか聞かれるので y で答えます
```

ここまできたらいったんローカルで動作確認してみます。

```shell
hugo server
```

ブラウザで http://localhost:1313/ にアクセスすると、デモページと同じ内容が確認できました。

### .gitignore

とりあえず以下のような感じで .gitignore を作っておきます。  
（他に入れたほうがいいものがあれば教えてください）

```
.DS_Store
public
/resources/_gen/
```

### ドメイン設定

ドメインを config.toml に設定しておきます。  
Netlify の URL でそのまま公開する場合は、この後発行される URL を設定します。

```config.toml
#baseURL = "https://zen-varahamihira-53ea57.netlify.app/"
baseURL = "https://tege.work/"
```

### Netlify の設定を追加

[ここ](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/#configure-hugo-version-in-netlify) に設定のサンプルがあるので、プロジェクト直下に `netlify.toml` として保存しておきます。

### コンテンツをよしなに編集

ここまでではデモサイトそのままなので、_index.md や about.md 、 contents 以下の記事などを実際に公開したい情報に置き換えて行きましょう。

## 3. Netlify に登録

先にGitHub に今回のプロジェクトを push する リポジトリを作っておきます。  
次にNetlify にアカウント登録＆アプリケーション登録をします。  
https://app.netlify.com/

以下に詳しい手順が書いてありました。  
https://gohugo.io/hosting-and-deployment/hosting-on-netlify/

ドメインの設定などもここで行います。（別途 DNS の設定が必要）

## 4. GitHub に push

あとは master にプッシュすれば自動でデプロイされます！

```
git add .
git push origin master
```

簡単にブログが公開できました〜！  
実はこの後、細々としたスタイルの修正に少し時間がかかっているのだけど、それはまた別のお話・・・
