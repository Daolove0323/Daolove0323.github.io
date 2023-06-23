---
layout: single
categories:
  - iOS
tags:
- ios
title: "앱을 시작하게 되면"
comments: true
---

## 앱을 시작(Launch)하게 되면

<hr/>

앱을 시작하면 앱의 자료구조를 초기화하고, 실행할 준비를 하고, 시스템으로부터 런치 시간 요청에 반응한다.

사용자가 홈 스크린의 앱 아이콘을 탭하게되면, 시스템은 앱을 런치한다.

만약 앱이 특정 이벤트에 의해 요청되면, 시스템은 그 이벤트를 처리하기 위해 앱을 백그라운드에서 런치한다.

씬 기반 앱에서 특정 씬이 스크린에 보여져야 할 때 또는 어떤 작업을 수행해야 할 때, 시스템은 유사하게 앱을 실행한다.



모든 앱들은 UIApplication 객체가 표시하는 관련 프로세스를 가진다.

앱은  또한 그 프로세스에서 발생하는 중요  이벤트에 반응하는 UIApplicationDelegate 프로토콜을 준수하는 app delegate 객체를 가진다.

씬 기반 앱은 런치나 종료와 같은 근본적인 이벤트를 관리하는 app delegate를 사용한다.

앱이 런치될때, UIKit은 자동으로 UIApplication 객체와 app delegate를 생성하고 앱의 메인 이벤트 루프를 시작한다.



### 런치 스토리보드 제공

사용자가 앱을 처음 시작하면, 시스템은 앱 UI가 준비될때까지 런치 스토리보드를 보여준다.

런치 스토리보드를 보여주는 것은 사용자에게 앱이 런치되었고 작동중임을 알려주기 위함이다.

만약 앱이 시작되고 UI가 빠르게 준비되면, 런치 스토리보드는 순식간에 지나가게 된다.

Xcode는 앱의 기본 런치 스토리보드를 제공하고, 필요에 따라 런치 스토리보드를 더 추가할 수도 있다.

```
런치 스크린에 정적 이미지를 사용하면 안된다. iOS 14 이상에서는 런치 스크린의 용량이 25MB로 제한된다.
```



### 앱의 자료구조 초기화

런치 시간 초기화 코드를 다음 메소드에 추가할 수 있다.

`application(_:willFinishLaunchingWithOptions:)`

`application(_:didFinishLaunchingWithOptions:)`

UIKit은 앱의 런치 사이클이 시작할 때 이 메소드들을 호출한다.



이 메소드는 다음 목적으로 사용된다.

앱의 자료구조를 초기화할 때

앱이 실행하기 위해 필요한 리소스를 가졌는지 확인하기 위해

앱이 처음 실행될 때, 1회 셋업을 하기위해 (예 : 쓰기 권한이 있는 디렉토리에 템플릿 또는 사용자가 수정가능한 파일 설치)

앱이 사용하는 중요한 서비스에 연결할 때 (예 : 앱이 원격 알림을 사용하는 경우, 애플 푸쉬 알림 서비스에 연결)

앱이 실행된 이유에 대한 정보를 런치 옵션 딕셔너리에서 확인하기 위해



씬 기반이 아닌 앱들의 경우, UIKit은 런치  타임에 자동으로 기본 UI를 로드한다.

이 때, 기본 UI가 스크린에 보여지기 전에 추가적으로 변경할 사항이 있으면 `application_:didFinishLaunchingWithOptions:)` 메소드를 사용할 수 있다.

예로 들어 앱을 마지막으로 사용했을 때 유저가 하던 일을 보여주기 위해 다른 뷰 컨트롤러를 설치할 수 있다.



### 장기 실행 작업을 메인 스레드에서 이동

사용자가 앱을 시작할 때, 빠르게 시작함으로써 좋은 인상을 남길 수 있다.

UIKit은 `application(_:didFinishLaunchingWithOptions:)` 메소드가 반환될 때까지 앱 UI를 보여주지 않는다.

`application(_:didFinishLaunchingWithOptions:)` 또는 `application(_:willFinishLaunchingWithOptions:)` 메소드에서 장시작 작업을 수행하는 것은 사용자로 하여금 앱이 느리다고 느끼게 한다.

시스템은 앱의 백그라운드 실행시간을 제한하기 때문에, 백그라운드에서 시작할 때도 빠른 반환은 중요하다.



다음과 같이 앱의 시작 순서에서 앱의 초기화에 중요하지 않은 작업을 옮길 수도 있다.

앱이 즉시 필요하지 않는 기능의 초기화의 연기

중요하고 장기 실행 작업을 앱의 메인 스레드에서 이동 (예 : 전역 디스패치 큐로 옮겨서 비동기식으로 실행)



### 앱이 시작된 이유

UIKit이 앱을 시작할 때, 런치 옵션 딕셔너리를  `application(_:willFinishLaunchingWithOptions:)` 와 `application(_:didFinishLaunchingWithOptions:)` 메소드에 앱이 시작한 이유에 대한 정보와 함께 전달한다.

딕셔너리의 키는 즉시 실행해야 할 중요한 작업을 가르킨다.

예로 들어 사용자가 다른 곳에서 시작하여 앱에서 계속 이어하길 원하는 작업을 나타낸다.

키에 대한 런치 옵션 딕셔너리의 콘텐츠를 항상 확인하고, 이에 적절하게 반응해야 한다.

씬 기반 앱의 경우, UIKit이 씬을 만든 이유를 확인하려면 `application(_:configurationForConnecting:options:)` 메소드에 전달한 옵션을 확인해야 한다.



아래는 백그라운드 위치 업데이트를 처리하는 앱 델리게이트 메소드의 코드이다.

위치 키가 존재할 때, 앱은 앱은 즉시 위치 업데이트를 시작하고, 이는 Core Location 프레임워크가 새로운 위치 이벤트를 전달하도록 한다.

```swift
class AppDelegate: UIResponder, UIApplicationDelegate, 
               CLLocationManagerDelegate {
    
   let locationManager = CLLocationManager()
   func application(_ application: UIApplication,
              didFinishLaunchingWithOptions launchOptions:
              [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
       
      // If launched because of new location data,
      //  start the visits service right away.
      if let keys = launchOptions?.keys {
         if keys.contains(.location) {
            locationManager.delegate = self
            locationManager.startMonitoringVisits()
         }
      }
       
      return true
   }
   // other methods…
}
```

앱이 해당 기능을 지원하지 않으면, 시스템은 키를 포함하지 않는다.

예로 들어 시스템은 원격 알림을 지원하지 않는 앱의 remoteNotification 키를 포함하지 않는다.