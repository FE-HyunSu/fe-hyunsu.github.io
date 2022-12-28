---
layout: post
title: "🧯 router.isReady"
date: 2022-12-28
tags: [frontend-study]
---

## 🔋 개요.

- Nextjs에서 Router를 사용하다보면 컴포넌트 최초 렌더링 시점에서 router 정보를 얻어오려고 할때 값이 잘 호출되지 않는다.
- 정적 파일 최적화(Automatic Static Optimization)에 의해 정적으로 최적화된 페이지는 루트 매개 변수가 제공되지 않아서, query는 빈 객체가 된다고 함.
- router.isReady를 통해 이를 체크하고 해결할 수 있다.

## 🪫 바로 해결.

- useEffect Hook의 의존성 배열에 router.isReady 값을 담아 호출.
- NextJS@10.0.5 이후.
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

## 🎫 참고 페이지

- [https://im-designloper.tistory.com/98](https://im-designloper.tistory.com/98){:target="\_blank"}
  <br/><br/>

---
