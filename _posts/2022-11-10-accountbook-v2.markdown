---
layout: post
title: '📟 AccountBook develop'
date: 2022-11-11
tags: [frontend-study]
---

## 🔉 AccountBook project migration

- AccountBook project 를 nextjs + Typescript 로 migration.
- 기존 작성했던 [Nextjs+Ts](https://fe-hyunsu.github.io/next_ts){:target="\_blank"}을 참고하여 기본 셋팅 진행.

<br/>

## 📺 URL

- [https://tubular-cocada-39cf07.netlify.app](https://tubular-cocada-39cf07.netlify.app){:target="\_blank"}

<br/>

## 📻 Add Package

- firebase : firebase firestore에 등록한 데이터 연동을 위해 package 설치.

<br/>

## 🪂 Component convention

- 페이지를 구성하는 영역은 UI와 기능을 기준으로 component를 나눔.
- 모든 영역은 폴더로 관리하고, 폴더안에 style.tsx, index.tsx 로 분리.
- 이와 같은 관리 포인트는 컴포넌트의 목적성을 명확히 갖기 위함.

<br/>

## 📚 Folder tree.

```jsx
|-- [components] // 컴포넌트 폴더
    ㄴ[accountList] // 페이지
      ㄴ[item] // 영역
       ㄴ index.tsx // 구조 or 기능
       ㄴ style.tsx // UI
      ㄴ[list]
       ㄴ index.tsx
       ㄴ style.tsx
    ㄴ[layout]
      ㄴ[header]
        ㄴ index.tsx
        ㄴ style.tsx
      ㄴ[footer]
        ㄴ index.tsx
        ㄴ style.tsx
|-- [pages]
    ㄴ _app.tsx
    ㄴ _document.tsx
    ㄴ index.tsx
|-- [public]
    ㄴ ...
|-- [styles]
    ㄴ global-style.ts // reset style
    ㄴ styled.d.ts
    ㄴ theme.ts
|-- .babelrc // SSR styled-components 이슈해결을 위한 설정값 지정.
|-- .gitignore
|-- firebaseConfig.js
|-- next-env.d.ts
|-- next.config.js
|-- package-lock.json
|-- package.json
|-- README.md
|-- tsconfig.json
```

<br/>

## 🤾‍♂️ Develop1 : totalPrice 업데이트 시 count action

- 초기 totalPrice값을 보여줄때 or 특정 유저를 선택하여, totalPrice 값이 업데이트 될때 count action 적용.
- number type의 매개변수를 갖는 countEffect 함수 생성.

```tsx
...
 const countEffect = (num: number) => {
    let viewCount = 0;
    let gap = (num / 30) * (num > 0 ? 1 : -1);

    let countInterval = setInterval(() => {
      if (viewCount >= Math.abs(num)) {
        clearInterval(countInterval);
        setTotalPrice(addComa(num));
      } else {
        viewCount = viewCount + gap;
        setTotalPrice(addComa(Math.floor(viewCount)));
      }
    }, 16);
  };
...
```

<br/>

## 🤹‍♂️ Develop2 : AccountCard 호출 시 Motion 적용

- AccountCard 컴포넌트가 렌더링 될때, animation 이 적용되도록 적용.
- 순차 animation을 적용하기 위해 컴포넌트 style에 animationDelay를 시간차로 적용.

```tsx
...
<AccountCard style={{ animationDelay: itemIndex * 0.1 + `s` }}>
  <dt>
    <span>{shortDate(dateTime.split(' ')[0])}</span>
    <strong>{Number(price) > 0 ? accountName : description}</strong>
  </dt>
  <dd className={Number(price) > 0 ? `plus` : `minus`}>{addComa(price)}</dd>
</AccountCard>
...
```

<br/>

---
