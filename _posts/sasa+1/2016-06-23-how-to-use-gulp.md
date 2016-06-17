---
author: sasa+1
tags: gulp
layout: slide
title: はじめてのgulp
---
<!-- class: middle, center -->

# はじめてのgulp

---

## はじめてのgulp

[http://gulpjs.com/](http://gulpjs.com/)

> Automate and enhance your workflow

[https://github.com/gulpjs/gulp](https://github.com/gulpjs/gulp)

> The streaming build system

[Grunt](http://gruntjs.com/)とか[GNU Make](https://www.gnu.org/software/make/)とかそんな感じのもの

---
<!-- class: middle, center -->

# gulpを使うための準備

---

## gulpを使うための準備

gulpをインストール、実行するために必要なものは以下の2つ

- [node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/)

---

## gulpを使うための準備

ターミナルを開いて以下のように実行し、

バージョン番号が出力されればそれぞれ使用できる

```console
$ node --version
v6.2.0
$ npm --version
3.8.9
```

---

## gulpを使うための準備

以下のように表示されたら環境変数`PATH`を確認する

```console
$ node --version
-bash: node: command not found
```

---

## gulp-cliのインストール

gulp-cliをインストールして、

ターミナルから`gulp`コマンドを実行できるようにする

```console
$ npm install -g gulp-cli
```

- -g,--global
  - モジュールをグローバルにインストールする

---

## gulp-cliのインストール

以下の様に実行してバージョン番号が出力されれば

`gulp`コマンドが実行できる

```console
$ gulp --version
[00:00:00] CLI version 1.2.1
```

---
<!-- class: middle, center -->

# gulpタスクの作り方

---

## gulpタスクの作り方

gulpのタスクを作るには以下の2つの作業が必要

- gulpモジュールをインストールする
- `gulpfile.js`にタスクの内容を書く

---

## gulpタスクの作り方

適当なディレクトリを作り、移動する

```console
$ mkdir project
$ cd project
```

---

## gulpタスクの作り方

gulpモジュールをインストールする

```console
$ npm install gulp
```

---

## gulpタスクの作り方

`gulpfile.js`を作成し、以下のコードを書く

```js
'use strict';

var gulp = require('gulp');

gulp.task('hello', function() {
  console.log('Hello!');
});
```

`task`関数に渡している引数の意味は以下の通り

1. タスクの名前（ここでは`hello`という名前）
2. タスクの内容（ここでは`Hello!`と標準出力に出力する）

---

## gulpタスクを実行する

タスクの一覧を確認する

```console
$ gulp -T
[00:00:00] Using gulpfile /path/to/gulpfile.js
[00:00:00] Tasks for /path/to/gulpfile.js
[00:00:00] └── hello
```

---

## gulpタスクを実行する

作成したタスクを実行する

```console
$ gulp hello
[00:00:00] Using gulpfile /path/to/gulpfile.js
[00:00:00] Starting 'hello'...
Hello!
[00:00:00] Finished 'hello' after 111 μs
```

---
<!-- class: middle, center -->

# 実用的なタスクを作る

## Sassをコンパイルする

---

## Sassをコンパイルする

gulp-sassモジュールをインストールする

```console
$ npm install gulp-sass
```

Sassをコンパイルするモジュールとしては他に以下の2つがある

- [gulp-ruby-sass](https://github.com/sindresorhus/gulp-ruby-sass)
- [gulp-compass](https://github.com/appleboy/gulp-compass)

gulp-sassは[node-sass](https://github.com/sass/node-sass)を使用するのでRuby環境を作る必要がない

---

## Sassをコンパイルする

`gulpfile.js`に以下のコードを追記する

```js
var sass = require('gulp-sass');

gulp.task('sass', function() {
  return gulp.src('./sass/**/*.scss')
    .pipe(sass())
    .pipe(gulp.dest('./css'));
});
```

---

## Sassをコンパイルする

関数に書いたコードの意味は以下の通り

```js
gulp.task('sass', function() {
  // sassディレクトリ以下すべての*.scssを
  return gulp.src('./sass/**/*.scss')
    // gulp-sassでコンパイルして
    .pipe(sass())
    // cssディレクトリに出力する
    .pipe(gulp.dest('./css'));
});
```

---

## Sassをコンパイルする

タスクが追加されたか確認する

```console
$ gulp -T
[00:00:00] Tasks for /path/to/gulpfile.js
[00:00:00] ├── hello
[00:00:00] └── sass
```

---

## Sassをコンパイルする

`sass`ディレクトリにお好みでScssのテキストファイルを作る

```console
$ tree ./sass
./sass
├── aaa
│   └── aaa.scss
└── index.scss
```

---

## Sassをコンパイルする

タスクを実行してSassをコンパイルする

```console
$ gulp sass
[00:00:00] Using gulpfile /path/to/gulpfile.js
[00:00:00] Starting 'sass'...
[00:00:00] Finished 'sass' after 36 ms
```

---

## Sassをコンパイルする

ScssのファイルがコンパイルされてCSSのファイルが生成された

```console
$ tree ./css
./css
├── aaa
│   └── aaa.css
└── index.css
```

---

## Sassをコンパイルする

出力スタイルを`expanded`に変更したい場合

[node-sass#Options](https://github.com/sass/node-sass#options)を見ると`outputStyle`が指定できるので

以下のようにコードを修正する

```diff
   return gulp.src('./sass/**/*.scss')
-    .pipe(sass())
+    .pipe(sass({
+      outputStyle: 'expanded',
+    }))
     .pipe(gulp.dest('./css'));
```

---
<!-- class: middle, center -->

# コンパイルしたあと加工する

## プレフィックスの付加・コードの圧縮

---

## コンパイルしたあと加工する

さらにベンダープレフィックスの付加や圧縮なども

同時にしてしまいたい場合gulp-pleeeaseモジュールを

インストールする

```console
$ npm install gulp-pleeease
```

gulp-pleeeaseの代わりに以下のモジュールを使用してもよい

- [gulp-autoprefixer](https://github.com/sindresorhus/gulp-autoprefixer)
- [gulp-cssnano](https://github.com/ben-eb/gulp-cssnano)

---

## コンパイルしたあと加工する

gulp-pleeeaseを使用するため以下のコードを追記する

```diff
 var sass = require('gulp-sass');
+var pleeease = require('gulp-pleeease');
```

```diff
     .pipe(sass({
       outputStyle: 'expanded',
     }))
+    .pipe(pleeease())
     .pipe(gulp.dest('./css'));
```

これによりgulp-sassでSassがコンパイルされたあと

gulp-pleeeaseで圧縮などの処理がされファイルとして保存される

---

## コンパイルしたあと加工する

`sass/index.scss`に以下のコードを書く

```scss
div {
  animation: fadein 1s linear 0s;
}

@keyframes fadein {
  from { opacity: 0; }
  to { opacity: 1; }
}
```

---

## コンパイルしたあと加工する

タスクを実行してSassをコンパイルする

```console
$ gulp sass
[00:00:00] Using gulpfile /path/to/gulpfile.js
[00:00:00] Starting 'sass'...
[00:00:00] Finished 'sass' after 91 ms
```

コンパイルされた`css/index.css`を見ると以下のことがわかる

- 圧縮されている
- `-webkit-`が付加されたプロパティが追加されている
- `-ms-filter`を使ったプロパティが追加されている

---
<!-- class: middle, center -->

# CSS Spriteを作る

---

## CSS Spriteを作る

gulp.spritesmithモジュールをインストールする

```console
$ npm install gulp.spritesmith
```

---

## CSS Spriteを作る

gulp.spritesmithを使用するため以下のコードを追記する

```diff
 var pleeease = require('gulp-pleeease');
+var spritesmith = require('gulp.spritesmith');
```

```js
gulp.task('sprite', function() {
  return gulp.src('./image/**/*.png')
    .pipe(spritesmith({
      imgName: 'sprite.png',
      cssName: 'sprite.css',
    }))
    .pipe(gulp.dest('./sprite'));
});
```

---

## CSS Spriteを作る

タスクが追加されたか確認する

```console
$ gulp -T
[21:42:35] Tasks for /path/to/gulpfile.js
[21:42:35] ├── hello
[21:42:35] ├── sass
[21:42:35] └── sprite
```

---

## CSS Spriteを作る

`image`ディレクトリにお好みでPNGファイルを置く

```console
$ tree ./image
./image
├── icon1.png
├── icon2.png
└── icon3.png
```

---

## CSS Spriteを作る

タスクを実行してCSS Spriteを生成する

```console
[00:00:00] Using gulpfile /path/to/gulpfile.js
[00:00:00] Starting 'sprite'...
[00:00:00] Finished 'sprite' after 338 ms
```

---

## CSS Spriteを作る

複数の画像からCSS Spriteが生成された

```console
$ tree ./sprite
./sprite
├── sprite.css
└── sprite.png
```

---
<!-- class: middle, center -->

# その他、参考になりそうなリンク

---

## その他、参考になりそうなリンク

- [gulpjs.com](http://gulpjs.com/)
- [gulpjs.com/plugins](http://gulpjs.com/plugins/)


- [github.com/gulpjs](https://github.com/gulpjs)
- [qiita.com/tags/gulp](http://qiita.com/tags/gulp)


- [blackList.json](https://github.com/gulpjs/plugins/blob/master/src/blackList.json)

---
<!-- class: middle, center -->

# おわり
