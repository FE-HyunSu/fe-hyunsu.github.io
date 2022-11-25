---
layout: post
title: '🦹🏼‍♀️ Nextjs _app, _document'
date: 2022-11-25
tags: [frontend-study]
---

## 🧚 \_app.tsx와 \_document.tsx

<img src="../assets/images/post/img_20221125_01.png" alt="" style="width:100%; min-width:300px;" alt="" />
- Nextjs 프로젝트 진행 시 \_app.tsx와 \_document.tsx에 대해 알아보자.

<br/>

### 🧜🏻‍♂️ \_app.tsx

- 컴포넌트 위치 : pages/\_app.tsx
- 실행 시점 : Nextjs는 기본적으로 SSR(Server Side Rendering)으로 동작되고, Server로 요청이 들어왔을때 최초로 실행되는 컴포넌트.
- 모든 페이지는 해당 컴포넌트를 거치게 되며, 모든 레이아웃을 구성한다.
- Server로 요청이 들어왔을때 최초로 실행되므로, 최초 접근 시 Client에서 시도하려는 제어는 적용되지 않는다.
- 개인적으로 전역으로 사용될 theme style과, 상태관리를 위한 셋팅을 적용했다.

<br/>

### 🧝‍♂️ \_document.tsx

- 컴포넌트 위치 : pages/\_document.tsx
- nextjs에서 제공하는 html 문서를 커스터마이징 할 수 있음.
- 공통적으로 사용할 head / mete / font / 웹 접근성 설정 / body 등을 커스터마이징 할 때 활용.
- Content들을 브라우저가 html로 이해하도록 구조화 시킴.
- \_app.tsx 컴포넌트 다음으로 실행된다.
- 해당 컴포넌트 내 render 함수를 통해, 첫 페이지가 노출되는데, 여기서 styled-components를 함께 사용하는 경우, render 함수가 실행되기 전 호출해야 최초 페이지 접근 시 style이 없는 상태로 잠깐 노출되는 현상을 방지할 수 있다.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://velog.io/@woodong/2.-app.tsx-%EC%99%80-document.tsx](https://velog.io/@woodong/2.-app.tsx-%EC%99%80-document.tsx){:target="\_blank"}
- [https://merrily-code.tistory.com/154](https://merrily-code.tistory.com/154){:target="\_blank"}
- [https://asperbrothers.com/blog/server-side-rendering-in-react](https://asperbrothers.com/blog/server-side-rendering-in-react){:target="\_blank"}
  <br/><br/>

---
