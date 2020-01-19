---
layout: post
title:  "Xcode 에셋 카탈로그(Asset Catalog) 와 앱 시닝(App Thining)"
date:   2020-01-19
excerpt: "Xcode 에셋 카탈로그와 앱 시닝 기초 알아보기"
tag:
- Xcode
- BoostCourse
comments: false
---

<center>Xcode 에셋 카탈로그와 앱 시닝 기초 알아보기<br></center>

[[부스트코스]iOS 프로그래밍 강좌](https://www.edwith.org/boostcourse-ios)를 참고하였습니다.

[프로젝트에 이미지 추가하기](https://www.edwith.org/boostcourse-ios/lecture/16842/)에 대한 정리글입니다.

## 에셋 카탈로그(Asset Catalog)란?

---

어플리케이션을 개발할 때는 수 많은 리소스(Resource) 파일들이 필요합니다. 리소스 파일이란 *이미지 파일이나, 음악 파일, 또는 그 외의 여러 파일 형식들*을 말합니다. 그러나 이 리소스 파일들을 그대로 사용할 수는 없습니다. 디바이스마다 필요로 하는 크기나 비율이 다르기 때문입니다.

> iPhone 과 iPad 에서 어플리케이션이 똑같이 작동하려면 이미지 크기가 조금씩 달라야겠죠?

Xcode 에서는 이를 해결하기 위해 에셋(Asset) 을 사용합니다. 에셋은 다양한 디바이스들에서 사용하기 위해 여러 파일로 이루어져 있습니다. 예를 들어 iPhone 과 iPad 둘 다에서 동일한 이미지를 사용하기 위해 이미지 에셋을 만들 수 있습니다.

**에셋 카탈로그(Asset Catalog)** 는 에셋을 관리하기 위한 폴더입니다. Xcode 에서 처음 프로젝트를 생성하면 Assets.xcassets 폴더가 생성되는데, 이 폴더를 에셋 카탈로그라고 하며, 다양한 에셋들을 관리할 수 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/asset_catalog.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/asset_catalog.png"></a>
</figure>

> 왼쪽에 보이는 Assets.xcassets 폴더가 바로 에셋 카탈로그입니다. 아직은 에셋이 없는 상태입니다.

에셋 카탈로그에 대해서 더 많은 것들을 알고 싶으시다면 [애플 공식 문서](https://help.apple.com/xcode/mac/current/#/dev10510b1f7) 를 참조하시기 바랍니다.

## 에셋 카탈로그의 종류

---

에셋 카탈로그는 여러 종류가 있지만, 대표적으로 *App Icon Type, Image Set Type, Data Set Type, Launch Image Type* 이 있습니다.

**App Icon Type** 은 어플리케이션 아이콘에 사용되는 이미지입니다. 확장자는 .appiconset 입니다.

**Image Set Type** 은 객체가 사용하는 이미지 파일입니다. .imageset 확장자를 사용합니다.

**Data Set Type** 은 객체가 사용하는 모든 종류의 파일입니다. .dataset 확장자를 사용합니다. 일반적으로 모든 바이너리 파일을 말하지만, 실행파일(executable file)은 사용할 수 없습니다.

**Launch Image Type** 은 어플리케이션이 실행될 때 사용되는 이미지 파일입니다. .launchimage 확장자를 사용합니다.

그 외의 종류들에 대해서는 [여기](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_ref-Asset_Catalog_Format/AssetTypes.html)를 참조하시기 바랍니다.

## 에셋 카탈로그에 이미지 추가하기

---

그럼 간단하게 에셋 카탈로그에 사과 이미지 파일을 추가해보도록 하겠습니다.

간단합니다. Xcode 에 사진을 드래그 드롭으로 끌어서 놓으면 됩니다. 그러면 다음과 같이 이미지 에셋이 추가가 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_apple1.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_apple1.png"></a>
</figure>

또는 화면 하단에 **+** 버튼을 눌러 New Image Set 을 클릭할 수도 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_new_image_set.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_new_image_set"></a>
</figure>

iPad 등의 기기를 위해 2x 와 3x 크기를 추가하도록 하겠습니다. 이 방법도 간단합니다. 사과를 복사해서 붙여넣으면 다음과 같이 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_apple3.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_apple3.png"></a>
</figure>

폴더를 만들어 그룹별로 관리할 수도 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_apple_group.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/xcode-asset/xcode_apple_group.png"></a>
</figure>

## 앱 시닝(App Thining)

---

**앱 시닝(App Thining)** 이란 어플리케이션이 설치될 때 디바이스에 최적화되어 설치될 수 있도록 하는 기술을 말합니다. 어플리케이션의 설치 용량을 줄이고 다운로드 시간을 줄일 수 있습니다. 앱 시닝의 요소로는 *슬라이싱(Slicing), 비트코드(Bitcode), 주문형-리소스(ODRs, On-demand resource)* 가 있습니다.

**슬라이싱**은 어플리케이션을 여러 조각으로 나눈 다음, 다운로드를 할 때 그 중에서 디바이스에 가장 적합한 버전을 다운로드하는 방식입니다. 에셋 카탈로그의 이미지들을 자동으로 적용해줍니다.

**비트코드**는 나중에 새로운 애플 디바이스가 출시되더라도 새로운 버전을 만들 필요 없이 애플 측에서 알아서 재컴파일하기 위한 방식입니다. 비트코드를 사용하게 되면 앱 스토어에 업로드를 할 때, 애플에서 그 어플리케이션을 새로 컴파일하여 최적화합니다. 

> 만약 새로운 아키텍쳐가 나오더라도 애플이 알아서 재컴파일을 하면 새로운 버전을 만들 필요가 없겠죠?

**주문형-리소스**는 굳이 어플리케이션에 포함될 필요 없는 이미지나 음악 파일에 태그를 달아, 나중에 애플 서버에서 해당 파일을 요청할 때 받을 수 있도록 하는 방식입니다. 어플리케이션 사이즈를 줄일 수 있습니다.