카프카는 송신자와 수신자 간의 효율적인 메시지 교환을 지원하는 메시지브로커임 (Apache Kafka, RebbitMQ, Apache ActiveMQ 등이 있음)


스트리밍 데이터 : 실시간으로 생성되고 처리 및 전송되는 데이터. 배치 처리와는 다르게 지연 없이 처리되며, 데이터의 실시간 특성을 강조함


메시지 브로커 종류
Kafka : 로그 기반 스트리밍 중심. 로그기반 데이터 파이프라인, 스트리밍 처리 및 이벤트 기반 애플리케이션에 사용됨
RabbitMQ : 대기열 중심. 비동기 메시지 전달 및 이벤트 기반 아키텍처 구현에 사용됨
Redis : 인메모리 및 Pub/Sub을 중심으로 동작. 캐싱, 세션 관리, 실시간 알림 및 메시지 기반 통신에 사용됨

이벤트 브로커 종류
Kafka : 메시지를 처리하고 저장하기 위한 메시지 브로커이자, 실시간 이벤트 스트림을 관리하고 분배하는 이벤트 브로커 역할도 수행함
AWS Kinesis : 이벤트스트림을 효율적으로 관리하고, 이벤트를 발행하고 구축하는데 씀. 실시간 스트리밍 및 이벤트 기반 아키텍처를 구축하는데 매우 적합함


소스 애플리케이션 : 데이터의 원천 또는 발생 지점. 데이터를 생성하거나 수집하는 애플리케이션. DB, 로그파일등에서 데이터를 가져올 수 있음
타겟 애플리케이션 : 데이터의 목적지 또는 도착 지점. 데이터를 수신하고 저장하는 애플리케이션. 소스 애플리케이션에서 추출한 데이터를 타겟애플리케이션으로 가져와 처리하거나 저장함

카프카는 소스 애플리케이션과 타겟 애플리케이션을 약하게 하기 위해서 사용함

기존에 아래처럼 데이터가 전송되었다면
소스 애플리케이션 → 타켓 애플리케이션

카프카를 사용하면 아래처럼 데이터가 흐름
소스 애플리케이션 → 카프카 → 타겟 애플리케이션

소스 애플리케이션 : 카프카에 데이터(클릭로그,결제로그) 등을 보냄
타겟 애플리케이션 : 카프카에서 데이터를 가져와서 로그 적재, 로그 처리등의 역할을 함


클러스터(cluster) : 여러대의 서버로 구성된 분산 데이터플랫폼. 클러스터에는 데이터를 수신, 저장, 전송하는 역할을 하는 여러개의 브로커가 포함됨
브로커(broker) : 클러스터내에서 개별적으로 동작하는 서버노드(클러스터안에 있는 개별서버). 데이터를 수신, 저장, 전송함
	데이터를 안정적으로 처리하고 병렬로 분산 저장하기 위해 클러스터 형태로 구성돼있음
	생산자가 보낸 메시지를 구독자에게 전달하는 역할도 함(토픽/파티션 기반)
토픽(topic, 주제) : 클러스터 내에서 데이터의 주제나 카테고리를 나타냄. 하나 이상의 파티션으로 나뉨. kafka에 메시지를 게시하거나 가져오려는 구독자들 사이에서 데이터를 분류할때 씀
파티션 : 토픽을 쪼개놓은것. 각 파티션은 리더와 여러개의 팔로워(복제본)을 가질수 있음. 각 브로커는 자신이 담당하는 파티션을 관리함

프로듀서(producer, 송신자, 생산자) : 데이터를 Kafka 클러스터로 보내는 역할을 함. Producer는 메시지를 토픽에 게시함
	토픽에 저장된 데이터가 있을 때, 메시지 브로커는 해당 데이터를 → 구독한 컨슈머에게 전달함
컨슈머(consumer, 수신자, 소비자) : Producer가 보낸 데이터를 읽어오는 역할. Consumer는 토픽의 파티션으로부터 데이터를 구독함
주피커(zooKeeper) : Kafka 클러스터의 구성, 조정 및 관리를 담당함. 최근 버전의 Kafka에서는 ZooKeeper를 사용하지 않는 옵션도 제공됨

소스 애플리케이션에서 보낼 수 있는 데이터포맷은 거의 제약이 없음(java, tsv, avro 등 여러 포맷 지원)

