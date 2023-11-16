Ubuntu 기준
sudo apt update
sudo apt install mariadb-server

설치 확인
mariadb --version

디스크 여유 확인
df -h

## 비밀번호 없이 db접속

sudo mysql

만약 안되면 아래처럼 해서 비밀번호 없이 로그인
sudo systemctl stop mysql
sudo mysqld_safe --skip-grant-tables &
sudo mysql

## root계정 비밀번호 초기화

```sql
use mysql;
update user set password=password('비밀번호') where user='root';
FLASH PRIVILEGES;

// 아래는 안해도 되긴 함
update user set plugin='mysql_native_password' where user='root';
FLASH PRIVILEGES;
```

exit 후 root계정 접속

```bash
mysql -u root -p
```

다른 서버에서 db접근이 가능하게 하려면 설정파일을 변경해줘야함

/etc/mysql/mariadb.conf.d/50-server.cnf
파일 (or /etc/mysql/mysql.conf.d/mysqld.cnf 파일 or /etc/mysql/my.cnf 파일?)에서

1. 아래 내용을 주석 하기
bind-address	= 127.0.0.1

2. DB 서비스 재시작
sudo service mysql restart

## MariaDB 삭제 방법

MariaDB 테이블 확인

MariaDB 서버 중지
sudo systemctl stop mariadb

락 해제
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/lib/dpkg/lock

프로세스 실행 확인 및 종료
ps aux | grep mysql
sudo kill 프로세스ID

MariaDB 완전히 제거
sudo apt remove --purge mariadb-server mariadb-client mariadb-common

MariaDB 설정 파일과 데이터베이스 디렉토리를 삭제
sudo rm -rf /etc/mysql /var/lib/mysql

패키지 관리자의 자동 설치된 의존성 정리
sudo apt autoremove
sudo apt autoclean


