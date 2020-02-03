---
layout: post
title:  "[Booster 2기] 오토레이아웃이 무엇인지 알아보고 직접 코드로 구현해보기"
date:   2020-01-31
excerpt: "#boostcourse #booster #xcode"
tag:
- boostcourse
- booster
- xcode
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

이제 인터페이스 빌더를 통해 직접 오토레이아웃을 구현해보도록 하겠습니다.

## 코드로 오토레이아웃 구현하기

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>