---
author: sasa+1
tags: bash
title: コマンドに渡すオプションをファイルに記述する
---
`find`コマンドでファイルを検索するときに、特定のディレクトリを除外するなどの条件を追加していくとオプションが非常に長くなると思う。

```sh
$ find . -type d \( -name node_modules -or -name bower_components \) -prune -or -type f -name '*.js' -print
```

これをなんとか短くしたく、可能なら除外条件などはほぼ変更しないのでファイルに記述できないかと思い調べた。

---

[command line arguments from a file content - Stack Overflow](http://stackoverflow.com/questions/4227994/command-line-arguments-from-a-file-content)

コマンド置換で`cat`もしくは標準入力にファイルを渡せば可能なようだ。

オプションを書いたファイルを`.findrc`として用意する。

```
-type d
(
  -name node_modules
  -or
  -name bower_components
)
-prune
-or
```

`.findrc`をコマンド置換で渡す。

```sh
$ find . $(< .findrc) -type f -name '*.js' -print
```

これで検索条件をファイルに記述して`find`コマンドを短く書く事ができた。

これなら`find`以外のコマンドにも応用できると思う。
