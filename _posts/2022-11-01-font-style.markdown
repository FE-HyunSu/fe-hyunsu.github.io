---
layout: post
title: 'đ°ď¸ font unicode-range'
date: 2022-11-01
tags: [frontend-study]
---

## đŹ unicode-rang

- ě§ě í í°í¸ę° íę¸ě ę´ě°Žěë°, ěëŹ¸ í°í¸ę° ë§ěě ěëë ę˛˝ě°, ě ëě˝ë ě¤ě ěźëĄ í°í¸ ě¤íěź ě ěŠë˛ěëĽź ě§ě í  ě ěë¤.

```css
@font-face {
  font-family: 'font-name';
  src: url('font-name-file.woff2') format('woff2'), url('font-name-file.woff') format('woff');
  unicode-range: U+AC00-U+D7A3; /* íę¸í°í¸ě ě ěŠ. */
}
@font-face {
  font-family: 'font-name-number';
  src: url('font-name-number-file.woff2') format('woff2'), url('font-name-number-file.woff') format('woff');
  unicode-range: U+0030-0039; /* ěŤěí°í¸ě ě ěŠ. */
}
```

### đ Unicode ě˘ëĽ

- ëŞ¨ë  ëŹ¸ě : U+0020-007E
- íšěëŹ¸ě : U+0020-002F, U+003A-0040, U+005B-0060, U+007B-007E
- ěëŹ¸ : U+0041-005A(ëëŹ¸ě), U+0061-007A(ěëŹ¸ě)
- ěŤě : U+0030-0039
- íę¸ : U+AC00-U+D7A3

<br/>

---

<br/>

## đŤ ě°¸ęł  íě´ě§

- [https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range){:target="\_blank"}
- [https://d2.naver.com/helloworld/4969726](https://d2.naver.com/helloworld/4969726){:target="\_blank"}
  <br/><br/>

---
