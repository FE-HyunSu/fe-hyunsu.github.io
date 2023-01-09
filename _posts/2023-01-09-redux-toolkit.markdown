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

<img src="../assets/images/post/img_20230109_01.gif" alt="" style="width:90%; max-width:500px; margin: auto 1rem; vertical-align:top;" />

<br/>

## 🏺 Redux-toolkit 설치.

```sh
$ npm install @reduxjs/toolkit react-redux
```

<br/>

## 🪓 용어설명.

- Store : 스토어는 컴포넌트의 상태를 관리하는 저장소다. 하나의 프로젝트는 하나의 스토어만 가질 수 있다.
- Action : 스토어의 상태를 변경하기 위해서는, 액션을 생성해야한다. 액션은 객체이며, 반드시 type을 가져야 한다. 액션 객체는 액션생성함수에 의해서 만들어진다.
- Reducer : 리듀서는 현재 상태와 액션 객체를 받아 새로운 상태를 리턴하는 함수다.
- Dispatch : 디스패치는 스토어의 내장 함수 중 하나이며, 액션 객체를 넘겨줘 상태를 업데이트 시켜주는 역할을 한다.
- Subscribe : 스토어의 내장 함수 중 하나로, 리듀서가 호출될 때 서브스크라이브된 함수 및 객체를 호출한다.
- createSlice : action과 reducer를 간단하게 생성할 수 있는 API.
- configureStore : store의 구성설정. Reducer에서 반환된 새로운 state를 Store라는 객체로 정리해 관리하는곳.
- persistReducer : redux-persist와 리덕스 모듈 정보를 종합하여 persist 정보를 반환.
- combineReducers : combineReducers 헬퍼 함수는 서로 다른 리듀싱 함수들을 값으로 가지는 객체를 받아서 createStore에 넘길 수 있는 하나의 리듀싱 함수로 바꿔줌.

<br/>

## 🔬 진행과정.

<img src="../assets/images/post/img_20230109_02.gif" alt="" style="width:90%; max-width:600px; margin: auto 1rem; vertical-align:top;" />

- UI가 처음 렌더링될 때, UI 컴포넌트는 리덕스 스토어의 상태에 접근하여 해당 상태를 렌더링한다.
- 이후 UI에서 상태가 변경되면, 앱은 디스패치를 실행해 액션을 일으킨다.
- 새로운 액션을 받은 스토어는 리듀서를 실행하고 리듀서를 통해 나온 값을 새로운 상태로 저장한다.
- 서브스크라이브된 UI은 상태 업데이트로 변경된 데이터를 새롭게 렌더링한다.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://velog.io/@sweet_pumpkin/%EB%AC%B4%EC%9E%91%EC%A0%95%EB%94%B0%EB%9D%BC%ED%95%98%EA%B8%B0-%EC%B5%9C%EA%B3%A0-%EB%A6%AC%EB%8D%95%EC%8A%A4%EC%95%BC-%EA%B3%A0%EB%A7%99%EB%8B%A4-Redux-Redux-Toolkit-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0](https://velog.io/@sweet_pumpkin/%EB%AC%B4%EC%9E%91%EC%A0%95%EB%94%B0%EB%9D%BC%ED%95%98%EA%B8%B0-%EC%B5%9C%EA%B3%A0-%EB%A6%AC%EB%8D%95%EC%8A%A4%EC%95%BC-%EA%B3%A0%EB%A7%99%EB%8B%A4-Redux-Redux-Toolkit-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0){:target="\_blank"}
  <br/><br/>

---
