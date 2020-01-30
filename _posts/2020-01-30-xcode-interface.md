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

인터페이스는 어플리케이션과 사용자가 소통할 수 있도록 해주는 일종의 시스템입니다. 모바일 디바이스에서는 보통 사용자의 터치, 슬라이드 등의 손동작을 통해 어플리케이션을 제어할 수 있도록 합니다. 버튼, 스위치, 툴바 등이 대표적인 인터페이스입니다.

이번에는 어플리케이션의 인터페이스를 구성해보도록 하겠습니다. Xcode 에서는 Main.storyboard 를 눌러 인터페이스를 구성할 수 있습니다. 그러면 다음과 같은 화면이 등장하게 됩니다.

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

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>
