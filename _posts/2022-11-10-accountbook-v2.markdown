---
layout: post
title: '📟 AccountBook develop (작성중)'
date: 2022-11-10
tags: [frontend-study]
---

## 🔉 AccountBook project migration

- AccountBook project 를 nextjs + Typescript 로 migration.

<br/>

## 📰 .babelrc

- nextjs 프로젝트 진행 시 styled-components으로 적용한 style이 제대로 적용되지 않는다.
- 이유는 styled-components의 style이 적용전에 렌더링이 되기 때문.
- .babelrc 파일을 통해서, styled-components 설정값을 지정함.

```tsx
{
  "presets": ["next/babel"],
  "plugins": [
    [
      "babel-plugin-styled-components",
      {
        "fileName": true, // 코드가 포함된 파일명을 알려줌
        "displayName": true, // 클래스명에 해당 스타일 정보 추가
        "pure": true // 사용하지 않은 속성 제거
      }
    ]
  ]
}
```

<br/>

## 📚 Folder tree.

```
|-- [.next]
|-- [node_modules]
|-- [pages]
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
