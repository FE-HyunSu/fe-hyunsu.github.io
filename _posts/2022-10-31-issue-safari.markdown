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

<br/>

### 🔎 이슈 발생 사례

- addComa 라는 함수를 선언. 해당 함수의 기능으로는, 정규 표현식을 이용하여 매개변수로 숫자타입을 넣었을때, 3자리마다 ',' 표기를 찍어 return 해주는 함수를 선언하였다.

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

- safari 브라우저에서 적용되지 않았던 regex의 lookbehind 문법에 대해 알아보자.

```javascript
// Negative Lookahead
// X를 찾되 Y가 따라오지 않는 경우만 매치.
{X(?!Y)}

// X를 찾되 Y가 따라붙는 경우에만 X에 대해 매치.
{X(?=Y)}

```

- Y의 입장에서 X가 앞쪽에 놓여있기 때문에, Lookahead 라는 표현으로 사용.
- Lookahead가 조건 Y의 앞에 놓인 X를 바라보는 경우라면, 뒤를 바라보게 하는 것도 있는데 이를 Lookbehind 라고 함.

```javascript
// Positive Lookbehind
// Y의 뒤에 따라붙는 X를 찾되 Y조건을 만족하는 경우에만 매치.
{(?<=Y)X}

// Y의 뒤에 따라붙는 X를 찾되 Y조건을 만족하지 않는 경우에만 매치.
{(?<!Y)X}
```

- 결국 X의 위치에 따라 달라질뿐이므로, Lookahead 의 표현식을 Lookbehind로 변경이 가능하다.

<br/>

### 📌 기억해둘점

- javascript의 경우, 정규표현식의 lookbehind 문법을 브라우저에서 지원안하는 경우가 있다고 함.
- 정규표현식 적용 후엔 크로스브라우징 체크를 반드시 해볼것.

<br/>

## 🎫 참고 페이지

- [https://github.com/typesense/typesense-instantsearch-adapter/issues/29](https://github.com/typesense/typesense-instantsearch-adapter/issues/29){:target="\_blank"}
- [https://mc500.tistory.com/658](https://mc500.tistory.com/658){:target="\_blank"}
- [https://javascript.info/regexp-lookahead-lookbehind](https://javascript.info/regexp-lookahead-lookbehind){:target="\_blank"}
  <br/><br/>

---
