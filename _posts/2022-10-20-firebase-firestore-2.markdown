---
layout: post
title: ' ❤️‍🔥 Firebase firestore - 2'
date: 2022-10-21
tags: [backend-study]
---

## 🎇 Firebase firestore 활용

<br/>

### 🚒 firestore 셋팅.

- 컬렉션에 필요한 data 입력.<br/><img src="../assets/images/img_firestore.png" alt="" style="width:90%; max-width:700px; min-width:300px;" />

- npm 설치

```java
 > npm install firebase
```

- firebaseConfig.js 파일 추가.
- firestore 데이터베이스를 사용할 것이기 때문에 firestore 함수도 가져오도록 하자. (getFirestore)

```javascript
// Import the functions you need from the SDKs you need
import { initializeApp } from 'firebase/app';
import { getFirestore } from 'firebase/firestore';
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: { KEY_apiKey },
  authDomain: { KEY_authDomain },
  projectId: { KEY_projectId },
  storageBucket: { KEY_storageBucket },
  messagingSenderId: { KEY_messagingSenderId },
  appId: { KEY_appId },
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const database = getFirestore(app);
```

### 📥 컴포넌트에 data 호출.

- 해당 컴포넌트에서는 data 호출만 적용할 것이기 때문에 app, addDoc 함수는 사용되지 않는다.
- getMemberList 함수를 통해, firestore에 등록한 data 호출에 성공.

```jsx
...
import { app, database } from '../firebaseConfig';
import { collection, addDoc, getDocs } from 'firebase/firestore';
...
const dbInstance = collection(database, 'userList'); // firestore 'userList'
const getMemberList = () => {
    getDocs(dbInstance).then((data) => {
      const list = data.docs.map((item) => {
        return { ...item.data(), id: item.id };
      });
      setmemberList(list);
    });
  };

```

<br/>

## 🎫 참고 페이지

- [https://firebase.google.com](https://firebase.google.com){:target="\_blank"}
- [https://www.npmjs.com/package/@firebase/firestore](https://www.npmjs.com/package/@firebase/firestore){:target="\_blank"}
- [https://www.freecodecamp.org/news/nextjs-firebase-tutorial-build-an-evernote-clone](https://www.freecodecamp.org/news/nextjs-firebase-tutorial-build-an-evernote-clone/){:target="\_blank"}
  <br/>

---
