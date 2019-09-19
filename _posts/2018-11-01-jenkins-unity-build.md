---
layout: post
title: 맥 환경에서 Jenkins 설치
date:   2018-11-01 21:20:00 +0900
categories: blog
---

맥 환경에서 Jenkins 설치

<!--more-->

## Homebrew 설치 (없는 경우)
    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## 젠킨스 설치
    $ brew install jenkins

## 초기 비밀번호 세팅
    $ cat ~/.jenkins/secrets/initialAdminPassword
    1c6002e332504fe3b076dbe598834170

## 젠킨스 시작
    $ brew services start jenkins

## 젠킨스 삭제
    $ brew services stop jenkins
    $ brew remove jenkins

