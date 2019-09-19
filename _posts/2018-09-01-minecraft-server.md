---
layout: post
title: "마인크래프트 서버 구축"
description: "마인크래프트 JAVA Edition 서버 구축"
tags: [minecraft]
categories: [environment]
---

## 클라이언트 설치파일 다운로드
https://minecraft.net/ko-kr/download

## 서버 구동 파일 다운로드(jar)
https://minecraft.net/ko-kr/download/server

## 서버 실행
    $ java -Xmx1024M -Xms1024M -jar minecraft_server.1.13.1.jar nogui

## EULA 동의 처리
    open file in vim or Nano. Change false to true. Save file and reload