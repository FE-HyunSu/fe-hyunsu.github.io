---
layout: post
title: '๐จ๐ฟโ๐ Firebase Login (2์ฐจ)'
date: 2022-11-16
tags: [frontend-study]
---

## ๐ค ๊ธฐ๋ฅ ๊ตฌํ ๊ฐ์

- React Nextjs + Typescript ํ๋ก์ ํธ์ Firebase Authentication ๊ธฐ๋ฅ์ ํตํด ๋ก๊ทธ์ธ ๊ธฐ๋ฅ ์ ์ฉ, ์๋ฌ ํธ๋ค๋ง.

<br/>

### โน๏ธ TODO LIST

- ๐งฉ React nextjs typescript์ ์ ์ฉ.
- ๐โโ๏ธ Login UI ์ ์ฉ.
- ๐งโโ๏ธ JWT ํ์ฉ Login ์ ์ฉ.
- ๐ ์ํ๊ด๋ฆฌ๋ก ๋ก๊ทธ์ธ ์ํ ์ ์ง. (Recoil)
- ๐ฉ๐ปโ๐ซ Login ์ฒ๋ฆฌ์ ๋ํ ๋ฐ์ดํฐ ๋ก์ง ์ ๋ฆฌ.

<br/>

### ๐ ๋ก๊ทธ์ธ ๊ด๋ จ ๊ธฐ๋ฅ ๊ตฌ์ฑ ๊ณํ

- ์ ํจ์ฑ ์ฒดํฌ.
- ํต์ .(Firebase ์ด๋ฉ์ผ / ํจ์ค์๋)
- ํต์  ํ response๊ฐ ๋ถ๊ธฐ.
- ๋ก๊ทธ์ธ ์ ์ง.
- ๋ก๊ทธ์์ ์ฒ๋ฆฌ.

<br/>

### ๐ Firebase.js ์ํ

- firestore์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๊ธฐ ์ํด getData, setData ํจ์ ์ ์ธ ๋ฐ Auth ์ฒ๋ฆฌ ํจ์ ์ ์ธ.

```js
import { database } from './firebaseConfig';
import { collection, addDoc, getDocs } from 'firebase/firestore';
import { signInWithEmailAndPassword } from 'firebase/auth';
import { firebaseClientAuth } from '../firebase/firebaseConfig';

const getData = async (collectionName) => {
  return await getDocs(collection(database, collectionName));
};

const setData = async (collectionName, data) => {
  return await addDoc(collection(database, collectionName), data);
};

const loginAuth = async (email, password) => {
  return await signInWithEmailAndPassword(firebaseClientAuth, email, password);
};

export { getData, setData, loginAuth };
```

- ์ loginAuth ํจ์๋ฅผ ์๋ ์ปดํฌ๋ํธ์์ import, ํผ์ ์๋ ฅ๋ ์ด๋ฉ์ผ, ํจ์ค์๋ ์ ๋ณด๋ฅผ ์ธ์๊ฐ์ผ๋ก ๋ก๊ทธ์ธ ์๋.

```jsx
// email, password ์๋ ฅ๊ฐ์ ์ธ์๋ก loginAuth ํจ์ ์คํ.
const tryLogin = (email: HTMLSelectElement | null, password: HTMLInputElement | null) => {
  // validation check.
  loginAuth(email.value, password.value)
    .then((userCredential) => {
      // ๋ก๊ทธ์ธ ์ฑ๊ณต ๋ก์ง.
    })
    .catch((error) => {
      // ๋ก๊ทธ์ธ ์๋ฌ ๋ก์ง.
    });
};
```

- loginAuth ํจ์๋ฅผ ํตํด ๋ฐํ๋ Promise ๊ฐ์ฒด๋ฅผ then, catch ๋ฉ์๋๋ฅผ ํตํด ์ฑ๊ณต or ์๋ฌ ์ผ์ด์ค๋ก ๋ถ๊ธฐํ๋ค.

<br/>

---

