---
layout: post
title:  "Hash tag"
date:   2019-10-24 00:00:00
categories: Django
image: django.png
description: Article의 해쉬태그 만들기.
tags: python 파이썬 Django 
comments: true
---

# Hash Tags

Article(게시글)과 M:N 관계



get_or_create(defaults=None, **kwargs)

- 주어진 kwargs 로 객체를 찾으며 필욯나 경우 하나를 만든다.
- (object, created) 형태의 튜플을 리턴한다.
- object는 검색 또는 생성된 객체이고, created 는 새 객체 생성 여부를 지정하는 boolean 값이다. (새로만들어진 object라면 True, 기존에 존재하던 object라면 False)
- 단, 이 메서드는 DB가 키워드 인자의 `unique`옵션을 강제하고 있다고 가정하고 실행된다. (중복 방지)
- 이는 요청이 병렬로 작성 될 때, 중복 코드에 대한 문제 방지로 중복 오브젝트가 작성되는 것을 예방한다.



unique

- True인 경우 이 필드는 테이블 전체에서 고유한 값이어야 한다.
- 유효성 검사 단계에서 실행되며, 중복 값이 있는 모델을 저장하려고 하면, .save() 메서드로 인해 'IntegrityError'가 발생한다. 
- ManyToManyField 및 OneToOneField를 제외한 모든 필드에서 유효하다.



Update

수정할 때는 게시글의 hashtag 전체를 삭제한 후 다시 등록하는 과정.