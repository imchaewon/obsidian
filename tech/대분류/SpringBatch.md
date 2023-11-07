UnsatisfiedDependencyException: Error creating bean with name 'commentSentimentJobConfig' defined in file
springframework.beans.factory.BeanCreationException: Error creating bean with name 'sqlSessionFactory'
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'sqlSessionFactory' defined in class path resource
Caused by: org.apache.ibatis.type.TypeException: The alias 'CoordinateEntity' is already mapped to the value
↓↓↓
application-common.yml 에서 
mybatis:
  type-aliases-package: kr.or.visitkorea.common 뒤에 .entity 추가


Parameter 0 of constructor in kr.or.visitkorea.common.client.ParkingApiClient required a single bean, but 5 were found:
	- purpleBookRestTemplate: defined by method 'restTemplate' in class path resource [kr/or/visitkorea/common/client/PurpleBookApiRestTemplate.class]
	- pythonApiRestTemplate: defined by method 'restTemplate' in class path resource [kr/or/visitkorea/common/client/PythonApiRestTemplateConfig.class]
	- skApiRestTemplate: defined by method 'skApiRestTemplate' in class path resource [kr/or/visitkorea/common/client/SkApiRestTemplateConfig.class]
	- tmapApiRestTemplate: defined by method 'tmapApiRestTemplate' in class path resource [kr/or/visitkorea/common/client/TmapApiRestTemplateConfig.class]
	- tournMasterRestTemplate: defined by method 'restTemplate' in class path resource [kr/or/visitkorea/common/client/TournMasterApiRestTemplate.class]
Action:
Consider marking one of the beans as @Primary, updating the consumer to accept multiple beans, or using @Qualifier to identify the bean that should be consumed
↓↓↓
생성자 주입했는데 클래스명이 겹칠때 발생

-----

Consider defining a bean of type 'kr.or.visitkorea.common.config.properties.ParkingProperties' in your configuration.
↓↓↓
빈등록이 안되어있다는 뜻

