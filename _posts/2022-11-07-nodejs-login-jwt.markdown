---
layout: post
title: '🍹 Firebase Authentication (Login)'
date: 2022-11-15
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
- 🔊 상태관리로 로그인 상태 유지. (Recoil)
- 👩🏻‍🏫 Login 처리에 대한 데이터 로직 정리.

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

- 위 loginAuth 함수를 아래 컴포넌트에서 import, 폼에 입력된 이메일, 패스워드 정보를 인자값으로 로그인 시도.

```jsx
// email, password 입력값을 인자로 loginAuth 함수 실행.
const tryLogin = (email: HTMLSelectElement | null, password: HTMLInputElement | null) => {
  // validation check.
  loginAuth(email.value, password.value)
    .then((userCredential) => {
      // 로그인 성공 로직.
    })
    .catch((error) => {
      // 로그인 에러 로직.
    });
};
```

- loginAuth 함수를 통해 반환된 Promise 객체를 then, catch 메서드를 통해 성공 or 에러 케이스로 분기한다.

<br/>

### 👮‍♀️ 로그인 로직 Flow 체크. (작성중..)

(1) login 컴포넌트에서 폼에 입력된 이메일주소, 패스워드 정보를 인자값으로 tryLogin 함수 실행.

```jsx
// login component.
import { loginAuth } from '../../firebase/firestore';
...
// 인자로 담긴 이메일과 패스워드는 validation check 후 loginAuth 함수를 실행.
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

(2) loginAuth 함수는 async, await을 통해 firebase/auth 내장 함수인 signInWithEmailAndPassword 함수를 실행하고, Promise를 반환함.

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

(3) 다시 login component의 tryLogin 함수로 돌아와 반환된 Promise로 then, catch 메서드를 통해 성공 or 에러 케이스로 분기한다.

```jsx
// login component -> tryLogin 함수 중.
loginAuth(email.value, password.value)
  .then((userCredential) => {
    // login success.
  })
  .catch((error) => {
    // login error.
  });
```

(4) loginAuth에서 반환된 Promise로 then, catch 처리되는 로직에 대해 좀 더 알아보자.

```js
// Promise는 Pending(대기), Fulfilled(이행), Rejected(실패) 이렇게 3단계 상태로 나눌 수 있는데,
// Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태.
// Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태.
// Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태.
```

- loginAuth 함수의 Promise 처리 흐름.

<img src="../assets/images/post/img_20221116_01.png" alt="" style="width:95%; max-width:700px; min-width:300px; vertical-align:top;" />

<br/>

### 👨‍🚀 NEXT STEP.

- (response 값으로 받은 user data의 accesstoken, refreshtoken으로 로그인 유지 로직)

<br/>

---

<br/>

## 🎫 참고 페이지

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

```

```
