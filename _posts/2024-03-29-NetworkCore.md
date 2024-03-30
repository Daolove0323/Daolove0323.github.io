---
layout: single
categories:
  - iOS
tags:
- ios
title: "네트워크 코어"
comments: true
---

## 네트워크 코어

<hr/>

네트워크 코어

종단 간 지연

네트워크 애플리케이션에서 종단 시스템들은 서로 메시지를 교환한다. 메시지를 송신하는 종단 시스템에서 목적지 종단 시스템으로 메시지를 보내기 위해 송신 시스템은 긴 메시지를 패킷이라고 하는 작은 데이터 조각으로 분할한다. 송신 측과 수신 측 사이에서 각 패킷은 통신 링크와 패킷 스위치(라우터와 링크 계층 스위치 두 종류가 있음)를 거치게 된다. 패킷은 링크의 최대 전송률과 같은 속도로 각각의 통신 링크에서 전송된다. 따라서 송신 종단 시스템 혹은 패킷 스위치가 R bits/s의 속도로 링크에서 L bits의 패킷을 송신한다면 그 패킷을 전송하는 데 걸리는 시간은 L/R s이다. 대부분의 패킷 스위치는 저장-후-전달 전송(store-and-forward transmission) 방식을 이용한다. 저장-후-전달은 스위치가 출력 링크로 패킷의 첫 비트를 전송하기 전에 전체 패킷을 받아야 함을 의미한다. 따라서 전파 지연을 무시한다면, 라우터가 전체 패킷을 수신하고 출력 링크로 보내는데 걸리는 시간, 즉 종단 간 지연은 N * L/R s이다. (N은 출발지로부터 목적지까지 링크의 개수를 의미)

큐잉 지연

각 패킷 스위치는 여러 개의 링크와 연결되어 있고, 각 링크에 대해 출력 버퍼(output buffer, 출력 큐(ouput queue)라고도 부름)를 가진다. 출력 버퍼에는 그 링크로 송신하려고 하는 패킷을 저장하고 있다. 도착하는 패킷이 한 링크로 전송되어야 하는데 그 링크가 다른 패킷을 전송하고 있다면 도착하는 패킷은 출력 버퍼에서 대기해야 한다. 이때 걸리는 지연을 큐잉 지연(queuing delay)라고 한다. 이러한 지연은 가변적이고 네트워크의 혼잡 정도에 따른다. 버퍼 공간의 크기가 유한하기 때문에 도착하는 패킷은 버퍼가 전송을 위해 대기 중인 다른 패킷들로 가득찬 경우가 있을 수도 있는데, 이를 패킷 손실(packet loss)이라고 한다.

포워딩 테이블

인터넷에서 모든 종단 시스템은 IP 주소를 갖는다. 한 종단 시스템이 패킷을 보낼 때, 패킷의 헤더에는 목적지의 IP 주소를 포함한다. 각 라우터는 목적지 IP 주소를 라우터의 출력 링크로 매핑하는 포워딩 테이블을 가지고 있다.  패킷이 라우터에 도착하면 라우터는 올바른 출력 링크를 찾기 위해 목적지 IP 주소를 읽어들이고 이 주소를 이용하여 포워딩 테이블을 검색한다. 그 후 라우터는 그 패킷을 출력 링크로 전송한다.

회선 교환

