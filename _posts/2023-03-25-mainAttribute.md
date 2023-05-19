---
layout: single
categories:
  - iOS
title: "@main과 @UIApplicationMain"

---

### @main과 @UIApplicationMain

<hr/>

Swift 기반 xCode 프로젝트에서는 Entry Point 역할을 하는 main() 함수가 보이지 않는다. UIKit 프레임워크 속에 구현되있기 때문이다.

@main 은 이 앱이 어디서 최초 시작할지 명시해주는 키워드이다.

이 어노테이션은 Swift 5.3 이상(xCode12)부터 사용된 키워드이고, 이전에는 @UIApplicationMain 키워드를 사용함

```swift
import UIKit

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
...
}
```

```swift
import SwiftUI

@main
struct SwiftUIApp: App {
...
}
```

이렇게 UIKit의 라이프사이클로 앱을 만들면 AppDelegate 클래스에 @main이 붙는다.

SwiftUI 라이프사이클을 따르는 앱을 만들면 App 구조체에 @main이 붙는다.

SwiftUIApp 구조체는 앱 실행 시 처음 마주치는 AppDelegate와 비슷한 역할이기에 여기를 시작 진입점으로 기본 설정됨.

@UIApplication 이노테이션은 앱의 라이프사이클을 관리하기 위한 UIApplication 객체 생성을 위한 키워드

그런데 SwiftUI로 구성된 앱 진입점에 해당 키워드를 사용하면 에러 발생

해당 키워드는 오직 클래스에서 선언됨

@main : Type-Based program entry points

이를 사용하면 top-level 코드 작성을 대체 할 수 있음

Top-level 코드

The top-level code in a Swift source file consists of zero or more statements, declarations, and expressions. By default, variables, constants, and other named declarations that are declared at the top-level of a source file are accessible to code in every source file that’s part of the same module. You can override this default behavior by marking the declaration with an access-level modifier, as described in [Access Control Levels](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations#Access-Control-Levels).

There are two kinds of top-level code: top-level declarations and executable top-level code. Top-level declarations consist of only declarations, and are allowed in all Swift source files. Executable top-level code contains statements and expressions, not just declarations, and is allowed only as the top-level entry point for the program.

The Swift code you compile to make an executable can contain at most one of the following approaches to mark the top-level entry point, regardless of how the code is organized into files and modules: the `main` attribute, the `NSApplicationMain` attribute, the `UIApplicationMain` attribute, a `main.swift` file, or a file that contains top-level executable code..

스위프트 파일에서 탑-레벨. 코드는 0개. 이상의 statements, 선언, 표현으로 구성된다. 기본적으로 탑-레벨 소스파일에 선언된 변수, 상수 그리고 그외 선언들은 동일 모듈의 일부인 모든 소스 파일에서 접근할 수 있다. You can override this default behavior by marking the declaration with an access-level modifier, as described in [Access Control Levels](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/declarations#Access-Control-Levels).

탑레벨 코드에는 탑레벨 선언과 실행가능 탑레벨 코드 두종류가 있다. 탑레벨 코드는 선언으로만 구성되며 모든 스위프트 파일에서 허락되어짐. 실행가능한 탑레벨 코드는 스테이트먼트와 표현, 선언 포함, 그리고 프로그램의 탑레벨 엔트리포인터에서만 허락되어짐.

실행파일을 만들기위해 너가 컴파일하는 스위프트코드는 어떻게 코드가 파일과 모듈로 조직화되어졌는지와 관계없이 탑레벨인트리 포인트를 표시하기 위에 다음중에 하나를 포함할 수 있다. 메인 어트리뷰트, NSApplicationMain 어트리뷰트, UIApplicationMain 어트리뷰트, main.swift 파일, 실행가능한 탑레벨 코드를 포함하는 파일..

objective-c에서 swift로 언어가 넘어오면서 main.swift에서 main 함수를 관리함과 동시에 uikit 프레임워크에 이 main함수를 넣고 관리하고 우리는 @uiapplicationmain 키워드를 사용

<https://github.com/apple/swift-evolution/blob/main/proposals/0281-main-attribute.md>

<https://medium.com/@abedalkareemomreyh/what-is-main-in-swift-bc79fbee741c>

<https://docs.swift.org/swift-book/ReferenceManual/Declarations.html>

<https://developer.apple.com/documentation/uikit/1622933-uiapplicationmain>

@uiapplicationmain attribute는 이 코드를 대체

```
func main(argc: Int32, argv: UnsafeMutablePointer<UnsafeMutablePointer<Int8>?>) -> Int32 {
   return UIApplicationMain(argc, argv, nil, "AppDelegate")
}
```

attribute와 annotation : 스위프트에서는 어트리뷰트
