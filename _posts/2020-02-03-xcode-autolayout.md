---
layout: post
title:  "[Booster 2기] 오토레이아웃이 무엇인지 알아보고 직접 코드 없이, 또는 코드를 사용해서 구현해보기"
date:   2020-01-31
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

[[이전 포스트]코코아 터치 프레임워크에 대해 알아보기](https://woojin-hwang.github.io/xcode-cocoa/)

---

## 오토레이아웃(Auto Layout) 이란?

---

사람들은 다양한 크기의 아이폰 디바이스들을 사용합니다. *iPhone 4 부터 iPhone 11, iPhone SE, iPhone XS 그리고 iPhone XS MAX* 등 모두 크기나 비율이 제각각인 디바이스들입니다. 그렇기 때문에 어플리케이션이 디바이스 사이즈에 구애받지 않고 동일한 화면을 구성할 필요가 있습니다.

그래서 나온 것이 **오토레이아웃(Auto Layout)** 입니다. 오토 레이아웃은 뷰의 크기와 위치를 동적으로 계산합니다. 즉 인터페이스에 절대적인 좌표가 아닌 상대적인 좌표가 필요할 때 유용합니다.

오토레이아웃이 주로 사용되는 이유는 외부 변경과 내부 변경때문입니다.

### 외부 변경

외부 변경은 슈퍼뷰의 크기나 모양이 변경될 때 발생합니다. 보통 *디바이스를 회전하거나, 다른 크기의 클래스나 스크린을 지원하거나, 아이패드에서 분할 뷰(split view) 를 사용할 때*입니다.

### 내부 변경

내부 변경은 인터페이스 뷰의 크기나 설정이 변경될 때 발생합니다. 보통  *어플리케이션의 컨텐츠가 변경되거나, 국제화를 지원하거나, 동적인 타입을 지원하는 경우*입니다. 예를 들어 신문 기사 어플리케이션의 경우, 이미지나 텍스트를 신문 기사의 레이아웃에 맞게 조정해야 하는 경우입니다.

## 오토레이아웃의 속성

---

그러면 이제 오토 레이아웃의 핵심적인 속성들에 대해 알아보겠습니다.

### 안전 영역(Safe Area)

안전 영역(Safe Area) 은 어플리케이션이 상태바, 네비게이션바, 툴바, 탭바를 가리는 것을 방지하는 영역입니다. 표준 시스템이 제공하는 뷰들은 모두 안전 영역을 준수하고 있습니다.


### 제약(Constraint)

제약(Constraint) 는 뷰와 뷰 사이의 관계를 속성을 통해 정의하는 것을 말합니다. 제약은 위치를 방정식으로 나타냅니다. 이를 이해하기 위해서는 먼저 오토레이아웃의 위치에 대해 알아야 합니다.

오토레이아웃은 정렬 사각형을 기반으로 한 위치 속성을 사용하고 있습니다. 이 위치 속성에는 다음과 같은 것들이 있습니다.

| <center>속성</center> | <center>설명</center> |
|:--------|:--------:|
| <center>Width</center> | <center>너비</center> |
| <center>Height</center> | <center>높이</center> |
| <center>Top</center> | <center>정렬 사각형의 상단</center> |
| <center>Bottom</center> | <center>정렬 사각형의 하단</center> |
| <center>Baseline</center> | <center>텍스트의 하단</center> |
| <center>Leading</center> | <center>텍스트 시작</center> |
| <center>Trailing</center> | <center>텍스트 끝</center> |
| <center>CenterX</center> | <center>수평 중심</center> |
| <center>CenterX</center> | <center>수직 중심</center> |

그러면 제약을 다음과 같이 표현할 수 있습니다.

{% highlight swift %}
B.Leading = 1.0 * A.Trailing + 8.0
{% endhighlight %}

이 제약은 **B 라는 이름의 뷰의 텍스트 시작위치는 A 뷰의 텍스트 끝의 1.0 배에 8.0 을 더한 위치** 라는 의미를 가집니다.

### 고유 콘텐츠 크기(Intrinsic Content Size)

뷰가 원래 가지고 있었던 크기를 고유 콘텐츠 크기(Intrinsic Content Size)라고 합니다. 즉 오토레이아웃에 의해 변경되기 전 원본 크기를 의미합니다.

### 제약 우선도(Constant Priority)

오토레이아웃에서 제약이 가지는 우선도를 말합니다. 만약 제약이 충돌하는 경우, 우선도가 높은 제약부터 레이아웃에 적용됩니다. 고유 콘텐츠 크기보다 뷰가 커지지 않도록 제한하는 **콘텐츠 허깅 우선도(Contents Hugging Priority)** 와, 이와 반대로 작아지지 않도록 제한하는 **콘텐츠 축소 방지 우선도(Contents Compression Resistance Priority)** 가 있습니다.

### 레이아웃 마진(Layout Margin)

레이아웃에 사용되는 기본적인 간격을 말합니다.

여기까지 오토레이아웃의 개념과 속성에 대해 알아보았습니다.

## 인터페이스 빌더로 오토레이아웃 구현하기

---

이제 인터페이스 빌더를 통해 직접 오토레이아웃을 구현해보도록 하겠습니다. 인터페이스 빌더에서 오토레이아웃을 구현하는 방법에는 크게 3가지가 존재합니다.

### 인터페이스 빌더가 알아서 제약 생성하도록 하기

가장 간단하고 쉬운 방법은 인터페이스 빌더가 알아서 제약을 생성하도록 하는 것입니다. 사용자가 기본적인 뷰를 설정하기만 하면 인터페이스 빌더는 그에 최적화된 제약을 스스로 판단해서 생성하게 됩니다.

상단 탭에서 **Editor -> Resolve Auto Layout Issues** 에서 원하는 제약을 추가할 수 있습니다. **Reset to Suggested Constraint** 를 누르면 인터페이스 빌더가 제안하는 제약을 추가합니다. **Add Missing Constrainrs** 를 눌러 인터페이스 빌더가 생각하기에 뷰에 빠진 제약을 추가할 수도 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/resolve_autolayout.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/resolve_autolayout.png"></a>
</figure>

> 상단 탭의 Editor 메뉴 말고 다른 방법으로 제약을 만들수도 있습니다. 이에 대해서는 아래에서 설명하겠습니다.

사용하기 매우 간단하지만 이는 장점이 되기도 하고 단점이 되기도 합니다. 즉 간단히 오토레이아웃을 생성하기에는 적합하지만, 복잡한 레이아웃이나 혹은 개발자가 원하는 특별한 레이아웃이 있다면 이 방법으로 구현하기는 어렵습니다.

### ctrl 클릭으로 제약 생성하기

다음은 ctrl 클릭으로 오토레이아웃을 생성하는 방법입니다. 일반적으로 두개의 뷰 사이의 관계를 만들 때 사용합니다. 만약 버튼과 레이블 사이의 제약을 생성하고 싶다면, 다음과 같이 버튼을 **ctrl 클릭** 한 다음 드래그해서 레이블 위에서 놓으면 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/ctrl_autolayout.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/ctrl_autolayout.png"></a>
</figure>

그러면 다음과 같은 창이 나타납니다. 이 창은 생성가능한 제약들을 보여줍니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/ctrl_autolayout2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/ctrl_autolayout2.png"></a>
</figure>

> 원하는 제약을 선택하면 되겠습니다.

### 툴바를 사용해서 제약 생성하기

툴바를 사용해서 제약을 생성할 수도 있습니다. 툴바는 에디터 영역의 제일 오른쪽 아래 부분에 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/toolbar.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/toolbar.png"></a>
</figure>

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/toolbar2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/toolbar2.png"></a>
</figure>

하나씩 알아보도록 하겠습니다.

첫 번째 도구는 **정렬(Align)** 입니다. 가로 정렬과 세로 정렬, 그리고 그 외의 여러 정렬들을 사용할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/align.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/align.png"></a>
</figure>

> 정렬 도구 옆에 새로고침 모양의 도구는 Update Frame 으로, 레이아웃을 제약에 맞게 업데이트합니다.

두 번째 도구는 **핀(Pin)** 입니다. 뷰의 위치나 크기를 결정합니다. 고정 값으로 설정하거나 화면 크기에 맞춘 비율로 설정할 수도 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/pin.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/pin.png"></a>
</figure>

세 번째 도구는 **리졸브(Resolve)** 입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/resolve.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/resolve.png"></a>
</figure>

잘 보면 알겠지만, **인터페이스 빌더가 알아서 제약 설정하도록 하기** 에서 사용한 메뉴가 동일합니다.

마지막 도구는 **스택(Stack)** 입니다. 이 도구는 스택 뷰를 빠르게 생성하거나 크기를 조정할 수 있도록 도와줍니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/stack.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/stack.png"></a>
</figure>

이렇게 만든 제약들을 확인하고 싶다면, 뷰 목록에서 찾으면 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/view.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/view.png"></a>
</figure>

또는 우측에 사이즈 인스펙터에서 찾을 수도 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/inspector.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/inspector.png"></a>
</figure>

> 여기서 Edit 를 눌러 제약을 수정할 수도 있습니다.

## 코드로 오토레이아웃 구현하기

이번에는 직접 코드를 이용하여 오토레이아웃을 구현해 보도록 하겠습니다. 저는 다음과 같이 버튼과 레이블을 생성해서 시작하도록 하겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/interface.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/interface.png"></a>
</figure>

ViewController.swift 파일에서 @IBOulet 을 통해 버튼과 레이블을 생성한 후 뷰와 연결해줍니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/iboutlet.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/iboutlet.png"></a>
</figure>

### 앵커(Anchor) 를 통해서 오토레이아웃 구현하기

먼저 **앵커(Anchor)**를 통해서 버튼과 레이블을 배치해보도록 하겠습니다. 먼저 오토레이아웃과 기존의 오토리사이징 마스크가 충돌하는 것을 막기 위해 다음 코드를 추가합니다.

{% highlight swift %}
button.translatesAutoresizingMastIntoConstraints = false
{% endhighlight %}

버튼을 중앙에 배치하기 위해 버튼의 수평과 수직 앵커를 뷰 컨트롤러의 뷰의 중앙에 기준을 맞춰 주도록 하겠습니다. 이를 위해 다음 제약을 생성합니다.

{% highlight swift %}
var constraintX: NSLayoutConstraint
constraintX = button.centerXAnchor.constraint(equalTo: self.view.centerXAnchor)

var constraintY: NSLayoutConstraint
constraintY = button.centerYAnchor.constraint(equalTo: self.view.centerYAnchor)
{% endhighlight %}

> NSLayoutConstraint 는 레이아웃 제약에 대한 앵커 프로퍼티입니다.

생성된 제약을 적용하려면 isActive 프로퍼티를 사용하면 됩니다.

{% highlight swift %}
constraintX.isActive = true
constrainY.isActive = true
{% endhighlight %}

레이블도 버튼과 똑같이 중앙에 배치해보도록 하겠습니다. 이를 적용한 전체 코드는 다음과 같습니다.

{% highlight swift %}
import UIKit

class ViewController: UIViewController {
    
    @IBOutlet weak var button: UIButton!
    @IBOutlet weak var label: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        button.translatesAutoresizingMaskIntoConstraints = false
        
        var constraintX: NSLayoutConstraint
        constraintX = button.centerXAnchor.constraint(equalTo: self.view.centerXAnchor)
        
        var constraintY: NSLayoutConstraint
        constraintY = button.centerYAnchor.constraint(equalTo: self.view.centerYAnchor)
        
        constraintX.isActive = true
        constraintY.isActive = true
        
        label.translatesAutoresizingMaskIntoConstraints = false
        
        var buttonConstraintX: NSLayoutConstraint
        buttonConstraintX = label.centerXAnchor.constraint(equalTo: self.view.centerXAnchor)
        
        var buttonConstraintY: NSLayoutConstraint
        buttonConstraintY = label.centerYAnchor.constraint(equalTo: button.topAnchor, constant: -10)
        
        buttonConstraintX.isActive = true
        buttonConstraintY.isActive = true
    }
    
}
{% endhighlight %}
> 레이블의 y 좌표는 버튼의 topAnchor 로부터 10 만큼 위에 있도록 설정하였습니다.

