---
layout: post
title: "๐ AccountBook develop"
date: 2022-11-12
tags: [retrospect]
---

## ๐ AccountBook project migration

- AccountBook project ๋ฅผ nextjs + Typescript ๋ก migration.
- ๊ธฐ์กด ์์ฑํ๋ [Nextjs+Ts](https://fe-hyunsu.github.io/next_ts){:target="\_blank"}์ ์ฐธ๊ณ ํ์ฌ ๊ธฐ๋ณธ ์ํ ์งํ.

<br/>

## ๐บ URL

- ํ์ด์ง URL : [https://tubular-cocada-39cf07.netlify.app](https://tubular-cocada-39cf07.netlify.app){:target="\_blank"}
- Github ์ ์ฅ์ : [https://github.com/FE-HyunSu/accountbook.v2](https://github.com/FE-HyunSu/accountbook.v2){:target="\_blank"}

<br/>

## ๐ช Firebase ๋ฐ์ดํฐ ์ฐ๋ ์ํ

#### 1. Firebase npm package ์ค์น.

```javascript
$ npm install firebase
```

#### 2. firebaseConfig.js ํ์ผ ์ถ๊ฐ. (๊ฐ์ธ ์ธ์ฆํค ๊ฐ๋ฆผ)

```js
// firebaseConfig.js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: process.env.NEXT_PUBLIC_FIREBASE_APIKEY,
  authDomain: process.env.NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.NEXT_PUBLIC_FIREBASE_PROJECT_ID,
  storageBucket: process.env.NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID,
  appId: process.env.NEXT_PUBLIC_FIREBASE_APP_ID,
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const database = getFirestore(app);
```

#### 3. ์ปดํฌ๋ํธ์์ Firebase firestore database ํธ์ถ.

```tsx
// firebaseConfig.js์์ exportํ app, database ๋ฅผ import.
import { app, database } from '../../../firebaseConfig';
// firesotre์์ ์ ๊ณตํ๋ ํจ์๋ฅผ import.
import { collection, addDoc, getDocs } from 'firebase/firestore';
...

// Firestore ๋ฐ์ดํฐ ํธ์ถ ๋ฐฉ๋ฒ1.
const db = firebase.firestore();
db.collection('์์ฑํ ์ปฌ๋ ์ ์ด๋ฆ').get().then((result)=>{
  console.log(result);
});

// Firestore ๋ฐ์ดํฐ ํธ์ถ ๋ฐฉ๋ฒ2.
const db = firebase.firestore();
db.collection('product') //์ํ๋ ์ปฌ๋ ์ ์ ํํ๊ธฐ, ์ง๊ธ์ product๋ฅผ ์ ํํจ
  .where('์ํ๋ ์กฐ๊ฑด1') // ์ฟผ๋ฆฌ ์กฐ๊ฑด ์ค์ 
  .where('์ํ๋ ์กฐ๊ฑด2') // ์ฟผ๋ฆฌ ์กฐ๊ฑด์ ์ฌ๋ฌ๊ฐ ์ค์  ๊ฐ๋ฅํจ
  .orderBy('์ค๋ฆ์ฐจ์ ๋ด๋ฆผ์ฐจ์?') // ์ ๋ ฌ๋ฐฉ์ ์ต์ ์๋ฃ ๋จผ์  ์ ๋ ฌ ๊ฐ๋ฅํจ
  .limit(10) // ๊ฐ์ง๊ณ  ์ค๋ ๊ฐฏ์๋ฅผ ์ ํ ํ  ์ ์๋ค.
  .doc('์ํ๋ ๋ํ๋จผํธ') // ์ํ๋ ๋ํ๋จผํธ ์ ํํ๊ธฐ
  .get() // ์ด์ ๊น์ง ์ ๋ณด๋ฅผ ํตํด ์๋ฃ๋ฅผ ๊ฐ์ ธ์ค๋ผ๋ ์๋ฏธ
  .then((result) => { // ๊ฒฐ๊ณผ๋ฅผ then์ผ๋ก ๋ฐ์ ์ ์๋ค.
    console.log(result);
  });
```

<br/>

## ๐ช Component convention

- ํ์ด์ง๋ฅผ ๊ตฌ์ฑํ๋ ์์ญ์ UI์ ๊ธฐ๋ฅ์ ๊ธฐ์ค์ผ๋ก component๋ฅผ ๋๋.
- ๋ชจ๋  ์์ญ์ ํด๋๋ก ๊ด๋ฆฌํ๊ณ , ํด๋์์ style.tsx, index.tsx ๋ก ๋ถ๋ฆฌ.
- ์ด์ ๊ฐ์ ๊ด๋ฆฌ ํฌ์ธํธ๋ ์ปดํฌ๋ํธ์ ๋ชฉ์ ์ฑ์ ๋ชํํ ๊ฐ๊ธฐ ์ํจ.

<br/>

## ๐ Folder tree.

```jsx
|-- [components] // ์ปดํฌ๋ํธ ํด๋
    ใด[accountList] // ํ์ด์ง
      ใด[item] // ์์ญ
       ใด index.tsx // ๊ตฌ์กฐ or ๊ธฐ๋ฅ
       ใด style.tsx // UI
      ใด[list]
       ใด index.tsx
       ใด style.tsx
    ใด[layout]
      ใด[header]
        ใด index.tsx
        ใด style.tsx
      ใด[footer]
        ใด index.tsx
        ใด style.tsx
|-- [pages]
    ใด _app.tsx
    ใด _document.tsx
    ใด index.tsx
|-- [public]
    ใด ...
|-- [styles]
    ใด global-style.ts // reset style
    ใด styled.d.ts
    ใด theme.ts
|-- .babelrc // SSR styled-components ์ด์ํด๊ฒฐ์ ์ํ ์ค์ ๊ฐ ์ง์ .
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

## ๐คพโโ๏ธ Develop1 : totalPrice ์๋ฐ์ดํธ ์ count action

- ์ด๊ธฐ totalPrice๊ฐ์ ๋ณด์ฌ์ค๋ or ํน์  ์ ์ ๋ฅผ ์ ํํ์ฌ, totalPrice ๊ฐ์ด ์๋ฐ์ดํธ ๋ ๋ count action ์ ์ฉ.
- number type์ ๋งค๊ฐ๋ณ์๋ฅผ ๊ฐ๋ countEffect ํจ์ ์์ฑ.

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

## ๐คนโโ๏ธ Develop2 : AccountCard ํธ์ถ ์ Motion ์ ์ฉ

- AccountCard ์ปดํฌ๋ํธ๊ฐ ๋ ๋๋ง ๋ ๋, animation ์ด ์ ์ฉ๋๋๋ก ์ ์ฉ.
- ์์ฐจ animation์ ์ ์ฉํ๊ธฐ ์ํด ์ปดํฌ๋ํธ style์ animationDelay๋ฅผ ์๊ฐ์ฐจ๋ก ์ ์ฉ.

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

## ๐ Develop3 : Firebase Data ์ฐ๋ ๋ฐฉ์ ์์ 

- ver1 ์์ Firebase Data ์ ๋ณด๋ฅผ accountList ์ปดํฌ๋ํธ์์ ์ง์  ๋ถ๋ฌ์์.
- ์ฝ๋์ ๊ฐ๋์ฑ ๋ฐ ๋นํจ์จ์ ์ธ ๊ด๋ฆฌ์ ํธ์ถ์ด ์ผ์ด๋๊ณ  ์์ด, ๊ฐ์ . (๊ทผ์๋ ์ถ์ฒ)
- firebase ๊ด๋ จ ํ์ผ ํด๋ ์ ๋ฆฌ ๋ฐ ๋ฐ์ดํฐ ํธ์ถ ์ปดํฌ๋ํธ ์ถ๊ฐ. (์ปดํฌ๋ํธ ์ญํ  ๋ถ๋ฆฌ)
- firebase config ํ์ผ.

```javascript
// firebase.js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

const firebaseConfig = {
  apiKey: process.env.NEXT_PUBLIC_FIREBASE_APIKEY,
  authDomain: process.env.NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.NEXT_PUBLIC_FIREBASE_PROJECT_ID,
  storageBucket: process.env.NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID,
  appId: process.env.NEXT_PUBLIC_FIREBASE_APP_ID,
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const database = getFirestore(app);
```

- firestore์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๊ธฐ ์ํด getData, setData ํจ์ ์ ์ธ.

```javascript
// firestore.js
import { database } from "./firebaseConfig";
import { collection, addDoc, getDocs } from "firebase/firestore";

const getData = async (collectionName) => {
  return await getDocs(collection(database, collectionName));
};
const setData = async (collectionName, data) => {
  return await addDoc(collection(database, collectionName), data);
};
export { getData, setData };
```

<br/>

## ๐ Develop4 : ํ๊ฒฝ๋ณ์ ์ ์ฉ(.env)

- nextjs ์์๋ envํ์ผ์ ํ๋ฆฌํฝ์ค๋ฅผ NEXT_PUBLIC ๋ก ์ค์ ํ ๊ฒ.

```jsx
// ์ ์ฉ ์ฐ์ ์์ ์์๋ก ์์ฑ.
// 1) .env.local : ๋ค๋ฅธ ํ์ผ๋ค์ ์ ์๋ ๊ฐ๋ค์ ๋ชจ๋ ๋ฎ์ด์ด๋ค.
// 2) .env.test : ํ์คํธ ํ๊ฒฝ(process.env.NODE_ENV === 'test') ์์ ์ ์ฉ๋๋ค.
// 3) .env.production : ๋ฐฐํฌ/๋น๋ ํ๊ฒฝ(process.env.NODE_ENV === 'production') ์์ ์ ์ฉ๋๋ค.
// 4) .env.development : ๊ฐ๋ฐ ํ๊ฒฝ(process.env.NODE_ENV === 'development') ์์ ์ ์ฉ๋๋ค.
// 5) .env : ๋ชจ๋  ํ๊ฒฝ์์ ๊ณตํต์ ์ผ๋ก ์ ์ฉํ  ๋ํดํธ ํ๊ฒฝ๋ณ์๋ฅผ ์ ์ํ๋ค. ๊ฐ์ฅ ์ฐ์ ์์๊ฐ ๋ฎ๋ค.
```

- .env ํ์ผ์ ๋ฐฐํฌ ์๋ฒ์ ์ง์  ์ฌ๋ ค์ผ ํ๊ธฐ๋๋ฌธ์ ๋ฐฐํฌํ๋ netlify ํ์ด์ง์ ์ง์  ๋ฐฐํฌํจ.
- netlify ์ฌ์ดํธ ๋ก๊ทธ์ธ ํ ํด๋น ํ๋ก์ ํธ์ Build & deploy -> Environment -> Environment variables -> Edit variables ์ง์.
  <img src="../assets/images/post/img_20221113_01.png" alt="" style="width:90%; max-width:700px; min-width:300px;" />

- ๋ณ์๋ช๊ณผ ํค๊ฐ ์๋ ฅ.

  <img src="../assets/images/post/img_20221113_02.png" alt="" style="width:90%; max-width:700px; min-width:300px;" />

- ๋ฐฐํฌ, ์ ์ฉ๊ฒฐ๊ณผ ์ฑ๊ณต.

  <img src="../assets/images/post/img_20221113_03.png" alt="" style="width:70%; max-width:500px; min-width:300px;" />

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://velog.io/@edbera/react-admin-firebase-%EC%9D%98-api-key%EB%A5%BC-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98%EB%A1%9C-%EB%B3%B4%ED%98%B8%ED%95%98%EA%B8%B0](https://velog.io/@edbera/react-admin-firebase-%EC%9D%98-api-key%EB%A5%BC-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98%EB%A1%9C-%EB%B3%B4%ED%98%B8%ED%95%98%EA%B8%B0){:target="\_blank"}
- [https://curryyou.tistory.com/503](https://curryyou.tistory.com/503){:target="\_blank"}
- [https://kyounghwan01.github.io/blog/etc/netlify-env/](https://kyounghwan01.github.io/blog/etc/netlify-env/){:target="\_blank"}
  <br/>

---
