---
layout: single
categories:
  - iOS
tags:
- ios
title: "iOS 앱은 어떻게 실행될까?"
comments: true

---



## iOS 앱은 어떻게 실행될까?

<hr/>

C언어 기반 애플리케이션들은 main() 함수로부터 시작된다.

이를 엔트리 포인트(Entry Point)라고 하는데, 운영체제가 애플리케이션 내부의 main() 함수를 호출하면 여기에 작성된 코드들이 연쇄적으로 실행되는 방식이다. 

Objective-C 또한 C 기반 언어이기에 Ojective-C로 만들어진 iOS 앱 또한 main() 함수로부터 시작된다.

Objective-C 기반의 Xcode 프로젝트를 생성했을 때 main.m 파일에 생성되는 main() 함수는 다음과 같다. 

```objective-c
int main(int argc, char * argv[]) {
    @autoreleasepool {
        // Setup code that might create autoreleased objects goes here.
        appDelegateClassName = NSStringFromClass([AppDelegate class]);
        }
    return UIApplicationMain(argc, argv, nil, appDelegateClassName);
}
```

main() 함수는 운영체제로부터 전달받은 두 값(argc, argv)과 AppDelegate 클래스의 이름을 이용해 UIApplicationMain() 함수를 호출한다. 

> NSStringFromClass() : 클래스의 이름을 String 으로 반환하는 함수
>
> @autoreleasepool{} : 블록 내부의 객체들의 참조 카운트 감소를 미루어 해제를 연기했다가 블록이 끝날 때 모두 해제한다.



### UIApplicationMain() 함수

<hr/>

UIApplicationMain() 함수는 iOS 앱의 엔트리 포인트라고 할 수 있을 정도로 매우 중요하며, 함수의 선언은 다음과 같다. (아래는 각각 Objective-C, Swift 코드)    
```objective-c
int UIApplicationMain(int argc, char * _Nullable *argv, NSString *principalClassName, NSString *delegateClassName);
```
```swift
func UIApplicationMain(
    _ argc: Int32,
    _ argv: UnsafeMutablePointer<UnsafeMutablePointer<CChar>?>,
    _ principalClassName: String?,
    _ delegateClassName: String?
) -> Int32
```

UIApplicationMain() 함수의 파라미터는 argc, argv, principalClassName, delegateClassName 이 있다. 

argc와 argv는 대부분 main() 함수의 인자와 일치하며 각각 argv의 개수, arguments의 변수 리스트이다.

principalClassName은 UIApplication 클래스(혹은 서브 클래스)의 이름이다. <br>만약 이 값이 nil인 경우, UIApplication으로 가정된다.

delegateClassName은 인스턴스화될 delegate의 클래스 이름이다.

UIApplicationMain() 함수의 반환형은 int이지만, 이 함수는 결코 반환하지 않는다.<br>홈 버튼을 눌러 앱을 나가더라도, 앱은 백그라운드로 넘어간다. 

> 만약 principalClassName에 UIApplication의 서브 클래스를 지정하면 delegateClassName에도 그 서브 클래스가 지정되며, 서브 클래스의 인스턴스는 application-delegate 메시지를 받는다. 
>
> 앱의 메인 nib 파일에서 delegate 객체를 로드하는 경우에는 delegateClassName를 nil로 지정한다. 




### UIApplicationMain() 함수의 역할
<hr/>

- application 객체와 delegate 객체를 생성하고, 두 객체를 연결한다.
- 앱의 run loop와 같은 main event loop를 설정한다.
- 앱의 Info.plist이 로드할 메인 nib 파일(NSMainNibFile Key나 그 값이 유효한 nib 파일 이름 포함)을 지정하면, 이를 로드한다.
- 스토리보드 파일로부터 앱의 유저 인터페이스를 읽어들이고, 커스텀 코드를 호출해 앱 생성 초기 설정을 구현한다.




### UIApplication
<hr/>

UIApplication 객체는 UIApplicationMain() 함수로부터 만들어지며, 모든 iOS 앱은 단 하나의 UIApplication 인스턴스를 가진다. 

UIApplication 객체는 사용자 이벤트의 초기 라우팅을 처리하여, 컨트롤 객체(UIControl 클래스의 객체)로부터 전달받은 액션 메시지를 적절한 타겟 오브젝트로 전달한다. 

UIApplication 객체는 열린 windows(UIWindow 객체)를 유지함으로써, 앱의 UIView 객체를 다시 불러올 수 있다.

UIApplication class는 UIApplicationDelegate 프로토콜을 준수하고 프로토콜의 특정 메서드를 반드시 실행하는 delegate를 정의한다.<br>그리고 그 UIApplication 객체는 그 delegate에게 적절하게 대응할 수 있도록 중요한 runtime events(앱 실행, 메모리 부족 경고, 앱 종료)를 전달한다. 

