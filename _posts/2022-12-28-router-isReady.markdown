---
layout: post
title: "๐งฏ router.isReady"
date: 2022-12-28
tags: [issue]
---

## ๐ ๊ฐ์.

- Nextjs์์ Router๋ฅผ ์ฌ์ฉํ๋ค๋ณด๋ฉด ์ปดํฌ๋ํธ ์ต์ด ๋ ๋๋ง ์์ ์์ router ์ ๋ณด๋ฅผ ์ป์ด์ค๋ ค๊ณ  ํ ๋ ๊ฐ์ด ์ ํธ์ถ๋์ง ์๋๋ค.
- ์ ์  ํ์ผ ์ต์ ํ(Automatic Static Optimization)์ ์ํด ์ ์ ์ผ๋ก ์ต์ ํ๋ ํ์ด์ง๋ ๋ฃจํธ ๋งค๊ฐ ๋ณ์๊ฐ ์ ๊ณต๋์ง ์์์, query๋ ๋น ๊ฐ์ฒด๊ฐ ๋๋ค๊ณ  ํจ.
- router.isReady๋ฅผ ํตํด ์ด๋ฅผ ์ฒดํฌํ๊ณ  ํด๊ฒฐํ  ์ ์๋ค.

## ๐ชซ ๋ฐ๋ก ํด๊ฒฐ.

- useEffect Hook์ ์์กด์ฑ ๋ฐฐ์ด์ router.isReady ๊ฐ์ ๋ด์ ํธ์ถ.
- NextJS@10.0.5 ๋ฒ์  ์ด์.
- ```tsx
  ...
  const router = useRouter();
  ...
  useEffect(() => {
    if (!router.isReady) return;
    console.log(lat);
    console.log(lng);
  }, [router.isReady]);
  ```

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://im-designloper.tistory.com/98](https://im-designloper.tistory.com/98){:target="\_blank"}
  <br/><br/>

---
