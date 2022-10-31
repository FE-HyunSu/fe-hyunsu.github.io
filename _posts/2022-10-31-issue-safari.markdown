---
layout: post
title: ' 🧨 Safari lookbehind 문법 이슈'
date: 2022-10-31
tags: [issue]
---

## 📚 Safari 브라우저 lookbehind 문법 지원 이슈

### 📰 개요

- 개발 및 배포 시 크롬 브라우저에서는 잘 나왔는데, safari 브라우저에서 페이지가 제대로 나오지 않았다.
- 브라우저 콘솔에는 단순히 SyntaxError: Invalid regular expression: invalid group specifier name 라는 메세지만 발생되었음.
- 검색 결과, 원인은 정규표현식이 safari 브라우저에서 제대로 인식되지 못했고, 좀 더 자세히 찾아보니 safari에서는 regex의 lookbehind 문법을 지원하지 않는다고 한다.

### 🔎 이슈 발생 사례

- addComa 라는 함수를 선언. 매개변수로 숫자타입을 넣었을때, 3자리마다 ',' 표기를 찍어 return 해주는 함수를 선언하였다.

```javascript
// 수정 전
const addComa = (number) => {
  return number.toString().replace(/\B(?<!\.\d*)(?=(\d{3})+(?!\d))/g, ',');
};
```

- 위 방식으로 사용 시 safari 브라우저에서 이슈가 발생되었고, 아래 방식으로 변경하여 이슈를 해결하였다.

```javascript
// 수정 후
const addComa = (number) => {
  const numberComa = number.toString().split('.');
  numberComa[0] = numberComa[0].replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  return numberComa.join('.');
};
```

### 📌 기억해둘점

- 정규표현식을 사용할때 regex의 lookbehind 문법을 지원하지 않는다.
- 정규표현식 적용 후엔 크로스브라우징 체크를 반드시 해볼것.

<br/>

## 🎫 참고 페이지

- [https://github.com/typesense/typesense-instantsearch-adapter/issues/29](https://github.com/typesense/typesense-instantsearch-adapter/issues/29){:target="\_blank"}
- [https://mc500.tistory.com/658](https://mc500.tistory.com/658){:target="\_blank"}
  <br/>

---
