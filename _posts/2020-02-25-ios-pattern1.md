---
layout: post
title:  "[Booster 2기] iOS 의 다양한 디자인 패턴 알아보기 1"
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

[[이전 포스트]뷰의 상태변화를 감지하는 메서드 알아보기](https://woojin-hwang.github.io/view-behavior/)

---

디자인 패턴이란 소프트웨어를 개발할 때 사용되는 특정한 구조를 말합니다. iOS 개발에는 대표적으로 MVC 패턴이 사용됩니다. 이에 대해서는 [여기](https://woojin-hwang.github.io/mvc)를 참조하시기 바랍니다.

그러나 모든 iOS 개발에 MVC 패턴이 사용되지는 않습니다. 이 외이도 정말 다양한 패턴들이 사용됩니다. 예를 들어 델리게이션 패턴, 싱글톤 패턴 그리고 타겟-액션 패턴이 있습니다. 이번에는 이 패턴들에 대해서 알아보겠습니다.

### 델리게이션 패턴(Delegation Pattern)

Delegation 는 '위임하다' 는 뜻을 가지고 있습니다. 이 뜻에서 알 수 있듯이, 델리게이션 패턴이란 하나의 객체가 다른 객체를 설정하거나 대신해서 동작하도록 하는 디자인 패턴입니다. 주로 Foundation, UIKit, AppKit, Cocoa Touch 등의 프레임워크에서 자주 사용됩니다. 개발자가 작성한 객체가 프레임워크의 위임을 받아서 기능을 구현하도록 합니다. 예시를 통해서 알아보도록 하겠습니다.

지금 만들어 볼 것은 간단한 imagePicker 프로젝트입니다. 버튼을 누르면 사용자의 라이브러리에서 사진을 선택할 수 있도록 해서, 사용자가 특정 사진을 선택하면 그 사진을 화면에 나타나도록 하는 어플리케이션입니다.

먼저 스토리보드에서 *ImageView* 와 *Button* 을 하나씩 생성합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/storyboard.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/storyboard.png"></a>
</figure>

그리고 ViewController.swift 파일에 다음 코드를 생성합니다.

{% highlight swift %}
import UIKit

class ViewController: UIViewController, UIImagePickerControllerDelegate, UINavigationControllerDelegate {

  lazy var imagePicker: UIImagePickerController = {
    let picker: UIImagePickerController = UIImagePickerController()
    picker.sourceType = .photoLibrary
    picker.delegate = self
    return picker
  }()

  @IBOutlet weak var imageView: UIImageView!
    
  @IBAction func touchUpSelectImageButton(_ sender: UIButton) {
    self.present(self.imagePicker, animated: true, completion: nil)
  }
}
{% endhighlight %}

> 코드에 대한 상세한 설명보다는 델리게이션 패턴에 대해 중점적으로 다루겠습니다.

imageView 는 이미지를 위한 프로퍼티입니다. 아까 스토리보드에서 만든 ImageView 와 연결해줍니다.

touchUpSelectImageButton 은 버튼을 위한 메서드입니다. 사용자가 버튼을 누르면 present 함수를 통해 사진을 보여주도록 합니다. 이 때 우리가 원하는 것은 사용자가 포토 라이브러리에서 사진을 선택하도록 한 후 그 사진을 보여주는 것입니다.

이를 위해 선언한 것이 imagePicker 프로퍼티입니다. imagePicker 는 사용자의 포토 라이브러리에서 사진을 가져오기 위한 UIImagePickerController 타입의 변수입니다.

위 코드를 실행한다고 해서 어플리케이션이 원하는대로 동작하지는 않습니다. 아직 구현을 하지 않은 부분이 있습니다. 이 때 델리게이션 패턴이 사용되는데, 이에 대해서는 Apple 개발자 문서에서 UIImagePickerControllerDelegate 에 대해 설명하고 있는 내용을 참조하겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/guide1.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/guide1.png"></a>
</figure>

이 프로토콜에는 두개의 메서드가 존재합니다. 바로 imagePickerController 와 imagePickerControllerDidCancel 입니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/guide2.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/guide2.png"></a>
</figure>

설명을 보면, imagePickerController 는 사용자가 이미지를 선택했을 때 그리고 imagePickerCOntrollerDidCancel 는 사용자가 취소를 선택했을 때 호출되는 메서드인 것을 확인할 수 있습니다. 이를 사용하도록 하겠습니다. ViewController.swift 파일에 다음 코드를 추가합니다.

{% highlight swift %}
func imagePickerControllerDidCancel(_ picker: UIImagePickerController) {
    self.dismiss(animated: true, completion: nil)
}
    
func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey : Any]) {
        
  if let originalImage: UIImage = info[UIImagePickerController.InfoKey.originalImage] as? UIImage {
    self.imageView.image = originalImage
  }
        
  self.dismiss(animated: true, completion: nil)
}
{% endhighlight %}

이 코드를 자세히 살펴보면 개발자 문서에서 서술한 imagePickerController 메서드와 imagePickerControllerDidCancel 메서드가 그대로 사용된 것을 볼 수 있습니다. 여기에 사용된 패턴이 바로 **델리게이션 패턴**입니다. ViewController.swift 에서 선언한 imagePicker 프로퍼티가 UIImagePickerControllerDelegate 로부터 위임을 받아 동일한 기능을 수행하도록 합니다. 어플리케이션 실행시 정상적으로 동작하는 것을 확인할 수 있습니다.

{% highlight html %}
<figure class="third">
	<img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/app1.png">
	<img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/app2.png">
	<img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/ios-pattern/app3.png">
</figure>
{% endhighlight %}

---


[[다음 포스트]iOS 의 다양한 디자인 패턴 알아보기 2](https://woojin-hwang.github.io/ios-pattern2/)


---

<figure>
  <a href="https://woojin-hwang.github.io/boostcourse-ios/"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/boostcourse/tag.jpg"></a>
</figure>
<center>클릭하면 처음 포스트로 돌아갑니다.</center>