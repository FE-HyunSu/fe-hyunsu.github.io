---
layout: post
title: '📟 AccountBook develop (작성중)'
date: 2022-11-10
tags: [frontend-study]
---

## 🔉 AccountBook project migration

- AccountBook project 를 nextjs + Typescript 로 migration.
- 기존 작성했던 [Nextjs+Ts](https://fe-hyunsu.github.io/next_ts){:target="\_blank"}을 참고하여 기본 셋팅 진행.

<br/>

## 📻 Add Package

- firebase : firebase firestore에 등록한 데이터 연동을 위해 package 설치.

<br/>

## 🪂 Component convention

- component를 나누는 기준을 UI와 기능으로 나눔.
- 모든 component는 폴더로 관리하고, 폴더안에 index 와 style 컴포넌트를 분리했다.
- 이렇게 관리하려는 이유는, 해당 컴포넌트의 목적성을 명확히 갖기 위함.

```
// components 폴더 구조 예시
|-- [components]
  |-- [accountList]
    |-- [index.tsx]
    |-- [style.tsx]
  |-- [layout]
    |-- [header]
      |-- index.tsx
      |-- style.tsx
    |-- [footer]
      |-- index.tsx
      |-- style.tsx
...
```

<br/>

## 📚 Folder tree.

```jsx
|-- [.next]
|-- [node_modules]
|-- [pages]
|-- [components]
|-- [public]
|-- [styles]
|-- next-env.d.ts
|-- next.config.js
|-- package-lock.json
|-- package.json
|-- README.md
|-- tsconfig.json
```

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://defineall.tistory.com/919](https://defineall.tistory.com/919){:target="\_blank"}
  <br/><br/>

---
