# notes

notes repository

## ノートの書き方

`_posts`ディレクトリ以下に`yyyy-mm-dd-title.md`という形式でファイル名を指定し、GitHub Flavored Markdown記法で文章を書きます。

例えば、`2015-12-24-christmas-eve.md`とした場合、記事は2015年12月24日に作成されたものとして扱われ、URIには`christmas-eve`が使用されます。

GitHub Flavored Markdown記法については以下を参考にしてください。

- [Basic writing and formatting syntax](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [Organizing information with tables](https://help.github.com/articles/organizing-information-with-tables/)
- [Creating and highlighting code blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/)
- [Autolinked references and URLs](https://help.github.com/articles/autolinked-references-and-urls/)

ファイルの配置場所は`_posts`ディレクトリ以下であれば直下であってもサブディレクトリ以下でも構いません。

公開せずに下書きとして見たい場合は`_posts`ディレクトリの代わりに`_drafts`ディレクトリ以下に配置します。

## メタデータの指定

ファイルの先頭にメタデータを書くことができます。メタデータは`---`で区切った中に書きます。

```
---
author: John Doe
tags: christmas event
title: Christmas Eve
---
# Christmas Eve

...
```

## スライドの書き方

レイアウトにデフォルトの`note`でなく`slide`を指定することでスライドとして表示することができます。

```
---
author: John Doe
layout: slide
tags: christmas event
title: Christmas Eve
---
```

ライブラリは[remark](http://remarkjs.com/)を使用しています。

また、同時に[mermaid](http://knsv.github.io/mermaid/)も使用しているのでフローチャートやダイアグラムを表示することができます。

```markdown
<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>
```

とすることで図を表示できます。

## ローカルマシンで確認する

Rubyと[github-pages](https://rubygems.org/gems/github-pages)というgemがインストールされていればローカルマシンで確認できます。

```sh
$ gem install github-pages
$ jekyll serve --drafts --watch
```

とすることでサーバを起動し、ファイルに変更があった場合にはリコンパイルを自動的に行います。

### rbenvとruby-buildがインストールされている場合

[rbenv](https://github.com/rbenv/rbenv)と[ruby-build](https://github.com/rbenv/ruby-build)がインストールされている場合は以下の通りにコマンドを実行するとローカルマシンで確認できるようになります。

```sh
$ rbenv install `cat .ruby-version`
$ gem install bundler rake
$ rake install
$ rake preview
```

1. `.ruby-version`に書かれたバージョンのRubyをインストールする
2. `Bundler`と`Rake`をインストールする
3. `github-pages`を`Bundler`でインストールする
4. サーバを起動する
