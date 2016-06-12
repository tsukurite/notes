---
author: sasa+1
tags: css postcss
title: postcss-importでCSSモジュールを取り込む
---
[postcss-import](https://github.com/postcss/postcss-import)でnpmからインストールしたCSSのモジュールをインポートできると知ったので試した。

---

まず[postcss](https://github.com/postcss/postcss)などのモジュールをインストールする。

同時に[normalize.css](https://necolas.github.io/normalize.css/)をインポートするモジュールとしてインストールする。

```sh
$ npm install postcss postcss-cli postcss-import normalize.css
```

---

次に`postcss.json`として設定ファイルを作成する。

```json
{
  "use": [
    "postcss-import"
  ],
  "input": "index.scss",
  "output": "index.css",
  "local-plugins": true
}
```

---

`index.scss`として以下のような内容のファイルを作成する。

```css
@import "normalize.css";
```

これで`index.scss`にnormalize.cssがインポートされてコンパイルされる。

---

コンパイルする。

```sh
$ ./node_modules/.bin/postcss --config postcss.json
```

コンパイルされたファイルを見ると、normalize.cssがインポートされていることがわかる。

```sh
$ head index.css
/*! normalize.css v4.1.1 | MIT License | github.com/necolas/normalize.css */

/**
 * 1. Change the default font family in all browsers (opinionated).
 * 2. Prevent adjustments of font size after orientation changes in IE and iOS.
 */

html {
  font-family: sans-serif; /* 1 */
  -ms-text-size-adjust: 100%; /* 2 */
```

---

normalize.cssの他に[animate.css](http://daneden.github.io/animate.css/)もインポートできたので、`package.json`の`main`にCSSが指定されていればどんなモジュールでもインポートできると思う。

CSSのモジュール別の管理にはとても良いと思った。
