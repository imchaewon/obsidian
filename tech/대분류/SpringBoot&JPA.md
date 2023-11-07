인텔리제이 그래들로 할때 오류나면 왼쪽아래 그래들Run창 항목하나하나 클릭해서 들어가서 자세히 살펴보기

Whitelabel Error Page (404)
1. 컨트롤러가 main폴더안에 올바르게 있는지
2. @Controller 어노테이션을 올바르게 넣었는지

Whitelabel Error Page (500)
1. 연결된 jsp가 없을경우

------------------------------

Cannot find template location
↓↓↓↓↓
resources 폴더 하위에 templates 폴더가 없어서 발생

------------------------------

의존성주입으로 가져온 클래스가 null일때
↓↓↓↓↓
① 의존성주입을 받을것이라고 알려야함(@Autowired등)
② 톰캣을 실행을 시켜서 요청을 해야함

Field cc2 in com.example.testProject.CC1 required a bean of type 'com.example.testProject.CC2' that could not be found.
↓↓↓↓↓
의존성주입으로 가져올원본클래스에서 스프링빈등록을 안한것 (@Component등)

------------------------------

DTO/VO 로 받은 데이터가 null일때
↓↓↓↓↓
DTO에 필드들이 제대로 들어가있는지 확인


java.sql.SQLNonTransientConnectionException : Could not connect to address=(host=localhost)(port=3306)(type=master) : 
Socket fail to connect to host:localhost, port:3306. Connection refused (Connection refused)
org.hibernate.HibernateException
↓↓↓
도커로 DB 켜기


org.hibernate.HibernateException: identifier of an instance of com.example.gettingstartedjpa.domain.member.jpo.MemberJpo was altered from 5 to null
↓↓↓
기본키가 5에서 null로 변경됨
id는 바꿀 필요가 없으니 setId는 빼기


org.hibernate.DuplicateMappingException: Table [push] contains physical column name [created_at] referred to by multiple logical column names: [created_at], [createdAt]
↓↓↓
이름이 중복됨 (created_at 와 createdAt 중 하나 제거하기)


java.sql.SQLSyntaxErrorException: (conn=16) Connection.setNetworkTimeout cannot be called on a closed connection
↓↓↓
재시작


ResourceHttpRequestHandler :Path with "WEB-INF" or "META-INF"
↓↓↓
jsp의존성 추가 후 Maven Update 하기


UnsatisfiedDependencyException: Error creating bean with name 'gitLabWebhookController' defined in file [/Users/mac/git/naverworks-bot-server/build/classes/java/main/kr/co/uniess/controller/GitLabWebhookController.class]: Unsatisfied dependency expressed through constructor parameter 1; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'gitPushService' defined in file 
↓↓↓
쿼리메소드를 잘못쓴경우.
언더바 쓰면 안되고 카멜로 바꾸기


.BeanCreationException: Error creating bean with name 'pushJpaRepository' defined in kr.co.uniess.domain.gitlab.repository.PushJpaRepository defined in @EnableJpaRepositories declared on JpaRepositoriesRegistrar.EnableJpaRepositoriesConfiguration: Invocation of init method failed; nested exception is org.springframework.data.repository.query.QueryCreationException: Could not create query for public abstract java.util.Optional kr.co.uniess.domain.gitlab.repository.PushJpaRepository.findByPushId(java.lang.String); Reason: Failed to create query for method public abstract java.util.Optional kr.co.uniess.domain.gitlab.repository.PushJpaRepository.findByPushId(java.lang.String)! No property 'pushId' found for type 'PushJpo'; nested exception is java.lang.IllegalArgumentException: Failed to create query for method public abstract java.util.Optional kr.co.uniess.domain.gitlab.repository.PushJpaRepository.findByPushId(java.lang.String)! No property 'pushId' found for type 'PushJpo'
↓↓↓
쿼리메소드 DB컬럼명 말고 VO/DTO속성명으로 해야함
속성명을 id로 했으면 findById 이렇게 쓰기


No property 'XXX' found for type 'XXX'; nested exception is java.lang.IllegalArgumentException: Failed to create query for method public abstract
↓↓↓
jpa의 필드명으로 _(언더바) 쓰면 안됨. db테이블이 스네이크로 되어있어도 카멜케이스로 바꾸기
@Column(name = "aaa_bbb") 이안에서 쓰는건 괜찮음


nested exception is com.fasterxml.jackson.databind.exc.InvalidDefinitionException: Conflicting getter definitions for property
↓↓↓
jpa의 필드명으로 _(언더바) 쓰면 안됨. 카멜케이스로 바꾸기


HttpMessageNotReadableException: JSON parse error: Cannot deserialize value of type `java.lang.String` from Object value (token `JsonToken.START_OBJECT`); nested exception is com.fasterxml.jackson.databind.exc.MismatchedInputException: Cannot deserialize value of type `java.lang.String` from Object value (token `JsonToken.START_OBJECT`)<EOL> at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 1, column: 2430] (through reference chain: kr.co.uniess.domain.gitlab.dto.GitUndefinedPushEvent["push_options"])]
↓↓↓
json데이터를 뭔가 보내는쪽의 형식과 다르게 받은경우
포맷을 똑같이 맞춰야함


IllegalArgumentException: The given id must not be null!
↓↓↓
@ID어노테이션이 삽입된 필드에 null이 들어간 경우


nested exception is org.springframework.orm.jpa.JpaSystemException: ids for this class must be manually assigned before calling save()
↓↓↓
@id어노테이션이 붙은 컬럼이 매핑이 되지 않은상태로 save 메소드가 실행된경우 발생
jao컬럼에 mapping시키는 vo/dto컬럼의 id가 이름이 다르진 않은지 확인.
이외에도 보낼때는 long으로 보내놓고 받을때는 Integer로 받거나
보낼때는 int로 보냈는데 받을때는 String으로 받는 등 서로 안맞는 자료형으로 받으려고 하면 값이 안들어가서 null이 나올수 있음


IllegalArgumentException: Conflicting getter definitions for property "id": kr.co.uniess.domain.gitlab.dto.GitPushEvent$GitCommit#getId() vs kr.co.uniess.domain.gitlab.dto.GitPushEvent$GitCommit#getPushId()
↓↓↓
"id"속성에대해 "getId()"랑 "getPushID()" 두개가 써서? 뭔가 충돌난상황.
하나를 지우던가 속성명을 바꿔야함 id → commitId 이런식으로


Unknown column 'commitfile0_.commit_id' in 'field list'
↓↓↓
1. @JoinColumn name속성값이 DB의 컬럼에 없는경우
2. DB의 컬럼명과 필드속성명이 다른경우
필드속성명은 카멜표기법으로 쓰고, DB컬럼명은 스네이크표기법으로 써야함


EntityNotFoundException: Unable to find kr.co.uniess.domain.gitlab.jpo.CommitFileJpo with id 9d2f89645ed5e5448c944fe7ba897d673f773ce5
↓↓↓
@JoinColumn 어노테이션의 파라미터 문제


JpaObjectRetrievalFailureException
↓↓↓
@OneToMany 어노테이션에 cascade = CascadeType.MERGE 속성 추가


IllegalStateException: Multiple representations of the same entity
↓↓↓
@Id 어노테이션이 붙은 속성에 중복된값이 들어감

------------------------------

org.thymeleaf.exceptions.TemplateInputException
↓↓↓
html파일이 templates폴더 밑에 지정한 경로에 없는 경우 발생

return "kakaoCI/login"
만약 컨트롤러가 위와 같다면

html페이지는 templates/kakaoCI/login.html 이경로에 있어야함

혹은 @Controller 대신 @RestController를 써서 뷰페이지 없이 개발 할 수도 있음

------------------------------

심볼 'ComponentScan'를 해결할 수 없습니다

build.gradle 에서 스프링관련 의존성이 있는지 확인
implementation 'org.springframework.boot:spring-boot-starter-security'
implementation 'org.springframework.security:spring-security-test'
implementation 'org.springframework.boot:spring-boot-starter-web'

있으면

프로젝트 루트폴더에서 아래 명령어 실행해보기
gradle clean build --debug

FAILURE 또는 ERROR 메시지: 빌드 실패 또는 오류를 나타냅니다.
Could not find 또는 Required by와 함께 언급된 라이브러리: 필요한 의존성이 발견되지 않은 경우를 나타냅니다.
이런 핵심 문장 찾기

↓↓↓

프로젝트 루트 디렉토리에서 .gradle 디렉토리를 찾아 삭제하고, 다시 gradle 빌드

------------------------------

Wrong user name or password

application.properties 파일에서
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver

밑에 아래 내용 추가

spring.datasource.username=sa

------------------------------

org.h2.jdbc.JdbcSQLNonTransientConnectionException: URL format error; must be "jdbc:h2:{ {.|mem:}[name] | [file:]fileName | {tcp|ssl}:[//]server[:port][,server2[:port]]/name }[;key=value...]" but is "jdbc:h2:tcp://localhost/~/jpashop" [90046-214]

url: jdbc:h2:tcp://localhost/~/test;MVCC:TRUE
↓↓↓
url: jdbc:h2:tcp://localhost/~/test;MVCC=TRUE

------------------------------

org.h2.jdbc.JdbcSQLNonTransientConnectionException: Unsupported connection setting "MVCC" [90113-214]

MVCC 옵션을 제거해야함

url: jdbc:h2:tcp://localhost/~/test;MVCC=TRUE
↓↓↓
url: jdbc:h2:tcp://localhost/~/test

------------------------------

No EntityManager with actual transaction available for current thread - cannot reliably process 'persist' call; nested exception is javax.persistence.TransactionRequiredException: No EntityManager with actual transaction available for current thread - cannot reliably process 'persist' call

트랜잭션이 없음
엔티티매니저를 통한 모든 데이터 변경은 항상 트랜잭션 안에서 이루어져야함

repository클래스에 걸거나 테스트케이스 메서드에 @Transactional어노테이션을 걸면됨

@Transactional 는 org.springframework.transaction.annotation껄로 쓰기. 쓸 수 있는 옵션이 javax.transaction꺼보다 많음

단 @Transactional 을 테스트케이스 메서드에 사용할 경우 테스트가 끝나고 롤백이 되버림. 데이터가 들어가있으면 반복적인 테스트를 못하기때문에 스프링이 자동으로 롤백을 해버림
실행후 로그에 rollback이 출력된걸로 확인가능

어썰트 만으로 테스트가 성공했는지 의심스러울때는 @Rollback(false) 어노테이션을 추가로 붙이기
@Test
@Transactional
@Rollback(false)
public void testNumber() throws Exception{
	.
	.

@Rollback(false) 대신 @Commit을 붙여도 됨

그리고 실행해보면 DB에 데이터가 잘 반영된걸 확인할 수 있음

------------------------------

com.mysql.cj.jdbc.exceptions.CommunicationsException: Communications link failure

The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
	at com.mysql.cj.jdbc.exceptions.SQLError.createCommunicationsException(SQLError.java:174) ~[mysql-connector-java-8.0.28.jar:8.0.28]

db연결 설정이 제대로 되지 않은 경우 발생
application.yml이나 application.properties 에서 db관련 설정을 잘 해주기

ex)
spring:
  datasource:
    url: jdbc:mysql://database-1.cwi9srgotlqn.ap-northeast-2.rds.amazonaws.com:3306/asdf
    username: admin
    password: qwer1234
    driver-class-name: com.mysql.cj.jdbc.Driver

------------------------------

java.lang.IllegalStateException: org.springframework.context.annotation.AnnotationConfigApplicationContext@3232a28a has not been refreshed yet

스프링 컨테이너에 등록된 빈이 없음

------------------------------

Failed to destroy the filter named [Tomcat WebSocket (JSR356) Filter] of type [org.apache.tomcat.websocket.server.WsFilter]

java.lang.AbstractMethodError: Receiver class org.apache.tomcat.websocket.server.WsFilter does not define or inherit an implementation of the resolved method 'abstract void destroy()' of interface javax.servlet.Filter.

org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean]: Factory method 'entityManagerFactory' threw exception; nested exception is java.lang.RuntimeException: Driver net.sf.log4jdbc.sql.jdbcapi.DriverSpy claims to not accept jdbcUrl, jdbc:mariadb://localhost:3306

Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate [org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean]: Factory method 'entityManagerFactory' threw exception; nested exception is java.lang.RuntimeException: Driver net.sf.log4jdbc.sql.jdbcapi.DriverSpy claims to not accept jdbcUrl, jdbc:mariadb://localhost:3306

↓↓↓

url: jdbc:mariadb://localhost:3306
를
url: jdbc:log4jdbc:mariadb://localhost:3306
로 변경

------------------------------

@Transactional 작동이 안될때 (예외가 발생했는데도 롤백이 안될때)

@Transactional
↓↓↓
@Transactional(rollbackFor = Exception.class)

수정해보기

------------------------------

org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'logDemoController' defined in file [/Users/imchaewon/git/study/core/out/production/classes/hello/core/web/LogDemoController.class]: Unsatisfied dependency expressed through constructor parameter 0; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'logDemoService' defined in file [/Users/imchaewon/git/study/core/out/production/classes/hello/core/web/LogDemoService.class]: Unsatisfied dependency expressed through constructor parameter 0; nested exception is org.springframework.beans.factory.support.ScopeNotActiveException: Error creating bean with name 'myLogger': Scope 'request' is not active for the current thread; consider defining a scoped proxy for this bean if you intend to refer to it from a singleton; nested exception is java.lang.IllegalStateException: No thread-bound request found: Are you referring to request attributes outside of an actual web request, or processing a request outside of the originally receiving thread? If you are actually operating within a web request and still receive this message, your code is probably running outside of DispatcherServlet: In this case, use RequestContextListener or RequestContextFilter to expose the current request.

↓↓↓

@Controller
@RequiredArgsConstructor
public class LogDemoController {
	private final MyLogger myLogger;

스프링이 뜰때 컨트롤러가 스프링빈에 등록되고, 의존관계 주입이 일어나는데 이때 MyLogger가 @Scope("request") 인 경우,
request스코프의 생존범위는 고객의 요청이 들어왔다가 나갈때까지인데 고객의 요청이 아직 안들어왔기때문에 발생.
빈이 없는데 스프링한테 달라고 하니까 오류를 내버린것. 오류메시지를 보면 Scope 'request' is not active (스코프 request가 아직 활성화되지 않았음) 라고 나와있음

해결방법은 Provider를 써야함

----------------------------------------------------------------------------------------------------

의존성주입

"서버를 실행시키면" 의존성주입을 설정한 클래스들을 알아서 생성해줌

그러면 @Controller어노테이션이 있는 클래스에서 @RequestMapping으로 호출했을때
빈으로 등록한(@Component 어노테이션 이용) 클래스를 의존성주입(@Autowired등)으로 가져올 수가 있게됨

-----

스프링부트는 의존성주입시

DemoApplication 파일(프로젝트를 만들면 자동으로 생기는 파일(servlet-context.xml, root-context.xml))에서 ApplicationContext를 직접 만들어 사용할 필요 없이
@SpringBootApplication이라는 어노테이션 때문에 @ComponentScan 등 여러가지 기능을 편리하게 사용할 수 있다.
↓↓↓↓↓
@SpringBootApplication
public class DemoApplication {
	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}
}
@SpringBootApplication 어노테이션 안에는 Component, Configuration 어노테이션이 존재한다

위와 같은 이유 때문에,

아래처럼 하나하나 bean으로 등록하거나
<bean id="bookRepository" class="com.example.demo.BookRepository">
</bean>

아래처럼 component-scan을 쓸 필요가 없으며
<beans ~~~>
    <context:component-scan base-package="com.example.demo"/>

해당 클래스에 @Configuration 어노테이션을 달아주면 된다

Container에 Spring Bean으로 등록시켜주는 Annotation
ex) @Configuration, @Bean, @Component, @Controller, @Service, @Repository ...... ★Mapper는 안됨!

-----

Container에 있는 Spring Bean을 찾아 주입시켜주는 Annotation
- @Autowired : 스프링 컨테이너에 있는 참조할 Bean을 찾아 주입한다. (SPRING 표준)

----------------------------------------------------------------------------------------------------

yml 파일에 내용 작성시 :(콜론) 뒤에 한칸 띄워야함 (안띄우면 오류)

type-aliases-package:abc → X
type-aliases-package: abc → O

----------------------------------------------------------------------------------------------------

스프링부트는 기존에 dependency 설정에서 버전까지 직접 적어줘야 했던것을,
단순하게 groupID와 artifactID만 있으면 자동으로 권장 버전으로 설정해주기때문에 편리함

의존성 설정시

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

dependencies는 implementation과 testImplementation으로 나뉘어져있음
implementation은 개발할때 내가 필요한 라이브러리를 적어 가져와달라고 하는것이고
testImplementation은 JAVA에서 테스트 코드를 작성할 때 필요한 라이브러리를 적는 곳임

현재 jUnit5 라이브러리를 사용하고 있음

----------------------------------------------------------------------------------------------------

스프링 부트 스타터(start.spring.io/)

Spring Boot 버전 선택할때

SNAPSHOT은 아직 만들고 있는 버전을 뜻하고
M1은 정식으로 릴리즈 된 버전이 아님을 뜻함

----------------------------------------------------------------------------------------------------

1. 프로젝트 생성

-----

방법1. 이클립스 sts3설치해서 New → Other... → Spring Boot → Spring Starter Project

Package에 Group + Artifact 합친걸 직접 입력해줘야함
Group가 com.example이고 Artifact가 spring-boot-project라면 com.example.spring-boot-project 이렇게

-----

방법2. spring initializr 검색해서 https://start.spring.io/ 들어가기

Project : Maven Project
Language : -(Java)

Spring Boot : -(2.6.3)

Group : com.example
Artifact : spring-boot-project
Name : -
Description : -
Package name : -
Packaging : War
Java : 8

ADD DEPENDENCIES : Spring Web, Spring Boot DevTools, MariaDB Driver, MariaDB Framework, Lombok, Spring Data JPA
검색해서 선택

다했으면 GENERATE 클릭해서 압축파일 다운받은다음 원하는 위치에 풀고, 이름 바꾸고(spring-boot-project),
import → Projects from Folder or Archive 해서 가져오기

-----

pom.xml DB 드라이버 Dependency 있는지 확인

<dependency>
	<groupId>org.mariadb.jdbc</groupId>
	<artifactId>mariadb-java-client</artifactId>
	<scope>runtime</scope>
</dependency>

-----

src/main/resources 밑에 application.properties를 yml로 변경
spring:
  datasource:
    url: jdbc:mariadb://61.98.130.167:3306/member_manager
    username: front
    password: front!@#$
    driver-class-name: org.mariadb.jdbc.Driver

  jpa:
    show-sql: true
    properties:
      hibernate:
        format_sql: true
    hibernate:
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
        
server:
  port: 9999

-----

2. 빌드 및 실행

-----

war파일로 빌드

1. 터미널에서 톰캣 실행
톰캣폴더 → bin → startup.sh

2. 톰캣 잘 실행되고있는지 확인
	방법1) ps -ef | grep tomcat
	방법2) 브라우저에 localhost:8080 쳐서 고양이

3. 이클립스 프로젝트 폴더 우클릭 → Run As → Maven build
Goals에 install 입력 후 Run

4. Show in → System Explorer
탐색기로 연, 프로젝트폴더의 target 안에 war파일 만들어진거 확인

5. 프로젝트폴더에 만들어진 war파일을 톰캣폴더의 webapps로 이름바꿔서복사 (이름 : spring-project.war)
cp ~/eclipse-workspace/asd/target/spring-boot-project-0.0.1-SNAPSHOT.war ~/apache-tomcat-9.0.58/webapps/qwer.war
그럼 같은 이름의 폴더가 자동으로 생긴다(톰캣이 실행중이여야함.
폴더가 생겼다면 추후에 어떤 작업 없이 톰캣만 켜면 해당 프로젝트에 접속할 수 있음.
변경시 Run As → Java Appication)

6. 브라우저 주소창에 http://localhost:8080/spring-project/index.do (컨텍스트 루트패스로 webapps안의 방금만들어진 폴더 이름을 입력) 쳐서 연결되는거 확인

7. 프로젝트명을 안쓰고 루트경로로 바꾸려면(프로젝트명을 안쓰기위해)
기존에 있던 webapps밑의 ROOT폴더 삭제 후(삭제하면 고양이 안나옴) spring-project.war를 ROOT.war로 변경후(이때 폴더명도 자동으로 바뀜) 브라우저 주소창에
http://localhost:8080/index.do 쳐서 들어가보기

8. 화이트라벨 에러 페이지가 뜨면 성공.

9. 톰캣을 끌때는 톰캣폴더 → bin → shutdown.sh

10. 빌드된 프로젝트를 제거하고싶으면 톰캣폴더/webapps의 해당프로젝트war파일과 폴더를 삭제
(톰캣폴더로 빼놨다면 Maven clean과 관련없어짐.)

+++

톰캣폴더로 빼면 수정시 반영이 안되는듯.
Run As → Java Appication으로 appication.yml에서 설정한 포트번호 띄운 페이지만 반영됨

----------------------------------------------------------------------------------------------------

jar파일로 배포 (톰캣실행여부, 이클립스와 상관없이 독립적으로 실행가능)

jar로하면 webapp에 옮겨놔도 폴더가 생성되지 않음. war처럼 tomcat만 켜도 실행되지가 않음.
메인메소드에서 Run As → Java Application 하거나 Maven빌드후 명령어로 직접실행해야함.
즉 결국 tomcat이 실행되고있지않아도 jar파일만 있으면 배포를 할 수 있다)

1. pom.xml 에서 <packaging>태그에 jar이 입력되어있거나 태그가 아예 없는거 확인
(war에서 jar로 바꿨다면 maven update 한번 해야함)

2. 프로젝트 폴더 우클릭 → Run As → Maven build

3. 탐색기로 연, 프로젝트폴더의 target 안에 jar파일 만들어진거 확인

4. 현재위치에서 터미널 열어서 실행
java -jar jar파일이름.jar

5. application.properties 에서 설정한 포트로 브라우저에서 접속

6. 화이트라벨 에러 페이지가 뜨면 성공.

7. 끌때는 ps -ef | grep 으로 pid 찾아서 kill [pid] 로 종료하거나 이클립스에서 정지버튼 누르기
터미널로 켰다면 끌때도 터미널로 꺼야함

8. 빌드된 프로젝트를 제거하고싶으면 프로젝트우클릭 → Run As → Maven clean
(jar로 한번 배포하면 프로젝트폴더/target 안에 여러 폴더들과 jar파일이 빌드가 되는데
target폴더안의 내용들이 살아있으면(jar파일은 상관없음)Run As → Java Appication으로 실행이 가능하고,
clean을 하면 target폴더가 지워졌다 새로 생긴다 = 초기화된다
jar파일을 다른폴더로 뺴놨다면 clean을 해도 터미널로 계속 실행가능함)

----------------------------------------------------------------------------------------------------

위처럼 배포 안하고 그냥 실행만 하려면

이클립스의 프로젝트의 메인함수가 있는 파일(/src/main/java → com.example.springbootproject → SpringBootProjectApplication.java)에서 실행
Run As → Java Application

위 방법으로 하면 저장할때마다 자동 반영되고, 오류가 나면 종료됨. 다시 실행시켜줘야함

----------------------------------------------------------------------------------------------------

DB 연결

src/main/resources 밑에 있는
application.properties 또는 application.yml

----------------------------------------------------------------------------------------------------

<인텔리제이>

Maven or Gradle 선택
스프링부트 버전 선택
자바 / 코틀린 / 그루비 선택
8 / 11 / 15 자바버전 선택
jar / war 선택
그룹과 Artifact명을 입력하면 패키지명이 합쳐져서 입력됨

라이브러리들을 pom.xml에 직접 추가하지않고, 클릭만으로 간편하게 추가할수있음
Spring Boot DevTools, Lombok, Spring Web 정도 추가


<인텔리제이 커뮤니티 버전>

인텔리제이 커뮤니티 버전은 Spring Initializr가 없음 → https://start.spring.io/ 여기서 해야됨

라이브러리 추가시 ADD DEPENDENCIES... 여기서 하면됨

다했으면 GENERATE 클릭 → 압축풀기 → 인텔리제이에서 Project → Open → 압축푼 폴더 선택 → 아까 선택한 Maven/Gradle 선택


<이클립스>

Help → Eclipse Marketplace... → sts검색 → 3버전 애드온 → 다운 → 이클립스 재시작

New → Other... → Spring Boot → Spring Starter Project

Service URL은 데모 설정을 불러오는 항목이고 https://start.spring.io를 넣으면 된다
그 밑에있는 Name부터 설정하면 된다
패키지명은 Group + Artifact로 복붙해 입력

