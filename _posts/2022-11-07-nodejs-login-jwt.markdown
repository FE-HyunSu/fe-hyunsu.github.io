---
layout: post
title: '๐งโ๐ Firebase Login (1์ฐจ)'
date: 2022-11-15
tags: [frontend-study]
---

## ๐ฅฎ Firebase Login ๊ธฐ๋ฅ ๊ตฌํ

- Firebase Authentication ๊ธฐ๋ฅ์ ํตํด ๋ก๊ทธ์ธ ๊ธฐ๋ฅ ์ ์ฉ.
- 1์ฐจ : nodejs express ์ํ ํ html์์ ๊ตฌํ.
- 2์ฐจ : react nextjs + typescript ํ๋ก์ ํธ์ ์ ์ฉ.
- ๊ธฐ์กด Firebase ์์ฑํด๋์ ํ๋ก์ ํธ๋ฅผ ํ์ฉํด์, ๋ก๊ทธ์ธ ํ์ด์ง ๊ตฌํ.

<br/>

## ๐ต 1์ฐจ.

### ๐น Firebase set.

- firebase-tools, login, init.

```js
// firebase-tools.
$ npm install -g firebase-tools@9.12.1

// firebase Login.
$ firebase login

// firebase init.
$ firebase init
```

- Setting..

<img src="../assets/images/img_firebase_init.png" alt="" style="width:90%; max-width:700px; min-width:300px; vertical-align:top;" />

- Use an existing project.

<img src="../assets/images/img_firebase_set.png" alt="" style="width:90%; max-width:600px; min-width:300px; vertical-align:top;" />

<img src="../assets/images/img_firebase_set_end.png" alt="" style="width:90%; max-width:600px; min-width:300px; vertical-align:top;" />

- Firebase Authentication ์์ ๊ณ์  ์ถ๊ฐ.

<img src="../assets/images/post/img_20221108_01.png" alt="" style="width:90%; max-width:700px; min-width:300px; vertical-align:top;" />

- Firebase ํ๋ก์ ํธ ์ค์ ์์, CDN ํ์์ผ๋ก ์ ์ฉ.

<img src="../assets/images/post/img_20221108_02.png" alt="" style="width:90%; max-width:600px; min-width:300px; vertical-align:top;" />

- Firebase์์ '์ด๋ฉ์ผ ์ฃผ์์ ๋น๋ฐ๋ฒํธ๋ก ์ฌ์ฉ์ ๋ก๊ทธ์ธ' ๊ธ ์ฐธ์กฐํ์ฌ ์ํ.
- ๊ธฐ์กด 'firebase/auth' -> https://www.gstatic.com/firebasejs/9.13.0/firebase-auth.js ๋ก ๋ณ๊ฒฝํ๋ค.
- [https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko](https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko){:target="\_blank"}

```jsx
import {
  getAuth,
  signInWithEmailAndPassword,
} from 'https://www.gstatic.com/firebasejs/9.13.0/firebase-auth.js';

const auth = getAuth();
signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in
    const user = userCredential.user;
    // ...
  })
  .catch((error) => {
    const errorCode = error.code;
    const errorMessage = error.message;
  });
```

- ์ ๋ด์ฉ์ ๊ธฐ๋ฐ์ผ๋ก, ์คํฌ๋ฆฝํธ ์์ .
- ๊ธฐ๋ฅ ํ์ธ์ ์ํด UI ์์ด ์ ์ฉํด๋ด.

<img src="../assets/images/post/img_20221108_03.png" alt="" style="width:90%; max-width:300px; min-width:200px; vertical-align:top;" />

- ๋ก๊ทธ์ธ ์ฑ๊ณต!.. response ๊ฐ์ console๋ก ์ฐ์ด๋ณด์๋ค.

<img src="../assets/images/post/img_20221108_04.png" alt="" style="width:95%; max-width:800px; min-width:300px; vertical-align:top;" />

- accessToken๊น์ง ์ ๋์ด์ค๋๊ฒ ํ์ธ. ๋ฐ๋ก 2์ฐจ๋ก ๋์ด๊ฐ๋ณด์.

<br/>

## ๐ง 2์ฐจ. TODO LIST

- ๐งฉ React nextjs typescript์ ์ ์ฉ.
- ๐งโโ๏ธ JWT ํ์ฉ Login ์ ์ฉ.
- ๐โโ๏ธ Login UI ์ ์ฉ.
- ๐ ์ํ๊ด๋ฆฌ๋ก ๋ก๊ทธ์ธ ์ํ ์ ์ง. (Recoil)
- ๐ฉ๐ปโ๐ซ Login ์ฒ๋ฆฌ์ ๋ํ ๋ฐ์ดํฐ ๋ก์ง ์ ๋ฆฌ.
- ๐จโ๐จ [2์ฐจ](https://fe-hyunsu.github.io/Firebase-login)๋ก ๋์ด๊ฐ๋ณด์

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://www.youtube.com/watch?v=bJ-33ANIScE&t=365s](https://www.youtube.com/watch?v=bJ-33ANIScE&t=365s){:target="\_blank"}
- [https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko](https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest/setRequestHeader](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest/setRequestHeader){:target="\_blank"}
- [https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0](https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0){:target="\_blank"}
- [https://hungseong.tistory.com/67](https://hungseong.tistory.com/67){:target="\_blank"}
- [https://joshua1988.github.io/web-development/javascript/promise-for-beginners](https://joshua1988.github.io/web-development/javascript/promise-for-beginners){:target="\_blank"}
- [https://velog.io/@vraimentres/async-%ED%95%A8%EC%88%98%EC%99%80-try-catch](https://velog.io/@vraimentres/async-%ED%95%A8%EC%88%98%EC%99%80-try-catch){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then){:target="\_blank"}
  <br/><br/>

---
