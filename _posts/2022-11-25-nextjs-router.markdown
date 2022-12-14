---
layout: post
title: '๐ NextJS Router'
date: 2022-11-25
tags: [frontend-study]
---

## โท Nextjs Router

- Nextjs์์ Router ๋ฉ์๋์ ๋ํด ์์๋ณด์.

<br/>

### โ๐ป useRouter import.

- Nextjs ์์ ํจ์ํ์์ผ๋ก ์ฌ์ฉํ  ์ ์๋ ๋ด์ฅ ๋ผ์ด๋ธ๋ฌ๋ฆฌ useRouter๋ฅผ import ํจ.

```jsx
import { useRouter } from 'next/router'
...
```

<br/>

### โ๐ป useRouter method ์ข๋ฅ.

### ๐ถ router.push

```jsx
router.push(url, as, options);
```

- url: [ํ์] ๋ผ์ฐํ ํ๋ ค๋ url.
- as: [์ ํ] ๋ธ๋ผ์ฐ์  url ๋ฐ์ ๋ณด์ฌ์ง๋ path.
- options: [์ ํ] scroll(๋ผ์ฐํ ํ ์คํฌ๋กค์), shallow, locale ๋ฑ.

```jsx
// ex) /history ๋ก ์ด๋.
router.push('/history');
// ex) /history?pageIndex=3๋ก ์ด๋๋์ง๋ง, URLํ๊ธฐ๋ /history๋ก ์ ์ฉ.
router.push('/history?pageIndex=3', '/history');
```

### ๐ง router.replace

```jsx
router.replace(url, as, options);
```

- router.push ์ ์ฌ์ฉ๋ฐฉ์ ๋์ผ.
- ์ฐจ์ด์ ์ router history stack์ ์์ง ์๊ณ , ํ์ด์ง ์ด๋.
- ex) ์๋น์ค ํ์ด์ง -> ๋ก๊ทธ์ธ -> ๋ก๊ทธ์ธ ์ฑ๊ณต ํ ๋ค๋ก๊ฐ๊ธฐ(router.back()) ์ฒ๋ฆฌ ํ์๋ ์๋น์คํ์ด์ง๋ก ์ด๋.

### ๐ง router.prefetch

- ๋น ๋ฅธ ํด๋ผ์ด์ธํธ ์ ํ์ ์ํด ํ์ด์ง๋ฅผ ๋ฐ์ดํฐ๋ฅผ ๋ฏธ๋ฆฌ ๊ฐ์ ธ์ด.
- next/link ์ ๊ฒฝ์ฐ ์๋์ผ๋ก ํ์ด์ง๋ฅผ ๋ฏธ๋ฆฌ ๊ฐ์ ธ์ค๊ธฐ ๋๋ฌธ์ next/link ๊ฐ ์๋ ํ์์์ ์ ์ฉํจ.

```jsx
// ์ด๋ํ  url > url ๊ฐ์ฒด ์ฌ์ฉ ๊ฐ๋ฅ.
// ์ด๋ ํ ๋ธ๋ผ์ฐ์ ์ ํ์๋  URL.
router.prefetch(url, as);
```

### ๐ฉ router.beforePopState

- ๋ผ์ฐํฐ๊ฐ ๋์ํ๊ธฐ์ ์ ๋ฌด์ธ๊ฐ ์์์ ํ๊ณ  ์ถ์ ๋ ์ฌ์ฉ.

```jsx
...
useEffect(() => {
  router.beforePopState(({ url, as, options }) => {
    // ์๋ ๋ url๋ก๋ง ์ด๋์ ํ์ฉํ๊ณ  ์ถ์๋
    if (as !== '/' && as !== '/other') {
      // Have SSR render bad routes as a 404.
      window.location.href = as
      return false
    }

    return true
  })
}, [])
...
```

### ๐ง router.back

- ๋ค๋ก๊ฐ๊ธฐ.

```jsx
router.back();
```

### ๐ฉโ๐ฆฑ router.reload

- ์๋ก๊ณ ์นจ.

```jsx
router.back();
```

### ๐งโ๐ฆฑ router.events

- next/router๋ก ์ด๋ฒคํธ๋ฅผ ๊ฐ์งํด์ ํน์  ์ด๋ฒคํธ๊ฐ ๋ฐ์ํ๋ฉด ํจ์๋ฅผ ์คํ
  (1) routeChangeStart

```jsx
// ๊ฒฝ๋ก๊ฐ ๋ณ๊ฒฝ๋๋ ์์ ์์ ์ ๋ฐ์.
routeChangeStart(url, { shallow });
```

(2) routeChangeComplete

```jsx
// ๊ฒฝ๋ก ๋ณ๊ฒฝ์ด ์๋ฃ๋๋ฉด ๋ฐ์.
routeChangeComplete(url, { shallow });
```

(3) routeChangeError

```jsx
// ๊ฒฝ๋ก ๋ณ๊ฒฝ ์ ์ค๋ฅ or ๊ฒฝ๋ก ์ ํ ์ทจ์ ์ ๋ฐ์.
// (err.cancelled - ํ์์ด ์ทจ์๋์๋์ง ์ฌ๋ถ)
routeChangeError(url, { shallow });
```

(4) beforeHistoryChange

```jsx
// ๋ธ๋ผ์ฐ์ ์ history๋ฅผ ๋ณ๊ฒฝํ๊ธฐ ์ ์ ๋ฐ์.
beforeHistoryChange(url, { shallow });
```

(5) hashChangeStart

```jsx
// ํด์๋ ๋ณ๊ฒฝ๋์ง๋ง ํ์ด์ง๋ ๋ณ๊ฒฝ๋์ง ์์๋ ๋ฐ์.
hashChangeStart(url, { shallow });
```

(6) hashChangeComplete

```jsx
// ํด์๊ฐ ๋ณ๊ฒฝ๋์์ง๋ง ํ์ด์ง๋ ๋ณ๊ฒฝ๋์ง ์์๋ ๋ฐ์.
hashChangeComplete(url, { shallow });
```

<br/>

### ๐ค๐ป Link ํ๊ทธ๋ก ์ด๋.

- Nextjs ์์ ์ ๊ณต๋๋ ๋ด์ฅํจ์ next/link๋ฅผ import.

```jsx
import Link from 'next/link';
```

- a ํ๊ทธ ์ฌ์ฉํ๋ฏ์ด ์ฐ์ง๋ง, ์ค์  aํ๊ทธ์๋ ๋ค๋ฆ.
- Link๋ฅผ ํตํ ์ด๋์, React ๋ด router๋ฅผ ํตํด ์ด๋, aํ๊ทธ๋ฅผ ํตํ ์ด๋์ ์ค์  URL ์ด๋. (์ค์ DOM์๋ ๋๋ค aํ๊ทธ๋ก ํ๊ธฐ๋๋ค.)

```jsx
<Link href={url}>{name}</Link>
```

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://nextjs.org/docs/api-reference/next/router](https://nextjs.org/docs/api-reference/next/router){:target="\_blank"}
- [https://nextjs.org/docs/api-reference/next/link](https://nextjs.org/docs/api-reference/next/link){:target="\_blank"}
- [https://im-designloper.tistory.com/102](https://im-designloper.tistory.com/102){:target="\_blank"}
  <br/><br/>

---
