---
layout: post
title:  "Xcode 의 인터페이스 구성하기"
date:   2020-01-30
excerpt: "#boostcourse #booster #xcode"
tag:
- boostcourse
- booster
- xcode
comments: false
---

[[부스트코스] iOS 프로그래밍 강좌](https://www.edwith.org/boostcourse-ios/)에 대한 정리글입니다.

[[이전 포스트]Xcode 의 에셋 카탈로그(Asset Catalog) 와 앱 시닝(App Thining) 알아보기](https://woojin-hwang.github.io/xcode-asset/))

---

## 인터페이스란?

---

인터페이스는 어플리케이션과 사용자가 소통할 수 있도록 해주는 일종의 시스템입니다. 모바일 디바이스에서는 보통 사용자의 터치, 슬라이드 등의 손동작을 통해 어플리케이션을 제어할 수 있도록 합니다. 버튼, 스위치, 툴바 등이 대표적인 인터페이스입니다.

## 인터페이스 추가하기

---

이번에는 어플리케이션의 인터페이스를 구성해보도록 하겠습니다. Xcode 에서는 **Main.storyboard** 를 눌러 인터페이스를 구성할 수 있습니다. 그러면 다음과 같은 화면이 등장하게 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/storyboard.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/storyboard.png"></a>
</figure>

여기에 인터페이스를 추가해보도록 하겠습니다. 인터페이스를 추가하기 위해서는 가장 위 오른쪽에 있는 **+** 버튼을 누르면 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode/library.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode/library.png"></a>
</figure>

> 라이브러리(Library) 라고 부르는 버튼입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode/library2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode/library2.png"></a>
</figure>

> 버튼을 누르면 이렇게 라이브러리 창이 나타납니다.

여러 인터페이스들 중 원하는 것을 선택해서 더블클릭하거나 에디터 영역으로 끌어다 놓아서 추가할 수 있습니다. 저는 여기에 버튼을 하나 추가해보도록 하겠습니다. 그러면 다음과 같이 에디터 영역에 버튼이 나타나는 것을 볼 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/button.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/button.png"></a>
</figure>

이제 이 버튼의 속성을 바꾸어보도록 하겠습니다. 가장 오른쪽 유틸리티 영역에서 **Show the Attributes inspector** 탭을 눌러줍니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/attributes_inspector.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/attributes_inspector.png"></a>
</figure>

이 버튼을 음악 재생 버튼으로 한번 바꾸어보도록 하겠습니다. Type 을 Custom 으로 변경한 후, Title 은 없애고 Image 를 play.fill 로 변경하고 Configuration 의 Point size 를 원하는 크기만큼 설정합니다. 그러면 다음과 같이 그럴듯한 재생 버튼을 만들 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/button2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/button2.png"></a>
</figure>

같은 방식으로 재생 시간을 나타내기 위한 텍스트와 슬라이더를 추가해보도록 하겠습니다. 그러면 다음과 같이 만들 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/button3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/button3.png"></a>
</figure>

> 지금은 좀 허접할 수도 있지만 디테일적인 부분은 나중에 신경쓰도록 하겠습니다.

## 인터페이스 객체를 코드와 연결하기

---

스토리보드에는 **View Controller** 라는 것이 있습니다. 여기에는 지금까지 만든 버튼, 텍스트레이블, 슬라이더들이 View 로 모두 들어있습니다. 이 View Controller 는 ViewController 라는 클래스의 인스턴스입니다. 이 클래스는 ViewController.swift 소스 파일에 선언되어 있습니다. 코드는 다음과 같습니다.

{% highlight swift %}
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
    }


}
{% endhighlight %}

여기에 원하는 코드를 추가해서 생성한 인터페이스 객체를 코드와 연결할 수 있습니다. 다음 코드를 ViewController 클래스 안에 추가해줍니다.

{% highlight swift %}
@IBOutlet var playPauseButton: UIButton!
@IBOutlet var timeLabel: UILabel!
@IBOutlet var progressSlider: UISlider!
{% endhighlight %}

이것은 위에서 만든 버튼, 텍스트레이블, 슬라이더에 대한 인스턴스 프로퍼티를 생성하는 코드입니다. 여기서 @IBOutlet 은 인터페이스 객체와 코드를 연결시켜주는 모디파이어입니다. 정상적으로 추가했다면 에디터에 다음과 같이 표시됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/iboutlet.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/iboutlet.png"></a>
</figure>

왼쪽에 동그라미가 비어있는 것을 확인할 수 있습니다. 이는 인스턴스 프로퍼티는 정상적으로 생성했지만 아직 인터페이스 객체와 연결되지는 않았다는 뜻입니다. 이는 직접 연결시켜 주어야 합니다. 이 방법에는 크게 3가지가 있습니다.

## 코드에서 직접 연결하기

---

에디터 영역 오른쪽 위에는 이런 모양의 아이콘이 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/split.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/split.png"></a>
</figure>

누르면 하나의 에디터 영역이 두 개로 분할됩니다. 이를 활용해서 왼쪽에는 코드, 오른쪽에는 스토리보드를 띄운 후 코드의 동그라미를 클릭해서 직접 해당 인터페이스에 끌어다 놓아 연결할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/split2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/split2.png"></a>
</figure>

## 스토리보드의 View Controller 에서 연결하기

---

스토리보드의 View Controller 를 이용해서 연결할 수도 있습니다. View Controller 는 Main.storyboard 를 눌렀을 때 View Controller Scene 하위에 있습니다. 또는 가운데 인터페이스 화면 위에 조그마한 3개의 아이콘 중 가장 왼쪽에 있습니다.

View Controller 를 *ctrl 을 누르고 클릭*하면 다음과 같은 창이 나타납니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/view_controller.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/view_controller.png"></a>
</figure>

여기서 원하는 인스턴스 프로퍼티와 인터페이스를 다음과 같이 마우스로 끌어서 연결하면 되겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/view_controller2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/view_controller2.png"></a>
</figure>

## 유틸리티 영역에서 연결하기

---

스토리보드의 View Controller 를 클릭한 상태에서 우측 유틸리티 영역의 **Show the Connections inspector** 를 사용해서 연결할 수도 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/connections_inspector.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/connections_inspector.png"></a>
</figure>

마찬가지로 원하는 인스턴스 프로퍼티와 인터페이스를 마우스로 끌어서 연결하면 되겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/connections_inspector2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/connections_inspector2.png"></a>
</figure>

인스턴스 프로퍼티와 인터페이스를 연결할 때 주의해야 할 것이 있습니다. 만약 연결하고 난 후 인스턴스 프로퍼티의 이름을 변경하게 되면 당연히 에러가 발생합니다. 이 경우 잘못된 연결을 삭제하고 새로 연결을 해 주어야 에러가 발생하지 않습니다.

만약 새로 연결하기가 힘들거나 귀찮은 경우, 변경하고자 하는 인스턴스 프로퍼티를 *오른쪽 마우스 클릭*하여 **Refactor -> Rename** 을 눌러 이름을 변경해주는 방법이 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/refactor_rename.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/refactor_rename.png"></a>
</figure>

> 이렇게 이름을 변경하면 Xcode 가 알아서 새로 연결해줍니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>
