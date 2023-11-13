고성능 [[시계열]] 데이터베이스(Time Series Database, TSDB)

[[InfluxData]]가 만듦

시간에 따른 데이터를 효과적으로 수집, 저장, 검색 및 관리하기 위해 설계된 [[오픈 소스]] [[DBMS]]

데이터를 효율적으로 저장하고 쿼리할 수 있는 기능을 제공하며, [[모니터링]] 및 분석 시나리오에 적합합

InfluxDB는 주로 [[메트릭]] 데이터 및 [[시계열]] 데이터를 저장하고 분석하는 데 사용됨


## RDB와 구조비교

|RDB|InfluxDB|
|-|-|
|Table|Measurement
|Column|Key
|Indexed Column|Tag Key (String Only)
|Unindexed Column|Fileld Key
|Row|Point

## 버전 비교

|버전|1.x|2.x|
|-|-|-|
|데이터베이스 명칭|database|bucket
|웹UI|미지원|지원
|인증 방식|id, password|organization, token
|쿼리 언어|influxQL|Flux
|스택|TICK|TI(I에 CK가 통합됨)
|보존 정책|Retention Policy|Retention Period

## [[InfluxDB 설치 방법]]






