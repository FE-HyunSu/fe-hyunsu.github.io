---
layout: post
title: ' 💵 AccountBook'
date: 2022-10-18
tags: [frontend-study, backend-study]
---

## 🛼 React study 모임 정산 페이지

<br/>

### 🌎 URL

- 페이지 URL : [https://illustrious-arithmetic-f0422e.netlify.app](https://illustrious-arithmetic-f0422e.netlify.app){:target="\_blank"}
- Github 저장소 : [https://github.com/FE-HyunSu/groupAccountBook](https://github.com/FE-HyunSu/groupAccountBook){:target="\_blank"}

### 🥲 작업 내용

- React 스터디 모임에서 총무에 당첨되었고, 회비 정산내역 기록용으로 React 프로젝트를 생성했다.
- React nextJs 환경으로 페이지를 만들었고, 데이터는 json 파일로 대체했다.
  - memberList.json : 멤버 정보. { id : 고유값, userName : 이름, imgUrl : 프로필 이미지 }
  - accountList.json : 입출금 내역. { targetId : 멤버id, dateTime : 날짜, description : 내용, calculation : 금액 }
- UI는 카카오뱅크 모임통장을 참고했다.
- 업데이트 할게 많긴 하지만 일단, 여기까지.. 추후에 디벨롭하기로 하자.

### 🚏 next step

- (해결됨) <span class="text-middle-line">(이슈) IOS safari 브라우저에서 style 적용이 되지 않고 있다. 이슈 해결 필요.</span>
- (해결됨) <span class="text-middle-line">(개선) AccountList를 선언순서와 관계없이 sort 되도록 기준 정리 및 적용 필요.</span>
- (개선) 특정 user를 선택했을때, 해당 user의 입출금 내역만 보여지도록 개선 필요.
  <br/><br/>

---