그러면 다음과 같은 결과를 얻을 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/result.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/result.png"></a>
</figure>

Xcode 는 자동완성을 통해 코드로 어떤 제약을 설정할 수 있는지 보여줍니다. 다음과 같이 매개변수를 통해 제약의 위치를 얼마만큼으로 할 것인지, 몇 배로 할 것인지 등을 설정할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/constraints.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/constraints.png"></a>
</figure>

지금까지 NSLayoutConstraint 앵커를 통해 코드로 제약을 생성하여 오토레이아웃을 구현해 보았습니다. 이 외에도 NSLayoutXAxisAnchor 와 같은 여러 프로퍼티들이 있습니다. 이에 대해서는 [Apple 개발자 문서](https://developer.apple.com/documentation/uikit/view_layout) 를 참조하시기 바랍니다.

### 인스턴스로 오토레이아웃 구현하기

이번에는 앵커가 아닌, NSLayoutConstraint 인스턴스를 통해서 오토레이아웃을 구현해 보도록 하겠습니다. NSLayoutConstraint 는 다음과 같이 사용합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/nsconstraints.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-autolayout/nsconstraints.png"></a>
</figure>
 
매개변수가 굉장히 많은것을 알 수 있는데, 이제 하나씩 알아보도록 하겠습니다.

**item** 은 제약을 받기 위한 뷰를 말합니다. 만약 button 에 제약을 추가하는 경우라면 *item: button* 이 값으로 들어가게 됩니다.

**attribute** 는 제약 조건의 속성을 말합니다. *.left, .right, .top, .bottom, .leading, .trailing, .width, .height* 등의 값이 들어갈 수 있습니다.

**relatedBy** 는 제약 조건을 받는 뷰 사이의 관계를 정의합니다. 즉 제약을 특정 값으로 설정하거나, 최소 또는 최대의 범위를 정할 수 있습니다. *.equal, .lessThanOrEqual, .greaterThanOrEqual* 등의 값이 들어갈 수 있습니다.

**toItem** 은 *item* 의 제약을 받는 뷰를 말합니다. button 과 label 사이에 제약을 만드는 경우, *item 을 button 으로, toItem 을 label 으로* 설정할 수 있습니다. 오직 하나의 뷰의 제약을 만드는 경우, nil 값이 들어갈 수도 있습니다.

**multiplier** 는 크기나 위치를 비율로 설정하고자 할 때 사용합니다.

**constraint** 는 크기나 위치를 상수값으로 설정하고자 할 때 사용합니다.

이 매개변수들을 이용해서 원하는 제약을 생성할 수 있습니다. 한번 만들어보도록 하겠습니다.

다음은 버튼의 너비를 50보다 크거나 같도록 설정하는 코드입니다.

{% highlight swift %}
var constantWidthButton: NSLayoutConstraint
constraintWidthButton = NSLayoutConstraint(item: button,
                     attribute: .width,
                     relatedBy: .greaterThanOrEqual,
                     toItem: nil,
                     attribute: .notAnAttribute,
                     multiplier: 1.0,
                     constant: 50.0)
{% endhighlight %}

다음 코드는 레이블의 너비를 버튼과 같게 만드는 코드입니다.

{% highlight swift %}
var constraintWidthLabel: NSLayoutConstraint
constraintWidthLabel = NSLayoutConstraint(item: button,
 			  attribute: .width,
 			  relatedBy: .equal,
 			  toItem: label,
 			  attribute: .width,
 			  multiplier: 1.0,
 			  constant: 0.0)
{% endhighlight %}

버튼과 레이블 사이의 간격을 설정할 수도 있습니다. 여기서는 10 으로 주도록 하겠습니다.

{% highlight swift %}
var constraintMarginButtonWidth: NSLayoutConstraint
constraintMarginButtonWidth = NSLayoutConstraint(item: topField,
 			  attribute: .bottom,
 			  relatedBy: .equal,
 			  toItem: bottomField,
 			  attribute: .top,
 			  multiplier: 1.0,
 			  constant: -10.0)
{% endhighlight %}

이 인스턴스에 우선도를 부여할 수 있습니다. 방법은 다음과 같습니다.

{% highlight swift %}
NSLayoutConstraint(item: topField,
 			  attribute: .bottom,
 			  relatedBy: .equal,
 			  toItem: bottomField,
 			  attribute: .top,
 			  multiplier: 1.0,
 			  constant: -10.0).priority = UILayoutPriority(rawValue: 20)
{% endhighlight %}

우선도는 1 에서 1000 까지의 값을 가질 수 있으며, 두개 이상의 제약이 있다면 그 중 우선도가 높은 제약이 수행됩니다.

### Visual Format Language 를 통해 오토레이아웃 구현하기

이번에는 동일한 제약을 Visual Format Language 를 통해 구현해 보겠습니다. Visual Format Language 는 인스턴스처럼 매개변수로 값을 넘기는 것이 아닌, 특정한 형식에 맞춰서 간단하게 오토레이아웃을 구현할 수 있습니다. 예를 들어 버튼의 너비를 50보다 크거나 같도록 설정하는 코드는 아래와 같이 한 줄로 표현할 수 있습니다.

{% highlight swift %}
H:[button(>=50)]
{% endhighlight %}

버튼과 레이블 사이의 간격을 10으로 설정하는 방법은 다음과 같습니다.

{% highlight swift %}
V:[button]-10-[label]
{% endhighlight %}

이렇게 제약을 간단하고 쉽게 나타낼 수 있습니다. Visual Format Language 를 잘 사용하기 위해서는 여기에 사용되는 기호와 문자열을 알아야 할 필요가 있습니다. 이에 대해서는 아래의 표를 참조하시기 바랍니다.

| <center>기호 및 문자열</center> | <center>설명</center> |
|:--------|:--------:|
| <center>|</center> | <center>슈퍼뷰를 의미합니다.</center> |
| <center>-</center> | <center>표준 간격입니다. (8포인트)</center> |
| <center>==</center> | <center>같은 너비입니다.</center> |
| <center>-10-</center> | <center>사이의 간격이 10포인트 입니다.</center> |
| <center><=50</center> | <center>50보다 작거나 같습니다.</center> |
| <center>>=50</center> | <center>50보다 크거나 같습니다.</center> |
| <center>@750</center> | <center>우선도를 750으로 지정합니다.</center> |
| <center>H</center> | <center>수평 방향입니다.</center> |
| <center>V</center> | <center>수직 방향입니다.</center> |

Visual Format Language 에 대한 더 많은 예시는 [Apple 개발자 문서](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/VisualFormatLanguage.html#//apple_ref/doc/uid/TP40010853-CH27-SW1) 에서 찾을 수 있습니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>