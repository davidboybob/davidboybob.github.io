---
layout: post
title:  "JSON Web Tokken 회원 인증 및 정보 교환"
date:   2019-11-08 00:00:00
categories: Vue.js
image: vuelogo.png
description: youtube 연동하기.
tags: Django Vue.js Json Tokken 정보
comments: true
---

# Json Web Tokken

## (정리) JWT

- 세션/쿠키와 함께 모바일과 웹의 인증을 책임지는 대표 기술 중 하나. (세션/쿠키와는 다르지만, 유사한 모습), 세션/쿠키의 정보 전달 방식과 유사하게 사용자는 Access Token (JWT token)을 HTTP header에 실어서 서버로 요청을 보냄.
- 세션/쿠키 방식과 가장 큰 차이점은 세션/쿠키는 세션 저장소에 유저의 정보를 넣지만, JWT는 토큰 안에 유저의 정보를 넣는다.
- Client의 입장에서는 HTTP header에 세션ID/ 토큰을 실어서 보낸다는 점은 동일하지만, Server 입장에서는 인증을 위해 암호화 (JWT 방식)를 하는 것이냐 혹은 별도의 저장소(세션/쿠키 방식)를 이용하느냐의 차이

### 사용 상황

1. 회원 인증
   - 서버가 유저 정보에 기반한 토큰 (JWT)을 발급해 유저에게 전달하고, 유저는 서버에 요청을 보낼 때마다 JWT를 포함하여 전달.
   - 서버는 세션을 유지할 필요 없이 유저의 요청정보 안에 있는 JWT 만 확인하면 된다. (서버 자원 아낄 수 있음.)
2. 정보 교환
   - 정보가 서명 되어 있기 때문에 정보를 보낸 사람의 정보 혹은 정보가 조작여부 확인 등이 가능.

### 요약 

- 두 개체에서 JSON 객체를 사용하여 가볍고 `자가수용적인(self-contained, 필요한 모드 정보를 자체적으로 지님)` 방식으로 안정성 있게 전달.
- 세션 상태를 저장하는 것이 아니라 필요한 정보를 JWT에 저장해서 사용자가 가지고 있게 하고, 해당 JWT를 증명서처럼 사용하는 방식.

### 장점

1. 세션/쿠키처럼 별도의 저장소 관리가 필요 없고 발급한 이후에 검증만 하면 된다.
2. 토큰을 기반으로 한 다른 인증시스템에 접근이 용이하기 떄문에 확장성이 뛰어나다.
3. 모바일 환경에 적합(쿠키와 같은 데이터로 인증할 필요가 없기 떄문)
4. Python, JS, rUBY, Go 등 주류 프로그래밍 언어에서 대부분 지원된다.

### 단점

1. 이미 발급된 JWT는 유효기간이 완료될 때까지 계속 사용하기 때문에 악용될 가능성이 있다.(한번 발급된 토큰은 값을 수정하거나 페기할 수 없다.)

   그래서, 이 문제는 Access Token의 유효기간(expire time)을 짧게하고 Refresh Token 등을 이용해서 중간 중간 새로운 토큰을 재발행 해준다.

2. 세션/쿠키 방식에 비해 claim 데이터가 많아진다면, JWT 토큰의 길이가 길어지기 때문에 인증요청이 많아 질수록 네트워크의 대역푝이 낭비될 수 있다. (API 호출 시 매 호출마다 헤더에 붙여서 전달하기 때문.)

3. 





정보를 안전하게 JSON 객체로 전송하기 위한 간결하고 독립적인 방법

Header.Payload.signature

xxxx.yyyy.zzzz 

- Header : token의 type과 사용 algorithm
- Payload : 토큰에 담길 정보가 들어있는 곳 (claim - key:value)
- Header와 Payload의 값에 비밀 키로 hashing

![image](https://user-images.githubusercontent.com/52685322/69019870-e1506000-09f5-11ea-9640-d51b4ccc989c.png)

## 정보(payload)

1. registerd Claim
   - 토큰에 대한 정보들을 담기 위해 이름이 이미 정해진 클레임들. 클레임의 사용은 모두 선택적이다.
2. public claim
   - 공개 클레임은 충돌이 되지 않는 이름을 가지고 잇어야 함. 보통 충돌을 방지하기 ㅜ이해 key 값을 URI 형태로 만든다.(예: "apple" = > 'http://test.co.kr/jwt_token')
3. private claim
   - 등록된 클레임도 아니고 공개 클레임도 아님. 클라이언트와 서버간에 협의하에 사용되는 클레임들.
   - key 값이 중복되서 충돌이 도리 수 있으니 유의해서 사용.
   - 예) {"username": "admin"}

## 서명(signature)

- HEADER의 인코딩 값과, PAYLOAD의 인코딩 값을 합친 후 주어진 비밀키로 해쉬를  생성한 값

---

## PROJECT INSTRUCTURE



### router-link

- router 지원 앱에서 사용자 네비게이션을 가능하게 해주는 컴포넌트
- 목표 위치는 `to` prop 으로 지정된다.
- 라우팅은 URI 에 따라 해당하는 정적 파일을 내려주는 방식인데 이를 브라우저에서 구현하는 것이 SPA 개발의 핵심.
- `router-link`는 `a`태그보다 선호되는 데 이유는 HTML5 히스토리 모드에서 클릭 이벤트 자체를 차단하여 브라우저가 페이지를 다싱 로드하지 않도록 한다.



### router_View