카프카는 각종 데이터를 담는 토픽(큐)가 있음
토픽(큐)에 데이터를 넣는 역할은 프로듀서가 하고, 토픽(큐)에서 데이터를 가져가는 역할은 컨슈머가 함

프로듀서&컨슈머는 라이브러리로 되어있어서 애플리케이션에서 구현가능함


카프카에서는 토픽을 여러개 생성할 수 있음
프로듀서가 토픽에 데이터를 넣어놓으면 컨슈머가 가져감

토픽의 이름을 지을때는 목적에 따라 click_log, send_sms, location_log 등과 같이 무슨 데이터를 담는지 명확하게 명시하는게 좋음


토픽 내부

하나의 토픽은 여러개의 파티션으로 구성될 수 있으며 첫번재 파티션 번호는 0번지부터 시작함
하나의 파티션은 큐와 같이 내부에 데이터가 파티션 끝에서부터 차곡차곡 쌓이게 됨

토픽에 컨슈머가 붙으면 데이터를 가장 오래된 순서대로 가져가고
더이상 데이터가 들어오지않으면 컨슈머는 또 다른 데이터가 들어올 때까지 기다림

컨슈머가 토픽 내부의 파티션에서 데이터를 이용하더라도 데이터는 삭제되지 않고 파티션에 그대로 남아있음

새로운 컨슈머가 들어왔을때 0번부터 이용할 수 있음
★단, 컨슈머 그룹이 달라야 하고 auto.offset.reset = earliest로 되어있어야함
이렇게 하면 동일 데이터를 여러번 처리할 수 있는데, 이는 카프카를 사용하는 아주 중요한 이유이기도 함

클릭로그등을 분석하고 시각화하기 위해 엘라스틱서치에 저장하기도 하고, 클릭로그등을 백업하기 위해 하둡에 저장을 할 수도 있음


파티션이 2개 이상인 경우

								click_log 토픽
	    				ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ					
					ㅣ			ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ	ㅣ
 Producer				ㅣ	파티션 #0 ㅣ			| 6 | 5 | 4 | 3 | 2 | 1 | 0ㅣ	ㅣ			Consumer
       ||	   →→→→→	ㅣ			ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ	ㅣ →→→→→		||
   Source				ㅣ			ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ	ㅣ			    Target
Application			ㅣ	파티션 #1 ㅣ						    ㅣ7ㅣ	ㅣ			Application
					ㅣ			ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ	ㅣ
					ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

1. 키가 null이고, 기본 파티셔너 사용할 경우 : 라운드 로빈(Round robin)으로 할당됨
2. 키가 있고, 기본 파티셔너 사용할 경우 : 키의 해시(hash)값을 구하고, 특정 파티션에 할당됨


파티션을 늘리면 좋은점
메시지 스트림라인이 여러 파티션으로 분산되므로, 여러 컨슈머가 동시에 메시지를 처리할 수 있음

★파티션을 늘리는것은 조심해야함
한번 늘린 파티션은 다시 줄일 수 없기때문

비유하면 파티션은 고속도로의 톨게이트라고 볼수있음
파티션이 없다면 마치 1차로 도로를 달리는 것과 같고, 파티션을 늘릴수록 n차선 도로를 달리는 것과 같음

하나의 파티션은 큐처럼 내부에 데이터가 파티션 끝에서부터 차곡차곡 쌓임

------------------------------

파티션의 데이터가 삭제되는 타이밍

레코드가 저장되는 최대 시간과 크기를 지정하는 옵션이 있음
일정한 기간 혹은 용량 범위내에서 데이터를 저장할 수 있으며, 적절하게 데이터가 삭제될 수 있도록 설정할 수 있음

log.retention.ms : 최대 record 보존 시간
log.retention.byte : 최대 record 보존 크기(byte)

----------------------------------------------------------------------------------------------------

브로커(broker)

카프카가 설치되어있는 서버 단위

보통 3개 이상의 브로커로 구성해 사용하는것을 권장

만약 레플리케이션이 1인 토픽이 존재하고, 브로커가 3대라면 브로커 3대중 1대에 해당 토픽의 정보(데이터)가 저장됨

------------------------------

레플리케이션(replication, 복제)

파티션의 복제를 의미

레플리케이션이 1이라면 파티션은 1개만 존재한다는 뜻

레플리케이션이 2라면 파티션은 원본1개와 복제본 1개로 총 2개가 존재하게 됨  

