---
title: About jekyll-paginate
tags: [Jekyll, Website, Japanese]
style: fill
color: success
description: Jekyllでページ区切りをしたいときには
---

Source: [seahal.net](https://seahal.net/article/programming/2018/05/04/jekyll-paginate.html)

## 概要

Jekyllでつくったサイトも記事が増えて１ページで収まりきれないなー、って思ったそこのあなた！ jekyll-paginate-v2ってRuby Gemがありますよ、って話をしていこうと思う。

## やること

1. “Gemfile”に“gem ‘jekyll-paginate-v2’”を追記して“bundle install”を実行する。
2. “_config.yml”に以下のコードを挿入する。

```yml
plugins:
  - jekyll-paginate-v2
  
pagination:
  enabled: true
  per_page: 10
  sort_reverse: true
  sort_field: 'date'
```
3. ページ表示をしたいテンプレートファイルを編集する。自分の場合 index.html を以下のコードのように改変した。

```
---
layout: index
title: Home
pagination: 
  enabled: true
---

<div id="main">
  {% for post in paginator.posts %}
  <h1><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h1>
  <ul>
    <li>⏰ {{ post.date | date: '%F %H:%M' }} </li>
  </ul>

  {% endfor %}

  <div class="pagination">
    {% if paginator.previous_page == 1 %}
      <a href="../" class="previous">Previous</a>
    {% elsif paginator.previous_page %}
      <a href="/page{{ paginator.previous_page }}" class="previous">Previous</a>
    {% else %}
      <span class="previous">Previous</span>
    {% endif %}
      <span class="page_number ">Page: {{ paginator.page }} of {{ paginator.total_pages }}</span>
    {% if paginator.next_page %}
      <a href="/page{{ paginator.next_page }}" class="next">Next</a>
    {% else %}
      <span class="next ">Next</span>
    {% endif %}
  </div>
</div>
```
4. ビルドをおこない、確認する。
5. おしまい

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
