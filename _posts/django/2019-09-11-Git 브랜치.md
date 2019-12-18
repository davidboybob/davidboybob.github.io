---
layout: post
title:  "Git branch 협업을 위한 툴"
date:   2019-09-11 00:00:00
categories: Django
image: django.png
description: Git 브랜치에 대한 설명 및 방법
tags: python 파이썬 Django Git Branch
comments: true
---

# Git 브랜치

- 브랜치(나뭇가지의 비유적 표현 )

## 1. 개요

1. 특징

   - 매우 가볍다
   - 순식간에 브랜치를 만들고 브랜치 사이를 이동할 수 있다.
   - Git 이 가지고 온 혁신 중 하나는 브랜치 기능을 매우 쓸만한 수준까지 만들었다는 것

   

2. 브랜치 만들기

   ```bash
   git init (최초의 한번만 설정하여서 master 생성하기)
   git branch branch_name
   touch a.txt
   touch b.txt
   git branch ssafy (ssafy 라는 브랜치를 생성)
   git checkout ssafy (master -> ssafy로 이동)
   
   --> git checkout -b branch_namet
   ```

   

   1. fast commit

      ```bash
      
      ```

   2. merge commit

      ```bash
      $ git log --oneline --graph
      *   f0e7ac5 (HEAD -> master) Merge branch 'feature/signout'
      |\
      | * 1b87cc3 (feature/signout) Complete login.txt
      | * ddbe115 Complete signout.txt
      * | 9ef1a3d Make master.txt
      |/
      * ee3c1a7 (feature/test) complete test.txt
      * 9964750 first commit
      
      ```

   3.  merge-conflict

      ```bash
      $ git merge feature/article
      Auto-merging a.txt
      CONFLICT (content): Merge conflict in a.txt
      Automatic merge failed; fix conflicts and then commit the result.
      ---- 충돌 ---
      해당 파일 수정 후 
      git add .
      git commit
      ---- merge창 ----
      esc :wq 로 탈출
      
      ```

      

3. PULL request

   - 기능 개발을 끝내고 master 에 바로 병합시키는게 아니라, 브랜치를 중앙 원격 저장소에 올리고(push) master에 병합을 요청(merge)
   - 주의) 중앙엣 병합을 했다면, 다른 팀원들은 master 브랜치를 pull 받아야 한다.

4. Forking workflow

   - git remote add upstream [중앙 원격 저장소 주소]
   - git remote -V
   - git checkout -b feature/login
   - git push -u origin feature/login
   - 



2. merge commit

   1. feature/login 이동

      ```bash
      $ git checkout -b feature
      ```



3. Vim 에디터로 열림
4. 메세지를 수정하곶 ㅏ하면 `i`를 편집 모드로 바꾼 다음에 commit을 