리플리케이션이 브로커의 개수를 초과할 수는 없음. (브로커개수가 3이면 리플리케이션은 4가 될 수 없음)

원본 1개의 파티션은 리더 파티션 이라고 부르고, 나머지 복제본들은 팔로워 파티션이라고 부름

이 리더와 팔로워를 합쳐서 ISR(In Sync Replica)이라고 부름

레플리케이션은 파티션의 고가용성을 위해 사용함
만약 레플리케이션이 1이라면 브로커가 어떤 이유로 인해 사용불가하게 된다면 해당파티션은 복구할 수가 없음
만약 레플리케이션이 2라면 브로커 1개가 죽더라도 복제본(팔로워 파티션)이 존재하므로 복제본으로 복구가 가능함. 팔로워파티션이 리더파티션 역할을 승계하게 됨

래플리케이션개수가 많아지면 그만큼 브로커의 리소스 사용량도 늘어나게 됨
3개이상의 브로커를 사용할때 래플리케이션은 3으로 설정하는것이 좋다고 함

----------------------------------------------------------------------------------------------------

리더파티션과 팔로워파티션의 역할

프로듀서가 토픽의 파티션에 데이터를 보내면, 그걸 받는 것이 리더파티션임

프로듀서는 ack라는 상세 옵션이 있음
ack를 통해 고가용성을 유지할 수 있는데
이 옵션은 파티션의 래플리케이션과 관련이 있음

ack는 0, 1, all 옵션 3개중 1개를 골라서 사용할 수 있음

0
프로듀서는 리더파티션에 데이터를 전송하고 응답값을 받지 않음
리더파티션에 데이터가 정상적으로 전송됐는지, 그리고 나머지 파티션에 정상적으로 복제되었는지 일수없음. 속도는 빠르지만 데이터 유실가능성 있음

1
리더파티션에 데이터를 전송하고, 리더파티션이 정상적으로 값을 받았는지 응답값을 받음
다만 나머지 파티션에 복제되었는지는 알 수 없음. 만약 리더파티션이 데이터를 받은 즉시 브로커가 장애가 난다면
나머지 파티션에 데이터가 미처 전송되지 못한 상태이므로 이전의 ack0과 마찬가지로 데이터유실가능성이 있음

all
1옵션에 추가로 팔로워파티션에 복제가 잘 이루어졌는지 응답값을 받음
리더파티션에 데이터를 보낸 후 나머지 팔로워파티션에도 데이터가 저장되는것을 확인하는 절차를 거침

ack all 옵션을 사용할경우 데이터 유실은 없다고 보면 됨
하지만 0, 1 에 비해 확인할게 많기때문에 속도가 현저히 느라다는 단점이 있음

----------------------------------------------------------------------------------------------------

파티셔너

데이터를 토픽의 어떤 파티션에 넣을지 결정하는 역할

프로듀서가 데이터를 보내면 무조건 파티셔너를 통해서 브로커로 데이터가 전송됨
레코드에 포함된 메시지 키 또는 메시지 값에 따라서 파티션의 위치가 결정됨

프로듀서를 사용할때 파티셔너를 따로 설정하지 않으면 UniformStickyPartitioner로 설정이 됨
이 파티셔너는 메시지 키가 있을 때와 없을 때 다르게 동작함


<메시지 키가 있는 경우>
메시지 키를 가진 레코드는 파티셔너에 의해서 특정한 해시값이 생성됨
이 해시값을 기준으로 어느 파티션에 들어갈지 정해지게 됨

 동일한 메시지 키를 가진 레코드는 동일한 해시값을 만들기 때문에 항상 동일한 파티션에 들어가는걸 보장함 (순서를 지켜서 데이터를 처리할 수 있다는 장점이 있음)


<메시지 키가 없는 경우>
라운드로빈방식으로 들어감. 전통적인 라운드로빈방식과는 조금 다르게 동작하는데,
UniformStickyPartitioner는 프로듀서에서 배치로 모을 수 있는 최대한의 레코드들을 모아서 파티션으로 데이터를 보냄
이때 라운드 로빈방식으로 돌아가며 데이터를 넣음. 메시지 키가 없는 레코드들은 파티션에 적절히 분배됨

----------------------------------------------------------------------------------------------------

컨슈머 렉(Lag)

