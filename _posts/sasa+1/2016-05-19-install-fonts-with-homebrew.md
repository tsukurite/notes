---
author: sasa+1
tags: font homebrew
title: Homebrewでフォントをインストールする
---
[Homebrew](http://brew.sh/)でフォントがインストールできることを知った。[Homebrew Cask](https://caskroom.github.io/)も使える必要があるはずなのでそれもインストールしておく。

---

以下のコマンドでリポジトリを取得する。

```sh
$ brew tap caskroom/fonts
```

あとはFormulaを指定してインストールする。

```sh
$ brew cask install font-migmix-1p
```

インストールしたフォントは`~/Library/Fonts`に配置される。

---

インストールできるフォントの一覧は以下のコマンドで表示できる。

```sh
$ brew cask search /^font-/
```
