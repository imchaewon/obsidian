경량이면서, 특정 유형의 데이터에 특화된 데이터 수집 [[에이전트]]

- Elastic에서 [[개발]]한 데이터 수집 [[에이전트]]
- Beats는 특정 유형의 데이터에 특화되어 있음
	- [[Filebeat]] : 로그 파일 수집기
		- 파일에서 [여러 유형의 데이터](https://okestro.atlassian.net/wiki/spaces/6/pages/1365934143/Telegraf+Beats#Filebeat-%EC%88%98%EC%A7%91-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%9C%A0%ED%98%95 "#Filebeat-수집-데이터-유형")를 수집하고, 실시간으로 이를 [지정된 대상](https://okestro.atlassian.net/wiki/spaces/6/pages/1365934143/Telegraf+Beats#Beats-%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%86%A1-%EB%AA%A9%EC%A0%81%EC%A7%80-%EC%9C%A0%ED%98%95 "#Beats-의-데이터-전송-목적지-유형")으로 전송함
		- [[로그 파일]]의 변경을 감지하고, 변경된 부분만을 전송하여 효율적으로 데이터를 처리함
		- 다양한 [[로그]] [[포맷]]에 대한 지원 및 [[파싱]] 기능을 제공함
	- [[Metricbeat]] : 시스템 및 서비스 메트릭 수집기
		- 여러 [유형의 메트릭 데이터](https://okestro.atlassian.net/wiki/spaces/6/pages/1365934143/Telegraf+Beats#Metricbeat-%EC%88%98%EC%A7%91-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%9C%A0%ED%98%95 "#Metricbeat-수집-데이터-유형")를 수집하고, 실시간으로 이를 [지정된 대상](https://okestro.atlassian.net/wiki/spaces/6/pages/1365934143/Telegraf+Beats#Beats-%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%86%A1-%EB%AA%A9%EC%A0%81%EC%A7%80-%EC%9C%A0%ED%98%95 "#Beats-의-데이터-전송-목적지-유형")으로 전송함|

- Beats는 데이터를 [[Elasticsearch]]에 직접 전송할 수 있으며, [[Logstash]]를 통해서 데이터를 전송할 수도 있음

모든 유형의 데이터를 위한 모든 종류의 수집기
- [[Filebeat]] - 로그파일
- [[Metricbeat]] - Metrics를 주기적으로 수집
- Packetbeat - 네트워크 데이터
- [[Winlogbeat]] - [[Windows]] [[이벤트 로그]]
- Auditbeat - 감사(Audit) 데이터
- [[Heartbeat]] - 가동 시간 [[모니터링]]
- Functionbeat - [[서버]]를 사용하지 않는 수집기

## Beats 의 데이터 전송 목적지 유형

- **[[Elasticsearch]]**: 기본적으로 Beats는 수집한 [[메트릭]] 데이터를 [[Elasticsearch]]로 전송하여 저장, 검색, 분석 및 [[시각화]]에 활용함
    
- **[[Logstash]]**: Beats는 [[Logstash]]로 메트릭 데이터를 전송할 수 있음. [[Logstash]]는 데이터를 가공하거나 다른 대상으로 전송하는 역할을 함
    
- **다른 출력(Output) 옵션**: Beats는 [[Kafka]], [[Redis]], [[Amazon S3]], [[MySQL]], [[PostgreSQL]] 등과 같은 다른 출력 옵션을 통해 [[메트릭]] 데이터를 다양한 대상으로 전송할 수 있음


