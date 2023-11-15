centos 기준

1. Grafana Yum 저장소 추가 (/etc/yum.repos.d폴더에 grafana.repo파일 생성)
```
sudo tee /etc/yum.repos.d/grafana.repo<<EOF
[grafana]
name=grafana
baseurl=https://packages.grafana.com/oss/rpm
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF
```

2. grafana 설치
sudo yum install grafana
Complete! 나올 때까지 y 입력

3. 구동
sudo systemctl start grafana-server

4. 브라우저에서 접속 (ec2 방화벽 3000 포트 열어야함)
IP주소:3000

접속 후 로그인
기본 id/password : admin/admin

새 비밀번호 설정
admin1234

5. 데이터 소스 추가
Add your first data source 클릭 → InfluxDB 클릭
InfluxDB Details 에 InfluxDB 정보 입력하면되는데
⭐️ Influx2 라면, Query language를 InfluxQL이 아닌, Flux로 설정해야함
Name: Influxdb
HTTP
	URL: http://IP주소:8086
Database
	Organization: 조직명입력
	Token: 토큰입력
	Default Bucket: 버킷명입력

6. 다른사람들이 Grafana 홈페이지에 올려둔 대시보드 다운
아래 링크 들어가서 Download JSON으로 json파일 다운
ex1) https://grafana.com/grafana/dashboards/2381-olympus/
ex2) https://grafana.com/grafana/dashboards/10581-host-dashboard/

7. 대시보드 생성
대시보드 → New → Import → Upload dashboard JSON file










