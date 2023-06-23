---
layout: single
categories:
  - iOS
tags:
- ios
title: "App and environment"
comments: true
---

### 앱과 작동 환경

<hr/>

iOS13 이후, 여러 앱 UI 인스턴스를 동시에 생성 및 관리할 수 있고, 앱 스위처를 통해 이들간 전환이 가능하게 되었다.

아이패드에서는 앱의 인스턴스들을 나란히 배치하여 볼 수 있으며, 각 인스턴스는 다른 콘텐츠를 보여주거나 동일한 콘텐츠를 다른 방식으로 보여준다.

예로들어 캘린더 앱에서 특정 날을 보여주는 인스턴스와 달력을 보여주는 인스턴스를 배치할 수 있다.

UIKit은 특성 콜렉션(디바이스 설정, 인터페이스 설정, 사용자 선호를 포함)을 사용하여 현재 환경에 대한 정보을 전달할 수 있다.

예로 들어, 현재 뷰 또는 뷰 컨트롤러에 다크 모드가 적용됐는지 감지하는 특성을 사용할 수 있다.

또한 UIView 또는 UIViewController 객체의 특성 콜렉션을 참조하여 현재 환경에  따라 콘텐츠를 커스터 마이즈할 수 있다.

만약 특성 알림 변경들을 전달받으려면, 다른 객체들에게서 UITraitEnvironment 프로토콜을 채택할 수 있다.