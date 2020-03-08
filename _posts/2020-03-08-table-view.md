---
layout: post
title:  "[Booster 2기] iOS 가 사용자의 제스쳐를 인식하는 방법"
date:   2020-03-08
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

[[이전 포스트]iOS 가 사용자의 제스쳐를 인식하는 방법](https://woojin-hwang.github.io/gesture/)

---

iOS 어플리케이션에서 다음과 같은 모습의 인터페이스를 종종 볼 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView1.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView1.png"></a>
</figure>

스크롤을 통해 아래로 내릴 수 있는 리스트 형태의 이 인터페이스를 바로 **테이블뷰(TableView)** 라고 합니다. 테이블뷰는 iOS 어플리케이션에서 자주 사용되는 인터페이스들 중 하나입니다. 이 글에서는 이 테이블뷰에 대해 자세히 알아보도록 하겠습니다.

## 테이블 뷰의 구조

기본적으로 테이블뷰는 여러개의 **행(row)**을 가지고 있습니다. 그러나 단 하나의 열(colume)을 가지고 있기 때문에 수직으로만 스크롤할 수 있습니다. 위의 사진에서 *Display, Motion, Spoken Content, Touch, Face ID & Attention, keyboards* 부분이 해당됩니다.

이 행들은 각각 순서를 가지고 있습니다. *Display* 는 0번 행, *Motion* 은 1번 행, *Spoken Content* 는 2번 행입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView2.png"></a>
</figure>

> 그러면 그 아래의 *Touch* 는 3번행이 될까요?

그러나 *Touch* 는 3번 행이 아니라 다시 0번 행이 됩니다. 왜냐하면 위의 행들과 아래의 행들은 **섹션(Section)**에 의해 나뉘어져 있기 때문입니다. 섹션은 행을 시각적으로 나뉘기 위해 존재합니다.

섹션도 행처럼 순서를 가지고 있습니다. 이 테이블 뷰에는 두개의 섹션이 사용되고 있습니다. 가장 위의 행들이 바로 0번 섹션이 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView3.png"></a>
</figure>

> 0번 섹션의 0번 행, 1번 행, 2번 행

그 아래의 행들은 당연히 1번 섹션이 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView4.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView4.png"></a>
</figure>

> 1번 섹션의 0번 행, 1번 행, 2번 행

이 섹션은 특별한 이름을 가지고 있지 않습니다. 그래서 이 섹션에 텍스트나 이미지를 추가하고 싶을 떄 사용되는 것이 바로 **헤더(header)** 와 **푸터(footer)** 입니다. 헤더는 섹션의 가장 위에, 푸터는 섹션의 가장 아래에 나타납니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView5.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView5.png"></a>
</figure>

이 섹션의 헤더는 *EMOJI* 이고, 푸터는 *Send Memoji and Animoji stickers from your emoji keyboard.* 입니다.

여기까지 테이블뷰의 전체적인 구조에 대해 알아보았습니다. 이제는 테이블뷰의 개별적인 행에 대해 알아보겠습니다.

## 테이블뷰 셀

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView6.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView6.png"></a>
</figure>

테이블뷰에서 행 하나를 **테이블뷰 셀(TableView Cell)** 이라고 합니다. 테이블뷰 셀은 UItableViewCell 을 상속받고 있기 때문에 이 클래스에 정의된 스타일을 통해 셀을 생성할 수 있습니다.

테이블뷰 셀은 기본적으로 두가지 부분으로 나뉩니다. 바로 셀 콘텐츠와 액세사리 뷰 입니다. **셀 콘텐츠(Cell Contents)**는 셀 왼쪽의 이미지와 텍스트로 이루어진 부분입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView7.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView7.png"></a>
</figure>

텍스트는 아래와 같이 주제목과 부제목으로 나뉘기도 합니다. 아래의 1번 행의 경우, 텍스트가 *한국어(대한민국)* 이라는 주제목과 *Korean (South Korea)* 라는 부제목으로 나뉘어져 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView8.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView8.png"></a>
</figure>

UITableView 클래스에는 이 셀 콘텐츠를 위한 프로퍼티가 정의되어 있습니다. 프로퍼티는 아래와 같습니다.

| <center>프로퍼티 이름</center> | <center>타입</center> | <center>역할</center> |
|:--------|:--------|:--------:|
| <center>textLabel</center> | <center>UILabel</center> | <center>주제목 레이블</center> |
| <center>detailTextLabel</center> | <center>UILabel</center> | <center>부제목 레이블</center> |
| <center>imageView</center> | <center>UIImageView</center> | <center>이미지</center> |

**액세사리 뷰(Accessory View)** 는 컨트롤 객체가 위치하는 부분입니다. 컨트롤 객체란 사용자가 원하는 동작을 할 수 있도록 제어하는 부분을 말합니다. 대표적인 컨트롤 객체는 **<** 입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView9.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView9.png"></a>
</figure>

> 터치하면 해당 정보로 이동합니다.

테이블뷰 셀은 편집 모드(Editing Mode)일 경우 모양이 조금 달라집니다. 인터페이스들 중 가장 오른쪽 위에 *Edit* 이나 *편집*버튼이 있는 경우가 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView10.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView10.png"></a>
</figure>

이를 누르면 아래와 같이 편집 모드로 진입할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView11.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView11.png"></a>
</figure>

테이블뷰 셀의 모습이 조금 달라진 것을 확인할 수 있습니다. 액세사리 뷰가 사라지고 왼쪽과 오른쪽에 새로운 컨트롤들이 나타난 것이 보입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView12.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tableView12.png"></a>
</figure>

iOS 를 사용해본 적이 있다면 이는 매우 익숙한 모습입니다. 왼쪽 컨트롤을 눌러 해당 셀을 삭제하거나, 오른쪽 컨트롤을 드래그해서 해당 셀의 위치를 위나 아래로 이동할 수 있습니다. 이 때 왼쪽 컨트롤은 **편집 컨트롤** 이라 하고, 오른쪽 컨트롤은 **재정렬 컨트롤** 이라고 합니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>