<br/>

## ๐ฎโโ๏ธ ๋ก๊ทธ์ธ ๋ก์ง Flow ์ฒดํฌ.

(1) login ์ปดํฌ๋ํธ์์ ํผ์ ์๋ ฅ๋ ์ด๋ฉ์ผ์ฃผ์, ํจ์ค์๋ ์ ๋ณด๋ฅผ ์ธ์๊ฐ์ผ๋ก tryLogin ํจ์ ์คํ.

```jsx
// login component.
import { loginAuth } from '../../firebase/firestore';
...
// ์ธ์๋ก ๋ด๊ธด ์ด๋ฉ์ผ๊ณผ ํจ์ค์๋๋ validation check ํ loginAuth ํจ์๋ฅผ ์คํ.
const tryLogin = (email: HTMLSelectElement | null, password: HTMLInputElement | null) => {
  // validation check.
  loginAuth(email.value, password.value)
    .then((userCredential) => {
      // login success.
    })
    .catch((error) => {
      // login error.
    });
};
...
```

<br/>

(2) loginAuth ํจ์๋ async, await์ ํตํด signInWithEmailAndPassword ํจ์๋ฅผ ์คํํ๊ณ , Promise๋ฅผ ๋ฐํํจ.

```js
// firebase.js
...
import { signInWithEmailAndPassword } from 'firebase/auth';
...
const loginAuth = async (email, password) => {
  return await signInWithEmailAndPassword(firebaseClientAuth, email, password);
};
...
```

<br/>

(3) ๋ค์ login component์ tryLogin ํจ์๋ก ๋์์ ๋ฐํ๋ Promise๋ก ์ฑ๊ณต or ์๋ฌ ์ผ์ด์ค๋ก ๋ถ๊ธฐ.

- loginAuth์์ return๋ Promise๋ฅผ then-catch ์ try-catch ๋ฉ์๋๋ก ์ฒ๋ฆฌํด๋ณด๊ณ  ๋น๊ตํด๋ณด์.
- Promise ์ํ์ ํ๋ฆ์ ์ดํดํ๋ฉฐ ์ฒดํฌํด๋ณผ๊ฒ.

```js
// [Promise ์ํ 3๋จ๊ณ]
// Pending(๋๊ธฐ) : ๋น๋๊ธฐ ์ฒ๋ฆฌ ๋ก์ง์ด ์์ง ์๋ฃ๋์ง ์์ ์ํ.
// Fulfilled(์ดํ) : ๋น๋๊ธฐ ์ฒ๋ฆฌ๊ฐ ์๋ฃ๋์ด ํ๋ก๋ฏธ์ค๊ฐ ๊ฒฐ๊ณผ ๊ฐ์ ๋ฐํํด์ค ์ํ.
// Rejected(์คํจ) : ๋น๋๊ธฐ ์ฒ๋ฆฌ๊ฐ ์คํจํ๊ฑฐ๋ ์ค๋ฅ๊ฐ ๋ฐ์ํ ์ํ.
```

<br/>

---

<br/>

## ๐งต then-catch ๋ฉ์๋๋ก ์ฒ๋ฆฌํ ๊ฒฝ์ฐ.

```jsx
loginAuth(email.value, password.value)
  .then((userInfo) => {
    // login success.
  })
  .catch((error) => {
    // login error.
  });
```

- Promise ํ๋ฆ(then-catch)

<img src="../assets/images/post/img_20221120_01.png" alt="" style="width:95%; max-width:700px; min-width:300px; vertical-align:top;" />

์ถ์ฒ : [MDN:Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="\_blank"}

<img src="../assets/images/post/img_20221116_01.png" alt="" style="width:95%; max-width:700px; min-width:300px; vertical-align:top;" />

- MDN์ ์ค๋ช๋ ์๊ณ ๋ฆฌ์ฆ์ผ๋ก ๋ก์ง์ ๊ทธ๋ ค๋ดค์๋ ๊ฐ์ธ์ ์ผ๋ก ํผ์ ์ด ์์ด then-catch ๋ก์ง์ ๋ํด ๋ด๋ฐฉ์๋๋ก ์ฌ์ ๋ฆฌ ํด๋ณด์์.

