---
author: sasa+1
tags: git svn
title: git-svn
---
notes for [git-svn](https://git-scm.com/book/en/v1/Git-and-Other-Systems-Git-and-Subversion) ([ja](https://git-scm.com/book/ja/v1/Git%E3%81%A8%E3%81%9D%E3%81%AE%E4%BB%96%E3%81%AE%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%81%AE%E9%80%A3%E6%90%BA-Git-%E3%81%A8-Subversion))

## clone

```sh
$ git svn clone -rHEAD (svn repository uri)
```

if need username:

```sh
$ git svn clone -rHEAD --username (username) (svn repository uri)
```

## get ignores from svn

```sh
$ git svn show-ignore >> .git/info/exclude
```

or

```sh
$ git svn show-ignore >> `git rev-parse --show-toplevel`/.git/info/exclude
```

## set ignores to svn

```sh
$ cat <<'EOB' >> .svnignore
> npm-debug.log
> node_modules
> EOB
$ git svn propset svn:ignore -R -F .svnignore .
```

## push

```sh
$ git svn dcommit
```

## fetch

```sh
$ git svn fetch
```

## pull

```sh
$ git svn rebase
```

or

```sh
$ git svn fetch
$ git (merge or rebase) git-svn
```

## show commands and options

```sh
$ git svn
```