Next 누르면 라이브러리 추가할수 있는 화면이 나온다
필요한거 다 체크했으면 Finish

----------------------------------------------------------------------------------------------------

롬복 추가는 IntelliJ IDEA → Preferences... → Plugins → lombok 검색 → Install (Installed탭에 있으면 이미 다운된것)
jar파일받거나 설정파일 변경할 필요없음

이후 인텔리제이를 껏다키면 우측 하단에 Lombok~~창이 떠있는데 Enable 클릭하면됨

----------------------------------------------------------------------------------------------------

포트 변경

스프링부트는 톰캣이 내장되어있음
실행을 시키면 로그에 Tomcat initialized with port(s): 8080 (http) 떠있는게 보임

포트를 변경하고싶다면 설정파일을 수정하면 되는데,
src/resources/application.properties 파일에서 설정하면 됨

들어가서 port까지 입력하면 목록이 나옴 → Enter → 8081 이런식으로 입력 (결과: server.port=8081)
참고로 Ultimate버전만 이런 자동완성 기능이 있고 Community버전은 이런 자동완성 기능이 없음
(이클립스는 무료지만 똑같은 기능이 있음. 근데 살짝 느리게 뜸)

----------------------------------------------------------------------------------------------------

인텔리제이에서 실행은 우측 위에있는 ▶︎ 누르면 되고 ctrl+R 눌러도 됨

----------------------------------------------------------------------------------------------------

인텔리제이에서 jar파일로 실행을 시킬수있음 (▶︎ 누른것과 같은효과)

방법은 Gradle메뉴에서 프로젝트명 → Tasks → build → bootJar 우클릭 실행
그러면 프로젝트폴더밑에 build폴더가 만들어지고 그안에 libs폴더에 ~~.jar파일이 생김
복사후 파인더에서 아무데나 붙여넣고, 터미널의 cd로 파일위치까지 들어가서 java -jar 파일명.jar 하면
똑같이 실행됨 이후 웹에서 원하는 경로로 들어갈수있음

----------------------------------------------------------------------------------------------------

JPA

-----

어노테이션

@Entity : 테이블 만들때 [클래스에]
@Id : 기본키 설정할때 [필드에]

@GeneratedValue() : 시퀀스만들때 [필드에]
@GeneratedValue(strategy = GenerationType.AUTO) : 
@GeneratedValue(strategy = GenerationType.IDENTITY) : 사용하는 데이터베이스가 키 생성을 결정. MYSQL이나 MariaDB의 경우 auto increment 방식을 이용
@GeneratedValue(strategy = GenerationType.SEQUENCE) : 데이터베이스의 sequence를 이용해서 키를 생성. @SequenceGenerator랑 같이 씀
@GeneratedValue(strategy = GenerationType.TABLE) : 키 생성 전용 테이블을 생성해서 키 생성. @TableGenerator랑 같이 씀

@Table(name="이름") : 테이블 이름 설정 [클래스에]

-----

application.properties

<DB설정>
spring.datasource.dbcp2.driver-class-name=org.mariadb.jdbc.Driver
spring.datasource.url=jdbc:mariadb://localhost:3306/bootex
spring.datasource.username=bootuser
spring.datasource.password=java1234

spring.jpa.hibernate.ddl-auto=update : 프로젝트 실행시 테이블을 추가할건지 업데이트할건지 설정 (update로 해놓으면 클래스를 바꾸면 테이블이 바뀜)
spring.jpa.properties.hibernate.format_sql=true : sql로그를 보기 깔끔하게 보여줌
spring.jpa.show-sql=true : 만들어진 sql을 보여줌
logging.level.org.hibernate.type.descriptor.sql=trace : hibernate가 보여주는 ? 에 어떤 값이 들어갔는지 보여줌

-----

① 새프로젝트 → Spring Boot → Spring Starter Project

Name : ex2
Type : Gradle
Packaging : War
Java Version : 8
Language : Java
Group : org.zerock

추가할것 : Lombok, Spring Boot DevTools, Spring Web, Spring Data JPA, MariaDB Driver
총 5개 라이브러리를 추가


② DB 연결해주는 속성 추가

/src/main/resources/application.properties에서 내용 변경

spring.datasource.dbcp2.driver-class-name=org.mariadb.jdbc.Driver
spring.datasource.url=jdbc:mariadb://localhost:3306/bootex
spring.datasource.username=bootuser
spring.datasource.password=java1234


③ 실행해보고 오류 안찍히고 잘 되는지 확인

④ src/main/java → 패키지 → entity 패키지 생성

⑤ entity 패키지 안에 Memo.java 생성 (이 클래스가 데이터베이스에서의 "테이블", @Entity 어노테이션 붙이기)
@Entity
public class Memo {


⑥ Memo.java 안에 내용 추가 (컬럼이 데이터베이스에서의 "컬럼", 기본키에는 @Id 어노테이션 붙이기)
@Entity
public class Memo {

	@Id
	private long mno;
	
}


⑦ 시퀀스 및 컬럼 추가
@Entity
public class Memo {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private long mno;
	
	private String memoText;
		
}


⑧ 프로젝트 실행시 테이블을 추가할건지 업데이트할건지 설정 (update로 해놓으면 클래스를 바꾸면 테이블이 바뀜)
/src/main/resources/application.properties에서 내용 추가

spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.show-sql=true


⓽ 테이블 이름 지정 및 어노테이션들 추가
@Entity
@Table(name="tbl_meno")
@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class Memo {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private long mno;
	
	private String memoText;
		
}


⑩ 실행
로그가 찍히며, 디비버에서 테이블 추가된거 확인하기

-----

JPA 리파지토리(Repository)

엔티티같은걸 찾아주는 것인데, DAO라고 보면 됨

repository패키지 안의 클래스이름은 보통 repository or DAO 로 씀

① /src/main/java/org/zerock/ex2/entity/Memo.java 에서 패키지 추가(name:repository)

② 만든 repository패키지 안에 인터페이스 추가(name:MemoRepository)

③ extends JpaRepository<Memo,Long> 추가 (@Entity했던게 첫번째인수로 들어가고, @Id했던게 두번째 인수로 들어감)

④ /src/test/java/org/zerock/ex2에 repository패키지 추가

⑤ 그안에 테스트클래스(name:MemoRepositoryTest) 추가

⑥ @SpringBootTest 어노테이션 추가

-----

JPA CRUD

insert → save(엔티티객체)
select → findById(키 타입), getOne(키 타입)
	findById는 실행할때 동작, getOne은 실행한다음 사용할때 동작(lazy loding, 게으른 로딩)
update → save(엔티티 객체)
	update와 insert는 똑같이 save이며, 없으면 insert, 있으면 update를 한다
delete → deleteById(키 타입), delete(엔티티객체)

----------------------------------------------------------------------------------------------------

1. 영문으로된 글을 한글로 번역하는 것은 컴파일이다.

2. 번역한 글을 책으로 엮는 것은 빌드이다.

3. 완성된 책을 고객들이 읽을 수 있도록 서점에 진열하는 것은 배포이다.

4. 1~2번 과정을 하나로 묶어 '빌드 한다'고 하기도 한다.

----------------------------------------------------------------------------------------------------

JPA 쓰기 위한 설정

1. 아무 인터페이스나 만들어서 JpaRepository<MemberEntity, Long> 를 상속받는다
ex) public interface MemberRepository extends JpaRepository<MemberEntity, Long> {

2. 그 인터페이스를 서비스클래스에서 끌어온다
ex)
@RequiredArgsConstructor
public class MemberService {
	private final MemberRepository memberRepository;

3. 서비스클래스에서 아래처럼 이용하면 됨
	public List<Member> fetchList(){
		return memberRepository.findAll()
		.stream()
		.map(Member::of)
			.collect(Collectors.toList());
	}

	@Transactional(readOnly = true)
	public Member fetch(Long id) {
		
		MemberEntity memberEntity = memberRepository.findById(id)
				.orElseThrow(RuntimeException::new);
		
		return Member.of(memberEntity);
		
	}

----------------------------------------------------------------------------------------------------

application.yml

spring:
  datasource:
    url: jdbc:mariadb://localhost:3306/spring
    username: root
    password: root!@#$
    driver-class-name: org.mariadb.jdbc.Driver

  jpa:
    show-sql: true
    properties:
      hibernate:
        format_sql: true
    hibernate:
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
        
mybatis:
  mapper-locations: com/secondproject/mapper/*.xml
  type-aliases-package: com.example.secondproject
  
server:
  port: 9998

-----

스프링부트에서 mybatis xml 쓰기위한 설정

제일 바깥라인(spring과 형제라인)에 아래내용 추가 (경로는 상황에 맞게 수정)

mybatis:
  mapper-locations: com/secondproject/mapper/*.xml

-----

mybatis에서 사용자자료형(클래스)를 쓸때 풀경로(패키지를포함한) 안쓰고 클래스명만 쓰기위한 설정

제일 바깥라인(spring과 형제라인)에 아래내용 추가 (경로는 상황에 맞게 수정)

mybatis:
  type-aliases-package: com.example.secondproject

----------------------------------------------------------------------------------------------------

JPA레파지토리상속받은인페.findAll() : 다가져옴
JPA레파지토리상속받은인페.findOne() : @Id 걸려있는걸로 조회해서 가져옴

----------------------------------------------------------------------------------------------------

대리님 예제
.
.
.

프로젝트 생성
Name: jpa-tutorial
Language: java
Type: Gradle
Group: io.starter
Artifact: jpa-tutorial
Java: 11
Packaging: Jar

Spring Boot DevTools
Lombok
Spring Data JPA
MariaDB Driver


데이터베이스 스키마 생성
CREATE DATABASE tutorial CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE USER 'tutorial'@'%' IDENTIFIED BY 'tutorial';
CREATE USER 'tutorial'@'localhost' IDENTIFIED BY 'tutorial';
GRANT ALL PRIVILEGES ON tutorial.* TO tutorial@'%';
GRANT ALL PRIVILEGES ON tutorial.* TO tutorial@'localhost';
FLUSH PRIVILEGES;


application.yml 설정
spring:
	datasource:
		url: jdbc:mariadb://localhost:3306/tutorial
		username: tutorial
		password: tutorial
		driver-class-name: org.mariadb.jdbc.Driver
	jpa:
		show-sql: true
		properties:
			hibernate:
				format_sql: true
		hibernate:
			ddl-auto: update

프로젝트에 Spring Data JPA 의존성이 걸려 있으면 디폴트 설정으로 인해 DataSource 설정을 필수적으로 해주어야 됩니다. 해당 설정이 없는 경우 JPA 모듈을 사용할 수 없기 때문입니다.

`spring.jpa.show-sql` 설정은 repository method가 수행될 때 실제로 수행되는 SQL문을 콘솔에 출력해주고 `spring.jpa.properties.hibernate.format_sql` 설정을 통해 한 라인으로 길게 표시되는 로그의 형태를 비교적 이쁜 형태로 보여주도록 하는 설정입니다.

`spring.jpa.hibernate.ddl-auto` 설정은 Database Scheme 초기화 전략과 관련된 설정인데 가능한 설정 옵션으로는 다음과 같습니다.


- none (Default) : 아무런 처리를 하지 않음
- update : 변경된 스키마가 존재하면 갱신
- validate : 변경된 스키마가 존재하면 종료
- create : 기존 스키마를 초기화 후 다시 생성 (테이블 내용이 삭제됨)
- create-drop : 기존 스키마를 초기화 후 다시 생성한 후 종료 시점에 초기화


Entity클래스 및 모델 클래스 작성

[io.starter.jpatutorial.domain.jpo.PostJpo]
@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "post")
public class PostJpo {
		/**
     * 게시글 번호 (Auto Increment)
     */
    @Id
		@GeneratedValue(strategy = GenerationType.IDENTITY)
		private Long no = 0L;
    
    /**
     * 게시글 제목
     */
    private String title;

    /**
     * 게시글 내용
     */
    private String content;
		
		/**
     * 게시글 작성 일시
     */
    private LocalDateTime createdAt = LocalDateTime.now();

    /**
     * 조회수
     */
    private int views = 0;
}


[io.starter.jpatutorial.domain.model.Post]
@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Post {
    private Long no;
    private String title;
    private String content;
    private LocalDateTime createdAt;
    private int views;

		/**
     * Jpo -> Domain 객체 변환
     */
    public static Post jpoOf(PostJpo postJpo) {
        Post post = new Post();
        BeanUtils.copyProperties(postJpo, post);
        return post;
    }

    /**
     * Domain 객체 -> Jpo 변환
     */
    public PostJpo asJpo() {
        PostJpo postJpo = new PostJpo();
        BeanUtils.copyProperties(this, postJpo);
        return postJpo;
    }
}


Jpo는 Java Persistence Object로 영속성 Layer에서 Database와 Application Layer에서 사용을 하기 위한 클래스입니다.

쉽게 말하여 Application 레벨에서 Database 와의 데이터 조회 및 갱신은 Entity 객체로 이루어져야 되는 것이고, View 또는 데이터가 보여지는 즉 Client와 데이터를 주고 받는 영역에서 DTO 클래스를 통해 이루어져야 됩니다.

그에 따라 Jpo ↔  Dto 클래스 간에는 속성이 흡사할 수 있고, 서로 변환이 가능한 구조로 만들어줍니다.

해당 내용을 도식화해보면 다음과 같습니다.
https://cyan-grape-340.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa7c4ac9e-e96d-4156-bb1e-6308a4164938%2FUntitled.png?table=block&id=40239dd8-8c89-415c-aefb-316cd7c3d545&spaceId=19968373-79c0-4f83-bb2e-4e32f96650c6&width=2000&userId=&cache=v2


### Repository Interface 작성

- **`io.starter.jpatutorial.domain.repository.PostMariaRepository`**

```java
@Repository
public interface PostMariaRepository extends JpaRepository<PostJpo, Long> {
}
```

Spring Data JPA 모듈에서 제공하는 Repository Interface는 대표적으로 `CrudRepository`, `JpaRepository`, `PagingAndSortingRepository` 등이 있습니다.

용도 및 환경에 따라 다를 수 있으나 일반적으로 간단하게 가장 많이 사용되는 `JpaRepository`을 상속받아 Generic 구체 타입은 특정 Entity 클래스와 해당 클래스의 `@Id`가 되는 필드의 타입을 선언합니다.

`JpaRepository` 클래스 기준으로 보면 다음과 같은 메소드들이 이미 선언이 되어있으며 이미 명칭에 따라 구현된 로직으로 실행이 됩니다.

- save
- saveAll
- findById
- findAll
- exists
- deleteById
- deleteAll



### Service 클래스 조회 로직 작성

- **`io.starter.jpatutorial.service.PostListService`**

```java
@Service
@RequiredArgsConstructor
public class PostListService {
    private final PostMariaRepository postMariaRepository;

    @Transactional(readOnly = true)
    public List<Post> fetch() {
        return postMariaRepository.findAll()
                .stream()
                .map(Post::jpoOf)
                .collect(Collectors.toList());
    }
}
```


```java
@Service
@RequiredArgsConstructor
public class PostListService {
    private final PostMariaRepository postMariaRepository;

    @Transactional(readOnly = true)
    public List<Post> fetch() {
        return postMariaRepository.findAll()
                .stream()
                .map(Post::jpoOf)
                .collect(Collectors.toList());
    }
}
```


### Entity 조회(Select) 테스트

[io.starter.jpatutorial.JpaTutorialApplicationTests]

package io.starter.jpatutorial;

import io.starter.jpatutorial.domain.model.Post;
import io.starter.jpatutorial.service.PostListService;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import java.util.List;

@SpringBootTest
class JpaTutorialApplicationTests {
    @Autowired
    private PostListService postListService;

    @Test
    @DisplayName("게시글 목록 전체 조회 테스트")
    void fetch() {
        List<Post> posts = postListService.fetch();
        Assertions.assertNotNull(posts);
        System.out.println("Posts --> " + posts);
    }
}


간단하게 Junit을 활용한 테스트 코드를 작성해줌으로 손쉽게 테스트를 해볼 수 있습니다.

최초에 실행할 시 별도로 데이터베이스에서 테이블을 생성해주지 않았는데, `spring.jpa.hibernate.ddl-auto` 설정을 해줌으로 인해 서비스가 Bootstrap 되는 과정에서 내가 설계한 Entity 클래스의 내용을 바탕으로 자동으로 테이블을 생성해주는것을 알 수 있습니다.

또한 지금은 임의의 데이터를 생성해주지 않았음으로 결과 레코드는 조회가 되지 않는것이 정상입니다.


추가로 임의로 Entity에 필드를 추가하거나하는 등의 스키마 구조가 변경되는 경우 아래에서 확인할 수 있듯이 자동으로 데이터베이스 테이블 속성 변경이 이루어지는것도 알 수 있습니다.


Service 클래스 저장(Insert) 로직 작성
[io.starter.jpatutorial.service.PostListService]
@Service
@RequiredArgsConstructor
public class PostListService {
    private final PostMariaRepository postMariaRepository;

    @Transactional(readOnly = true)
    public List<Post> fetch() {
        return postMariaRepository.findAll()
                .stream()
                .map(Post::jpoOf)
                .collect(Collectors.toList());
    }

		@Transactional
    public void save(List<Post> posts) {
        List<PostJpo> postJpos = posts.stream()
                .map(Post::asJpo)
                .collect(Collectors.toList());

        postMariaRepository.saveAll(postJpos);
    }
}


Entity 저장(Insert) 로직 테스트
[io.starter.jpatutorial.JpaTutorialApplicationTests]
@SpringBootTest
class JpaTutorialApplicationTests {
    @Autowired
    private PostListService postListService;

    @Test
    @DisplayName("게시글 목록 전체 조회 테스트")
    void fetch() {
        List<Post> posts = postListService.fetch();
        Assertions.assertNotNull(posts);
        System.out.println("Posts --> " + posts);
    }

		@Test
    @DisplayName("게시글 생성 테스트")
    void save() {
        List<Post> posts = Arrays.asList(
                Post.builder().title("게시글 1").content("게시글 1 내용").build(),
                Post.builder().title("게시글 2").content("게시글 2 내용").build(),
                Post.builder().title("게시글 3").content("게시글 3 내용").build()
        );
        postListService.save(posts);
    }
}


임의의 임시 Post 객체들을 생성하여 save 로직을 수행하면 insert SQL문이 수행되면서 데이터베이스에 정상적으로 생성됨을 확인할 수 있습니다.

-----

연관 관계 자식(하위) Entity 작성

1:N 연관 관계를 가지는 하위 Entity 작성
[io.starter.jpatutorial.domain.jpo.CommentJpo]
@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "comment")
public class CommentJpo {
    /**
     * 댓글 고유 ID
     */
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id = 0L;

    /**
     * 게시글 번호
     */
    private Long postNo;

    /**
     * 댓글 내용
     */
    private String content;

    /**
     * 댓글 작성 일시
     */
    private LocalDateTime createdAt;
}


상위 Entity에 하위 Entity를 필드로 추가
[io.starter.jpatutorial.domain.jpo.PostJpo]
@Getter
@Setter
@ToString
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "post")
public class PostJpo {
    /**
     * 게시글 번호 (Auto Increment)
     */
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long no = 0L;

    /**
     * 게시글 제목
     */
    private String title;

    /**
     * 게시글 내용
     */
    private String content;

    /**
     * 게시글 작성 일시
     */
    private LocalDateTime createdAt = LocalDateTime.now();

    /**
     * 조회수
     */
    private int views = 0;

    @ToString.Exclude
    @OneToMany(cascade = CascadeType.PERSIST)
    @JoinColumn(name = "postNo")
    private List<CommentJpo> comments = new ArrayList<>();

    /**
     * 댓글 생성
     */
    public void addComment(CommentJpo commentJpo) {
        this.comments.add(commentJpo);
    }
}

우선 `@ToString.Exclude` 애노테이션을 달아줌으로써 Lazy loading이 되는 필드와 Lombok으로 Generation되는 ToString간의 우려되는 성능상의 문제를 제거해줍니다.

Join의 기준이 되는 컬럼은 임의로 설정을 해주지 않는 경우 기본적으로 각 Entity들의 Primary key를 기준으로 수행됩니다. 그래서 `@JoinColumn` 애노테이션을 통해 임의로 Join의 기준이 되는 컬럼을 설정해 줄 수 있습니다.

다음으로 Post Entity와 Comment Entity는 도메인 특성상 1:N 관계로 `@OneToMany` 애노테이션을 달아주면서 cascade 정책으로는 Persist로 설정해주었습니다. cascade는 연관 관계에 있는 Entity간에 영속성을 전파하는 옵션으로 가능 설정은 다음과 같습니다.

- **`CascadeType.ALL`**
- **`CascadeType.PERSIST`**
- **`CascadeType.MERGE`**
- **`CascadeType.REMOVE`**
- **`CascadeType.REFRESH`**
- **`CascadeType.DETACH`**

엔티티간의 연관 관계를 설정하는 Annotation의 종류는 다음과 같고 특성에 따라 알맞은 Annotation을 사용할 수 있습니다.

- `**@OneToOne**` - 1:1
- `**@OneToMany**` - 1:N
- `**@ManyToOne**` - N:1
- `**@ManyToMany**` - N:N

마지막으로 Comment 객체를 추가하는 addComment 메소드를 작성해줍니다.


하위 Entity Service 클래스 저장(insert) 로직 작성
[io.starter.jpatutorial.service.CommentService]
@Service
@RequiredArgsConstructor
public class CommentService {
    private final PostMariaRepository postMariaRepository;

    @Transactional
    public void save(long postNo, Comment comment) {
        PostJpo postJpo = postMariaRepository.findById(postNo)
                .orElseThrow(IllegalArgumentException::new);
        postJpo.addComment(comment.asJpo());
    }
}

우선 특정 게시글 번호(ID)와 작성된 댓글의 객체를 받아서 댓글을 추가하는 함수를 작성합니다.

처리 순서는 다음과 같습니다.

1. 특정 {postNo} 번호의 게시글 Select
    a. 게시글이 존재하는 경우 해당 게시글 Entity에 Comment 객체 추가
    b. 게시글이 존재하지 않는 경우 예외 Case로 Exception 발생

여기서 별도로 Repository 클래스에서 Insert가 이루어지는 save 메소드를 호출하지 않고 Entity의 상태를 변경해주는 `addComment` 함수를 호출하게 되면 Spring Data JPA의 더티체킹(Dirty Checking) 변경 감지로 인해 자동으로 SQL문이 수행됩니다.


하위 Entity 저장(insert) 로직 테스트
[io.starter.jpatutorial.JpaTutorialApplicationTests]
package io.starter.jpatutorial;

import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import java.util.List;

@SpringBootTest
class JpaTutorialApplicationTests {
		@Autowired
    private CommentService commentService;

		@Test
    @DisplayName("게시글 댓글 생성 테스트")
    void saveComment() {
        Comment comment = Comment.builder()
                .content("게시글 1의 첫번째 댓글")
                .build();
        commentService.save(1, comment);
    }
}
테스트를 수행해보면 아래와 같이 총 4번의 SQL이 수행되는데 간략하게 설명을 해보면

1. 게시글의 번호(no)가 1인 Post 데이터 조회
2. 해당 Post 데이터의 자식 Entity 조회
3. 해당 Post Entity에서 Comment가 추가됨에 따라 Insert문 수행
4. 저장된 Comment 데이터의 Join 기준이되는 postNo 값을 해당 Post 객체의 No 값으로 Update

그리고 다시 전체 게시글을 조회하는 테스트 로직을 수행해보면 성공적으로 자식 Entity(댓글) 목록이 조회됩니다.


그런데 한가지의 문제가 있습니다.

고작 게시글 목록과 해당 게시글들의 댓글 목록을 조회하는데 예상과는 달리 조금 많은 SQL이 수행되고 있습니다.

이는 Post 목록 조회 → 3개의 데이터가 조회됨 → 3개 각각의 Post의 Comment 목록들을 하나하나 조회가 이루어지기 때문입니다.

그렇다면 만약 Post 데이터가 10,000개라고 가정을 해본다면, 실제 쿼리 수행 횟수는 10,001회가 수행될 것 입니다. 또한 만약 Comment Entity에도 연관 관계를 가지는 자식 Entity가 있다면 그 SQL 수행 횟수는 천문학적으로 늘어날것입니다. 이를 **N + 1 문제**라고 불리고 있습니다.

물론 기능 또는 도메인 특성에 따라 현재와 같은 엔티티 지연 로딩이 적합할 수도 있고 부적합할 수 있는데 이를 해결할 수 있는 방법은 `Fetch Join`, `@EntityGraph` 등이 있는데 비교적 간단하게 적용할 수 있는 Fetch Join으로 해결해보도록 하겠습니다.


