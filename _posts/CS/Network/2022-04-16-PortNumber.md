---
title: "MAC주소, IP주소, Port번호가 식별하는 것"

categories:
  - Network
tags:
  - [network, MAC, IP, PORT]

toc: true
toc_sticky: true
---

# Port Number의 이해

생성일: 2022년 4월 16일 오전 12:48

- Port Number

  - Process 식별자
    - 개발자의 입장에서는 Process가 무엇인지 알수 있는 식별자라고 알고 있자
  - Service 식별자
  - Interface 식별자

- Port Number 의 크기는 16bit이다

  - 0 ~ 65535 범위인데 0과 65535는 안쓴다
  - 2^16 - 2 라고 볼 수 있다

- Port Number는 소켓에 바인딩이 된다
