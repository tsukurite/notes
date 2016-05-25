---
author: sasa+1
layout: slide
tags: bash terminal
title: ターミナルとシェル
---
<!-- class: middle, center -->

# ターミナルとシェル

あまり黒い画面を触らない人へ向けたスライド

---

<!-- class: middle, center -->

## ターミナル

---

## ターミナル

「**黒い画面**」を**表示**するためのもの

[VT100 - Wikipedia](https://ja.wikipedia.org/wiki/VT100)

端末をエミュレートするソフトウェアを仮想端末と呼ぶことも

[端末エミュレータ - Wikipedia](https://ja.wikipedia.org/wiki/%E7%AB%AF%E6%9C%AB%E3%82%A8%E3%83%9F%E3%83%A5%E3%83%AC%E3%83%BC%E3%82%BF)

---

## ターミナル

よく知られているターミナル

| Windows | Mac          | Linux |
| ------- | ------------ | ----- |
| ckw-mod | Terminal.app | xterm |
| mintty  | iTerm2       | rxvt  |

これら以外にも存在し、Linuxでは特に数が多い

[Windowsで使えるターミナルとシェルのまとめ - Qiita](http://qiita.com/Ted-HM/items/9a60f6fcf74bbd79a904)

---

<!-- class: middle, center -->

## シェル

---

## シェル

ユーザがコマンドを**実行**するためのもの

- [コマンドラインインタプリタ - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%97%E3%83%AA%E3%82%BF)
- [シェル - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%B7%E3%82%A7%E3%83%AB)
- [Unixシェル - Wikipedia](https://ja.wikipedia.org/wiki/Unix%E3%82%B7%E3%82%A7%E3%83%AB)

---

## シェル

よく知られているシェル

| Windows    | UNIX/Linux |
| ---------- | ---------- |
| PowerShell | bash       |
| NYAOS      | zsh        |

UNIXシェルは他にsh, ash, dash, ksh, tcsh, fishなど、

ターミナルと同様に数多く存在する

---

## シェル

なにができるかは、

[シェル - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%B7%E3%82%A7%E3%83%AB)の『シェルの機能』を参照のこと

---

## ターミナルとシェル

.center[まとめ]

| ターミナル                       | シェル                       |
| -------------------------------- | ---------------------------- |
| シェルの入力・出力を表示するもの | コマンドを実行するためのもの |

---

<!-- class: middle, center -->

## コマンド

Bashに関わるところも含んでいます

---

## コマンド

シェルから処理をさせたいときに実行する命令のこと

[コマンド - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89_(%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF)

ここではほとんどのLinuxディストリビューションで

使われている多機能シェルのBashを使うことを前提に進める

[Bash - Wikipedia](https://ja.wikipedia.org/wiki/Bash)

---

## コマンド

`ls`などのコマンドは環境(OS)によって

全く異なるものを使用していることがある

- [Shell builtin - Wikipedia](https://en.wikipedia.org/wiki/Shell_builtin)
- [GNU core utilities - Wikipedia](https://ja.wikipedia.org/wiki/GNU_Core_Utilities)
- [BusyBox - Wikipedia](https://ja.wikipedia.org/wiki/BusyBox)

---

## コマンド

コマンドの実行は`command arg1 arg2 ...`という形式で入力する

```sh
$ cd /path/to/dir
```

`C-x C-e`を入力することで複数行のコマンドを

テキストエディタから入力することもできる

`EDITOR`環境変数に指定されたテキストエディタが使用される

---

## コマンド

コマンドは環境変数`PATH`のディレクトリから検索される

```sh
$ export PATH=
```

と実行すると大半のコマンドを絶対パスで入力しないと

コマンドが実行できない

---

## コマンド

環境変数は`env`で表示することができる

```sh
$ env
```

変数名を把握している場合は`echo`で表示して確認することも多い

```sh
$ echo $PATH
```

---

## コマンド

`type`でコマンドがどこにあるかを調べることができる

```sh
$ type cc
cc is /usr/bin/cc
$ type cd
cd is a shell builtin
$ type ls
ls is aliased to `ls -G'
```

---

## コマンド

コマンドのヘルプを表示するには大抵

```sh
$ command -h
```

もしくは

```sh
$ command --help
```

で表示される

---

## コマンド

コマンドにマニュアルが存在すれば

```sh
$ man command
```

を実行することで詳細な情報を見ることができる

環境変数`MANPATH`のディレクトリからファイルを検索している

---

## コマンド

`;`で区切ることで複数のコマンドを同時に実行できる

```sh
cd ./path/to/dir; ls; cd -
```

`&&`で区切るとコマンドが成功した時のみ

後ろのコマンドを実行できる

```sh
cd ./path/to/dir && ls && cd -
```

---

## コマンド

`|`で出力を次のコマンドに渡すことができる

```sh
$ printf 'foobar'
foobar
$ printf 'foobar' | sed -e 's/foobar/hoge/'
hoge
```

---

## コマンド

`>`で出力をファイルに上書き保存することができる

```sh
$ printf 'foobar' > foobar.txt
```

`>>`とすると追記になり、対象のファイルに追加できる

```sh
$ printf 'foobar' >> foobar.txt
```

---

## コマンド

`<`で入力をファイルから受け取ることができる

```sh
$ vi - < foobar.txt
```

---

## コマンド

もっと詳しく知りたい場合は以下の書籍を読むと良い

- [詳解 シェルスクリプト - O'Reilly Japan](https://www.oreilly.co.jp/books/4873112672/)
- [入門 bash 第3版 - O'Reilly Japan](https://www.oreilly.co.jp/books/4873112540/)
- [bashクックブック - O'Reilly Japan](https://www.oreilly.co.jp/books/9784873113760/)

あるいは

```sh
$ man bash
```

や日本語で読みたい場合[JM Project](https://linuxjm.osdn.jp/)も有用

---

<!-- class: middle, center -->

## 終わり 