링크와 스위치의 네트워크를 통해 데이터를 전송하는 방식에는 회선 교환(circuit switching)과 패킷 교환(packet switching) 두 가지가 있다. 패킷 교환과 달리 회선 교환 네트워크에서 종단 시스템 간에 통신을 제공하기 위해 경로상에 필요한 자원(버퍼, 링크 전송률)은 통신 세션 동안에 확보된다. 세션 메시지는 온디맨드(on-demand) 방식으로 자원을 요청하여 사용하고, 통신 링크에 대한 접속을 위해 기다릴(큐에서 대기) 수도 있다. 회선 교환 네트워크의 예로 전통적인 전화망이 있다. 송신자가 정보를 보내기 전에 네트워크는 송신자와 수신자 간의 연결을 설정해야 한다. 이것은 송신자와 수신자 간의 경로에 있는 스위치들이 해당 연결 상태를 유지해야 하는 연결이다. 전기통신 용어로 이 연결을 회선이라고 한다. 네트워크가 회선을 설정할 때, 그 연결이 이루어지는 동안 네트워크 링크에 일정한 전송률을 예약한다. 주어진 전송률이 송신자-수신자 연결을 위해 예약되므로 송신자는 수신자에게 보장된 일정 전송률로 데이터를 보낼 수 있다.

회선 교환 네트워크에서의 다중화

링크 내 한 회선은 주파수 분할 다중화(FDM, Frequency-Division Multiplexing) 혹은 시분할 다중화(TDM, Time-Division Multiplexing)로 구현된다. FDM에서 링크를 통해 설정된 연결은 그 링크의 주파수 스펙트럼을 공유한다. 특히 그 링크는 연결되는 동안 각 연결에 대해 주파수 대역을 고정 제공한다. 이런 대역의 폭을 대역폭(bandwidth)이라고 한다. TDM 링크의 경우는 시간을 일정 주기의 프레임으로 구분하고 각 프레임은 고정된 수의 시간 슬롯으로 나뉜다. 네트워크가 링크를 통해 하나의 연결을 설정할 때, 네트워크는 모든 프레임에서 시간 슬롯 1개를 그 연결에 할당한다. 이들 슬롯은 그 연결을 위해 사용되도록 할당되고 그 연결의 데이터를 전송하기 위해 모든 프레임에 하나의 시간 슬롯을 갖게 된다. TDM 회선의 전송률은 한 슬롯 안의 비트 수에 프레임 전송률을 곱한 것과 같다. 예를 들어, 링크가 초당 8,000 프레임을 전송하고 각 슬롯이 8비트로 구성된다면 회선의 전송률은 64kbps이다.

패킷 교환 옹호자들은 회선 교환의 경우 할당된 회선이 비활용 기간에는 놀게 되므로 낭비가 발생한다고 한다. 또한 패킷 교환이 회선 교환보다 전송 용량의 공유에서 더 효율적이며, 구현 비용이 적다고 주장한다. 패킷 교환 옹호자들이 드는 예는 다음과 같다. 사용자가 1Mbps 링크를 공유한다고 하자. 또한 각 사용자는 활동 시간(100kbps의 일정속도로 데이터 생산)과 비활동 시간(데이터를 생산하지 않음)을 반복한다. 그리고 사용자는 전체 시간에서 10%만 활동한다고 하자. 회선 교환의 경우 100kbps가 항상 각각의 사용자에게 예약되어야 한다. 회선 교환 TDM에서 1초 프레임이 100ms마다 10개 시간 슬롯으로 나뉜다면 각 사용자에게는 한 프레임에 한 번의 시간 슬롯이 할당된다. 즉 회선 교환 링크는 동시에 10명(=1Mbps/100kbps)만 지원할 수 있다. 패킷 교환의 경우에는 만일 35명의 사용자가 있다면, 11명 이상의 사용자가 동시에 활동할 확률은 0.0255, 즉 2퍼센트에 불과하다. 만약 10명 이하의 동시 사용자가 있을 때, 사용자의 패킷은 회선 교환의 경우와 마찬가지로 지연 없이 링크를 통과한다. 10명 이상의 동시 사용자가 있다면 패킷의 통합 도착률이 링크의 출력 용량을 초과하므로 출력 큐가 커지기 시작한다. 하지만 10명 이상의 동시 사용자가 있을 확률은 매우 작으므로 패킷 교환은 거의 항상 회선 교환과 대등한 지연 성능을 가지면서도 3배 이상의 사용자 수를 허용한다. 한가지 예를 더 들어보자. 10명의 사용자가 있다. 한 사용자가 한번에 1,000비트 패킷을 1,000개 생성하고 다른 사용자는 패킷을 생성하지 않는다. 한 프레임은 10개 슬롯으로 구성되고 각 슬롯은 1,000비트로 구성된 TDM 회선 교환의 경우, 사용자는 데이터 전송을 위해 한 프레임당 1개의 시간 슬롯만 사용할 수 있다. 반면에 각 프레임에 남겨진 9개의 시간 슬롯은 쉬는 상태가 된다. 이 경우에는 사용자의 데이터 100만 비트를 모두 전송하려면 10초가 걸린다. 패킷 교환으 ㅣ경우에는 패킷을 생성하는 다른 사용자가 없기에 다중화가 요구되지 않고 사용자는 1Mbps의 링크가 가득 찰 때까지 패킷을 계속 보낼 수 있다. 그러므로 사용자의 데이터는 1초만에 전송된다.  반면 회선 교환 옹호자들은 패킷 교환에서는 가변적이고 예측할 수 없는 종단 간의 지연(주로 불규칙적이고 예측할 수 없는 큐잉 지연) 때문에 패킷 교환이 화상 통화와 같은 실시간 서비스에는 적절하지 않다고 주장한다. 링크 전송률을 공유하는 두 방식의 가장 큰 차이점은 회선 교환이 요구에 관계없이 미리 전송 링크를 할당하는 반면에 패킷 교환은 요구할 때만 링크의 사용을 할당한다는 것이다. 패킷 교환과 회선 교환은 현재 전기통신 네트워크에서 널리 이용되지만 그 추세는 패킷 교환으로 바뀌고 있다. 특히 오늘날에는 많은 회선 교환 전화망이 패킷 교환으로 전환되고 있는 중이다.