<img src="../assets/images/post/img_20221119_01.png" alt="" style="width:95%; max-width:800px; min-width:300px; vertical-align:top;" />

<br/>

---

<br/>

## ๐ผ try-catch ๋ฉ์๋๋ก ์ฒ๋ฆฌํ ๊ฒฝ์ฐ.

```jsx

...
const customError = new Error('์ปค์คํ์๋ฌ');
try {
  // ์ ํจ์ฑ์ ์ถฉ์กฑํ์ง ์๋๋ค๋ฉด, throw Error;
  if(!์ ํจ์ฑ์ฒดํฌ){
    throw customError;
  }

  // loginAuth ์์.
  const returnUserInfo = await loginAuth(email.value, password.value);
  const userInfo = returnUserInfo.user;
  // login success.
  ...
} catch (error) {
  // login error.
  if(error.message === '์ปค์คํ์๋ฌ'){
    console.log('์ ๋๋ก ์๋ ฅํ๊ณ  ๋ค์์ค์ธ์.');
  } else {
    ...
  }
  ...
}
```

- ํจ์ ์คํ ์ auth api๋ฅผ ํธ์ถ ์  ์ ํจ์ฑ ์ฒดํฌ๋ฅผ ํ๊ณ , throw๋ก ์์ธ์ฒ๋ฆฌ๋ฅผ ์ ์ฉ์์ผฐ๋ค.

<img src="../assets/images/post/img_20221120_02.png" alt="" style="width:95%; max-width:700px; min-width:300px; vertical-align:top;" />

<br/>

### ๐งโโ๏ธ ์ ๋ฆฌ.

- then-catch ๋ฌธ๋ฒ์ ๋ํ์ ์ธ ๋จ์ ์ผ๋ก chaining ํ์์ ๋๋ง ์ธ์งํ๊ณ  ์์๋ค.
- ์ ์ฐํ Error ์ฒ๋ฆฌ๋ฅผ ์ํด then-catch ์์์๋ try-catch๋ฅผ ์ฌ์ฉํ๊ฒ ๋ ๊ฒ.
- ์ฝ๋์ ๊ฐ๋์ฑ ๋ฐ ์ ์ง๋ณด์ ํจ์จ์ฑ์ ์ํด then-catch ๋ณด๋ค๋ try-catch๋ฅผ ์ฌ์ฉํ๋๋ก ํ์.

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0](https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0){:target="\_blank"}
- [https://hungseong.tistory.com/67](https://hungseong.tistory.com/67){:target="\_blank"}
- [https://joshua1988.github.io/web-development/javascript/promise-for-beginners](https://joshua1988.github.io/web-development/javascript/promise-for-beginners){:target="\_blank"}
- [https://velog.io/@vraimentres/async-%ED%95%A8%EC%88%98%EC%99%80-try-catch](https://velog.io/@vraimentres/async-%ED%95%A8%EC%88%98%EC%99%80-try-catch){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then){:target="\_blank"}
- [https://eundol1113.tistory.com/m/226](https://eundol1113.tistory.com/m/226){:target="\_blank"}
- [https://velog.io/@design0728/clean-code-typescript-%EC%97%90%EB%9F%AC%EC%B2%98%EB%A6%ACError-Handling](https://velog.io/@design0728/clean-code-typescript-%EC%97%90%EB%9F%AC%EC%B2%98%EB%A6%ACError-Handling){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="\_blank"}
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw){:target="\_blank"}
- [https://anerim.tistory.com/63](https://anerim.tistory.com/63){:target="\_blank"}
- [https://www.youtube.com/watch?v=FXtooPhupr4](https://www.youtube.com/watch?v=FXtooPhupr4){:target="\_blank"}
  <br/><br/>

---
