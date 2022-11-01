---
layout: post
title: '🅰️ font unicode-range'
date: 2022-11-01
tags: [frontend-study]
---

## 💬 unicode-rang

- 지정한 폰트가 한글은 괜찮은데, 영문 폰트가 마음에 안드는 경우, 유니코드 설정으로 폰트 스타일 적용범위를 지정할 수 있다.

```css
@font-face {
  font-family: 'font-name';
  src: url('font-name-file.woff2') format('woff2'), url('font-name-file.woff') format('woff');
  unicode-range: U+AC00- U+D7A3; /* 한글폰트에 적용. */
}
@font-face {
  font-family: 'font-name-number';
  src: url('font-name-number-file.woff2') format('woff2'), url('font-name-number-file.woff') format('woff');
  unicode-range: U+0030-0039; /* 숫자폰트에 적용. */
}
```

### 📚 Unicode 종류

- 모든 문자 : U+0020-007E
- 특수문자 : U+0020-002F, U+003A-0040, U+005B-0060, U+007B-007E
- 영문 : U+0041-005A(대문자), U+0061-007A(소문자)
- 숫자 : U+0030-0039
- 한글 : U+AC00-U+D7A3

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range)
- [https://d2.naver.com/helloworld/4969726](https://d2.naver.com/helloworld/4969726)
  <br/><br/>

---
