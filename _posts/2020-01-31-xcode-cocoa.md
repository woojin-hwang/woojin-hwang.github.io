---
layout: post
title:  "코코아 터치 프레임워크에 대해 알아보기"
date:   2020-01-31
excerpt: "#boostcourse #booster #xcode"
tag:
- boostcourse
- booster
- xcode
comments: false
---

[[부스트코스] iOS 프로그래밍 강좌](https://www.edwith.org/boostcourse-ios/)에 대한 정리글입니다.

[[이전 포스트]Xcode 의 UI 중 버튼, 레이블 그리고 슬라이더 알아보기](https://woojin-hwang.github.io/xcode-ui/)

---

**코코아 터치 프레임워크**는 iOS 개발에 필요한 여러 프레임워크들을 포함하고 있는 최상위 레벨의 프레임워크입니다. 핵심 프레임워크로는 UI 개발에 사용되는 UIKit 과 자료형과 메소드가 정의되어 있는 Foundation Kit 이 있습니다.

> macOS 개발에는 코코아 프레임워크가 사용됩니다. 여기서는 UIKit 대신 Application Kit 이 사용됩니다.

## UIKit

---

UIKit 은 iOS 또는 tvOS 에서 사용자의 인터페이스를 구현하고 이벤트를 관리하는 프레임워크입니다. 많은 요소들이 있지만 그 중에서 사용자 인터페이스와 사용자 액션에 대해서 알아보겠습니다.

### 사용자 인터페이스

[Views and Control](https://developer.apple.com/documentation/uikit/views_and_controls) 는 화면에 콘텐츠를 표시하는 것을 다룹니다.

[View Controller](https://developer.apple.com/documentation/uikit/view_controllers) 는 사용자 인터페이스를 관리합니다.

[View Layout](https://developer.apple.com/documentation/uikit/view_layout) 은 뷰의 레이아웃을 관리합니다.

[Appearance Customizaion](https://developer.apple.com/documentation/uikit/appearance_customization) 는 다크 모드를 추가하거나 그 외의 인터페이스를 변경할 수 있도록 합니다.

[Animation and Haptics](https://developer.apple.com/documentation/uikit/animation_and_haptics) 는 애니메이션과 햅틱을 통한 피드백을 제공합니다.

[Windows and Screens](https://developer.apple.com/documentation/uikit/windows_and_screens) 는 뷰 계층을 위한 윈도우를 제공합니다.

### 사용자 액션

[Touches, Presses, Gestures](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures) 는 제스처 인식기를 통해 이벤트를 다룹니다.

[Drag and Drop](https://developer.apple.com/documentation/uikit/drag_and_drop) 는 화면 위에서 드래그 앤 드롭 기능을 다룹니다.

[Pencil Interactions](https://developer.apple.com/documentation/uikit/pencil_interactions) 는 애플 펜슬의 더블 탭 이벤트를 다룹니다.

[Focus-based Navigation](https://developer.apple.com/documentation/uikit/focus-based_navigation) 는 어플리케이션이 외부 컨트롤러를 사용할 때의 인터페이스를 다룹니다.

[Menus and Shortcuts](https://developer.apple.com/documentation/uikit/menus_and_shortcuts) 는 메뉴, 퀵 액션, 단축키를 통해 사용자 액션을 단순하게 합니다.

[Accessibilities](https://developer.apple.com/documentation/uikit/accessibility) 는 어플리케이션의 접근성을 다룹니다.

그 외의 UIKit 의 요소들을 알고 싶으시다면 [Apple 개발자 문서](https://developer.apple.com/documentation/uikit) 를 참조하시기 바랍니다.

## Foundation Kit

---

Foundation Kit 은 Int, String 등의 데이터 타입 및 Array, Dictionary 등의 컬렉션 타입과 운영체제의 서비스를 이용해서 어플리케이션의 기본적인 기능을 관리하는 프레임워크입니다. 시간 계산이나 네트워킹 등의 기본 기능을 제공합니다.

### 기본 요소

[Numbers, Data, and Basic Values](https://developer.apple.com/documentation/foundation/numbers_data_and_basic_values) 는 원시 데이터 타입들에 대해 다룹니다.

[Strings and Text](https://developer.apple.com/documentation/foundation/strings_and_text) 는 문자열과 정규 표현식에 대해 다룹니다.

[Collections](https://developer.apple.com/documentation/foundation/collections) 는 컬렉션 타입들에 대해 다룹니다.

[Dates and Times](https://developer.apple.com/documentation/foundation/dates_and_times) 는 날짜와 시간에 대해 다룹니다.

[Units and Measurement](https://developer.apple.com/documentation/foundation/units_and_measurement) 는 물리적인 차원들을 표현하는 것에 대해 다룹니다.

[Data Formatting](https://developer.apple.com/documentation/foundation/data_formatting) 는 데이터들의 형변환에 대해 다룹니다.

[Filters and Sorting](https://developer.apple.com/documentation/foundation/filters_and_sorting) 는 컬렉션 타입의 요소 검사와 정렬에 대해 다룹니다.

### 앱 지원

[Task Management](https://developer.apple.com/documentation/foundation/task_management) 는 어플리케이션이 핸즈오프나 단축키에 어떻게 반응할 지 관리합니다.

[Resources](https://developer.apple.com/documentation/foundation/resources) 는 에셋과 번들들을 어플리케이션에 사용하도록 합니다.

[Notifications](https://developer.apple.com/documentation/foundation/notifications) 는 알림에 대한 디자인 패턴을 다룹니다.

[App Extension Support](https://developer.apple.com/documentation/foundation/app_extension_support) 는 확장 어플리케이션에 대해 다룹니다.

[Errors and Exceptions](https://developer.apple.com/documentation/foundation/errors_and_exceptions) 는 에러가 발생할 수 있는 상황에 대응하는 방법에 대해 다룹니다.

[Scripting Support](https://developer.apple.com/documentation/foundation/scripting_support) 는 사용자가 어플리케이션 안에서 스크립트를 제어하거나 실행하는 것에 대해 다룹니다.

### 파일 및 데이터 관리

[File System](https://developer.apple.com/documentation/foundation/file_system) 는 파일 시스템에서 파일과 폴더를 관리합니다.

[Archives and Serialization](https://developer.apple.com/documentation/foundation/archives_and_serialization) 는 속성 리스트나 JSON 또는 바이너리 파일들을 객체로 변환하거나 객체로부터 변환하는 것을 다룹니다.

[Preferences](https://developer.apple.com/documentation/foundation/preferences) 는 설정에 사용되는 정보를 영구적으로 저장하는 방법에 대해 다룹니다.

[Spotlight](https://developer.apple.com/documentation/foundation/spotlight) 는 어플리케이션 검색을 위해 인덱싱하는 방법에 대해 다룹니다.

[iCloud](https://developer.apple.com/documentation/foundation/icloud) 는 iCloud 를 통해 데이터를 동기화하도록 관리합니다.

### 네트워킹

[URL Loading System](https://developer.apple.com/documentation/foundation/url_loading_system) 는 표준 프로토콜들을 통해 URL 과 통신하는 방법에 대해 다룹니다.

[Bonjour](https://developer.apple.com/documentation/foundation/bonjour) 는 로컬 네트워크를 통해 통신하는 방법에 대해 다룹니다.

이 외의 Founcation Kit 의 요소들에 대해서는 [Apple 개발자 문서](https://developer.apple.com/documentation/foundation) 를 참조하시기 바랍니다.

---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>
