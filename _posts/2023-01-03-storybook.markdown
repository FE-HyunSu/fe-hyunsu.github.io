---
layout: post
title: "๐ค Storybook(์ ๋ฆฌ์ค)"
date: 2003-01-03
tags: [frontend-study]
---

## ๐ฝ Storybook ์ด๋?

- ์คํ ๋ฆฌ๋ถ(Storybook)์ UI ์ปดํฌ๋ํธ ๊ฐ๋ฐ ๋๊ตฌ.

## ๐งบ Storybook ์ฌ์ฉ ๋ชฉ์ .

- UI ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ๋ด๋ถ ๊ฐ๋ฐ์๋ค์ ์ํด ๋ฌธ์ํ(documentation) ๋ชฉ์ .
- ์ธ๋ถ ๊ณต๊ฐ์ฉ ๋์์ธ ์์คํ(Design System)์ ๊ฐ๋ฐํ๊ธฐ ์ํ ๊ธฐ๋ณธ ํ๋ซํผ ๋ชฉ์ .

## ๐ Storybook ํน์ง.

- ๊ธฐ๋ณธ ๊ตฌ์ฑ ๋จ์๋ ์คํ ๋ฆฌ(Story)์ด๋ฉฐ ํ๋์ UI ์ปดํฌ๋ํธ๋ ๋ณดํต ํ๋ ์ด์์ Story๋ฅผ ๊ฐ์ง๊ฒ ๋จ.
- ๊ฐ Story๋ ํด๋น UI ์ปดํฌ๋ํธ๊ฐ ์ด๋ป๊ฒ ์ฌ์ฉ๋  ์ ์๋์ง๋ฅผ ๋ณด์ฌ์ฃผ๋ ์ํ.
- Storybook์ ํ๋ก์ ํธ์์ ๊ฐ๋ฐํ๋ ๋งค์ธ ์ ํ๋ฆฌ์ผ์ด์๊ณผ ๋ณ๊ฐ๋ก ๋ฐ๋ก ๊ตฌ๋์ด ๊ฐ๋ฅํ ์น์ฌ์ดํธ.

<br/>

## ๐ง Storybook ์ค์น. (React NextJS + Typescript)

- ์คํ ๋ฆฌ๋ถ + webpack ์ค์น.

```sh
$ npx sb init --builder webpack5
```

<br/>

## ๋ฒ๋ค๋ง์ผ๋ก Vite๊ฐ ์๋ Webpack์ ์ ํํ ์ด์ .

- Vite์ SSR ์ง์ ๋จ๊ณ๋ ์์ง ์คํ์  ๋จ๊ณ๋ผ๊ณ  ํจ.
- Nextjs์ ๊ฐ์ SSR์์ ์ฌ์ฉ ์ vite-plugin-ssr๊ณผ ๊ฐ์ ํ๋ฌ๊ทธ์ธ ๋์์ ๋ฐ์์ผ ํจ.

```sh
// ์คํ ๋ฆฌ๋ถ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ด๊ธฐํ ์ค์น.
$ npx sb init
```

- package.json ํ์ผ์ ์คํฌ๋ฆฝํธ์ ๊ฐ๋ฐ ์์กด์ฑ ์ถ๊ฐ ํ์ธ.

```json
"scripts": {
  // ์๋ต
  "storybook": "start-storybook -p 6006",
  "build-storybook": "build-storybook"
},
"devDependencies": {
  "@storybook/addon-actions": "^6.5.15",
  "@storybook/addon-essentials": "^6.5.15",
  "@storybook/addon-interactions": "^6.5.15",
  "@storybook/addon-links": "^6.5.15",
  "@storybook/builder-webpack5": "^6.5.15",
  "@storybook/manager-webpack5": "^6.5.15",
  "@storybook/react": "^6.5.15",
  "@storybook/testing-library": "^0.0.13",
  "@types/styled-components": "^5.1.26",
  "babel-loader": "^8.3.0",
  "sb": "^6.5.15"
}
```

- .storybook ๋๋ ํฐ๋ฆฌ ๋ด Storybook ๊ด๋ จ 2๊ฐ์ ์ค์  ํ์ผ์ด ์์.
- addons.js : Storybook ์ ๋์จ์ ์ถ๊ฐํ  ๋ ์ฌ์ฉ.
- config.js : ๊ทธ ์ธ ๋ค๋ฅธ ์ค์ ์ ํ  ๋ ์ฌ์ฉ.
- .storybook/config.js ํ์ผ์ ์ด๊ณ , src ๋๋ ํฐ๋ฆฌ ๋ด๋ถ์ stories.js๋ก ๋๋๋ ๋ชจ๋  ํ์ผ์ด Story๋ก ์ธ์๋๋๋ก ์ค์ ํด์ค.<br/>(๊ธฐ๋ณธ ์ค์ ์ src/stories ๋๋ ํฐ๋ฆฌ ํ์๋ง ํ์ํ๋ฏ๋ก ์ฃผ์ ์ฒ๋ฆฌ๊ฐ ํ๊ฑฐ๋ ์ญ์ )
- .gitignore์ storybook ๊ด๋ จ ๋ด์ฉ ์ถ๊ฐ.

```tsx
# Storybook build outputs
.out
.storybook-out
storybook-static
```

<br/>

## ๐ฆ StoryBook ๊ตฌ๋.

- Storybook ๊ตฌ๋ ์, 6006 ํฌํธ๋ก ์ค์ ํจ.

```sh
$ npm run storybook
```

<br/>

---

<br/>

## ๐ซ ์ฐธ๊ณ  ํ์ด์ง

- [https://im-designloper.tistory.com/98](https://im-designloper.tistory.com/98){:target="\_blank"}
  <br/><br/>

---
