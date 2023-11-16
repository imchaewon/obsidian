Ubuntu 기준
sudo apt update
sudo apt install mariadb-server

설치 확인
mariadb --version

디스크 여유 확인
df -h

## sql문 입력창으로 이동
sudo mysql

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


