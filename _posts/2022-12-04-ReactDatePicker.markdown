---
layout: post
title: "⛄️ React Datepicker"
date: 2022-12-04
tags: [frontend-study]
---

## 🌗 React Datepicker

- React Datepicker 패키지를 빠르게 적용해보자.

#### 👒 npm 설치

```tsx
$ npm install react-datepicker --save
$ npm i --save-dev @types/react-datepicker
$ npm install date-fns --save
```

#### 🪷 import

- DatePicker 와 관련 style을 import 하고, 지정값을 저장할 상태값도 선언해주자.

```tsx
import DatePicker from "react-datepicker";
import "react-datepicker/dist/react-datepicker.css";
import { ko } from "date-fns/esm/locale";
...
const [selectDate, setSelectDate] = useState(new Date());
```

#### 💐 DatePicker 사용

- DatePicker 의 props값으로 selected와 onChange를 매개변수로 넣어주자.
- onChange : DatePicker를 통해 선택된 날짜를 date로 받는다. return 받은 값을 setSelectDate으로 업데이트.
- selected : 지정된 일자를 date로 받는다. 기본값은 오늘.

```tsx
import DatePicker from "react-datepicker";
import "react-datepicker/dist/react-datepicker.css";
...
const [selectDate, setSelectDate] = useState(new Date());
...
<DatePicker
  selected={selectDate}
  onChange={(date: Date) => setSelectDate(date)}
/>
```

<br/>

### 💫 Result

- AccountAdmin 프로젝트에 적용해봄. [이동](https://reliable-florentine-21f16f.netlify.app){:target="\_blank"}

<img src="../assets/images/post/img_20221204_01.png" alt="" style="width:90%; max-width:200px; margin: auto 1rem; vertical-align:top;" />

- Good.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://www.npmjs.com/package/react-datepicker](https://www.npmjs.com/package/react-datepicker){:target="\_blank"}
- [https://reactdatepicker.com/](https://reactdatepicker.com/){:target="\_blank"}
  <br/><br/>

---
