---
layout: post
title:  "Django 인증"
date:   2019-10-21 00:00:00
categories: Django
image: django.png
description: 쿠키 세션 캐쉬 등 http 인증에 관한 강의.
tags: python 파이썬 Django Cookie Session Cache
comments: true
---


# 191021. 월

## http

1.  비연결지향(connetionless)
2. 상태정보 유지안함( stateless, 무상태) : 연결이 ㅡㄶ어지는 순간 클라이언트와 서버간의 통신이 끝남 (각각 완벽하게 독립적)

### 쿠키(Cookie) =>  Browser = 클라이언트

- 클라이언트의 로컬에 저장되는 키-값의 작은 데이터파일
- 웹페이지에 접속하면 요청한 웹페이지를 서버로부터 받고 쿠키를 로컬에 저장하고, 클라이언트가 재요청시에 웹페이지 요청과 함께 쿠키 값도 함께 전송
- 아이디 자동완성 / 공지 메세지 하루 안보기 / 팝업 안보기 체크 / 비로그인 장바구니에 담기 /  등 면의를 위하되 지워지거나 유출되도 큰 일이 없을 정보를 저장.

### 세션(session)

- 사이트와 특정 브라우저(클라이언트) 사이의 상태를 유지시키는 것
- 일정 시간동안 같은 브라우저로부터 들어오는 일련의 요구를 하나의 상태로 보고 상태를 유지하는 기술
- 클라리언트가 서버에 접속하면 서버가 특정  session id를 발급하고, 클라이언트는 session_id를 쿠키를 사용해 저장. 클라이언트가 다시 서버에 접속하면 해당 쿠키(session_id 가 담긴)를 이용해 서버에 session_id를 전달한다.
- Django 는 특정 session id를 포함하는 쿠키를 사용해서 각각의 브라우저와 사이트가 연결된 세션을 알아낸다. 실질적인 session의 database에 기본 설정 값으로 저장된다. (이는 쿠키 안에 데이터를 저장하는 것보다 더 보안에 유리하고, 쿠키는 악의적인 사용자들에게 취약하기 때문)
- 세션을 남발하면 사용자가 많은 서버일 경우 서버 부하가 발생합니다.
- 쿠키를 지우면 로그아웃은 왜?? 서버에서는 session에 사용자 로그인 정보를 가지고 있지만, 그것이 내 꺼라는 증명할(인증키) session id가 쿠키에서 사라졌기 때문에



### 차이 점

- 쿠키 : 클라이언트 로컬에 파일로 저장
- 세션 : 서버에 저장(이 때 session id는 쿠키의 형태로 클라이언트의 로컬에 저장)

