---
layout: post
title: '🍹 Firebase Authentication (Login)'
date: 2022-11-07
tags: [frontend-study]
---

## 🥮 Firebase Login 기능 구현

- Firebase Authentication 기능을 통해 로그인 기능 적용.
- 1차 : nodejs express 셋팅 후 html에서 구현.
- 2차 : react nextjs + typescript 프로젝트에 적용.
- 기존 Firebase 생성해놓은 프로젝트를 활용해서, 로그인 페이지 구현.

<br/>

## 🚵 1차.

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

- accessToken까지 잘 넘어오는것 확인. 바로 2차로 넘어가보자.

<br/>

## 🧗 2차.

### ⛹️ TODO LIST

- 🧩 React nextjs typescript에 적용.
- 🧘‍♂️ JWT 활용 Login 적용.
- 🏄‍♀️ Login UI 적용.
- 🔊 상태관리로 로그인 상태 유지.

<br/>

### 😈 Firebase.js 셋팅

- firestore의 데이터를 받아오기 위해 getData, setData 함수 선언 및 Auth 처리 함수 선언.

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

- export 한 loginAuth 함수를 사용하여, 폼에 입력된 정보를 통해 로그인 시도.

```jsx
// email, password 입력값을 인자로 loginAuth 함수 실행.
loginAuth(email.value, password.value)
  .then((userCredential) => {
    // 로그인 성공 로직.
  })
  .catch((error) => {
    // 로그인 에러 로직.
  });
```

- loginAuth 함수를 통해 반환된 Promise 객체를 then, catch 메서드를 통해 성공 or 에러 케이스로 분기한다.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://www.youtube.com/watch?v=bJ-33ANIScE&t=365s](https://www.youtube.com/watch?v=bJ-33ANIScE&t=365s){:target="\_blank"}
- [https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko](https://firebase.google.com/docs/auth/web/password-auth?authuser=0&hl=ko){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest/setRequestHeader](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest/setRequestHeader){:target="\_blank"}
- [https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0](https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0){:target="\_blank"}
- [https://hungseong.tistory.com/67](https://hungseong.tistory.com/67){:target="\_blank"}
  <br/><br/>

---
