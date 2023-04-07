---
layout: single
categories:
- Linux
tags:
- Linux
title: "Linux란?"
comments: true
---

 Linux는 서버 시스템뿐만 아니라 클라우드 컴퓨팅, 임베디드 시스템 등 다양한 분야에서 사용된다. 특히 모바일 운영체제의 양대 산맥 중 하나인 안드로이드 역시 Linux 커널을 기반으로 만들어졌고, 이처럼 Linux가 활용되는 분야는 더욱 확대됨에 따라 Linux를 다루는 능력은 중요한 역량으로 평가받기도 한다.

<br>

### UNIX

<hr/>

UNIX는 1969년 브라이언 커니핸, 켄 톰슨, 데니스 리치 등 벨 연구소 직원들에 의해 개발된  다중 사용자(Multi-user), 다중 작업(Multi-tasking) 운영체제이다.

따라서 UNIX는 여러 사용자들이 동시에 시스템에 로그인할 수 있으며, 각 유저들은 동시에 여러 작업이 가능하다.

UNIX는 처음에 Assemby 언어로 작성되었지만, UNIX 개발자 중 한명인 데니스 리치가 C언어를 개발하고 나서 C언어로 다시 작성되었다.

<br>

### Linux

<hr/>

Linux는 1991년 리누스 토발즈가 출시한 Linux 커널에 기반을 둔 오픈소스 UNIX 계열 운영체제 계열이다.

Linux는 GNU GPL(General Public Licnese)에 따라 누구든지 무료로 이용할 수 있게 개발되었고, 현재 오픈소스 소프트웨어의 대표적인 예시이다.

Linux 배포판은 커널과 지원 시스템 소프트웨어 그리고 라이브러리를 포함하고 있으며, 이들 중 대부분은 GNU 프로젝트에 의해 제공된다.

주된 Linux 배포판은 RedHat, Fedora, OpenSUSE, Debian의 Ubuntu Linux 등이 있다.

안드로이드 또한 Linux는 아니지만, Linux 커널을 기반으로 구글이 제작하는 모바일 운영체제이다.

<br>

### Linux 시스템

<hr/>

컴퓨터 시스템은 다음과 같은 구조를 가지며, 위 개념은 아래 개념을 포함한다.

`응용 소프트웨어(Application software)` - 웹 브라우저, 게임, 워드 프로세서 등

`시스템 소프트웨어(System software)` - 운영체제(Operating System), 유틸리티(Utility)

`하드웨어(Hardware)` - CPU, SSD, RAM 등

<br>

`커널(Kernel)`은 항상 메모리에 올라가 있는 운영체제의 핵심적인 부분으로, 시스템의 모든 것을 완전히 제어한다.

커널은 하드웨어와 소프트웨어 사이의 상호작용을 용이하게 하며, 그리고 하드웨어의 모든 자원들을 관리하고, 자원에 관련된 프로세스 간의 충돌을 중재한다.

또한 커널은 CPU 및 캐시 사용, 파일 시스템 및 네트워크 소켓과 같은 공통 자원에 대한 사용을 최적화한다.

![1280px-Kernel_Layout svg](https://user-images.githubusercontent.com/90020593/230552175-b1962df2-c4a8-42dd-aba3-fb18436f16bd.png)

<br>

다음은 Linux에서의 시스템 계층을 표로 나타낸 것이다.

![image](https://user-images.githubusercontent.com/90020593/230564966-49f80b14-e68a-4f53-9779-25bdce124ef8.png)

위 표는 시스템 계층을 User mode와 Kernel mode로 분리해서 보여주고 있다.

User mode에는 응용 소프트웨어와 시스템 구성요소, C 표준 라이브러리가 있으며, Kernel mode에는 Linux kernel이 있다. 그리고 그 아래 계층으로 하드웨어가 있다.

<br>

원칙적으로 User mode는 커널에 접근을 할 수 없기 때문에 커널이 관리하는 자원을 사용할 수 없다.

그래서 시스템 호출(System call)을 사용하는데, 이는 응용 프로그램이 커널이 관리하는 자원에 접근하기 위한 인터페이스이다.

쉘(Shell)은 운영체제와 사용자 사이의 인터페이스를 제공하는 소프트웨어로 시스템 호출의 일종이다. 쉘은 사용자로부터 명령어를 입력받아 이를 처리하는 명령어 처리기 역할을 수행한다.

<br>

### 참고 자료

<hr/>

 \- [위키백과](https://en.wikipedia.org/wiki/Kernel_(operating_system))

 \- [리눅스 시스템 이해와 활용](https://www.gjudec.com/content/61c55674192e57261ef25238)