![HTTp](https://user-images.githubusercontent.com/52685322/67169156-9df9d600-f3e4-11e9-83b4-a34750e976aa.png)

---

### 캐시(cache)

- 가져오는 데 비용이 드는 데이터를 한 번 가져온 뒤에는 임시로 저장.
- 

```bash
In [1]: request.session
Out[1]: <django.contrib.sessions.backends.db.SessionStore at 0x1f80903c908>

In [2]: dir(request.session)
Out[2]:
['TEST_COOKIE_NAME',
 'TEST_COOKIE_VALUE',
 '_SessionBase__not_given',
 '_SessionBase__session_key',
 '__class__',
 '__contains__',
 '__delattr__',
 '__delitem__',
 '__dict__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getitem__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
 '__module__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__setitem__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 '__weakref__',
 '_get_new_session_key',
 '_get_or_create_session_key',
 '_get_session',
 '_get_session_from_db',
 '_get_session_key',
 '_hash',
 '_session',
 '_session_key',
 '_set_session_key',
 '_validate_session_key',
 'accessed',
 'clear',
 'clear_expired',
 'create',
 'create_model_instance',
 'cycle_key',
 'decode',
 'delete',
 'delete_test_cookie',
 'encode',
 'exists',
 'flush',
 'get',
 'get_expire_at_browser_close',
 'get_expiry_age',
 'get_expiry_date',
 'get_model_class',
 'has_key',
 'is_empty',
 'items',
 'keys',
 'load',
 'model',
 'modified',
 'pop',
 'save',
 'serializer',
 'session_key',
 'set_expiry',
 'set_test_cookie',
 'setdefault',
 'test_cookie_worked',
 'update',
 'values']

In [3]: request.session._session
Out[3]:
{'_auth_user_id': '1',
 '_auth_user_backend': 'django.contrib.auth.backends.ModelBackend',
 '_auth_user_hash': '38db5c184a8f6b04acec65933e9f59a956423f4d'}

In [4]: request.session.get('_auth_user_id')
Out[4]: '1'

In [5]: exit
```



---

## 인증

Authentication(인증) - 신원확인

- 자신이 누구라고 주장하는 사람의 신원을 확인하는 것

Authorization(권한, 허가) - 권한 부여

- 가고 싶은 곳으로 가도록 혹은 원하는 정보를 얻도록 허용하는 과정

---

### Sign UP - create 

- user를 create

### Login - create

- Session을 create

### Logout - delete

- session을 delete



### 로그인 사용자에 대한 접근 제한 ( 인증 )

- django는 세션과 미들웨어를 통해 인증 시스템을 request 객체에 연결한다.
- request는 현재 사용자를 나타내는 모든 요청에서 'request.user'를 제공한다.
- 

`is_authenticated`

- User model의 속성(attributes)들 중 하나
- 사용자가 인증 되었는지 알 수 있는 방법
- User에는 항상 True / AnonymousUser에 대해서만 항상 False
- 단, 이것은 권한과는 관련이 없으며 사용자가 활동 중(active)이거나 유효한 세션(valid sesstion)을 가지고 있는지도 확인하지 않습니다.
- 일반적으로 `request.user`에서 이 속성을 사용하여 미들웨어의 `django.contrib.auth.middleware.AuthenticationMiddleware`를 통과했는지 확인하는 역할.
{% raw %}
```html
<!-- base.html -->

{% load bootstrap4 %}

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  {% bootstrap_css %}
  <title>Document</title>
</head>
<body>
<div class="container">
{% if user.is_authenticated %} request.user.is_authenticated
  <h3>
    Hello, {{ user.username }} request.user.username
    <a href="{% url 'accounts:logout' %}">LogOut</a> 
  </h3>
{% else %}
  <h3>
    <a href="{% url 'accounts:login' %}">로그인</a>
    <a href="{% url 'accounts:signup' %}">회원가입</a>
  </h3>
{% endif %}
  <hr>
  {% block content %}
  {% endblock  %}
</div>

  {% bootstrap_javascript jquery='full' %}
</body>
</html>
```
{% endraw %}




1. 비로그인
2. admin 로그인
3. 



#### `next` query string parameter	

- @login_required 데코레이터가 기본적으로 인증 성공 후 사용자를 리다이렉트 할 경로를 next라는 문자열 매개 변수에 저장한다.
- 우리가 url로 접근하려고 했던 그 주소가 로그인하지 않으면 볼 수 없는 곳이라서, django가 로그인 페이지로 강제로 리다이렉트 했는데, 로그인을 다시 정상적으로 하고 나면 원래ㅔ 요청했던 주소로 보내주기 위해 keep해주는 것



`@required_POST`가 있는 @login_required 가 설정 되었다면, 로그인 이후 "next" 매개변수를 따라 해당 함수로 다시 redirect 되면서 @required_POST 때문에 405에러가 발생



### 회원 탈퇴



### 회원 수정



`get_user_model()`

- `user`를 직접 참조하는 대신 `django.contrib.auth.get_user_model()`를 사용하여 User model을 참조해야 한다.
- 이 함수는 현재 활성화(active)된 User model 을 return 한다.



### 비밀번호 변경

- 비밀번호 변경 후 로그아웃 되버림
- 비밀번호가 변경되면 기존 세션과의 회원 인증 정보가 일치하지 않게 되어 버렸기 때문이다.

`update_session_auth_hash(request,user)` 

- 현재 사용자의 인증 세션이 무효화 되는 것을 막고, 세션을 유지한 상태로 업데이트.
- 현재 request 와 새로운 session hash가 생긴 업데이트 된 user 객체를 적절히 업데이트