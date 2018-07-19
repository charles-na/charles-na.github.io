---
layout: post
title: nginx 파일 업로드 용량 제한 수정
description: "이미지 업로드를 하려는데 1M 이상의 이미지 파일이 업로드 되지 않아 애를 먹었다면 아래의 이 방법을 참고하기 바라니다."
modified: 2018-07-18
tags: [nginx upload size limit]
---

1M넘는 파일을 업로드 하려고 했는데, 응답이 없어서 애를 먹었다면 아래의 이 방법을 참고하기 바라니다.
nginx 의 업로드 용량에 관한 설정을 따로 해주지 않았다면, 디폴트는 1M 인것을 알게 되었습니다.


## AWS Elastic 환경
ebextension 폴더에 config 추가

    files:
      "/etc/nginx/conf.d/proxy.conf" :
        mode: "000755"
        owner: root
        group: root
        content: |
          client_max_body_size 10M;
    
    container_commands:
      01_reload_nginx:
        command: "sudo service nginx reload"

## 터미널 환경
아래 파일을 수정하면 됩니다

    /etc/nginx/nginx.conf

위 파일을 열고 server 탭에

    client_max_body_size [원하는 용량]
    
설정을 추가해줍니다.

저장 후 sudo service nginx reload 명령을 수행합니다. 