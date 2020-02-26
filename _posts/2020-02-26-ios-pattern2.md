---
layout: post
title:  "[Booster 2기] iOS 의 다양한 디자인 패턴 알아보기 2"
date:   2020-02-25
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

클래스들의 역할을 보면 알 수 있듯이 싱글톤 디자인 패턴은 객체가 불필요하게 여러개 존재할 이유가 없을 때 주로 사용합니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>