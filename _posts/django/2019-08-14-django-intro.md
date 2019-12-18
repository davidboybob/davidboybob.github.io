---
layout: post
title:  "Django Intro"
date:   2019-08-14 00:00:00
categories: Django
image: django.png
description: 본격적인 강의에 앞서서 장고가 무엇인지 알고가는 강의입니다.
tags: python 파이썬 Django Intro
comments: true
---

# 1. 8월 14일 

## 	1.장고 django 영어발음 `재~~ㅇ고~ ㅜ~`

1. 특징

   1. versatile
   2. Secure
   3. Scalable
   4. Comlpete
   5. Maintainable
   6. Portable

2. 성격

   1. 독선적 Opinionated 쉽게 할 수 있지만, 자유도가 떨어짐. 생산성이 높음. (약속된 언어, 방식이 많다)
   2. 관용적 Unopinionated 개발자가 처음부터 손볼 것들이 많지만, 자유도가 높음

3. Dynamic Web

   1. Web Application program (Web APP)

   2. 카페에 비유 = 개인창업, 프렌차이즈 창업

      A-Z 모두 직접하기 / 프레임워크사용

   3. 기본적인 필요한 재료 제공, 좋은 카페를 만드는 것에 집중!

   4. 프레임워크 사용 Express JS, Ruby on Rails, Python django, PHP Laravel, Java Spring

4. How working django?

   1. 의존성

      본인의 컴퓨터에서 잘 작동하던 프로그램도, 다른 프로그램에 설치 했을 때 잘 동작하리라는 보장이 없음.

      파이썬도 같은 버전, 같은 모듈을 쓴다는 보장이 없다.

      특정 프로그램만을 실행하기 위하 파이썬 환경을 따로 만들어서, 그 환경 속에서만 모듈을 관리하고, 앱을 실행시키기 위해 가상환경을 설정한다.

      다른 앱을 실행 시키는 일이 생기면 그 가상환경을 빠져나와 다른 환경을 만드는 방식으로 진행한다.

   2. bash 명령어 및 환경설정 하기.
   
      1. gitignore 설정하기 
   
         1. 사이트에서 django + visualcode 로 생성버튼 클릭.
         2. 폴더 최상단에 `.gitignore` 파일 생성 해당 명령어 복붙하자**.**
         3. **`### VisualStudioCode ###`  주석 아래에 `.vscode/*` 을 `.vscode`로 변경해주자**
   
      2. django 설치 전 설정
   
         ```bash
         python -m venv (가상환경 경로 + 이름)
         python -m venv ~/documents/ssafy
         ```
   
         1. 
   
         ```bash
         python -m venv venv #venv 3.7 파이썬 가상 환경을 설정
         source venv/Scripts/activate # 파이썬 가상환경 켜기
         
         pip list #환경 확인
         ```
   
         
   
         2. 
   
         ```python
         >interpreter 환경설정을 3.7.3 venv로 잡아주자.
         ```
   
         3. 
   
         ```python
         #visualcode 업데이트 깨알 꿀팁
         # json setting 들어가서 `"terminal.integrated.cwd": "${workspaceFolder}",`을 추가해 주자
         ```
   
      3. django 설치하기
   
         1. `pip install django`
   
      4. `django-admin startproject (이름 예시 + .(현재폴더에만생성))`
   
         1. ex) `django-admin startproject django_intro .`
         2. `manage.py` 파일이 생성되고, `diango_intro`폴더 안에 4가지의 파일이 생성된다.(ex) \__init__.py 등등)
   
      5. django 실행하기
   
         1. `python manage.py runserver` 명령어 입력후 
         2. `Starting development server at http://127.0.0.1:8000` 을 새로운 창으로 띄워준다.
         3. 종료시 `ctrl + c` 키로 종료 시켜 주자
   
      6. `__init__.py` : 초기화 파일, `setting.py`: 작업공간, `wsgi.py`: 아마존에 서버를 올릴 때 사용.
   
   3. MVC ( Model View Controler ) --> MTV(장고만)(Model Template View) 장고의 프레임 워크
   
      1. 역할과 기능을 각각의 파일로 쪼개주자.
   
      2. `python manage.py startapp pages`
   
      3. `view.py`에 기능별 함수들을 작성해 줄 예정.
   
      4. 프로젝트 설정 하기
   
         1. `setting.py` 파일 에서 코딩하면 된다.
         2. `INSTALLED_APPS = []` 안에 `'pages.apps.PagesConfig',` 작성한다. (`파일명.파일명.객체이름`)
            - 무조건 쉼표 (`,`) 작성하는 규칙을 항상 주의!!  == 장고 1번쨰 규약
            - 앱 등록 순서 1. local apps, 2. Third party apps
            - 한글지원 : setting.py --> I18n 국제화 `LANGUAGE_CODE = 'ko-kr'`로 변경
            - 시간변경 : TIME_ZONE = 'UTC' --> 'Asia/Seoul'
   
      5. 프로젝트 만들기
   
         1. 동작 : pages>view.py 이동 def ...
   
         2. 입구 : urls ...
   
         3. 창고 : templates 폴더 만들기 : 필요한 자료 (페이지 저장)
   
            - 정리 : 코드 작성 순서  
            - 1. 만들고자 하는 view 함수 작성
              2. urls : views에서 만든 함수에 주소를 연결
              3. templates: 해당 view 함수가 호출 될때, 보여질 페이지
            - 실습 : view 함수 이름은  introduce, introduce.html 보여주는 프로젝트.
   
         4. \###django imports style guide ###
   
            \# 1. stndard library
   
            \# 2. third-party
   
            \# 3. django
   
            \# 4. local django
   
         5. 실습 : view - image // image.html // 랜덤이미지 띄우기 picsum.photos/500/500.jpg
   
      6. 동적 페이지 만들기
   
         1. 이유 : 주소 마다 일일이 만들필요 없고, 주소 뒤쪽을 <...> 변수화 시켜주어서 변화하도록 만든다.
         2. variable routing
            - 동적 라우팅 : 기본값은 string
         3. 실습
            1. 자기소개 : introduce 확장 이름과 나이를 받아서 출력
            2. 숫가 2개를 받아 두 수의 곱셈 결과를 출력(times)
            3. 반지름 값을 받아 원의 넓이 출력(area)
   
      7. DTL (Django Template Language)
   
         1. django template 에서 사용 하는 내장 template system이다.
         2. 조건, 반복, 변수 치환, 필터 등 많은 기능을 제공한다.
         3. 실습 : is it Gwangbok? -views-isitgwangbok-현재시점이 광복절이라면 오늘은 광복절입니다라고 출력 - 아니라면 오늘은 광복절이 아닙니다를 출력
   
         
   
      -의존성 기록(구성환경 리스트 목록 만들기)
   
      pip freeze > requirements.txt
      
      -의존성 설치
      
      pip install -r requirements.txt
      
      