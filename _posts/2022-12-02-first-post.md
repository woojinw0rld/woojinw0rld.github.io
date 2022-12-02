---
title: 전산 언어II 프로젝트 및 발표
layout: post
post-image: /cpp_fitness.jpg
description: 이번에 구현해본 전산언어 프로젝트에 대해. 이 프로젝트는 구조체와 메모리 동적할당, 파일 입출력등의 기능등을 사용하였다. 
tags:
- 전산 언어 II
- cpp
- 프로젝트
---

# 전산언어 II 
## 피트니스 회원관리 프로그램



<br>

- 구현한 주요 기능
  1. 회원등록
  2. 등록된 회원 조회
  3. 생일 회원 조회 
  4. 회원 정보 출력 
  5. 회원 탈퇴 
  6. 파일 입출력
  7. 종료
<br><br>

[//]: # (|제목|내용| 비고  |)
[//]: # (|---|----|-----| )
[//]: # (|송우진|21살| 인제대 |)

- 간단한 코드 소개 cpp 
  - 구조체 정의
  - 메인 함수
  - 주요 기능 함수
<br><br>
- 결론 
  1. 아쉬웠던 점.
  2. 느낀 점.


#### 본론으로 들어가기전 피트니스 회원 관리 프로그램에는 총 6개의 주요 기능이 있다. 각각 별도의 함수로 구현을 하였다. visual studio 2022버전을 사용하였다.
# 본론

 
>1번째 기능 회원 등록.

<br>
회원 등록을 한다면 먼저 회원의 락커룸(회원코드)를 등록한다. 등록 후 회원의 정보인 성함, 전화 번호, 주소 마지막으로 생년월일을 등록한다.
총 등록할 수 있는 회원의 수는 50명이다. 회원의 정보는 모두 구조체에 저장한다.  그리고 만약 락커룸(회원 코드)에 먼저 등록된 회원이 있다면 더 이상 등록이 되지 않게 설계하였다.
<br><br>

구조체와 주요 코드에대해서는 나중에 간단하게 소개하겠다.
<br><br><br><br><br>

>2번째 기능 등록된 회원 조회

