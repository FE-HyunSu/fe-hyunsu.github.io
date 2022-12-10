---
layout: post
title: "🚃 subwayInfo"
date: 2022-12-10
tags: [frontend-study]
---

## 🚉 SUBWAY OPEN API

- 서울시 지하철 실시간 도착정보 OPEN API를 가져왔으나, 데이터 활용도를 높이기 위해 api response 값에 대해 정리해보자.

  <br/>

## 🚠 API 요청 인자값.

- KEY : String(필수) / 인증키 / OpenAPI 에서 발급된 인증키.
- TYPE : String(필수) / 요청파일타입 / xml : xml, xml파일 : xmlf, 엑셀파일 : xls, json파일 : json.
- SERVICE : String(필수) / 서비스명 / realtimeStationArrival.
- START_INDEX : INTEGER(필수) / 요청시작위치 / 정수 입력 (데이터 행 시작번호).
- END_INDEX : INTEGER(필수) / 요청종료위치 / 정수 입력 (데이터 행 끝번호).
- statnNm : STRING(필수) / 지하철역명.

<br/>

## 🚟 response 데이터.

- api 호출 시 data.realtimeArrivalList 경로에 필요한 데이터가 들어있다.

<img src="../assets/images/post/img_20221210_01.png" alt="" style="width:90%; width:400px; margin: auto 1rem; vertical-align:top;" />

- response 값들에 대해 자세히 알아보자.

```tsx
// arvlCd : "1" - 도착코드 (0:진입, 1:도착, 2:출발, 3:전역출발, 4:전역진입, 5:전역도착, 99:운행중)
// arvlMsg2 : "서울 도착" - 첫번째도착메세지 (전역 진입, 전역 도착 등)
// arvlMsg3 : "서울" - 두번째도착메세지 (종합운동장 도착, 12분 후 (광명사거리) 등)
// barvlDt : "0" - 열차도착예정시간 (단위:초)
// beginRow : null - ??
// bstatnId : "171" - 종착지하철역ID
// bstatnNm : "광운대" - 종착지하철역명
// btrainNo : "0456" - 열차번호(현재운행하고 있는 호선별 열차번호)
// btrainSttus : null - 열차종류(급행,ITX)
// curPage : null - ??
// endRow : null - ??
// ordkey : "01000광운대0" - 도착예정열차순번(상하행코드(1자리), 순번(첫번째, 두번째 열차 , 1자리), 첫번째 도착예정 정류장 - 현재 정류장(3자리), 목적지 정류장, 급행여부(1자리))
// pageRow : null - ??
// recptnDt : "2022-12-10 15:44:45" - 열차도착정보를 생성한 시각
// rowNum : 1 - ??
// selectedCount : 5 - ??
// statnFid : "1001000134" - 이전지하철역ID
// statnId : "1001000133" - 지하철역ID
// statnList : "1001000133,1004000426,1063080313,1065006501" - 연계지하철역ID(1002000233,1007000744)
// statnNm : "서울" - 지하철역명
// statnTid : "1001000132" - 다음지하철역ID
// subwayHeading : "오른쪽" - 내리는문방향(오른쪽,왼쪽)
// subwayId : "1001" - 지하철호선ID
// subwayList : "1001,1004,1063,1065" - 연계호선ID(1002, 1007 등 연계대상 호상ID)
// subwayNm : null - ??
// totalCount : 23 - ??
// trainCo : null - ??
// trainLineNm : "광운대행 - 시청방면" - 도착지방면(성수행 - 구로디지털단지방면)
// updnLine : "상행" - 상하행선구분(2호선 : (내선:0,외선:1),상행,하행)
```

<br/>

## 🚆 구현 모델 기획

- 1차 : 주요 지하철역 이름을 리스트업하고, 특정역을 클릭 시 실시간 도착정보 데이터 정보를 호출.
- 2차 : 호출 받은 데이터를 보기 편하도록 UI 커스텀 적용.

<br/>

## 🗺 1차. 지하철역 리스트업, 해당역의 실시간 데이터 호출.

- 지하철역 명을 매개변수로 갖는 getSubwayInfo 함수 선언.
- 인자로 받은 지하철역 명을 인코딩 후 axios를 통해 api 호출.
- 해당 함수는 api 통신 후 response 값을 return함.

```tsx
const getSubwayInfo = async (name: string) => {
  return await axios.get(
    `http://swopenAPI.seoul.go.kr/api/subway/${swServiceKey}/json/realtimeStationArrival/1/100/${encodeURIComponent(
      name
    )}`
  );
};
```

- 버튼 UI도 가볍게 만들고, 위 함수를 활용하여 데이터를 호출해보자.

<img src="../assets/images/post/img_20221210_02.png" alt="" style="width:90%; width:400px; margin: auto 1rem; vertical-align:top;" />

<br/>

## 🏰 2차. 호출된 데이터 UI 커스텀.

- 진행중..

<br/>

---

<br/>

## 🎫 참고 페이지

- [https://data.seoul.go.kr](https://data.seoul.go.kr){:target="\_blank"}
- [http://data.seoul.go.kr/dataList/OA-12764/F/1/datasetView.do](http://data.seoul.go.kr/dataList/OA-12764/F/1/datasetView.do){:target="\_blank"}
  <br/><br/>

---
