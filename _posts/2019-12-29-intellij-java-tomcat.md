---
layout: post
title:  "Eclipse 가 아닌, IntelliJ IDEA 로 해보는 Java 와 Tomcat 의 Servlet 개발환경 구축하기"
date:   2019-12-29
excerpt: "#intellij-idea #java #tomcat #servlet"
tag:
- intellij-idea
- java
- tomcat
- servlet
comments: false
---

`Java` 와 `Tomcat` 을 통한 `Servlet` 개발 환경을 구축할 때는 보통 `Eclipse` 를 많이 사용합니다.

그러나 `Eclipse` 말고도 좋은 개발환경은 얼마든지 있습니다.

여기서는 [Jetbrain](https://www.jetbrains.com) 의 `IntelliJ IDEA` 를 통해 개발환경을 만들어 보도록 하겠습니다.

`IntelliJ IDEA` 는 [Jetbrain 홈페이지](https://www.jetbrains.com/idea/) 에서 받을 수 있습니다.

Ultimate 와 Community 버전이 있습니다.

상황에 맞는 버전을 다운로드해서 사용하시면 됩니다.

> 저는 Github Student Developer Pack 을 통해 Ultimate 버전을 사용하고 있습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_welcome.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_welcome.png"></a>
</figure>

새로운 프로젝트를 생성합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_tomcat.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_tomcat.png"></a>
</figure>

Ultimate 버전에서는 Enterprise 를 사용할 수 있습니다.

Community 버전의 경우 직접 `Java` 를 설치해서 사용하면 됩니다.

Application Server 에는 설치한 `Tomcat` 경로를 지정합니다.

Tomcat 은 [Tomcat 홈페이지](http://tomcat.apache.org) 에서 받을 수 있습니다.

라이브러리로는 Web Application 을 체크합니다.

그러면 다음과 같이 프로젝트가 생성됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_project.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_project.png"></a>
</figure>

New 를 눌러서 `Servlet`을 만들어 보도록 하겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_create_new_servlet.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_create_new_servlet.png"></a>
</figure>

만약 여기서 Create New Servlet 이 없는 경우, `Maven` 을 통해 `Tomcat Servlet` 을 직접 받아야 합니다.

직접 해보도록 하겠습니다.

프로젝트의 Open Module Setting 에 들어갑니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_open_module_settings.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_open_module_settings.png"></a>
</figure>

Library 탭에 들어가서 + 를 눌러 From Maven 을 선택합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_Maven.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_Maven.png"></a>
</figure>

`tomcat:servlet` 을 검색합니다.

라이브러리로 다운로드합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_tomcat_servlet.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_tomcat_servlet.png"></a>
</figure>

> 여기서는 tomcat:servlet:4.1.36 버전을 검색해서 사용하였습니다.

그러면 프로젝트에 `tomcat:servlet` 라이브러리가 생성됩니다.

그리고 Create New Servlet 메뉴가 활성화되어 있는 것을 알 수 있습니다.

한번 Maven 을 통해서 받은 후에는 굳이 프로젝트마다 `Maven` 으로 받지 않아도 Create New Servlet 을 사용할 수 있습니다.

`Servlet` 을 생성해 보겠습니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_new_servlet.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_new_servlet.png"></a>
</figure>

MyServlet 코드는 다음과 같이 작성했습니다.

{% highlight java %}
package mypack;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/MyServlet")
public class MyServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        out.print("<h1>MyServlet!<h1>");
    }
}
{% endhighlight %}

이제 `Servlet` 을 설정할 차례입니다.

상단의 Run 에서 Edit Configurations ... 를 선택합니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_edit_configurations.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_edit_configurations.png"></a>
</figure>

Deployment 탭에 들어갑니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_configurations_deployment.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/IntelliJ_IDEA_configurations_deployment.png"></a>
</figure>

Application context 의 값이 `Servlet` 에서 가지는 서브 주소값을 의미합니다.

Application context 가 untitled_war_exploded 이면

만약 localhost:8080 에 서버를 돌리는 경우 localhost:8080/untitled_war_exploded 에 해당 `Servlet` 이 배포됩니다.

원하는 주소를 입력하면 되겠습니다.

저는 Application context 를 /content 로 설정하도록 하겠습니다.

그러면 tomcat 서버를 실행하였을 때 다음과 같이 설정이 됩니다.

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/localhost_new.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/localhost_new.png"></a>
</figure>

> localhost:8080/content

<figure>
  <a href="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/localhost_servlet.png"><img src="https://raw.githubusercontent.com/woojin-hwang/woojin-hwang.github.io/master/_posts/img/intellij-java-tomcat/localhost_servlet.png"></a>
</figure>

> localhost:8080/content/MyServlet

[#intellij-idea](https://woojin-hwang.github.io/tags/#intellij-idea) [#java](https://woojin-hwang.github.io/tags/#java) [#tomcat](https://woojin-hwang.github.io/tags/#tomcat) [#servlet](https://woojin-hwang.github.io/tags/#servlet)
