오픈소스 RESTful 검색 및 분석엔진. 자바로 개발되어있음

테이블과 스키마 대신에 문서 구조로 된 데이터를 사용

#### 엘라스틱서치 vs RDB
	RDB			ElasticSearch
	Database		Index
	Table		Type
	Row			Document
	Column		Field	
	Schema		Mapping

----------------------------------------------------------------------------------------------------

엘라스틱서치는 데이터를 json형태로 저장하고, 검색 성능이 매우 뛰어난 검색엔진
엘라스틱서치는 db가 아님
물론 데이터를 삽삭갱할수있는 특징만 보면 일반적인 RDBMS와 데이터를 JSON형식으로
저장하고 관리한다는것에 NoSQL(MongoDB)과 비슷한 Database풀럇폼이라고 할 순 있으나 엄연히 검색엔진일뿐 DB는 아님

엘라스틱서치는 왜 검색성능이 뛰어날까?
데이터를 조회하고 삽입하는 등의 그러한 액션은 일반적인 DB와 다른점은 없어보이지만 조회(검색)에 특화시킨 알고리즘(엔진)을 활용해 검색을 함 (루씬 알고리즘)

먼 과거에는 엘라스틱서치 플랫폼 명칭이 루씬이였음

엘라스틱서치는 자바언어로 개발된 오픈소스이며 깃허브에 보면 엘라스틱서치가 있음

데이터를 효율적으로 수집/저장/조회하고 관리할 수 있는 아키텍쳐를 만들어야함


조회를 하려면 kibana의 Elasticsearch QueryDSL로 해야함
{
	clientid: 106.251.
}


엘라스틱서치를 안쓰는곳이 없음(네이버 추천검색어 등)


엘라스틱서치는 json기반으로 select/insert/update/delete 를 함

문법중 from/size 는 limit


일반적으로 엘라스틱서치만 독립적으로 사용하는경우는 없음
항상 같이 사용하는 플랫폼들이 있음
ELK Stack (Elasticsearch + Logstash + Kibana)
	Elasticsearch : 검색엔진이자 저장소
	Logstash : 로그 파이프라인(데이터 전처리, 필터, 가공) 데이터를 잘라서 변화시키는 등. 가공해서 엘라스틱서치에 보내줌
	Kibana : 엘라스틱서치에 저장된 데이터를 조금더 보기 편하게 시각화해주는 인터페이스 (DBeaver, DataGrip) 엘라스틱서치랑 데이터를 왔다갔다
		키바나 없이 쓰면 es.visitkorea.or.kr/_nodes 쌩 JSON이나 텍스트로나옴
		차트도 키바나를 쓰면 차트라이브러리를 쓰지 않고도 쉽게 만들 수 있음
	Filebeat(옵션) : 시스템에서 파일 시스템을 추적하는 에이전트
		로그파일 내용이 변경될때 변경된 내용을 Kafka에 보내주는 감지기
	Kafka(옵션) : 메시지큐(Message Queue)
		대용량 처리할때 많이 씀. FIFO를 활용한 메세지 영속성이 보장됨. 지워도 n일동안 보관됨
		Logstash에 보내줌 (파이프라인)


위의 것들만 있는 서버가 따로 있음
서버명은 'LOG_MAN(로그메인)' 서버


일반적으로 엘라스티서치를 실제 운영되는 서비스에서 사용하는경우 단일 노드로 운영하는경우가 잘 없음
	클러스터(군집, 무리)
	노드(클러스터보다 작은 단위)
"묶는 단위" 라고 생각
빅데이터 플랫폼(엘라스틱서치, 하둡, 스파크)들은 클러스터라는 개념과 노드라는 개념을 공통적으로 씀
여러개의 클러스터 또는 노드로 분산시스템으로 구성함

