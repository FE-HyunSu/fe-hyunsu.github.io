---
layout: post
title: '๐ฆน๐ผโโ๏ธ Nextjs _app, _document'
date: 2022-11-25
tags: [frontend-study]
---

## ๐ง \_app.tsx์ \_document.tsx

<img src="../assets/images/post/img_20221125_01.png" alt="" style="width:100%; min-width:300px;" alt="" />
- Nextjs ํ๋ก์ ํธ ์งํ ์ \_app.tsx์ \_document.tsx์ ๋ํด ์์๋ณด์.

<br/>

### ๐ง๐ปโโ๏ธ \_app.tsx

- ์ปดํฌ๋ํธ ์์น : pages/\_app.tsx
- ์คํ ์์  : Nextjs๋ ๊ธฐ๋ณธ์ ์ผ๋ก SSR(Server Side Rendering)์ผ๋ก ๋์๋๊ณ , Server๋ก ์์ฒญ์ด ๋ค์ด์์๋ ์ต์ด๋ก ์คํ๋๋ ์ปดํฌ๋ํธ.
- ๋ชจ๋  ํ์ด์ง๋ ํด๋น ์ปดํฌ๋ํธ๋ฅผ ๊ฑฐ์น๊ฒ ๋๋ฉฐ, ๋ชจ๋  ๋ ์ด์์์ ๊ตฌ์ฑํ๋ค.
- Server๋ก ์์ฒญ์ด ๋ค์ด์์๋ ์ต์ด๋ก ์คํ๋๋ฏ๋ก, ์ต์ด ์ ๊ทผ ์ Client์์ ์๋ํ๋ ค๋ ์ ์ด๋ ์ ์ฉ๋์ง ์๋๋ค.

<br/>

### ๐งโโ๏ธ \_document.tsx

- ์ปดํฌ๋ํธ ์์น : pages/\_document.tsx
- nextjs์์ ์ ๊ณตํ๋ html ๋ฌธ์๋ฅผ ์ปค์คํฐ๋ง์ด์ง ํ  ์ ์์.
- ๊ณตํต์ ์ผ๋ก ์ฌ์ฉํ  head / mete / font / ์น ์ ๊ทผ์ฑ ์ค์  / body ๋ฑ์ ์ปค์คํฐ๋ง์ด์ง ํ  ๋ ํ์ฉ.
- Content๋ค์ ๋ธ๋ผ์ฐ์ ๊ฐ html๋ก ์ดํดํ๋๋ก ๊ตฌ์กฐํ ์ํด.
- \_app.tsx ์ปดํฌ๋ํธ ๋ค์์ผ๋ก ์คํ๋๋ค.

<br/>

### ๐ ์ ๋ฆฌ

- ๋ชจ๋  ํ์ด์ง๋ \_app.tsx -> \_document.tsx ์์๋ก ๋ ๋๋ง.
- \_app์ theme style๊ณผ, ์ํ๊ด๋ฆฌ๋ฅผ ์ํ ์ํ์ ์ ์ฉ. (๋ณธ์ธ ๊ธฐ์ค)
- \_document๋ HTML ๋งํฌ์ ๊ตฌ์กฐ๋ฅผ ์ํ. (๋ณธ์ธ ๊ธฐ์ค : ํด๋น ์ปดํฌ๋ํธ ๋ด render ํจ์๋ฅผ ํตํด, ์ฒซ ํ์ด์ง๊ฐ ๋ธ์ถ๋๋๋ฐ, ์ฌ๊ธฐ์ styled-components๋ฅผ ํจ๊ป ์ฌ์ฉํ๋ ๊ฒฝ์ฐ, render ํจ์๊ฐ ์คํ๋๊ธฐ ์  ํธ์ถํด์ผ ์ต์ด ํ์ด์ง ์ ๊ทผ ์ style์ด ์๋ ์ํ๋ก ์ ๊น ๋ธ์ถ๋๋ ํ์์ ๋ฐฉ์งํ  ์ ์๋ค.)

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://velog.io/@woodong/2.-app.tsx-%EC%99%80-document.tsx](https://velog.io/@woodong/2.-app.tsx-%EC%99%80-document.tsx){:target="\_blank"}
- [https://merrily-code.tistory.com/154](https://merrily-code.tistory.com/154){:target="\_blank"}
- [https://asperbrothers.com/blog/server-side-rendering-in-react](https://asperbrothers.com/blog/server-side-rendering-in-react){:target="\_blank"}
  <br/><br/>

---
