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

## 🪖 Firebase 데이터 연동 셋팅

#### 1. Firebase npm package 설치.

```javascript
$ npm install firebase
```

#### 2. firebaseConfig.js 파일 추가. (개인 인증키 가림 - [링크](https://github.com/FE-HyunSu/accountbook.v2/blob/main/firebaseConfig.js){:target="\_blank"})

```js
// firebaseConfig.js
// Import the functions you need from the SDKs you need
import { initializeApp } from 'firebase/app';
import { getFirestore } from 'firebase/firestore';
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: FIREBASE_API_KEY,
  authDomain: FIREBASE_AUTH_DOMAION,
  projectId: FIREBASE_PROJECT_ID,
  storageBucket: FIREBASE_STORAGE_BUCKET,
  messagingSenderId: FIREBASE_MESSAGING_SENDER_ID,
  appId: FIREBASE_APP_ID,
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const database = getFirestore(app);
```

#### 3. 컴포넌트에서 Firebase firestore database 호출.

```tsx
// firebaseConfig.js에서 export한 app, database 를 import.
import { app, database } from '../../../firebaseConfig';
// firesotre에서 제공하는 함수를 import.
import { collection, addDoc, getDocs } from 'firebase/firestore';
...

// Firestore 데이터 호출 방법1.
const db = firebase.firestore();
db.collection('생성한 컬렉션 이름').get().then((result)=>{
  console.log(result);
});

// Firestore 데이터 호출 방법2.
const db = firebase.firestore();
db.collection('product') //원하는 컬렉션 선택하기, 지금은 product를 선택함
  .where('원하는 조건1') // 쿼리 조건 설정
  .where('원하는 조건2') // 쿼리 조건은 여러개 설정 가능함
  .orderBy('오름차순 내림차순?') // 정렬방식 최신자료 먼저 정렬 가능함
  .limit(10) // 가지고 오는 갯수를 제한 할 수 있다.
  .doc('원하는 도큐먼트') // 원하는 도큐먼트 선택하기
  .get() // 이제까지 정보를 통해 자료를 가져오라는 의미
  .then((result) => { // 결과를 then으로 받을 수 있다.
    console.log(result);
  });
```

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

## 📝 Develop3 : Firebase Data 연동 방식 수정

- ver1 에서 Firebase Data 정보를 accountList 컴포넌트에서 직접 불러왔음.
- 코드의 가독성 및 비효율적인 관리와 호출이 일어나고 있어, 개선. (근영님 추천)
- firebase 관련 파일 폴더 정리 및 데이터 호출 컴포넌트 추가. (컴포넌트 역할 분리)

```tsx
// 작성중..
```

<br/>

---
