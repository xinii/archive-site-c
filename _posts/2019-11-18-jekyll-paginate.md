---
title: About jekyll-paginate
tags: [Jekyll, Website, Japanese]
style: fill
color: warning
description: Jekyllでページ区切りをしたいときには
comments: true
---

Source: [seahal.net](https://seahal.net/article/programming/2018/05/04/jekyll-paginate.html)

## 概要

Jekyllでつくったサイトも記事が増えて１ページで収まりきれないなー、って思ったそこのあなた！ jekyll-paginate-v2ってRuby Gemがありますよ、って話をしていこうと思う。

## やること

- “Gemfile”に“gem ‘jekyll-paginate-v2’”を追記して“bundle install”を実行する。
- “_config.yml”に以下のコードを挿入する。

{% gist 70cc4adf649df5e8d03a7abffd715a9f jekyll-paginate-v2-config.yml %}

- ページ表示をしたいテンプレートファイルを編集する。自分の場合 index.html を以下のコードのように改変した。

{% gist 37ec2c22ec4ae735fcd2a122385d0189 pagination.erb %}

- ビルドをおこない、確認する。
- おしまい

## 気をつけること

- Jekyll のページネーションでは “page1” となるはずのページが作成されないので注意が必要である
- “Gemfile” や “config.yml” を変更しないといけないので敷居が高いかもしれない

## まとめ

以上がjekyll-paginate-v2を利用してJekyllでページ分割をする方法である。
もともとこの記事はjekyll-paginateという旧世代のRuby Gemを利用した内容となっていたのが，
高機能となったV2が出ていたので全面的に書き換えを実行することにした。
旧世代からのアップデートからは容易とはちょっといえないが、
それでも高機能になったので移行するのに二の足を踏んでいる方は
是非ともアップデートにトライしていただきたい。
