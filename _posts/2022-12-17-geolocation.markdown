---
layout: post
title: "๐บ Geolocation"
date: 2022-12-17
tags: [frontend-study]
---

## ๐ navigator.Geolocation API.

- ์ฌ์ฉ์์ ํ์ฌ ์์น ์ ๋ณด๋ฅผ ๊ฐ์ ธ์์ผ ํ๋ ๊ฒฝ์ฐ, ํด๋น API๋ฅผ ์ฌ์ฉ.
- ์ฌ์ฉ์์ ๋ธ๋ผ์ฐ์ ๊ฐ ์์น ์ ๋ณด ์ ๊ทผ ๊ถํ์ ์์ฒญ -> ์ฌ์ฉ์๊ฐ ํ๊ฐํ  ๊ฒฝ์ฐ ๋์ํจ.
- ํ์ฌ ์ฅ์น์์ ์ฌ์ฉ ๊ฐ๋ฅํ ์ต์ ์ ๋ฐฉ๋ฒ(GPS, WiFi, ...)์ ํตํด ์์น๋ฅผ ์์๋๋๋ค.

<br/>

## ๐ฝ API ์ฌ์ฉ.

- Geolocation API๋ navigator.geolocation์ ํตํด ์ ๊ทผ.
- Geolocation.getCurrentPosition(): ์ฅ์น์ ํ์ฌ ์์น๋ฅผ ๊ฐ์ ธ์ด.
- Geolocation.watchPosition(): ์ฅ์น์ ์์น๊ฐ ๋ฐ๋ ๋๋ง๋ค, ์๋์ผ๋ก ์๋ก์ด ์์น๋ฅผ ์ฌ์ฉํด ํธ์ถํ  ์ฒ๋ฆฌ๊ธฐ ํจ์๋ฅผ ๋ฑ๋ก.
- ํด๋น ํจ์ ํธ์ถ ์ ์ต๋ 3๊ฐ์ง์ ๋งค๊ฐ๋ณ์๋ฅผ ๊ฐ์ง ์ ์์.
- ์ฑ๊ณต์ ์คํ ํจ์(ํ์) : GeolocationPosition
- ์คํจ์ ์คํ ํจ์(์ ํ) : GeolocationPositionError
- ์ ํ์  ์ง์  ์ต์(์ ํ) : PositionOptions

```tsx
navigator.geolocation.getCurrentPosition((position) => {
  console.log(`์๋` : position.coords.latitude);
  console.log(`๊ฒฝ๋` : position.coords.longitude);
});
```

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://developer.mozilla.org/ko/docs/Web/API/Geolocation_API](https://developer.mozilla.org/ko/docs/Web/API/Geolocation_API){:target="\_blank"}
  <br/><br/>

---
