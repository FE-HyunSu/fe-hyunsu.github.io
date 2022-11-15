---
layout: post
title: '👨‍🎤 Fireabse Database Test Mode'
date: 2022-11-15
tags: [issue]
---

## 🧤 Firebase Database 유의할점.

- 초기 Firebase Database 설정 중 Mode 선택에서 Test Mode로 선택했었음.
- 꽤 시간이 지나고 해당 메일을 수신함..<br/><br/><img src="../assets/images/post/img_20221115_01.png" alt="" style="width:90%; max-width:500px; min-width:300px;" />
- 내가 사용하고 있는 Firebase database는 Test Mode이고 곧 만료된다는 이야기.
- Test Mode 만료 시 Firestore 데이터베이스에 대한 모든 클라이언트 요청이 거부된다고 한다. 🙊
- 내가 사용하고 있는 database Test Mode 설정.<br/><br/><img src="../assets/images/post/img_20221115_02.png" alt="" style="width:90%; max-width:700px; min-width:300px;" />
- 규칙 수정 버튼을 눌러, 위 조건문을 아래와 같이 수정하면 Test Mode에서 Production mode로 전환이 가능함.

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

- 하마터면 4일뒤 모든 요청이 거부되어 영문도 모르고 문제 생길뻔 했다.
- 해결됨.

<img src="../assets/images/post/img_20221115_03.png" alt="" style="width:90%; max-width:400px; min-width:300px;" />

<br/>

## 🎫 참고 페이지

- [https://ardmos.tistory.com/entry/Firebase-Cloud-Firestore-Test-Mode-Production-Mode-%EB%B3%80%EA%B2%BD](https://ardmos.tistory.com/entry/Firebase-Cloud-Firestore-Test-Mode-Production-Mode-%EB%B3%80%EA%B2%BD){:target="\_blank"}
  <br/><br/>

---