iOS앱들은 서로 자원(이미지 파일, 이메일 등)을 특정 메서드를 통해 함께 관리한다.<br>예를 들면 어떤 앱은 특정 메서드에 이메일 주소를 전달하여 메일 앱을 실행하고 메시지를 보여줄 수 있다.

UIApplication 클래스의 API들은 디바이스의 특정 동작을 다룰 수 있다.

* 일시적으로 터치 이벤트의 입력을 중단
* 푸시 알림 설정
* 실행 취소 및 되돌리기
* URL scheme을 처리하기 위해 등록된 앱이 있는지 확인
* 백그라운드에서 작업을 마칠 수 있도록 앱의 실행 연장
* 로컬 알림 설정 및 해지, 원격 컨트롤 이벤트 수신 조정, 앱 상태 복구)

대부분의 앱에서는 UIApplication를 서브 클래스할 필요가 없으며, 대신 시스템과 앱의 상호작용을 관리하기 위해 app delegate를 사용한다.<br>매우 드문 경우로 앱이 시스템보다 먼저 데이터 수신을 다뤄야 할 때, UIApplication을 서브 클래스하고 sendEvent: 또는 sendAction:to:from:forEvent: 메서드를 오버라이드 하여 사용 지정 이벤트나 action dispatching 메커니즘을 수행할 수 있다.<br>가로챈 이벤트를 처리한 후에는 super.sendEvent(event) 메서드를 호출하여 시스템에 다시 돌려줘야 한다. 이벤트를 가로채는 것은 극히 일부여야 하며 가능한 한 피하는 것이 좋다.

UIApplication 객체는 사실상 앱 그자체이며 우리가 작성하는 커스텀 코드와 앱의 기능이라 생각하는 것들은 다 UIApplication에 포함된 하위 객체이다. <br>
앱을 실행하면 초기 구동 과정을 거쳐 앱 프로세스가 메모리에 올라가는데, 이때의 앱 프로세스가 곧 UIApplication 객체라고 봐도 무방하다.



### AppDelegate
<hr/>

AppDelegate 또한 UIApplication과 마찬가지로 앱내에서 단 하나의 인스턴스만 생성된다. 

또한 앱이 처음 만들어질 때 객체가 생성되고 앱이 종료되면 소멸된다.<br> 즉 앱과 생명 주기를 함께 한다.<br>따라서 AppDelegate 객체에 데이터를 저장하면 앱이 종료될 때까지 데이터를 유지할 수 있다. 

AppDelegate는 UIApplication으로부터 일부 권한을 위임받아 커스텀 코드와 상호작용하는 역할을 담당하고, 이를 통해 우리가 필요한 코드를 구현할 수 있게 한다.

AppDelegate 객체는 커스텀 코드와 연결되는 만큼, 대부분의 경우 커스터마이징하거나 서브 클래싱하여 사용할 수 있도록 오픈되어 있다.

다음과 같은 작업들을 다루기 위해 app deletegate를 사용할 수 있다.

* 앱의 핵심 데이터 구조를 실행
* 앱의 씬을 설정
* 메모리 부족, 다운로드 완료 알림과 같은 앱 외부 알림에 반응
* 앱의 씬, 뷰, 뷰 컨트롤러로 지정되지 않는 앱 그자체를 타겟으로 하는 이벤트에 반응
* 애플 푸쉬 알림 서비스와 같은 실행 시 요구되는 서비스 설정



### @main
그런데 Swift 기반의 xCode 프로젝트를 생성해도 우리가 위에서 배웠던 main.m 파일을 찾을 수 없다.    
이는 UIKit 프레임워크 안에 main 함수 구현을 숨겼기 때문인데, 우리는 대신 이를 @main 어노테이션으로 대체한다.  

이후 이벤트 루프를 만드는 등 실행에 필요한 준비를 진행하고, 실행 완료 직전, AppDelegate의 application(\_:didFinishLaunchingWithOptions:) 메소드를 호출하며 앱은 실행된다.    

수정중..





