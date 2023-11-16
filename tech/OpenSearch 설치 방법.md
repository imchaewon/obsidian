도커 먼저 설치
[[Docker 설치 방법]]

도커 이미지 검색
docker search 이미지명

도커 풀
docker pull opensearchproject/opensearch:1.0.1

도커 이미지 확인
docker images

도커 이미지 실행
docker run -p 9200:9200 -p 9600:9600 -e "discovery.type=single-node" opensearchproject/opensearch:1.0.1

실행중인 도커 컨테이너 확인
docker ps

전체 도커 컨테이너 확인
docker ps -a

컨테이너 실행
docker start 컨테이너ID

도커 로그 확인
docker logs [컨테이너 ID 또는 이름]




