---
layout: post
title: "🔮 Redux-toolkit"
date: 2023-01-09
tags: [frontend-study]
---

## ⚱️ Redux-toolkit.

- 리덕스를 라이브러리 없이 사용 시 액션타입 정의 -> 액션함수 생성 -> 리듀서 정의 의 작업이 필요함.
- 많아지는 액션을 관리하기 위해 redux-actions 설치.
- 불변성 보존을 위한 immer 설치.
- store값을 효율적으로 핸들링하여 불필요한 리렌더링을 막기 위해 reselect.
- 비동기 작업을 위한 thunk 와 saga 등 리덕스의 유효한 기능을 사용하기 위해 라이브러리를 사용해야 함.
- Redux-Toolkit은 saga를 제외한 위 모든 기능을 내장된 기능으로 제공한다.

<br/>

## 🏺 Redux-toolkit 설치.

```sh
$ npm install @reduxjs/toolkit react-redux.
```

<br/>

## 🪓 용어설명.

- createSlice : action과 reducer를 간단하게 생성할 수 있는 API.
- configureStore : store의 구성설정. Reducer에서 반환된 새로운 state를 Store라는 객체로 정리해 관리하는곳.
- persistReducer : redux-persist와 리덕스 모듈 정보를 종합하여 persist 정보를 반환.
- combineReducers : combineReducers 헬퍼 함수는 서로 다른 리듀싱 함수들을 값으로 가지는 객체를 받아서 createStore에 넘길 수 있는 하나의 리듀싱 함수로 바꿔줌.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://im-designloper.tistory.com/98](https://im-designloper.tistory.com/98){:target="\_blank"}
  <br/><br/>

---
