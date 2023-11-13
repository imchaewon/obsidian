## 설치
- centos
	- 버전 1 : sudo yum install influxdb
	- 버전 2 : sudo yum install influxdb2
- macOS
	- brew install influxdb

## 버전확인
influxd version

## 설치경로 확인
brew --prefix influxdb

## 설정파일
~/.influxdbv2/configs
- 다른 서버에서 전송할 수 있게 수신 설정
```toml
[[input]]
  name = "influx"
  listen = ":8086"  # 수신 대기할 포트를 설정
```
- 설정 파일이 적용되도록 재시작
	- `sudo service influxdb restart`

## 실행
- centos
	- sudo service influxdb start
- macOS
	- brew services start influxdb

## 중지
- macOS
	- brew services stop influxdb

## 삭제(계정정보 등 설정도 함께 삭제(안되는듯))
- macOS
	- brew uninstall --force influxdb
	- brew cleanup
	- rm -rf /usr/local/etc/influxdb
	- rm -rf /usr/local/var/influxdb
	- rm -rf $(brew --cache)

## UI 접속
http://localhost:8086/

로그인에 사용할 Username(ID) / Password 설정, Organization과 Bucket 이름 설정
QUICK START로 빠르게 시작

## influx CLI 설치
brew install influxdb-cli

이후 아래 명령어로 CLI접속이 가능함
influx v1 shell











