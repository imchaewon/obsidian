도커(Docker) : Immutable Infrastructure Paradigm 이라는 개념을 기반으로 한
서비스 환경(서비스 인프라) 부분을 이미지화(실행파일화)하여 배포한 뒤 가급적 변경하지 않고 사용하는것

도커 이미지 : 도커에서 서비스 운영에 필요한 서버 프로그램, 소스코드 및 라이브러리, 컴파일뙨 실행파일을 묶는 형태.
	다시말해, 특정프로세스를 실행하기 위한(즉,컨테이너 생성(실행)에 필요한) 모든 파일과 설정값(환경)을
	지닌 것으로, 더이상의 의존성 파일을 컴파일하거나 이것저것 설치 할 필요 없는 상태의 파일을 의의함
	예를들어 Ubuntu이미지는 Ubuntu를 실행하기 위한 모-든 파읾을 가지고 있으며, Oracle 이미지는 Oracle을
1) 따라서 도커 이미지의 용량은 보통 수백MB ~ 수 GB가 넘음. 하지만 가상머신의 이미지에 비하면 굉장히 적은 용량임
2) 이미지는 상태값을 가지지 않고, 변하지 않음(Immutable)
3) 하나의 이미지는 여러 컨테이너를 생성할 수 있고, 컨테이너가 삭제되도 이미지는 변하지 않고 그대로 남아있음.
4) 도커 이미지들은 github와 유사한 서비스인 DockerHub를 통해 버전관리 및 배포(push&pull)가 가능함
5) 다양한 API가 제공되어 원하는 만큼 자동화가 가능
6) 도커는 Dockerfile이라는 파일로 이미지를 만듦. Dockerfile는 소스와 함께 의존성 패키지 등 사용했던
	설정 파일을 버쩐관리하기 쉽도록 명시되어짐(그래서 누구나 이미지 생성과정을 확인할 수 있으며 수정도 가능함)

이미지와 레이어 : 기존 이미지에 추가적인 파일이 필요할때 다시 다운로드받는 방법이 아닌 해당 파일을 추가하기 위한 개념.
	이미지는 여러 개의 읽기 전용(read only) layer로 구성되고, 파일이 추가되면 새로운 layer가 생성됨.
	그리고 도커는 여러개의 layer를 묶어서 하나의 파일시스템으로 쓸수있게 해줌. 그래서 이미지와 레이어는
	같은 의미로도 사용됨. 추가적으로 DockerHub및 개인저장소에서 이미지를 공유할때는
	바뀐부분(layer = image)만 주고받기 가능하다

도커 컨테이너 : 이미지를 실행한 상태.
	응용프로그램의 종속성과 함께 응용프로그램 자체를 패키징 or 캡슐화하여 격리된 공간에서
	프로세스를 동작시키는 기술
1) 컨테이너는 이미지 layer에 읽기/쓰기(read-write) layer를 추가하는 것으로 생성/실행됨. 따라서 여러개의 컨테이너를
	생성해도 최소한의 용량만 사용되며, 바뀐 부분을 읽기/쓰기 layer에 적음
2) 컨테이너는 종료되었다고 메모리에서 삭제되지않고 남아있음. 삭제하려면 명시적으로 삭제해야함.
	즉, 종료가 되어도 컨테이너 & 읽기/쓰기 layer또한 그대로 존재하기 때문에 다시 시작할 수 있음.
3) 컨테이너를 삭제했다는 것은 컨테이너에서 생성한 파일이 사라진다는것.
	ex) DBMS라면 그동안 쌓였던 DB사용자를 포함한 모든 데이터가 사라진다는 뜻과 동일.
4) 한 서버는 여러개의 컨테이너를 가져도 당연히 상관없으며, 컨테이너는 각각 독립적으로 실행됨
5) 컨테이너는 커널공간과 호스트OS자원(시스템 콜)을 공유함

----------------------------------------------------------------------------------------------------

도커로 마리아db 설치하는 방법

docker search [이미지명] : 이미지 검색
이름 | 설명 | 추천 | 공식 이미지인지

docker images : 가진 이미지 확인
docker pull [이미지명 or ID] : 이미지 다운
docker run [이미지명 or ID] : 이미지 실행
docker run -p 3306:3306 -e MARIADB_ROOT_PASSWORD=root d462573d8688 : 마리아DB
docker run -d -p 3306:3306 -e MARIADB_ROOT_PASSWORD='root!@#$' -v ./data/mariadb:/var/lib/mariadb --name mariadb mariadb : 마리아DB
	이때 d옵션은 백그라운드에서 실행하라는뜻(이 옵션 안넣으면 해당 터미널을 종료하면 컨테이너도 종료됨)
docker run -d -p 8088:8088 -p 1521:1521 jaspeen/oracle-xe-11g : 오라클
docker rmi [이미지id] : 이미지 삭제
docker rmi -f [이미지id] : 이미지 삭제하고 이미지로생성한 컨테이너도 삭제 (이것도 컨테이너 실행중지는 먼저 시킨후 해야함)


