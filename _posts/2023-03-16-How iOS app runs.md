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

```
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
> @autoreleasepool{} : 블록 내부의 객체의 release message를 연기했다가 블록이 끝날 때,  release message를 보낸다. 참조 카운트의 감소를 미루


### UIApplicationMain() 함수
<hr/>

UIApplicationMain() 함수는 iOS 앱의 엔트리 포인트라고 할 수 있을 정도로 매우 중요하며, 함수의 선언은 다음과 같다. (Objective-C, Swift)    
```
int UIApplicationMain(int argc, char * _Nullable *argv, NSString *principalClassName, NSString *delegateClassName);
```
```
func UIApplicationMain(
    _ argc: Int32,
    _ argv: UnsafeMutablePointer<UnsafeMutablePointer<CChar>?>,
    _ principalClassName: String?,
    _ delegateClassName: String?
) -> Int32
```

UIApplicationMain() 함수의 파라미터는 argc, argv, principalClassName, delegateClassName 이 있다.    
argc와 argv는 대부분 main() 함수의 인자와 일치하며 각각 argv의 개수, arguments의 변수 리스트이다.    
principalClassName은 UIApplication 클래스(혹은 서브 클래스)의 이름이다. 만약 이 값이 nil인 경우, UIApplication으로 가정된다.    
delegateClassName은 인스턴스화될 delegate의 클래스 이름이다.    
UIApplicationMain() 함수의 반환형은 int이지만, 이 함수는 결코 반환하지 않는다. 홈 버튼을 눌러 앱을 나가더라도, 앱은 백그라운드로 넘어간다.    

> 만약 principalClassName에 UIApplication의 서브 클래스를 지정하면 delegateClassName에도 그 서브 클래스가 지정되며, 서브 클래스의 인스턴스는 application-delegate 메시지를 받는다.    
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
UIApplication 객체는 open windows(UIWindow 객체)를 유지함으로써, 앱의 UIView 객체를 다시 불러올 수 있다.
UIApplication class는 UIApplicationDelegate 프로토콜을 준수하고 프로토콜의 특정 메서드를 반드시 실행하는 delegate를 정의한다. 그리고 그 UIApplication 객체는 그 delegate에게 적절하게 대응할 수 있도록 중요한 runtime events(앱 실행, 메모리 부족 경고, 앱 종료)를 전달한다.    
앱들은 서로 리소스(이미지 파일, 이메일)를 특정 메서드를 통해 협력적으로 관리한다.    
예를 들면 앱은 이 메서드에 이메일 주소를 전달하여 메일 앱을 실행하고 메시지를 보여줄 수 있다.
UIApplication 클래스의 API들은 디바이스의 특정 동작을 다룰 수 있다.    
(예를 들어 일시적으로 터치 이벤트의 입력을 중단, 푸시 알림 설정, 실행 취소 및 되돌리기,  URL scheme을 처리하기 위해 등록된 앱이 있는지 확인, 백그라운드에서 작업을 마칠 수 있도록 앱의 실행 연장, 로컬 알림 설정 및 해지, 원격 컨트롤 이벤트 수신 조정, 앱 상태 복구)
대부분의 앱은 UIApplication를 서브 클래스할 필요가 없으며, 대신 시스템과 앱의 상호작용을 관리하기 위해 app delegate를 사용한다.    
매우 드문 경우 만약 앱이 시스템보다 먼저 데이터 수신을 다뤄야 할 때, UIApplication을 서브 클래스하고 sendEvent: 또는 sendAction:to:from:forEvent: 메서드를 오버라이드 하여 사용 지정 이벤트나 action dispatching 메커니즘을 수행할 수 있다. 가로챈 이벤트를 처리한 후에는 super.sendEvent(event) 메서드를 호출하여 시스템에 다시 돌려줘야 한다. 이벤트를 가로채는 것은 극히 일부여야 하며 가능한 한 피하는 것이 좋다.
UIApplication 객체는 사실상 앱 그자체이며 커스텀 코드와 앱의 기능이라 생각하는 것들은 다 UIApplication에 포함된 하위 객체이다.    
앱을 실행하면 초기 구동 과정을 거쳐 앱 프로세스가 메모리에 올라가는데, 이때의 앱 프로세스가 곧 UIApplication 객체라고 봐도 무방하다.   

### AppDelegate
<hr/>

AppDelegate 또한 UIApplication과 마찬가지로 앱내에서 단 하나의 인스턴스만 생성된다.    
또한 앱이 처음 만들어질 때 객체가 생성되고 앱이 종료되면 소멸된다. 앱과 생명 주기를 함께 한다.    
따라서 AppDelegate 객체에 데이터를 저장하면 앱이 종료될 때까지 데이터를 유지할 수 있다.    

### @main
그런데 Swift 기반의 xCode 프로젝트를 생성해도 우리가 위에서 배웠던 main.m 파일을 찾을 수 없다.    
이는 UIKit 프레임워크 안에 main 함수 구현을 숨겼기 때문인데, 우리는 대신 이를 @main 어노테이션으로 대체한다.    

이후 이벤트 루프를 만드는 등 실행에 필요한 준비를 진행하고, 실행 완료 직전, AppDelegate의 application(\_:didFinishLaunchingWithOptions:) 메소드를 호출하며 앱은 실행된다.    

수정중..
