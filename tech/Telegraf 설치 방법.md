centos7 기준

1. telegraf 설치
sudo wget https://dl.influxdata.com/telegraf/releases/telegraf-1.22.3-1.x86_64.rpm
sudo yum localinstall telegraf-1.22.3-1.x86_64.rpm
y 입력


2. telegraf.conf 수정
/etc/telegraf/telegraf.conf

```
[global_tags]

# Configuration for telegraf agent
[agent]
    interval = "10s"
    debug = false
    hostname = "server-hostname"
    round_interval = true
    flush_interval = "10s"
    flush_jitter = "0s"
    collection_jitter = "0s"
    metric_batch_size = 1000
    metric_buffer_limit = 10000
    quiet = false
    logfile = ""
    omit_hostname = false

###############################################################################
#                                  OUTPUTS                                    #
###############################################################################

[[outputs.influxdb]]
    urls = ["http://localhost:8086"] # InfluxDB가 설치된 서버의 IP를
    database = "telegraf" # 데이터바에스 이름, 생성이 되어있지 않으면 자동 생성됨
    timeout = "5s"
    username = "admin" # InfluxDB 기본 계정
    password = "admin"
    retention_policy = ""

###############################################################################
#                                  INPUTS                                     #
###############################################################################

[[inputs.cpu]]
    percpu = true
    totalcpu = true
    collect_cpu_time = false
    report_active = false
[[inputs.disk]]
    ignore_fs = ["tmpfs", "devtmpfs", "devfs", "iso9660", "overlay", "aufs", "squashfs"]
[[inputs.io]]
[[inputs.mem]]
[[inputs.net]]
[[inputs.system]]
[[inputs.swap]]
[[inputs.netstat]]
[[inputs.processes]]
[[inputs.kernel]]
```

- agent : 수집 및 전송 주기 설정
- outputs : 수집된 데이터를 어디로 보낼지 설정
- inputs : 수집할 항목 설정


3. 구동
```
systemctl start telegraf
systemctl enable telegraf
```

4. 테스트
telegraf -test -config /etc/telegraf/telegraf.conf

5.  InfluxDB랑 연결
```sh
brew update
brew install influxdb
```

6. 텔레그래프 로그 확인
sudo journalctl -u telegraf -f