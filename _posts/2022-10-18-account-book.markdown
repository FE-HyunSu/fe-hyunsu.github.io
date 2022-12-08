---
layout: post
title: " 💵 AccountBook"
date: 2022-11-04
tags: [retrospect]
---

## 🛼 React study 모임 정산 페이지

### 🌎 URL

- 페이지 URL : [https://illustrious-arithmetic-f0422e.netlify.app](https://illustrious-arithmetic-f0422e.netlify.app){:target="\_blank"}
- Github 저장소 : [https://github.com/FE-HyunSu/groupAccountBook](https://github.com/FE-HyunSu/groupAccountBook){:target="\_blank"}

<br/>

### 🥲 개요

- React 스터디 모임에서 총무에 당첨됨.
- 개인 스터디겸 회비 정산내역 기록용으로 React 프로젝트를 생성.

<br/>

### 🚍 초기모델 배포(v1.0)

- React nextJs 환경으로 페이지 생성.
- UI는 카카오뱅크를 참고.
- 유저 정보와 입출금 데이터는 json 파일로 대체했다.
  - memberList.json : 멤버 정보. { id : 고유값, userName : 이름, imgUrl : 프로필 이미지 }
  - accountList.json : 입출금 내역. { targetId : 멤버id, dateTime : 날짜, description : 내용, calculation : 금액 }
- netlify를 통해 배포.
- 추가 개선내용 TodoList를 작성.

<br/>

### 🚏 TODOLIST.

- (완료) (개선) AccountList를 선언순서와 관계없이 sort 되도록 기준 정리 및 적용 필요.
- (완료) (개선) 특정 user를 선택했을때, 해당 user의 입출금 내역만 보여지도록 개선 필요.
- (완료) (개선) 데이터를 json이 아닌, db 데이터 연동 적용.
- (완료) (개선) 기타 UI 개선.

<br/>

### 🚌 개선 내용 반영(v2.0)

- sort함수를 통해 AccountList item의 dateTime을 비교하여, 내림차순으로 목록 정렬.
- firebase 의 firestore를 통해 json 데이터를 db에 저장시켜 데이터를 호출.
- 전체 accountList를 저장하는 상태값과 target의 accountList를 저장하는 상태값을 나눠 유저 이미지 선택 시 해당 목록을 호출.
- UI 개선 적용.
  <br/><br/>

---
