---
layout: post
title: '๐จโ๐ค Fireabse Database Test Mode'
date: 2022-11-15
tags: [issue]
---

## ๐งค Firebase Database ์ ์ํ ์ .

- ์ด๊ธฐ Firebase Database ์ค์  ์ค Mode ์ ํ์์ Test Mode๋ก ์ ํํ์์.
- ๊ฝค ์๊ฐ์ด ์ง๋๊ณ  ํด๋น ๋ฉ์ผ์ ์์ ํจ..<br/><br/><img src="../assets/images/post/img_20221115_01.png" alt="" style="width:90%; max-width:500px; min-width:300px;" />
- ๋ด๊ฐ ์ฌ์ฉํ๊ณ  ์๋ Firebase database๋ Test Mode์ด๊ณ  ๊ณง ๋ง๋ฃ๋๋ค๋ ์ด์ผ๊ธฐ.
- Test Mode ๋ง๋ฃ ์ Firestore ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ๋ํ ๋ชจ๋  ํด๋ผ์ด์ธํธ ์์ฒญ์ด ๊ฑฐ๋ถ๋๋ค๊ณ  ํ๋ค. ๐
- ๋ด๊ฐ ์ฌ์ฉํ๊ณ  ์๋ database Test Mode ์ค์ .<br/><br/><img src="../assets/images/post/img_20221115_02.png" alt="" style="width:90%; max-width:700px; min-width:300px;" />
- ๊ท์น ์์  ๋ฒํผ์ ๋๋ฌ, ์ ์กฐ๊ฑด๋ฌธ์ ์๋์ ๊ฐ์ด ์์ ํ๋ฉด Test Mode์์ Production mode๋ก ์ ํ์ด ๊ฐ๋ฅํจ.

```jsx
// Production Mode
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

- ํด๊ฒฐ๋จ. ๐

<img src="../assets/images/post/img_20221115_03.png" alt="" style="width:90%; max-width:400px; min-width:300px;" />

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://ardmos.tistory.com/entry/Firebase-Cloud-Firestore-Test-Mode-Production-Mode-%EB%B3%80%EA%B2%BD](https://ardmos.tistory.com/entry/Firebase-Cloud-Firestore-Test-Mode-Production-Mode-%EB%B3%80%EA%B2%BD){:target="\_blank"}
  <br/><br/>

---
