---
layout: post
title: '🛝 NextJS Router'
date: 2022-11-25
tags: [frontend-study]
---

## ⛷ Nextjs Router

- Nextjs에서 Router 메서드에 대해 알아보자.

<br/>

### ☝🏻 useRouter import.

- Nextjs 에서 함수형식으로 사용할 수 있는 내장 라이브러리 useRouter를 import 함.

```jsx
import { useRouter } from 'next/router'
...
```

<br/>

### ✌🏻 useRouter method 종류.

### 👶 router.push

```jsx
router.push(url, as, options);
```

- url: [필수] 라우팅 하려는 url.
- as: [선택] 브라우저 url 바에 보여지는 path.
- options: [선택] scroll(라우팅 후 스크롤업), shallow, locale 등.

```jsx
// ex) /history 로 이동.
router.push('/history');
// ex) /history?pageIndex=3로 이동되지만, URL표기는 /history로 적용.
router.push('/history?pageIndex=3', '/history');
```

### 👧 router.replace

```jsx
router.replace(url, as, options);
```

- router.push 와 사용방식 동일.
- 차이점은 router history stack에 쌓지 않고, 페이지 이동.
- ex) 서비스 페이지 -> 로그인 -> 로그인 성공 후 뒤로가기(router.back()) 처리 했을때 서비스페이지로 이동.

### 🧒 router.prefetch

- 빠른 클라이언트 전환을 위해 페이지를 데이터를 미리 가져옴.
- next/link 의 경우 자동으로 페이지를 미리 가져오기 때문에 next/link 가 없는 탐색에서 유용함.

```jsx
// 이동할 url > url 객체 사용 가능.
// 이동 후 브라우저에 표시될 URL.
router.prefetch(url, as);
```

### 👩 router.beforePopState

- 라우터가 동작하기전에 무언가 작업을 하고 싶을 때 사용.

```jsx
...
useEffect(() => {
  router.beforePopState(({ url, as, options }) => {
    // 아래 두 url로만 이동을 허용하고 싶을때
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

### 🧑 router.back

- 뒤로가기.

```jsx
router.back();
```

### 👩‍🦱 router.reload

- 새로고침.

```jsx
router.back();
```

### 🧑‍🦱 router.events

- next/router로 이벤트를 감지해서 특정 이벤트가 발생하면 함수를 실행
  (1) routeChangeStart

```jsx
// 경로가 변경되는 시작 시점에 발생.
routeChangeStart(url, { shallow });
```

(2) routeChangeComplete

```jsx
// 경로 변경이 완료되면 발생.
routeChangeComplete(url, { shallow });
```

(3) routeChangeError

```jsx
// 경로 변경 시 오류 or 경로 전환 취소 시 발생.
// (err.cancelled - 탐색이 취소되었는지 여부)
routeChangeError(url, { shallow });
```

(4) beforeHistoryChange

```jsx
// 브라우저의 history를 변경하기 전에 발생.
beforeHistoryChange(url, { shallow });
```

(5) hashChangeStart

```jsx
// 해시는 변경되지만 페이지는 변경되지 않을때 발생.
hashChangeStart(url, { shallow });
```

(6) hashChangeComplete

```jsx
// 해시가 변경되었지만 페이지는 변경되지 않을때 발생.
hashChangeComplete(url, { shallow });
```

<br/>

### 🤟🏻 Link 태그로 이동.

- Nextjs 에서 제공되는 내장함수 next/link를 import.

```jsx
import Link from 'next/link';
```

- a 태그 사용하듯이 쓰지만, 실제 a태그와는 다름.
- Link를 통한 이동은, React 내 router를 통해 이동, a태그를 통한 이동은 실제 URL 이동. (실제DOM에는 둘다 a태그로 표기된다.)

```jsx
<Link href={url}>{name}</Link>
```

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://nextjs.org/docs/api-reference/next/router](https://nextjs.org/docs/api-reference/next/router){:target="\_blank"}
- [https://nextjs.org/docs/api-reference/next/link](https://nextjs.org/docs/api-reference/next/link){:target="\_blank"}
- [https://im-designloper.tistory.com/102](https://im-designloper.tistory.com/102){:target="\_blank"}
  <br/><br/>

---
