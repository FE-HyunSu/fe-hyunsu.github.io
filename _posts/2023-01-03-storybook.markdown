---
layout: post
title: "🤐 Storybook"
date: 2023-01-03
tags: [frontend-study]
---

## 👽 Storybook.

- 스토리북(Storybook)은 UI 컴포넌트 개발 도구.
- UI 라이브러리를 내부 개발자들을 위해 문서화(documentation) 목적.
- 외부 공개용 디자인 시스템(Design System)을 개발하기 위한 기본 플랫폼 목적.
- 스토리북(Storybook)을 기본 구성 단위는 스토리(Story)이며 하나의 UI 컴포넌트는 보통 하나 이상의 Story를 가지게 됨.
- 각 Story는 해당 UI 컴포넌트가 어떻게 사용될 수 있는지를 보여주는 샘플.

<br/>

## 🧍 Storybook 설치.

- React NextJS + Typescript.

```sh
// 스토리북 설치.
$ npm install -D sb

// 스토리북 라이브러리 초기화 설치.
$ npx sb init
```

- package.json 파일에 스크립트와 개발 의존성 추가 확인.

```json
"scripts": {
  // 생략
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

- .storybook 디렉터리 내 Storybook 관련 2개의 설정 파일이 있음.
- addons.js : Storybook 애드온을 추가할 때 사용.
- config.js : 그 외 다른 설정을 할 때 사용.
- .storybook/config.js 파일을 열고, src 디렉터리 내부에 stories.js로 끝나는 모든 파일이 Story로 인식되도록 설정해줌.<br/>(기본 설정은 src/stories 디렉터리 하위만 탐색하므로 주석 처리가 하거나 삭제)
- .gitignore에 storybook 관련 내용 추가.

```tsx
# Storybook build outputs
.out
.storybook-out
storybook-static
```

<br/>

## 🦖 StoryBook 구동.

- Storybook 구동 시, 6006 포트로 설정함.

```sh
$ npm run storybook
```

- Storybook은 프로젝트에서 개발하는 매인 애플리케이션과 별개로 따로 구동이 가능한 웹사이트.
- (정리중)

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://im-designloper.tistory.com/98](https://im-designloper.tistory.com/98){:target="\_blank"}
  <br/><br/>

---
