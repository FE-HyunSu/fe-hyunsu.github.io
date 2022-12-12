---
layout: post
title: "🛟 API Error (http)"
date: 2022-12-11
tags: [issue]
---

## 🚁 API ERROR (http)

- 프로젝트 진행중 외부 api를 연동하는 작업에서 로컬환경에선 이슈가 없었으나, 실제 라이브 배포시 api 통신을 하지 못하는 이슈가 발생되었다.

### 🌎 에러 내용

```
Mixed Content: The page at '{url}' was loaded over HTTPS, but requested an insecure XMLHttpRequest endpoint '{url}'. This request has been blocked; the content must be served over HTTPS.
```

- https 페이지에서 http 호출을 했을때 발생되는 에러.
- https는 http와 달리 보안이 강화된 프로토콜.
- https로 통신을 하는중 http로 연결이 발생하면 https의 보안정책에 의해서 block 처리 된다.
- http -> https 요청은 (O)
- https -> http 요청은 (X)

<br/>

### 🗻 해결 방법 1

- 호출 api의 http를 https 로 변경.
- 또는 아래 meata 태그를 추가. (React 프로젝트라면 \_document.tsx)

```tsx
<meta
  http-equiv="Content-Security-Policy"
  content="upgrade-insecure-requests"
></meta>
```

<br/>

### 🏔 해결 방법 2

- 해결방법 1,2는 결국 http 요청을 https로 변환하여 요청하는 방식이다.
- http환경에서만 제공되는 api 라면 'https://proxy.cors.sh' 를 이용하여, 우회하여 사용이 가능.<br/>ex) https://proxy.cors.sh/http://{url}
- 보안상 http 주소의 api 요청은 자제하도록 하자.

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://github.com/swagger-api/swagger-ui/issues/1670](https://github.com/swagger-api/swagger-ui/issues/1670){:target="\_blank"}
- [https://cors.sh](https://cors.sh){:target="\_blank"}
  <br/><br/>

---
