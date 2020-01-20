---
layout: post
title:  "방문기록 관리 앱, whaletime"
date:   2020-01-01
excerpt: "#html #css #javascript #chrome-extension"
tag:
- html
- css
- javascript
- chrome-extension
project: true
comments: false
---

제가 처음으로 만든 크롬 웹 확장 프로그램 개발 과정과 그 실패에 대해서 이야기하려고 합니다.

우연히 [네이버 웨일 확장앱 콘테스트 2019](https://whale.naver.com/contest/) 에 대해 들었고, 아이디어만 가지고 별 생각 없이 지원했습니다.

그리고 본선 진출작이 되었습니다.

5일의 개발 시간이 주어졌습니다.

문제는 제가 당시에 HTML/CSS/Javascript 를 모르는 상태였다는 것이었습니다.

> ??

HTML/CSS/Javascript 에 대해 하나도 모르는 데 5일 만에 그럴듯한 크롬 웹 확장 프로그램을 만드는 것이 가능할까?

Google 과 StackOverflow 는 이 모든것을 가능하게 했습니다.

그렇게 그럴듯한 크롬 확장 프로그램 하나가 출시되었습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/whaletime/chrome_web_store.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/whaletime/chrome_web_store.png"></a>
</figure>

[whaletime 코드](https://github.com/woojin-hwang/whaletime)

> 방문기록 관리를 도와주는 간단한 크롬 웹 확장 프로그램입니다.

*그럴듯한* 이라는 이름 뒤편에서, 이 프로그램은 많은 문제를 가지고 있었습니다.

## 생각하는대로 구현이 가능한가?

아이디어는 "사용자들의 검색 기록을 분석하는 프로그램" 입니다.

검색기록을 가져와서 분석한 후 카테고리에 따라서 나누어 그래프로 보여주고 싶었습니다.

`iOS` 의 [스크린타임](https://support.apple.com/ko-kr/HT208982) 과 `Android` 의 [디지털웰빙](https://play.google.com/store/apps/details?id=com.google.android.apps.wellbeing&hl=ko) 을 브라우저 환경에 구현하는 것이 목표였습니다.

그런데 실제로 구현을 하면서 불가능한 부분들이 많다는 것을 발견했습니다.

사용자의 검색기록을 카테고리화 하기 위해서는 URL 에 대한 카테고리 데이터가 필요했습니다.

이를 API 를 통해 사용하려고 했으나 비용이 매우 비효율적이었습니다.

다른 방법을 찾아보려 했으나 결국에는 포기했습니다.

## 생각하는대로 구현이 가능한가? 2

사용자가 날짜를 선택하면 해당 날짜로 이동을 하도록 만들어야 합니다.

근데 이걸 어떻게 구현해야 되는지 알고 있는 것이 없었습니다.

그래서 날짜값을 임시 브라우저 공간에 저장한 후 좌우 화살표를 누르면 값 변경을 해서 새로고침하는 방식으로 구현했습니다.

대충 이런 식으로 작동하게 만들었습니다.

{% highlight javascript %}
chrome.storage.local.set(items, function() {});
location.reload(true);
{% endhighlight %}

> 그래서 날짜를 변경할때마다 페이지가 계속 새로고침됩니다. 와우.

## 해당 기술에 경험이 있는가?

앞서 말했듯이, 크롬 확장 프로그램에 대한 경험이 전무했습니다.

심지어 웹 관련 기술 스택이나 경험에 대해서도 무지했습니다.

그래서 여러 놀라운(?) 결정들을 내리고는 했습니다.

예를들어, 처음에는 사용자 로컬에 저장된 브라우저 검색 기록 sqlite 파일을 분석에 사용하려고 했습니다.

history API 로 검색기록을 쉽게 가져올 수 있다는 것을 몰랐기 때문입니다.

## UI/UX 는?

UI/UX 적인 측면을 전혀 고려하지 않은 것은 아닙니다.

다만, 기획이나 기술적인 측면에 있어서 부족했기 때문에 그 한계가 UI/UX 에 그대로 나타났습니다.

Adobe XD 와 같은 도구를 사용한 것도 아니었습니다.

그냥 CSS 를 디버깅 돌려가며 작업했습니다.

> 그리고 작살이 났다고 합니다.

## 확장성을 고려했는가?

문제의 HTML 코드는 다음과 같습니다.

{% highlight html %}
...
<link rel="stylesheet" href="reset.css" type="text/css">
...
<!--left button / write button--->
<div class="content" style="height:50px; position:relative; z-index: 1;">
    <input type="button" id="leftbutton" class="left-button">
    <input type="button"  id="rightbutton" class="right-button">
</div>
<!--date-->
<div class="content" style="height:50px;text-align:center;font-size:20px;">
    <span class="date" id="id_date" style="position:relative; z-index: 2;"></span>
</div>
<!--1 day graph-->
<div class="content" id="id_graph" style="height:300px;text-align:center;">
  <script src = "donut.js"></script>
  <div class="table" id="id_donut" style="position:relative;"></div>
</div>
<!--erase history-->
<div class="content" style="height:100px;text-align:center;">
  <input type="button" id="erasethis" value="Delete current historclass="erase">
  <br><br><input type="button"  id="eraseall" value="Delete all historclass="erase">
</div>
<div style="font-size:10px;top:20px;text-align:center;">Caution : No turniback.</div><br>
{% endhighlight %}

분명히 외부의 `css` 파일을 참조하도록 되어있습니다.

그러나 배치를 할 떄 계속 조금씩 수정을 하다 보니 `html` 코드 내부에 `css` 코드가 들어가게 되고, 결국 지저분한 코드가 되었습니다.

z-index 를 조작해서 억지로 배치를 한 모습이 보입니다.

만약에 여기서 기능을 하나 추가하려면 어떻게 해야 할까요?

아마 모든 HTML 코드를 뜯어 고쳐야 할 지도 모릅니다.

## 정리

정말 많은 것들을 느낄 수 있었던 경험이었습니다.