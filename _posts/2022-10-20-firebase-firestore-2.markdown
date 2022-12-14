---
layout: post
title: ' β€οΈβπ₯ Firebase firestore - 2'
date: 2022-10-21
tags: [backend-study]
---

## π Firebase firestore νμ©

<br/>

### π firestore μν.

- μ»¬λ μμ νμν data μλ ₯.<br/><img src="../assets/images/img_firestore.png" alt="" style="width:90%; max-width:700px; min-width:300px;" />

- npm μ€μΉ

```java
 > npm install firebase
```

- firebaseConfig.js νμΌ μΆκ°.
- firestore λ°μ΄ν°λ² μ΄μ€λ₯Ό μ¬μ©ν  κ²μ΄κΈ° λλ¬Έμ firestore ν¨μλ κ°μ Έμ€λλ‘ νμ. (getFirestore)

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

### π₯ μ»΄ν¬λνΈμ data νΈμΆ.

- ν΄λΉ μ»΄ν¬λνΈμμλ data νΈμΆλ§ μ μ©ν  κ²μ΄κΈ° λλ¬Έμ app, addDoc ν¨μλ μ¬μ©λμ§ μλλ€.
- getMemberList ν¨μλ₯Ό ν΅ν΄, firestoreμ λ±λ‘ν data νΈμΆμ μ±κ³΅.

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

### π­ Next step

- firebaseConfig.js μ key κ° dotenv μ μ©.
- firebase νΈμ€ν μ€μ .
- memberList μΈ accountListλ firestore μ°λ μ²λ¦¬.
- firestore νΈμΆ ν¨μ λ‘μ§ κ°μ .

<br/>

## π« μ°Έκ³  νμ΄μ§

- [https://firebase.google.com](https://firebase.google.com){:target="\_blank"}
- [https://www.npmjs.com/package/@firebase/firestore](https://www.npmjs.com/package/@firebase/firestore){:target="\_blank"}
- [https://www.freecodecamp.org/news/nextjs-firebase-tutorial-build-an-evernote-clone](https://www.freecodecamp.org/news/nextjs-firebase-tutorial-build-an-evernote-clone/){:target="\_blank"}
- [https://velog.io/@hoho_0815/env-%ED%8C%8C%EC%9D%BC%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC](https://velog.io/@hoho_0815/env-%ED%8C%8C%EC%9D%BC%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC){:target="\_blank"}
  <br/><br/>

---
