---
layout: post
title: '🍹 Firebase Authentication (Login)'
date: 2022-11-07
tags: [frontend-study]
---

## 🥮 Login 기능 구현 (feat. Firebase)

- Firebase Authentication 기능을 통해 로그인 기능 적용.
- 서버는 nodejs express 셋팅.
- 기존 Firebase 생성해놓은 프로젝트를 활용해서, 로그인 페이지 구현.

### 🛹 Firebase set.

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

- Firebase Authentication 에서 계정 추가.

<img src="../assets/images/post/img_20221108_01.png" alt="" style="width:90%; max-width:700px; min-width:300px; vertical-align:top;" />

- Firebase 프로젝트 설정에서, CDN 타입으로 적용.

<img src="../assets/images/post/img_20221108_02.png" alt="" style="width:90%; max-width:600px; min-width:300px; vertical-align:top;" />

- Firebase에서 '이메일 주소와 비밀번호로 사용자 로그인' 글 참조하여 셋팅.
- 기존 'firebase/auth' -> https://www.gstatic.com/firebasejs/9.13.0/firebase-auth.js 로 변경한다.
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

- 위 내용을 기반으로, 스크립트 수정.
- 기능 확인을 위해 UI 없이 적용해봄.

<img src="../assets/images/post/img_20221108_03.png" alt="" style="width:90%; max-width:300px; min-width:200px; vertical-align:top;" />

- 로그인 성공!.. response 값을 console로 찍어보았다.

<img src="../assets/images/post/img_20221108_04.png" alt="" style="width:95%; max-width:800px; min-width:300px; vertical-align:top;" />

<br/>

## ⛹️ TODO LIST

- 🧘‍♂️ 로그인 상태 유지.
- 🏄‍♀️ 로그인 UI 적용.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://www.youtube.com/watch?v=bJ-33ANIScE&t=365s](https://www.youtube.com/watch?v=bJ-33ANIScE&t=365s){:target="\_blank"}
- [https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko](https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest/setRequestHeader](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest/setRequestHeader){:target="\_blank"}
  <br/><br/>

---
