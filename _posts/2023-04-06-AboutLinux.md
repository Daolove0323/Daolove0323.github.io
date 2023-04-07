---
layout: single
categories:
- Linux
tags:
- Linux
title: "Linux란?"
comments: true
---

<br>

 서버 분야에서 Linux의 점유율은 압도적이다.  또한 안드로이드 또한 Linux 기반 운영체제라고 한다. 그렇다면 Linux란 무엇일까? Linux가 등장한 배경과 다른 운영체제와 구별되는 Linux의 특징에 대해 알아보자.

<br>

글을 시작하기 전에 먼저 컴퓨터 시스템에 대해 알아보자.

컴퓨터 시스템은 다음과 같은 구조를 가지며, 위 개념은 아래 개념을 포함한다.

`응용 소프트웨어(Application software)` - 웹 브라우저, 게임, 워드 프로세서 등

`시스템 소프트웨어(System software)` - 운영체제(Operating System), 유틸리티(Utility)

`하드웨어(Hardware)` - CPU, SSD, RAM 등

<br>

### UNIX

<hr/>

UNIX는 다중 사용자(Multi-user), 다중 작업(Multi-tasking) 운영체제이다.

따라서 여러 사용자들이 동시에 시스템에 로그인할 수 있으며, 각 유저들은 동시에 여러 작업이 가능하다.

<br>

### 커널

<hr/>

커널(Kernel)은 항상 메모리에 올라가 있는 운영체제의 핵심적인 부분으로, 시스템의 모든 것을 완전히 제어한다.

커널은 사용자와 각각의 프로세스를 분리하며, 하드웨어의 접근을 통제한다.

또한 하드웨어와 소프트웨어 사이의 상호작용을 용이하게 한다. 그리고 하드웨어의 모든 자원들을 관리하며, 자원과 관련된 프로세스 간의 충돌을 중재한다. CPU 및 캐시 사용, 파일 시스템 및 네트워크 소켓과 같은 공통 자원에 대한 사용을 최적화한다.

사용자들은 쉘(Shell)을 통해 커널에 명령어를 전달할 수 있다.

![1280px-Kernel_Layout svg](https://user-images.githubusercontent.com/90020593/230552175-b1962df2-c4a8-42dd-aba3-fb18436f16bd.png)



### 참고 자료

<hr/>

 \- [위키백과](https://en.wikipedia.org/wiki/Kernel_(operating_system))

 \- [리눅스 시스템 이해와 활용](https://www.gjudec.com/content/61c55674192e57261ef25238)