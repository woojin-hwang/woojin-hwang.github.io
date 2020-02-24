---
layout: post
title:  "[Booster 2기] 뷰의 상태변화를 감지하는 메서드 알아보기"
date:   2020-02-24
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

[[이전 포스트]모달 알아보기](https://woojin-hwang.github.io/modal/)

---

이전 포스트에서는 내비게이션 인터페이스나 모달을 활용해서 뷰를 이동시키는 것을 구현해 보았습니다. 이번에는 이러한 뷰 상태변화가 일어날 때 이를 감지할 수 있는 메서드들에 대해 알아보겠습니다.

**뷰 상태변화 메서드**란 뷰가 사라지거나 나타나는 등 뷰의 상태변화가 일어날 때 호출되는 메서드를 말합니다. ViewController 파일을 생성할 때 Xcode 가 자동으로 만들어주는 viewDidLoad 메서드가 대표적인 뷰 상태변화 메서드입니다.

{% highlight swift %}
override func viewDidLoad() {
    super.viewDidLoad()
}
{% endhighlight %}

**viewDidLoad** 메서드는 뷰 계층이 메모리에 로드된 직후 호출되는 메서드를 말합니다. 뷰가 화면에 나타나기 전이며, 여러 초기 작업들을 처리하기에 적합합니다. 처음에 한번만 호출되는 메서드입니다.

여기서 주의해야 할 점은 메서드 안에 반드시 super 키워드를 사용해서 해당 메서드를 호출해 주어야 한다는 것입니다. 이는 해당 클래스에서 메소드를 실행하기 전에, 부모 클래스의 메서드를 먼저 수행하도록 합니다. 가능하면 써주는 것이 좋은 코딩 습괍입니다.

이 외에도 다양한 메서드가 존재합니다. 한번 알아보도록 하겠습니다.

{% highlight swift %}
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(_ animated: Bool)
}
{% endhighlight %}

**viewWillAppear** 메서드는 뷰가 뷰 계층에 추가되어 화면에 나타나기 직전에 호출되는 메서드입니다. viewDidLoad 가 한번만 호출되는 것과는 달리 여러번 호출됩니다. 그래서 다른 뷰로 이동했다가 다시 돌아올 때 수행해야 하는 작업이 있으면 이 메서드를 통해 수행할 수 있습니다.

{% highlight swift %}
override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(_ animated: Bool)
}
{% endhighlight %}

**viewDidAppear** 는 뷰가 화면에 나타났을 때 호출되는 메서드입니다.

{% highlight swift %}
override func viewWillDisappear(_ animated: Bool) {
    super.viewWillDisappear(_ animated: Bool)
}
{% endhighlight %}

**viewWillDisappear** 메서드는 뷰가 뷰 계층에서 사라지기 직전에 호출되는 메서드입니다. 보통 뷰에서 일어난 변화들을 다시 초기 상태로 돌려야 할 떄 이 메서드를 활용합니다.

{% highlight swift %}
override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(_ animated: Bool)
}
{% endhighlight %}

**viewDidDisappear** 메서드는 뷰가 뷰 계층에서 사라진 후 호출되는 메서드입니다.

뷰 말고도 레이아웃의 변화를 감지하는 메서드들도 존재합니다. 대표적인 메서드는 viewWillLayoutSubviews 와 viewDidLayoutSubviews 입니다.

{% highlight swift %}
override func viewWillLayoutSubviews() {
    super.viewWillLayoutSubviews()
}
{% endhighlight %}

**viewWillLayoutSubviews** 메서드는 뷰가 서브뷰의 레이아웃을 변경하기 직전에 호출되는 메서드입니다.

{% highlight swift %}
override func viewDidLayoutSubviews() {
    super.viewDidLayoutSubviews()
}
{% endhighlight %}

**viewDidLayoutSubviews** 메서드는 뷰가 서브뷰의 레이아웃을 변경한 후에 호출되는 메서드입니다.

지금까지 뷰 또는 레이아웃 감지 메서드들에 대해 알아보았습니다. 이번에는 직접 코드를 통해 메서드들이 호출되는 순서에 대해 알아보겠습니다. 이를 위해 다음과 같은 모달을 먼저 생성합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/interface.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/interface.png"></a>
</figure>

