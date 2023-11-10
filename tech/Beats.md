서버에 에이전트 형식으로 설치하는 오픈소스 데이터 수집기
Beats는 데이터를 [[Elasticsearch]]에 직접 전송할 수 있으며, [[Logstash]]를 통해서 데이터를 전송할 수도 있음

모든 유형의 데이터를 위한 모든 종류의 수집기
- [[Filebeat]] - 로그파일
- [[Metricbeat]] - Metrics를 주기적으로 수집
- Packetbeat - 네트워크 데이터
- [[Winlogbeat]] - [[Windows]] [[이벤트 로그]]
- Auditbeat - 감사(Audit) 데이터
- [[Heartbeat]] - 가동 시간 [[모니터링]]
- Functionbeat - [[서버]]를 사용하지 않는 수집기

## Beats 의 데이터 전송 목적지 유형

- **[[Elasticsearch]]**: 기본적으로 beats는 수집한 [[메트릭]] 데이터를 [[Elasticsearch]]로 전송하여 저장, 검색, 분석 및 [[시각화]]에 활용함
    
- **[[Logstash]]**: beats는 [[Logstash]]로 메트릭 데이터를 전송할 수 있음. [[Logstash]]는 데이터를 가공하거나 다른 대상으로 전송하는 역할을 함
    
- **다른 출력(Output) 옵션**: beats는 [[Kafka]], [[Redis]], [[Amazon S3]], [[MySQL]], [[PostgreSQL]] 등과 같은 다른 출력 옵션을 통해 [[메트릭]] 데이터를 다양한 대상으로 전송할 수 있음