Fetch Join (N + 1 Issue) - JPQL
[io.starter.jpatutorial.domain.repository.PostMariaRepository]
@Repository
public interface PostMariaRepository extends JpaRepository<PostJpo, Long> {
    @Query("SELECT P FROM PostJpo P LEFT OUTER JOIN FETCH P.comments")
    List<PostJpo> findAllFetchJoin();
}

여기서 `@Query` 애노테이션에 작성하는 유사 SQL은 JPA 고유의 JPQL이라는 문법을 사용할 수 있습니다.
게시글과 댓글의 연관 관계를 고려하여 Left Outer Join으로 수행하도록 합니다.
[io.starter.jpatutorial.service.PostListService]
@Service
@RequiredArgsConstructor
public class PostListService {
    private final PostMariaRepository postMariaRepository;

    @Transactional(readOnly = true)
    public List<Post> fetch() {
        return postMariaRepository.findAllFetchJoin()
                .stream()
                .map(Post::jpoOf)
                .collect(Collectors.toList());
    }
}

fetch 메소드의 조회 로직을 약간 수정해준 뒤 전체 게시글을 조회하는 테스트 로직을 수행해보면 아래와 같이 한방 쿼리로 이전과 동일한 결과 데이터가 조회되는것을 알 수 있습니다.


JPA Query Methods (쿼리 메소드)

Spring Data JPA는 간편하게 Repository 인터페이스에서의 Method Naming 만으로 간단한 SQL문을 수행해줍니다. 이를 Query Methods라고 합니다.

Query Methods는 이미 정해진 단어 및 SQL 예약어에 따라 메소드의 Naming Rule이 존재합니다. 자세한 설명은 아래 공식 문서를 통해 확인할 수 있습니다.

[Spring Data JPA - Reference Documentation](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods)

----------------------------------------------------------------------------------------------------

JpaRepository를 상속받은 인터페이스에서

메소드명을
findBy컬럼명(@Param("ㅋㅋㅋ") String ㅌㅌㅌ){
}
이렇게 생성하면 findBy뒤에적은 컬럼명으로 조회가 가능함

★findByGender로 검색하고자 한다면 엔티티클래스의 컬럼명도 gender여야하고 DB의 컬럼도 gender여야함
★검색할 컬럼의 값은 고유한 값이어야함

★파라미터명은 아무렇게나 막 해도되고 @Param("")은 안써도 됨(결과가 똑같음)

ex) 컬럼명이 gender일때
findByGender(@Param("gender") String gender){
}

----------------------------------------------------------------------------------------------------


그렇다면 예시로 게시글의 제목이 특정 키워드를 포함하는 게시글의 목록을 조회하는 쿼리를 수행하는 로직을 작성해봅니다.
[io.starter.jpatutorial.domain.repository.PostMariaRepository]
@Repository
public interface PostMariaRepository extends JpaRepository<PostJpo, Long> {
    List<PostJpo> findByTitleContains(String keyword);
}

[io.starter.jpatutorial.service.PostListService]
@Service
@RequiredArgsConstructor
public class PostListService {
    private final PostMariaRepository postMariaRepository;

		@Transactional(readOnly = true)
    public List<Post> fetchByContains(String title) {
        return postMariaRepository.findByTitleContains(title)
                .stream()
                .map(Post::jpoOf)
                .collect(Collectors.toList());
    }
}

[io.starter.jpatutorial.JpaTutorialApplicationTests]
@SpringBootTest
class JpaTutorialApplicationTests {
    @Autowired
    private PostListService postListService;

    @ParameterizedTest
    @ValueSource(strings = "1")
    @DisplayName("게시글의 제목이 특정 키워드를 포함 목록 조회 테스트")
    void fetch(String keyword) {
        List<Post> posts = postListService.fetchByContains(keyword);
        Assertions.assertNotEquals(posts.size(), 0);
        System.out.println("Posts --> " + posts);
    }

}

테스트 코드는 게시글 제목에 숫자 1이 포함되는 게시글의 목록을 조회하는것으로 수행합니다.
테스트 코드 수행시 아래와 같이 임의의 Where Like 구문이 수행되는것을 알 수 있고 결과 데이터도 1이 포함되 있는 데이터 1건이 조회되는것을 알 수 있습니다.


기본적인 가이드는 여기서 마무리하고자 합니다.
실제 Spring Data JPA를 기반으로 실제 서비스를 운영하고 복잡한 비즈니스 로직을 개발하다보면 다양한 문제점이 많이 발생할 수 있습니다.

또한 중요한 개념적 정립이 필요한 사항들도 있습니다.

하지만 레퍼런스는 많고 진영에서의 기술적 지원도 활발하니 문제의 돌파구를 찾기 어렵지는 않을것 같습니다.

----------------------------------------------------------------------------------------------------

Dirty Checking

개요
Entity 조회 → Entity 속성(상태) 변경 → Transaction 커밋 → Update Query 발생
데이터베이스로부터 조회된 Entity를 Programming Level에서 Entity의 속성을 변경하고 Transaction   Commit이 된 경우 변경된 Update 쿼리 발생

원인
JPA는 트랜잭션 종료 시점에 Entity 조회 시점 기준의 Entity들 중 변화가 있는 Entity를 데이터베이스에 자동으로 반영함.
→ JPA에서는 엔티티를 조회하면 해당 엔티티의 조회 상태 그대로 스냅샷을 만들어놓는다.
그리고 트랜잭션이 끝나는 시점에는 이 스냅샷과 비교해서 다른점이 있다면 Update Query를 데이터베이스로 전달함.

문제점
Dirty Checking으로 생성되는 update 쿼리는 기본적으로 모든 필드를 업데이트 한다.
→ JPA에서는 전체 필드를 업데이트하는 방식을 기본으로 사용한다.
그래서 이런 경우엔 @DynamicUpdate로 변경된 필드만 갱신되도록 할 수 있습니다.

@Convert

QueryDSL


null이 아닐때만 DB에 save()하는법
memberJpo.getName() != null) {
	jpo.setName(memberJpo.getName());
}
if (memberJpo.getNickname() != null) {
	jpo.setNickname(memberJpo.getNickname());
}
if (memberJpo.getEmail() != null) {
	jpo.setEmail(memberJpo.getEmail());
}
if (memberJpo.getPassword() != null) {
	jpo.setPassword(memberJpo.getPassword());
}
if (memberJpo.getGender() != null) {
	jpo.setGender(memberJpo.getGender());
}

setXXX를 하면 자동으로 save()가 되기때문에 save()메소드를 따로 쓸 필요는 없음.
변경된 값이 없을 경우는 쿼리가 실행되지 않음

----------------------------------------------------------------------------------------------------

JPO에서 enum 쓸때 0,1,2... 대신 문자열(String)로 저장되게 하려면 컬럼에 다음 어노테이션 붙이기

@Enumerated(EnumType.STRING)

----------------------------------------------------------------------------------------------------

<날짜시간 자료형>

MySQL의 DATETIME 자료형은 java.util.Data를 쓰면 됨
MySQL의 시간 자료형은 String을 쓰거나 LocalTime 쓰기

----------------------------------------------------------------------------------------------------

로직 이해

XXXController or XXXTest 에서 XXXService를 불러오고
XXXService에서는 XXXRepository를 불러옴. JpaRepository에서 상속받은 findAll, findById 등 기본 메소드 이외에도 추가 가능함.

보통 insert / update를 XXXTest에서 많이 하는듯

-----

1대다 관계일때는 부모JPO에 List컬럼을 만들고 거기에 @OneToMany를 붙이고,

연관관계를 만들기 위해 @JoinColumn(name = "n쪽 테이블의 외래키컬럼명")을 붙임. 해당 컬럼을 외래키로 쓰겠다는 뜻
그럼 save() 시 해당 컬럼에는 부모테이블의 기본키(@ID)컬럼의 값이 들어감

글고 (fetch = FetchType.LAZY) 붙여서 지연 select되게 해주고?
글고 조회 했을때 컬럼이 생성되지 않도록 @ToString.Exclude 를 붙인다

ex)
@ToString.Exclude
@OneToMany(fetch = FetchType.LAZY)
@JoinColumn(name = "member_id")
private List<CommentJpo> comments;


1대다 관계일때는 JPO, DTO, fetch join 모두 써서 해야함 (속성의 일부만 받기위해서 DTO를 만듦)
아래는 패치조인쿼리 (XXXRepository에 넣기)
@Query("SELECT DISTINCT M FROM MemberJpo M LEFT OUTER JOIN FETCH M.comments ORDER BY M.id")
List<MemberJpo> findFetchJoin();

불러와지는 데이터는 똑같지만 쿼리를 한번만 날리기 위해서 'FETCH' 키워드를 넣음

DISTINCT를 쓰면 결과를 하나만 불러옴. 쿼리를 보내는 갯수는 똑같음

일단 다 받아온다음에, DTO로 필요한것만 남도록 빼거나 추가하는것

-----

인수 받아서 일부만 가져오고 싶으면 아래처럼 조건문을 쿼리에 넣으면 됨.
파라미터는 :파라미터1 이렇게 콜론 붙여서 써야되고
일단 @Query를 쓰면, 메소드네임쿼리는 무효화됨.

@Query("SELECT DISTINCT M " +
		"FROM MemberJpo M LEFT OUTER JOIN FETCH M.comments " +
		"WHERE M.name = :name " +
		"AND M.email = :email " +
		"ORDER BY M.id ASC")
List<MemberJpo> findByNameAndEmail(String name, String email);

----------------------------------------------------------------------------------------------------

JPQL(Java Persistence Query Language)

----------------------------------------------------------------------------------------------------

fetchJoin

----------------------------------------------------------------------------------------------------

checking

----------------------------------------------------------------------------------------------------

querydsl

https://devkingdom.tistory.com/243

-----

querydsl config

-----

querydsl repository

----------------------------------------------------------------------------------------------------


Member(1) : Car(N) 관계의 테이블이 있다고 할때

Member의 자동차 목록을 가져오기위해선 List<Car> cars 필드값이 필요함.
이를 Member → Car 단방향 참조라고 함

반대로 Car엔티티만 존재할때, 이 자동차의 소유를 알고 싶으면 Member member필드값이 필요한데
이것 역시 Car → Member 단방향 참조임

이렇게 Member ↔ Car 처럼 각 엔티티가 서로를 단방향으로 참조하고 있는걸 양방향 참조라고 함
성능상 문제도 없는데 전부 양방향으로 참조하면 되지 않을까? 하는 생각이 들 수도 있지만
양방향 참조를 한다는건 엔티티의 필드 갯수가 그만큼 늘어난다는 것을 의미함

특히 사용자를 나타내는 User/Member/Account 등의 엔티티가 모든 엔티티에 대해 참조를 해버리면 필드 갯수가 어마어마하게 많은 복잡한 클래스가 될것임
그렇기때문에 엔티티를 설계할 때 참조가 꼭 필요하지 않은 상황이라면 단방향참조만 하는게 좋음

-----

양방향 매핑은 반대방향으로 조회(객체 그래프 탐색) 기능이 추가된 것 뿐

-----

양방향 연관관계 설정시 ToString 때문에 무한루프가 발생할 수 있음

해당 외래컬럼에 @ToString.Exclude 를 붙여서 방지

----------------------------------------------------------------------------------------------------

@~~To~~(mappedBy = "") 속성

양방향 관계 연결시 씀
mappedBy 선언시 양방향 연결 관계가 됨

-----

@OneToMany(mappedBy = "cellularPhone") 
	private User user;

mappedBy : 나는 cellularPhone에 의해서 관리가 된다 : User 객체의 cellularPhone 변수에 의해서 관리된다.

----------------------------------------------------------------------------------------------------

<1:1 단방향>
@Table(name = "user")
public class User extends DateAudit {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "user_id", unique = true, nullable = false)
    private Long id;

    private String username;
    ...(생략)...

    @OneToOne
    @JoinColumn(name = "phone_id") // 여기에는 자식의 DB컬럼명을 써야함
    private CellularPhone cellularPhone;
		...(생략)...
}
@Table(name = "cellular_phone")
public class CellularPhone extends DateAudit {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "phone_id")
    private Long id;

    private String phoneNumber;

    private String model;
		...(생략)...
}

-----

저장하고 조회

@Test
public void save_user_phone() {
  CellularPhone cellularPhone = CellularPhone.builder()
    .model("android")
    .phoneNumber("010-2342-5234")
    .build();
  phoneRepository.save(cellularPhone);

  User user = User.builder()
    .name("Frank")
    .email("sdf@sdf.com")
    .username("id1234")
    .password("1234")
    .build();
  
  user.setCellularPhone(cellularPhone); //연관관계를 맺음

  userRepository.save(user);

  List<User> users = userRepository.findAll();
  assertThat(users.get(0).getName()).isEqualTo("Frank");
  assertThat(users.get(0).getCellularPhone().getPhoneNumber()).isEqualTo("010-2342-5234");
}


<1:1 양방향>


----------------------------------------------------------------------------------------------------

연관관계 편의 메소드

Team team = Team.builder()
    .name("TeamA")
    .build();

teamRepository.save(team);

Member member = Member.builder()
    .username("member1")
    .team(team)
    .build();

team.getMembers().add(member);

이런식으로, Member에 한줄을 넣어주기 보다 → 연관관계 편의 메소드를 생성하자

Member에서 team을 set 해줄때 설정해버린다. - 하나면 세팅해도 두개가 같이 세팅이 되게!

----------------------------------------------------------------------------------------------------

CascadeType.ALL
상위 엔터티에서 하위 엔터티로 모든 작업을 전파

CascadeType.PERSIST
하위 엔티티까지 영속성 전달
Person Entity를 저장하면 Address Entity도 저장

CascadeType.MERGE
하위 엔티티까지 병합 작업을 지속
Address와 Person 엔티티를 조회한 후 업데이트

CascadeType.REMOVE
하위 엔티티까지 제거 작업을 지속
연결된 하위 엔티티까지 엔티티 제거

CascadeType.REFRESH
데이터베이스로부터 인스턴스 값을 다시 읽어 오기(새로고침)
연결된 하위 엔티티까지 인스턴스 값 새로고침

CascadeType.DETACH
영속성 컨텍스트에서 엔티티 제거
연결된 하위 엔티티까지 영속성 제거

----------------------------------------------------------------------------------------------------

@Transient

해당 데이터를 테이블의 컬럼과 매핑 시키지 않는다.

"컬럼을 제외한다.” 라기보다 "영속 대상에서 제외" 시키기 위해 사용한다

----------------------------------------------------------------------------------------------------

포트 변경 (기본: 8080)

★.yml
server:
  port: 5555

★.properties
server.port = 5555

----------------------------------------------------------------------------------------------------

스프링부트에서 view페이지 만들기

spring-boot-starter-web 포함된 tomcat은 JSP엔진을 포함하고 있지 않음.
때문에 jsp를 적용하기 위해서는 아래와 같은 의존성을 추가해야함
Maven Update 필요

★pom.xml
<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>jstl</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.tomcat.embed</groupId>
	<artifactId>tomcat-embed-jasper</artifactId>
</dependency>


★build.gradle 
dependencies {
	implementation 'javax.servlet:jstl'
	implementation "org.apache.tomcat.embed:tomcat-embed-jasper"
}


뷰 경로 지정
앞서 말했듯이 스프링 부트에서 jsp를 기본 지원하지 않기 때문에 아래와 같은 정보를 application.properties에 설정해서

스프링 부트에게 jsp 뷰의 경로를 알려주어야 한다.

★application.properties
spring.mvc.view.prefix=/WEB-INF/
spring.mvc.view.suffix=.jsp

★application.yml
spring:
	mvc:
		view:
			prefix: /WEB-INF/
			suffix: .jsp

----------------------------------------------------------------------------------------------------

Thymeleaf(타임리프)

백엔드에서 html을 동적으로 랜더링하는 기능
컨트롤러에서 HttpServletRequest으로 보낸걸 html에서 받을 수 있음

------------------------------

의존성 추가

implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'

------------------------------

html 태그에 속성 추가 (안해도 동작이 되긴하는듯. 이 속성을 넣으면 IDE에서 자동완성이 됨(태그의 속성으로 th까지만 입력해보기))

<html xmlns:th="http://www.thymeleaf.org">

------------------------------

사용법

-----

문자열 출력

<p th:text="${변수}"></p>

-----

객체에서 찾을때는 게터를 만든후 get뒤에 소문자를 쓰면 되고,

Map은 key를 쓰면 됨

ex) 객체 or Map
${member.name}

-----

변수와 문자열 합치기

대괄호 이용 : <span>hello [[${변수}]]</span>
파이프라인 이용 : <span th:text="|asdf ${변수}|"></p>
홑따옴표, + 이용 : <span th:text="'asdf '+${변수}"></p>

-----

★href속성에 집어넣기 : <a th:href="${a}"></a>

-----

<p th:if="${condition}">이 요소는 조건이 참일 때만 나타납니다.</p>

-----

반복문

<h1>회원 목록</h1>
<ul>
	<li th:each="member : ${members}">
		<span th:text="${member.name}"></span>
	</li>
</ul>

------------------------------

thymeleaf의 장점

-----

jsp 스크립틀릿이나 JSTL 등의 경우 html 중간에 if문이나 for문 등이 들어가는데

ex) 스크립틀릿
<div>
	<% 
		for(int i=0; i<10; i++){
	%>	
			<p id="demo1">
				P Tag <%=i+1%>
			</p>		 
	<%
		}
	%>
</div>

ex) JSTL(& EL)
<div>
	<c:forEach var="i" begin="1" end="5">	
		<p id="demo1">
			P Tag ${i}
		</p>		 
	 </c:forEach>
</div>

-----

타임리프는 html을 깨지 않고 그대로 쓸 수 있음 (html파일이라 웹 브라우저로 그냥 열어서 랜더링 되기 전 상태를 볼 수도 있음)

ex) thymeleaf
<div>
	<p id="demo1" th:each="number : ${#numbers.sequence(1, 10)}" th:text="|P Tag ${number}|"></p>
</div>

----------------------------------------------------------------------------------------------------

src/main/resources/static 경로에

index.html 파일을 올려두면 Welcome page 기능을 제공함

-----

컨트롤러에서 경로를 입력하면
src/main/resources/templates 경로에서 html파일을 찾음 ('viewResolver'가 찾아줌)

return "hello.html"
이렇게 입력하면

src/main/resources/templates/hello.html 를 찾음

----------------------------------------------------------------------------------------------------

spring-boot-devtools 라이브러리를 추가하면,
html 파일을 컴파일만 해주면 서버 재시작 없이 View 파일 변경이 가능함

인텔리제이 컴파일방법 : 메뉴 build → Recompile

----------------------------------------------------------------------------------------------------

빌드

1. 터미널에서 프로젝트 폴더로 들어가기

2. ./gradlew build 입력
그럼 build 폴더가 생김

3. cd build/libs 들어가기
프로젝트명-0.0.1-SNAPSHOT.jar 가 생겨있음

5. java -jar 프로젝트명-0.0.1-SNAPSHOT.jar 입력
인텔리제이에서 실행했을때와 마찬가지로, 스프링 로고랑 포트가 시작되었다고 나옴

6. 주소창에 포트 입력해서 접속되는거 확인

7. 잘 안되면 ./gradlew build 대신 ./gradlew clean build 하면 됨
그럼 build 폴더가 없어졌다가 다시 빌드됨

----------------------------------------------------------------------------------------------------

정적 컨텐츠 (프로그래밍을 할수없는 페이지)

src/main/resources/templates 폴더에 넣어 템플릿 엔진과 연계할때와는 다르게
src/main/resources/static 폴더 안에 hello-static.html을 만들고, 브라우저에서 localhost:8080/hello-static.html이렇게 치면 정적 페이지가 로드됨

그럼 내장톰캣서버가 요청을 받아서 컨트롤러를 한번 거쳤다가 hello-static컨트롤러가 없으면
resources/static/hello-static.html을 찾음. 있으면 그대로 반환해줌

참고로 static폴더안에 있는 html파일은 서버를 껏다키지 않고도 build > Recompile '~.html' (cmd + shift + f9) 로 즉시반영이 가능함

templates폴더 안에있는 html파일도 서버를 껏다키지 않고도 반영시킬 수 있는데 spring-boot-devtools 라이브러리를 넣으면 됨
서버 재실행 했을때 로그창에 restartedMain들이 찍혀있다면 devtools 세팅이 잘 된거임
이제 build > Recompile '~.html' (cmd + shift + f9)로 즉시반영이 가능해짐

----------------------------------------------------------------------------------------------------

테스트 케이스

------------------------------

스프링 부트에는

src/main 패키지가 있고
src/test 패키지가 있음

테스트 클래스를 생성할때는
src/test 패키지에 똑같은 경로로 클래스 생성(클래스명은 원래클래스(src/main안에있는 테스트할 클래스)명 뒤에 "Test" 를 붙여서 생성)

------------------------------

메소드에 @Test 어노테이션을 붙이면 main메소드 실행하듯이 바로 메소드 실행이 가능함

메소드 단위,
클래스 단위,
패키지 단위

모두 테스트(실행)가 가능

------------------------------

기대값과 결과값을 대조해서 다를 경우 실행시 오류를 발생 & 오류메시지 출력 시키도록 할 수 있음

-----

org.junit.jupiter.api의 Assertions 클래스의 assertEquals 스태틱메서드를 사용하는 방법

Assertions.assertEquals(기대값, 결과값);

-----

org.assertj.core.api의  Assertions 클래스의 assertThat 스태틱메서드를 사용하는 방법

Assertions.assertThat(기대값).isEqualsTo(결과값)

------------------------------

한 클래스의 필드를 여러 메소드에서 참조해서 사용하는 경우 테스트 메소드들의 실행순서에 의해서 결과가 내가 원하는 결과와 다르게 나올수 있음.
모든 테스트는 순서와 상관없이 메소드별로 따로 동작되게끔 설계해야함

예를들어서 아래와 같이 repository 라는 멤버 변수(필드)가 있다고 할때
여러 메서드에서 필드로 선언된 인스턴스 변수(repository)를 참조할 경우 다른 메소드에 의해 인스턴스(repository)의 상태가 바뀌게 됨

class MemoryMemberRepositoryTest {
	MemoryMemberRepository repository = new MemoryMemberRepository();

	@Test
	public void save(){
		...
		repository.save(member);

		Member result = repository.findById(...).get();
		...
		org.assertj.core.api.Assertions.assertThat(member).isEqualTo(result);
	}

	@Test
	public void findByName(){
		...
		repository.save(member1);
		...
		repository.save(member2);

		Assertions.assertEquals(member2, repository.findByName(...).get());
	}

	@Test
	public void findAll(){
		repository.save(...);
		...
		Assertions.assertEquals(2, repository.findAll().size());
	}
}

그래서 이런일이 발생되지 않도록 메소드 실행이 끝난 후 공용 객체의 상태를 리셋시켜야함

그 방법은 아래와 같음

MemoryMemberRepository 클래스에서
public void clearStore(){
	store.clear();
}
이런식으로 객체의 상태를 초기화해주는 메서드를 하나 만들어놓고 (멤버변수가 컬렉션이라면 컬렉션멤버변수.clear(); 이런식으로)

테스트 클래스에서 메서드를 하나 만들고,
@AfterEach 어노테이션을 붙이면 됨.

그럼 @AfterEach 가 붙은 메서드의 내용이
각각의 메서드가 끝날 때마다 실행됨

ex)
class MemoryMemberRepositoryTest {
	MemoryMemberRepository repository = new MemoryMemberRepository();

	@AfterEach
	public void afterEach(){
		repository.clearStore();
	}

	@Test
	public void save(){
		...
	}

	...
}

------------------------------

테스트 케이스 쉽게 만드는 방법

클래스 파일열고 (커서는 아무곳에나 놔도 됨) cmd + shift + t → enter

테스트 라이브러리: JUnit5
클래스 이름: 기본값(현재 클래스명)
테스트하고싶은 메서드 선택한 후 확인

그럼 테스트 패키지에서 똑같은 경로로 뒤에 Test가 붙은 클래스가 생성되고
선택했던 클래스의 메서드들과 똑같은 이름의 메서드들이 void반환타입으로 생성됨

즉 테스트 케이스 껍데기를 편리하게 만들 수 있음

------------------------------

테스트 메서드는 한글로 사용해도 됨

직관적으로 쉽게 알아들을 수 있음

빌드될때 src/test 디렉토리에 위치한 테스트 클래스들은 포함되지 않음(실제 애플리케이션의 빌드나 배포에는 영향을 주지 않음)

------------------------------

테스트 메서드를 만들때 given/when/then 으로 나눠서 만들면 복잡한 테스트도 쉽게 만들 수 있음

