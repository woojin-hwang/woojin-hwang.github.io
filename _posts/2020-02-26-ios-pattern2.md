---
layout: post
title:  "[Booster 2기] iOS 의 다양한 디자인 패턴 알아보기 2"
date:   2020-02-26
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

[[이전 포스트]iOS 의 다양한 디자인 패턴 알아보기 1](https://woojin-hwang.github.io/ios-pattern1/)

---

이전 포스트에서는 iOS 의 델리게이션 디자인 패턴에 대해 알아보았습니다. 이번에는 또 다른 디자인 패턴 중 하나인 싱글톤 패턴에 대해 알아보겠습니다.

### 싱글톤 패턴(Singleton Pattern)

싱글톤 패턴은 특정 클래스의 인스턴스가 오직 하나임을 보장하는 객체를 의미합니다. 즉 어플리케이션 내에서 인스턴스가 반드시 하나만 존재하게 되며 다른 인스턴스들이 이를 공유하면서 사용하게 됩니다. 대표적인 클래스로는 *파일 시스템을 관리하는 FileManager, URL 세션을 관리하는 URLSession, 알림의 정보를 활용할 수 있도록 하는 NotificationCenter, 간단한 데이터를 저장할 수 있도록 하는 UserDefault, 그리고 iOS 에서 중앙제어를 담당하는 UIApplication* 이 있습니다.

클래스들의 역할을 보면 알 수 있듯이 싱글톤 디자인 패턴은 객체가 불필요하게 여러개 존재할 이유가 없을 때 주로 사용합니다. 간단한 예제 코드를 직접 구현해보도록 하겠습니다. 먼저 스토리보드에서 TextField 두개와 Button 하나를 생성해서 다음과 같이 만들어 줍니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/storyboard2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/storyboard2.png"></a>
</figure>

싱글톤 디자인 패턴을 사용해서, 위 텍스트 필드 값을 입력한 후 버튼을 누르면 그 값이 아래 텍스트 필드에 나타나도록 구현해 보겠습니다. 이를 위해서 먼저 새로운 파일을 생성합니다. 저는 UserInformation.swift 를 생성하도록 하겠습니다. 생성한 파일에 다음 코드를 입력합니다.

{% highlight swift %}
import Foundation

class UserInformation {
  static let shared: UserInformation = UserInformation()

  var name: String?
}
{% endhighlight %}

UserInformation 이라는 이름의 클래스를 선언하였습니다. 내부를 잘 보면 shared 라는 프로퍼티가 존재합니다. 이 프로퍼티는 누가 호출하던지 항상 하나의, 같은 인스턴스를 사용하도록 해줍니다. 바로 싱글톤 패턴이 사용되었다고 할 수 있습니다.

다시 ViewController.swift 파일로 돌아와서 이제 레이블과 버튼을 위한 프로퍼티와 메서드를 추가해줍니다. 코드는 다음과 같습니다.

{% highlight swift %}
@IBOutlet weak var inputField: UITextField!
@IBOutlet weak var outputField: UITextField!
    
@IBAction func touchUpSetButton(_ sender: UIButton) {
  UserInformation.shared.name = inputField.text
  self.outputField.text = UserInformation.shared.name
}
{% endhighlight %}

그리고 어플리케이션을 실행하면 원하는 결과를 얻을 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/hello.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/hello.png"></a>
</figure>

위 텍스트 필드에 값을 입력하고 버튼을 클릭하면 아래 텍스트 필드에 결과가 나타납니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/hello2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/hello2.png"></a>
</figure>

만약 이 예시에서 싱글톤 디자인 패턴을 사용하지 않아도 동작하기는 합니다. 즉 UserInformation 클래스 없이 ViewController.swift 의 touchUpSetButton 메서드를 다음과 같이 수정하여도 이 어플리케이션이 동작하기는 합니다. 왜냐하면 이 어플리케이션은 하나의 뷰 컨트롤러에서 동작하기 때문입니다.

{% highlight swift %}
@IBAction func touchUpSetButton(_ sender: UIButton) {
  self.outputField.text = inputField.text
}
{% endhighlight %}

그러나 만약 뷰가 두개 이상이라면 위 코드는 정상적으로 동작하지 않습니다. 결국 모든 뷰에서 공동으로 사용하는 인스턴스가 필요하게 되고, 이 때 싱글톤 디자인 패턴이 유용하게 사용됩니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>