---
layout: post
title: '👨🏿‍🚒 Firebase Login (2차)'
date: 2022-11-16
tags: [frontend-study]
---

## 🤐 기능 구현 개요

- React Nextjs + Typescript 프로젝트에 Firebase Authentication 기능을 통해 로그인 기능 적용.

<br/>

### ⛹️ TODO LIST

- 🧩 React nextjs typescript에 적용.
- 🏄‍♀️ Login UI 적용.
- 🧘‍♂️ JWT 활용 Login 적용.
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

---

<br/>

## 👮‍♀️ 로그인 로직 Flow 체크.

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

<br/>

(2) loginAuth 함수는 async, await을 통해 signInWithEmailAndPassword 함수를 실행하고, Promise를 반환함.

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

(3) 다시 login component의 tryLogin 함수로 돌아와 반환된 Promise로 성공 or 에러 케이스로 분기.

- loginAuth에서 return된 Promise를 then-catch 와 try-catch 메서드로 처리해보고 비교해보자.
- Promise 상태의 흐름을 이해하며 체크해볼것.

```js
// [Promise 상태 3단계]
// Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태.
// Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태.
// Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태.
```

<br/>

---

<br/>

## 🧵 then-catch 메서드로 처리한 경우.

```jsx
loginAuth(email.value, password.value)
  .then((userInfo) => {
    // login success.
  })
  .catch((error) => {
    // login error.
  });
```

- Promise 흐름(then-catch)

<img src="../assets/images/post/img_20221120_01.png" alt="" style="width:95%; max-width:700px; min-width:300px; vertical-align:top;" />

출처 : [MDN:Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="\_blank"}

<img src="../assets/images/post/img_20221116_01.png" alt="" style="width:95%; max-width:700px; min-width:300px; vertical-align:top;" />

- MDN에 설명된 알고리즘으로 로직을 그려봤을때 개인적으로 혼선이 있어 then-catch 로직에 대해 내방식대로 재정리 해보았음.

<img src="../assets/images/post/img_20221119_01.png" alt="" style="width:95%; max-width:800px; min-width:300px; vertical-align:top;" />

<br/>

---

<br/>

## 🌼 try-catch 메서드로 처리한 경우.

```jsx
try {
  const returnUserInfo = await loginAuth(email.value, password.value);
  const userInfo = returnUserInfo.user;
  // login success.
  ...
} catch (error) {
  // login error.
  ...
}
```

<br/>

### 👨‍🚀 NEXT STEP.

- (response 값으로 받은 user data의 accesstoken, refreshtoken으로 로그인 유지 로직)

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0](https://velog.io/@byron1st/Next.js-%EC%97%90-Firebase-Auth-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0){:target="\_blank"}
- [https://hungseong.tistory.com/67](https://hungseong.tistory.com/67){:target="\_blank"}
- [https://joshua1988.github.io/web-development/javascript/promise-for-beginners](https://joshua1988.github.io/web-development/javascript/promise-for-beginners){:target="\_blank"}
- [https://velog.io/@vraimentres/async-%ED%95%A8%EC%88%98%EC%99%80-try-catch](https://velog.io/@vraimentres/async-%ED%95%A8%EC%88%98%EC%99%80-try-catch){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then){:target="\_blank"}
- [https://eundol1113.tistory.com/m/226](https://eundol1113.tistory.com/m/226){:target="\_blank"}
- [https://velog.io/@design0728/clean-code-typescript-%EC%97%90%EB%9F%AC%EC%B2%98%EB%A6%ACError-Handling](https://velog.io/@design0728/clean-code-typescript-%EC%97%90%EB%9F%AC%EC%B2%98%EB%A6%ACError-Handling){:target="\_blank"}
- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="\_blank"}
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw){:target="\_blank"}
  <br/><br/>

---