메인메소드 있는곳에서 아래 어노테이션에
@EnableConfigurationProperties({
	ParkingProperties.class,
이런식으로 추가

+++
application-common.yml에 아래처럼 추가하고
parking123:
#    base-url: http://api.data.go.kr/openapi/tn_pubr_prkplce_info_api
    base-url: http://api.data.go.kr
    app-key: hcE1K3wHaBBeIpLySxcb9TT0%2FoeX8BlEjpOz2biXGLGl2n5dW5ov9OnM%2Btnn%2BKEyRlPSwj7l5Vv9tICntqjNog%3D%3D

----------------------------------------------------------------------------------------------------


대용량 일괄처리를 편하게 하기 위해 설계된 가볍고 포괄적인 배치 프로그램

보통 아래와 같을때 많이 씀
대용량의 비즈니스 데이터를 복잡한 작업으로 처리해야하는경우
특정한 시점에 스케줄러를 통해 자동화된 작업이 필요한 경우(ex. 푸시알림, 월 별 리포트)
대용량 데이터의 포맷을 변경, 유효성 검사 등의 작업을 트랜잭션 안에서 처리 후 기록해야 하는 경우

Spring Batch는 로깅/추적, 트랜잭션 관리, 작업 처리 통계, 작업 재시작, 건너뛰기, 리소스 관리 등 대용량 레코드 처리에 필수적인 재사용 가능한 기능을 제공함
또한 최적화 및 파티셔닝 기술을 통해 대용량 및 고성능 일괄 작업을 가능하게 하는 고급 기술 서비스 및 기능을 제공함

------------------------------

배치 어플리케이션은 다음의 조건을 만족해야함

대용량 데이터 : 대량의 데이터를 가져오거나, 전달하거나, 계산하는 등의 처리를 할 수 있어야 함
자동화 : 심각한 문제 해결을 제외하고는 사용자 개입 없이 실행되어야함
신뢰성 : 무엇이 잘못되었는지를 추적할 수 있어야 한다(로깅, 알림)
성능 : 지정한 시간 안에 처리를 완료하거나 동시에 실행되는 다른 애플리케이션을 방해햐지 않도록 수행되어야함

----------------------------------------------------------------------------------------------------

스프링 배치 아키텍처

Application : 스프링배치를 사용하여 개발자가 작성한 모든 배치 작업과 사용자 정의 코드
Batch Core : 배치 작업을 시작하고 제어하는 데 필요한 핵심 런타임 클래스를 포함
Batch Infrastructure : 개발자와 애플리케이션에서 사용하는 일반적인 Reader와 Writer 그리고 RetryTemplate과 같은 서비스를 포함

------------------------------

스프링 배치 아키텍쳐 상세 해설

-----

어플리케이션(Application)

스프링 배치 프레임워크를 통해 개발자가 만든 모든 배치 Job 과 커스텀 코드를 포함함.
개발자는 업무로직의 구현에만 집중하고, 공통적인 기반기술은 프레임워크가 담당함

-----

배치 코어(Batch Core)

Job을 설정하고 구성, 실행, 모니터링, 관리하는 API로 구성되어 있음
JobLauncher, Job, Step, Flow 등이 있음

-----

배치 인프라스트럭처(Batch Infrastructure)

배치 코어에서 만든 Job의 구성 / 설계도 / 명세서를 바탕으로 그 안에서 실제로 그안에서 데이터의 흐름들을 처리하는(핸들링하는) 클래스들이 모여있음
데이터들을 어떻게 처리할것인가(파일, DB)
Application, Core 모두 공통 Infrastructure 위에서 빌드함
Job 실행의 흐름과 처리를 위한 틀을 제공함.
Reader, Processer Writer, Skip, Retry 등이 속함

----------------------------------------------------------------------------------------------------

JobRepository : 다양한 배치 수행과 관련된 수치 데이터와 잡의 상태를 유지 및 관리함
	일반적으로 관계형 데이터베이스를 사용하며 스프링 배치 내의 대부분의 주요 컴포넌트가 공유함
	실행된 Strp, 현재 상태, 읽은 아이템 및 처리된 아이템 수 등이 모두 JobRepository에 저장됨

Job : Job은 배치 처리 과정을 하나의 단위로 만들어 표현한 객체이고, 여러 Step 인스턴스를 포함하는 컨테이너다
	Job이 실행될 때 스프링 배치의 많은 컴포넌트는 탄력성(resiliency)을 제공하기 위해 서로 상호작용을 함

JobLauncher : Job을 실행하는 역할을 담당함. Job.execute를 호출하는 역할
	Job의 재실행 가능 여부 검증, 잡의 실행 방법, 파라미터 유효성 검증 등을 수행함
	스프링부트의 환경에서는 부트가 Job을 시작하는 기능을 제공하므로, 일반적으로 직접 다룰 필요가 없는 컴포넌트임
	Job을 실행하면 해당 잡은 각 Step을 실행함. 각 스텝이 실행되면 JobRepository는 현재 상태로 갱신됨

-----

Step : 스프링 배치에서 가장 일반적으로 상태를 보여주는 단위. 각 Step은 잡을 구성하는 독립된 작업의 단위다
	Step에는 Tasklet, Chunk 기반으로 2가지가 있음

-----

Tasklet : Step이 중지될 때까지 execute 메서드가 계속 반복해서 수행하고, 수행할 때마다 독립적인 트랜잭션이 얻어짐
	초기화, 저장 프로시저 실행, 알림 전송과 같은 잡에서 일반적으로 사용됨

Chunk : 한 번에 하나씩 데이터(row)를 읽어 Chunk라는 덩어리를 만든 뒤, Chunk 단위로 트랜잭션 단위를 나누는 것
	Chunk 단위로 트랜잭션을 수행하기 때문에 실패할 경우엔 해당 Chunk만큼만 롤백이 되고, 이전에 커밋된 트랜잭션 범위까지는 반영이 됨
	Chunk 기반 Step은 ItemReader, ItemProcessor, ItemWriter라는 3개의 주요 부분으로 구성될 수 있음
	ItemReader와 ItemProcessor에서 데이터는 1건씩 다뤄지고, Writer에선 Chunk 단위로 처리됨

일반적으로 스프링 배치는 대용량 데이터를 다루는 경우가 많기 떼문에 Tasklet보다 상대적으로 트랜잭션의 단위를 짧게 할 수 있는
ItemReader, ItemProcessor, ItemWriter를 이용한 Chunk 지향 프로세싱을 이용함

----------------------------------------------------------------------------------------------------

스프링 배치 초기화 설정 클래스

1. BatchAutoConfiguration
	스프링 배치가 초기화 될 때 자동으로 실행되는 설정클래스
	Job을 수행하는 JobLauncherApplicationRunner 빈을 생성

2. SimpleBatchConfiguration
	JobBuilderFactory와 StepBuilderFactory 생성
	스프링배치의 주요 구성 요소 생성 - 프록시 객체로 생성됨

........
........



