한 종단 시스템에서 목적 종단 시스템까지의 경로에서 패킷은 다양한 지연을 겪게 된다. 주요 지연으로는 노드 처리 지연(nodal processing delay), 큐잉 지연(queuing delay), 전송 지연(transmission delay), 전파 지연(propagation delay) 등이 있으며 이러한 지연들이 쌓여서 전체 노드 지연(total nodal delay)를 일으킨다. 처리 지연은 패킷 헤더를 조사하고 그 패킷을 어디로 보낼지를 결정하는 시간이다. 큐잉 지연은 패킷이 큐에서 링크로 전송되기를 기다리는 시간이다. 큐잉 지연 길이는 큐에 저장되어 링크로 전송되기를 기다리는 앞선 패킷의 수에 의해 결정된다. 전송지연은 패킷의 모든 비트를 링크로 밀어내는 데 필요한 시간이다. 전파지연은 링크의 처음부터 다음 라우터까지의 전파에 필요한 시간이다. 전파 속도는 링크의 물리 매체(광섬유, 꼬임쌍선, 동축케이블 등)에 따라 다른데 대략적으로 빛의 속도와 같거나 약간 작다. 전파 지연의 크기는 두 라우터 사이의 거리를 전파 속도로 나눈 값이다. 전송 지연은 라우터가 패킷을 내보내는 데 필요한 시간이다. 이는 패킷 길이와 링크 전송률의 함수이다. 전체 노드 지연은 다른 모든 지연들의 합과 같다. 출발 호스트에서 목적 호스트 사이에 N - 1개의 라우터가 있다고 하자. 그리고 네트워크가 혼잡하지 않을 때(큐잉 지연을 무시), 종단간 지연은 N x (처리 지연 + 전송 지연 + 전파 지연)이다. 여기서 전송 지연은 L / R이며 L은 패킷의 크기이다.

지연과 패킷 손실 외에도 컴퓨터 네트워크에서  주요한 성능 수단으로 종단 간 처리율(throughput)이 있다. 서버와 클라이언트 간에 N개의 링크를 가진 네트워크가 있다고 하자. 이 네트워크에서의 처리율은 min(R1, R2, R3, ..., Rn), 즉 병목 링크(bottleneck link)의 전송률이다.