![image](![iOSAppLaunchSequence](https://user-images.githubusercontent.com/90020593/227989650-1e7adc8b-6971-447f-8174-84cea6f06a44.png))





1. The system executes the `main()` function that Xcode provides.
2. The `main()` function calls [`UIApplicationMain(_:_:_:_:)`](https://developer.apple.com/documentation/uikit/1622933-uiapplicationmain), which creates an instance of [`UIApplication`](https://developer.apple.com/documentation/uikit/uiapplication) and of your app delegate.
3. UIKit loads the default storyboard you specify in your app’s `Info.plist` file, or in the target’s Custom iOS Target Properties tab of Xcode’s project editor; apps that don’t use a default storyboard skip this step.
4. UIKit calls the [`application(_:willFinishLaunchingWithOptions:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623032-application) method in your app delegate.
5. UIKit performs state restoration, which results in the execution of additional methods in your app delegate and app’s view controllers.
6. UIKit calls your app delegate’s [`application(_:didFinishLaunchingWithOptions:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application) method.

After the launch sequence completes, the system uses your app or scene delegates to display your app’s user interface and to manage its life cycle.

1. 사용자 또는 시스템이 앱을 실행하거나 시스템이 앱을 예열(prewarms)한다.

2. 시스템은 Xcode가 제공하는 main() 함수를 실행한다.

3. main() 함수는 UIApplication 객체와 app delegate 객체를 생성하는 UIApplicationMain() 함수를 호출한다.

4. UIKit은 앱 Info.plist 파일에 지정된 디포트 스토리보드 파일을 로드한다. (앱이 디포트 스토리보드를 사용하지 않으면 이 단계를 건너뛴다.)

5. UIKit이 app delegate의 application(_:willFinishLaunchingWithOptions:) 메서드를 호출한다.

6. UIKit이 상태 복원을 함으로써 app delegate와 view controller의 추가 메서드를 실행한다.

7. UIKit이 app delegate의 application(_:didFinishLaunchingWithOptions:) 메서드를 호출한다.

   위 과정들이 끝나면 시스템은 앱 UI를 보여주고 앱의 라이프사이클을 관리하기 위해 앱 또는 scene delegate를 사용한다.



### [Prepare your app for prewarming](https://developer.apple.com/documentation/uikit/app_and_environment/responding_to_the_launch_of_your_app/about_the_app_launch_sequence#3894431)

In iOS 15 and later, the system may, depending on device conditions, *prewarm* your app — launch nonrunning application processes to reduce the amount of time the user waits before the app is usable. Prewarming executes an app’s launch sequence up until, but not including, when `main()` calls `UIApplicationMain(_:_:_:_:)`. This provides the system with an opportunity to build and cache any low-level structures it requires in anticipation of a full launch.



iOS 15 이상에서, 시스템은 디바이스의 상태에 따라 앱을 prewarm한다.

이는 사용자가 앱을 사용하기 위해 기다리는 시간을 줄이기 위해 현재 실행하지 않는 앱을 시작하는 것이다.

prewarming 은 main() 함수가 UIApplicationMain() 함수를 호출하기 직전까지 앱을 실행한다.

이것은 시스템으로 하여금 완전한 실행의 예상에서 요구하는 low-level 구조를 만들고 cache할 수 있게 한다.



앱의 실행에서 시스템이 요구하는 low-level structures이란? 

wwdc : [App Startup Time: Past, Present, and Future](https://developer.apple.com/videos/play/wwdc2017/413).



After the system prewarms your app, its launch sequence remains in a paused state until the app launches and the sequence resumes, or the system removes the prewarmed app from memory to reclaim resources. The system can prewarm your app after a device reboot, and periodically as system conditions allow.

시스템이 앱을 준비(prewarm)한 후에는 앱이 실행되기 전까지 launce 절차는 정지된다. 또는 시스템은 리소스를 되찾기 위해 메모리로부터 준비된(prewarmed) 앱을 제거한다. 시스템은, 시스템은 디바이스 재부팅 후 또는 시스템 조건이 허락하는 한 주기적으로 앱을 준비(prewarm)할 수 있다. 

If your app executes code before the call to `UIApplicationMain(_:_:_:_:)`, such as in static initializers like [`load()`](https://developer.apple.com/documentation/objectivec/nsobject/1418815-load), don’t make assumptions about what services and resources are available. For example, keychain items may be unavailable because their data protection policies require an unlocked device and prewarming happens even when the device is in a locked state. If your code is dependent upon access to a specific service or resource, migrate that code to a later part of the launch sequence.

만약 앱이 UIApplicationMain() 함수가 호출되기 전에 앱이 코드를 실행한다면(예로 들면 정적 load() 와 같은 정적 이니셜라이저), 서비스와 자원을 사용할 수 있다고 가정하면 안된다. 예로 키체인 아이템은 사용 할 수 없는데, 그 데이터 보호 정책이 잠금이 풀린 디바이스를 요구하고, 준비는 심지어 디바이스가 잠금상태에서도 일어나기 때문이다. 만약 코드가 특정 서비스나 리소스에 의존적이라면, 코드를 실행 절차의 뒷 부분으로 옮겨야 한다.

Prewarming an app results in an indeterminate amount of time between when the prewarming phase completes and when the user, or system, fully launches the app. Because of this, use [MetricKit](https://developer.apple.com/documentation/metrickit) to accurately measure user-driven launch and resume times instead of manually signposting various points of the launch sequence.

앱을 준비하는 것은 준비 단계가 완료되는 때와 사용자 혹은 시스템이 완전히 앱을 실행하는 때 사이에 쉽게 가늠할 수 없는 시간을 야기한다. 그래서 다양한 시작 시점을 수동으로 표시하는 대신 유저가 사용자가 앱을 실행하고 재개하는 것을 정확하게 측정하기 위해 metricKit를 사용할 수 있다.