카프카 프로듀서는 토픽의 파티션에 데이터를 차곡차곡 넣는데
이 파티션에 데이터가 하나하나씩 들어가게 되면 각 데이터는 오프셋이라고 하는 숫자가 붙음

만약 파티션이 1개인 토픽에 프로듀서가 데이터를 넣을 경우를 가정해본다

기본적으로 데이터는 0부터 차례대로 오프셋이 매겨지게 되는데
프로듀서는 계속해서 데이터를 넣게되고, 컨슈머는 계속해서 데이터를 가져감

만약 프로듀서가 데이터를 넣어주는 속도가, 컨슈머가 가져가는 속도보다 빠르다면?
프로듀서가 넣은 데이터의 오프셋, 컨슈머가 가져간 데이터의 오프셋
이 2개의 오프셋 간에 차이가 발생함
이게 바로 컨슈머 렉(Lag)임

렉은 적을수도 있고 많을 수도 있음

이 렉의 숫자를 통해 현재 해당 토픽에 대해 파이프라인으로 연계되어있는 프로듀서와 컨슈머의 상태에 대해 유추가 가능함. 주로 컨슈머의 상태를 확인하고싶을때 사용

카프카 컨슈머 렉 = 프로듀서가 마지막으로 넣은 오프셋 - 컨슈머가 마지막으로 읽은 오프셋

토픽에 여러 파티션이 존재할 경우, 렉은 여러개가 존재할 수 있음
만약 컨슈머그룹이 1개이고 파티션이 2개인 토픽에서 데이터를 가져간다면 렉은 2개가 측정될 수 있음
이렇게 1개의 토픽과 컨슈머그룹에 대한 렉이 여러개 존재할 수 있을때, 그중 높은 숫자의 렉을 records-lag-max 라고 부름

----------------------------------------------------------------------------------------------------

발행-구독(Publisher-Subscriber, Pub/Sub) 패턴

전송자와 수신자를 분리하는 다대다 비동기식 메시지 서비스
MSA(마이크로서비스)를 위한 서비스라고 생각하면 됨

프로듀서를 퍼블리셔. 컨슈머를 서브스크라이버 라고 명명함

퍼블리셔가 서브스크라이버 에게 직접 메시지를 보내고 받는 것이 아닌, 브로커를 통해 전달함
퍼블리셔는 누가 수신하는지는 알 수 없음 (컨슈머의 존재를 알 필요가 없음)

브로커 내의 토픽(Topic) 이라는 카테고리에 등록함
서브스크라이버는 자신이 흥미있는 토픽만을 선택해서 읽을 수 있고, 같은 토픽을 읽는 서브스크라이버들은 동일한 메시지를 받음

----------------------------------------------------------------------------------------------------

Topic 목록 출력

서버로 접속 후 카프카폴더/bin 경로로 들어가서 아래 명렁어 입력

./kafka-topics.sh --bootstrap-server localhost:9092 --list

------------------------------

Topic 정보 출력

서버로 접속 후 카프카폴더/bin 경로로 들어가서 명렁어 입력

./kafka-topics.sh --bootstrap-server localhost:9092 --topic 토픽명--describe

결과는 아래처럼 출력됨
ex1) 새로만든토픽
Topic: test-topic	PartitionCount: 1	ReplicationFactor: 1	Configs: retention.ms=10000
	Topic: test-topic	Partition: 0	Leader: 3	Replicas: 3	Isr: 3

ex2) delta-topic
Topic: delta-topic	PartitionCount: 3	ReplicationFactor: 3	Configs: min.insync.replicas=1,cleanup.policy=delete,retention.ms=600000,max.message.bytes=1048588,retention.bytes=-1
	Topic: delta-topic	Partition: 0	Leader: 2	Replicas: 2,1,3	Isr: 1,2,3
	Topic: delta-topic	Partition: 1	Leader: 3	Replicas: 3,2,1	Isr: 1,2,3
	Topic: delta-topic	Partition: 2	Leader: 1	Replicas: 1,3,2	Isr: 1,2,3

ex3) event-pusher
Topic: event-pusher	PartitionCount: 1	ReplicationFactor: 1	Configs: retention.ms=10000
	Topic: event-pusher	Partition: 0	Leader: 2	Replicas: 2	Isr: 2

