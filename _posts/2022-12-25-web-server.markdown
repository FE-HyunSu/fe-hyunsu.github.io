---
layout: post
title: "🚂 Web & WAS"
date: 2022-12-29
tags: [backend-study]
---

## ⛲️ Server 구성 및 요청 흐름.

<img src="../assets/images/post/img_20221229_01.png" alt="" style="width:90%; max-width:800px; margin: auto 1rem; vertical-align:top;" />

<br/>

## 🌏 Web Server가 하는일.

- (1) 클라이언트로 부터 HTTP 요청을 받을 수 있다.
- (2) 요청받은 정적 컨텐츠를 제공할 수 있다. (html, png, css 등)
- (3) 동적 컨텐츠 요청을 받은 경우, WAS로 전달하여 WAS가 처리한 결과를 클라이언트에게 전달.

<br/>

## 📡 WAS(Web Application Server)

- (1) 클라이언트로 부터 HTTP 요청 및 요청받은 정적 컨텐츠를 제공할 수 있음. (대부분의 WAS는 Web Server가 내장되어 있기 때문)
- (2) DB조회나 다양한 로직 처리를 위해 동적 컨텐츠를 제공.

<br/>

## 🔌 Containner

- 컨테이너는 동적인 데이터들을 처리하여 정적인 페이지로 생성해주는 소프트웨어 모듈.
- 사용자가 로그인해서 MyPage 메뉴에 들어간다고 가정했을때 이 메뉴에서는 각자 사용자에 따라 보여질 정보가 다름.
- 사용자의 요청이 들어오면 웹 서버는 정적인 요소만 클라이언트 측에 보낼 수 있고, 동적으로 처리해야 하는 부분은 처리할 수 없음.
- 컨테이너는 이러한 부분을 대신 처리해서 웹 서버에 정적인 파일로 만들어서 보내주는 모듈.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://www.youtube.com/watch?v=mcnJcjbfjrs](https://www.youtube.com/watch?v=mcnJcjbfjrs){:target="\_blank"}
- [https://www.youtube.com/watch?v=NyhbNtOq0Bc](https://www.youtube.com/watch?v=NyhbNtOq0Bc){:target="\_blank"}
- [https://kyungjinsprogramming.tistory.com/3](https://kyungjinsprogramming.tistory.com/3){:target="\_blank"}
  <br/><br/>

---