docker ps : 도커의 컨테이너 실행상태 확인
docker ps -a,
docker ps --all : 도커의 모든 컨테이너 목록(정지된 컨테이너 포함) 확인

docker stop [컨테이너ID or name] : 도커의 현재 실행중인 모든 컨테이너 종료
docker kill [컨테이너ID or name] : 도커의 현재 실행중인 모든 컨테이너 강제종료 (빠름)

docker start [컨테이너ID or name],
docker restart [컨테이너ID or name] : 도커의 컨테이너 재실행

docker rm [컨테이너ID or name] : 도커의 종료된 컨테이너 삭제 (DBMS컨테이너를 지울경우 안에있는 데이터도 다 날라감)
DB를 내컴퓨터로 옮기고싶으면 여기 참고 : https://dololak.tistory.com/402 (docker run -v명령어로 하는듯?)

docker inspect [컨테이너ID or name] : 도커의 이미지 정보 출력 (사용자비번도 나와있음 ex)"MARIADB_ROOT_PASSWORD=root!@#$",)

docker exec -it [컨테이너ID or name] bash : 컨테이너에 접속

-----

도커 에러 : Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
docker service가 실행이 안되어있을때 발생

cmd+space → docker 실행하면 화면 맨위에 고래가 생긴걸 볼수있음

-----

도커로 설치한 DB의 사용자계정은 컨테이너를 중지시키면 다 날라감(create/insert한 테이블 등도)

----------------------------------------------------------------------------------------------------

아래와 같은 오류가 날 경우

Access denied for user 's'@'172.17.0.1' (using password: YES)

1. 컨테이너 접속
docker exec -it <CONTAINER_ID>  mysql -uroot -p

2. 디렉터리 이동
cd /var/lib/mysql

3. mysql실행
mysql -u root -p

4. CREATE USER '사용자명'@'172.17.0.1' IDENTIFIED BY '비밀번호';

5. 권한부여
GRANT ALL PRIVILEGES ON *.* TO '사용자명'@'172.17.0.1' WITH GRANT OPTION;

6. 저장
flush privileges;

----------------------------------------------------------------------------------------------------

도커로 마리아DB 등 DB를 설치할때 내 로컬에서 사용자/테이블 등 데이터를 가져오는 방법

방법
pull해온 이미지를 한번 실행시키고, 하드에 저장된 data폴더를 복사해서 아무데나 빼놓고
컨테이너를 삭제하고 다시 실행시킬때 데이터가 저장되는 폴더를 빼놓은 폴더로 지정한다

1. 먼저 모든 DB관련 데이터가 저장될 폴더를 로컬에 생성한다 ex) ~/data/mariadb
mkdir data
cd data

2. pull해온 이미지를 가상의 운영체제로 실행할때 DB데이터를 로컬과 연결시킨다
docker run -d -p 3306:3306 -e MARIADB_ROOT_PASSWORD='root!@#$' -v ./data/mariadb:/var/lib/mariadb --name mariadb mariadb

3. 로그한번 찍어보기
docker logs [컨테이너ID일부]

3. 아래 명령어로 도커 가상 운영체제에 접근할 수 있다
docker exec -it mariadb bash

4. 가상운영체제에서 mariadb 프로세스가 실행되고있는거 확인
ps -ef |grep mariadb

5. 가상운영체제에서 다음 경로로 이동
cd /var/lib/mysql

6. 해당경로에서 sql문 입력할 수 있는 명령어 입력
mysql -u root -p

참고. 비밀번호 까먹었을때는 도커 INSPECT 들어가보면 비밀번호가 나와있음

참고. sql파일 불러와서실행하는 명령어
mysql -u root -p --default-character-set=utf8 [사용자명] < [sql파일명.sql]

7. DB 생성
create database KTO;

8. sql문 입력 나가기
exit

9. KTO라는 폴더가(사용자가) 만들어졌는지 확인
ll

10. 디비버에서 해당 사용자로 test테이블 하나 생성

11. 가상운영체제 나가기
exit

12. 컨테이너 상태 확인
docker inspect maria

13. 컨테이너 중지
docker stop mariadb

14. 컨테이너 삭제
docker rm mariadb

15. 로컬 아무곳에 컨테이너를 실행시키는 쉘스크립트(.sh) 생성 (ex.홈디렉토리)
vi mariadb_run.sh

내용: docker run -d -p 3306:3306 -e MARIADB_ROOT_PASSWORD='root!@#$' -v ~/data/mariadb:/var/lib/mysql --name mariadb mariadb


16. 생성한 쉘스크립트파일에 실행권한 부여
chmod 755 mariadb_run.sh

ll찍어보면 파일 색깔 주황색으로 바뀌어있음


17. 쉘스크립트파일 실행
./mariadb_run.sh

18. 디비버 들어가서 계정/테이블이 안사라진것을 확인

----------------------------------------------------------------------------------------------------