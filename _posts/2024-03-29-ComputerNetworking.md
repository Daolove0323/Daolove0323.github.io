---
layout: single
categories:
  - iOS
tags:
- ios
title: "인터넷에 어떻게 접속을 하는가"
comments: true
---

## 인터넷에 어떻게 접속을 하는가

<hr/>

인터넷에 연결되는 모든 장치를 호스트 또는 종단 시스템이라고 부른다. 종단 시스템은 통신 링크와 패킷 스위치의 네트워크로 연결된다. 통신 링크는 동축케이블, 구리선, 광케이블, 라디오 스펙트럼을 포함한 다양한 물리 매체로 구성된다. 이때 각각의 링크들이 데이터를 전송하는 전송률은 초당 비트 수를 의미하는 bps단위를 다용한다. 한 종단 시스템이 다른 종단 시스템으로 데이터를 보낼 때, 데이터를 세그먼트로 나누고 각 세그먼트에 헤더를 붙힌다. 이렇게 만들어진 정보 패키지를 패킷이라고 한다. 패킷이 목적지에 도달하면 원래의 데이터로 다시 복구된다. 패킷 교환기(또는 스위치)는 입력 통신 링크 중 하나로 도착하는 패킷을 받아서 출력 통신 링크 중 하나로 그 패킷을 전달한다. 오늘날 널리 사용되는 패킷 교환기로는 라우터와 링크 계층 스위치가 있다.

ISP(Internet Service Provider)는 패킷 스위치와 통신 링크로 이루어진 네트워크인데, 종단 시스템은 ISP를 통해 인터넷에 접속한다. 인터넷은 종단 시스템을  서로 연결하는 것이므로 종단 시스템에 접속을 제공하는 ISP들은 서로 연결되어야 한다. 이러한 하위 계층 ISP는 국가 그리고 국제 상위 계층 ISP를 통해 서로 연결되고, 이러한 상위 계층 ISP들은 서로 직접 연결된다. 상위 계층 ISP는 광 링크로 연결된 고속 라우터로 구성된다. 모든 ISP 네트워크는 따로 관리되며 IP 프로토콜을 준수하고 네이밍과 주소배정 방식을 따른다. 종단 시스템, 패킷 스위치를 비롯한 인터넷의 구성요소들은 정보 송수신을 제어하는 여러 프로토콜을 준수한다. 특히 TCP(Transmission Control Protocol)과 IP(Internet Protocol)은 인터넷에서 가장 중요한 프로토콜이다. IP 프로토콜은 라우터와 종단 시스템 사이에서 송수신되는 패킷 포맷을 기술한다. 이러한 인터넷의 주요 프로토콜을 통칭하여 TCP/IP라고 한다. 각각의 프로토콜들이 무엇을 수행하는지에 합의하는 것은 매우 중요한데, 그렇게 함으로써 상호 호환되는 시스템을 만들 수 있기 때문이다. 인터넷 표준은 IETF(Internet Engineering Task Force)에서 개발하며 IETF 표준 문서를 RFC(Requests for comment)라고 한다.

인터넛에 접속된 종단 시스템들은 다른 종단 시스템으로 어떻게 데이터를 전달하도록 요구하는지 명시하는 소켓 인터페이스를 제공한다. 인터넷 소켓 인터페이스는 송신 프로그램이 따라야 하는 규칙들이며, 인터넷은 이 규칙에 따라 데이터를 목적지 프로그램으로 전달하게 된다. 데이터를 송수신하는 인터넷의 모든 활동은 프로토콜이 제어한다. 물리적으로 연결된 두 컴퓨터의 네트워크 접속 카드에서 하드웨어로 구현된 프로토콜은 컴퓨터 사이에 연결된 선로상의 비트 흐름을 제어한다. 예를 들어, 종단 시스템에 있는 혼잡 제어(congestion-control) 프로토콜은 송수신자 간에 전송되는 패킷 전송률을 조절한다. 라우터에서 프로토콜은 출발지에서 목적지까지 패킷 경로를 설정한다. 

