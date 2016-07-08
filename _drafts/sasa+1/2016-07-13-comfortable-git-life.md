---
author: sasa+1
tags: git
layout: slide
title: 快適Git生活
---
<!-- class: middle, center -->

# 快適Git生活

---

#### 快適Git生活

このスライドは

```sh
$ history | grep git
```

を実行して表示されたコマンドを元に構成されています

その他、Gitと言われて思いついたコマンドなど

そのへんの話をテキトーにします

---

#### shallow clone

時間が無いときに大きいリポジトリをcloneするのはつらいので

リポジトリを小さく取得します(shallow clone)

```sh
$ git clone --depth 1 [repository]
```

`--depth 1`で最新のコミットだけのリポジトリがcloneできます

---

#### shallow clone

時間に余裕ができたら履歴をすべて取得して

普通のリポジトリに戻しましょう

```sh
$ git fetch --unshallow
```

[開発コラボレーションのヒント from Atlassian Blogs](http://news.mynavi.jp/column/atlassian/019/)より：

> かつての Shallow clone は、いくつかの機能のサポートがほとんどなく、git の世界の問題児とでも言えるものでした。しかし、最近のバージョン (1.9 以降) において状況は大きく改善されており、現在では shallow clone からでもリポジトリへの pull や push を正しく行うことができます。

---

#### add patch

ファイルの指定した箇所だけコミットしたいとき

```diff
+000
 111
 222
+333
```

上記の`333`の行だけステージングしたいとき

```sh
$ git add -p file
```

あとは好きなハンク（修正のかたまり）を選びましょう

---

#### commit

過去に`add`した事があるファイルを変更して、

`git add`するのが面倒なとき

```sh
$ git ci -am "コミットメッセージ"
```

`ci`は`commit -v`のエイリアス

---

#### commit

直前のコミットのメッセージを変えたいとき

```sh
$ git commit --amend -m "新しいコミットメッセージ"
```

直前のコミットにファイルを追加し忘れたとき

```sh
$ git add file
$ git amend
```

`amend`は`commit --amend --reuse-message=HEAD`のエイリアス

---

#### status

```sh
$ git st
```

`st`は`status --branch --short`のエイリアス

変更したファイルを確認する

---

#### checkout

ブランチを切ってチェックアウトも同時にするとき

```sh
$ git co -b branch
```

`co`は`checkout`のエイリアス

---

#### checkout

ファイルを編集したけど修正する前(HEAD)に戻したい

```sh
$ git co -- file
```

ファイルを特定のコミットのものにしたい

```sh
$ git co [hash] -- file
```

---

#### branch

とにかくブランチを消す

```sh
$ git branch -D branch
```

ブランチ一覧を見る

```sh
$ git branches
```

`branches`は`branch -a`のエイリアス

たぶんMercurialから移行するときに作ったもの

---

#### cherry-pick

指定したコミットを取ってくる

```sh
$ git cp [hash]
```

`cp`は`cherry-pick`のエイリアス

指定したコミットの変更点を適用してコミットしない

```sh
$ git cp -n [hash]
```

---

#### reflog

```sh
$ git reflog
```

ご存知`reset --hard`に失敗したときなどに使う

---

#### diff

```sh
$ git di
```

`di`, `dif`は`diff`のエイリアス

```sh
$ git sdi
```

コミットする前に変更点を確認する

`sdi`, `sdif`は`diff --staged`のエイリアス

---

#### log

```sh
$ git sl
```

`sl`は`log --all --branches --decorate --graph --oneline`

のエイリアス

コミットグラフがどういった風になっているか確認する

```sh
$ git gl
```

`gl`は`log --all --branches --graph`のエイリアス

---

#### remote

```sh
$ git remote -v
```

リモートの名前とURLの確認

---

#### fetch

```sh
$ git fetch --all
```

すべてのリモートから変更点を取得する

---

#### pull

```sh
$ git pull --rebase
```

`--rebase`でfetchとmergeでなくfetchとrebaseにする

---

#### stash

変更した箇所をとりあえず避けておきたい

```sh
$ git stash
```

追加していないファイルも含めたいときは`save -u`で

```sh
$ git stash pop
```

避けておいたのを戻す

```sh
$ git stash clear
```

避けたけど必要なくなったので削除する

---

#### unstage

```sh
$ git unstage file
```

`unstage`は`reset HEAD --`のエイリアス

ファイルをステージングから取り除く

---

#### rev-parse

```sh
$ git rev-parse --git-dir
```

リポジトリの`.git`ディレクトリをフルパスで出力

```sh
git rev-parse --show-toplevel
```

リポジトリのルートディレクトリをフルパスで出力

---

#### merge

```sh
$ git merge --no-ff
```

明示的にfast-forwardしないマージをする

```sh
$ git merge --ff-only
```

明示的にfast-forwardするマージをする

---

#### reset

```sh
$ git reset --hard ORIG_HEAD
```

マージに失敗したときに

---

#### fixup

```sh
$ git fixup [hash]
```

`fixup`は`commit --fixup`のエイリアス

これからするコミットを指定したコミットに

`rebase -i`でまとめたいときに（`rebase.autosquash`を`true`にする）

---

#### rebase

```sh
$ git rebase [branch]
```

今のブランチを指定したブランチから派生したことにする

```sh
$ git rebase -i [hash]
```

歴史改変たのしい

---

#### package

自分で作ったサブコマンド

[git-package](https://github.com/tsukurite/git-package)

自分が今日更新したファイルだけを階層はそのままにコピーする

```sh
$ git package --date=local --since=midnight --author=sasaplus1
```

`log`にオプションをそのまま渡しているので

`log`で使えるオプションはすべて使用可能

---

#### git-svn

とにかくSubversionがつらいのでGitリポジトリとして扱う

```sh
$ git svn clone -rHEAD [repository]
```

```sh
$ git svn [rebase/fetch]
```

```sh
$ git svn dcommit
```

とてもよいのでSubversionで困っているのなら是非

---
<!-- class: middle, center -->

# Git以外の便利コマンド

---

#### vcprompt

[vcprompt](https://bitbucket.org/gward/vcprompt)

リポジトリの各種情報を出力するコマンド

```sh
$ vcprompt -f '(%n:%b:%r)'
(git:master:000000000000)
```

という風に出力されるので環境変数`PS1`に入れておくと

プロンプトに自動的にリポジトリ情報が表示されてとても便利

```sh
$ export PS1='$(vcprompt -f "%n:%b:%r") $ '
git:master:000000000000 $ 
git:master:000000000000 $ 
git:master:000000000000 $ 
```

---

#### tig

[tig](http://jonas.nitro.dk/tig/)

Gitブラウザ

---

#### ghq

[ghq](https://github.com/motemen/ghq)

Gitリポジトリ管理ツール

```sh
$ ghq get -p tsukurite/notes
```

で`$HOME/.ghq/github.com/tsukurite/notes`にcloneしてくれる

```sh
$ ghq look tsukurite/notes
```

でカレントディレクトリの移動も簡単にできる

---

#### ghs

[ghs](https://github.com/sona-tar/ghs)

GitHubリポジトリ検索ツール

```sh
$ ghs -u tsukurite | awk '{ print $1 }' | xargs -n1 ghq get
```

といった使い方などに便利

---
<!-- class: middle, center -->

# 入門に良さそうな資料など

---

#### 入門に良さそうな資料など

- https://git-scm.com/book/ja/v1
- https://git-scm.com/book/ja/v2


- http://www.backlog.jp/git-guide/
- http://www.backlog.jp/git-guide/reference/


- https://github.com/jlord/git-it
- https://github.com/jlord/git-it-electron

---
<!-- class: middle, center -->

# おわり
