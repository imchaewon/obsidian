
현재 [[Telegraf]]의 설정파일은 [[TOML]]형식만을 지원함

1. **File Output (`outputs.file`):**
    - 로컬 파일에 데이터를 저장

```
[[outputs.file]]
	files = ["stdout", "/tmp/telegraf-metrics.out"]
```


2. **InfluxDB Output (`outputs.influxdb`):**
    - InfluxDB에 데이터를 전송

```
[[outputs.influxdb]]
	urls = ["http://localhost:8086"]
	database = "your_database"
	username = "your_username"
	password = "your_password"
```


3. **Prometheus Output (`outputs.prometheus_client`):**
    - Prometheus로 메트릭을 노출

```
[[outputs.prometheus_client]]
	listen = ":9273"
```


4. **OpenTSDB Output (`outputs.opentsdb`):**
    - OpenTSDB에 데이터를 전송

```
[[outputs.opentsdb]]
	address = "localhost:4242"
```


5. **Kafka Output (`outputs.kafka`):**
    - Kafka에 데이터를 전송

```
[[outputs.kafka]]
	brokers = ["localhost:9092"]
	topic = "telegraf_metrics"
```


6. **HTTP Output (`outputs.http`):**
    - HTTP 엔드포인트로 데이터를 전송

```
[[outputs.http]]
	url = "http://example.com/metrics"
	data_format = "influx"
```


7. **Elasticsearch Output (`outputs.elasticsearch`):**
    - Elasticsearch에 데이터를 전송

```
[[outputs.elasticsearch]]
	urls = ["http://localhost:9200"]
	index_name = "telegraf_metrics"
```


8. **Socket Listener Output (`outputs.socket_listener`):**
    - 소켓 리스너를 통해 데이터를 전송

```
[[outputs.socket_listener]]
	service_address = "tcp://:8094"
```






