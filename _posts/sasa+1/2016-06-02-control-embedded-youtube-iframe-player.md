---
author: sasa+1
tags: youtube
title: YouTube IFrame Player APIを埋め込まれたiframeに使う
---
[iframe 組み込みの YouTube Player API リファレンス](https://developers.google.com/youtube/iframe_api_reference)には、divタグにidを付与してそのidとパラメータをAPIに渡すことでプレーヤーを生成する、という風にサンプルコードが書いてあるので、この方法で使うことが多いと思う。

JavaScriptで生成することになるので、動画のID・高さ・幅などをデータとして持つことになると思うが、できればJavaScriptでデータを持ちたくない。`data-*`属性を使ってJavaScriptはその属性の値を取得する、という作りにすれば良いとは思うが、埋め込まれたiframeをそのまま使えないのかと思いリファレンスを読み進めたところ、iframeタグにも適用できると書いてあった。

[動画プレーヤーの読み込み](https://developers.google.com/youtube/iframe_api_reference#Loading_a_Video_Player)より：

> \<iframe\> タグを自分で書くと、YT.Player オブジェクトを作成するときに、\<iframe\> タグの属性または videoId パラメータおよびプレーヤー パラメータ（src URL で指定）として指定する、width および height の値を指定する必要がなくなります。

---

埋め込まれたiframeのインスタンスも取得できるということで、JavaScriptで`onStateChange`のイベント発生時にログを表示させようと試してみたところ、ログが表示されたり表示されなかったりと安定しなかった。

HTMLは以下のように書いていた。

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/OcTyKLgRhWc?wmode=transparent&enablejsapi=1" frameborder="0" allowfullscreen></iframe>
```

---

どうも挙動が安定しないのでリファレンスの`origin`に関する箇所を読んでいたら重要なことが書いてあった。

[パラメータ](https://developers.google.com/youtube/player_parameters#origin)より：

> このパラメータは IFrame API のセキュリティを強化します。埋め込み IFrame でのみ使用できます。IFrame API を使用している場合、つまり enablejsapi パラメータの値を 1 に設定している場合は、常に自分のドメインを origin パラメータ値として指定する必要があります。

とあるので、`enablejsapi=1`を指定する以外にも`origin`を指定する必要があるようだ。（`origin`以外のところに書いておいて欲しい）

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/OcTyKLgRhWc?wmode=transparent&enablejsapi=1&origin=http://sasaplus1-prototype.github.io" frameborder="0" allowfullscreen></iframe>
```

これでプレーヤーの挙動が安定するようになった。ソースコードは以下で参照できる。

- [sasaplus1-prototype/control-embedded-youtube-iframe-player](https://github.com/sasaplus1-prototype/control-embedded-youtube-iframe-player)

---

ドメインが決まっているなら`origin`を指定するのは苦ではないが、開発環境など環境が複数存在する場合に環境にあわせて書き換えるのは面倒だと思う。

また、それ以外のパラメータも細かく指定したい場合に`data-*`属性では煩雑になると思うので、思い切ってscriptタグの中にJSONを書いてみるというのも試してみた。

個人的には案外悪くないと思った。ソースコードは以下で参照できる。

- [sasaplus1-prototype/generate-youtube-iframe-player](https://github.com/sasaplus1-prototype/generate-youtube-iframe-player)