- 라우팅이 경로에 맞는 컴포넌트를 제공하는 데 해당 경로에 맞는 컴포넌트를 렌더링 해주는 부분

---

## CORS(Cross-Origin Resource Sharing)

### 정의

- 한 도메인에서 로드되어 다른 도메인에 있는 리소스와 상호 작용 하는 것.
- 즉, 도메인이나 포트가 다른 서버의 자원을 요청하는 메커니즘

### 문제상황

1. 요청을 할 때 cross-origin HTTP 에 의해 요청을 한다.
2. 하지만 CORS 와 같은 상황이 발생하면 외부 서버에 의한 요청 데이터를 브라우저에서 차단하기 떄문에 (보안목적) 정상적으로 데이터를 받을 수 없다.
3. 예를 들어, `http://localhost:8080/`에서 vue를 실행하고, `http://localhost:8000/`에서 django를 실행할 경우 포트가 달라 다른 도메인으로 인지하고 브라우저가 요청을 차단한다.

### 해결방법

1. 서버(django)와 클라이언트(vue)가 같은 도메인과 포트를 사용하도록 한다.
2. 서버에서 cross-origin HTTP 요청을 허가하낟. (우리가 해결할 방법)
   - 실제 API 서버들은 이러한 CORS 제한과 관련된 처리를 모두 해두어야 한다.
   - 





2일차

<img width="807" alt="Screen Shot 2019-11-19 at 10 31 41 AM" src="https://user-images.githubusercontent.com/52685322/69108747-f93ce800-0ab8-11ea-8fe2-6db61f51e26c.png">

DRF

DRF-jwt

cors

### Vue-session

` this.$session.start() `

- session-id 초기화. 만약 세션이 없이 저장하려고 하면 vue-session 플러그인이 자동으로 새로운 세션을 시작

`this.$session.set(key,value)`

- session에 해당 key에 맞는 값을 저장

` this.$session.has(key)`

- key(JWT)가 존재하는지 여부를 확인

` this.$session.destroy() `

- 세션을 삭제

---

0. Django
   - 회원가입
1. Vue -> Django
   - 로그인 정보(credentials)를 django 서버로 보냄
2. Django
   - Vue에서 받은 윶정보에 해당하는 고유한 Web Token 발급
3. Django -> Vue
   - 해당 유저에 대한 토큰을 Vue로 보냄
4. Vue
   - django에서 받은 토큰을 vue-session을 통해 저장( 이 시점부터 vue에서는 로그인 성공 상태)
5. Vue -> Django
   - vue-session에 저장된 토큰을 가지고 django에 로그인 요청
6. Django
   - 최초로 보낸 토큰과 일치하는지 여부를 확인(session에 저장된 토큰 == 요청자의 토큰) => 일치하면 로그인

---

`.start()`를 통해 `session-id:sess` + `Date.now()` 가 만들어짐

`.set()` 을 통해 `jwt: jwt 값` 이 만들어짐

---

Vue의 라이프 사이클

1. Vue instance 생성 (create)
2. DOM에 부착(mounted)
3. 업데이트(updated)
4. 삭제(destroy)

---

FormData (Create, 필요한 정보 받아오기)

- 기존 키에 새로운 값을 추가하거나 키가 없느 ㄴ경우 새로운 키를 추가.(`FormData.append()`)
- `FormData.append(name,value)`
- name: 
- 



---

## 3일차 (UD)

`splice()`

- 배열의 기존 요소를 삭제 혹은 교체하거나 새 요소를 추가하여 배열의 내용을 변경

문법

- `Array.splice(시작 index,  삭제할 요소 수, 배열에 추가할 요소)
- ` splice(start, deleteCount, [item1, item2, item3])

1. start
   - 배열의 변경을 시작할 인덱스 (시작점 잡기)
   - 배열의 길이보다 큰 값이면 시작 인덱스는 배열의 길이로 설정
   - 음수인 경우 배열의 가장 마지막에서 시작
   - 절대 값이 배열의 길이보다 큰 경우는 0으로 설정.
2. deleteCount
   - 배열에서 제거할 요소의 수
   - 생략할 경우 start부터 모든 요소를 제거
   - 0 이하인 경우 어떤 요소도 삭제하지 않음. 이때는 최소한 하나의 추가할 새로운 요소 지정
3. [ item1, item 2 ... ]
   - 배열에 추가할 요소
   - 추가할 아무 요소도 지정하지 않으면 요소를 제거만 한다.
   - 즉, 추가할 요소를 지정하지 않으면 원본 배열의 특정 인덱스에서 몇개의 요소를 삭제할지 정한다.

---

### updated

타입 

- function

상세

- 데이터가 변경되어 DOM 이 re-render 되고, patch 되면 호출된다.(DOM 변화에 반응)
- DOM의 변화는 일반적으로 데이터의 변경의 의해 re-render 되는 시점에 일어난다.
- 데이터의 변화(상태의 변화)에 반응하기 위해서는 comnputed 나 watch를 사요하는 것이 좋다.



### Vuex

- State 관리를 위해 탄생
- 컴포넌트 간의 통신 혹은 데이터 전달을 유기적으로 관리
- 컴포넌트 간의 통신 혹은 이벤트 등의 관계를 한 곳에서 관리하기 쉽게 구조화



현재 todo 프로젝트에서는 Auth 정보(로그인 혹은 로그아웃)은 django로 요청을 보낼 때 항상 필요하기 때문에, 요청을 수행하는 모든 컴포넌트에서 알고있어야 하고 그 정보를 내가 필요한 순간에 활용할 수 있어야 한다.