ex4) rule-command
Topic: rule-command	PartitionCount: 3	ReplicationFactor: 3	Configs: retention.ms=10000
	Topic: rule-command	Partition: 0	Leader: 2	Replicas: 2,1,3	Isr: 1,2,3
	Topic: rule-command	Partition: 1	Leader: 3	Replicas: 3,2,1	Isr: 1,2,3
	Topic: rule-command	Partition: 2	Leader: 1	Replicas: 1,3,2	Isr: 1,2,3

ex5) rule-event
Topic: rule-event	PartitionCount: 1	ReplicationFactor: 1	Configs: retention.ms=10000
	Topic: rule-event	Partition: 0	Leader: 1	Replicas: 1	Isr: 1

ex6) tuba-topic
Topic: tuba-topic	PartitionCount: 3	ReplicationFactor: 3	Configs: min.insync.replicas=1,cleanup.policy=delete,retention.ms=600000,max.message.bytes=1048588,retention.bytes=-1
	Topic: tuba-topic	Partition: 0	Leader: 2	Replicas: 2,1,3	Isr: 1,2,3
	Topic: tuba-topic	Partition: 1	Leader: 3	Replicas: 3,2,1	Isr: 1,2,3
	Topic: tuba-topic	Partition: 2	Leader: 1	Replicas: 1,3,2	Isr: 1,2,3

ex7) vista-to-stream-api-os-data
Topic: vista-to-stream-api-os-data	PartitionCount: 3	ReplicationFactor: 3	Configs: retention.ms=10000
	Topic: vista-to-stream-api-os-data	Partition: 0	Leader: 3	Replicas: 3,2,1	Isr: 1,2,3
	Topic: vista-to-stream-api-os-data	Partition: 1	Leader: 1	Replicas: 1,3,2	Isr: 1,2,3
	Topic: vista-to-stream-api-os-data	Partition: 2	Leader: 2	Replicas: 2,1,3	Isr: 1,2,3

ex8) vista-to-stream-daemon-os-qu 
Topic: vista-to-stream-daemon-os-query	PartitionCount: 3	ReplicationFactor: 3	Configs: retention.ms=10000
	Topic: vista-to-stream-daemon-os-query	Partition: 0	Leader: 1	Replicas: 1,3,2	Isr: 1,2,3
	Topic: vista-to-stream-daemon-os-query	Partition: 1	Leader: 2	Replicas: 2,1,3	Isr: 1,2,3
	Topic: vista-to-stream-daemon-os-query	Partition: 2	Leader: 3	Replicas: 3,2,1	Isr: 1,2,3

------------------------------

Topic 생성

./kafka-topics.sh --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic 토픽명 --create

------------------------------

Topic 삭제

./kafka-topics.sh --bootstrap-server localhost:9092 --topic 토픽명 --delete

----------------------------------------------------------------------------------------------------

참고: kafka의 기본 포트번호는 9092
참고: https://blog.advenoh.pe.kr/cloud/Kafka-CLI-%EB%AA%85%EB%A0%B9%EC%96%B4-%EB%AA%A8%EC%9D%8C/

----------------------------------------------------------------------------------------------------

주키퍼(Zookeeper)

분산 애플리케이션의 관리와 조정을 위한 오픈 소스 분산 코디네이션 서비스

-----

역할

분산 시스템의 동기화
ZooKeeper는 다수의 서버 노드 간의 동기화를 도와줌
분산 시스템에서 여러 서버 간에 일관된 상태를 유지하고 변경 사항을 동기화하기 위해 사용됨

설정 관리
시스템의 구성 설정(configuration)을 중앙에서 관리하고 변경 사항을 분산 노드에 효과적으로 배포할 수 있도록 도와줌
이를 통해 서비스 구성 관리를 단순화하고 일관성을 유지할 수 있음

리더 선출
ZooKeeper는 분산 환경에서 리더 노드를 선출하는데 사용됨
이를 통해 분산 시스템에서 단일 리더가 일관된 결정을 내릴 수 있도록 함

락 관리
분산 락(Distributed Lock)을 구현하는 데 사용됨
여러 클라이언트가 공유 리소스에 대한 엑세스를 조절하려면 락 메커니즘이 필요한데, ZooKeeper는 이를 제공함

분산 시계(Clock) 서비스
ZooKeeper는 각 클라이언트에게 정확한 시간 정보를 제공하여 분산 시간 동기화에 사용됨