//given(어떤 환경이 주어졌을때)
Member member = new Member();
member.setName("aaa");

Member member2 = new Member();
member2.setName("aaab");

//when(어떻게 하면)
Long saveId = memberService.join(member);

//then(이렇게 되어야 한다)
Member findMember = memberService.findOne(saveId).get();
Assertions.assertEquals(member.getName(), findMember.getName());

------------------------------

테스트케이스 작성시 보기 편하게 DisplayName 어노테이션으로 한글 테스트제목을 쓸 수 있음(테스트창에 뜰 테스트제목을 이 어노테이션으로 변경가능)

@Test
@DisplayName("VIP가 아니면 할인이 적용되지 않아야 한다")
void vip_x() {

------------------------------

예외를 발생시키는걸 테스트를 하려면 아래처럼 하면 됨

//given
Member member = new Member();
member.setName("aaa");

Member member2 = new Member();
member2.setName("aaa");

//when
memberService.join(member);
try {
	memberService.join(member2);
	Assertions.fail("예외가 발생해야 합니다");
} catch (Exception e) {
	Assertions.assertEquals(e.getMessage(), "이미 존재하는 회원입니다");
}

------------------------------

try-catch 문을 안쓰고 하는 방법이 있음 (Assertions.assertThrows 메서드 사용)

첫번재인수로 터져야하는 예외 클래스리터럴(클래스명.class)을 넣고
두번째인수로 예외가 발생되어야 하는 메서드를 넣으면 됨

Assertions.assertThrows(NoSuchBeanDefinitionException.class,
	() -> ac.getBean("xxxxx", MemberService.class));

------------------------------

발생해야 할 예외가 발생하지 않았거나
다른 예외가 발생했을 경우

테스트가 실패되며아래와같이 나옴

<발생해야 할 예외가 발생하지 않은 경우>
org.opentest4j.AssertionFailedError: Expected java.lang.IllegalStateException to be thrown, but nothing was thrown.

<다른 예외가 발생한 경우>
org.opentest4j.AssertionFailedError: Unexpected exception type thrown, 
필요:class java.lang.NullPointerException
실제   :class java.lang.IllegalArgumentException

그리고 발생해야할예외가 발생하지 않은부분의 라인도 함께 출력됨
at hello.hellospring.service.MemberServiceTest.중복회원예외(MemberServiceTest.java:39)

------------------------------

Assertions.assertThrows 메서드는 예외객체를 반환함

이를 이용해 오류가 발생했을때 오류메시지도 정확하게 출력되는지 확인 가능함

IllegalStateException illegalStateException = assertThrows(IllegalStateException.class, () -> memberService.join(member2));
Assertions.assertEquals("이미 존재하는 회원입니다", illegalStateException.getMessage());

------------------------------

Assertions.assertThat(객체1).isSameAs(객체2) // == 비교랑 동일
Assertions.assertThat(객체1).isEqualTo(객체2) //  .equals() 비교랑 동일

----------------------------------------------------------------------------------------------------

서비스 클래스는 기능들의 결과물이라고 생각하고 비즈니스에 가까운 네이밍을 하는게 관습

insert X
join O

findAll X
findMembers() O

서비스는 비스니스에 의존적으로 설계를 하고
리파지토리 같은 경우는 단순히 기계적으로 개발스럽게 용어들을 선택함

"단순히 데이터를 넣어" 이게 리파지토리의 역할이기 때문

----------------------------------------------------------------------------------------------------

스프링은 스프링컨테이너에 스프링 빈 이라는 @Component가 붙은 클래스의 객체들을 등록해놓고 필요할때 주입을 시킬 수 있음.

단, 메인 클래스(@SpringBootApplication이 붙은 클래스) 를 기준으로 형제&하위 패키지만 뒤짐
상위 패키지에 @Component가 붙은 클래스가 있어도 인식되지 않음

이때 스프링빈은 싱글톤으로 등록(싱글톤으로 등록(유일하게 하나만 등록해서 공유)됨. 따라서 같은 스프링 빈이면 모두 같은 인스턴스임

------------------------------

@Autowired 어노테이션을 붙이면 스프링 빈들끼리의 연관관계(화살표) 를 설정해줌

------------------------------

@Component가 들어있는 어노테이션(@Service, @Reposirory) 등은 인터페이스에 쓰는게 아닌,
인스턴스를 생성할수 있는(new 연산자를 쓸 수 있는) 클래스인 구현체(implement 한 클래스)에 써야함

----------------------------------------------------------------------------------------------------

@Component를 안쓰고 직접 만드는 방법

1. 메인클래스(@SpringBootApplication가 붙은 클래스) 와 동일 선상에 SpringConfig 클래스를 생성

2. @Configuration 과 @Bean 어노테이션 사용
@Configuration
public class SpringConfig {
	@Bean
	public MemberService memberService(){
		return new MemberService();
	}
}

위처럼 하면 스프링이 뜰때 @Configuration을 읽고, @Bean 이 붙은 메서드를 실행해서 반환되는 객체를 스프링빈으로 등록해줌

-----

의존관계일경우 아래처럼 하면 됨

@Configuration
public class SpringConfig {
	@Bean
	public MemberService memberService(){
		return new MemberService(memberRepository());
	}

	@Bean
	public MemberRepository memberRepository(){
		return new MemoryMemberRepository();
	}
}

컨트롤러는 어쩔수없이 @Controller 어노테이션을 써야함. @Autowired 도 메서드에 붙여서 주입을 시켜야함

@Controller
public class MemberController {
	private final MemberService memberService;

	@Autowired
	public MemberController(MemberService memberService) {
		this.memberService = memberService;
	}
...

-----

실무에서는 주로

1. 정형화된(일반적으로 작성하는) 컨트롤러, 서비스, 리파지토리 같은 코드는 컴포넌트스캔을 사용함(@Service / @Repository)
2. 정형화되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다(@Configuration / @Bean)

------------------------------

필드 주입 / 생성자 주입 / 세터 주입

-----

필드주입 예시

@Autowired
private MemberService memberService;

★필드 주입이 권장되지 않는 이유
필드주입으로 하면 스프링이 뜰때 바로 넣어지기때문에, 바꿀수 있는 방법이 없음

-----

세터주입 예시

private MemberService memberService;

@Autowired
public void setMemberService(MemberService memberService) {
	this.memberService = memberService;
}

생성은 생성대로 되고 나중에 setter를 통해 값이 들어감
★단점은 한번 세팅을 하면 바꿀일이 없는데, public으로 열려있어서 노출이 됨. 그래서 추후 잘못 바뀌게 되면 문제가 생김
애플리케이션 로딩시점(조립시점, 스프링 컨테이너에 올라가는 시점)에 바뀌어야 되는 것임. 한번 세팅이 되면 바꿀일이 없음. 의존관계가 실행중에 동적으로 변하는 경우는 거의(아예) 없음
만약 그럴 일이 있을때는 설정을 바꿔서 서버를 다시 실행시키는게 맞음

-----

생성자주입 예시

private final MemberService memberService;

public MemberController(MemberService memberService) {
	this.memberService = memberService;
}

장점1. 중간에 조작이 가능해져서 좋음
장점2. 생성하는 시점에 딱 넣고 그 다음부터는 변경을 못하도록 막을 수 있음

----------------------------------------------------------------------------------------------------

h2 db

설치 방법

1. h2 database 검색후 사이트 접속
2. Download부분에 All platforms 클릭해서 다운
3. 압축 풀기
4. h2폴더→bin폴더로 가서 터미널 열기
5. chmod 755 로 h2.sh 파일에 읽기 권한 부여
6. ./h2.sh 입력해서 실행
7. 브라우저에 h2콘솔이 열림
8. 바로 Connect 누르기. 오류가 날 경우 해당 경로에 touch명령어로 test.mv.db 파일을 직접 만들고 다시 Connect 클릭
9. 접속이 잘 되는걸 확인
10. 여러곳에서 접속이 가능케 하기 위해 다시 나와서 JDBC URL 을 변경하기(이렇게 하면 파일을 직접 접근하는게 아닌 TCP/IP 프로토콜을 사용하여 접속하게 됨
이렇게 해야 여러군데에서 접근이 가능함)
jdbc:h2:~/test → jdbc:h2:tcp://localhost/~/test

만약 H2 콘솔이 안들어가지면 IP부분을 localhost 로 바꾸기
http://ip:포트/login.jsp?~~~ → http://localhost:포트/login.jsp?~~~

------------------------------

테이블 생성

drop table if exists member CASCADE;
create table member(
	id bigint generated by default as identity,
	name varchar(255),
	primary key(id)
)

이때 generated by default as identity 는 오라클의 시퀀스, mySQL의 오토인크리먼트랑 같음

------------------------------

조회

SELECT 문 써도 되고
'SQL문 입력창이 비어있는 상태에서' 왼쪽 메뉴에서 테이블을 클릭하면 SELECT문이 자동으로 입력됨 (SQL문 입력창에 내용이 있는 상태에서 테이블을 클릭하면 그냥 테이블명만 삽입됨)

------------------------------

h2 db 스프링과 연결

1. 의존성 추가
implementation 'org.springframework.boot:spring-boot-starter-jdbc'
runtimeOnly 'com.h2database:h2'

2. application.properties 에서 내용 입력
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver

빨간불이 뜬다면 gradle 리로드


3. 리파지토리 구현체(implements 연산자 쓴 파일)에서 db연결
private final DataSource dataSource;

그다음 스프링한테 주입받아야함(생성자 생성하기)

참고로 application.properties 에서 세팅(설정)을 해놓으면 스프링이 DataSource(데이터소스: 애플리케이션에서 DB와 연결하는 기능)라는걸 만들어 놓음

참고로 데이터소스 객체에 .getConnection() 메소드를 사용해 DB커넥션(DB와 애플리케이션 사이의 연결)을 얻을 수 있음
public JdbcMemberRepository(DataSource dataSource) {
	this.dataSource = dataSource;
	dataSource.getConnection();
}

근데 위에 처럼 getConnection()을 쓰면 안되고 아래처럼 써야함. 물론 이 방법은 모두 순수 JDBC로 할때 이야기고, 스프링으로 하면 이런 코드를 쓸 필요 없음
DataSourceUtils.getConnection(dataSource객체);

릴리즈(닫기)할때도 아래처럼 닫아야함
DataSourceUtils.releaseConnection(커넥션객체, dataSource객체);

------------------------------

만약
메모리에 저장하는 방식 → DB에 저장하는 방식
이렇게 바꾼다고 할때
서비스를 수정할 필요 없이, 서비스에서 사용하는 인터페이스를 구현하는 클래스를 새로 추가해서 SpringConfig로 의존성을 주입해주기만 하면 됨

클래스를 만들고,

기존에 아래처럼 되어있던걸
@Configuration
public class SpringConfig {
	@Bean
	public MemberService memberService(){
		return new MemberService(memberRepository());
	}

	@Bean
	public MemberRepository memberRepository(){
		return new MemoryMemberRepository();
	}
}

아래처럼 갈아끼우기만 하면 됨
MemoryMemberRepository 에서 JdbcMemberRepository 라는, 같은 인터페이스를 구현하는 클래스로 바꿔준것이고, db를 써야하니 DataSource의존성까지 추가해야함
@Configuration
public class SpringConfig {
	private DataSource dataSource;

	public SpringConfig(DataSource dataSource) {
		this.dataSource = dataSource;
	}

	@Bean
	public MemberService memberService(){
		return new MemberService(memberRepository());
	}

	@Bean
	public MemberRepository memberRepository(){
		return new JdbcMemberRepository(dataSource);
	}
}

즉 MemberService는 MemberRepository를 의존하고 있고,
MemberRepository의 구현체로는 MemoryMemberRepository와 JdbcMemberRepository가 있음

기존에는 MemoryMemberRepository를 스프링빈으로 등록을 했다면 원래 등록되어있던걸(MemoryMemberRepository) 뺴고, JdbcMemberRepository를 등록한 것

그럼 나머지는 손댈게 하나도 없음. JdbcMemberRepository로 바껴서 프로그램이 잘 돌아가게 됨

이걸 SOLID 원칙중에서 개방-폐쇄 원칙을 지켰다고 함 (jdbc기반의 memberRepository(JdbcMemberRepository)를 만들었지만 기존 코드는 하나도 손댈 필요가 없었기 때문)

기존 코드를 전혀 손대지 않고, 스프링 설정만으로 구현 클래스를 변경할 수 있음

아무튼 MemoryMemberRepository에서 JdbcMemberRepository로 바꿨기 때문에, 데이터를 DB에 저장하므로 스프링 서버를 재실행해도 데이터가 안전하게 저장됨

----------------------------------------------------------------------------------------------------

통합테스트

스프링컨테이너랑 DB까지 연동해서 테스트하는걸 보통 통합테스트라고 말함
(단위테스트는 반대로 스프링 안쓰고 순수하게 자바 코드로 하면서 최소한의 단위로 하는것. 단위단위로 쪼개서 테스트할수 있도록 하고 스프링컨테이너 없이 테스트할 수 있도록 훈련해야함.
그게 좋은 테스트일 확률이 높음. 물론 통합테스트도 필요할 수 있음. 하지만 단위테스트를 잘 만드는게 훨씬더 좋음)


1. 클래스에 @SpringBootTest 붙이기
ex)
@SpringBootTest
class MemberServiceIntegrationTest {

참고: @SpringBootTest 애노테이션은 스프링 컨테이너와 테스트를 함께 실행하기 위해 씀


2. 클래스에 @Transactional 붙이기

참고: @Transactional 애노테이션은 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백됨
트랜잭션 시작하고 테스트메서드가 하나 끝나면 롤백하고, 또 트랜잭션 시작하고 다음 테스트가 하나 끝나면 롤백하고... 이런식으로 테스트메서드마다 일일이 반복동작됨
이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않음
(테스트케이스에 붙었을때만 이렇게 동작함. 서비스같은데 붙으면 롤백하지 않고 정상적으로 동작함)
(테스트메서드에 @Commit을 붙이면 해당 메서드는 롤백되지않고 커밋됨)


3. @BeforeEach 를 지우고, 스프링컨테이너한테 내놔 해야함
테스트에서는 생성자주입을 쓰지 않고 필드주입(@Autowired)로 보통 씀(편하기 때문에. 다른곳에서 테스트클래스를 쓰지 않고, 현재 테스트클래스 내에서만 실행하고 끝날 것이기 때문에)
ex)
@SpringBootTest
@Transactional
class MemberServiceIntegrationTest {
	@Autowired MemberService memberService;
	@Autowired MemoryMemberRepository memberRepository;
.
.

4. 필드부분에서, 구현클래스 → 인터페이스로 변경하기
ex)
@Autowired MemoryMemberRepository memberRepository;
↓↓↓
@Autowired MemberRepository memberRepository;

이때 SpringConfig에 아래처럼 설정이 당연히 되어있어야 함
@Configuration
public class SpringConfig {

	private DataSource dataSource;

	public SpringConfig(DataSource dataSource) {
		this.dataSource = dataSource;
	}

	@Bean
	public MemberService memberService(){
		return new MemberService(memberRepository());
	}

	@Bean
	public MemberRepository memberRepository(){
		return new JdbcMemberRepository(dataSource);
	}
}


5. @AfterEach부분 지우기
메모리에 있던 데이터를 다음 테스트에 영향이 없게끔 지워주는 코드 를 지우기(@Transactional로 대체 가능)
@AfterEach
void afterEach(){
	memberRepository.clearStore();
}

----------------------------------------------------------------------------------------------------

테스트 클래스 실행시 실행창에서 트리형태로

MemberServiceTest
	회원가입()
	중복회원예외()
	.
	.

이런식으로 클래스명 밑에 메서드명들이 보여지고 있을텐데
여기서 메서드를 클릭하면 해당 메서드와 관련된 로그만 볼 수 있음

----------------------------------------------------------------------------------------------------

테스트에서의 @Transactional 어노테이션

테스트를 실행할때 먼저 트랜잭션을 실행을 하고
DB에 쿼리를 날릴거 다 날린다음에
테스트가 다 끝나면 Rollback을 해줌

그래서 DB에 넣었던 데이터들이 다 깔끔하게 지워짐. 즉, 다음 테스트를 또 반복해서 실행할 수 있게됨(테스트가 끝날때마다 수동으로 데이터를 지우지 않아도 됨)


반대로 테스트가 끝난 후에도 수정했던것들이 유지되게 하려면 @Transactional 어노테이션을 지우기

----------------------------------------------------------------------------------------------------

JPA

JPA는 자바 진영의 표준 인터페이스고 구현체로는 Hibernate, EclipseLink, OpenJPA 등이 있는데 거의 Hibernate만 쓴다고 보면 됨

JPA는 ORM(Object Relational Mapping, 객체 관계 매핑)이라는 기술임. 프로그래밍 언어와 RDB(Relational Database, 관계형 DB)의 데이터를 자동으로 매핑(연결) 해주는 도구임

------------------------------

SpringBoot + JPA 사용법

1. build.gradle에서 의존성 추가 후 gradle새로고침
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'

참고로
~~스프링부트스타터~~data-jpa 가
~~스프링부트스타터~~jdbc 까지 포함함


2. 라이브러리가 잘 받아졌는지 확인
프로젝트창 > External Libraries(외부 라이브러리) 에서 hibernate 입력했을때 검색이 돼야함


3. application.properties에 jpa와 관련된 설정 추가

아래 설정코드 추가 시 jpa가 날리는 sql문을 볼 수 있음
spring.jpa.show-sql=true

아래 설정코드 추가 시 자동으로 테이블을 생성하는걸 끔
spring.jpa.hibernate.ddl-auto=none

spring.jpa.hibernate.ddl-auto의 값
validate : Hibernate는 유효성 검사만 함. 즉, 애플리케이션과 DB스키마가 일치하는지 확인만 함
none : Hibernate는 DB스키마에 아무런 작업도 수행하지 않음. DB스키마를 수동으로 관리해야함
create : Hibernate는 DB스키마를 삭제하고 새로 생성함. 애플리케이션을 시작할 때마다 스키마가 재생성됨. 개발 및 테스트 시에만 사용하기
create-drop : create와 비슷하게 DB스키마를 생성하며, 애플리케이션 종료시 스키마를 다시 삭제함. 주로 테스트 시에 임시 DB를 만들 때 사용함
update : Hibernate는 DB스키마를 변경하며, 기존 데이터는 보존됨. 하지만 스키마 변경은 신중하게 고려되어야 하며, 어쨌든 테이블 설계를 바꾸는것이므로
	프로덕션 환경에서는 잠재적인 위험과 영향을 신중하게 평가해야함

참고로 spring.jpa.hibernate.ddl-auto의 기본값은
Spring Boot 2.0 이전 = validate
Spring Boot 2.0 이후 = none


4. JPA를 쓰려면 먼저 엔티티(DB테이블과 일치하는 자바 객체)를 매핑해야함

아래처럼 클래스에 @Entity를 붙이면 이제부터 JPA가 관리하는 엔티티가 됨

@Entity
public class Member {
	private Long id;
	private String name;
	게터
	세터
	.
	.


5. PK 매핑

아래처럼 @Id를 붙이면 PK가 매핑됨

@Entity
public class Member {

	@Id
	private Long id;
	private String name;
	게터
	세터
	.
	.


6. 자동으로 숫자 증가(MySQL의 오토인크리먼트, Oracle의 시퀀스) = 아이덴티티 전략

아래처럼 @GeneratedValue(strategy = GenerationType.IDENTITY)를 붙이기 (오라클은 GenerationType.SEQUENCE 라고 넣어야함)

@Entity
public class Member {

	@Id @GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	private String name;
	게터
	세터
	.
	.


7. DB의 컬럼명과 맞게끔 매핑하기

만약 컬럼명과 엔티티의 필드변수명이 다를 경우, 아래처럼 @Column(name = "DB컬럼명") 으로 매핑하면 됨

@Entity
public class Member {

	@Id @GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

	@Column(name = "username")
	private String name;
	게터
	세터
	.
	.


8. 리파지토리 만들기

JPA는 EntityManager클래스를 써서 모든걸 동작하게 할 수 있음

아까 build.gradle에서 implementation 'org.springframework.boot:spring-boot-stater-data-jpa' 로 라이브러리를 받아놓으면
스프링부트가 자동으로 DB랑 연결이랑, application.properties 에서 설정해놓은것들 등을 반영해서 결과물로 엔티티매니저 라는것을 생성해줌. 그럼 만들어진것을 injection 받으면 됨

public class JpaMemberRepository implements MemberRepository{
	private final EntityManager em;

	public JpaMemberRepository(EntityManager em) {
		this.em = em;
	}
	.
	.

참고로 엔티티메니저는 내부적으로 데이터소스를 갖고있어서 DB와 통신하는걸 다 처리할 수 있음

------------------------------

9. '저장' 기능 구현

엔티티매니저의 persist메서드로 저장할 수 있음. 리턴값은 void임(이 예시에서는 인터페이스 스펙에 맞추기 위해서 걍 받은 Member객체를 그대로 반환했음)

public class JpaMemberRepository implements MemberRepository{
	.
	.
	@Override
	public Member save(Member member) {
		em.persist();
		return member;
	}


10. '아이디로 검색' 기능 구현

엔티티매니저의 find메서드를 이용해 단일행을 반환받을 수 있음
(1번째인수: 클래스리터럴(클래스명.class), 2번째인수: PK값)

public class JpaMemberRepository implements MemberRepository{
	.
	.
	@Override
	public Optional<Member> findById(Long id) {
		Member member = em.find(Member.class, id);
		return Optional.ofNullable(member);
	}


11. '전체 검색' 기능 구현

찾고자하는 기준열이 PK라면 find메서드를 쓰면 되지만
DB테이블 전체 조회를 하고싶은경우 or PK가 아닌 다른열로 검색하고싶은경우에는 JPQL 이라는 객체지향쿼리언어를 써야함

JPQL이란? DB테이블 대상이 아닌 객체를 대상으로 쿼리를 날리는것. 그럼 SQL로 변역이 됨

select m from Member m 은
select m from Member as m 과 같고,
뜻은 "Member 객체를 조회" 임
public class JpaMemberRepository implements MemberRepository{
	.
	.
	@Override
	public List<Member> findAll() {
		return em.createQuery("select m from Member m", Member.class).getResultList();
	}


12. '이름으로 검색' 기능 구현
public class JpaMemberRepository implements MemberRepository{
	.
	.
	@Override
	public Optional<Member> findByName(String name) {
		List<Member> result = em.createQuery("select m from Member m where m.name = :name", Member.class)
				.setParameter("name", name)
				.getResultList();
		return result.stream().findAny();
	}


13. 실행하기 전에 주의해야할 점
JPA를 쓰려면 항상 @Transactional을 붙여야함. 서비스클래스에 붙이거나 서비스클래스의 특정 메서드에 붙이면 됨

@Transactional
public class MemberService {
	.
	.


14. SpringConfig 에서 DI해주기

@Configuration
public class SpringConfig {

	private EntityManager em;

	public SpringConfig(EntityManager em) {
		this.em = em;
	}

	@Bean
	public MemberService memberService(){
		return new MemberService(memberRepository());
	}

	@Bean
	public MemberRepository memberRepository(){
		return new JpaMemberRepository(em);
	}
}


15. 테스트 클래스 실행하기

오류 없이 실행이 되었다면 로그를 확인해보기. 아래처럼 Hibernate: ~~ 이렇게 실행된 쿼리가 출력된걸 볼 수 있음

Hibernate: select m1_0.id,m1_0.name from member m1_0 where m1_0.name=?
Hibernate: insert into member (name,id) values (?,default)


16. 테스트클래스 메서드에 @Commit을 넣고 실행하면 테스트 종료후 커밋됨
	.
	.
	@Test
	@Commit
	void 회원가입() {
	.
	.

----------------------------------------------------------------------------------------------------

Spring Data JPA 사용법

SpringBoot와 JPA라는 기반 위에, Spring Data JPA라는 환상적인 프레임워크를 더하면 개발이 정말 즐거워짐
지금까지 조금이라도 단순하고 반복이라 생각했던 개발 코드들이 확연하게 줄어듦. 따라서 개발자는 핵심 비즈니스 로직을 개발하는 데 집중할 수 있음

------------------------------

1. 인터페이스 만들기

public interface SpringDataJpaMemberRepository {


2. JpaRepository 상속받기(인터페이스가 인터페이스를 받을때는 implements가 아닌 extends를 써야함)

제네릭의 키는 엔티티클래스, 값은 PK의 타입을 넣으면 됨 

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>{

참고로 JpaRepository를 상속받으면 인터페이스가 구현체를 자동으로 만들고, 스프링 빈에 자동으로 등록됨


3. 하나 더 추가로 상속받기(인터페이스는 다중상속이 가능함)

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {


4. 사용자기능('이름으로 검색') 메소드 헤드 추가

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {
	@Override
	Optional<Member> findByName(String name);
}


5. SpringConfig DI설정

@Configuration
public class SpringConfig {
	private final MemberRepository memberRepository;

	public SpringConfig(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}

	@Bean
	public MemberService memberService(){
		return new MemberService(memberRepository);
	}
}


6. 테스트 실행

쿼리 잘 날라갔는지 로그로 확인

------------------------------

쿼리 메서드

SpringDataJpa에서 메서드명에 findBy 접두어를 사용하면 메서드 이름을 엔티티 필드명과 매칭시켜서 쿼리를 생성함

이건 Spring Data JPA 의 간단하고 강력한 기능 중 하나임

예를들어 findBy 접두어와 엔티티의 필드명을 사용해 아래와 같이 메서드를 정의할 수 있음

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
	List<User> findByFirstName(String firstName);
	List<User> findByLastName(String lastName);
	List<User> findByAge(int age);
}

위 코드에서 findByFirstName, findByLastName, findByAge 메서드는 각각 User엔티티의 필드에 해당하는 firstName, lastName, age를 기반으로 쿼리를 생성함
예를들어 findByFirstName("john") 이렇게 호출하면 firstName이 "john"인 모든 사용자들을 찾는 쿼리가 생성됨

이걸 잘 사용하면 단순한 작업이 80% 고 복잡한 작업이 20%라고 할때 80%는 인터페이스만으로 끝남

----------------------------------------------------------------------------------------------------

lombok을 마켓플레이스에서 설치한 후에는 아래 설정을 해줘야 함(2019년 이후 버전의 인텔리제이에서는 안해도 되는듯)

Preferences > Build, Execution, Depoloyment > Compiler > Annotation Processors 에서 Enable annotaion processing 을 체크하고 확인버튼 클릭
(한글판: 설정 > 빌드, 실행, 배포 > 컴파일러 > 어노테이션 프로세서 에서 어노테이션 처리 활성화)

----------------------------------------------------------------------------------------------------

gradle

------------------------------

gradle의 의존관계를 터미널에서 보는 방법

cd 명령어로 프로젝트 폴더로 이동

./gradlew dependencies 입력

그럼 의존관계가 단계별(테스트일때 / 컴파일단계 일때 의존관계 등) 트리형태로 표시됨

근데 인텔리제이 gradle탭에서 보는게 더 편함

------------------------------

Spring Web Starter 를 의존성 추가하면

그 안에 톰캣(spring-boot-stater-tomcat), spring-webmvc 등이 들어있음

-----

Spring Data JPA 를 의존성 추가하면

그 안에 Spring Data JPA를 사용하기 위해 필요한 모든 라이브러리와 설정이 함께 추가됨.
AOP와 관련된것들(spring-boot-starter-aop), JDBC(spring-boot-starter-jdbc)(내부적으로 DB커넥션을 쓰기 때문), 하이버네이트(hibernate-core) 등이 들어있음

spring-boot-starter-jdbc 안에는 커넥션풀인 HikariCP가 들어있음
spring-boot-starter-jdbc 안에는 트랜잭션(spring-tx)도 들어있음

------------------------------

spring-boot-starter-어쩌구저쩌구~~~ 를 쓰면

그것이
spring-boot-starter 를 쓰고있고

그것은 또
spring-boot-starter-logging 을 의존하고있음

그것은 또
로그백(logback), slf4j 를 쓰고있음

slf4j 는 단순히 인터페이스의 모음이고(로그를찍기위한)
이것의 구현체로 logback을 꽂거나 log4j를 꽂는 등을 할 수 있음(보통은 거의 slf4j에 logback을 씀)

------------------------------

또 spring-boot-starter는 spring-boot-core(부트스트래핑:애플리케이션을 초기화하고 실행 가능한 상태로 만드는것),
spring-boot-context(ApplicationContext를 통한 스프링 빈 관리) 가 들어있음

------------------------------

테스트쪽을 보면

spring-boot-starter-test 라는 라이브러리가 있고

그 안에는
junit, spring-test, mockito-core(모의 객체(Dock Object) 만드는 라이브러리), assertj-core(테스트를 편하게 해주는 유틸리티 클래스들이 들어있음)

------------------------------

핵심 라이브러리 : 스프링MVC, 스프링ORM, JPA, 하이버네이트, 스프링 데이터 JPA
기타 라이브러리 : H2 DB클라이언트, 커넥션 풀(부트 기본은 HikariCP), WEB(thymeleaf - 뷰 템플릿), 로깅 SLF4J & LogBack, 테스트

----------------------------------------------------------------------------------------------------

start.spring.io 에 들어가서

ADD DEPENDENCIES.. 를 누르면
카테고리(개발툴 / 웹 / 탬플릿엔진 / 보안 / SQL / NoSQL / 메시징 / I/O / OPS / 옵저빌리티 / 테스팅 / 스프링클라우드 등) 별로 무슨무슨 라이브러리들이 있는지 볼 수 있음

----------------------------------------------------------------------------------------------------

스프링 가이드

spring.io 접속 후 메뉴에서 가이드를 누르면 (https://spring.io/guides)

스프링부트 메뉴얼을 볼 수있음

----------------------------------------------------------------------------------------------------

application.yml

spring:
  datasource:
    url: jdbc:h2:tcp://localhost/~/jpashop;MVCC=TRUE
    username: sa
    password:
    driver-class-name: org.h2.Driver
  jpa:
    hibernate:
      ddl-auto: create # 애플리케이션 실행시점에 테이블을 다 지웠다가 다시 생성함
    properties:
      hibernate:
        # show_sql: true # 하이버네이트가 실행하는 SQL쿼리를 로그로 출력할지 여부. System.out으로 찍히기때문에 안쓰는게 좋음
        format_sql: true # 출력된 SQL 쿼리를 읽기 쉽게 포맷할지 여부

logging:
  level:
    org.hibernate.SQL: debug // 하이버네이트 SQL 모드를 디버그 레벨로 씀. 로그를 통해서 찍힘

----------------------------------------------------------------------------------------------------

스프링부트 프로젝트에서 엔티티매니저 사용하는법

<MemberRepository.java>
@Repository
public class MemberRepository {

	@PersistenceContext
	private EntityManager em;
.
.

위처럼 빈으로 등록되는 클래스에서
@PersistenceContext 어노테이션을 넣으면 스프링이 엔티티매니저를 넣어주고
이를 이용해 DB와 상호작용이 가능해짐

.
.
	public Long save(Member member){
		em.persist(member);
		return member.getId();
	}
}

이때 save메소드가 Member객체를 반환하지 않고 id만 반환하게 설계한 이유는
커멘드랑 쿼리를 분리해야하는 원칙을 지키기 위해서임
커멘드성(사이드이펙트를 일으키는것)은 리턴값을 안만듦. 대신 id정도 있으면 다시 조회할수 있으니까 id만 리턴하는것으로 설계할수있음

----------------------------------------------------------------------------------------------------

테스트 케이스 작성시

아래와 같은 형태로 작성하는데

@RunWith(SpringRunner.class)
@SpringBootTest
class MemberRepositoryTest {

	@Test
	void save() {
	}

	@Test
	void find() {
	}
}

Junit5에서는 @RunWith(SpringRunner.class) 부분을 아래처럼 써야함
@ExtendWith(SpringExtension.class)

----------------------------------------------------------------------------------------------------

쿼리 파라미터 로그 남기는 라이브러리

insert into member(id, username) values(?, ?)

기존에 이렇게 ?(물음표)로 출력되던걸 실제 값이 나오게 바꿀 수 있음

logging:
  level:
    org.hibernate.SQL: debug
    org.hibernate.type: trace ←←← 이 부분 추가하면 됨


그럼 로그에 아래처럼 쿼리문 밑에 파라미터 정보가 잘 출력됨

insert into member(username, id) values(?, ?)
2023-09-10 15:10:08.029 TRACE 56324 --- [    Test worker] o.h.type.descriptor.sql.BasicBinder      : binding parameter [1] as [VARCHAR] - [asd]
2023-09-10 15:10:08.029 TRACE 56324 --- [    Test worker] o.h.type.descriptor.sql.BasicBinder      : binding parameter [2] as [BIGINT] - [1]

-----

만약 위의 기능에 만족하지 못하고 ? ? 까지 실제 값으로 만들고 싶을경우

아래 url 들어가서
https://github.com/gavlyukovskiy/spring-boot-data-source-decorator

P6Spy를 의존성추가하면 됨

implementation("com.github.gavlyukovskiy:p6spy-spring-boot-starter:${version}")

ex) implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.5.6'


gradle 업데이트 후 다시 실행하면 아래처럼 파라미터가 괄호안에서 잘 출력됨

insert into member (username, id) values (?, ?)
insert into member (username, id) values ('asd', 1);


참고로 의존성추가할때 버전을 적어야할때가 있고 안적어도 될때가 있는데,
스프링부트가 유명한 메이저 라이브러리들을 스프링버전과 궁합/조합이 맞는 버전으로 다 세팅해놓는데 미리 세팅을 안해놓은 라이브러리들은 버전정보를 직접 적어야함

----------------------------------------------------------------------------------------------------

스프링의 핵심

스프링은 자바 언어 기반의 프레임워크
자바 언어의 가장 큰 특징 → 객체 지향 언어
스프링은 객체 지향 언어가 가진 강력한 특징을 살려내는 프레임워크
스프링은 좋은 객체 지향 애플리케이션을 개발할 수 있게 도와주는 프레임워크

------------------------------

다형성

역활과 구현으로 세상을 구분하는것

-----

객체 지향을 실세계에 비유했을때

ex) 운전자 - 자동차
운전자역할은 자동차를 탈줄만 알면 자동차 구현(K3 / 아반떼 / 테슬라 모델3) 차종이 달라져도
내부 구조가 어떻게 되어있는지 몰라도 되고,
내부 구조가 기름차에서 하이브리드로 변경되어도,
K3에서 테슬라로 아예 구현대상을 변경해도,
엑셀 밟으면 가고 핸들을 왼쪽으로 돌리면 왼쪽으로 감

ex) 공연 무대
로미오 역할(구현: 장동건 / 원빈 / 기타 등등) - 줄리엣 역할(구현: 김태희 / 송해교 / 기타 등등)
로미오 역할은 장동건이 할수도 있고 원빈이 할수도 있고 최후의 경우(배우들이 몸이 아플경우)엔 다른 무명배우로라도 대체가 가능해야함(공연이 되어야함)
줄리엣 역할도 김태희가 할수도있고 송해교하 할수도 있음
로미오 역할을 맡은 사람은 누가 줄리엣 역할을 맡든 상대 배우가 누구인지 몰라도 대본만 충실히 외우면 됨
즉, 변경 가능한, 대체 가능성이 생김. 유연하고 변경이 용이하다는 뜻. 내부 구조를 몰라도 됨

ex) 키보드, 마우스 등 세상의 표준 인터페이스들
커세어 기계식키보드 쓰다가, 리얼포스 무접점으로 바꿔도 그냥 적응할 수 있는것

ex) 정렬 알고리즘
정렬하는 기능만 똑같으면 성능이 더 나은 알고리즘으로 교체할 수 있음

ex) 할인 정책
할인기능을 구현할 예정인데 정액으로 할인할건지 정률로 할인할건지 등의 의사결정이 아직인 경우

-----

역할과 구현으로 구분하면 세상이 단순해지고, 유연해지며 변경도 편리해짐

장점
클라이언트는 대상의 역할(인터페이스)만 알면 됨
클라이언트는 구현 대상의 내부 구조를 몰라도 됨
클라이언트는 구현 대상의 내부 구조가 변경되어도 영향을 받지 않음
클라이언트는 구현 대상 자체를 변경해도 영향을 받지 않음

역할 : 인터페이스
구현 : 인터페이스를 구현한 클래스나 구현 객체

객체를 설계할때 역할과 구현을 명확하게 분리해서 설계를 하는것
객체를 설계할때 일단 인터페이스(역할)를 먼저 설계하고 그 역할을 수행하는 구현 객체를 그 다음에 만드는것

물론 인터페이스가 아니고 일반 클래스간 상속관계도 다형성이 가능하지만, 다중 상속이 안되고 단일 상속밖에 안되는 등의 문제점이 있기때문에 주로 인터페이스를 씀

핵심은 구현보다 인터페이스가 먼저다(역할이 더 중요하다)

-----

다형성의 본질

인터페이스를 구현한 객체 인스턴스를 실행 시점에 유연하게 변경할 수 있음
클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있음

-----

한계

역할(인터페이스) 자체가 변하면, 클라이언트 / 서버 모두에게 큰 변경이 발생함

ex)
자동차를 비행기로 변경해야한다면?
대본 자체가 변경된다면?
USB인터페이스가 변경된다면?

최초 설계시 인터페이스를 안정적으로 잘 설계하는 것이 중요함

-----

스프링과 객체지향

다형성이 가장 중요!
스프링은 다형성을 극대화하여 이용할 수 있게 도와줌
스프링에서 이야기하는 제어의역전(IoC), 의존관계주입(DI) 은 다형성을 활용해서 역할과 구현을 편리하게 다룰 수 있도록 지원함
스프링을 사용하고 나면 마치 레고 블럭 조립하듯이! 공연의 무대의 배우를 선택하듯이! 구현을 편리하게 변경할 수 있음

------------------------------

좋은 객체지향 설계의 5가지 원칙(SOLID)

-----

SRP 단일 책임의 원칙

한 클래스는 하나의 책임만 가져야 함

하나의 책임이라는 것은 모호함
	클 수 있고, 작을 수 있음
	문맥과 상황에 따라 다름
중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임의 원칙을 잘 따른것
ex) UI 변경을 하는데 sql코드랑 애플리케이션을 막 다 고쳐야 하면 잘못설계한것, 객체의 생성과 사용을 분리하는것

범위를 너무 작게하면 기능이 너무 잘게 쪼게지고,
범위를 너무 크게하면 책임이 너무 많아져서 단일책임의 원칙이 깨질 수 있음

적절하게 잘 조절하는것이 객체지향 설계의 묘미

-----

OCP 개방-폐쇄 원칙

소프트웨어 요소는 확장에는 열려있으나 변경에는 닫혀있어야 함

다형성을 활용하면됨
자동차역할에서, 테슬라가 나온다고 해서 운전하는 기본적인 방식이 바뀌지 않음

인터페이스를 구현한 새로운 클래스를 만들어서 새로운 기능을 구현. 이것은 기존 코드를 변경하는게 아님


문제점
MemberService클라이언트가 구현 클래스를 직접 선택
	MemberRepository m = new MemoryMemberRepository(); // 기존 코드
	MemberRepository m = new JdbcMemberRepository(); // 변경 코드
구현 객체를 변경하려면 클라이언트 코드를 변경해야함
분명 다형성을 사용했지만 OCP원칙을 지킬 수 없음
이 문제를 해결하려면 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요함

설정파일을 만들어 주입해주면 클라이언트코드는 변경할필요가 없기때문에
소프트웨어 요소를 새롭게 확장해도 사용영역의 변경은 닫혀있음. =OCP준수

-----

LSP 리스코프 치환원칙

프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 함

하위 클래스는 인터페이스의 규약을 다 지켜야 함

ex) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반. 느리더라도 앞으로 가야함

-----

ISP 인터페이스 분리 원칙

특정 클라이언트를 위한 인터페이스 여러개가 범용 인터페이스 하나보다 낫다

ex)
자동차 인터페이스
운전 인터페이스, 정비 인터페이스
인터페이스를 2가지로 분리했음. 하나만 있으면 너무 크기때문

사용자 클라이언트
운전자 클라이언트, 정비사 클라이언트로 분리

이렇게 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음
(정비와 관련된 문제가 있어서 기능을 바꿔야 할 경우, 정비 인터페이스에 대한 부분과, 정비인터페이스를 사용하는 정비사 관련된 부분만 바꾸면 되지,
운전인터페이스&운전자클라이언트는 바꿀필요가 없음)


그리고 하나의 인터페이스에 기능이 너무 많으면 복잡함

기능이 크면 그걸 다 구현하기 힘듦. 기능을 알맞게, 적당한 크기로 잘 쪼개는게 중요

-----

DIP 의존관계 역전 원칙

프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다

즉, 클라이언트 코드가 구현 클래스를 바라보지 말고, 인터페이스만 바라보라는 뜻

MemberService가 MemberRepository인터페이스만 바라보고, MemoryMemberRepository나 JdbcMemberRepository에 대해서는 몰라야 한다는 뜻

앞에서 얘기한 역할(Role)에 의존하게 해야 한다는 것과 같음. 객체 세상도 클라이언트가 인터페이스에 의존해야 유연하게 구현체를 변경할 수 있음. 구현체에 의존하게 되면 변경이 아주 어려워짐

ex) 공연예시에서, 원빈이 김태희랑만 공연 연습을 했음. 김태희 아니면 다른사람이랑 공연하기 힘듦. 그럼 안됨.
대본을 보고 연습을 안하고, 둘이 따로 대본없이 연습을 했음. 그럼 나중에 다른 배우로 바뀌면 공연이 망함

역할과 구현을 철저하게 분리하도록 시스템도 그렇게 설계해아함. 언제든지 갈아끼울 수 있도록!
그게 되려면 역할에 의존해야지, 구현에 의존하면 절대 안됨

그런데 아래 코드에서는 인터페이스에 의존하지만, 구현클래스도 동시에 의존한다(의존한다 = 내가 저 코드를 안다. 알기만 하면 다 의존하는것임)
public class MemberService{
	private MemberRepository memberRepository = new MemoryMemberRepository();
}
위 코드에서 MemberService는 MemberRepository인터페이스 뿐만 아니라, MemoryMemberRepository클래스 까지 알고있는것임
그래서 MemoryMemberRepository를 다른걸로 바꾸려고 할때 코드를 변경을 해야함

이는 DIP 위반임. 추상(인터페이스)에 의존하는 동시에, 구체(구현) 클래스인 MemoryMemberRepository에도 의존하고 있기 때문

-----

정리

객체 지향의 원칙은 다형성임
다형성 만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없음
다형성 만으로는 구현 객체를 변경할 때, 클라이언트 코드도 함께 변경됨
다형성 만으로는 OCP, DIP를 지킬 수 없음

무언가가 더 필요한 상황인데, 그게 바로 스프링 컨테이너임

------------------------------

스프링에서는 다음 기술로 다형성 + OCP, DIP 를 가능하게 지원함
	DI(Dependency Injection): 의존관계, 의존성 주입
	DI 컨테이너 제공

클라이언트 코드의 변경 없이 기능 확장 가능

쉽게 부품을 교체하듯이 개발 가능

------------------------------

종합 정리

모든 설계에 역할과 구현을 분리하기
자동차, 공연의 예를 떠올리기
애플리케이션 설계도 공연을 하듯이 배역만 만들어두고, 배우는 언제든지 유연하게 변경할 수 있도록 만드는 것이 좋은 객체지향 설계임
이상적으로는 모든 설계에 인터페이스를 부여하기

하지만 인터페이스를 도입하게 되면 추상화라는 비용이 발생함
추상화가 돼버리면, 개발자가 코드를 한번 더 열어봐야함. 런타임에 MemoryMemberRepository를 쓸지 JdbcMemberRepository를 쓸지 선택이 되기때문에
인터페이스만 보이고, 구현클래스가 뭐지 하고 또 들어가봐야함. 이런식으로 코드가 추상화됨으로써 오는 단점도 있음
추상화의 장점이 단점을 넘어설때 선택을 해야함

기능을 확장할 가능성이 없다면, 구체 클래스를 직접 사용하고, 향후 꼭 필요할 때 리팩터링해서 인터페이스를 도입하는것도 방법임

----------------------------------------------------------------------------------------------------

주문 서비스와 할인 서비스가 있음

주문서비스에서 할인서비스를 가져다 쓴다고 할때,

public class OrderServiceImpl implements OrderService{
	private MemberRepository memberRepository = new MemoryMemberRepository();
	private DiscountPolicy discountPolicy = new FixDiscountPolicy();

이렇게 쓰는것은 DIP에 어긋난 방법임. 왜냐? 할인정책을 변경할경우(구현클래스가 바뀔경우) 아래처럼 코드를 변경해야하는데

public class OrderServiceImpl implements OrderService{
	private MemberRepository memberRepository = new MemoryMemberRepository();
	private DiscountPolicy discountPolicy = new RateDiscountPolicy();

이는 무대공연 비유로 따지면 로미오역을 맡은 디카프리오 배우가 줄리엣역을 맡을 배우를 직접 섭외하는 것과 같음
각각의 배역에 맞는 배우를 선택하는것은 공연을 주관하는 기획자(기획팀)가 해야하는것이지 배우들이 정하는게 아님

디카프리오는 공연도 해야하고 동시에 여자 주인공도 공연에 직접 섭외해야하는 "다양한 책임"을 갖게 됨 (너무 많은 일을 해야하므로 공연이 당연히 잘 안됨)
배우는 본인의 역할인 배역을 수행하는것에만 집중해야함
디카프리오는 어떤 여자주인공이 선택되더라도 똑같이 공연을 할 수 있어야함

주문 서비스도 마찬가지로 어떤 할인정책이 설정되든 알 필요 없이 주문만 잘 되면 됨

이를 위해서는 공연을 구성하고, 담당 배우를 섭외하고, 역할에 맞는 배우를 지정하는 책임을 담당하는 별도의 "공연 기획자가" 등장해야함
공연 기획자를 만들고, 배우와 공연 기획자의 책임을 확실히 분리하기 (관심사 분리)

----------------------------------------------------------------------------------------------------

정적인 클래스 의존관계

클래스가 사용하는 import 코드만 보고 의존관계를 쉽게 파악할 수 있음. 정적인 의존관계는 애플리케이션을 실행하지 않아도 분석할 수 있음
실제 어떤 객체가 주입될지는 알 수 없음

-----

동적인 객체 인스턴스 의존관계

애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존 관계

애플리케이션 실행시점(런타임)에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계가 연결되는 것을 의존관계 주입이라고 함
객체 인스턴스를 생성하고, 그 참조값을 전달해서 연결됨

의존관계 주입을 사용하면 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있음
의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있음

AppConfig처럼 객체를 생성하고 관리하면서 의존관계를 연결해주는 것을 Ioc컨테이너 또는 DI컨테이너라고 함(또는 어샘블러, 오브젝트팩토리 등으로 불리기도 함)

------------------------------

스프링에서는 애플리케이션의 구성(=설정)를 담당하는 설정정보 클래스에 @Configuration을 붙임

사용하는곳에서 아래처럼 쓰면 됨

// 기존 방식
AppConfig appConfig = new AppConfig();
MemberService memberService = appConfig.memberService();

↓↓↓

// 설정클래스의 클래스리터럴을 넣으면 됨
ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);

// 첫번째인수는 설정파일에서 호출하고싶은 메서드명 넣으면 되고, 두번째 인수는 반환할 타입(인터페이스)의 리터럴 넣으면 됨
MemberService memberService = ac.getBean("memberService", MemberService.class);

-----

실행을 하면 로그에 아래처럼 찍히는걸 볼 수 있음

22:29:55.035 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'appConfig'
22:29:55.037 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'memberService'
22:29:55.046 [main] DEBUG org.springframework.beans.factory.support.DefaultListableBeanFactory - Creating shared instance of singleton bean 'orderService'
.
.

스프링에 싱글톤으로 등록이 되었다는뜻. 등록되는 빈에는 설정클래스도 포함됨

------------------------------

스프링 컨테이너

ApplicationContext를 스프링 컨테이너라 한다

기존에는 개발자가 AppConfig를 사용해서 직접 객체를 생성하고 DI를 했지만, 이제부터는 스프링 컨테이너를 통해서 사용함

스프링컨테이너는 @Configuration이 붙은 AppConfig를 설정(구성)정보로 사용함. 여기서 @Bean이라 적힌 메서드를 모두 호출해서 ★반환된 객체★를 스프링 컨테이너에 등록함
이렇게 ★스프링 컨테이너에서 등록된 객체를 스프링 빈★이라 함

스프링 빈은 @Bean이 붙은 메서드의 명을 스프링 빈의 이름으로 사용함("memberService", "orderService"). (물론 바꿀 수 있으나 관례를 따르는게 좋음)

이전에는 개발자가 필요한 객체를 AppConfig를 사용해서 직접 조회했지만, 이제부터는 스프링컨테이너를 통해서 필요한 스프링 빈(객체)를 찾아야 함
스프링 빈은 applicationContext객체.getBean()메서드를 사용해서 찾을 수 있음

기존에는 개발자가 직접 자바코드로 모든 것을 했다면, 이제부터는 스프링 컨테이너에게 객체를 스프링 빈으로 등록하고, 스프링 컨테이너에서 스프링 빈을 찾아서 사용하도록 변경되었음

----------------------------------------------------------------------------------------------------

참고로 스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나누어져 있음

그런데 이렇게 자바코드로 스프링 빈을 등록하면 생성자를 호출하면서 의존관계 주입도 한번에 처리됨

----------------------------------------------------------------------------------------------------

스프링 컨테이너에 등록된 빈 목록 조회

ac.getBeanDefinitionNames() : 모든 빈의 이름을 String배열로 가져옴. 이중에는 스프링이 내부적으로 만들어놓은 빈도 포함되어있음
	참고로 ApplicationContext클래스는 부모클래스라서 이 메서드가 없음. AnnotationConfigApplicationContext 또는 GenericXmlApplicationContext 등에 있음
ac.getBean(빈이름) : 빈의 이름에 매핑된 객체(설정파일에서 메서드의 return객체)를 가져올 수 있음

ex)
String[] beanDefinitionNames = ac.getBeanDefinitionNames();
for (String beanDefinitionName : beanDefinitionNames)
	System.out.println("key: " + beanDefinitionName + ", val: " + ac.getBean(beanDefinitionName));

-----

내가 등록한 bean만 출력하고싶은 경우

String[] beanDefinitionNames = ac.getBeanDefinitionNames();
for (String beanDefinitionName : beanDefinitionNames) {
	BeanDefinition beanDefinition = ac.getBeanDefinition(beanDefinitionName);
	if(beanDefinition.getRole() == BeanDefinition.ROLE_APPLICATION)
		System.out.println("key: " + beanDefinitionName + ", val: " + ac.getBean(beanDefinitionName));
}

스프링이 내부에서 사용하는 빈은 BeanDefinition.ROLE_INFRASTRUCTURE 로 바꾸면 됨

----------------------------------------------------------------------------------------------------

빈 조회

첫번째인수: 빈 이름
두번째인수: 빈 타입(인터페이스) 리터럴 (메서드선언부의 반환타입(인터페이스)이 아니여도 됨. 구현클래스를 넣어도 됨. 하지만 구현클래스를 넣으면 당연히 안좋음(역할에 의존해야하기때문))

메서드명+타입 으로 조회
MemberService memberService = ac.getBean("memberService", MemberService.class);

타입으로만 조회도 가능 (같은 타입이 2개이상일경우는 예외 발생시켜줌)
MemberService memberService = ac.getBean(MemberService.class);

타입의 모든 빈 조회
Map<String, MemberRepository> beansOfType = ac.getBeansOfType(MemberRepository.class);


부모 타입으로 조회하면, 자식 타입도 함께 조회됨
그래서 모든 자바 객체의 최고 부모인 Object 타입으로 조회하면, 모든 스프링 빈을 조회함

----------------------------------------------------------------------------------------------------

BeanFactory

getBean()은 BeanFactory에 선언돼있는 메서드임

계층구조가 아래처럼 되어있음

<interface>
BeanFactory
	↑
<interface>
ApplicationContext
	↑
<class>
AnnotationConfigApplicationContext


어플리케이션을 개발하려면 빈 관리기능 말고도 여러가지 기능들이 필요함

ApplicationContext 는 BeanFactory 말고도 다른 여러가지 인터페이스들을 상속받고 있음. 아래는 그 종류이다

EnvironmentCapable : 환경변수(로컬, 개발, 운영등을 구분해서 처리)
MessageSource : 메시지소스를 활용한 국제화 기능(한국에서 들어오면 한국어로, 영어권에서 들어오면 영어로 출력)
ApplicationEventPublisher : 애플리케이션 이벤트(이벤트를 발행하고 구독하는 모델을 편리하게 지원)
ResourcePatternResolver : 편리한 리소스 조회(파일, 클래스패스, 외부 등에서 리소스를 편리하게 조회)

정리
ApplicationContext는 BeanFactory의 기능을 상속받음
ApplicationContext는 빈 관리기능 + 편리한 부가 기능을 제공함
BeanFactory를 직접 사용할 일은 거의 없음. 부가기능이 포함된 ApplicationContext를 사용함
BeanFactory나 ApplicationContext를 스프링 컨테이너라 한다

----------------------------------------------------------------------------------------------------

스프링은 다양한 설정 형식을 지원함(자바 코드, XML, Groovy 등)

							<interface>
							BeanFactory
								↑
							<interface>
							BeanFactory
								↑
<class>							<class>						<class>
AnnotationConfigApplicationContext	GenericXmlApplicationContext	XxxApplicationContext(임의로 구현해서 만들 수도 있음)
(AppConfig.class)					appConfig.xml					appConfig.xxx

XML 설정 사용시 장점
컴파일 없이 빈 설정 정보를 변경할 수 있음

------------------------------

xml로 설정하는법

src/resources 패키지에 appConfig.xml을 만듦(새로만들기 > XML구성파일 > Spring 구성 에서 쉽게 만들 수 있음)
참고로 자바파일이 아닌건 다 resources밑에 넣어야 함


1. 설정은 아래처럼 <bean>태그로 하면 됨
생성자에 다른 객체를 넣어야할때는 <constructor-arg> 태그를 쓰고, ref 속성으로 다른 빈(<bean>)과 연결시키면 됨

@Configuration
public class AppConfig {
	@Bean
	public MemberService memberService(){
		return new MemberServiceImpl(getMemberRepository());
	}

	@Bean
	public OrderService orderService(){
		return new OrderServiceImpl(getMemberRepository(), getDiscountPolicy());
	}

	@Bean
	private static DiscountPolicy getDiscountPolicy() {
		return new FixDiscountPolicy();
	}

	@Bean
	private static MemberRepository getMemberRepository() {
		return new MemoryMemberRepository();
	}
}

위 코드를 xml로 하면 아래와 같음

<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="memberService" class="hello.core.member.MemberServiceImpl">
		<constructor-arg ref="memberRepository"/>
	</bean>

	<bean id="orderService" class="hello.core.order.OrderServiceImpl">
		<constructor-arg ref="memberRepository"/>
		<constructor-arg ref="discountPolicy"/>
	</bean>

	<bean id="memberRepository" class="hello.core.member.MemoryMemberRepository"/>

	<bean id="discountPolicy" class="hello.core.discount.FixDiscountPolicy"/>
</beans>


2. 호출은 AnnotationConfigApplicationContext 대신 GenericXmlApplicationContext 클래스의 생성자를 쓰면 됨

ApplicationContext ac = new GenericXmlApplicationContext("appConfig.xml");
Assertions.assertThat(ac.getBean("discountPolicy", DiscountPolicy.class)).isInstanceOf(FixDiscountPolicy.class);

----------------------------------------------------------------------------------------------------

스프링 빈 설정 메타 정보 - BeanDefinition 인터페이스

스프링은 어떻게 이런 다양한 설정 형식을 지원하는 것일까? 그 중심에는 BeanDefinition이라는 추상화가 있음
쉽게 이야기해서 "역할과 구현을 개념으로 나눈 것" 이다

XML을 읽어서 BeanDefinition을 만들면 된다
자바 코드를 읽어서 BeanDefinition을 만들면 된다

스프링컨테이너는 자바 코드인지, XML인지 몰라도 된다. 오직 BeanDefinition만 알면 된다

BeanDefinition을 빈 설정 메타정보라고 함

@Bean, <bean> 당 각각 하나씩 메타정보가 생성됨

스프링 컨테이너는 이 메타정보를 기반으로 스프링 빈을 생성함

----------------------------------------------------------------------------------------------------

웹 애플리케이션과 싱글톤

웹 애플리케이션은 보통 여러 고객이 동시에 요청을 함

우리가 만들었던 스프링 없는 순수한 DI컨테이너인 AppConfig는 요청을 할 때마다 객체를 새로 생성함
고객 트래픽이 초당 100이 나오면 초당 100개 객체가 생성되고 소멸됨 → 메모리 낭비가 심함
해결방안은 해당 객체가 딱 1개만 생성되고, 공유하도록 설계하면 됨 → 싱글톤 패턴

------------------------------

싱글톤 방식의 주의점

여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 상태를 유지(stateful)하게 설계하면 안됨

무상태(stateless)로 설계해야함
특정 클라이언트에 의존적인 필드가 있으면 안됨
특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안됨
가급적 읽기만 가능해야함
필드 대신에 자바에서 공유되지 않는 지역변수, 파라미터, TreadLocal 등을 사용해야함

스프링 빈의 필드에 공유 값을 설정하면 정말 큰 장애가 발생할 수 있음

----------------------------------------------------------------------------------------------------

설정파일로 스프링 빈 등록시 주의사항

private static으로 하면 안됨 (싱글톤이 안됨. 객체 주소가 다 다름)


private static MemberRepository memberRepository() {
    return new MemoryMemberRepository();
}
이 코드에서 memberRepository() 메서드는 private static으로 선언되어 있음
이것은 해당 메서드가 스프링 컨테이너에 의해 호출되지 않을 것임을 나타냄
즉, MemoryMemberRepository 객체가 스프링 빈으로 등록되지 않음. 따라서 이 코드는 MemoryMemberRepository를 스프링 빈으로 사용할 수 없게 됨


public MemberRepository memberRepository() {
    return new MemoryMemberRepository();
}
이 코드에서 memberRepository() 메서드는 public으로 선언되어 있음
이렇게 하면 스프링 컨테이너에서 해당 메서드를 호출하여 MemoryMemberRepository 객체를 반환하고 이 객체를 스프링 빈으로 등록함
따라서 이 코드는 MemoryMemberRepository를 스프링 빈으로 사용할 수 있게 됨

----------------------------------------------------------------------------------------------------

스프링이 싱글톤을 보장하는 원리

@Configuration
public class AppConfig {
	@Bean
	public MemberService memberService(){
		System.out.println("call AppConfig.memberService");
		return new MemberServiceImpl(memberRepository());
	}

	@Bean
	public OrderService orderService(){
		System.out.println("call AppConfig.orderService");
		return new OrderServiceImpl(memberRepository(), discountPolicy());
	}

	@Bean
	public MemberRepository memberRepository() {
		System.out.println("call AppConfig.memberRepository");
		return new MemoryMemberRepository();
	}
}

@Configuraion이 붙은 클래스는 스프링이 CGLIB라는 바이트코드 조작 라이브러리를 사용해서 AppConfig클래스를 상속받은 임의의 다른 클래스를 만들고,
그 다른 클래스를 빈으로 등록함
@Bean이 붙은 메서드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 생성해서 스프링 빈으로 등록하고 반환하는 코드가 동적으로 만들어짐

기존에 내가 작성한 AppConfig클래스는 사라지고 AppConfig클래스를 상속받은 임의의 다른 클래스를 만들고 그 클래스를 스프링빈으로 등록함

따라서 System.out.println("call AppConfig.memberRepository");이 3번 호출되지 않고 딱 1번만 호출됨


아래 코드를 실행했을때
@Test
void configurationDeep(){
	ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
	AppConfig bean = ac.getBean(AppConfig.class);

	System.out.println("bean = " + bean.getClass());
}

@Configuration을 안붙이면 아래처럼 나오고
bean = class hello.core.AppConfig

@Configuration을 붙이면 아래처럼 나오는걸 확인할 수 있음
bean = class hello.core.AppConfig$$EnhancerBySpringCGLIB$$4a5fc277

스프링 빈 조회가 된 이유는 AppConfig@CGLIB는 AppConfig의 자식타입이기때문에, AppConfig타입으로 조회할 수 있음


@Configuration을 빼도 @Bean을 읽어서 스프링 빈으로 등록이 되지만, 싱글톤이 깨짐(순수한 자바코드가 실행됨)

즉 System.out.println("call AppConfig.memberRepository");이 3번 호출됨

----------------------------------------------------------------------------------------------------

컴포넌트 스캔을 사용하려면 먼저 @ComponentScan을 설정 정보에 붙여주면 됨

기존의 AppConfig와는 다르게 @Bean으로 등록한 클래스가 하나도 없음

컴포넌트 스캔을 사용하면 @Configuration이 붙은 설정 정보도 자동으로 등록되기 때문에
AppConfig, TestConfig 등 앞서 만들어두었던 설정 정보도 함께 등록되고 실행돼버림. 그래서 excludeFilters를 이용하여 설정정보는 컴포넌트 스캔 대상에서 제외시키겠음
보통 설정정보를 스캔 대상에서 제외하지는 않지만, 기존 예외코드를 최대한 남기고 유지하기 위해서 이 방법을 선택했음

@Configuration
@ComponentScan(
		excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Configuration.class)
)
public class AutoAppConfig {

------------------------------

그다음 빈을 등록할 클래스파일들에 직접 들어가서 @Component를 붙이면 됨

@Component
public class MemoryMemberRepository implements MemberRepository{

@Component
public class FixDiscountPolicy implements DiscountPolicy{

------------------------------

의존관계 주입이 필요할경우

ex) 설정파일로 의존성 설정시
@Configuration
public class AppConfig {
	@Bean
	public MemberService memberService(){
		return new MemberServiceImpl(new MemoryMemberRepository());
	}

ex) @Component로 의존성 설정시
@Component
public class MemberServiceImpl implements MemberService{
	private final MemberRepository memberRepository;

	@Autowired
	public MemberServiceImpl(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}

위처럼 @Autowired를 붙이면 스프링이 MemberRepository타입에 맞는 애를 찾아와서 자동으로 주입해줌

@Autowired가 붙은건 파라미터로 타입인 MemberRepository를 bean에서 찾아서 주입해줌(MemoryMemberRepository가 MemberRepository의 자식이므로 이게 주입됨)
즉 위 예시에서 @Autowired는 ac.getBean(MemberRepository.class)랑 같음

------------------------------

빈으로 등록됐는지 확인하는법

public class AutoAppConfigTest {
	@Test
	void basicScan(){
		ApplicationContext ac = new AnnotationConfigApplicationContext(AutoAppConfig.class);

		MemberService memberService = ac.getBean(MemberService.class);

이렇게 @ComponentScan이 있는 클래스인 AutoAppConfig클래스를 넣고 실행하면

Identified candidate component class: file [/~~~/RateDiscountPolicy.class] 이렇게 클래스를 후보로 지정했다고 나오면서
Creating shared instance of singleton bean 'rateDiscountPolicy' 이렇게 싱글톤 빈으로 등록됐다고 나옴

그리고 autowired에 대한 정보도 나오는데

Autowiring by type from bean name 'memberServiceImpl' via constructor to bean named 'memoryMemberRepository'
↓↓↓
MemberServiceImpl 빈을 생성할때 MemoryMemberRepository 빈을 생성자를 통해 주입하고 있다는 것을 의미

------------------------------

@ComponentScan은 @Component가 붙은 모든 클래스를 스프링 빈으로 등록함

이때 스프링 빈의 기본 이름은 클래스명이 사용되되, 맨 앞글자만 소문자로 바뀜

빈 이름 기본 전략 : MemberServiceImpl클래스 → memberServiceImpl
빈 이름 직접 지정 : 만약 스프링 빈의 이름을 직접 지정하고 싶으면 @Component("memberService2") 이런식으로 하면 됨

------------------------------

@ComponentScan을 할때 모든 자바클래스를 다 스캔하려면 시간이 오래걸림. 그래서 꼭 필요한 위치부터 탐색하도록 시작위치를 정할수 있음

@ComponentScan(
	basePackages = "hello.core",
)

basePackages : 탐색할 패키지의 시작 위치를 지정함. 이 패키지를 포함해서 하위 패키지를 모두 탐색함
	basePackages = {"hello.core", "hello.service"} 이렇게 여러 시작 위치를 지정할 수도 있음

basePackageClasses : 지정한 클래스의 패키지를 탐색 위치로 지정함
만약 지정하지 않으면 @ComponentScan이 붙은 설정 정보 클래스의 패키지를 루트디렉토리로 해서 찾음

java
	hello
		core
			member
			discount
			order
			AppConfig.java

이렇게 있다고 할때 @ComponentScan을 붙인 AppConfig.java 는 java.hello.core에 있으므로 java.hello.core안에 있는 모든 클래스들을 탐색함

관례는 내 프로젝트의 최상단에 놓고 basePackages는 쓰지 않는것

스프링 부트를 사용하면 스프링 부트의 대표 시작정보인 @SpringBootApplication를 이 프로젝트 시작 루트 위치에 두는 것이 관례임
그리고 이 설정 안에 바로 @ComponentScan이 들어있음!!

------------------------------

@Filter

컴포넌트스캔에서 제외하고싶을때 씀

먼저 어노테이션 2개 만들기

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface MyIncludeComponent {
}

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface MyExcludeComponent {
}


BeanA는 포함하고 BeanB는 포함하지않으려면

@MyIncludeComponent
public class BeanA {
}

@MyExcludeComponent
public class BeanB {
}

public class ComponentFilterAppConfigTest {
	@Test
	void filterScan(){
		ApplicationContext ac = new AnnotationConfigApplicationContext(ComponentFilterAppConfig.class);

		BeanA beanA = ac.getBean("beanA", BeanA.class);
		Assertions.assertThat(beanA).isNotNull();

		BeanB beanB = ac.getBean("beanB", BeanB.class);

	}

	@Configuration
	@ComponentScan(
			includeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class),
			excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class)
	)
	static class ComponentFilterAppConfig{
	}
}

beanB가 등록되지 않았으므로(제외했으므로) beanB를 찾으려고 할때 오류 발생됨

beanA도 스캔에서 제외시키고싶으면 아래처럼 다중 속성으로 {} 안에 넣으면 됨. 클래스를 직접제외시킬땐 FilterType.ASSIGNABLE_TYPE 쓰기
@Configuration
@ComponentScan(
		includeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class),
		excludeFilters = {
				@ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class),
				@ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, classes = BeanA.class)
		}
)
static class ComponentFilterAppConfig{
}

사실 @Component면 충분하기 때문에, includeFilters를 사용할 일은 거의 없음
excludeFilters는 여러가지 이유로 간혹 사용할 일은 있지만 많지는 않음

----------------------------------------------------------------------------------------------------

빈 이름 충돌

------------------------------

자동 빈, 자동 빈 충돌

예를들어 아래와 같은 service이름으로 빈을 2개등록했을때

@Component("service")
public class OrderServiceImpl implements OrderService{

@Component("service")
public class MemberServiceImpl implements MemberService{


그럼 아래와 같이 hello.core.order.OrderServiceImpl 랑 hello.core.member.MemberServiceImpl 랑 충돌했다고 예외 발생함
Caused by: org.springframework.context.annotation.ConflictingBeanDefinitionException: Annotation-specified bean name 'service' for bean class [hello.core.order.OrderServiceImpl] conflicts with existing, non-compatible bean definition of same name and class [hello.core.member.MemberServiceImpl]

------------------------------

자동 빈, 수동 빈 충돌

예를들어 아래와같이 memoryMemberRepository라는 이름으로 2개의 빈을 등록했을때

@Component // 첫글자가 소문자로 바뀌어서 memoryMemberRepository 라는 이름으로 빈 등록됨
public class MemoryMemberRepository implements MemoryRepository{...}

@Bean("memoryMemberRepository") // 같은 이름의 빈 등록
MemberRepository memberRepository(){
	return new MemoryMemberRepository();
}

이때는 실행이 잘 됨

수동빈이 우선권을 가짐 (수동빈으로 덮임)

아래처럼 출력되는걸 볼 수 있음 (수동빈이 자동빈을 오버라이딩 했다는 뜻)
Overriding bean definition for bean 'memoryMemberRepository' with a different definition: replacing [Generic bean: class [hello.core.member.MemoryMemberRepository];


최근 스프링부트는 수동 빈과 자동 빈 등록이 충돌나면 오류가 발생하도록 기본값을 바꿨음

스프링부트로 실행시켜보면 아래와같은 오류메시지가 출력되고 실행이 종료됨(@Test로 말고 @SpringBootApplication으로 실행시켜야함)

The bean 'memoryMemberRepository', defined in class path resource [hello/core/AutoAppConfig.class], could not be registered. A bean with that name has already been defined in file [/Users/imchaewon/git/study/core/out/production/classes/hello/core/member/MemoryMemberRepository.class] and overriding is disabled.


만약 오버라이딩하고싶으면 설정파일 변경하기
<application.properties>
spring.main.allow-bean-definition-overriding=true

<application.yml>
spring.main.allow-bean-definition-overriding: true

부트는 기본값을 false로 쓰도록 결정함. 이유는 이런 오류는 잡기가 어렵기때문(개발은 혼자하는것이 아니므로 애매한 상황을 만들지 않는게 가장 좋음)

----------------------------------------------------------------------------------------------------

@Autowired 동작원리

ex)
@Component
public class OrderServiceImpl implements OrderService{
	private final MemberRepository memberRepository;
	private final DiscountPolicy discountPolicy;

	@Autowired
	public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
		this.memberRepository = memberRepository;
		this.discountPolicy = discountPolicy;
	}

스프링이 @ComponentScan해서 @Component가 붙어있는 OrderServiceImpl이 스프링빈으로 등록될때
생성자가 호출되면서, @Autowired가 있네 라고 하면 스프링컨테이너에서 스프링빈을 꺼내서(MemberRepository 랑 DiscountPolicy) 주입해줌

★참고로 생성자가 딱 1개만 있으면 @Autowired를 생략할 수 있음

----------------------------------------------------------------------------------------------------

생성자 주입

생성자 호출 시점에 딱 1번만 호출되는것이 보장됨
"불변", "필수" 의존관계에 사용

공연예시로, 공연하기 전에 배우들을 다 정하고 끝내고 싶은것.
공연하는 중간에 배우를 바꿀일이 없는것

------------------------------

수정자 주입(setter 주입)

"선택", "변경" 가능성이 있는 의존관계에 사용
자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법

ex) required = false로 속성을 넣으면, 해당 타입(DiscountPolicy)의 빈이 존재하지 않더라도 오류를 발생시키지 않고 null을 주입함
@Autowired(required = false)
public void setDiscountPolicy(DiscountPolicy discountPolicy) {
	System.out.println("discountPolicy = " + discountPolicy);
	this.discountPolicy = discountPolicy;
}

자바빈 프로퍼티(JavaBean Property): 멤버변수(필드) 와 이 상태에 접근하고 수정하는 데 사용되는 메서드(게터와 세터)

------------------------------

필드 주입

이름 그대로 필드에 바로 주입하는 방법

코드가 간결하지만 외부에서 변경이 불가능해서 테스트하기 힘들다는 치명적인 단점이 있음

예를들어 아래의 코드가 있다고 할때
@Component
public class OrderServiceImpl implements OrderService{
	@Autowired private MemberRepository memberRepository;

memberRepository를 가짜 멤버리파지토리 객체로 바꾸고싶을때(직접 DB에 접근이 안되는경우 뭔가 임시의 데이터를 넘기는 멤버리파지토리로 바꾸고 싶을때가 있음)
하지만 이 값을 바꿀수 있는 방법이 없음

아래 코드를 보면 순수한 자바코드로 OrderServiceImpl 객체를 만들었을때, 이 객체에 필드를 세팅할수가 없어서 memberRepository 가 null이 됨

@Test
void fieldInjectionTest(){
	OrderServiceImpl orderService = new OrderServiceImpl();
}

orderService의 필드를 바꿀수 있는 방법이 없음. 그럼 결국 세터를 만들어야함
Autowired는 스프링컨테이너에서 가져와야(스프링 컨테이너가 관리하는걸 가져와야) 적용되는것이지,
임의로 new 연산자로 만드는건 당연히 Autowired가 안됨

순수한 자바코드로 OrderServideImpl 같은 애들만 테스트 하는 경우가 진짜 많음
근데 필드주입을 쓰면 di컨테이너가 없으면 아무것도 할수없음(스프링 컨테이너를 다 띄우고 스프링에서 가져와야함)


필드주입은 아래와 같은 곳에서만 사용
∙애플리케이션의 실제 코드와 관련없는 테스트 코드
∙스프링설정을 목적으로하는 @Configuration

ex) 테스트코드
@SpringBootTest
class CoreApplicationTests {

	@Autowired
	OrderService orderService;

	@Test
	void contextLoads() {
		orderService.
	}

ex) 스프링설정 클래스
@Configuration
@ComponentScan
public class AutoAppConfig {

	@Autowired MemberRepository memberRepository;
	@Autowired DiscountPolicy discountPolicy;

	@Bean
	OrderService orderService(){
		return new OrderServiceImpl(memberRepository, discountPolicy);
	}

------------------------------

일반 메서드 주입

한번에 여러 필드를 주입받을 수 있음
일반적으로 잘 사용하지 않음

@Autowired
public void init(MemberRepository memberRepository, DiscountPolicy discountPolicy){
}

참고로 당연한 이야기지만 의존관계 자동주입은 스프링 컨테이너가 관리하는 스프링 빈이어야 동작함
스프링빈이 아닌 Member같은 클래스에서 @Autowired코드를 적용해도 아무 기능도 동작하지 않음

------------------------------

생성자 주입을 선택해야하는 이유

∙불변
대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없음(불변해야함)
수정자 주입을 사용하면, setXXX메서드를 public으로 열어두어야함
누군가 실수로 변경할 수도 있고, 변경하면 안되는 메서드를 열어두는것은 좋은 방법이 아님
생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없음. 따라서 불변하게 설계할 수 있음

∙누락
프레임워크 없이 순수한 자바 코드를 단위테스트하는 경우에 발생하는 누락을 막을 수 있음

∙final 키워드
final키워드를 사용해 혹시라도 생성자에서 값이 설정되지 않는걸 방지할 수 있음(컴파일 오류를 만들어줌)

수정자 주입을 포함한 나머지 주입방식은 모두 생성자 이후에 호출되므로 필드에 final 키워드를 쓸 수 없음. 오직 생성자 주입 방식만 final키워드를 쓸 수 있음


정리
생성자 주입을 선택하는 이유는 여러가지가 있지만, 프레임워크에 의존하지 않고, 순수한 자바 언어의 특징을 잘 살리는 방법이기도 함
기본으로 생성자 주입을 사용하고, 필수 값이 아닌 경우에는 수정자 주입 방식을 옵션으로 부여하면 됨. 생성자주입과 수정자주입을 동시에 사용할 수 있음
항상 생성자 주입을 사용하기. 그리고 가끔 옵션이 필요하면 수정자 주입을 선택하기. 필드 주입은 사용하지 않는게 좋음

----------------------------------------------------------------------------------------------------

Autowired 테스트

스프링빈이 아닌(@Component 어노테이션이 안붙은) 아무 클래스를 autowired하려고 할경우

public class AutowiredTest {
	@Test
	void autowiredOption(){
		ApplicationContext ac = new AnnotationConfigApplicationContext(TestBean.class);
	}

	static class TestBean{
		// UnsatisfiedDependencyException 예외가 터짐
		// @Autowired
		// public void setNoBean1(Member noBean1) {
		// 	System.out.println("noBean1 = " + noBean1);
		// }

		@Autowired(required = false)
		public void setNoBean1(Member noBean1) {
			System.out.println("noBean1 = " + noBean1);
		}

		@Autowired
		public void setNoBean2(@Nullable Member noBean2) {
			System.out.println("noBean2 = " + noBean2);
		}

		@Autowired
		public void setNoBean3(Optional<Member> noBean3){
			System.out.println("noBean3 = " + noBean3);
		}
	}
}

<결과>
noBean2 = null
noBean3 = Optional.empty

<설명>
1. @Autowired
자동주입할 대상이 없으면 예외가 발생함

2. @Autowired(required = false)
자동주입할 대상이 없으면 수정자 메서드 자체가 호출이 안됨

3. @Nullable
@Nullable을 넣으면 자동주입할 대상이 없을경우 null을 받을 수 있음

4. Optional<타입>
타입 대신 Optional<타입> 이렇게 Optional로 감싸서 넣으면 자동주입할 대상이 없을 경우 Optional.empty를 받을 수 있음. (값이있으면 Optional로 감싼값이 들어감)


@Nullable, Optional을 사용하면
null인경우에 default객체를 넣는 식으로 구현 가능함

참고로 @Nullable, Optional은 스프링 전반에 걸쳐서 지원됨. 생성자주입에서 특정 필드에만 사용해도 됨

----------------------------------------------------------------------------------------------------

롬복을 쓰면 자바의 어노테이션 프로세서라는 기능을 이용해서 컴파일 시점에 생성자 코드를 자동으로 생성해줌

cmd + f12 혹은 class를 열어보면 생성자가 들어있는걸 확인할 수 있음

최근에는 생성자를 딱 1개 두고, @Autowired를 생략하는 방법을 주로 사용함
여기에 Lombok 라이브러리의 @RequiredArgsConstructor를 함께 사용하면 기능은 다 제공하면서, 코드는 깔끔하게 사용할 수 있음

----------------------------------------------------------------------------------------------------

조회 빈이 2개 이상일때의 문제

@Autowired는 타입으로 조회함

@Autowired
private DiscountPolicy discountPolicy

타입으로 조회하기 때문에 마치 다음 코드와 유사하게 동작함(실제로는 더 많은 기능을 제공함)
ac.getBean(DiscountPolicy.class)

타입으로 조회하면 선택된 빈이 2개 이상일 때 문제가 발생함
Caused by: org.springframework.beans.factory.NoUniqueBeanDefinitionException: No qualifying bean of type 'hello.core.discount.DiscountPolicy' available: expected single matching bean but found 2: fixDiscountPolicy,rateDiscountPolicy
↓↓↓
하나의 빈을 기대했는데 fixDiscountPolicy,rateDiscountPolicy 2개가 발견되었다는 뜻

이때 하위 타입으로 지정할수도 있지만 DIP를 위배하고 유연성이 떨어짐
그리고 이름만 다르고 완전히 똑같은 타입의 스프링빈이 2개있을때 해결이 안됨

해결 방법은 여러가지가 있음

------------------------------

@Autowired 필드 명 매칭

필드명을 빈 이름으로 변경

@RequiredArgsConstructor
public class OrderServiceImpl implements OrderService{
	private final MemberRepository memberRepository;
	private final DiscountPolicy discountPolicy;
↓↓↓
@RequiredArgsConstructor
public class OrderServiceImpl implements OrderService{
	private final MemberRepository memberRepository;
	private final DiscountPolicy rateDiscountPolicy;

or

생성자 파라미터 변수명을 바꿔도 됨

public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy rateDiscountPolicy) {
	this.memberRepository = memberRepository;
	this.discountPolicy = rateDiscountPolicy;
}

------------------------------

@Quilifier 사용

아래처럼 미리 이름을 지정해놓으면

@Component
@Qualifier("mainDiscountPolicy")
public class RateDiscountPolicy implements DiscountPolicy{

@Component
@Qualifier("fixDiscountPolicy")
public class FixDiscountPolicy implements DiscountPolicy{

아래처럼 생성자주입할때 @Qualifier 를 붙여서 원하는걸 쓸 수 있음
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
	this.memberRepository = memberRepository;
	this.discountPolicy = discountPolicy;
}

만약 같은 이름의 Qualifier를 못찾으면 bean이름중에 같은 이름을 찾음(하지만 @Qualifier는 @Qualifier를 찾는 용도로만 사용하는게 명확하고 좋음)

1. @Qualifier끼리 매칭
2. 빈 이름 매칭
3. NoSuchBeanDefinitionException 예외 발생


직접 빈 등록시에도 @Qualifier를 동일하게 선언할 수 있음

@Bean
@Qualifier("mainDiscountPolicy")
public DiscountPolicy discountPolicy(){
}

------------------------------

@Primary 사용

@Primary는 우선순위를 정하는 방법임
@Autowired 시에 여러개의 빈이 매칭되면 @Primary가 우선권을 가짐

@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy{

------------------------------

@Primary 와 @Qualifier 중에 어떤것을 선택해야할까

@Qualifier의 단점은 주입받을 때 모든 코드에 @Qualifier를 붙여줘야 한다는 것임
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
	this.memberRepository = memberRepository;
	this.discountPolicy = discountPolicy;
}

반면에 @Primary를 쓰면 위처럼 @Qualifier를 붙일 필요가 없음

예를들어 메인DB의 커넥션을 획득하는 스프링빈이 있고
코드에서 특별한 기능으로 가끔 사용하는 서브DB의 커넥션을 획득하는 스프링빈이 있다고 할때
메인DB의 커넥션을 획득하는 스프링빈은 @Primary를 적용해, 조회하는곳에서 @Qualifier지정없이 편하게 조회하고
서버DB의 커넥션을 획득하는 스프링빈은 @Qualifier를 지정해서 획득하는 방식으로 하면 코드를 깔끔하게 유지할 수 있음
물론 이때 메인DB의 스프링빈을 등록할때 @Qualifier를 지정해주는것은 상관없음

우선순위
@Primary는 기본값처럼 동작하는것이고, @Qualifier는 매우 상세하게 동작함
스프링은 자동보다는 수동이, 넓은 범위의 선택권보다는 좁은 범위의 선택권이 우선순위가 높음
따라서 여기서도 @Qualifier가 우선권이 높음

----------------------------------------------------------------------------------------------------

@Qualifier 단점

@Qualifier("mainDiscountPolicy")
문자열이라서 컴파일시 타입 체크가 안됨

애노테이션을 만들어서 문제를 해결할 수 있음


특별한 방법은 아니고 그냥 @Qualifier을 상속받는것처럼 보이는 애노테이션을 하나 만들면 됨

@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
@Qualifier("mainDiscountPolicy")
public @interface MainDiscountPolicy {
}

설명
@Qualifier애노테이션을 들어가서 붙어있는 어노테이션을 다 복사해서 붙이고, @Qualifier("XXX") 이걸 추가로 붙여주면 됨

만들었으면
@Qualifier("mainDiscountPolicy") 대신

@MainDiscountPolicy
이렇게 방금 만든 사용자어노테이션을 쓰기

----------------------------------------------------------------------------------------------------

조회한 빈이 모두 필요할 때 (List, Map)

public class AllBeanTest {
	@Test
	void findAllBean(){
		ApplicationContext ac = new AnnotationConfigApplicationContext(AutoAppConfig.class, DiscountService.class);
	}

	static class DiscountService{
		private final Map<String, DiscountPolicy> policyMap;
		private final List<DiscountPolicy> policies;

		public DiscountService(Map<String, DiscountPolicy> policyMap, List<DiscountPolicy> policies) {
			this.policyMap = policyMap;
			this.policies = policies;
			System.out.println("policyMap = " + policyMap);
			System.out.println("policies = " + policies);
		}
	}
}

AnnotationConfigApplicationContext 생성자의 다른 인수에서 등록한빈들을 즉시 주입받을수있음
그리고 생성자를 Map<String, 스프링빈클래스> 혹은 List<스프링빈클래스> 이렇게 선언해놓으면 바로 받을 수 있음

map은 key로 빈이름, value로 객체가 들어가고,
List는 바로 value가 들어감

<출력결과>
policyMap = {fixDiscountPolicy=hello.core.discount.FixDiscountPolicy@6c25e6c4, rateDiscountPolicy=hello.core.discount.RateDiscountPolicy@85e6769}
policies = [hello.core.discount.FixDiscountPolicy@6c25e6c4, hello.core.discount.RateDiscountPolicy@85e6769]

이후 DiscountService에서 빈이름(String)을 인수로 받는 메소드를 만들어서 .get(빈이름) 이렇게 빈을 활용할 수 있음

----------------------------------------------------------------------------------------------------

스프링 빈 자동등록 or 수동등록 기준

스프링이 나오고 시간이 갈수록 점점 자동을 선호하는 추세
스프링은 @Component뿐만 아니라 @Controller, @Service, @Repository처럼 계층에 맞추어 일반적인 애플리케이션 로직을 자동으로 스캔할 수 있도록 지원함
거기에 더해서 스프링부트는 컴포넌트스캔을 기본으로 사용하고, 스프링부트의 다양한 스프링빈들도 조건이 맞으면 자동으로 등록하도록 설계했음

설정정보를 기반으로, 애플리케이션을 구성하는 부분 / 실제 동작하는 부분 을 명확하게 나누는게 이상적이지만
개발자입장에서 @Component 만 넣으면 끝나는 일을 @Configuration 설정정보에 가서 @Bean을 적고, 객체를 생성하고, 주입할 대상을 일일이 적어주는 과정은 상당히 번거로음
또 관리할 빈이 많아서 설정 정보가 커지면 설정 정보를 관리하는것 자체가 부담이 됨
그리고 결정적으로 자동 빈 등록을 사용해도 OOP, DIP를 지킬 수 있음

------------------------------

업무 로직 빈 : 웹을 지원하는 컨트롤러, 핵심 비즈니스 로직이 있는 서비스, 데이터 계층의 로직을 처리하는 리파지토리 등
기술 지원 빈 : 기술적인 문제나 공통 관심사(AOP)를 처리할 때 주로 사용됨. DB연결이나, 공통 로그 처리 처럼 업무 로직을 지원하기 위한 하부 기술이나 공통 기술들

업무 로직은 숫자도 매우 많고, 한번 개발해야 하면 컨트롤러, 서비스, 리파지토리처럼 어느정도 유사한 패턴이 있음. 이런경우 자동 기능을 적극 사용하는것이 좋음
보통 문제가 발생해도 어떤 곳에서 문제가 발생했는지 명확하게 파악하기 쉬움

기술지원 로직은 업무 로직과 비교해서 그 수가 매우 적고, 보통 애플리케이션 전반에 걸쳐서 광범위하게 영향을 미침. 그리고 업무로직은 문제가 발생했을때 어디가 문제인지
명확하게 잘 드러나지만, 기술 지원 로직은 적용이 잘 되고있는지 아닌지 조차 파악하기 어려운 경우가 많음
그래서 이런 기술지원 로직들은 가급적 수동 빈 등록을 사용해서 명확하게 드러내는게 좋음

애플리케이션에 광범위하게 영향을 미치는 기술 지원 객체는 수동 빈으로 등록해서 딱! 설정 정보에 바로 나타나게 하는 것이 유지보수에 좋음

------------------------------

비즈니스 로직중에서 다형성을 적극 활용할 때

Map<String, DiscountPolicy>에 주입을 받는 상황을 생각해봤을때

class DiscountService{
	private final Map<String, DiscountPolicy> policyMap;
	private final List<DiscountPolicy> policies;

	public DiscountService(Map<String, DiscountPolicy> policyMap, List<DiscountPolicy> policies) {
		this.policyMap = policyMap;
		this.policies = policies;
		System.out.println("policyMap = " + policyMap);
		System.out.println("policies = " + policies);
	}

	public int discount(Member member, int price, String discountPolicy) {
		DiscountPolicy policy = policyMap.get(discountPolicy);
		return policy.discount(member, price);
	}
}

여기에 어떤 빈들이 주입될지, 각 빈들의 이름은 무엇일지 코드만 보고 한번에 쉽게 파악하기 어려움
내가 개발했으니 크게 관계가 없지만, 만약 이 코드를 다른 개발자가 개발해서 나에게 준것이라면?
자동 등록을 사용하고 있기 때문에 파악하려면 여러 코드를 찾아봐야함

이런경우 수동 빈으로 등록하거나 or 자동으로 하려면 "특정 패키지에 같이 묶어"두는게 좋음(RateDiscountPolicy와 관련된 인터페이스&구현체는 한곳에 모여있어야함)
핵심은 딱 보고 이해가 되어야 함

<자동>
@Component
public class FixDiscountPolicy implements DiscountPolicy{
}
@Component
public class RateDiscountPolicy implements DiscountPolicy{
}

<수동>
@Configuration
public class DiscountPolicyConfig{
	@Bean
	public DiscountPolicy rateDiscountPolicy(){
		return new RateDiscountPolicy();
	}
	@Bean
	public DiscountPolicy fixDiscountPolicy(){
		return new FixDiscountPolicy();
	}
}

------------------------------

참고로 스프링과 스프링부트가 자동으로 등록하는 수많은 빈들은 예외임

이런 부분들은 스프링 자체를 잘 이해하고 스프링의 의도대로 잘 사용하는게 중요함
스프링부트의 경우 DataSource같은 DB연결에 사용하는 기술 지원 로직까지 내부에서 자동으로 등록하는데,
이런 부분은 메뉴얼을 잘 참고해서 스프링부트가 의도한 대로 편리하게 사용하면 됨

반면에 스프링부트가 아니라 내가 직접 기술 지원 객체를 스프링 빈으로 등록한다면 수동으로 등록해서 명확하게 드러내는게 좋음

----------------------------------------------------------------------------------------------------

@Value

application.yml 에서 등록한 값을 가져올 수 있음

@Configuration
public class MyComponent {
    @Value("${opensearch.protocol}")
    private String protocol;
}


다른 프로퍼티 파일을 가져오고싶은경우 아래처럼 @PropertySource 를 이용해 프로퍼티파일의 경로를 지정하기

@Configuration
@PropertySource("classpath:custom.properties")
public class MyComponent {
    @Value("${opensearch.protocol}")
    private String protocol;
}

참고로 classpath: 는 보통 src/main/resources 라고 생각하면됨

정확히는 gradle 설정파일의 sourceSets 쪽에 있음
sourceSets {
    main {
        resources {
            srcDirs 'src/main/resources'
        }
    }
}

----------------------------------------------------------------------------------------------------

커넥션풀

애플리케이션 서버가 뜰때 DB와 연결을 미리 맺어놓음

연결하는데 오래걸리기때문에, 미리 연결을 100개, 200개 해놓고 요청이 올때 미리 연결해놓은걸 그대로 재활용할 수 있음

네트워크를 가지고 서버가 뜰때 미리 다른쪽이랑 통신할수있게 미리 열어놔야함. 그럼 다음에 고객의 요청이왔을때 이미 열려있는 소켓으로 빠른 응답이 가능함

그리고 연결을 미리 끊어줘야함. 안끄고 놔두면 서버가 꺼질때 꺼지는데 그러면 데이터가 날라갈까봐 불안하기때문에, 안전하게 정상적으로 잘 종료하는 작업을 스프링이 제공함

----------------------------------------------------------------------------------------------------

빈 생명주기 콜백

스프링빈이 생성되거나, 소멸되기 직전에 스프링이 스프링빈 안에 있는 메서드를 호출해 줄수 있는 기능

스프링빈(세터주입, 필드주입)은 간단하게 다음과 같은 라이프사이클을 가짐(생성자 주입은 예외. 객체를 만들때 인수로 스프링빈을 넣어야하므로)
객체생성 → 의존관계 주입

스프링빈은 객체를 생성하고, 의존관계 주입이 다 끝난 다음에야 필요한 데이터를 사용할 수 있는 준비가 됨
따라서 초기화작업은 의존관계 주입이 모두 완료되고 난 다음에 해야함

그런데 개발자가 의존관계 주입이 모두 완료된 시점을 어떻게 알 수 있을까?

스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공함
또한 스프링은 컨테이너가 종료되기 직전에 소멸 콜백을 줌. 따라서 안전하게 종료 작업을 진행할 수 있음

스프링빈의 이벤트 라이프사이클
스프링 컨테이너 생성 → 스프링빈 생성 → 의존관계 주입 → 초기화 콜백 → 사용 → 소멸전 콜백 → 스프링 종료

초기화 콜백 : 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출
소멸전 콜백 : 빈이 소멸되기 직전에 호출

스프링은 다양한 방식으로 생명주기 콜백을 지원함


객체의 생성과 초기화를 분리해야함

생성자는 필수 정보(파라미터)를 받고, 메모리를 할당해서 객체를 생성하는 책임을 가짐
반면에 초기화는 이렇게 생성된 값들을 활용해서 외부 커넥션을 연결하는 등 무거운 동작을 수행함

따라서 생성자 안에서 무거운 초기화 작업을 함께하는것 보다는 객체를 생성하는 부분과 초기화하는 부분을 명확하게 나누는 것이 유지보수 관점에서 좋음
물론 초기화 작업이 내부 값들을 약간 변경하는 정도로 단순한 경우에는 생성자에서 한번에 다 처리하는게 나을 수 있음

------------------------------

스프링은 3가지 방법으로 빈 생명주기 콜백을 지원함

방법1. 인터페이스(InitializingBean, DisposableBean)
방법2. 설정 정보에 초기화 메서드, 종료 메서드 지정
방법3. @PostConstruct, @PreDestroy 애노테이션 지원

------------------------------

인터페이스로 하는 방법

public class NetworkClient implements InitializingBean, DisposableBean {
	private String url;

	public NetworkClient() {
		System.out.println("생성자 호출, url = " + url);
	}

	public void setUrl(String url) {
		this.url = url;
	}

	// 서비스 시작시 호출
	public void connect(){
		System.out.println("connect: " + url);
	}

	public void call(String message){
		System.out.println("call: " + url + "message = " + message);
	}

	// 서비스 종료시 호출
	public void disconnect(){
		System.out.println("close: " + url);
	}

	@Override
	public void afterPropertiesSet() throws Exception {
		System.out.println("NetworkClient.afterPropertiesSet");
		connect();
		call("초기화 연결 메시지");
	}

	@Override
	public void destroy() throws Exception {
		System.out.println("NetworkClient.destroy");
		disconnect();
	}
}

public class BeanLifeCycleTest {
	@Test
	public void lifeCycleTest(){
		ConfigurableApplicationContext ac = new AnnotationConfigApplicationContext(LifeCycle.class);
		NetworkClient client = ac.getBean(NetworkClient.class);
		ac.close();
	}

	@Configuration
	static class LifeCycle{
		@Bean
		public NetworkClient networkClient(){
			NetworkClient networkClient = new NetworkClient();
			networkClient.setUrl("http://hello-spring.dev");
			return networkClient;
		}
	}
}

-----

출력 결과

생성자 호출, url = null
NetworkClient.afterPropertiesSet
connect: http://hello-spring.dev
call: http://hello-spring.devmessage = 초기화 연결 메시지
20:25:14.371 [main] DEBUG org.springframework.context.annotation.AnnotationConfigApplicationContext - Closing org.springframework.context.annotation.AnnotationConfigApplicationContext@342c38f8, started on Wed Sep 20 20:25:14 KST 2023
NetworkClient.destroy
close: http://hello-spring.dev


인터페이스 방법의 단점

이 인터페이스는 스프링 전용 인터페이스임. 해당코드가 스프링 전용 인터페이스에 의존함
초기화, 소멸 메서드의 이름을 변경할 수 없음
내가 코드를 고칠 수 없는 외부 라이브러리에 적용할 수 없음

인터페이스를 사용하는 초기화, 종료 방법은 스프링 초창기에 나온 방법들이고, 지금은 더 나은 벙법들이 있어서 거의 사용하지 않음

------------------------------

설정 정보에 지정하는 방법

public class NetworkClient{
	private String url;

	public NetworkClient() {
		System.out.println("생성자 호출, url = " + url);
	}

	public void setUrl(String url) {
		this.url = url;
	}

	// 서비스 시작시 호출
	public void connect(){
		System.out.println("connect: " + url);
	}

	public void call(String message){
		System.out.println("call: " + url + "message = " + message);
	}

	// 서비스 종료시 호출
	public void disconnect(){
		System.out.println("close: " + url);
	}

	public void init() throws Exception {
		System.out.println("NetworkClient.init");
		connect();
		call("초기화 연결 메시지");
	}

	public void close() throws Exception {
		System.out.println("NetworkClient.close");
		disconnect();
	}
}

public class BeanLifeCycleTest {
	@Test
	public void lifeCycleTest(){
		ConfigurableApplicationContext ac = new AnnotationConfigApplicationContext(LifeCycle.class);
		NetworkClient client = ac.getBean(NetworkClient.class);
		ac.close();
	}

	@Configuration
	static class LifeCycle{
		@Bean(initMethod = "init", destroyMethod = "close") // ★★★★★ 이부분 ★★★★★
		public NetworkClient networkClient(){
			NetworkClient networkClient = new NetworkClient();
			networkClient.setUrl("http://hello-spring.dev");
			return networkClient;
		}
	}
}

-----

@Bean 애노테이션에 initMethod / destroyMethod 속성을 추가하면 됨

출력 결과는 다른 방법들로 했을때와 동일함


설정정보 사용 방법 특징

메서드 이름을 자유롭게 줄 수 있음
스프링 빈이 스프링 코드에 의존하지 않음
코드가 아니라 설정정보를 사용하기 때문에 코드를 고칠 수 없는 외부 라이브러리에도 초기화, 종료 메서드를 적용할 수 있음


@Bean의 destroyMethod 속성에는 아주 특별한 기능이 있음
destroyMethod 속성의 기본값은 추론된 이라는 뜻의 "(inferred)" 가 설정돼있는데
라이브러리는 대부분 close, shutdown 이라는 이름의 종료 메서드를 사용함
이 추론 기능은 close, shutdown 라는 이름의 메서드를 자동으로 호출해줌. 이름 그대로 종료메서드를 추론해서 호출해줌

따라서 직접 스프링 빈으로 등록하면 종료메서드는 따로 적어주지 않아도 잘 동작함

추론 기능을 사용하기 싫으면 destroyMethod="" 이렇게 빈 공백을 지정하면 됨

------------------------------

애노테이션 @PostConstruct, @PreDestroy 로 하는 방법

public class NetworkClient{
	private String url;

	public NetworkClient() {
		System.out.println("생성자 호출, url = " + url);
	}

	public void setUrl(String url) {
		this.url = url;
	}

	// 서비스 시작시 호출
	public void connect(){
		System.out.println("connect: " + url);
	}

	public void call(String message){
		System.out.println("call: " + url + "message = " + message);
	}

	// 서비스 종료시 호출
	public void disconnect(){
		System.out.println("close: " + url);
	}

	@PostConstruct // ★★★★★ 이부분 ★★★★★
	public void init() throws Exception {
		System.out.println("NetworkClient.init");
		connect();
		call("초기화 연결 메시지");
	}

	@PreDestroy // ★★★★★ 이부분 ★★★★★
	public void close() throws Exception {
		System.out.println("NetworkClient.close");
		disconnect();
	}
}

public class BeanLifeCycleTest {
	@Test
	public void lifeCycleTest(){
		ConfigurableApplicationContext ac = new AnnotationConfigApplicationContext(LifeCycle.class);
		NetworkClient client = ac.getBean(NetworkClient.class);
		ac.close();
	}

	@Configuration
	static class LifeCycle{
		@Bean
		public NetworkClient networkClient(){
			NetworkClient networkClient = new NetworkClient();
			networkClient.setUrl("http://hello-spring.dev");
			return networkClient;
		}
	}
}

-----

출력 결과는 다른 방법들로 했을때와 동일함


애노테이션 사용 방법 특징

최신 스프링에서 가장 권장하는 방법임
애노테이션 하나만 붙이면 되므로 매우 편리함
패키지를 잘 보면 javax.annotation 임. 스프링에 종속적인 기술이 아니라 JSR-250이라는 자바 표준임. 따라서 스프링이 아닌 다른 컨테이너에서도 동작함
컴포넌트 스캔과 잘 어울림
유일한 단점은 외부 라이브러리에는 적용하지 못한다는 것임. 외부라이브러리를 초기화/종료 해야하면 @Bean의 속성으로 하는 방법을 쓰기

----------------------------------------------------------------------------------------------------

빈 스코프

지금까지는 스프링빈이 스프링컨테이너의 시작과 함께 생성되어서 스프링컨테이너가 종료될때까지 유지된다고 학습했음
이것은 스프링빈이 기본적으로 싱글톤 스코프로 생성되기 때문임. 스코프는 번역 그대로, 빈이 존재할 수 있는 범위를 뜻함


싱글톤 스코프 : 기본 스코프. 스프링컨테이너의 시작과 종료까지 유지되는 가장 넒은 범위의 스코프임
prototype(프로토타입) : 스프링컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 유지되는 매우 짧은 범위의 스코프
웹 관련 스코프
	request : 웹 요청이 들어오고 나갈때까지 유지되는 스코프
	session : 웹 세션이 생성되고 종료될 때까지 유지되는 스코프
	application : 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 스코프

------------------------------

스코프 지정 방법


컴포넌트 스캔 자동 등록

@Scope("prototype")
@Component
public class HelloBean{
}


수동 등록

@Scope("prototype")
@Bean
PrototypeBean HelloBean(){
	return new HelloBean();
}

------------------------------

싱글톤 스코프의 빈을 조회하면 스프링컨테이너는 항상 같은 인스턴스의 스프링빈을 반환함

반면에 프로토타입 스코프를 스프링컨테이너에 조회하면 스프링컨테이너는 항상 새로운 인스턴스를 생성해서 반환함

-----

싱글톤 스코프 메커니즘

1. 싱글톤 스코프의 빈을 스프링 컨테이너에 요청함
2. 스프링 컨테이너는 본인이 관리하는 스프링 객체를 반환함
3. 이후에 스프링 컨테이너에 같은 요청이 와도 같은 인스턴스의 스프링빈을 반환함

즉, 같은 주소를 공유해서 사용함

-----

프로토타입 스코프 메커니즘

1. 프로토타입 스코프의 빈을 스프링컨테이너에게 요청함
2. 스프링컨테이너는 이 시점에 프로토타입 빈을 생성하고, 필요한 의존관계를 주입함
3. 스프링컨테이너는 생성한 프로토타입 빈을 클라이언트에 반환함
4. 이후에 스프링 컨테이너에 같은 요청이 오면 항상 새로운 프로토타입 빈을 생성해서 반환함

스프링컨테이너는 빈 생성, 의존관계 주입, 초기화 까지만 처리한 후 그 빈을 클라이언트에 반환하고, 그 이후에는 한번 생성했던 프로토타입 빈을 관리하지 않음
프로토타입 빈을 관리할 책임은 프로토타입 빈을 받은 클라이언트에 있음. 그래서 @PreDestroy같은 종료 메서드가 동작하지 않음

------------------------------

싱글톤 스코프 예제

public class SingletonTest {
	@Test
	void singletonBeanFind(){
		AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SingletonBean.class);
		System.out.println("find singletonBean1");
		SingletonBean singletonBean1 = ac.getBean(SingletonBean.class);
		System.out.println("find singletonBean2");
		SingletonBean singletonBean2 = ac.getBean(SingletonBean.class);

		System.out.println("singletonBean1 = " + singletonBean1);
		System.out.println("singletonBean2 = " + singletonBean2);
		assertThat(singletonBean1).isSameAs(singletonBean2);
		ac.close();
	}

	@Scope("singleton")
	static class SingletonBean{
		@PostConstruct
		public void init(){
			System.out.println("SingletonBean.init");
		}

		@PreDestroy
		public void destroy() {
			System.out.println("SingletonBean.destroy");
		}
	}
}

-----

참고로 AnnotationConfigApplicationContext 생성자의 인수로 클래스리터럴을 넣으면 자동으로 스프링컨테이너의 설정클래스로 사용됨 @Configuration을 안붙여도됨

출력결과
SingletonBean.init
find singletonBean1
find singletonBean2
singletonBean1 = hello.core.scope.SingletonTest$SingletonBean@3daf7722
singletonBean2 = hello.core.scope.SingletonTest$SingletonBean@3daf7722
22:24:19.415 [main] DEBUG org.springframework.context.annotation.AnnotationConfigApplicationContext - Closing org.springframework.context.annotation.AnnotationConfigApplicationContext@43dac38f, started on Wed Sep 20 22:24:19 KST 2023
SingletonBean.destroy

------------------------------

프로토타입 스코프 예제

public class PrototypeTest {
	@Test
	void prototypeBeanFind(){
		AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(PrototypeBean.class);
		System.out.println("find prototypeBean1");
		PrototypeBean prototypeBean1 = ac.getBean(PrototypeBean.class);
		System.out.println("find prototypeBean2");
		PrototypeBean prototypeBean2 = ac.getBean(PrototypeBean.class);

		System.out.println("prototypeBean1 = " + prototypeBean1);
		System.out.println("prototypeBean2 = " + prototypeBean2);
		assertThat(prototypeBean1).isNotSameAs(prototypeBean2);
		ac.close();
	}

	@Scope("prototype")
	static class PrototypeBean{
		@PostConstruct
		public void init(){
			System.out.println("PrototypeBean.init");
		}

		@PreDestroy
		public void destroy() {
			System.out.println("PrototypeBean.destroy");
		}
	}
}

-----

출력결과
find prototypeBean1
PrototypeBean.init
find prototypeBean2
PrototypeBean.init
prototypeBean1 = hello.core.scope.PrototypeTest$PrototypeBean@6c2c1385
prototypeBean2 = hello.core.scope.PrototypeTest$PrototypeBean@5f354bcf
22:25:41.176 [main] DEBUG org.springframework.context.annotation.AnnotationConfigApplicationContext - Closing org.springframework.context.annotation.AnnotationConfigApplicationContext@2ed2d9cb, started on Wed Sep 20 22:25:41 KST 2023

destroy 메서드가 호출되지 않음. 프로토타입이라는 이름 그대로 만들고 버린(관리대상으로부터 제외한)것

------------------------------

정리

싱글톤 빈은 스프링컨테이너 생성 시점에 초기화 메서드가 실행되지만, 프로토타입 스코프의 빈은 스프링컨테이너에서 빈을 조회할 때 생성되고, 초기화 메서드도 이때 실행됨
프로토타입 빈을 2번 조회하면 완전히 다른 스프링 빈이 생성되고, 초기화도 2번 실행됨

싱글톤 빈은 스프링컨테이너가 관리하기 때문에, 스프링 컨테이너가 종료될 때 빈의 종료메서드가 실행되지만,
프로토타입 빈은 스프링컨테이너가 생성과 프로토타입 빈은 스프링컨테이너가 생성과 의존관계 주입 그리고 초기화까지만 관여하고, 더는 관리하지 않음
따라서 프로토타입 빈은 스프링컨테이너가 종료될 때, @PreDestory같은 종료 메서드가 전혀 실행되지 않음. 필요하면 수동으로 호출해야함

-----

싱글톤 스코프
스프링컨테이너 생성 → 모든 빈 생성 → 각각의 빈 조회시 → 조회한 빈 초기화 → 최초 생성해놨던 빈(최초 생성한 빈의 주소에 해당하는 인스턴스) 반환 → 스프링컨테이너 종료시 → 모든 빈들의 종료 매서드 호출됨

프로토타입 스코프
스프링컨테이너 생성 → 이때는 빈 생성안함 → 각각의 빈 조회시 → 조회하려는 빈 생성 → 생성된 빈 초기화 → 생성된 빈(새 인스턴스) 반환 → 스프링컨테이너 종료시 → 관리하고있던 빈이 없으므로 종료 메서드 호출되지 않음

----------------------------------------------------------------------------------------------------

싱글톤에서 프로토타입 빈 사용시

public class SingletonWithPrototypeTest1 {
	@Test
	void singletonClientUsePrototype(){
		AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(PrototypeBean.class, ClientBean.class);

		ClientBean bean1 = ac.getBean(ClientBean.class);
		int cnt1 = bean1.logic();
		assertThat(cnt1).isEqualTo(1);

		ClientBean bean2 = ac.getBean(ClientBean.class);
		int cnt2 = bean2.logic();
		assertThat(cnt2).isEqualTo(2);
	}

	@Scope("singleton")
	static class ClientBean{
		private final PrototypeBean prototypeBean;

		public ClientBean(PrototypeBean prototypeBean) {
			this.prototypeBean = prototypeBean;
		}

		public int logic(){
			prototypeBean.addCnt();
			return prototypeBean.getCnt();
		}
	}

	@Scope("prototype")
	static class PrototypeBean{
		private int cnt;

		void addCnt(){
			cnt++;
		}

		int getCnt(){
			return cnt;
		}

	}
}

싱글톤빈이 프로로타입 빈을 사용하게 됨
그런데 싱글톤 빈은 생성 시점에만 의존관계 주입을 받기 때문에, 프로토타입 빈이 새로 생성되기는 하지만, 싱글톤 빈과 함께 계속 유지되는 것이 문제

아마 원하는것이 이런것은 아닐것이다
프로토타입 빈을 주입 시점에만 새로 생성하는게 아니라, 사용할 때마다 새로 생성해서 사용하는 것을 원할것

------------------------------

계속 새로운 빈을 찾는 방법

@Scope("singleton")
static class ClientBean{
	@Autowired private ApplicationContext ac;

	public int logic(){
		PrototypeBean prototypeBean = ac.getBean(PrototypeBean.class);
		prototypeBean.addCnt();
		return prototypeBean.getCnt();
	}
}

의존관계를 외부에서 주입(DI) 받는게 아니라 이렇게 직접 필요한 의존관계를 찾는것을 DL(Dependency Lookup) 의존관계 조회(탐색) 라고 함
그런데 이렇게 스프링 애플리케이션 컨텍스트 전체를 주입받게 되면, 스프링컨테이너에 종속적인 코드가 되고, 단위 테스트도 어려워짐

지금 필요한 기능은 지정한 프로토타입 빈을 컨테이너에서 대신 찾아와주는 딱 DL 정도의 기능만 제공하는 무언가가 있으면 됨

------------------------------

ObjectFactory, ObjectProvider

지정한 빈을 컨테이너에서 대신 찾아주는 DL서비스를 제공하는 것이 바로 ObjectProvider 임
장점은 스프링의 기능을 다 쓰는것이 아닌 일부만 쓰는것

ObjectProvider.getObject() 를 통해서 ★항상 새로운 프로토타입빈이 생성★됨

참고로 과거에는 ObjectFactory 가 있었는데, 여기에 편의 기능을 추가해서 ObjectProvider 가 만들어짐

@Scope("singleton")
static class ClientBean{
	@Autowired private ObjectProvider<PrototypeBean> prototypeBeanProvider;

	public int logic(){
		PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
		prototypeBean.addCnt();
		return prototypeBean.getCnt();
	}
}

필드 주입 대신 생성자주입으로 해도 됨

----------------------------------------------------------------------------------------------------

참고로 아래처럼 하면 빈등록이 안되어있더라도 빈으로 자동등록돼서 갖고와짐

XXXBean 이라는 클래스에 @Component가 안붙어있어도
ApplicationContext를 주입받고 .getBean메서드호출할때 넣으면 빈이 자동으로 생성되서 가져와짐

@Autowired
ApplicationContext ac;

public void m1(){
	PrototypeBean prototypeBean = ac.getBean(XXXBean.class);

----------------------------------------------------------------------------------------------------

웹 스코프

웹 환경에서만 동작되는 스코프
웹 스코프는 프로토타입과 다르게 해당 스코프의 종료시점까지 관리함. 따라서 종료 메서드가 호출됨


웹 스코프 종류

request : HTTP요청 하나가 들어오고 나갈때까지 유지되는 스코프. 각각의 요청마다 별도의 빈 인스턴스가 생성되고 관리됨
session : HTTP Session과 동일한 생명주기를 가지는 스코프
application : 서블릿 컨텍스트(ServletContext)와 동일한 생명주기를 가지는 스코프
websoket : 웹 소켓과 동일한 생명주기를 가지는 스코프


만약 두 클라이언트가 0.00001초까지 똑같이 컨트롤러로 요청을 했을때

컨트롤러 로직에서 request스코프와 관련된걸 호출하면 → 클라이언트A, 클라이언트B 가 각각 다른 인스턴스가 할당됨. 각각 다른 스프링 빈이 생성됨

------------------------------

사용법

웹 라이브러리 의존성 추가해야함
implementation 'org.springframework.boot:spring-boot-starter-web'

@Component
@Scope(value = "request")
public class MyLogger {
	private String uuid;
	private String requestURL;

	public void setRequestURL(String requestURL) {
		this.requestURL = requestURL;
	}

	public void log(String message) {
		System.out.println("[" + uuid + "]" + "[" + requestURL + "]" + message);
	}

	@PostConstruct
	public void init(){
		uuid = UUID.randomUUID().toString();
		System.out.println("[" + uuid + "] request scope bean create: " + this);
	}

	@PreDestroy
	public void close() {
		System.out.println("[" + uuid + "] request scope bean close: " + this);
	}
}

이렇게 하면 이 빈은 HTTP 요청 당 하나씩 생성되고, HTTP 요청이 끝나는 시점에 소멸됨.
빈이 생성되는 시점에 자동으로 @PostConstruct 초기화 메서드를 써서 저장해둠.
이 빈은 HTTP요청 당 하나씩 생성되므로, uuid를 저장해두면 다른 HTTP요청과 구분할 수 있음
이 빈이 소멸되는 시점에 @PreDestroy를 써서 종료 메시지를 남김
★requestURL은 이 빈이 생성되는 시점에는 알 수 없으므로, 외부에서 setter로 입력받아야함

참고로 requestURL을 MyLogger에 저장하는 부분은 컨트롤러보다는, 공통 처리가 가능한 스프링 인터셉터나 서블릿 필터같은 곳을 활용하는 것이 좋음

인터셉터 : HTTP요청이 컨트롤러 호출 직전에 공통화해서 처리할 수 있는것

request scope를 안쓰고 이 모든 정보를 서비스 계층에 넘기려면 파라미터가 많아져서 지저분해짐
또, 웹과 관련된 부분은 서비스계층까지 넘어가지 않고 컨트롤러까지만 써야함. 서비스 계층은 웹 기술에 종속되지 않고 순수하게 유지하는것이 유지보수 관점에서 좋음


<스프링컨테이너에 빈이 없는데 주입을 받으려고 할 경우 스프링 실행시 오류 발생>
@Controller
@RequiredArgsConstructor
public class LogDemoController {
	private final LogDemoService logDemoService;
	private final MyLogger myLogger;

	@RequestMapping("log-demo")
	@ResponseBody
	public String logDemo(HttpServletRequest request) {
		String requestURL = request.getRequestURL().toString();
		myLogger.setRequestURL(requestURL);

		myLogger.log("controller test");
		logDemoService.logic("tsetId");
		return "OK";
	}
}

스프링이 뜰때 컨트롤러가 스프링빈에 등록되고, 의존관계 주입이 일어나는데 이때 MyLogger가 @Scope("request") 인 경우,
request스코프의 생존범위는 고객의 요청이 들어왔다가 나갈때까지인데 고객의 요청이 아직 안들어온상태에서(빈이 없는상태에서) 빈 주입을 받으려고 하면 오류가 남


ObjectProvider를 써서 요청이 왔을때 빈 주입이 되게끔 해야함

private final ObjectProvider<MyLogger> myLogger;
이렇게 바꿔주면 MyLogger객체를 주입받는게 아니라 MyLogger객체를 찾을 수 있는(DL 할 수 있는) 참조객체가 주입이 됨

그다음 주입시점(요청이 왔을때)에 주입 받으면 됨
@RequestMapping("log-demo")
@ResponseBody
public String logDemo(HttpServletRequest request) {
	String requestURL = request.getRequestURL().toString();
	MyLogger myLogger = myLoggerProvider.getObject();
	myLogger.setRequestURL(requestURL);

이렇게 하면 myLogger.setRequestURL(requestURL) 이 호출될때, 즉, MyLogger객체가 실제로 사용될 때 빈이 초기화고 등록됨

서비스계층에서도 마찬가지로 ObjectProvider로 감싸서 주입받는객체를 실제 빈이 아닌 참조객체를 받도록 만들기

그럼 처음에는 주입이 일어나지않아 스프링 실행시 오류가 안나고, 클라이언트 요청이 온 후, Provider객체.getObject() 이 실행되는 시점에 스프링 빈으로 등록함

브래우저 새로고침 여러번 해서 막 요청해도 요청 UUID가 각각 다르게 잘 생성된걸 확인할 수 있음

----------------------------------------------------------------------------------------------------

@Scope 의 proxyMode 속성

위에서 Provider로, 클라이언트의 요청이 들어왔을때 빈이 등록되게 했는데 코드를 더 간단하게 줄일 수 있음

@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class MyLogger {

"가짜를 만든다"는 개념

그럼 아래처럼 Provider를 쓰지 않았는데도 오류없이 잘 동작함

@Controller
@RequiredArgsConstructor
public class LogDemoController {
	private final LogDemoService logDemoService;
	private final MyLogger myLogger;

	@RequestMapping("log-demo")
	@ResponseBody
	public String logDemo(HttpServletRequest request) {
		String requestURL = request.getRequestURL().toString();
		myLogger.setRequestURL(requestURL);

		myLogger.log("controller test");
		logDemoService.logic("tsetId");
		return "OK";
	}
}

@Service
@RequiredArgsConstructor
public class LogDemoService {
	private final MyLogger myLogger;
	public void logic(String id) {
		myLogger.log("service id = " + id);
	}
}


적용 대상이
클래스면 TARGET_CLASS 를,
인터페이스면 INTERFACES 를 쓰면 됨

------------------------------

원리는 가짜 프록시 클래스를 다른 빈에 미리 주입받아놓는것임
MyLogger객체가 사용되기전에, 로그를찍어보면 아래처럼 내가 만든 클래스가 아닌, 임의의 클래스가 찍히는걸 볼 수 있음

class hello.core.common.MyLogger$$EnhancerBySpringCGLIB$$6f1259b1

빈으로 등록될때 이 클래스로 만들어진 객체가 대신 등록된것.
의존관계 주입도 이 가짜 프록시 객체가 주입됨

가짜 프록시객체는 객체요청(필드/메서드 호출)이 오면 그때 실제 객체를 찾아서 내부적으로 바꿔치기함
가짜 프록시객체는 원본 클래스를 상속받아서 만들어졌기 때문에, 이 객체를 사용하는 클라이언트 입장에서는 사실 원본인지 아닌지도 모르게, 동일하게 쓸 수 있음(다형성)

가짜 프록시 객체는 실제 request scope와는 관계가 없음. 그냥 가짜이고, 내부에 단순한 위임 로직만 있고, 싱글톤처럼 동작함
그래서 싱글톤 빈을 사용하듯이 편리하게 request scope를 쓸 수 있음

Provider를 쓰든, 프록시를 쓰든 핵심은 "진짜 객체 조회를 꼭 필요한 시점까지 지연처리한다는 것" 이다

단지 애노테이션 설정변경만으로 원본객체를 프록시객체로 대체할 수 있음. 이것이 다형성과 DI컨테이너가 가진 큰 장점임

꼭 웹 스코프가 아니더라도 프록시는 쓸 수 있음 ( AOP도 딱 이 원리로 돌아감(가짜를 만들고 돌아가는것) )

------------------------------

주의점

마치 싱글톤을 쓰는 것 같지만 다르게 동작하기 때문에 주의해서 써야함

이런 특별한 scope는 꼭 필요한 곳에만 최소화해서 써야함. 무분별하게 쓰면 유지보수가 어려워짐

----------------------------------------------------------------------------------------------------

AOP (Aspect Oriented Programming)

공통 관심사항(cross-cutting concern, 공통 기능) / 핵심 관심사항(core concern, 특정한 비즈니스와 관련된 로직) 을 분리할 수 있음

ex) 모든 메소드들의 호출시간을 측정하고 싶을때
public Long join(Member member) {
	long start = System.currentTimeMillis();
	try {
		validateDuplicatedMember(member);
		memberRepository.save(member);
	} catch (Exception e) {
		System.out.println("MemberService.join()");
		e.printStackTrace();
	}finally {
		long finish = System.currentTimeMillis();
		long timeMs = finish - start;
		System.out.println("join = " + timeMs + "ms");
	}
	return member.getId();
}
public List<Member> findMembers(){
	long start = System.currentTimeMillis();
	try {
		return memberRepository.findAll();
	} finally {
		long finish = System.currentTimeMillis();
		long timeMs = finish - start;
		System.out.println("join = " + timeMs + "ms");
	}
}

위 코드에서 메서드들 공통의 시간측정 관련 코드들을 일반적인 방법으로 따로 빼기는 쉽지 않음

이때 AOP를 쓰면 됨

------------------------------

@Aspect
@Component
public class TimeTraceAop {

	@Around("execution(* hello.hellospring..*(..))")
	public Object execute(ProceedingJoinPoint joinPoint) throws Throwable{
		long start = System.currentTimeMillis();
		System.out.println("START: " + joinPoint.toString());
		try {
			return joinPoint.proceed();
		} finally {
			long finish = System.currentTimeMillis();
			long timeMs = finish - start;
			System.out.println("END: " + joinPoint.toString() + " " + timeMs + "ms");
		}
	}
}

이때 "@Component 애노테이션"으로 스프링빈 등록을 해도 되지만, 이런 특별한 역할을 하는 클래스는 직접 수동등록(@Configuration / @Bean) 등록하는게 좋음
그럼 설정클래스를 보고 AOP가 등록돼서 쓰이는구나를 알 수 있음. (반대로 @Controller @Service @Repository 같은 정형화된 패턴은 그냥 애노테이션으로 하는게 좋음)

@Around 로 어느곳에 적용할건지 지정할 수 있음
<AOP의 Pointcut 표현식>
@Around("execution(* hello.hellospring.service.MemberService.findMembers(..))") : hello.hellospring.service패키지 밑 MemberService클래스의 findMembers메서드에 적용
@Around("execution(* hello.hellospring.service.MemberService(..))") : hello.hellospring.service패키지 밑 MemberService클래스의 모든 메서드에 적용
@Around("execution(* hello.hellospring.service.*(..))") : hello.hellospring.service패키지 밑 모든 클래스의 모든 메서드에 적용
@Around("execution(* hello.hellospring..*(..))") : hello.hellospring패키지 밑 모든 패키지 밑 모든 클래스의 모든 메서드에 적용
@Around("execution(* ~~~~~~~~~~~~~~(..))") : 메서드 파라미터 개수가 0개이상 (전체. 파라미터가 없든 몇개가 있든 상관없음)
@Around("execution(* ~~~~~~~~~~~~~~())") : 메서드 파라미터 개수가 0개 (파라미터가 없는 메서드)

------------------------------

스프링의 AOP 동작 방식은 프록시를 사용함

----------------------------------------------------------------------------------------------------







































