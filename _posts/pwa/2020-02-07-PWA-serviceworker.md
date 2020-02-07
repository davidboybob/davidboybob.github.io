---
layout: post
title:  "ServiceWorker"
date:   2020-2-6 00:00:00
categories: Pwa
image: pwa.png
description: 서비스 워커와 라이프 싸이클(주기)
tags: PWA
comments: true
---



# SERVICE WORKER

## 1. 정의

- 브라우저가 백그라운드에서 실항하는 스크립트로, 웹페이지와는 별개로 작동함.
- 푸시알림 백그라운드 동기화 기능 제공.
- 프로그래밍 가능한 네트워크 프록시로 페이지의 네트워크 요청 처리 방법을 제어.



`과제 : 프라미스에 대해서 공부하기`

https://developers.google.com/web/fundamentals/primers/promises?hl=ko

## 2. 서비스 워커 등록하기

- navigator에 서비스워커가 등록되어 있다.

```javascript
// app.js

if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('../service-worker.js').then(() => {
    console.log(navigator.serviceWorker)
    console.log('Service Worker Registered');
  });
}
```

- 서비스 워커의 수명 주기는 웹페이지와 완전히 별개임.
- 서비스 워커를 사이트에 설치하려면 페이지에서 자바스크립트를 이용하여 등록.
- 서비스 워커를 등록하면 브라우저가 백그라운드에서 서비스 워커 설치.



- life cycle
  - Installing
    - 