오늘날 가장 널리 보급된 광대역 가정 접속 유형은 DSL(Digital Subscriber Line)과 케이블이다(한국에서는 현재 FTTH, VDSL과 같은 인터넷 연결 방식이 보편화되어 있으며, 도시에서는 DSL이 흔치 않다). 일반적으로 가정에서는 유선 로컬 전화 서비스를 제공하는 같은 지역 전화 회사로부터 DSL 인터넷 접속 서비스를 제공받는다. 고객들의 DSL 모뎀은 지영 중앙국에 위치한 DSLAM(Digital Subscriber Line Access Multiplexer)과 데이터를 교환하기 위해 기존 전화 회선을 이용한다. 가정의 DSL 모뎀은 디지털 데이터를 받아서 전화선을 통해 지역 중앙국으로 전송하기 위해 고주파 신호로 변환한다. 여러 가정으로부터의 아날로그 신호는 DSLAM에서 디지털 포맷으로 다시 변환된다. 가정 전화 회선은 데이터와 전통적인 전화 신호를 동시에 전달하며 이들은 다른 주파수 대역에서 인코딩된다. (고속 다운스트림 채널: 50kHz ~ 1MHz 대역, 중간 속도의 업스트림 채널: 4~50kHz 대역, 일반적인 양방향 전화 채널: 0~4kHz 대역) 이 방식은 단일 DSL 링크가 3개의 분리된 링크인 것처럼 보이게 하여 하나의 전화 회선과 인터넷 연결이 동시에 DSL 링크를 공유할 수 있게 한다. 고객 쪽에 있는 스플리터는 가정에 도착하는 데이터와 전화 신호를 분리하고 데이터 신호를 DSL 모뎀으로 전송한다. DSLAM은 데이터와 전화 신호를 분리하고 데이터를 인터넷으로 송신한다. 수백 혹은 수천 개의 가정들이 하나의 DSLAM에 연결된다.

케이블 인터넷 접속은 케이블 TV 회사의 기존 케이블 TV 인프라스트런처를 이용한다. 가정은 케이블 TV 서비스를 제공하는 같은 회사로부터 인터넷 접속 서비스를 받는다. 광케이블은 케이블 헤드엔드를 이웃 레벨 정션에 연결하며 이로부터 개별 가정으로 도달 하는데는 동축케이블이 사용된다. 광케이블과 동축케이블 모두 이 시스템에서 채택하고 있기 때문에 흔히 HFC(Hybrid Fiber Coax)라고 부른다. 케이블 인터넷 접속은 케이블 모뎀이 필요한데, 이더넷 포트를 통해 가정 PC에 연결된다. 케이블 인터넷의 한 가지 중요한 특성은 공유 방송 매체라는 것이다. 헤드엔드가 보낸 모든 패킷이 모든 링크의 다운스트림 채널을 통해 모든 가정으로 전달된다. 이러한 이유로 여러 사용자가 다운스트림 채널에서 다른 비디오 파일을 동시에 수신하고 있다면 각 사용자가 비디오 파일을 수신하는 실제 수신율은 다운스트림 전송률보다 상당히 작아진다. 업스트림 채널도 공유되므로 분산 다중 접속 프로토콜은 전송을 조정하고 충돌을 피하기 위해 필요하다.

DSL과 케이블 네트워크가 현재 미국에서 가정 광대역 접속 주류를 이루고 있다. 더 빠른 속도를 제공하는 FTTH(Fiber To The Home) 기술도 존재하는데, 이는 지역 중앙국으로부터 가정까지 직접 광섬유 경로를 제공하는 것이다. FTTH는 잠재적으로 Gbps의 인터넷 속도를 제공하며, 현재 한국에서 많이 사용되는 방식이다. 일반적으로 지역 중앙국에서 시작되는 광섬유는 가정에 가까운 곳까지 하나의 광섬유로 와서 이곳에서 고객별 광섬유로 분리된다. 이러한 스플리팅을 수행하는 네트워크 구조로는 AON(Active Optical Network)와 PON(Passive Optical Network)가 있다. PON을 사용하는 네트워크에서 각 가정은 ONT(Optical Network Terminator)를 갖고 있으며 이는 광섬유를 통해 이웃한 스플리터에 연결된다. 스플리터는 여러 가정의 광섬유를 하나의 광섬유로 결합하고 이를 지역 중앙국에 있는 OLT(Optical Line Terminator)에 연결한다. 광신호와 전기신호 간의 변환을 제공하는 OLT는 라우터를 통해 인터넷에 연결된다. 가정에서 사용자는 홈 라우터를 ONT에 연결하고 이 홈 라우터를 통해 인터넷에 접속한다. PON 구조의 OLT에서 스플리터로 송신된 모든 패킷은 스플리터에서 복제된다. 그밖에도 최근 5G-FW 고정 무선(5G fixed wireless)은 고속 접속뿐만 아니라 빔포밍 기술을 사용하여 기지국에서 가정 내의 모뎀으로 데이터를 무선으로 전송한다.