이벤트 및 감시
ZooKeeper는 데이터 노드의 변경 사항을 클라이언트에게 알릴 수 있도록 이벤트 및 감시 기능을 제공함
이를 통해 클라이언트는 필요한 경우 실시간으로 데이터 변경을 감지하고 처리할 수 있음

-----

설치

1. 구글에 apache zookeeper 검색하고 사이트 접속

2. Download 클릭

3. 버전 선택

4. HTTP라고 쓰여있는항목의 URL 복사

5. wget 명령어로 주키퍼 다운
wget https://dlcdn.apache.org/zookeeper/zookeeper-3.9.0/apache-zookeeper-3.9.0-bin.tar.gz

6. tar 명령어로 압축 해제
tar -xvaf 파일명

-----

사용

주키퍼 앙상블 구축

앙상블 구축 : 주키퍼 서비스를 고가용성(High Availability) 상태로 만드는것
여러 대의 서버로 구성된 클러스터를 형성해 주키퍼 서비스를 실행하고, 이를 통해 주키퍼의 신뢰성과 가용성을 높히는 것


<AWS EC2로 앙상블구축>

1. 각 원격 서버 접속

2. cd 명령어로 apache-zookeeper-다운받은버전-bin/conf 폴더로 이동
cd ~/apache-zookeeper-3.9.0-bin/conf

3. vi zoo.cfg 로 설정파일 생성 후 내용 입력
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
initLimit=20
syncLimit=5
server.1=test-broker01:2888:3888
server.2=test-broker02:2888:3888
server.3=test-broker03:2888:3888

숫자가 1은 01, 2는 03, 3은 02 이런식으로다른 이유는 서버ID와 서버 이름은 서로 연관되어있지 않다는것을 보여주기 위함임


4. 각 서버들을 ip가 아닌 hostname으로 통신하기 위해 /etc/hosts를 수정
이때 현재 접속해있는 서버가 뭔지 알려면 터미널에 있는 사설ip와 ec2대시보드에 있는 사설ip를 비교하면됨

4-1. 관리자권한으로 파일 열기
sudo vi /etc/hosts

4-2. 각 서버별로 내용 추가
<기존 정보>
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost6 localhost6.localdomain6
<기존 정보 끝>

<서버1에 추가할 정보>
0.0.0.0 test-broker01
두번째서버공개키ip test-broker02
세번째서버공개키ip test-broker03

<서버2에 추가할 정보>
0.0.0.0 test-broker02
첫번째서버공개키ip test-broker01
세번째서버공개키ip test-broker03

<서버3에 추가할 정보>
0.0.0.0 test-broker03
첫번째서버공개키ip test-broker01
두번째서버공개키ip test-broker02

자기거는 0.0.0.0으로 하면됨


5. 주키퍼를 서로 연동하기위해서는 방화벽 설정이 필요함
aws의 보안그룹에서 설정하기
주키퍼는 2181포트, 2888포트, 3888포트, 9092포트 를 쓰므로 3개의 포트에 대해서 anywhere조건으로 open하면됨


6. 자바 다운
sudo yum update
yum list java*
sudo yum install java-11-amazon-corretto.x86_64


7. 주키퍼폴더/conf/zoo.cfg의 dataDir 속성에 적힌 경로에 myid를 만들어서 부여해야함

7-1. 폴더 생성
sudo mkdir /var/lib/zookeeper

7-2. 서버별로 myid 파일 생성
sudo sh -c 'echo 1 > /var/lib/zookeeper/myid'
sudo sh -c 'echo 2 > /var/lib/zookeeper/myid'
sudo sh -c 'echo 3 > /var/lib/zookeeper/myid'


8. 모든 원격 서버에서 주키퍼 실행
sudo ~/apache-zookeeper-3.9.0-bin/bin/zkServer.sh start

실행중인건 아래 명령어로 확인
~/apache-zookeeper-3.9.0-bin/bin/zkServer.sh status


잘 안되는거같으면

start를 디버깅용으로 실행 해보거나
~/apache-zookeeper-3.9.0-bin/bin/zkServer.sh start-foreground

start명령 입력시 생기는 로그 파일 보기
~/apache-zookeeper-3.9.0-bin/log/zookeeper-root-server-ip-172-31-42-59.ap-northeast-2.compute.internal.out


