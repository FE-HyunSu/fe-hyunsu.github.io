---
layout: post
title: "🗺 Geolocation"
date: 2022-12-17
tags: [frontend-study]
---

## 🚁 navigator.Geolocation API.

- 사용자의 현재 위치 정보를 가져와야 하는 경우, 해당 API를 사용.
- 사용자의 브라우저가 위치 정보 접근 권한을 요청 -> 사용자가 허가할 경우 동작함.
- 현재 장치에서 사용 가능한 최선의 방법(GPS, WiFi, ...)을 통해 위치를 알아냅니다.

<br/>

## 🗽 API 사용.

- Geolocation API는 navigator.geolocation을 통해 접근.
- Geolocation.getCurrentPosition(): 장치의 현재 위치를 가져옴.
- Geolocation.watchPosition(): 장치의 위치가 바뀔 때마다, 자동으로 새로운 위치를 사용해 호출할 처리기 함수를 등록.
- 해당 함수 호출 시 최대 3가지의 매개변수를 가질 수 있음.
- 성공시 실행 함수(필수) : GeolocationPosition
- 실패시 실행 함수(선택) : GeolocationPositionError
- 선택적 지정 옵션(선택) : PositionOptions

```tsx
navigator.geolocation.getCurrentPosition((position) => {
  console.log(`위도` : position.coords.latitude);
  console.log(`경도` : position.coords.longitude);
});
```

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://developer.mozilla.org/ko/docs/Web/API/Geolocation_API](https://developer.mozilla.org/ko/docs/Web/API/Geolocation_API){:target="\_blank"}
  <br/><br/>

---
