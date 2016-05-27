---
author: sasa+1
tags: javascript
title: TernでJavaScriptの入力補完をする
---
[Tern](http://ternjs.net/)で入力補完をすることにした。自分はVimを使用しているので[Tern for Vim](https://github.com/ternjs/tern_for_vim)を使う。

TernはJavaScriptで記述されていて、node.jsで動作するのでそれが必要になる。

ここではnode.js ver.6.2.0とnpm ver.3.8.9を使った。

---

npmからTernをインストールする。

```sh
$ npm install -g tern
```

---

`.vimrc`に以下のように記述してTern for Vimを読み込む。NeoBundleを使用しているのでNeoBundleLazyで読み込ませる。

```vim
NeoBundleLazy 'gh:marijnh/tern_for_vim.git', {
      \ 'disabled' : !has('python'),
      \ 'autoload' : {
      \   'filetypes' : 'javascript',
      \ },
      \ 'build' : 'npm install',
      \ }
```

入力補完がされるたびにプレビューウィンドウが表示されて煩わしいので非表示にする。

```vim
set completeopt-=preview
```

---

これでJavaScriptのコードを編集するときに入力補完がされるようになる。

[Tern Reference Manual](http://ternjs.net/doc/manual.html)を読むと`.tern-project`というファイルを作成することで補完に関する動作を設定できるようだ。
