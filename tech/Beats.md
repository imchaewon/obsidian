서버에 에이전트 형식으로 설치하는 오픈소스 데이터 수집기
Beats는 데이터를 [[Elasticsearch]]에 직접 전송할 수 있으며, [[Logstash]]를 통해서 데이터를 전송할 수도 있음

모든 유형의 데이터를 위한 모든 종류의 수집기
- [[Filebeat]] - 로그파일
- [[Metricbeat]] - Metrics를 주기적으로 수집
- Packetbeat - 네트워크 데이터
- [[Winlogbeat]] - Windows 이벤트 로그
- Auditbeat - 감사(Audit) 데이터
- [[Heartbeat]] - 가동 시간 모니터링
- Functionbeat - 서버를 사용하지 않는 수집기