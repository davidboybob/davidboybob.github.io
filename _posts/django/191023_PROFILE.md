---
layout: post
title:  "USER의 PROFILE"
date:   2019-10-23 00:00:00
categories: Django
image: django.png
description: 유저의 프로필 구현 구상 및 방법
tags: python 파이썬 Django 
comments: true
---

1. 유저가 작성한 게시글 목록
2. 유저가 작성한 댓글 목록
3. 정렬은 모두 최근에 작성한 것부터
4. 각 게시글의 부가정보까지(좋아요, 댓글 몇개 달렸는지)



`with` templates tag

- 복잡한 변수를 더 간단한 이름으로 저장(캐시)하며, 여러번 DB를 조회할 때 (특히 비용이 많이 드는) 유용하게 사용가능하다.



게시글 + 댓글 CRUD 전부( 파일 업로드 제외)

CSS나 bootstrap4  라이브러리는 필요없음

좋아요 구현까지

AUTH(회원가입/로그인/로그아웃 기능)

회원수정 등은 제외





M:N FLLOW