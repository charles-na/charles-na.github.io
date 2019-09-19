---
layout: post
title: 자주 사용하는 Git 명령어
date: 2018-07-18 21:20:00 +0900
categories: blog
---

자주 사용되어 알아두면 좋은 Git 명령어

<!--more-->

## 소스 되돌리기
    $ git 되돌리기
    $ git reset HEAD {파일명} | 
    $ git checkout -- {파일명}

## 로그 보기
    $ git log -p -5 or {filename} # 파일내 코드 수정 내용
    $ git log --stat # 변경되어진 파일 리스트
    $ git show {commit-id}

## cached 파일삭제
    $ git rm -r --cached .
    $ git add .
    $ git commit -m "fixed"

## 수정된 파일들 커밋
    $ git add -u
    $ git commit -m "message"

## 로컬 untracked 파일/폴더 제거
    $ git clean -fd

## 특정 커밋 로그만 볼때
    $ git show [커밋아이디]

## 파일 존재하는 디렉토리 상태 커밋
    $ git init
    $ git remote add origin PATH/TO/REPO
    $ git add .
    $ git commit -m "add base" .
    $ git push --set-upstream origin master

## 수정 파일들 압축파일 묶기
    $ zip {modified-files.zip} $(git ls-files --modified)

## 브랜치 생성 및 푸시
    $ git branch {mypage}
    $ git checkout {mypage}
    $ git push --set-upstream origin {mypage}

## 서브모듈 Clone
    $ git clone --recurse-submodules https://github.com/chaconinc/MainProject

## 서브모듈 프로젝트를 Fetch 하고 업데이트
    $ git submodule update --remote

## 브랜치/태그 목록
    $ git show-branch

## Soucetree Fetch 마다  Password Required 나오는 경우
    $ git config credential.helper store
    $ git pull

## 서브모듈 자동 업데이트 설정
    $ git config --global submodule.recurse true