애플리케이션 계층은 네트워크 애플리케이션과 애플리케이션 계층 프로토콜이 잇는 곳이다. 인터넷의 애플리케이션 계층은 HTTP(웹 문서 요청과 전송 제공), SMTP(전자메일 전송 제공), FTP(두 종단 시스템 간의 파일 전송 제공) 같은 많은 프로토콜을 포함한다. 우리에게 친숙한 도메인 네임을 32비트 네트워크 주소로 변환하는 네트워크 기능을 볼 것이고, 이것은 도메인 네임 서버(DNS, Domain Name Server)가 담당한다. 애플리케이션 계층 프로토콜은 여러 종단 시스템에 분산되어 있어서 한 종단 시스템에 있는 애플리케이션이 다른 종단 시스템에 있는 애플리케이션과 정보 패킷을 교환하는 데 이 프로토콜을 사용한다. 애플리케이션 계층에서의 이 정보 패킷을 메시지라고 한다.

트랜스포트 계층은 클라이언트와 서버 간에 애플리케이션 계층 메시지를 전송하는 서비스를 제공한다. 인터넷에는 TCP와 UDP라는 두 가지 트랜스포트 프로토콜이 있으며 이들은 애플리케이션 계층 메시지를 전달한다. TCP는 애플리케이션에게 연결 지향형 서비스를 제공한다. 이 서비스는 목적지로의 애플리케이션 계층 메시지 전달 보장과 흐름 제어(송신사/수신자의 속도 일치)를 포함한다. 또한 TCP는 긴 메세지를 짧은 메시지로 나누고 혼잡 제어 기능을 제공하여 네트워크가 혼잡할 때 출발지의 전송률을 줄이게 한다. UDP 프로토콜은 애플리케이션에 비연결형 서비스를 제공한다. 이 서비스는 신뢰성, 흐름제어, 혼잡 제어를 제공하지 않는 아주 간단한 서비스다. 트랜스포트 계층 패킷을 세그먼트라고 한다.

네트워크 계층은 한 호스트에서 다른 호스트로 데이터그램을 라우팅하는 책임을 진다. 출발 호스트에서 트랜스포트 계층 프로토콜(TCP 또는 UDP)은 트랜스포트 계층 세그먼트와 목적지 주소를 네트워크 계층으로 전달한다. 그런 다음 네트워크 계층은 목적지 호스트의 트랜스포트 계층으로 세그먼트를 운반하는 서비스를 제공한다. 네트워크 계층은 두 가지 주요 요소를 갖는다. 첫째는 이 계층은 IP 데이터그램의 필드를 정의하며 종단 시스템과 라우터가 이 필드에 어떻게 동작하는지를 정의하는 IP 프로토콜을 갖고 있다. 둘째는 출발지와 목적지 사이에 데이터그램이 이동하는 경로를 결정하는 라우팅 프로토콜을 포함한다. 

링크 계층에서 제공하는 서비스는 그 링크에서 채용된 특정 링크 계층 프로토콜에 의해 결정된다. 링크 계층 프로토콜의 예로는 이더넷, 와이파이 그리고 케이블 접속 네트워크의 DOCSIS 프로토콜을 들 수 있다. 데이터그램이 출발지에서 목적지로 가는데 여러 링크를 거치므로 데이터그램은 경로상의 각기 다른 링크에서 다른 링크 계층 프로토콜에 의해 처리될 수 있다. 가령 데이터그램은 하나의 링크에선 이더넷에 의해 다루어지고 다음 링크에서는 PPP에 의해 다루어질 수 있다. 링크 계층 패킷을 프레임이라고 한다.

물리 계층은 프레임 내부의 각 비트를 한 노드에서 다음 노드로 이동하는 것이다. 이 계층의 프로토콜들은 링크에 의존하고 더 나아가 링크의 실제 전송 매체(UTP, 광케이블)에 의존한다. 예를 들어 이더넷은 여러 가지 물리 계층 프로토콜을 갖고 있다.(UTP용, 광케이블용, 동축케이블용 등)