분산 시스템은 Master(Main) ↔︎ Slave(Sub)
마스터 노드, 슬레이브 노드
분산 클러스터링 또는 분산 노드로 구성할때 홀수개의 단위로 분산시킨다(1.3.5.7..)
스플릿 브레인 : 여러대의 노드가 통신을 이루어 클러스터링중 통신이 끊기거나 특정 노드가 죽는경우가 있을때
	만약 마스터가 죽거나 마스터와 연결되어있던 다수의 슬레이브가 마스터를 잃었을때 그중에서 마스터를 선출(투표)해야 함
	이때 짝수일경우 곤란함(2:2 이렇게 투표결과가 동일하게 나오는걸 방지 하기 위함)

uniess / uniess1208!

----------------------------------------------------------------------------------------------------

로컬에서 실행(웹에서 다운받은경우)

~/elasticsearch-8.10.2/bin/elasticsearch


실행 후 웹에서 localhost:9200 으로 들어가면 사용자이름/비밀번호를 입력하는 얼럿이 뜨는데
비밀번호 초기화 하는 법
엘라스틱 실행시킨 후 터미널 새탭열고 아래 명령어 입력하면 새 비밀번호를 설정할 수 있음
~/elasticsearch-8.10.2/bin/elasticsearch-reset-password -u elastic -i

----------------------------------------------------------------------------------------------------

삽입(PUT)

도큐먼트(행) 추가
PUT /인덱스명/_doc/1
{
	"movieCd" : "123",
	"movieNm" : "반지의 제왕3 왕의 귀환.",
	"movieNmEn": "The Lord Of The Rings: The Return Of The King",
	"prdtYear" : "2003",
	"repNationNm" : "뉴질랜드",
	"regGenreNm" : "판타지" 
}

기존에 있던 데이터가 덮이지 않게 하려면 _doc 대신 _create 를 쓰기
그럼 기존에 데이터가 있을경우
"type": "version_conflict_engine_exception" 가 리턴됨

------------------------------

조회(GET)

도큐먼트(행) 조회
GET /인덱스명/_doc/1

삭제된 도큐먼트를 조회하려고 할 시
"status" : 404 가 리턴됨

-----

모든 인덱스 조회

GET _cat/indices

-----

찾기

GET 인덱스명/_search?q=검색할value

결과를 보면 hits.total 부분에 검색 결과 전체에 해당되는 문서의 개수("value": n)가 표시되고 (이때 "relation":"eq"는 개수가 정확히 일치한다는 뜻)
다시 그 안의 hits:[ ] 구문 안에 배열로 가장 정확도가 높은 문서 10개가 나타남
이 정확도를 relevancy(렐러번시 라고 읽습니다) 라고 함

-----

특정 필드의 값 조회

GET 인덱스명/_search?q=검색할필드:검색할값

-----

AND / OR / NOT 조건 넣을 수 있음 (반드시 대문자로 입력해야함)
GET 인덱스명/_search?q=검색할value AND 검색할value2

-----

_search시 와일드카드 사용 가능

*단어*

-----

모든 인덱스의 디렉토리 조회 (10개만 조회되는듯)

GET _search
{
  "query": {
    "match_all": {
         
    }
  }
}

-----

quick, dog 중 단어 하나라도 들어가 있으면 검색되도록 한다.
디폴트는 OR 이지만 operator를 통해 AND로 설정할 수 있다.

GET my_index/_search
{
  "query": {
    "match": {
      "message": {
        "query": "quick dog",
        "operator": "and"
      }
    }
  }
}

-----

match_phrase
GET my_index/_search
{
  "query": {
    "match_phrase": {
      "message": "lazy dog"
    }
  }
}
정확히 일치하는 내용 검색, 입력된 검색어를 순서까지 고려

GET my_index/_search
{
  "query": {
    "match_phrase": {
      "message": {
        "query": "lazy dog",
        "slop": 1
      }
    }
  }
}
slop 옵션을 이용해 단어 사이에 검색어가 끼어드는 것을 허용한다.
하지만 slop이 클 수록 연관도가 낮아지므로 1이상은 사용하지 않는 것을 권장한다

