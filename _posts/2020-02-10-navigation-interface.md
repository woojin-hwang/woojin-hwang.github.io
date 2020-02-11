---
layout: post
title:  "[Booster 2기] 내비게이션 인터페이스에 대해 알아보고 직접 구현해보기"
date:   2020-02-10
excerpt: "#boostcourse #booster #xcode #swift"
tag:
- boostcourse
- booster
- xcode
- swift
comments: false
---

[[부스트코스]iOS 프로그래밍 강좌](https://www.edwith.org/boostcourse-ios/)에 대한 정리글입니다.

[[부스트코스]iOS 프로그래밍 Booster 2기 활동](https://woojin-hwang.github.io/boostcourse-ios/) 글입니다.

[[이전 포스트]iOS 의 디자인패턴, MVC 에 대해 간단하게 알아보기](https://woojin-hwang.github.io/mvc/)

---

iOS 어플리케이션에서 화면 전환을 할 떄 여러가지 방법이 사용됩니다. 그 중 하나인 **내비게이션 인터페이스**는 주로 계층적 구조의 화면 전환을 위해 사용되는 인터페이스입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/settings2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/settings2.png"></a>
</figure>

> 화면 하단의 툴바를 사용하는 경우도 있습니다.

이는 선택할 수 있는 항목들이 있고, 그것의 세부항목들이 존재하는 방식입니다. iOS 의 설정 화면에 가장 대표적인 예시입니다. 설정에는 화면 설정, 소리 설정 등 수 많은 항목들이 있습니다. 그리고 그 안에도 여러 세부 항목들이 존재합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/settings.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/settings.png"></a>
</figure>

> 아이폰의 설정 화면입니다.

이제 내비게이션 인터페이스를 구성하기 위한 개념들을 알아보고 실제로 구현해보도록 하겠습니다.

### 내비게이션 컨트롤러

**내비게이션 컨트롤러**는 다른 뷰 컨트롤러를 관리하는 컨테이너 뷰 컨트롤러입니다. 내비게이션 스택을 통해 콘텐츠를 보여주며, 이 떄 스택에 담긴 뷰 컨트롤러를 **컨텐트 뷰 컨트롤러**라고 합니다. 내비게이션 컨트롤러는 두개의 뷰를 화면에 표시합니다. 하나는 스택에 들어있는 최상위 컨텐트 뷰 컨트롤러의 뷰입니다. 다른 하나는 내비게이션 컨트롤러가 직접 관리하는 뷰입니다.

다음은 내비게이션 컨트롤러의 인스턴스를 생성하는 메서드입니다.

{% highlight swift %}
// 매개변수로 가장 하위의 뷰 컨트롤러를 넘겨줍니다.
init(rootViewController: UIViewController)
{% endhighlight %}

### 내비게이션 스택

보통 스택이라고 하는 것은 먼저 들어간 데이터가 나중에 나오고, 나중에 들어간 데이터가 처음으로 나오는 구조입니다. **내비게이션 스택**이란 뷰 컨트롤러를 담을 수 있는 스택을 말합니다. 가장 먼저 추가된 뷰 컨트롤러는 가장 하위의 루트 뷰 컨트롤러가 되고, 가장 나중에 추가된 뷰 컨트롤러는 최상위 뷰 컨트롤러가 되어 화면에 보이게 됩니다. 다음은 내비게이션 스택의 뷰 컨트롤러에 접근하기 위한 프로퍼티들입니다.

{% highlight swift %}
// 최상위 뷰 컨트롤러에 접근합니다.
var topViewController: UIViewController?

// 현재 보이는 뷰의 컨트롤러에 접근합니다.
var visibleViewController: UIViewController?

// 특정 뷰 컨트롤러에 접근하기 위한 프로퍼티입니다.
// 루트 뷰 컨트롤러의 인덱스를 0 으로 해서 1씩 증가한 인덱스를 사용합니다.
var viewController: [UIViewController]
{% endhighlight %}

뷰 컨트롤러를 스택에 추가하는 것을 **푸쉬(push)**라고 하며, 반대로 제거하는 것을 **팝(pop)**이라고 합니다. 이에 관한 메서드는 다음과 같습니다.

{% highlight swift %}
// 내비게이션 스택에 뷰 컨트롤러를 푸시합니다.
func pushViewController(UIViewController, animated: Bool)

// 내비게이션 스택에 있는 최상위 뷰 컨트롤러를 팝합니다.
func popViewController(animated: Bool) -> UIViewController?

// 내비게이션 스택에서 루트 뷰 컨트롤러를 제외한 모든 뷰 컨트롤러를 팝합니다.
// 이 때 루트 뷰 컨트롤러가 최상위 뷰 컨트롤러가 되며, 삭제된 모든 뷰 컨트롤러는 배열로 반환됩니다.
func popToRootViewController(animated: Bool) -> [UIViewController]?

// 특정 뷰 컨트롤러가 최상위 뷰 컨트롤러가 되기 전까지 상위에 있는 모든 뷰 컨트롤러들을 팝합니다.
// 루트 뷰 컨트롤러의 인덱스를 0 으로 해서 1씩 증가한 인덱스를 사용합니다.
func popToViewController(_ viewController: UIViewController, animated: Bool) -> [UIViewController]?
{% endhighlight %}

### 네비게이션 인터페이스 구현하기

그럼 이제 직접 네비게이션 인터페이스를 구현해보도록 하겠습니다. 이를 위해 ViewTransition 이라는 이름의 새로운 프로젝트를 생성합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_transition.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_transition.png"></a>
</figure>

여기서 우측 상단의 **+** 버튼, 즉 라이브러리 버튼을 눌러 새로운 View Controller 를 찾습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller.png"></a>
</figure>

> 단축키는 *option + command + shift + L* 입니다.

View Controller 를 스토리보드로 가져옵니다. 그러면 다음과 같이 스토리보드에 뷰 컨트롤러가 추가됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller2.png"></a>
</figure>

이 뷰 컨트롤러는 아직 아무것도 할 수 없는 상태에 있습니다. 그래서 이번엔 새로 만든 뷰 컨트롤러의 클래스를 생성하고, 직접 연결해보도록 하겠습니다. 이를 위해서는 새로운 클래스 파일을 생성해야 합니다. 상단 탭에서 **File -> New -> File...** 을 누르면 새로운 파일을 생성할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file.png"></a>
</figure>

> 단축키는 *command + N* 입니다.

템플릿은 Cocoa Touch class 를 선택합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file2.png"></a>
</figure>

클래스 이름은 SecondViewController 로 하도록 하겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file3.png"></a>
</figure>

그러면 다음과 같이, 현재 프로젝트 안에서 새로운 `swift` 클래스 소스 파일이 생성되는 것을 볼 수 있습니다. 이름은 아까 정한 SecondViewController 가 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file4.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/new_file4.png"></a>
</figure>

클래스는 성공적으로 생성했지만 아직 끝난 것은 아닙니다. 아까 스토리보드에서 생성한 뷰 컨트롤러 인스턴스와 클래스를 연결해주어야 합니다. 이를 위해 스토리보드로 이동한 후 새로 생성한 뷰 컨트롤러를 클릭합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller3.png"></a>
</figure>

이 상태에서 우측 인스펙터의 클래스를 SecondViewController 로 설정해주면 클래스가 해당 인스턴스와 연결이 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller4.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/view_controller4.png"></a>
</figure>

이제 두 뷰 컨트롤러를 연결해보도록 하겠습니다. 이를 위해서는 먼저 상단 탭에서 **Editor -> Embed In -> Navigation Controller** 를 눌러 스토리보드에 내비게이션 컨트롤러를 추가해야 합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller.png"></a>
</figure>

> 만약 해당 메뉴가 활성화되어있지 않다면, 뷰 컨트롤러를 누른 상태에서 새로 시도해보시기 바랍니다.

그러면 다음과 같이 성공적으로 내비게이션 컨트롤러가 스토리보드에 추가됩니다. *왼쪽은 내비게이션 컨트롤러, 중앙은 기존의 뷰 컨트롤러, 그리고 오른쪽은 새로 생성한 뷰 컨트롤러입니다.*

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller2.png"></a>
</figure>

새로운 뷰 컨트롤러를 연결하기 위해 여기서는 버튼을 사용하도록 하겠습니다. View Controller 에 버튼을 추가한 후, 해당 버튼을 누르면 Second View Controller 로 이동하는 방식입니다. 버튼을 생성하고 해당 버튼을 **ctrl 클릭**한 상태에서 새로 생성한 뷰 컨트롤러로 이동한 후 놓습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller4.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller4.png"></a>
</figure>

그러면 다음 창이 나타나게 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/segue.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/segue.png"></a>
</figure>

이것은 Action Segue 를 통해 내비게이션 인터페이스를 구현할 수 있도록 하는 창입니다. 이 중에서 **Show** 는 푸쉬를 통해 내비게이션 스택에 뷰를 쌓는 가장 일반적인 방법입니다. 이것을 선택하도록 하겠습니다. 그러변 다음과 같이 내비게이션 인터페이스가 생성됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/navigation_controller3.png"></a>
</figure>

성공적으로 생성된 상태입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/button.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/button.png"></a>
</figure>

버튼을 클릭했을 때 정상적으로 다음 뷰로 이동합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/back.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/navigation-interface/back.png"></a>
</figure>

지금까지 인터페이스와 Action Segue 를 통해 내비게이션 인터페이스를 구현해보았습니다.

---

[[다음 포스트]모달 알아보기](https://woojin-hwang.github.io/modal/)

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>