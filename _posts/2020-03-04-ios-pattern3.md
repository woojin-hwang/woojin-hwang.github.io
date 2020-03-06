---
layout: post
title:  "[Booster 2기] iOS 의 다양한 디자인 패턴 알아보기 3"
date:   2020-03-04
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

[[이전 포스트]iOS 의 다양한 디자인 패턴 알아보기 2](https://woojin-hwang.github.io/ios-pattern2/)

---

iOS 프로그래밍에서 자주 사용되는 패턴 중 하나인 타겟-액션 디자인 패턴에 대해 알아보겠습니다.

## 타겟-액션(Target-Action) 패턴

이 디자인 패턴에 대해 알아보기 전에 먼저 타겟과 액션이 각각 무엇을 의미하는지 먼저 알아보겠습니다. 액션이란 특정 이벤트가 발생했을 때 호출할 메서드를 의미합니다. 타겟은 액션이 호출될 객체를 의미합니다. 즉 타겟-액션 디자인 패턴은 이벤트가 발생할 때 객체가 다른 객체에 메세지를 보낼 때 필요한 정보를 포함하는 방식을 말합니다. 이 떄 전송되는 메세지를 액션 메세지라고 합니다.

이 디자인 패턴을 사용하는 이유는 특정 메서드를 호출해야 하는데 이 메서드가 여러 클래스에서 중복으로 정의된 경우가 있을 수 있기 때문입니다. 이 때 원하는 객체를 타겟으로 설정하여 그 메서드를 수행할 객체를 선택할 수 있도록 합니다.

액션 메서드는 다음과 같은 형식으로 정의되어야 합니다.

{% highlight swift %}
@object func doSomething(_ sender: Any) {

}
{% endhighlight %}

어색한 형식일 수도 있겠지만, 사실 이미 이 액션 메서드에 대해 다룬적이 있습니다. 바로 인터페이스 빌더입니다.

{% highlight swift %}
@IBAction func doSomething(_ sender: Any) {

}
{% endhighlight %}

> 인터페이스 빌더는 타겟-액션 디자인 패턴을 사용하고 있습니다.

UIKit 을 상속받고 있는 *UIButton, UISwitch, UIStepper* 등의 컨트롤 클래스에서 발생하는 다양한 컨트롤 이벤트들을 타겟이 되는 액션 메서드에 연결할 수 있습니다. 여기서 컨트롤 이벤트란 touchUpInside, touchDown 등의 이벤트입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/view_controller3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-interface/view_controller3.png"></a>
</figure>

코드로는 다음과 같이 선언할 수 있습니다.

{% highlight swift %}
button.addTarget(self, action: #selector(self.touchUpPlayPauseButton(_:)), for: UIControlEvents.touchUpInside)
{% endhighlight %}

이 코드의 의미는 touchUpInside 이벤트를 button 이라는 프로퍼티에 현재 뷰 컨트롤러 객체(self)를 타겟으로 설정하라는 의미입니다. 이 때 액션은 touchUpPlayPauseButton 이라는 이름의 메서드가 됩니다. 어떤 이벤트가 발생했을 때 타겟을 정하고 액션을 실행하는 것, 이것이 바로 타겟-액션 디자인 패턴이라고 할 수 있습니다.

---

[[다음 포스트]iOS 가 사용자의 제스쳐를 인식하는 방법](https://woojin-hwang.github.io/gesture/)

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>