만약 ~/apache-zookeeper-3.9.0-bin/bin/zkServer.sh status 실행시 아래와 같은 오류가 난다면
Error contacting service. It is probably not running.
↓↓↓
현재서버를start를 안했거나 다른 서버의 주키퍼가 모두 꺼져있는것.
zkServer.sh start 명령으로 다른 서버를 하나라도 켜야함

org.apache.zookeeper.server.persistence.FileTxnSnapLog$DatadirException: Cannot write to data directory /var/lib/zookeeper/version-2
↓↓↓
주키퍼가 사용하는 데이터디렉토리에 쓰기 권한 부여
sudo chmod -R 777 /var/lib/zookeeper/version-2

Cannot open channel to 1 at election address test-broker01/54.180.104.155:3888
↓↓↓
호스트에 연결할 수 없음. /ect/hosts파일에 설정돼있는 ip주소가 맞는지 확인(ec2에서 인스턴스를 한번 중지를 했다가 실행하면 ip주소가 바뀜)


잘 되면 각 서버에서 status 실행시 아래처럼 출력됨
Mode: follower
Mode: follower
Mode: leader


9. 로컬PC에서 주키퍼 접속
bin 폴더에서 아래 명렁어 입력
./zkCli.sh -server 퍼블릭ip

방화벽설정이 돼있어야함

그럼 아래처럼 명령어들을 입력할 수 있음
ls /
출력결과 : [zookeeper]
get /
출력결과 : 정보들

----------------------------------------------------------------------------------------------------

kafka 설치 / 클러스터 구성

1. 각 원격서버에 kafka 설치
https://kafka.apache.org/downloads 에서 원하는 버전 다운
wget https://downloads.apache.org/kafka/3.5.1/kafka_2.12-3.5.1.tgz

2. 압축해제
tar -xvaf kafka-3.5.1-src.tgz


3. 카프카 클러스터 구성을 위해 각 브로커별로(서버별로) 카프카 설정이 필요.
vi kafka_2.12-3.5.1/config/server.properties

3-1. 파일내용 중간에 broker.id=0 이라고 돼있는부분을 각 서버별로 다르게 설정하기
broker.id=0
broker.id=1
broker.id=2

3-2. zookeeper.connect 변경
zookeeper.connect=localhost:2181
↓↓↓
zookeeper.connect=test-broker01:2181,test-broker02:2181,test-broker03:2181/test


4. 메모리 늘리기
export KAFKA_HEAP_OPTS="-Xmx512M -Xms512M"

5. 카프카 실행
cd ~/kafka_2.12-3.5.1/bin
./kafka-server-start.sh ../config/server.properties

6. kafka 브로커가 정상적으로 실행중인지 확인
tail -f ~/kafka_2.12-3.5.1/logs/server.log

----------------------------------------------------------------------------------------------------

로컬에서 kafka를 이용해 Kafka Broker(원격 서버)로 메시지 전송

1. 로컬에 kafka 설치
https://kafka.apache.org/downloads 에서 원하는 버전 다운
wget https://downloads.apache.org/kafka/3.5.1/kafka_2.12-3.5.1.tgz

2. 로컬에서 advertised.listebers 설정
cd ~/kafka_2.12-3.5.1/config
vi server.properties
/advertised.listeners 로 찾은 다음 주석 풀고 아래처럼 값을 변경하기
advertised.listeners=PLAINTEXT://54.180.101.137:9092,PLAINTEXT://13.209.48.255:9092,PLAINTEXT://13.209.76.40:9092

3. 로컬에서 토픽 생성
./kafka-topics.sh --create --zookeeper 서버1:9092,서버2:9092,서버3:9092/test --replication-factor 1 --partitions 1 --topic test_log
./kafka-topics.sh --create --bootstrap-server 54.180.104.155:9092,15.164.163.248:9092,54.180.122.109:9092 --replication-factor 1 --partitions 1 --topic test-log

참고로 토픽명은 마침표나 밑줄이 포함되면 안됨


4. 로컬의? 콘솔 컨슈머로 데이터 확인
cd /kafka_2.12-3.5.1/bin

----------------------------------------------------------------------------------------------------

WARN [Producer clientId=console-producer] Bootstrap broker <broker-address> disconnected (org.apache.kafka.clients.NetworkClient)
↓↓↓
오류 메시지는 Kafka Producer가 지정된 브로커와의 연결을 실패하거나 연결이 끊어진 경우에 발생
브로커가 수신 대기중인지 확인

----------------------------------------------------------------------------------------------------




