캡슐화

송신 호스트에서 애플리케이션 계층 메시지는 트랜스포트 계층으로 보내진다. 애플리케이션 계층 메시지에 트랜스포트 계층 헤더 정보를 더해 트랜스포트 계층 세그먼트를 구성한다. 트랜스포트 계층 세그먼트는 애플리케이션 계층 메시지를 캡슐화한다. 추가된 정보는 수신 측의 트랜스포트 계층이 그 메시지를 적절한 애플리케이션으로 보내도록 하는 정보와 메시지의 비트들이 변경되었는지 아닌지 수신자가 결정하게 하는 오류 검출 비트를 포함한다. 그 후 트랜스포트  계층은 세그먼트를 네트워크 계층으로 보내면 네트워크 계층에서 출발지와 목적지 종단 시스템 주소와 동일한 헤더정보를 추가하여 네트워크 계층 데이터그램을 만든다. 이 데이터그램은 링크 계층으로 전달되고 헤더 정보를 추가하여 링크 계층 프레임을 만든다. 이처럼 각 계층에서 패킷은 헤더 필드와 페이로드 필드라는 두 가지 형태의 필드를 갖는다. 이때 페이로드는 일반적으로 그 계층 상위로부터의 패킷이다.

DoS)Denial-of-Service)

Dos 공격은 네트워크, 호스트 혹은 다른 인프라스트럭처의 요소들을 정상적인 사용자가 사용할 수 없게 하는것이다. 대부분의 인터넷 DoS 공격은 취약성 공격, 대역폭 플러딩, 연결 플러딩으로 분류된다. 취약성 공격(vulnerability attack)은 목표 호스트에서 수행되는 공격받기 쉬운 애플리케이션 혹은 운영체제에 교모한 메시지를 보내는 것을 포함한다. 만약 올바른 순서의 패킷을 공격받기 쉬운 애플리케이션 혹은 운영체제에 보내면 그 서비스는 중단되거나 더 나쁘게는 호스트가 동작을 멈출 수 있다. 연결 플러딩(connection flooding)은 호스트에 반열림 혹은 전열림된 TCP 연결을 설정한다. 호스트는 가짜 연결을 처리하느라 바빠서 정상적인 연결을 받아들이는 것을 중단하게 된다. 대역폭 플러딩(bandwidth flooding)은 목표 호스트로 수많은 패킷을 보내는 것이다. 목표 호스트의 접속 링크가 동작하지 못하도록 많은 패킷을 보내서 정당한 패킷들이 그 서버에 도달하지 못하게 한다. 만약 서버가 R bps의 접속 속도를 가진다면 공격자는 피해를 주기 위해 대략 R bps의 속도로 트래픽을 전송하면 된다.

 패킷 스니핑(packet sniffing)

오늘날 많은 사용자는 와이파이 또는 셀룰러를 통해 인터넷에 접속하고 있다. 무선 전송장치의 근처에 수동적인 수신자를 위치시킴으로써 그 수신자는 전송되고 있는 모든 패킷의 사본을 얻을 수 있다. 그리고 이 패킷들은 비밀번호, 주민등록번호, 영업 비밀 등 민감한 정보일 수 잇다. 이때 지나가는 모든 패킷의 사본을 기록하는 수동적인 수신자를 패킷 스니퍼라고 한다. 스니퍼는 또한 유선 환경에서도 배치될 수 있다.

IP 스푸핑(spoofing)

가짜 출발지 주소를 가진 패킷을 인터넷으로 보내는 것을 IP 스푸핑이라고 하며, 이를 통해 한 사용자가 다른 사용자인척 행동할 수 있다. 이 문제를 해결하기 위해 종단 인증(end-point authentication), 즉 메시지가 실제로 와야 할 곳으로부터 온 것인지 확인할 수 있는 방법이 필요하다.