-----

멀티테넌시(Multitanancy)

여러개의 인덱스를 한꺼번에 검색 가능

쉼표로 나열해서 여러 인덱스 검색 가능
GET 인덱스명1,인덱스명2/_search

와일드카드 * 를 이용해서 여러 인덱스 검색
GET 인덱스명일부*/_search

-----

인덱스명 대신 _all 지정자를 사용하여 GET _all/_search 와 같이 실행하면 클러스터에 있는 모든 인덱스를 대상으로 검색이 가능함
하지만 _all은 시스템 사용을 위한 인덱스 같은 곳의 데이터까지 접근하여 불필요한 작업 부하를 초래하므로 _all 은 되도록 사용하지 않도록 해야함

------------------------------

수정(POST)

기존 도큐먼트의 URL에 변경될 내용의 도큐먼트 내용을 다시 PUT 하는것으로 대치가 가능함.
하지만 필드가 여럿 있는 도큐먼트에서 필드 하나만 바꾸기 위해 전체 도큐먼트 내용을 매번 다시 입력하는 것은 번거로운 작업인데,
이때는 POST 인덱스명/_update/도큐먼트id 명령을 이용해 원하는 필드의 내용만 업데이트가 가능함. 업데이트 할 내용에 doc 라는 지정자를 사용

ex) _update API를 이용해서 my_index/_doc/1 도큐먼트(행)의 "name" 필드(열) 값을 "asd" 로 업데이트
POST my_index/_update/1
{
	"doc": {
		"name": "asd"
	}
}

-----

추가시 랜덤 _id 생성되게 하는법

POST 인덱스명/_doc
{
	"name":"Jongmin Kim",
	"message":"안녕하세요 Elasticsearch"
}

POST 메서드는 PUT 메서드와 유사하게 데이터 입력에 사용이 가능함
도큐먼트를 입력할 때 POST 메서드로 인덱스명/_doc 까지만 입력하면
자동으로 임의의 도큐먼트id("_id") 가 89GJnYQB317z_qbBBGiL 이런식으로 생성됨
도큐먼트id의 자동 생성은 PUT 메서드로는 동작하지 않음

------------------------------

삭제(DELETE)

도큐먼트(행) 삭제
DELETE /인덱스명/_doc/1

인덱스(테이블) 전체삭제
DELETE /인덱스명/

----------------------------------------------------------------------------------------------------

벌크 API (_bulk)

여러 명령을 배치로 수행하기 위해서 _bulk API의 사용이 가능함
_bulk API로 index, create, update, delete의 동작이 가능하며 

POST _bulk
{"index":{"_index":"test","_id":"1"}}	// "test"인덱스의 _id:"1" 에
{"key1":"value one"}				// 내용 삽입
{"index":{"_index":"test","_id":"2"}}	// "test"인덱스의 _id:"2" 에
{"key1":"value two"}				// 내용 삽입
{"delete":{"_index":"test","_id":"2"}}	// "test"인덱스의 _id:"2" 제거
{"create":{"_index":"test","_id":"3"}}	// "test"인덱스의 _id:"3"이 없을경우
{"key1":"value three"}				// 내용 추가
{"update":{"_index":"test","_id":"1"}}	// "test"인덱스의 _id:"1" 의
{"doc":{"field":"value oneone"}}		// 내용 변경

----------------------------------------------------------------------------------------------------

조회시

curl로 해도 되고

포스트맨 툴 써도 되고

자바 등에서 http 요청해도 됨


curl -XGET 'https://elk.visitkorea.or.kr/logstash-visitkorea_access_log*/_search' -u uniess:uniess1208!

또는

curl -XGET 'http://elk.visitkorea.or.kr/_search' -u develop:uniess1208 -H 'Content-Type:application/json' -d '{"query":{"match_all":{}}}'

----------------------------------------------------------------------------------------------------































