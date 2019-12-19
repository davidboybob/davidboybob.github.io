---
layout: post
title:  "URL Namespace"
date:   2019-09-18 00:00:00
categories: Django
image: django.png
description: URL에 대한 설명 및 HTTP 기초
tags: python 파이썬 Django HTTP URL
comments: true
---

```bash
pip freeze > requirements.txt
pip install -r requirements.txt
```

URL Namespace

1. 하드코딩 URL 제거

2. {% raw %} {% url %}  {% endraw %} template tag

3. 문제점
   1. app이 여러개가 되면, 단순히 url name 만 가지고는 어떤 app의 url 인지 알





웹서비스 HTTP 기초

요청 -----(주소URL)-----> 응답

정보를<-----(문서)---------	정보를 주는사람

원하는 

사람

cookie 와 session 



URL 파일 식별자 : Uniform Resource 

URI 통합 자원 식별자 : Uniform Resource Identifier

https://www.google.com

- URI 이면서 URL(모든 URL는 URI 이다.)

https://



-주소 + 특정 문자열(query)

form tag에 action이 없다면, 현재 머물고 있는 URL로 요청을 보낸다.



### URI

### - 인터넷에 자원을 나타내는 유일한 주소

- 인터넷에서 요구되는 기본조건으로서  http에 항상 붙어 다닌다.
  
  
  
  ### URL- 인터넷 상에서 자원이 어디 있는지 알려주기 위한 규약
  
  ### 예제1. [https://www.google.com](https://www.google.com/)  > 서버주소(URL 이면서 URI 이다)
  
  2. https://github.com/seasign10/STUDY/blob/master/01_Startcamp/190710_study2_HTML_CSS.md  > 주소 + 디렉토리 파일의 주소(자원의 위치)
  
  >
  >URL 이면서 URI3. [[https://www.google.com/search?q=%EC%82%BC%EC%84%B1](https://www.google.com/search?q=삼성)](https://www.google.com/search?q=삼성)  > 주소 + 특정 문자열(query string) -> search?q=
  >
  >search 까지가 URL + q=삼성 이라는 식별자가 필요하므로 URI 이지만 URL은 아니다.GET POST PATCH DELETE실제로 HTTP 에서는 공식적으로 GET POST 만 공식적으로 사용된다.GET articles/create/ -> 글을 작성하는 페이지POST articles/create/ -> 글이 실제로 작성되는 페이지같은 주소로 들어가는데 GET OR POST 에 따라 다르게 행동할 것이다. (NEW+CREATE)form tag 에 action 이 없다면, 현재 머물고 있는 URL 로 요청을 보낸다.

form tag에 action 이 없다면, 현재 머물고 있는 URL로 요청을 보낸다.





Model Instance Method

1. get_absolute_url()

   - 특정 모델에 대해 detail view를 작성할 경우, detail url을 완성하자 마자 사용한느 것을 권장한다.
   - 반복되는 코드가 줄고 보다 간결해진다.

     redirect(모델 인스턴스)를 통해서 모델 인스턴스의 get_absolute_url() 함수를 자동으로 호출

URL Reverse를 수행하는 함수들

reverse()

- 리턴값 : string (문자열)

- ```python
  revserse('articles:index') # '/articles/'
  ```

redirect()

- 리턴 값: HttpResponseRedirect(객체)

- 내부적으로 `resolve_url()`을 사용

- view 함수에서 특정 url 로 돌려보내고자 할 때 사용.

- view 함수에서 특정 url로 돌려보내고자 할 때 사용

- ```python
  redirect('articles:article')
  # <HttpResponseRedirect status_code=200, "text/html; charset=utf-8, url="/articles/">
  ```

url template tag({% raw %} {% url %} {% endraw %})

- 내부적으로 

1. model 2개 컬럼

   



View 2개

index / past_life

입력된 이름이 DB에 있는지 없는지

있다면 기존 DB에서 그대로 가져와서 출력

없다면 faker를 통해