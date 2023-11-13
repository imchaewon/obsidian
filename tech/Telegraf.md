![[707041d1-f715-4982-aacc-8b14e0b277d5.png]]

[[InfluxData]]에서 개발한 [[Go]] 언어로 [[개발]]된 범용적인 플러그인 기반 [[데이터 수집 에이전트]]

주로 [[메트릭]] 데이터를 수집하고 다양한 [[데이터베이스]]나 [[모니터링 시스템]]으로 전송하기 위해 사용됨

다양한 [[Telegraf 입력 플러그인]]을 통해 여러 [[데이터 소스]]에서 데이터를 수집할 수 있음

수집한 데이터를 다양한 출력 플러그인을 통해 다양한 형식으로 다양한 [[Telegraf 목적지]]에 전송할 수 있음

데이터를 [[필터링]], 처리, 집계하는 기능을 지원함

[[SNMP]]를 지원함

[[JSON]]형식을 지원함


[[ELK 스택]]에 [[Beats]]가 있다면 [[TICK 스택]]에는 Telegraf가 있음

다양한 소스에서 데이터를 수집할 수 있음
- **[[서버]] 및 [[시스템]]**: [[CPU]], 메모리, 디스크, [[네트워크]] 등 [[시스템 리소스 메트릭]]을 수집함
- **데이터베이스**: Telegraf는 여러 데이터베이스에서 데이터를 수집할 수 있습니다. [[InfluxDB]], [[MySQL]], [[PostgreSQL]], [[MongoDB]], [[Redis]] 등에서 데이터베이스 메트릭을 수집할 수 있음
- **[[네트워크 장비]]**: [[SNMP]]를 사용하여 라우터, 스위치, 서버 등의 네트워크 장비에서 메트릭을 수집할 수 있음
- **[[클라우드 서비스]]**: Telegraf는 클라우드 서비스인 AWS, Google Cloud Platform, Azure 등에서 메트릭을 수집할 수 있음
- **웹 서비스**: [[HTTP]], [[JSON]], [[XML]] 등의 웹 서비스로부터 데이터를 수집할 수 있음
- **컨테이너화된 환경**: Docker, Kubernetes와 같은 컨테이너 환경에서 컨테이너 메트릭을 수집할 수 있음

여러 데이터베이스([[InfluxDB]] 등), 서버, 네트워크 장치 및 다양한 데이터 소스에서 [[메트릭]], 로그 데이터를 수집하고 특정[[Telegraf 목적지]]로 전송함

텔레그래프에서 사용하여 메트릭 데이터와 로그 데이터를 모두 수집하고 처리하는 것이 가능함
이를 위해서는 텔레그래프의 입력 플러그인 중 하나를 사용하여 그 데이터를 수집하는 설정을 추가해야 함
예를 들어, 텔레그래프의 "inputs.logparser" 플러그인을 사용하여 로그 파일을 모니터링하고 데이터를 수집할 수 있음

## [[Telegraf 와 Beats의 차이]]


## Telegraf 흐름도 2 (Processor와 Aggregator plugin)

![[다운로드.png]]

Input과 Out Plugin 사이에 Process와 Aggregate가 자리하게 되며 transform/decorate/filter를 거쳐  
mean/quantiles/min,max/count 와 같은 함수를 거치게 된다

여러개의 input을 가질수도 있고 여러개의 output을 가질수도 있다  
만약 destination을 InfluxDB만 쓰는게 아니라 Graphite와 같은 다른 시계열 Data Engine을 사용할수도 있다  
만약 Telegraf를 Collector로 쓴다면 각각 다른 시계열 Data Engine에 데이터를 보내서 성능비교를 할수도 있다

Telegarf는 plugin 방식을 사용하며 4가지 플러그인 컨셉을 가지고 있다

1. **Input Plugin** : 시스템, 서비스, 써드파티 API로부터 메트릭 수집
    
2. **Processor Plugin** : 매트릭 설명, 변환 등을 지원
    
3. **Aggregator Plugin** : mean, min, max, quantiles와 같은 다양한 종합 매트릭 지원
    
4. **Output Plugin** : 다양한 목적지에 매트릭 저장
    

Telegraf v1.7의 Input Plugin 종류 : [https://docs.influxdata.com/telegraf/v1.7/plugins/inputs/](https://docs.influxdata.com/telegraf/v1.7/plugins/inputs/ "https://docs.influxdata.com/telegraf/v1.7/plugins/inputs/")

Telegraf v1.7의 Output Plugin 종류 : [https://docs.influxdata.com/telegraf/v1.7/plugins/outputs/](https://docs.influxdata.com/telegraf/v1.7/plugins/outputs/ "https://docs.influxdata.com/telegraf/v1.7/plugins/outputs/")


## Telegraf 흐름도 3
![[Telegraf-GREY-Diagram 2.webp]]


## [[Telegraf 설치 방법]]