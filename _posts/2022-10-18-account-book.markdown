---
layout: post
title: " ๐ต AccountBook"
date: 2022-11-04
tags: [retrospect]
---

## ๐ผ React study ๋ชจ์ ์ ์ฐ ํ์ด์ง

### ๐ URL

- ํ์ด์ง URL : [https://illustrious-arithmetic-f0422e.netlify.app](https://illustrious-arithmetic-f0422e.netlify.app){:target="\_blank"}
- Github ์ ์ฅ์ : [https://github.com/FE-HyunSu/groupAccountBook](https://github.com/FE-HyunSu/groupAccountBook){:target="\_blank"}

<br/>

### ๐ฅฒ ๊ฐ์

- React ์คํฐ๋ ๋ชจ์์์ ์ด๋ฌด์ ๋น์ฒจ๋จ.
- ๊ฐ์ธ ์คํฐ๋๊ฒธ ํ๋น ์ ์ฐ๋ด์ญ ๊ธฐ๋ก์ฉ์ผ๋ก React ํ๋ก์ ํธ๋ฅผ ์์ฑ.

<br/>

### ๐ ์ด๊ธฐ๋ชจ๋ธ ๋ฐฐํฌ(v1.0)

- React nextJs ํ๊ฒฝ์ผ๋ก ํ์ด์ง ์์ฑ.
- UI๋ ์นด์นด์ค๋ฑํฌ๋ฅผ ์ฐธ๊ณ .
- ์ ์  ์ ๋ณด์ ์์ถ๊ธ ๋ฐ์ดํฐ๋ json ํ์ผ๋ก ๋์ฒดํ๋ค.
  - memberList.json : ๋ฉค๋ฒ ์ ๋ณด. { id : ๊ณ ์ ๊ฐ, userName : ์ด๋ฆ, imgUrl : ํ๋กํ ์ด๋ฏธ์ง }
  - accountList.json : ์์ถ๊ธ ๋ด์ญ. { targetId : ๋ฉค๋ฒid, dateTime : ๋ ์ง, description : ๋ด์ฉ, calculation : ๊ธ์ก }
- netlify๋ฅผ ํตํด ๋ฐฐํฌ.
- ์ถ๊ฐ ๊ฐ์ ๋ด์ฉ TodoList๋ฅผ ์์ฑ.

<br/>

### ๐ TODOLIST.

- (์๋ฃ) (๊ฐ์ ) AccountList๋ฅผ ์ ์ธ์์์ ๊ด๊ณ์์ด sort ๋๋๋ก ๊ธฐ์ค ์ ๋ฆฌ ๋ฐ ์ ์ฉ ํ์.
- (์๋ฃ) (๊ฐ์ ) ํน์  user๋ฅผ ์ ํํ์๋, ํด๋น user์ ์์ถ๊ธ ๋ด์ญ๋ง ๋ณด์ฌ์ง๋๋ก ๊ฐ์  ํ์.
- (์๋ฃ) (๊ฐ์ ) ๋ฐ์ดํฐ๋ฅผ json์ด ์๋, db ๋ฐ์ดํฐ ์ฐ๋ ์ ์ฉ.
- (์๋ฃ) (๊ฐ์ ) ๊ธฐํ UI ๊ฐ์ .

<br/>

### ๐ ๊ฐ์  ๋ด์ฉ ๋ฐ์(v2.0)

- sortํจ์๋ฅผ ํตํด AccountList item์ dateTime์ ๋น๊ตํ์ฌ, ๋ด๋ฆผ์ฐจ์์ผ๋ก ๋ชฉ๋ก ์ ๋ ฌ.
- firebase ์ firestore๋ฅผ ํตํด json ๋ฐ์ดํฐ๋ฅผ db์ ์ ์ฅ์์ผ ๋ฐ์ดํฐ๋ฅผ ํธ์ถ.
- ์ ์ฒด accountList๋ฅผ ์ ์ฅํ๋ ์ํ๊ฐ๊ณผ target์ accountList๋ฅผ ์ ์ฅํ๋ ์ํ๊ฐ์ ๋๋  ์ ์  ์ด๋ฏธ์ง ์ ํ ์ ํด๋น ๋ชฉ๋ก์ ํธ์ถ.
- UI ๊ฐ์  ์ ์ฉ.
  <br/><br/>

---