> 해당 모달을 생성하는 방법에 대해서는 [여기](https://woojin-hwang.github.io/modal/) 를 참조하시기 바랍니다.

그리고 뷰 컨트롤러의 클래스에 다음과 같은 코드를 추가합니다. 저는 viewController.swift 에 다음 코드를 추가하였습니다.

{% highlight swift %}
override func viewDidLoad() {
        super.viewDidLoad()
        print("ViewController: viewDidLoad")
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        print("ViewController: viewWillAppear")
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        print("ViewController: viewDidAppear")
    }
    
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        print("ViewController: viewWillDisappear")
    }
    
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        print("ViewController: viewDidDisappear")
    }
    
    override func viewWillLayoutSubviews() {
        super.viewWillLayoutSubviews()
        print("ViewController: viewWillLayoutSubviews")
    }
    
    override func viewDidLayoutSubviews() {
        super.viewDidLayoutSubviews()
        print("ViewController: viewDidLayoutSubviews")
    }
{% endhighlight %}

> 상태변화 감지 메서드가 호출되면 호출되었다는 것을 확인할 수 있게 메세지를 출력하도록 하였습니다.

모달 클래스에도 마찬가지로 코드를 추가해줍니다. 저는 SecondViewController.swift 클래스에 다음 코드를 추가하였습니다.

{% highlight swift %}
override func viewDidLoad() {
        super.viewDidLoad()
        print("SecondviewController: viewDidLoad")
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        print("SecondViewController: viewWillAppear")
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        print("SecondViewController: viewDidAppear")
    }
    
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        print("SecondViewController: viewWillDisappear")
    }
    
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        print("SecondViewController: viewDidDisappear")
    }
    
    override func viewWillLayoutSubviews() {
        super.viewWillLayoutSubviews()
        print("SecondViewController: viewWillLayoutSubviews")
    }
    
    override func viewDidLayoutSubviews() {
        super.viewDidLayoutSubviews()
        print("SecondViewController: viewDidLayoutSubviews")
    }
{% endhighlight %}

> 출력하는 메세지가 조금 달라졌다는 것에 주의하시기 바랍니다.

그리고 어플리케이션을 처음 수행하면 다음과 같은 메세지를 확인할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg1.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg1.png"></a>
</figure>

이는 처음 뷰가 화면에 나타날 때까지 수행된 메서드입니다. 여기서 버튼을 눌러 모달을 띄우면 다음과 같은 메세지가 추가적으로 나타납니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg2.png"></a>
</figure>

흥미로운 점은 LayoutSubviews 에 대한 메서드들이 두번씩 수행되었다는 점입니다. 이는 클래스 내부에 선언된 메서드에 따라 달라질 수 있습니다. 어느 메서드들은 수행될 때 LayoutSubviews 를 호출하는 경우가 있습니다. 이 때문에 LayoutSubviews 메서드가 두번이 아닌 세번이나 네번씩 수행될 수도 있습니다.

모달을 종료하면 다음과 같은 메세지를 확인할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg3.png"></a>
</figure>

모달의 뷰가 종료된 것을 확인할 수 있습니다.

기존 뷰 위에 새로운 뷰를 띄우는 모달 방식이 아닌, 다른 뷰로 전환하는 내비게이션 인터페이스 방식이라면 어떨까요? 확인하기 위해 다음과 같이 뷰를 구성했습니다. 버튼을 누르면 다음 뷰로 이동하는 방식입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/interface2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/interface2.png"></a>
</figure>

> 내비게이션 인터페이스에 대해서는 [여기](https://woojin-hwang.github.io/navigation-interface) 를 참조하시기 바랍니다.

처음 뷰가 등장했을 때는 당연하게도 동일한 메세지를 출력합니다. 그러나 버튼을 눌러 뷰를 이동했을 때 달라진 메세지를 확인할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg4.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg4.png"></a>
</figure>

ViewController 에서 viewWillDisappear 메서드와 viewDidDisappear 메서드가 추가된 것을 확인할 수 있습니다. 즉 모달과는 다르게 이전 뷰가 사라지는 것을 확인할 수 있습니다. 이는 이전 화면으로 돌아가기를 눌렀을 때도 마찬가지입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg5.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/view-behavior/msg5.png"></a>
</figure>

이전 뷰가 사라진 상태였으므로 새로 뷰를 생성해서 화면에 나타나도록 하는 것을 확인할 수 있습니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>