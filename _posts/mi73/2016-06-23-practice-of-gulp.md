---
author: mi73
tags: gulp
title: gulpの課題
---
## 課題

下記のタスクが正常に動くようにgulpfileを記述せよ。

### works/gulp/top.jsに記述してください

| 実行するタスク       | タスク内容                                                                  |
|----------------------|-----------------------------------------------------------------------------|
| `top:sass`           | resource/scss/topからwebroot/cssに展開（圧縮）                              |
| `top:sass --d`       | resource/scss/topからwebroot/cssに展開（圧縮せず）                          |
| `top:jade`           | resource/jade/topからwebrootに展開（圧縮）                                  |
| `top:jade --d`       | resource/jade/topからwebrootに展開（圧縮せず）                              |
| `top:sassWatch`      | sass用のwatchタスク                                                         |
| `top:jadeWatch`      | jade用のwatchタスク                                                         |
| `top:imagemin`       | resource/img/topからwebroot/imgに展開 (gulp-imageminを)                     |
| `top:watch`          | top:sassWatchとtop:jadeWatchの複合タスク                                    |
| `top:build`          | top:sassとtop:jadeの複合タスク                                              |
| `top`                | top:watchとserverの複合タスク                                               |

### works/gulp/contentA.jsに記述してください

| 実行するタスク       | タスク内容                                                                  |
|----------------------|-----------------------------------------------------------------------------|
| `contentA:sass`      | resource/scss/contentAからwebroot/contentA/cssに展開（圧縮）                |
| `contentA:sass --d`  | resource/scss/contentAからwebroot/contentA/cssに展開（圧縮せず）            |
| `contentA:jade`      | resource/jade/contentAからwebroot/contentAに展開（圧縮）                    |
| `contentA:jade --d`  | resource/jade/contentAからwebroot/contentAに展開（圧縮せず）                |
| `contentA:sprite`    | sprite画像をresource/img/contentAに展開、scssをresource/scss/contentAに展開 |
| `contentA:sassWatch` | sass用のwatchタスク                                                         |
| `contentA:jadeWatch` | jade用のwatchタスク                                                         |
| `contentA:imagemin`  | resource/img/contentAからwebroot/contentA/imgに展開(gulp-imageminを)        |
| `contentA:watch`     | contentA:sassWatchとcontentA:jadeWatchの複合タスク                          |
| `contentA:build`     | contentA:spriteとcontentA:sassとcontentA:jadeの複合タスク使用               |
| `contentA`           | contentA:watchとserverの複合タスク                                          |

### works/gulpfile.jsに記述済

| 実行するタスク  | タスク内容                         |
|-----------------|------------------------------------|
| `server`        | ライブリロードサーバーを起動       |
| `serverReload`  | サーバーをリロードする             |
| `serverNoWatch` | ライブリロードしないサーバーを起動 |

# ディレクトリ構造

```
works
|
|--README.md - このページのテキスト
|
|--gulp
|  |--contentA.js
|  |--top.js
|--gulpfile.js
|
|--resource
|  |--img
|  |  |--contentA
|  |  |--top
|  |--jade
|  |  |--contentA
|  |  |--top
|  |--scss
|  |  |--contentA
|  |  |--top
|  |--sprite
|  |  |--contentA
|
|--webroot
|  |--contentA
|  |  |--css
|  |  |--img
|  |--css
|  |--img
```

## gulpfile.js

```js
/*--------------------------------------------------------
 modules
 --------------------------------------------------------*/
var gulp            = require('gulp');
var browserSync     = require('browser-sync');

require('./gulp/top');
require('./gulp/contentA');

// DEV SERVER
gulp.task('server', function() {

  browserSync.init({
    server: "./"
  });

  gulp.watch('./webroot/**/*.html', ['serverReload']);
  gulp.watch('./webroot/**/*.css', ['serverReload']);
  gulp.watch('./webroot/**/*.js', ['serverReload']);
});

gulp.task('serverReload', function() {
  browserSync.reload();
});

gulp.task('serverNoWatch', function() {
  browserSync.init({
    server: "./"
  });
});

gulp.task('default', ['server']);
```

## ヒント

[Browsersync](https://www.browsersync.io/)は

```sh
$ npm install browser-sync
```

でインストールできる。

### キーワード

`gulp-util`, `util.env.d`
