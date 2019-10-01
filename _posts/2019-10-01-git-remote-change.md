---
title: "Git Remote Repository Change!"
date: 2019-10-01
categories: git remote change 깃 리모트 변경
---
# Git Remote Repository Change

기존에 존재하는 `Repository`를 모두 최신화로 갱신해 준다.  
갱신이라는 것은 `Pull / Push` 모두를 처리하는 것을 말한다.

## Old `Repository` 최신화

```shell
$ git pull
$ git add .
$ git commit -m "clean push"
$ git push
```

## Old `Repository` Remote 제거

```shell
$ git remote remove origin
```

## New `Repository` Reomote 추가

```shell
$ git remote add origin ${신규 저장소 주소 : https://github.com/계정/리포지토리.git}
```
