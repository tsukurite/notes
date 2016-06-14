---
author: sasa+1
tags: browser iframe
title: iframeのページ内リンクのブラウザ毎の挙動について
---
iframeで表示したページにページ内リンクがあり、iframeのサイズが十分に小さくスクロールバーが表示されているときはiframeの中がスクロールする。

一方、iframeのサイズが十分に大きくスクロールバーが表示されていないときはスクロールされない……と思っていたら、IE11ではiframeを表示している親のページがスクロールされてしまった。

以下で挙動を確認できる。

- [http://sasaplus1-prototype.github.io/hash-change-in-iframe/](http://sasaplus1-prototype.github.io/hash-change-in-iframe/)
