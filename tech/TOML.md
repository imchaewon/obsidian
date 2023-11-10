Tom's Obvious Minimal Language

TOML은 간단하고 가독성이 높은 설정 파일 형식

[[YAML]]과 비슷한 목적을 가지고 있지만, 문법과 특징에서 차이가 있음

### TOML
```
[[outputs.file]]
	files = ["stdout", "/tmp/telegraf-metrics.out"]
	
[[outputs.influxdb]]
	urls = ["http://localhost:8086"]
	database = "your_database"
	username = "your_username"
	password = "your_password"
```

### [[YAML]]
```
outputs: 
	- file: 
		files: 
			- stdout
			- /tmp/telegraf-metrics.out
	- influxdb: 
		urls: 
			- http://localhost:8086
		database: "your_database"
		username: "your_username"
		password: "your_password"
```


TOML은 명시적이고 간단한 구조를 가지며 가독성이 좋음
반면에 YAML은 들여쓰기를 통해 계층을 나타내는 데에 의존하며, 문법적으로 더 자유로운 구조를 갖고 있음 

TOML과 [[YAML]]은 각각의 장단점이 있으며, 사용되는 환경 및 개발자의 취향에 따라 선택됨

