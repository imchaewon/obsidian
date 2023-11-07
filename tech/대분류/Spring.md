파라미터 (이름은 알아서 수정)

HttpServletRequest req : 세션 조회/조작, 쿠키 조회
HttpServletResponse resp : 쿠키 조작
Model model : 컨트롤러에서 뷰로 데이터를 전달할때 이용(jsp/servlet에서는 HttpServletRequest request 를 사용함)
RedirectAttributes rttr : 다른 jsp로 데이터를 갖고 이동시킬때 이용 (addFlashAttribute 말고 그냥 addAttribute는 el 못씀★)

----------------------------------------------------------------------------------------------------

오류모음

★ 404오류

서버 시작안됨 : 톰캣버전 달라서 발생하는 오류
 : Window → Preferences → Server → Runtime Environment에서 지우고 다시 만들기

서버 시작되면서 오류1 (The Network Adapter could not establish the connection)
 : OracleXE & OracleXETNSListener 켜져있는지 확인, 오라클 계정이 root-context.xml설정과 일치하는지 확인
		테이블 등 DB가 일치하는지 확인

스프링 빨간엑스(probloms창에  Error occured processing XML 'Are you using a JRE with an outdated version of '. See Error Log
for more details root-context.xml   /ex00/src/main/webapp/WEB-INF/spring Unknown Spring Beans Problem)
 : 전 컴퓨터와 jdk 버전이 달라서 발생하는 오류 : 프로젝트우클릭 → Biuld Path → Configure Biuld path에서 지우고 만들기

오류가 없는데 servlet-context.xml, root-context.xml에 엑스표시
 : 프로젝트 우클릭 → Spring → Remove Spring Project Nature

서버 실행시 오류(could not create the java virtual machine)
: 이클립스 자바 버전이 자바 버전(jdk)보다 높은지 확인 cmd(관리 자권한으로실행) → java -version 이거 확인하고
자바 11버전 

cmd에서 java명령어가 안될때(명령어 실행했는데 3초 멈췄다가 아무일도 안일어날때)
: 환경변수 → 시스템변수의 Path → 편집 → C:\Program Files\Common Files\Oracle\Java\javapath 이것과
%JAVA_HOME%\bin 이게 같이 있는지 확인 두개가  있다면 C:\Program Files\Common Files\Oracle\Java\javapath 이거 지우기

서버 실행시 오류2 (Port 8080 required by Tomcat v9.0 Server at localhost is already in use.)
: 오라클과 톰캣이 같은 8080포트를 써서 충돌하는것
이클립스에서 포트를 바꾸거나, 오라클을 바꾸거나 하면 됨
톰캣을 바꾸기(이클립스) : 서버더블클릭 → Port Name부분 HTTP/1.1을 8080에서 다른번호로 변경
오라클을 바꾸기(cmd/sql디벨로퍼) : exec dbms_xdb.sethttpport(9090); (권한이 있는 사용자로)

서버 실행안되면 이클립스에서
빨간네모 정지버튼 누르고 다시 실행시켜보기

그래도 안되면.. cmd에
netstat -a -n -o -p tcp입력후 포트번호 확인후 해당 pid로 강제종료
taskkill /f /pid 444


서버 실행시 ORA-12505 오류날시.. cmd에
lsnrctl service 쳐서 → 상태 : ready 인 항목 확인 후 "XE" or "orcl" 등으로 DB접속시 SID변경

안되면.. SQL Devloper 실행해서 계정 접속해놓고 실행해보기


서버는 정상 실행됬는데 주소창에 쳤는데 404에러 뜰때
: 서버더블클릭 → Modules탭 → Path 바꾸기 "Controller" → "/" → 서버 재시작


Error parsing Mapper XML. The XML location is 'com/fitper/mapper/MemberMapper.xml'.
↓↓↓
해당 xml에 같은 id의 sql태그가 2개있는지 확인


mybatis xml에서 mapper 태그 namespace 잘못썼는지 확인


mybatis xml에서 select태그 받는 type으로 vo쓸때 도메인 다 안쓰고 vo클래스명만 쓴경우
앞에 이거 써야됨 → com.fitper.domain.


xml이 반영이 이상해서 1분기다리면 풀리는 경우


pom.xml열었는데 다음과같은 에러 계속 나올때
An error has occurred. See error log for more details.
Could not initialize class org.eclipse.m2e.editor.xml.MvnImages


pom.xml 첫줄오류
↓↓↓ 아래내용 <dependencies>형제라인 <biuld>안에 <plugins>안에 추가 (이미 있을경우 잘 합치기) ↓↓↓
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-war-plugin</artifactId>
    <version>3.3.1</version>
</plugin>
<plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.8.1</version>
</plugin>


Consider defining a bean of type 'XXX' in your configuration.
↓↓↓
@Component로 빈으로 쓸 클래스를 등록하지 않음


Parameter 3 of constructor in com.example.testProject.test.Run required a single bean, but 2 were found:
Consider marking one of the beans as @Primary, updating the consumer to accept multiple beans, or using @Qualifier to identify the bean that should be consumed
↓↓↓
@Component가 붙은 자식클래스가 여러개이고 부모클래스는 @Component를 안붙인 상황에서 클래스이름과 호출필드변수명이 다를경우
private final Car kia;
private final Car hyundai;
자식클래스명과 변수명을 똑같이 맞춰 (첫글자는 소문자로 쓰고 두번째글자는 대문자면 안됨) 바꿔 쓰거나

or

@Qualifier("kia")
@Component
public class Kia extends Car{

@Qualifier("kia")
private final Car kia;
이렇게 클래스와 호출필드 각각에 어노테이션을 붙이기


invalid source release: 11
invalid source release: 8
↓↓↓
프로젝트 자바버전이 코드에서 설정한것과 다름. 맞추기


사이트에 보안 연결할 수 없음
localhost에서 잘못된 응답을 전송했습니다.
ERR_SSL_PROTOCOL_ERROR
↓↓↓
로컬인데 https 로 접속한경우. http로 접속하기


Error creating bean with name 'org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping': Invocation of init method failed; nested exception is java.lang.IllegalStateException: Ambiguous mapping. Cannot map 'egovMainController' method 
↓↓↓
컨트롤러에서 같은 url 경로를 중복으로 두 메소드에서 쓴 경우 충돌 발생. 다른거 복사해서 쓸때 경로 바꿔주기


You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '' at line 12
↓↓↓
12라인에는 문제가 없고, 서브쿼리에서 괄호를 안닫았는지 확인. 빨간밑줄이 나타났는지 확인하고 있다면 근처에서 문법오류가 있는것임

-----

★ 400 오류

① 주소창 이상없는지 확인
    url매개변수(쿼리스트링)에 이상한거 잘못넣어 보냈을때

② 크롬 개발자도구 → 새로고침(f5) → Network탭 → Name 탭에서 보낸페이지 이름 클릭 → Headers 탭에서 Form Data 항목 확인
전달된 데이터 이상없는지 확인!!!!!!!!!※※※

③ 요청 타입이 다른경우
ex) json으로 requestBody에 담아 요청해야하는데 다르게 요청했을때


★ 백지상태로 아무것도 안뜨고 아래와 같은 오류날때

① Failed to load resource: net::ERR_INCOMPLETE_CHUNKED_ENCODING
이때는 오류메세지 확인 (주로el 잘못써서 발생)

② GET http://localhost:8080/community?pageNum=21&amount=8&type=&keyword= net::ERR_INCOMPLETE_CHUNKED_ENCODING 200
	a. xml select문에서 해당 컬럼명(콘솔에 오류라고 뜨는)에 AS(앨리어스) 붙여서 다른이름으로 바꿔서 그 이름으로 vo필드속성명, jsp에 쓰기
	b. jsp foreach문에 var에 지정한 변수를 안쓰고 items를 foreach문 안에서 쓴경우
		ex) <c:forEach items="${list}" var="item"> 이렇게 설정해놓고 내부에서 ${list.NAME} 이렇게 쓴경우

③ 아무것도 아무오류도 안뜰때
	HttpServletResponse 파라미터를 쓰면 그렇게 될때가 있는듯


form에서 넘어온 값이 VO클래스 필드의 자료형과 일치하지않는지 확인 (이클립스 콘솔창확인)
HTTP 요청 오류


★ 401(Unauthorized)
상태: 클라이언트가 인증되지 않았거나, 유효한 인증 정보가 부족하여 요청이 거부됨
예시: 사용자가 로그인되지 않은 경우


geadle 리로드 하기


★ 403(Forbidden)
상태: 서버가 해당 요청을 이해했지만, 권한이 없어 요청이 거부됨
예시: 사용자가 권한이 없는 요청을 하는 경우

스프링 시큐리티 관련 오류


★ 404 오류
mybatis xml에서 중복된 태그id가 있는지 확인
있으면 톰캣 실행시 아래처럼뜸
org.apache.catalina.core.StandardContext.startInternal 하나 이상의 리스너들이 시작하지 못했습니다. 상세 내역은 적절한 컨테이너 로그 파일에서 찾을 수 있습니다.
org.apache.catalina.core.StandardContext.startInternal 이전 오류들로 인해 컨텍스트 []의 시작이 실패했습니다.


★ 500 오류

jsp include할 파일들이 같은파일을 또 include해서 변수가 중복되었는지 확인

★★★★★크롬 개발자도구 → 새로고침(f5) → Network탭 → Name 탭에서 보낸페이지 이름 클릭 → Headers 탭에서 Form Data 항목 확인
전달된 데이터 이상없는지 확인

부적합한 열 유형: 1111
1. #{} 으로 받은값이 null일때 발생 → 오류메시지에 무슨컬럼에 null이 들어갔는지 나와있음 "ParameterMapping"으로 검색 (둘이상널이면 첫번째만나옴)
Could not set parameters for mapping: ParameterMapping{property='빠진컬럼명',
	a. xml에 써진 #{}컬럼명과 form으로 전송시키는 데이터 짝 맞는지 먼저 확인
	b. 데이터가 xml로 들어가기전에 Mapper에서 로그찍어보기
2. 쿼리스트링으로 전송받아야할 데이터가 전송되지 않았을때
	a. 컨트롤러에서 전송받아야할 파라미터가, 보내는 페이지에서 (form태그나 링크를 통해) 전송이 안되고있는지 확인
		(히든태그로 보냈으면 submit 꺼놓고 개발자도구에서 hidden태그에 value 잘 들어가는지 먼저 테스트)
	b. textarea[name=]을 input[name=]으로 적었는지 확인
3. el 틀렸을때 발생 ex) ${vo.bno} 를 ${bno} 등으로 잘못썼는지 확인


/WEB-INF/views/board/../includes/header.jsp (행: [1], 열: [2]) 페이지 지시어: 다른 값들을 가지는 'contentType'이
여러 번 나타나는 것은 불허됩니다. (이전 값: [text/html; charset=EUC-KR], 신규 값: [text/html; charset=UTF-8])
↓↓↓
jsp페이지마다 인코딩 설정(<%@ %>← 이거)이 다른경우 발생함 다 똑같이 맞춰야됨
Window → Preferences → Web → Jsp Files → Encoding: ISO 10646/Unicode(UTF-8) 설정 후 새로 jsp페이지 만들었을때
처음에 나오는 인코딩 설정부분(<%@ %>← 이거) 복사해서 이미 만들어진 모든페이지들에 덮기


Request processing failed; nested exception is org.apache.ibatis.binding.BindingException:
Invalid bound statement (not found): com.fitper.mapper.MemberMapper.read_login
↓↓↓
mybatis 바인딩이 제대로 이루어지지 않았을때 발생
1. xml 위쪽에 namespace="com.fitper.mapper.XXX" 의 XXX가 내가 작업하는 Mapper의 경로와 일치하는지 확인
2. 해당 xml파일에 select/insert/delete/update 등의 id가 Mapper의 메소드명과 일치하는지 확인


Request processing failed; nested exception is org.apache.ibatis.binding.BindingException: 
Invalid bound statement (not found): com.fitper.mapper.MemberMapper.getPWQuestion
↓↓↓
xml내 모든 기능이 다 오류가 날때
1. xml파일 이름 체크해보기(대소문자까지 체크)
2. db연결하는부분 올바른지 체크


java.lang.UnsupportedOperationException
↓↓↓
resultType에 list/arraylist를 넣은경우 오류발생
1. 여러 컬럼을 받으면서 VO객체로 받는경우는 resultType="com.fitper.domain.MemberVO" 이처럼 패키지명까지 같이 써주기
2. 여러 컬럼을 받으면서 VO객체를 사용안하는 경우는 resultType="map"
	행이 하나면 DAO에서 받을때 Map<String,String> 로
	행이 여러개면 DAO에서 받을때 List<Map<String,String>>로
3. 단일 컬럼을 받는경우는 resultType="string", DAO에서 받을땐 List로 받기
	행이 하나면 DAO에서 받을때 String 로
	행이 여러개면 DAO에서 받을때 List<String> 로


at org.apache.jasper.compiler.Parser.parse(Parser.java:141)
at org.apache.jasper.compiler.ParserController.doParse(ParserController.java:244)
at org.apache.jasper.compiler.ParserController.parse(ParserController.java:149)
at org.apache.jasper.compiler.Parser.processIncludeDirective(Parser.java:347)
at org.apache.jasper.compiler.Parser.parseIncludeDirective(Parser.java:384)
at org.apache.jasper.compiler.Parser.parseDirective(Parser.java:485)
at org.apache.jasper.compiler.Parser.parseFileDirectives(Parser.java:1802)
↓↓↓
jsp에서 자기 자신을 인클루드 할경우 발생


org.mybatis.spring.MyBatisSystemException: nested exception is
org.apache.ibatis.executor.ExecutorException:
A query was run and no Result Maps were found for the Mapped Statement 'com.fitper.mapper.MemberMapper.autoLogin'.
org.apache.ibatis.executor.ExecutorException: A query was run and no Result Maps were found for the Mapped Statement 
'com.fitper.mapper.MemberMapper.autoLogin'. It's likely that neither a Result Type nor a Result Map was specified.
↓↓↓
해당 XML의 해당 ID에서 resultType/resultMap을 지정하지 않은경우 발생 (select문)


java.sql.SQLIntegrityConstraintViolationException: (conn=78120) Column count doesn't match value count at row 1
↓↓↓
쉼표 중간에 안썼을때 발생


ERROR: org.springframework.web.context.ContextLoader - Context initialization failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'dataSource' defined in ServletContext resource [/WEB-INF/spring/root-context.xml]: Cannot resolve reference to bean 'hikariConfig' while setting constructor argument; nested exception is org.springframework.beans.factory.NoSuchBeanDefinitionException: No bean named 'hikariConfig' available
↓↓↓
root-context.xml에 bean 추가
<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
	<property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
	<property name="jdbcUrl" value="jdbc:log4jdbc:oracle:thin:@localhost:1521:orcl"></property>
	<property name="username" value="health"></property>
	<property name="password" value="codnjs99!"></property>
</bean>


ERROR: com.zaxxer.hikari.pool.HikariPool - HikariPool-1 - Exception during pool initialization.
java.sql.SQLRecoverableException: IO 오류: The Network Adapter could not establish the connection
↓↓↓
도커로 오라클 실행

-----

ajax400오류
1. 컨트롤러←ajax 로 보낼 data가 VO클래스 자료형과 일치하지 않는경우 (빈문자열이거나 null이 넘어왔을때 주로 발생)
2. 컨트롤러←ajax 로 데이터를 보냈으나 파라미터에 @RequestBody를 넣지 않아 못받은경우
3. 컨트롤러←ajax 로 text (or) 폼.serialize() 데이터를 VO객체로 받을때 contentType: "application/json; charset-utf-8", 와 @RequestBody 를 안빼서 발생)
4. 컨트롤러←ajax 로 자바스크립트 객체가 넘어올시 String이외의 걸로 받을경우
	json형 데이터를 Map으로 받으려했다면 json형 객체를 JSON.stringify()로 감싸 문자열로 만들기
	ex) data : JSON:stringify({a:"aaa",b:"bbb"}) = data : {"a":"aaa","b":"bbb"}

ajax404오류
컨트롤러 메소드에 @ResponseBody를 안썼을때
ajax문 url틀렸을때

ajax405오류
get/post ajax↔컨트롤러 안맞을때

ajax415오류
1. 컨트롤러←ajax 로 text (or) 폼.serialize() 데이터를 VO객체로 받을때 파라미터의 @RequestBody 를 안빼서 발생)
2. 컨트롤러←ajax 로 json형 데이터 보낼때 contentType: "application/json; charset-utf-8", 추가안했을경우 발생

ajax500오류 (console창 최대화해서 잘 보기)
컨트롤러에서 ajax로 데이터 전송시 발생
1. VO객체에 담았다면 VO클래스에 getter/setter 있는지 확인
2. 자바객체 ↔ json 간 변환해주는 잭슨 dependency추가
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.10.0.pr3</version>
</dependency>
3. @ResponseBody 안넣었을경우
4. 오라클 오류일 수 있음. 세미콜론을 넣었다던지
5. mybatis로 날짜/시간 데이터를 갖고올경우 반드시 TO_CHAR(JOIN_DATE, 'yyyy-mm-dd hh24:mi:ss') AS JOIN_DATE 이렇게 변환해서 갖고와야함
6. mybatis로 돌려받을 행이 2개이상인데 DAO에서 VO객체를 감싼 List로 안받고 그냥 VO객체로 받았을떄
7. data속성으로 보낸 데이터가 html객체일때. (val() / value 안붙인경우)
8. 자바코드 중간에 문제가 있는 경우

ajax쓸때 밑에 submit() 이게 있는지 꼭 확인하기 (지워야함)★
ajax쓸때는 form태그의 method/action속성과는 상관없음 (ajax속성 이용)

-----

MyBatis update문 실행시 무한로딩 상태
↓↓↓
해당 테이블의 레코드를 다른 곳에서 잡고있어서 발생
예를 들면 SqlDeveloper와 같은 sql툴에서 업데이트(혹은 삭제)를 하고 커밋이나 롤백을 안한 상태에서,
애플리케이션에서 해당 값을 또 업데이트를 한다면 계속 기다리는 상태이다
본인 혹은 다른 자리에서 커밋을 안하고 그 레코드 값을 계속 잡고 있는 경우에 이렇게 된다


xml에서 수정한결과가 반영이 안될때
★★★ Project → clean , 서버 껏다켰다 계속해야함


xml빨간줄 오류
파일 복사붙여넣기 → 원본대조 후 원본삭제 → 이름변경


sql문에는 전혀 이상이 없는데 이상하게 반환결과가 안나올때 (""일때)
먼저 console창에 표로 나오는 sql문실행결과 출력된거 확인. 그래도 결과가 없으면
↓↓↓
sql디벨로퍼로 테스트값 insert한거 커밋 안하고 불러오려고 했을때


org.apache.ibatis.binding.BindingException: Invalid bound statement (not found): com.fitper.mapper.MemberMapper.메소드명
↓↓↓
해당 mapper메소드명과 xml의 실행할 sql문의 id가 정확히 일치하는지 확인하기
or
application.yml / application properties 이 파일에서
mybatis:
  mapper-locations: com/parking/mapper/*.xml
이거 넣었는지 체크


org.apache.ibatis.reflection.ReflectionException: There is no getter for property named 'id' in 'class com.fitper.domain.VO클래스명'
↓↓↓
sql쿼리부분 VO속성명 대소문자 틀림 ( #{ } 이부분 )


org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.binding.BindingException: 
Parameter 'allDay' not found. Available parameters are [arg0, collection, list]]을(를) 발생시켰습니다.
org.apache.ibatis.binding.BindingException: Parameter 'allDay' not found. Available parameters are [arg0, collection, list]
↓↓↓
List로 다중 insert할때 <forEach> 써야한다 (현파일 검색어:ajax로 리스트 넘겨받아 DB에 저장)


org.mybatis.spring.MyBatisSystemException: ested exception is org.apache.ibatis.executor.ExecutorException: 
A query was run and no Result Maps were found for the Mapped Statement 
'com.example.secondproject.repository.CommentMapper.findByContentId'.
↓↓↓
ResultType이나 ResultMap을 안쓰고 VO객체로 반환하려했을때


web.xml 오류아닌데 빨간줄
xsi:schemaLocation="http://java.sun.com~
이부분의 java를 JAVA(대문자)로 변경

-----

컨트롤러에↔ajax 데이터 통신시 오류나면 아래 에러로그 찍어보고 웹 검색 , 이클립스 console창도 유심히 살피기
,error:function(request,status,error){
	console.log("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
}


컨트롤러←ajax 로 데이터 받을때 ""이 출력될때
↓↓↓
파라미터에 @RequestBody 추가


컨트롤러←ajax 로 json형 데이터를 VO로 받으려고 할때 VO객체에 값이 안들어가는 경우
↓↓↓
기본적으로 json형 데이터는 VO에 안들어감. 자바스크립트에서 쿼리스트링형으로 바꿔서 받아야함


컨트롤러←ajax 로 text (or) 폼.serialize() 데이터를 VO로 받을때 VO객체에 값이 안들어갈때(값이 전부 null일때)
↓↓↓
ajax에서 contentType: "application/json; charset-utf-8", 빼야함


컨트롤러→ajax 로 보낸 한글데이터가 ?(물음표)로 깨질때
↓↓↓
@RequestMapping/@GetMapping/@PostMapping 어노테이션에 속성 추가
, produces="application/text; charset=UTF-8"
(Get/PostMapping에 추가할때는 기존 경로앞에 value= 를 붙이기)


컨트롤러→ajax 로 VO, Map을 받을때 console.log(data)찍어봤는데 오류나거나 객체가 아니라 텍스트로 나온다면
↓↓↓
dataType이 엉뚱한걸로 되어있지 않은지 보기 ex) dataType:"text",
→ 설정이 안되있거나(default), "json"으로 되어있어야함. (json형 자바스크립트 객체로 받아야해서 그런것)


컨트롤러→ajax 로 VO객체를 돌려받았을때
분명히 json형 자바스크립트 객체로 잘 받았는데
VO클래스의 필드명으로 data.PW_FIND_A 이런식으로 출력 했는데 undefined가 나올때
↓↓↓
console.log(data)로 찍어서 개발자도구에서 json형 객체 확인후 (확인해보면 대문자 일부가 소문자로 바껴있음)
속성명(컬럼명)을 똑같이 쓰기
(or)
VO객체 말고 Map으로 쓰기 (Map은 컬럼명이랑 똑같이 갖고와짐)


org.springframework.web.HttpMediaTypeNotSupportedException: Content type 'application/x-www-form-urlencoded;charset=UTF-8' not supported]
json객체로 보내고 contentType: "application/json; charset-utf-8" 속성 안넣은경우


org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: 
Cannot deserialize instance of `java.lang.Integer` out of START_OBJECT token; nested exception is 
com.fasterxml.jackson.databind.exc.MismatchedInputException: Cannot deserialize instance of `java.lang.Integer` out of START_OBJECT token
json → map으로 받을때 실수를 <Integer>로받았거나 문자가 아닌 input객체를 받은경우 (value 붙이기)


org.springframework.beans.factory.UnsatisfiedDependencyException
↓↓↓
1. DB 설정이나 쿼리문이 작성되는 xml 파일 점검 : http://bulkywebdeveloper.tistory.com/47
2. Bean에서 에러가 나는 경우 참고 링크 : http://liante0904.tistory.com/113
ex) 비어있는 sql태그가 있을경우 발생
ex) 태그의 id를 안쓴경우

org.apache.ibatis.type.TypeException
↓↓↓
ex) <resultMap>의 type속성을 잘못쓴경우

org.springframework.beans.BeanInstantiationException
↓↓↓
mybatis xml에서 namespace 확인

심각: 클래스 [com.ubintis.framework.SSOListener]의 인스턴스인 리스너에게 contextDestroyed 이벤트를 전송하는 중 예외 발생
java.lang.UnsatisfiedLinkError: no PniccJNI_1.1 in java.library.path
	at java.lang.ClassLoader.loadLibrary(ClassLoader.java:1860)
경고: 웹 애플리케이션 [ROOT]이(가) JDBC 드라이버 [org.mariadb.jdbc.Driver]을(를) 등록했지만, 웹 애플리케이션이 중지될 때, 해당 JDBC 드라이버의 등록을 제거하지 못했습니다. 메모리 누수를 방지하기 위하여, 등록을 강제로 제거했습니다.
↓↓↓
루트컨텍스트를 / 말고 공백(빈문자열)으로 설정


bad SQL grammar []; nested exception is java.sql.SQLSyntaxErrorException: (conn=54369) Incorrect datetime value: '08:00' for column `KTO`.`PUBLIC_PARKING_LOT_DATE_TIME`.`WEEKDAY_OPER_OPEN_HHMM` at row 1] with root cause
↓↓↓
08:00 이라는 데이터를 집어넣으려고 하는데 DB컬럼의 자료형과 안맞을경우


mybatis near~~어쩌구 뜨면
↓↓↓
해당 near 'XXX' 에서 'XXX'의 윗줄이 이상하게 끝났는지 보기
DB툴 에서 테스트후 복붙했는데 세미콜론까지 같이 갖고왔는지부터 확인


java.sql.SQLSyntaxErrorException: (conn=54508) You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')
↓↓↓
insert문에서 마지막 컬럼 ,(쉼표) 를 안뺀경우


org.apache.ibatis.binding.BindingException: Parameter 'basicTime' not found. Available parameters are [collection, list]] with root cause
↓↓↓
list로 받아서 <foreach> 를 써놓고 item.을 안찍은경우 ex) basicTime → item.basicTime 이렇게해야함


myc batis select문 결과들 null 나올때 → resultMap으로 하고 매핑 안돼있는지 확인


.UnsatisfiedDependencyException: Error creating bean with name 'parkingJobConfig' defined in file [/Users/mac/git/visitkorea-support/batch/target/classes/kr/or/visitkorea/batch/job/parking/ParkingJobConfig.class]: Unsatisfied dependency expressed through constructor parameter 7; nested exception is org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'kr.or.visitkorea.batch.repository.mapper.parking.ParkingDetailMapper' available: expected at least 1 bean which qualifies as autowire candidate. Dependency annotations: {}
↓↓↓
맵퍼에 @Mapper 어노테이션 안붙인경우


java.lang.NullPointerException: null
↓↓↓
데이터가 null일수도, null이 아닐수도 있을때 null인 데이터가 들어갔을때 발생.
★★★null이 아닐때만 실행하는 예외처리 필요


org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.reflection.ReflectionException
↓↓↓
xml 컬럼명 오타


Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: 123
↓↓↓
subString으로 짜르려던 중, 123번지의 데이터가 없을떄 발생.
indexOf랑 조합해서 쓸경우 데이터가 없으면 -1이 들어가면서, ~~~: -1 이렇게 -1이 나옴


org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'XXX' defined in file 
.type.TypeException: Could not resolve type alias 'XXX'.  Cause: java.lang.ClassNotFoundException: Cannot find class: XXX
&
org.apache.ibatis.builder.BuilderException: Error parsing Mapper XML. The XML location is 'file [~~~.xml]'. Cause: org.apache.ibatis.builder.BuilderException: Error resolving class. Cause: org.apache.ibatis.type.TypeException: Could not resolve type alias 'XXX'.  Cause: java.lang.ClassNotFoundException: Cannot find class: XXX
↓↓↓
yml설정파일에서 type-aliases-package를 설정 안했거나, 설정한 경로가 틀릴경우 발생
src/main/java 폴더 밑에서부터 dto폴더까지 쓰면 됨
ex)
mybatis:
	type-aliases-package: com.example.testproject.model
예시에서 model 바로 밑에 dto Class가 있어야함


java.sql.SQLInvalidAuthorizationSpecException: Could not connect to address=(host=localhost)(port=3306)(type=master) : 
(conn=34) Access denied for user 'mac'@'172.17.0.1' (using password: YES)
Current charset is UTF-8. If password has been set using other charset, consider using option 'passwordCharacterEncoding'
↓↓↓
application.yml / application.properties 설정파일에서
username & password 속성 key/value 모두 오타 없는지 확인. (db 비밀번호는 도커 이미지 INSPECT에 쓰여있음)


Factory method 'sqlSessionFactory' threw exception; 
nested exception is org.springframework.core.NestedIOException: Failed to parse mapping resource: 
'file [/Users/mac/eclipse-workspace/springboot-test-project/target/classes/mybatis/test/testMapper.xml]';
nested exception is org.apache.ibatis.builder.BuilderException: Error creating document instance.  
Cause: org.xml.sax.SAXParseException; lineNumber: 3; columnNumber: 65; 문서 루트 요소 "mapper"은(는) DOCTYPE 루트 "null"과(와) 일치해야 합니다.
↓↓↓
mapper xml 파일 맨위에 내용 복붙하기
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  


java.lang.IllegalArgumentException: Mapped Statements collection does not contain value for com.example.testProject.mapper.MemberMapper
↓↓↓
mybatis로 불러올 namespace가 없음. 불러오는 부분과 namespace가 불일치한지 확인


Caused by: java.lang.IllegalStateException: Ambiguous mapping. Cannot map 'XXX' method 
↓↓↓
컨트롤러에서 연결할 URL이 중복됨.
@RequestMapping, @GetMapping, @PostMapping name중복 체크

-----

새페이지 만들었는데 jsp에 내용이 있는데 내용도 오류도 아무것도 안나타날때
HttpServletResponse resp 빼기


컨트롤러에서 세션에 넣은 VO의 값을 뺄때
세션은 object형이라 VO클래스로 형변환을 해야 값을 꺼낼수 있음
String id = session.getAttribute("loginInfo").getID();
↓↓↓
String id = ((MemberVO) session.getAttribute("loginInfo")).getID();
	이떄 MemberVO를 먼저 import해야 형변환이 가능해져서 .찍었을때 getID가 나옴...

컨트롤러에서 log.info / System.out.println이 console창에 안찍힐때
1. 브라우저 새로고침 후 커서를 편집창안에 아무데나 놓고 드래그 한번 하면 안나왔던 내용이 보임
	너무 오랫동안 이클립스 켜놓으면 이런 현상이 발생하는듯. 이클립스 한번 껏다키기
2. ajax에서 컨트롤러로 보낼 data가 빈문자열이거나 null일경우 ajax400에러뜨며 실행이 안됨 → 컨트롤러도 당연히 실행 안됨
3. ajax자체가 실행이 안됐을때


VO클래스에 boolean 필드를 넣었는데 getter메소드 쓰려고 VO객체에 .get 쳐도 안보일때
boolean은 게터가 .get이 아니라 .is이다.
wapper클래스인 Boolean은 false일때 null로 나오는데 이때는 .isXXX가 아니라 .getXXX임 하지만 쓸일은 없다


VO객체의 값이 모두 null이면 VO객체자체를 null과 비교했을때도 true가 출력됨


문자열 비교시 == 말고 equals() ★


mybatis sql쿼리실행결과는 log.info()로 일일이 직접 찍어서 확인하지말고 로그 출력되있는거 보기(시간절약) ★★★
select - INFO : jdbc.resultsettable검색후 표 출력된거 보기
insert - 
update - INFO : jdbc.sqlonly검색후 값 유동적으로 들어간거 확인,
	INFO : jdbc.audit검색후 메소드가 행을 몇개 수정했는지 확인 → log.info(메소드) 랑 똑같음


자바클래스 변수를 컨트롤러에서 파라미터로 받으면 계속 똑같은 값으로 고정될때가 있음
서버 껏다켜도 안되고 클린해도 안되고 이럴때는 변수명을 다른이름으로 다 바꿔야함 (나중에 한참 지나면 갑자기 원래 변수도 쓸수있어짐)


List<VO> 를 jsp에서 불러올때 List가 비었는지 확인하려면 null이나 empty가 아닌 아래처럼 빈배열이랑 비교해야함
== '[]'


mybatis로 select했는데 결과가 empty일때 → sql디벨로퍼에서 insert후 commit 했는지 확인


cannot access org.springframework.web.WebApplicationInitializer
↓↓↓
의존성 추가
implementation 'org.springframework.boot:spring-boot-starter-web'


ation-specified bean name 'c2' for bean class
↓↓↓
bean 이름 중복. 중복된 곳으로 가서 새로운 bean이름 지정해주기
@Component
↓
@Component("새로운bean이름")

-----

www.facebook.com/tr/?id=2686987211544937&ev=PageView&dl=http%3A%2F%2Flocalhost%3A8080%2Fmypage%2Ftrss_main.do&rl=http%3A%2F%2Flocalhost%3A8080%2Fmain%2Fmain.do&if=false&ts=1677227272468&sw=2048&sh=1152&v=2.9.97&r=stable&a=tmgoogletagmanager&ec=0&o=30&cs_est=true&it=1677227272348&coo=false&rqm=GET:1          GET https://www.facebook.com/tr/?id=2686987211544937&ev=PageView&dl=http%3A%2F%2Flocalhost%3A8080%2Fmypage%2Ftrss_main.do&rl=http%3A%2F%2Flocalhost%3A8080%2Fmain%2Fmain.do&if=false&ts=1677227272468&sw=2048&sh=1152&v=2.9.97&r=stable&a=tmgoogletagmanager&ec=0&o=30&cs_est=true&it=1677227272348&coo=false&rqm=GET net::ERR_BLOCKED_BY_CLIENT
↓↓↓
확장 프로그램 끄고 해보기
해당 오류는 브라우저에서 요청한 URL에 대해 브라우저 자체에서 차단(block)을 시도한 결과입니다. 이것은 브라우저의 보안 기능 중 하나로, 브라우저는 보안 위험이 있는 리소스를 로드하지 못하도록 차단합니다.

이러한 오류는 보안 정책에 따라 발생할 수 있으며, 일반적으로 브라우저 확장 프로그램이나 방화벽과 같은 보안 솔루션에 의해 발생할 수도 있습니다.

따라서, 해당 오류가 발생하는 원인을 파악하려면 다음과 같은 점을 검토해 볼 수 있습니다.

브라우저 확장 프로그램 및 보안 솔루션을 비활성화하고 다시 시도해 보는 것이 좋습니다.
해당 URL을 호출하는 데 사용된 코드를 자세히 살펴보고, 이 코드에서 보안 위반이 발생하는 부분이 있는지 확인할 수 있습니다.
URL에 대한 서버 측 로그를 검토하여, 요청이 어떤 상황에서 발생하는지 확인할 수 있습니다.
이 문제가 계속해서 발생하는 경우, 브라우저 개발자 도구를 사용하여 오류 메시지를 자세히 살펴보고, 오류가 발생하는 위치와 관련된 정보를 확인할 수 있습니다.

-----

Failed to load resource: net::ERR_NAME_NOT_RESOLVED
↓↓↓
이 오류는 주로 DNS(Domain Name System) 문제로 발생합니다. DNS는 인터넷에서 도메인 이름을 IP 주소로 변환하는 역할을 합니다. 따라서 웹 브라우저가 도메인 이름을 IP 주소로 변환할 때 문제가 발생하면 해당 오류가 발생할 수 있습니다.
오류 메시지 "ERR_NAME_NOT_RESOLVED"는 DNS 서버에서 도메인 이름을 찾을 수 없기 때문에 발생합니다. 이 오류는 다음과 같은 이유로 발생할 수 있습니다.

DNS 서버 문제: DNS 서버가 제대로 작동하지 않을 때 발생할 수 있습니다.

잘못된 도메인 이름: 잘못된 도메인 이름을 입력하면 DNS 서버에서 찾을 수 없으므로 이 오류가 발생할 수 있습니다.

인터넷 연결 문제: 인터넷 연결이 끊어졌거나 불안정한 경우 DNS 서버와의 통신이 실패하여 이 오류가 발생할 수 있습니다.

해결 방법으로는 먼저 인터넷 연결이 정상적으로 작동하는지 확인하고, 도메인 이름을 정확하게 입력했는지 확인합니다. 그리고 DNS 서버가 문제가 있는 경우에는 다른 DNS 서버를 사용해보거나, 컴퓨터를 다시 시작하거나, 네트워크 장비를 재부팅하여 문제를 해결할 수 있습니다.


-----

org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: java.lang.NumberFormatException: For input string: "T"
### Cause: java.lang.NumberFormatException: For input string: "T"

큰따옴표랑 작은따옴표 바꾸기

<if test="certifiedType eq 'T'">
↓
<if test='certifiedType eq "T"'>

-----

### Error querying database.  Cause: org.apache.ibatis.type.TypeException: Could not set parameters for mapping: ParameterMapping{property='snsId', mode=IN, javaType=class java.lang.Object, jdbcType=null, numericScale=null, resultMapId='null', jdbcTypeName='null', expression='null'}. Cause: org.apache.ibatis.type.TypeException: Error setting null for parameter #1 with JdbcType OTHER . Try setting a different JdbcType for this parameter or a different jdbcTypeForNull configuration property. Cause: java.sql.SQLException: Could not set parameter at position 1 (values was <null>)
Query - conn:109152(M)  - "SELECT TP.TNM_ID tnmId
↓↓↓
파라미터로 받은 #{} 이거 주석이 제대로 되어있는지 확인
주석을 #로 하면 안되고 <!-- --> 로 해야함

----------------------------------------------------------------------------------------------------

api요청시 오류

------------------------------

"resultMsg": "INVALID_REQUEST_PARAMETER_ERROR(contentTypeId)"
↓↓↓
잘못된 URL파라미터를 요청했을때 (오류메시지에 나오는 해당하는 url파라미터키값을 빼보기 ex)contentTypeId )


java.util.concurrent.ExecutionException: com.fasterxml.jackson.core.JsonParseException: Unexpected character ('<' (code 60)): expected a valid value
↓↓↓
값을 찍어보면 아래 정보가 나옴
LIMITED_NUMBER_OF_SERVICE_REQUESTS_PER_SECOND_EXCEEDS_ERROR
↓↓↓
짧은 시간 내에 너무 많은 요청을 해서 발생하는 오류


------------------------------

CORS오류

만약 로컬호스트에서 호출했다면 앞에 http:// 붙이기
ex) url: "localhost:3000/sound/dog", → url: "http://localhost:3000/sound/dog",

응답 데이터를 로드할 수 없음 : No data found for resource with given identifier
↓↓↓
다른 프로토콜/Port/호스트/도메인에 ajax요청을 보낼경우 CORS 관련 오류가 남. 3가지가 동일해야 동일 출처로 판단됨
http://store.company.com/dir2/other.html	True	Path만 다르기 때문에
http://store.company.com/dir/inner/another.html	True	Path만 다르기 때문에
https://store.company.com/page.html	False	프로토콜이 다름
http://store.company.com:81/dir/page.html	False	Port가 다름
http://news.company.com/dir/page.html	False	호스트가 다름

jQuery에서는 프로토콜부터 그다음의 "/" 가 나올떄까지 도메인 문자열이 현재 보고있는페이지의 문자열과 상이하면 cross domain 문제을 일으킴
↓↓↓
해결방법
1. jsonp(json with padding)를 통한 해결
2. Proxy 서버를 두는 방법 (iframe 에서 접근할때 이 방법을 써야한다고 함)
	URL 앞에 https://cors-anywhere.herokuapp.com/ 붙이기
	ex) https://cors-anywhere.herokuapp.com/https://원하는URL
3. jquery.ajaxPrefilter() 사용 방법
4. 서버에서 Access-Control-Allow-Origin 헤더를 추가하기
4번 방법이 좋음
컨트롤러에 @CrossOrigin(origins = "*") 추가
or
web.xml에 필터 추가
<filter>
	<filter-name>CorsFilter</filter-name>
	<filter-class>org.apache.catalina.filters.CorsFilter</filter-class>
	<init-param>
		<param-name>cors.allowed.origins</param-name>
		<param-value>*</param-value>
	</init-param>
</filter>
<filter-mapping>
	<filter-name>CorsFilter</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
 
참고: https://velog.io/@jmkim87/%EC%A7%80%EA%B8%8B%EC%A7%80%EA%B8%8B%ED%95%9C-CORS-%ED%8C%8C%ED%97%A4%EC%B3%90%EB%B3%B4%EC%9E%90

서버가 스프링이라면 아래 어노테이션 붙이기
@CrossOrigin

만약 localhost에서 테스트중이라면 요청하는 URL에 http를 붙이기 (ex. http://localhost:~)

CORS 오류 참고: https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F

CORS 오류 경우의수 체험 사이트: https://chuckchoiboi.github.io/cors-tutorial/

------------------------------

Failed to launch 'localhost:5555/testt1?str=zxc' because the scheme does not have a registered handler.
↓↓↓
요청하는 URL에 http를 붙여야함 (ex. http://localhost:~)


java.lang.IllegalStateException: Current request is not of type [org.springframework.web.multipart.MultipartHttpServletRequest]: ServletWebRequest: uri=/filetest;client=0:0:0:0:0:0:0:1
↓↓↓
아래처럼 보내기
var form = $('#f1')[0].files[0];
var formData = new FormData();
formData.append('files', form);
$.ajax({
	data: formData,


org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'dataSourceScriptDatabaseInitializer' defined in class path resource [org/springframework/boot/autoconfigure/sql/init/DataSourceInitializationConfiguration.class]: Unsatisfied dependency expressed through method 'dataSourceScriptDatabaseInitializer' parameter 0; nested exception is org.springframework.beans.factory
↓↓↓
Gradle 창 열고 새로고침 버튼(Reload All Gradle Projects) 클릭


### Error updating database.  Cause: java.lang.IllegalStateException: Type handler was null on parameter mapping for property '__frch_item_0.TP_ID'. It was either not specified and/or could not be found for the javaType (java.util.HashMap) : jdbcType (VARCHAR) combination.
### Cause: java.lang.IllegalStateException: Type handler was null on parameter mapping for property '__frch_item_0.TP_ID'. It was either not specified and/or could not be found for the javaType (java.util.HashMap) : jdbcType (VARCHAR) combination.
↓↓↓
mybatis로 전송되는 파라미터 값 출력해서 이상이 없는지 확인
ex) TP_ID를 String으로 받아야하는데 map으로 잘못받아진 경우
[
  {
    WYBL_NO=6423,
    TTH_ID=fce0aafd-36fd-4c32-a402-00db167fdea9,
    TRS_MN=로젠택배,
    RGTR_ID=5a063c3d-856e-11ec-b08c-0050569dc2b9,
    TP_ID={
      TP_ID=feeee80d-e8b7-4f93-918a-47bfe2f3f176
    },
    IP_ADRES=106.251.247.138,
    TYPE=2
  },
.
.

----------------------------------------------------------------------------------------------------

스프링 동작 원리

1. 클라이언트로부터 요청이 들어오면 제일 먼저 web.xml이 실행된다
2. DispatcherServlet이 <url-pattern>의 형태로 들어오는 요청을 가로채고 servlet-context.xml을 실행시킨다
3. servlet-context.xml에서 <context:component-scan ~~> 에서는 해당 위치의 어노테이션을 읽어들여서 bean으로 등록한다
4. <annotation-driven />은 HandlerMapping & HandlerAdapter의 역할로써
component-scan을 통해서 스캔된 bean중에서 해당 요청과 알맞은 Controller를 찾아 연결시켜준다
5. HandlerMapping을 통하여 요청에 맞는 컨트롤러인 HomeController로 이동하였다
servlet-context.xml의 component-scan에 의해서 HomeController의 @Controller이 읽혀 bean을 등록되었고,
annotation-driven은 @RequestMapping을 읽어들이면서 해당 요청(/)을 처리할 수 있는 Controller를 찾아냈다
그렇게 해서 HomeController가 요청을 받을 수 있게 된것임
요청을 받은 Controller는 적당한 처리를 취한뒤, Model.addAttribute()를 통하여 처리완료된 데이터를 Model에 다시 담고,
"Home" 이라는 이름으로 return한다
6. 다시 servlet-context.xml로 돌아왔다
Model과 Controller를 거쳤으니 이제 View를 거칠 차례이다
다시 돌아온 servlet-context.xml에서는 Controller에서 반환된 "Home"을 가지고 View로 접근할 수 있는 경로를 만든다
이 과정을 거치면 /WEB-INF/views/Home.jsp 라는 경로가 최종적으로 만들어지게 되고
InternalResourceViewResolver를 통하여 이에 맞는 View를 찾는다
7. 이것이 다시 web.xml의 DispatcherServlet으로 넘어가게 되면서 우리가 Home.jsp를 브라우저 상에서 볼 수 있게 된다

----------------------------------------------------------------------------------------------------

모델1 방식

모델 1은 뷰와 로직을 모두 JSP페이지 하나에서 처리하는 구조를 말하며, 모델 1을 구성하는 요소는 다음과 같음

------------------------------

1. JSP

-----

2. 자바빈 혹은 서비스 클래스
JSP페이지 내에 로직 처리를 위한 자바 코드가 출력을 위한 코드와 함께 섞여 삽입됨
브라우저에서 요청이 들어오면 JSP페이지는 자신이 직접 자바빈이나 따로 작성한 서비스 클래스르 이용해 작업을 처리하고,
그 처리한 정보를 클라이언트에 출력함. 과거 가장 많이 사용되었던 아키텍처임

------------------------------

장점
구조가 단순하여 익히기가 쉬움
위와 같은 이유로 숙된된 개발자가 아니더라도 구현이 용이함

단점
출력을 위한 뷰 코드와 로직 처리를 위한 자바 코드가 함께 섞이기 때문에 JSP코드 자체가 복잡해짐
JSP코드에서 백엔드와 프론트엔드가 혼합되기 때문에 분업이 용이하지 않음
코드가 복잡해져 유지보수가 어려움

------------------------------------------------------------

MVC패턴 (모델2)

-----

Model - 서비스 클래스 or 자바빈

비즈니스 로직을 처리하는 모든것들이 모델에 속함.
컨트롤러로부터 특정 로직에 대한 처리 요청(ex: 게시판 글쓰기, 회원가입, 로그인 등)이 들어오면 이를 수행하고 수행 결과를 컨트롤러에 반환함.
필요한 정보는 request 객체나 session객체에 저장하기도 함

-----

View - JSP페이지

클라이언트에 출력되는 화면을 말함.
모델1과 달리 로직 처리를 위한 코드가 내포되어있지 않음. 요청 결과의 출력뿐만 아니라 컨트롤러에 요청을 보내는 용도로도 사용됨.
request객체나 session객체에 저장된 정보를 토대로 화면을 출력함

-----

Controller - 서블릿

MVC패턴(모델2) 모든 흐름제어를 맡음.
브라우저로 요청이 들어오면, 어떤 요청인지를 분석해서 이 요청을 처리하기 위한 모델을 사용해 처리함.
사용한 모델로부터 처리 결과를 받으면, 추가로 처리하거나 가공해야할 정보가 있다면 처리후 request객체나 session객체에 저장하고,
뷰(JSP페이지)를 선택하여 foward나 redirect하여 클라이언트에 출력함

------------------------------

장점
출력을 위한 뷰 코드와 로직 처리를 위한 자바 코드를 분리하기 때문에 JSP 모델1에 비해 코드가 복잡하지 않음
뷰, 로직 처리에 대한 분업이 용이함
기능에 따라 분리되어 있기 때문에 유지보수가 용이함

단점
구조가 복잡하여 습득이 어렵고 작업량이 많음
JAVA에 대한 깊은 이해가 필요함

------------------------------------------------------------

모델1 vs 모델2

모델2가 뒤늦게 나왔다고 무조건 장점만 가지고 있는 것은 아님
모델2는 규모가 큰 프로젝트나 업데이트가 빈번한 프로젝트엔 용이할지 모르나,
규모가 많이 크지 않고 업데이트가 적은 프로젝트일 경우엔 쓸대없이 복잡한 형태로 작업량이 늘어날 뿐임

이 경우에는 간단한 모델1로 개발하는게 더 나을 수도 있음

모델 1과 모델 2는 완전히 다른 장점과 단점을 가지고 있으므로,
하나만 무조건 사용한다기보다는 상황에 따라 적절한 선택이 필요함

------------------------------------------------------------

JSP에서 AJAX를 통해 서비스 클래스에 요청을 보내고 응답을 받아 출력하는 것은 모델2 방식입니다.

모델1 방식은 JSP 페이지 내에 비즈니스 로직과 뷰 로직이 함께 포함되는 구조입니다.
즉, JSP 페이지 자체가 비즈니스 로직을 처리하고 결과를 출력하는 역할을 수행합니다.

반면에 모델2 방식은 비즈니스 로직과 뷰 로직을 분리하여 각각의 역할을 담당하는 구조입니다.

모델2 방식에서는 JSP 페이지가 뷰 로직을 처리하는 역할을 수행하고, 비즈니스 로직은 서블릿이나 컨트롤러 클래스 등 다른 클래스에서 처리합니다.

따라서, JSP 페이지에서 AJAX를 통해 서비스 클래스에 요청을 보내고 응답을 받아 출력하는 것은 모델2 방식의 구조에 해당됩니다

------------------------------------------------------------

MVC패턴에서 모델(Model)은 애플리케이션의 데이터와 비즈니스 로직을 담당하는 부분을 의미함.

모델은 데이터의 생성/수정/삭제 등을 처리하고, 데이터의 상태 변화를 알리는 역할도 함

모델은 일반적으로 DB나 파일시스템과 같은 데이터 저장소와 상호작용하여 데이터를 가져오거나 업데이트함
이러한 작업은 보통 DAO(Data Access Object)나 ORM(Object-Relational Mapping)과 같은 패턴을 사용하여 처리함

모델은 컨트롤러(Controller)와 뷰(View) 사이에서 중개자 역할을 수행하며,
컨트롤러가 모델을 사용하여 데이터를 가져오거나 업데이트하고, 뷰가 모델을 사용해 데이터를 표시함.

이를 통해 데이터와 비즈니스 로직을 분리하고, 애플리케이션을 더육 유연하고 확장성 있는 구조로 만들 수 있음

----------------------------------------------------------------------------------------------------

웹 브라우저 동작 원리 (MVC)

컨트롤러: 클라이언트는 클라이언트로부터 요청을 받는다
뷰 : 최종 페이지를 생성한다
모델 : 최종 페이지에 쓰일 데이터들을 뷰에게 전달한다

<간략한 동작순서 설명>
url 요청 -> 컨트롤러 -> 적절한 처리 -> 뷰를 선택 -> 해당 뷰를 브라우저로 보내서 렌더링

<자세한 동작순서 설명>
1. localhost:8080/hi 로 접속을 하면 controller 가 받는다.
2. 컨트롤러에 정의된 메소드가 실행된다.
3. 그리고 해당 메소드가 반환하는 값을 통해 view 페이지를 보여준다.
4. 해당 view 페이지의 변수를 사용하기 위해서는 model을 거쳐야 한다.
5. 모델로 정의된 메소드 값을 뷰페이지로 출력한다.

----------------------------------------------------------------------------------------------------

스프링 프레임 워크, Spring Framework
- https://spring.io
- Spring 1.0 ~ 5.X.X
- Spring 4.X.X ~ 5.X.X -> 주력

- 스프링 프레임워크는 자바 플랫폼을 위한 "오픈 소스 애플리케이션 프레임워크"이다.
- 경량 프레임워크(EJB에 비해서)
- 프레임워크(틀 -> 작업 환경 제공)
	a. 개발자들의 행동을 정형화(제한 -> 규칙)
	b. 많은 기능을 제공
	c. 장점: 개발자의 실력 차이가 많이 줄어든다. > 팀작업 장점 > 대형화 프로젝트에 적합.
	d. 단점: 틀 때문에 자유도가 낮다.(X)
- 2004년 출시
- 전자 정부 표준 프레임워크: 정부 주도 > 개발 환경 통일 > Spring


STS, Spring Tools Suite
1. 이클립스 + 스프링 관련 라이브러리(*.jar) + 환경 설정 파일 작업
2. 이클립스 + 플러그인(STS)
3. STS(이클립스 + 플러그인(STS))


스프링 프레임워크 구성 요소
1. 의존성 주입 지원(DI, IoC)
2. 관점 지향 프로그래밍 지원(AOP)
3. Spring MVC 지원
4. 레이아웃 지원(Tiles)
5. 데이터베이스 프레임워크 지원
	a. JDBC 연동
	b. Spring JDBC 지원
	c. MyBatis 지원


1. 의존성 주입 지원(DI, IoC)

DI, Dependency Injection
- 스프링 DI
- 디자인 패턴 중 하나
- 프로그래밍에서 구성 요소간 의존 관계가 소스 내부가 아닌 외부 환경에 의해서 정의되게 하는 디자인 패턴

- 패키지 생성 > "com.test.spring.di1"
- 파일 생성 > "Ex01.java"
- 파일 생성 > "SpringDAO.java"

- 패키지 생성 > "com.test.spring.di2"
- 파일 생성 > "Ex02.java"
- 파일 생성 > "SpringDAO.java"

- 패키지 생성 > "com.test.spring.di3"
- 파일 생성 > "Ex03.java"
- 파일 생성 > "SpringDAO.java"
- 파일 생성 > "FileDAO.java"
- 파일 생성 > "DBDAO.java"
- 파일 복사 > "DBUtil.java" 복사


프로젝트 생성하면 필요한 코드와 라이브러리를 다운로드하게 된다
이 라이브러리들은 사용자폴더 내 '.m2'라는 이름의 폴더를 이용한다


프로젝트 실행 시 자주 발생하는 오류
Window → Show View → Other → General → Problems

pom.xml에서 빨간색 경고가 발생하는 경우 - 해당 라이브러리를 다운로드 하지 못하면서 생기는 문제인경우 많음
maven으로 여러 라이브러리들을 받으려고 할 때 가끔 비정상적으로 다운로드가 되는 경우가 생길 수 있음
따라서 이클립스를 종료한 후 '.m2'폴더 내의 모든 내용을 삭제한 후 다시 이클립스를 실행한다

톰캣 실행시 invalid loc header(bad signature) 메시지가 보이면서 정상적으오 실행되지 않는 경우 - 
이문제는 톰캣쪽에 라이브러리가 제대로 처리되지않아서 생기는문제이므로 '.m2'폴더 삭제해도 안된다면
프로젝트 우클릭 → Maven → Update Project

----------------------------------------------------------------------------------------------------

스프링프레임워크에서 제공하고있는 모듈종류
1. spring-core : 스프링의 핵심인 DI(Dependency Injection)와 IoC(Inversion of Control)를 제공
2. spring-aop : AOP구현기능 제공
3. spring-jdbc : 데이터베이스를 쉽게(적은 양의 코드) 다룰 수 있는 기능 제공
4. spring-tx : 스프링에서 제공하는 트랜잭션 관련 기능 제공
5. spring-webmvc : 스프링에서 제공하는 컨트롤러(Controller)와 뷰(View)를 이용한 스프링MVC구현 기능 제공


스프링 컨테이너(IoC)
스프링에서 객체를 생성하고 조립하는 컨테이너(container)로, 컨테이너를 통해 생성된 객체를 빈(bean)이라고 한다

----------------------------------------------------------------------------------------------------

① 스프링 다운
Help → Install New Software... → Add... → http://download.springsource.com/release/TOOLS/update/e4.8/
항목 모두 선택후 계속 설치 → 이클립스 재시작됨
화면 오른쪽 상단에 Perspective아이콘들에 Spring항목 잘 추가됬나 확인

② 스프링 프로젝트 5.x 이상 사용시 tomcat 9 서버 설정
Window → Preferences → Server → Runtime Environment → 기존서버 Remove →
Apache Tomcat v9.0으로 교체

파일은 http://tomcat.apache.org/ 에서 core 다운
다운받은 압축푼 폴더는 감싼폴더 제거후 c나 d에 놓기(지워지면안됨)


③ 프로젝트 생성
New → Other → Spring → Spring Legacy Project → 프조젝트명 지정 → Spring MVC Project → Next → 패키지명 지정 → Finish

그럼 자동으로 뭔가가 설치되는데 완료될때까지 기다리기

(패키지 명명법)
도메인.회사이름.프로그램이름	ex) com.codedragon.goodapp
도메인.회사이름.플랫폼.프로그램이름	ex) com.codedragon.android.goodapp


④ 스프링5에 맞게 자바버전 변경
pom.xml에서 <artifactId>maven-compiler-plugin</artifactId> 밑에 <source>와 <target>을 1.8로 변경
수정 한다음에는 프로젝트 우클릭 → Maven → Update Project... 해주면 좋음

패키지 옆에 버전 잘 바꼈나 확인
JRE system Library [JavaSE-1.6]
↓
JRE system Library [JavaSE-1.8]


⑤ 스프링버전 변경
pom.xml에서 <org.springframework-version> 5.0.7로 변경
3.1.1.RELEASE → 5.0.7.RELEASE

그럼 자동 다운로드된다
프로젝트폴더 → Maven Dependencies패키지에서 버전 잘 바꼈나 확인


⑥ 실행해보기
프로젝트명우클릭 → Run As → Run on Server로 Hello world!가 나오는지 실행해보기


⑦ 자바 개발시 getter/setter, toString(), 생성자 등을 자동으로 생성해주는 '롬복' 라이브러리 이클립스에 설치
https://projectlombok.org/download 에서 jar파일 다운

jar파일이 있는 폴더에서 shift + 우클릭 → 여기에 PowerShell 창 열기(여기서 명령 창 열기) →
java -jar lombok.jar
입력해서 설치 (→이클립스폴더를 자동으로 못찾는경우 Specify location... 으로 직접찾기)

롬복 설치했으면 (다운받은 jar파일은 지워도됨)
이클립스가 설치된 폴더에 lombok.jar가 생기고, eclipse.ini 파일에서 마지막줄에
-javaagent:D:\eclipse\lombok.jar 이런게 추가됬는지 확인

이건 개발도구(이클립스)에서의 롬복을 사용하기위한 세팅 (아직 프로젝트에 적용되지는 않음)

★여기까지 했는데 만약 이클립스가 로고만뜨고 실행이 안된다면↓↓↓
1. 이클립스 바로가기 말고 설치된 경로에서 실행시켜보기
2. 안된다면 eclipse.ini 에서 마지막줄에 있는 -javaagent: 부분에 lombok.jar의 경로가 제대로 되어있는지 확인
3. 안된다면 eclipse.ini 에서
	-vmargs
	을
	-vmargs -javaagent:lombok.jar
	로 변경


⑧ 프로젝트에 롬복 적용시키기
구글에 maven lombok 검색 → 첫번째링크(https://mvnrepository.com/artifact/org.projectlombok/lombok)
다운받은 버전과 같은 버전(⑦에서 확인) 클릭 → Maven탭에있는 소스 복사

↓ 이런거

<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
    <scope>provided</scope>
</dependency>

그다음 이클립스에서 pom.xml로 가서
마지막 </dependency>가 끝나는 부분과 같은 형제라인에 추가(붙여넣기) 후 저장
그럼 자동으로 다운받아짐

확인하는법은 프로젝트폴더 → Maven Dependencies 패키지에서 lombok~~.jar이 있나 확인

----------------------------------------------------------------------------------------------------

이렇게 롬복을 다운받았다면
src/main/java패키지의 HomeController.java파일의
@controller 밑에
@ToString 이라고 쓰고 저장해보기

그럼 자동으로 HomeController.java 파일에 toString()메소드가 만들어진다


★ 만약 만들어지지 않는경우 lombok.jar 다시 다운받아서
프로젝트 우클릭 → Build Path → Configure Build Path... → Add External JARs... 버튼 클릭
→ lombok.jar 파일 선택 → Apply and Close → 이클립스 껏다키기

이래도 안된다?

이클립스 메뉴에서 Help -> Install New Software -> 검색창에서 https://projectlombok.org/p2 검색
검색하면 lombok이 뜸 → lombok이 뜨면 선택하여 설치

----------------------------------------------------------------------------------------------------

만약 ctrl + space 이텔리센스가 잘안된다(여러번눌러야) 된다 하면
Window → Preferences → Java → Editor → Content Assist → Advanced에서
Java Proposals을 위아래 둘다 체크 후 Up버튼으로 맨위로올리기

----------------------------------------------------------------------------------------------------

스프링에서 객체를 관리하게 해주려면 콩(bean)으로 등록을 해야한다
오래 살아남아야 하고, 오래동안 일을 해야하는 애들은 스프링으로 특별관리가 필요한것

스프링의 콩으로 등록하려면 두가지 방법이 있다
1. XML을 설정해서 콩으로 등록하는 방법
2. 어노테이션을 설정해서 콩으로 등록하는 방법

----------------------------------------------------------------------------------------------------

어노테이션으로 등록하는법

프로젝트폴더 → src/main/java패키지 밑에 패키지 하나 만들고 Chef클래스 추가

객체로 만들 Chef클래스 위에
@Component 추가

(그러면 스프링은 객체로 만들어서 관리를 하고있어야 하는구나 라고 판단하게됨)

그리고
@Component 밑에
@Data 도 추가하기(롬복)

그다음 세팅을 해야하는데
프로젝트폴더 → src 패키지 → main → webapp → WEB-INF → spring → root-context.xml

들어가서
하단 Namespaces탭에서 context체크

이후 <context:component-scan base-package="Chef클래스의 부모패키지명"></context:component-scan>

이렇게 설정하면
Chef클래스에서 나온 객체는 스프링에서 관리가 된다
(패키지익스플로러에서 클래스 아이콘에 S자가 붙은것으로 확인 가능하다
s아이콘이 안보이면 프로젝트 우클릭 → Maven → Update Project + 이클립스 껏다켰다 반복해야됨)

이후 그 클래스를 필요로 하는 Restaurant클래스에도
@Component
@ToString
을 붙이고, 필드에

@Autowired
private Chef chef;

이렇게 적어서 Chef가 필요하다고 연결을 시켜준다

----------------------------------------------------------------------------------------------------

테스트 코드 만들기 위한 라이브러리 추가하는법

pom.xml 열고

① junit 버전을 4.12버전으로 바꾸기
<version>4.7</version>
↓↓↓
<version>4.12</version>


② 런타임에서만 동작하게 되어있는 스코프설정을 지우기
log4j 에서 version 뒤에있는 태그 다 지우기

<exclusions>
	<exclusion>
		<groupId>javax.mail</groupId>
		<artifactId>mail</artifactId>
	</exclusion>
	<exclusion>
		<groupId>javax.jms</groupId>
		<artifactId>jms</artifactId>
	</exclusion>
	<exclusion>
		<groupId>com.sun.jdmk</groupId>
		<artifactId>jmxtools</artifactId>
	</exclusion>
	<exclusion>
		<groupId>com.sun.jmx</groupId>
		<artifactId>jmxri</artifactId>
	</exclusion>
</exclusions>
<scope>runtime</scope>

제거


③ 지운거 바로위 log4j 버전을 1.2.17로 변경
<version>1.2.15</version>
↓↓↓
<version>1.2.17</version>


④ 테스트 라이브러리 추가
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-webmvc</artifactId>
	<version>${org.springframework-version}</version>
</dependency>

부분 복사해서 바로뒤에 붙이고

spring-webmvc를 spring-test로 변경



이제 테스트할 패키지를 프로젝트폴더 → src/test/java 패키지에 만들기
패키지안에 테스트 클래스 만들고

클래스 위에
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j
추가 (복붙이후 ctrl + shift + o로 import할것)

그리고
@Autowired
private Restaurant restaurant;
후 improt

@Test 나 @org.junit.Test
public void test(){
	System.out.println(11111); //log4j 동작확인
	log.info(22222); //로그 세팅, 롬복 세팅 확인 (log4j는 프린트할 값 앞에 현재 패키지명.클래스명이 앞에 붙여진다)
	log.info(restaurant);
}

test() (메소드머리부분)에 커서 올려놓고 우클릭 → Run As → JUnit Test 클릭해 테스트해보기

그리고
@Autowired
private Restaurant restaurant;

추가

그리고
@Test
public void test(){
	System.out.println(11111); //log4j 동작확인
	log.info(22222); //로그 세팅, 롬복 세팅 확인
에 log.info(restaurant); 추가

----------------------------------------------------------------------------------------------------

주입 방법은 네가지정도가 있는데 위의 방법은

1. 필드 주입,
2. Setter 주입,
3. 생성자 주입,
4. final 필드 자동주입

중 필드주입이다 (@Autowired 이용)
근데 좋지 않아서 다른걸 사용하는듯?


② Setter주입 으로 하는 방법
@Setter(onMethod_ = {@Autowired})
private Chef chef;


③ 생성자주입으로 하는 방법
필드위에 말고 Restaurant 클래스 위에
@AllArgsConstructor 추가


⑤ 최근에 가장많이 쓰이는 권장하는방법, 5.x에서 쓰임 (final필드 이용)
@RequiredArgsConstructor
public class Restaurant{
	private final Chef chef;
}

----------------------------------------------------------------------------------------------------

톰캣 에러 publishing to tomcat v9.0 server at localhost...' has encountered a problem

1. 작업관리자 → 세부 정보 → javaw.exe 작업끝내기
2. Servers에서 Delete후 다시 추가


5.0.7 Error occured processing XML 'Are you using a JRE with an outdated version of  '. See Error Log for more
details	root-context.xml	/ex00/src/main/webapp/WEB-INF/spring	Unknown	Spring Beans Problem
스프링 익스플로러에서 엑스표시가 뜨고 Problems에서 위와 같은 비슷한 XML오류가 3개 날경우

★이클립스에 설치한 darkest플러그인이 원인인데 jdk8보다 높은 버전을 필요로 해서 jdk11을 ini파일에서 jvm지정하면 된다
방법은 이클립스가 설치된 경로에 들어가서 eclipse.ini열고, -vm D:\Java\jdk-11.0.13\bin\javaw.exe 이렇게 jdk의 javaw.exe경로를 지정하면 됨

----------------------------------------------------------------------------------------------------

@AllArgsConstructor 사용시 원인 모를 에러가 엄청 발생할경우
★스프링 버전이 3버전일때 문제 (pom.xml에서 5.0.7로 수정안했을경우)

----------------------------------------------------------------------------------------------------

jdbc 연동하는법

구글에 maven oracle 검색후 사이트 들어가서 (사용자 많고 버전이 올라간것) 다운
Oracle Database → Oracle Database JDBC → Ojdbc6 → 버전클릭 → 소스 복사

pom.xml에 <dependency>들 마지막에 추가

이후 프로젝트폴더 → Maven Dependencies 에서 추가된거 확인


src/test/java에 패키지 하나 만들고 (org.zerock.persistence)

JDBCTests.java 파일 생성

이후 아래 내용 복붙후

@Log4j
public class JDBCTests {
	
	@Test
	public void testConnection() throws Exception {
		
		Class clz = Class.forName("oracle.jdbc.driver.OracleDriver");
		
		log.info(clz);
		
	}
	
}

우클릭 → Run As → JUnit Test 로 실행 해보기

INFO : org.zerock.persistence.JDBCTests - class oracle.jdbc.driver.OracleDriver
위와같이 뜨면

log.info(clz); 지우고

Connection con = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE","book_ex","book_ex");

추가 (import할때 java.sql.Connection 으로 하기) 해서 DB와 연결시키기

그다음 아래 두줄 추가하고 실행해보기

log.info(con);
		
con.close();


INFO : org.zerock.persistence.JDBCTests - oracle.jdbc.driver.T4CConnection@4c163e3
위와같이 나오면 DB연결에 문제가 없다는뜻

----------------------------------------------------------------------------------------------------

이후 HikariCP(커넥션 풀) 를 빈으로 등록하는데

방법은 구글에 maven hikaricp 치고 들어가서
3.4.5 버전 복사 → dependency부분에 추가

이후 프로젝트폴더→src→main→webapp→WEB-INF→spring→root-context.xml에서

<context:component-scan ~~> 위에

<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
	<property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"></property>
	<property name="jdbcUrl" value="jdbc:oracle:thin:@localhost:1521:XE"></property>
	<property name="username" value="book_ex"></property>
	<property name="password" value="book_ex"></property>
</bean>

위 내용 추가 (내용은 상황에 맞게 수정)

<잘 됬는지 테스트방법>
Spring Explorer탭에서 프로젝트폴더/Beans/root-context.xml/beans에
hikariConfig~~ 있는지 확인


이후

바로 아래에
<bean id="dataSource" class="com.zaxxer.hikariDataSource" destory-method="close">
	<constructor-arg ref="hikariConfig"></constructor-arg>
</bean>

추가하고


src/test/java → 패키지 → 클래스 만들고

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j
추가

	@Autowired
	private DataSource ds;

	@Test
	public void testConnection() {
		
		try(Connection con = ds.getConnection()){
			log.info(con);
			
		} catch (Exception e) {
			e.printStackTrace();
			log.error(e.getMessage());
			
		}
	}

추가


※ 오류1 - org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of
type 'javax.sql.DataSource' available: expected at least 1 bean which qualifies as autowire candidate.
↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
 root-context.xml에서 dataSource를 추가하지않은경우

※ 오류2 - java.net.ConnectException: Connection refused: connect
작업관리자 → 서비스 → OracleServiceXE & OracleXETNSListener 시작하기

----------------------------------------------------------------------------------------------------

mybatis 설정

구글에 maven mybatis 검색후 최신버전 (3.5.6) 복사후
pom.xml에 추가

구글에 maven mybatis spring 도 검색해서 최신버전 (2.0.6) 복사후
pom.xml에 추가

이후
spring-test 부분의 <dependency></dependency> 복사후
바로밑에 두번 붙여넣기 하고
하나는 spring-jdbc로,
하나는 spring-tx로 <artifactId></artifactId>의 내용 변경


root-context.xml에서
<bean id="dataSource" ~~></bean> 밑에

<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource"></property>
</bean>

추가


확인법
src/test/java / org.zerock.persistence에 만들어놓은 DataSourceTests.java에

@Autowired
private SqlSessionFactory sessionFactory;

필드 추가 후

@Test
public void testConnection2() {
	
	try(SqlSession session = sessionFactory.openSession();
		Connection con = session.getConnection()){
		
		log.info(session);
		log.info(con);
		
	} catch (Exception e) {
		e.printStackTrace();
	}

}

메소드도 추가 , 실행

----------------------------------------------------------------------------------------------------

프로젝트폴더에 org.zerock.mapper패키지 생성

생성한 패키지안에 TimeMapper 인터페이스 생성



<어노테이션으로 하는 방법>

public interface TimeMapper {

	// ; 없어야 한다
	@Select("select sysdate from dual")
	String getTime();
	
}

이후 src → main → webapp → WEB-INF → spring → root-context.xml에서 Namespaces 탭에서
mybatis-spring - ~~~~ 체크 후 ctrl + s

그럼 이제 root-context.xml에서 자동완성 기능이 지원된다
<m 까지 입력하고 ctrl+space

base-package명은 src/main/java에 있는 패키지 중에서 지정 (org.zerock.mapper)


테스트하는방법
src/test/java → 패키지(org.zerock.persistence) → 클래스(TimeMapperTests.java) 생성

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j
public class TimeMapperTests {

	@Autowired
	private TimeMapper timeMapper;
	
	@Test
	public void testTime1() {
		
		log.info(timeMapper.getTime());
		
	}
	
}

입력 후 testTime1(){ 에 커서 올려서 실행

----------------------------------------------------------------------------------------------------

<xml로 하는 방법>

src → main → resources 에 org 폴더, 그안에 zerock 폴더, 그안에 mapper 폴더를 하나씩 만든다

mapper 폴더 안에 xml파일을 만든다 인터페이스명과 동일하게(대소문자까지) (TimeMapper.xml)

아래는 내용인데
namespace에는 인터페이스 위치,
id에는 메소드 이름
을 적는다

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.zerock.mapper.TimeMapper">
  <select id="getTime2" resultType="string">
  	select sysdate from dual
  </select>
</mapper>


인터페이스파일에
String getTime2();
도 추가한다


이후 테스트 파일에서
@Test
public void testTime2() {
	log.info(timeMapper.getTime2());	
}

추가 하고 실행

----------------------------------------------------------------------------------------------------

maven log4jdbc-log4j2 검색해서
Log4Jdbc Log4j2 JDBC 4 1 → 1.16 라이브러리 다운

pom.xml에 붙이기

(내용)
<!-- https://mvnrepository.com/artifact/org.bgee.log4jdbc-log4j2/log4jdbc-log4j2-jdbc4.1 -->
<dependency>
    <groupId>org.bgee.log4jdbc-log4j2</groupId>
    <artifactId>log4jdbc-log4j2-jdbc4.1</artifactId>
    <version>1.16</version>
</dependency>


이후
src/main/resources 패키지와
src/test/resources 패키지
두군데에

log4jdbc.log4j2.properties 파일 붙여넣기

(내용은 한줄밖에없음)
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator


이후
<property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"></property>
↓
<property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>

(oracle.jdbc.driver.OracleDriver를 → net.sf.log4jdbc.sql.jdbcapi.DriverSpy로 변경)


이후
<property name="jdbcUrl" value="jdbc:oracle:thin:@localhost:1521:XE"></property>
↓
<property name="jdbcUrl" value="jdbc:log4jdbc:oracle:thin:@localhost:1521:XE"></property>

(사이에 :log4jdbc 추가)


다 했다면 JUnit 탭에서 우클릭 → Run
|------------|
|sysdate   |
|------------|
위처럼 결과가 찍히면 정상

----------------------------------------------------------------------------------------------------
==================================================
----------------------------------------------------------------------------------------------------

스프링 MVC 프로젝트 (part.2)

----------------------------------------------------------------------------------------------------

New → Other → Spring → Spring Legacy Project

Project name : ex01
Templates : Spring MVC Project

→ Next → 

패키지명 : org.zerock.controller

----------------------------------------------------------------------------------------------------

① 1. pom.xml에서 버전 변경 (jdk,스프링)

    ⓐ 3.1.1.RELEASE → 5.2.7.RELEASE

    ⓑ org.apache.maven.plugins검색 후 <source> 와 <target> 두개 1.6 → 1.8

    ⓒ 변경했으면 프로젝트우클릭 → Maven → UpdateProject


② lombok 세팅

maven lombok 검색 후 1.18.16 복사 후 pom.xml에 붙이기


③ pom.xml에 junit 버전 변경

<version> 4.7 → 4.12


④ spring-test 추가

<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-webmvc</artifactId>
	<version>${org.springframework-version}</version>
</dependency>

복사후 바로 밑에 붙인후

<artifactId>spring-webmvc</artifactId>
↓
<artifactId>spring-test</artifactId>

변경


⑤ servlet버전 올리기

maven servlet 검색후 들어가서 뒤로(Home>javax.servlet) 이동 후
↓
첫번째꺼(Java Servlet API) 클릭
↓
4.0.1 클릭

복사 후 아래에 있는 내용을

<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>servlet-api</artifactId>
	<version>2.5</version>
	<scope>provided</scope>
</dependency>

복사해온걸로 변경


⑥ log4j 버전 올리고, <exclusions></exclusions>와 <scope></scope> 제거

<groupId>log4j</groupId> 찾아서

<version>1.2.15</version>
↓
<version>1.2.17</version>

로 변경 후 바로 다음에 있는

<exclusions>
	<exclusion>
		<groupId>javax.mail</groupId>
		<artifactId>mail</artifactId>
	</exclusion>
	<exclusion>
		<groupId>javax.jms</groupId>
		<artifactId>jms</artifactId>
	</exclusion>
	<exclusion>
		<groupId>com.sun.jdmk</groupId>
		<artifactId>jmxtools</artifactId>
	</exclusion>
	<exclusion>
		<groupId>com.sun.jmx</groupId>
		<artifactId>jmxri</artifactId>
	</exclusion>
</exclusions>
<scope>runtime</scope>

위 내용 삭제


⑦ 실행

프로젝트폴더 우클릭 → Run As → Run on Server로 실행해보기

Hello world 뜨는지 확인

다음과 같은 오류가 나오면
Could not publish server configuration for Tomcat v9.0 Server at localhost.

Servers탭 → 서버 더블클릭 → Modules → 관련 프로젝트가 아닌것을 Remove후 저장하고 다시 실행해보기


⑧ Path 변경

Servers탭 → 서버 더블클릭 → Modules → 목록 클릭 → Edit...

/controller
↓
/ (그냥 슬래시만)

로 변경 후 저장

----------------------------------------------------------------------------------------------------

org.zerock.controller패키지에 SampleController.java 클래스 만들고

내용은 다음과 같이 입력후 저장

@Controller
@RequestMapping("/sample/*")
@Log4j
public class Samplecontroller {

	@GetMapping("/ex01")
	public void ex01(SampleDTO dto) {
		log.info(dto);
	}
	
}


org.zerock.domain패키지만들고 그안에 SampleDTO.java 만들고

내용은 다음과 같이 입력후 저장

@Data
public class SampleDTO {

	private String name;
	private int age;
	
}


서버 실행하고

브라우저 주소창에 http://localhost:8080/sample/ex01?name=aaa&age=13
이렇게 들어가 보면
Console에 정보가 찍히는것을 볼 수 있다

----------------------------------------------------------------------------------------------------

VO(Value Object)와 DTO(Data Transfer Object)의 비교

DTO는 메소드 호출 횟수를 줄이기 위해 데이터를 담고 있는 녀석으로,
VO는 값이 같으면 동일 오브젝트라고 볼 수 있는 녀석으로 표현을 하고 있습니다.

쉽게

DTO a = new DTO(1);
DTO b = new DTO(1);

이라고 했을 때 a != b 이지만,

VO a = VO(1);
VO b = VO(1); 이라고 했을때는 a == b라고 정의하는 형태입니다.

+ 추가
VO는 Read Only의 목적이 강하고 데이터 자체도 불변하게 설계하는것이 정석이라고 함
DTO는 주로 데이터 수집의 용도가 좀 더 강하다고 함
웹하면에서 로그인하는 정보를 DTO로 처리하는 방식을 사용한다고 함

----------------------------------------------------------------------------------------------------

배열 DTO 받는법

위에서 만들었던 Samplecontroller.java 클래스에서 아래 메소드 추가 후

@GetMapping("/ex02Bean")
public String ex02Bean(@ModelAttribute("asd") SampleDTOList list) {
	log.info(list);
	
	return "sample/ex02Bean";
	/* 브라우저에서 /ex02Bean URL로 받은걸 sample/ex02Bean으로 보낸다. 이때 URL로 받은 경로와 jsp파일의경로가 같다면 return없이 void로 해도 된다
	return스트링에는 servlet-context.xml의 설정때문에 prefix로 앞경로가 /WEB-INF/views/이 되고 suffix로 인해 뒤에 .jsp가 붙는다 */
}


위에서 만들었던 org.zerock.domain패키지에 SampleDTOList.java 클래스도 추가

내용은 다음과 같이 입력

@Data
public class SampleDTOList {

	private List<SampleDTO> list;
	
	public SampleDTOList() {
		list = new ArrayList<>();
	}
	
}


마지막으로 src > main > webapp > WEB-INF > views 폴더 밑에 sample폴더 생성후
그안에 ex02Bean.jsp 넣고 다음과 같이 이엘(el) 이용해서 저장

<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<h1>${asd}</h1>
</body>
</html>


이제 서버 재시작해주고
브라우저에
http://localhost:8080/sample/ex02Bean?list[0].name=AAA&list[0].age=16를 입력하면 되는데...
이때 중요한점은 대괄호( [ ] ) 가 URL에서 인식이 안되기때문에

URL인코딩을 해서 아래처럼 바꿔야한다
http://localhost:8080/sample/ex02Bean?list%5B0%5D.name=AAA&list%5B0%5D.age=16



그럼 화면에 SampleDTOList가 출력된것을 확인할 수 있다



그리고 위에 메소드를 보면 @ModelAttribute("asd") 라는게 있는데 이건 자기가 원하는 이름으로 바꿔서 쓸 수 있게 해주는것이다
저걸 안쓰고 하려면 jsp에서 el을 쓸때
<h1>${sampleDTOList}</h1>
이렇게 클래스이름의 첫글자를 소문자로 변경후 이용하면 된다



그리고 만약 메소드 리턴타입을 String으로 안하고 void로 해서,
return "sample/ex02Bean";
을 적지 않았을 경우,

클래스 어노텐션의 @RequestMapping("/sample/*") 에 적힌 경로 밑에,
메소드 어노텐션의 @GetMapping("/ex02Bean") 이 경로대로 맞춰진다

이때 uri를 배열로 여러개로도 처리할수있는데 @GetMapping({"/ex02Bean","ex022"})
이렇게 하고 같은 이름의 jsp페이지도 만들어주면
~ex022~ 라는 url도 실행할 수 있다



위에서 리턴타입은 void타입 이 기본이고, String 타입으로 할때는 페이지를 다른곳으로 넘기기 위해서 사용한다
(서블릿에서의 response.sendRedirect("URL") 와 동일하다)

@GetMapping("/re1")
public String re1() {
	log.info("re1....");
	return "redirect:/sample/re2";
}

@GetMapping("/re2")
public void re2() {
	log.info("re2....");
}

----------------------------------------------------------------------------------------------------

파일 업로드

① 라이브러리 추가
maven commons fileupload 검색 후 1.4버전 pom.xml에 복붙후 저장
commons-fileupload-1.4.jar, commons-io-2.2.jar 2개가 추가된것을 확인할 수 있다

서버에 반영하려면 서버restart해야함


② servlet-context.xml 맨 밑에 아래 내용 추가(beans:beans 안에)
<beans:bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
	<beans:property name="defaultEncoding" value="utf-8"></beans:property>
	
	<!-- 1024 * 1024 * 10 bytes 10MB -->
	<beans:property name="maxUploadSize" value="10485760"></beans:property>
	
	<!-- 1024 * 1024 * 2 bytes 2MB -->
	<beans:property name="maxUploadSizePerFile" value="2097152"></beans:property>
	
	<beans:property name="uploadTempDir" value="file:/C:/upload/tmp"></beans:property>
	<beans:property name="maxInMemorySize" value="1048576"></beans:property>
</beans:bean>


③ 클래스에 메소드 추가 & 어노텐션
src/main/java → org.zerock.controller > Samplecontroller.java 에

@GetMapping("/exUpload")
public void exUpload() {
	log.info("exUpload.....");
}

위 내용을 작성한다
이때 로그를 찍어놓는건 문제가 생겼을때 어디까지 실행됬는지 확인하는 용도이다


④ jsp페이지 생성
생성 전 서버 restart 후 브라우저에 localhost:8080/sample/exUpload 까지만 입력하고 들어가면
[/WEB-INF/views/sample/exUpload.jsp]을(를) 찾을 수 없습니다. 라고 jsp의 경로가 나온다 그럼 정상적으로 찾아가는것

아래 내용 삽입
<form action="/sample/exUploadPost" method="post" enctype="multiPart/form-data">
	<input type="file" name="files">
	<input type="file" name="files">
	<input type="submit">
</form>

이때 enctype이 제대로 입력되었는지 확인


⑤ 다시 src/main/java → Samplecontroller.java로 돌아와서 메소드 추가

@PostMapping("/exUploadPost")
public void exUploadPost(ArrayList<MultipartFile> files) {
	files.forEach(file -> {
		log.info(file.getOriginalFilename());
		log.info(file.getSize());
		log.info(file.getContentType());
	});
}


⑥ (서버 재시작후) 파일 업로드해서 제출해보기

파일정보가 찍히면 정상적으로 동작되는것

----------------------------------------------------------------------------------------------------

예외 처리

① org.zerock.exception 패키지 생성 후 안에 CommonExceptionAdvice.java 파일 생성 후 아래 내용 입력

@ControllerAdvice //@Controller와 마찬가지로 스프링의 빈으로 등록하는 어노테이션
@Log4j
public class CommonExceptionAdvice {

	@ExceptionHandler(Exception.class) //파라미터는 처리하고싶은 예외경우를 넣을 수 있음. (Exception은 최상위클래스)
	//예외가 발생하면 → 아래를 통해서 동작되도록
	public String except(Exception ex, Model model) { //View까지 전달되게 하고 싶으면 Model을 기억할것
	//return 타입이 String일경우 return문자열 이름이 jsp파일의 이름이 된다 (error_page.jsp)
		log.error("Exception........." + ex.getMessage());
		model.addAttribute("exception", ex);
		log.error(model);
		
		return "error_page";
	}
}


② 패키지 스캔

패키지를 새로 만들었으니 src → main → webapp → WEB-INF → spring → appServlet → servlet-context.xml에서
패키지를 스캔하기 위해서 <beans:beans> 하위에 <context:component-scan base-package="패키지명" /> 추가


③ src → main → webapp → WEB-INF → spring → views 에서 error_page.jsp 생성 후

	<h1>Exception Page</h1> ← 이런 오류를 나타내는 메시지 추가


④ 브라우저에서 테스트 해보기

주소창에서

localhost:8080/sample/ex01?name=AAA&age=14
원래는 이와같이 정상적으로 데이터를 입력하면 이클립스에서 로그가 찍히는것을 확인할 수 있다 하지만

localhost:8080/sample/ex01?name=AAA&age=BBB
위와같이 자료형을 잘못 받았을경우에는 설정한 예외처리한 페이지로 잘 이동되는것을 확인할 수 있다

----------------------------------------------------------------------------------------------------
==================================================
----------------------------------------------------------------------------------------------------

★ 3-tier(티어) 방식
일반적으로 웹프로젝트는 3-tier(티어) 방식으로 구성한다 (유지보수 용이를 위해)

Presentation Tier(화면 계층)는 화면에 보여주는 기술을 사용하는 영역이다
Servlet/JSP나 스프링 MVC가 담당하는 영역이 된다

Business Tier(서비스 계층)는 순수한 비즈니스 로직을 담고 있는 영역이다
이 영역은 고객이 원하는 요구사항을 반영하는 계층이다
이 영역은 주로 'xxxService와 같은 이름으로 구성하고, 메소드의 이름 역시 사용하는 용어를 그대로 사용하는게 좋다

Persistence Tier(영속 계층, 데이터 계층)는 데이터를 어떤 방식으로 보관하고, 사용하는가에 대한 설계가 들어가는 계층이다
MyBatis, Mybatis-spring 을 이용해서 구성한다 (SQL에 대한 처리를 담당하는 계층이다)


현재 프로젝트의 명명규칙
xxxController : 스프링 MVC에서 동작하는 Controller클래스를 설계할때 사용
xxxService : 비즈니스 영역을 담당하는 인터페이스
xxxServiceImpl : 그 인터페이스를 구현한 클래스
xxxDAO, xxxRepository : DAO(Data-Access-Object)나 Repository(저장소)라는 이름으로 영역을 따로 구성하는것이 보편적이나
이 프로젝트에서는 별도의 DAO를 구성하지 않고 MyBatis의 Mapper인터페이스를 활용한다
VO, DTO : VO와 DTO는 유사한 의미, 이 프로젝트에서는 VO라는 이름 사용

패키지 명명규칙
org.zerock.config : 프로젝트와 관련된 설정 클래스들의 보관 패키지
org.zerock.controller : 스프링 MVC의 Controller들의 보관 패키지
org.zerock.service : 스프링의 Service인터페이스와 구현 클래스 패키지
org.zerock.domain : VO/DTO클래스들의 패키지
org.zerock.persistence : MyBatis Mapper인터페이스 패키지
org.zerock.exception : 웹 관련 예외처리 패키지
org.zerock.aop : 스프링의 AOP관련 패키지
org.zerock.security : 스프링의 Security관련 패키지
org.zerock.util : 각종 유틸리티클래스 관련 패키지

----------------------------------------------------------------------------------------------------

게시판 (part.3)

----------------------------------------------------------------------------------------------------

New → Other → Spring → Spring Legacy Project

Project name : ex02
Templates : Spring MVC Project

→ Next → 

패키지명 : org.zerock.controller

----------------------------------------------------------------------------------------------------

① pom.xml에서 버전 변경 (jdk,스프링)

    ⓐ 3.1.1.RELEASE → 5.2.7.RELEASE

    ⓑ org.apache.maven.plugins검색 후 <source> 와 <target> 두개 1.6 → 1.8

    ⓒ 변경했으면 프로젝트우클릭 → Maven → UpdateProject


② pom.xml에서 라이브러리 추가 (DB세팅)

    ⓐ spring-webmvc검색 후 해당 부모<dependency>...<dependency> 복사 후 바로 밑에 x3번 붙이기 (총4개)

    ⓑ 복사한 <artifactId>태그에 있는 spring-□ 의 □를 각각 jdbc, tx, test 로 수정하기

    ⓒ 그밑에 아래 내용 추가 (jdbc드라이버)
<!-- https://mvnrepository.com/artifact/com.oracle.database.jdbc/ojdbc6 -->
<dependency>
	<groupId>com.oracle.database.jdbc</groupId>
	<artifactId>ojdbc6</artifactId>
	<version>11.2.0.4</version>
</dependency>


③ Hello world! 뜨는지 실행해보기

프로젝트폴더 우클릭 → Run As → Run On Server → Tomcat v9.0 Server at localhost 선택 → Next → Finish


④ 데이터베이스 커넥션 관련 세팅 (junit버전, Servlet버전, HikariCP, Mybatis-spring, Log4jdbc, dataSource)

    ⓐ pom.xml에서 junit검색후 4.7 → 4.12

    ⓑ pom.xml에서 <groupId>log4j</groupId> 검색 후 1.2.15 → 1.2.17

    ⓒ pom.xml에서 servlet-api검색후 아래 내용으로 변경
<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>javax.servlet-api</artifactId>
	<version>4.0.1</version>
	<scope>provided</scope>
</dependency>


    ⓓ pom.xml에서 다음 내용 dependency있는 쪽에 추가
<!-- https://mvnrepository.com/artifact/com.zaxxer/HikariCP -->
<dependency>
	<groupId>com.zaxxer</groupId>
	<artifactId>HikariCP</artifactId>
	<version>3.4.5</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
	<version>3.5.6</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis-spring</artifactId>
	<version>2.0.6</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.bgee.log4jdbc-log4j2/log4jdbc-log4j2-jdbc4.1 -->
<dependency>
	<groupId>org.bgee.log4jdbc-log4j2</groupId>
	<artifactId>log4jdbc-log4j2-jdbc4.1</artifactId>
	<version>1.16</version>
</dependency>


    ⓔ src/main/resources 패키지와 src/test/resources 패키지 '두 패키지' 에 log4jdbc.log4j2.properties 파일 만들기
(우클릭new → Other → General → File → Next → File name: log4jdbc.log4j2.properties → Finish)

내용은 다음과 같다(한줄밖에없음)
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator


    ⓕ src → main → webapp → WEB-INF → spring → root-context.xml 에서 beans 태그 안쪽 마지막에 다음 내용 붙이기 (DB연결)
<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
	<property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
	<property name="jdbcUrl" value="jdbc:log4jdbc:oracle:thin:@localhost:1521:XE"></property>
	<property name="username" value="book_ex"></property>
	<property name="password" value="book_ex"></property>
</bean>

<bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource" destroy-method="close">
	<constructor-arg ref="hikariConfig"></constructor-arg>
</bean>

    ⓖ 프로젝트우클릭 → Run As → Run on Server 실행시 헬로월드 및 Console창에 다음과 같은 내용이 무수히 찍힐경우 정상임을 확인 가능
INFO : org.springframework.web.context.ContextLoader - Root WebApplicationContext: initialization started
INFO : com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Starting...
INFO : jdbc.connection - 1. Connection opened
.
.
.

    ★ 중간마다 실행시 오류가 날경우 '저장' 및 '업데이트 프로젝트'(프로젝트우클릭 → Maven → Update Project) 해보기

    ⓗ root-context.xml 에서 다음 내용 추가
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource"></property>
</bean>

    ⓘ root-context.xml 파일 열고  하단 탭에서 Namespaces클릭하면 체크박스들 나옴, 거기서 mybatis-spring 체크후 저장하기


⑤ lombok 세팅

    ⓐ pom.xml에서 dependency부분에 아래 내용 추가
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.18.16</version>
	<scope>provided</scope>
</dependency>

    ⓑ 프로젝트우클릭 → Run As → Run on Server 실행해보기 (오류안나면정상)


⑥ mybatis가 정상적으로 동작하는지 테스트하기

    ⓐ src → main → webapp → WEB-INF → spring → root-context.xml 에서
        <beans></beans>태그 내부 최하단에 <m 까지 치고 ctrl + space 치면 <mybatis-spring:scan base-package=""/> 이렇게 나오는데
        base-package="" 에 org.zerock.mapper 넣기


    ⓑ 프로젝트 우클릭 → 패키지 생성 (name:org.zerock.mapper)

    ⓒ 생성한 패키지우클릭 → 인터페이스 생성 (name:TimeMapper)

    ⓓ 생성한 인터페이스의 내용으로 다음내용 추가 (ctrl+shift+o로 import 하기)
	@Select("select sysdate from dual")
	String getTime();

 
    ⓔ src/test/java 에서 패키지 생성 (name:org.zerock.mapper)

    ⓕ 생성한 패키지 우클릭 → 클래스 생성 (name:TimeMapperTests)

    ⓖ 생성한 클래스의 public class~ 위에 다음 어노테이션 추가
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j

    ⓗ 생성한 클래스에 private TimeMapper timeMapper; 멤버변수넣고 다음 어노테이션 추가
@Autowired

    ⓘ 생성한 클래스에 public void testGetTime(){ 메소드 넣고 다음 어노테이션 추가
        }
@Test

    ⓙ 생성한 클래스에 testGetTime 메소드 안에 log.info("testGetTime...................."); 로그 추가 (어디까지 테스트 됬는지 확인 위함)

    ⓚ 저장 후 testGetTime 메소드명 클릭 후 우클릭 → Run As → JUnit Test
        로그 찍혔는지 확인

    ⓛ log.info 찍은 바로 밑에 log.info(timeMapper.getTime()); 도 추가

    ⓜ 저장 후 testGetTime 메소드명 클릭 후 우클릭 → Run As → JUnit Test
select sysdate from dual
실행되는 sql문과

|----------------------|
|sysdate               |
|----------------------|
|2021-10-23 04:30:56.0 |
|----------------------|
실행결과 찍혔는지 확인

----------------------------------------------------------------------------------------------------

기본 세팅 끝

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

① 테이블 생성하기

    ⓐ SQL Developer의 "book_ex"계정에서 시퀀스/테이블/데이터를 생성한다 (insert는 5번정도 해준다)

create sequence seq_board;

create table tbl_board(
    bno number(10,0),
    title varchar2(200) not null,
    content varchar2(2000) not null,
    writer varchar2(50) not null,
    regdate date default sysdate,
    updatedate date default sysdate
);

alter table tbl_board add constraint pk_board primary key (bno);

insert into tbl_board(bno,title,content,writer) values(seq_board.nextVal,'테스트 제목','테스트 내용','user00');

select * from tbl_board order by bno desc;

commit;

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

영속,데이터 계층 (SQL 처리)


현재 아래 3-tier(티어) 방식 중

Presentation(표현)계층	↔	Business(서비스)계층	↔	Persistence(영속,데이터)계층	↔	DB
Spring MVC			Spring Core			MyBatis

에서 영속,데이터 계층을 구현할 예정

----------------------------------------------------------------------------------------------------

② VO 만들기

    ⓐ org.zerock.domain 패키지 생성

    ⓑ 생성한 패키지 안에 BoardVO 클래스 생성

    ⓒ 클래스 멤버변수로 DB의 컬럼과 똑같이 생성 이때 자료형 첫글자로 대문자 사용 (0으로 초기화되는것을 방지)
private Long bno;
private String title, content, writer;
private Date regdate, updatedate;

    ⓓ Date클래스 Import는 util의 Date로 하기

    ⓔ public class~ 위에 @Data 추가 (게터/세터 만드는용)

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

세팅 및 Select 리스트 구현

----------------------------------------------------------------------------------------------------

① Mapper인터페이스 만들기

    ⓐ org.zerock.mapper 패키지에서 인터페이스 추가(name:BoardMapper)

    ⓑ 다음 메소드헤더 추가
List<BoardVO> getList();

    ⓒ List클래스 Import는 util의 List로 하기


② XML 만들기 ★★★ (mapper만들때는 인터페이스 + 어노텐션 or XML로 만든다)

    ⓐ src/main/resources 우클릭 → New → Other → General → Folder 로 폴더 만들기 (name:org)

    ⓑ 그 밑에 또 폴더 만들기 (name:zerock)

    ⓒ 그 밑에 또 폴더 만들기 (name:mapper)

    ⓓ 폴더 우클릭 → New → Other → XML → XML File 로 인터페이스 이름과 동일한 XML파일 만들기 (name:BoardMapper)

    ⓔ xml파일의 내용은 다음과 같이 수정
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

    ⓕ xml파일에 내용 추가 (namespace:인터페이스명과 동일하게, id:인터페이스의 메소드명과 동일하게)
    그리고 SQL Developer에서 복사해온 select문을 넣으면 되는데 이때 세미콜론(;)은 반드시 빼야된다
    resultType은 DB로부터 select로 받은 결과를 담는 자료형(객체)이다 (대소문자 주의, hashmap으로 할경우 컬럼명,값 이렇게 가져와진다)

<mapper namespace="org.zerock.mapper.BoardMapper" resultType="org.zerock.domain.BoardVO">

	<select id="getList">
	
	select * from tbl_board order by bno desc
	
	</select>
	
</mapper>


③ 테스트 클래스 만들기

    ⓐ 먼저 스프링이 문제없이 동작하는지 중간 확인하기
src/test/java → org.zerock.mapper → TimeMapperTests.java에서 메소드 JUnit으로 실행해보기

    ⓑ 잘 동작한다면 src/test/java → org.zerock.mapper에 클래스 만들기(name:BoardMapperTests)

    ⓒ 생성한 클래스의 public class~ 위에 다음 어노테이션 추가
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j

    ⓓ 생성한 클래스에 멤버변수 + 어노테이션 추가
@Autowired
private BoardMapper boardMapper;

    ⓕ 메소드 + 어노테이션 추가
@Test
public void testGetList(){
	log.info("--------------------------------------------------");
	boardMapper.getList();
}

    ⓖ 메소드 클릭 후 우클릭 → Run As → JUnit Test로 실행해서 select문의 결과가 잘 나왔는지 확인

만약 오류가 났다면 JUnit 탭을 열어서 Failure Trace창에 에러메세지 확인하기
(JUnit탭이 없다면 Window → Show View → Other → Java → Junit)

org.apache.ibatis.binding.BindingException: Invalid bound statement (not found): org.zerock.mapper.BoardMapper.getList
위와같이 Invalid bound statement (not found) 라고 나올경우 xml에서 select태그 id명 틀린것

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

단일 Select

----------------------------------------------------------------------------------------------------

인터페이스.java 코드
BoardVO read(Long bno);

XML 코드
<select id="read" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where bno = #{bno}
</select>

테스트.java 코드
@Test
public void testRead() {
	BoardVO vo = boardMapper.read(5L); //5번 정보를 가져오겠다는뜻
	log.info(vo);
}

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

Insert

----------------------------------------------------------------------------------------------------

① 만들어놓은 인터페이스에 메소드헤더 추가

    ⓐ src/main/java → org.zerock.mapper → BoardMapper.java 에서 메소드 추가
int insert(BoardVO vo);


② 만들어놓은 XML에서 태그 추가

    ⓐ src/main/resources → org → zerock → mapper → BoardMapper.xml 에서 태그 추가 후
SQL Developer에서 복사해온 내용 삽입 (반드시 세미콜론 없애기)
<insert id="insert">
	insert into tbl_board(bno,title,content,writer) values(seq_board.nextVal,'테스트 제목','테스트 내용','user00')
</insert>

    ⓑ 이후 값들을 #{} 로 바꿔주기 #은 ?(치환)로 바뀌고(prepareStatement) 내부적으로 get메소드가 호출된다
insert into tbl_board(bno,title,content,writer) values(seq_board.nextVal,#{title},#{content},#{writer})


② 테스트 하기

    ⓐ org.zerock.mapper → BoardMapperTests.java 에서 메소드 + 어노테이션 추가
@Test
public void testInsert(){
	BoardVO vo = new BoardVO();
	vo.setTitle("title 테스트");
	vo.setContent("content 테스트");
	vo.setWriter("writer 테스트");

	boardMapper.insert(vo);
	log.info("--------------------");
	log.info("after insert" + vo.getBno()); //이때 결과는 Null임, 나오게 하려면 아래의 insertSelectKey를 이용해야함
}

    ⓑ 메소드 클릭 후 우클릭 → Run As → JUnit Test
Connection.prepareStatement(insert into tbl_board(bno,title,content,writer) ~~
등이 뜨면서 insert가 되는걸 볼 수 있음

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

Insert + 들어간 시퀀스값 알아내기

----------------------------------------------------------------------------------------------------

인터페이스.java 코드
int insertSelectKey(BoardVO vo);

XML 코드
<insert id="insertSelectKey">
	<selectKey order="BEFORE" keyProperty="bno" resultType="long"> //long타입으로 bno에다 select한 결과를 저장하는걸 가장먼저 실행
		select seq_board.nextVal from dual
	</selectKey>
	insert into tbl_board(bno,title,content,writer) values(#{bno},#{title},#{content},#{writer})
</insert> 

테스트.java 코드
@Test
public void testInsertSelectKey() {
	BoardVO vo = new BoardVO();
	vo.setTitle("AAAtitle 테스트");
	vo.setContent("AAcontent 테스트");
	vo.setWriter("Awriter 테스트");

	boardMapper.insertSelectKey(vo);
	log.info("--------------------");
	log.info("after insert selectkey : " + vo.getBno()); //시퀀스.nextval from dual을 먼저 작업후 그걸 다시
VO에 담아서 insert하기때문에 들어간 번호를 알 수 있다
}


시퀀스를 먼저 그냥 호출 하고, 이후 그 값을 VO에 담아 insert에 사용하는 방식이다 (성능은 감소)
게시판에서 'N'번글이 등록되었습니다. 이런거 할때는 selectKey를 사용

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

Update

----------------------------------------------------------------------------------------------------

인터페이스.java 코드
int update(BoardVO vo);

XML 코드
<update id="update">
	update tbl_board set title = #{title},
	content = #{content},
	writer = #{writer},
	updatedate = sysdate
	where bno = #{bno}
</update>

테스트.java 코드
@Test
public void testUpdate() {
	BoardVO vo = new BoardVO();
	vo.setBno(2L); //2번을 수정
	vo.setTitle("Updated Title");
	vo.setContent("Updated Content");
	vo.setWriter("user00");
	
	log.info("count : " + boardMapper.update(vo));
}

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

Delete

----------------------------------------------------------------------------------------------------

인터페이스.java 코드
int delete(Long bno);

XML 코드
<delete id="delete">
	delete from tbl_board where bno = #{bno}
</delete>

테스트.java 코드
@Test
public void testDelete() {
	int count = boardMapper.delete(1L);
	
	log.info("count : " + count);
}

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

비즈니스 계층(고객의 요구사항을 반영하는 계층)


현재 아래 3-tier(티어) 방식 중

Presentation(표현)계층	↔	Business(서비스)계층	↔	Persistence(영속,데이터)계층	↔	DB
Spring MVC			Spring Core			MyBatis

에서 비즈니스 계층을 구현할 예정

----------------------------------------------------------------------------------------------------

① 패키지 생성

    ⓐ 프로젝트 우클릭 → 패키지 생성 (name:org.zerock.service)


② 인터페이스 생성

    ⓐ 생성한 패키지 안에 인터페이스 생성 (name:BoardService)

    ⓑ 내용 추가 (메소드명은 고객과 의사소통하는 용어를 사용)
List<BoardVO> getList();
BoardVO get(Long bno);
int register(BoardVO vo);
Long registerKey(BoardVO vo); //return값으로 번호를 돌려줄 예정
int modify(BoardVO vo);
int remove(Long bno);


③ 인터페이스를 구현할 클래스 생성 ★★★ (service만들때는 인터페이스 + 구현클래스로 만든다)

    ⓐ 생성한 패키지 안에 클래스 생성 (name:BoardServiceImpl)

    ⓑ 내용 추가(인터페이스구현) + 어노테이션
@Log4j
@Service
@AllArgsConstructor
@ToString
public class BoardServiceImpl implements BoardService{

	@Autowired
	private BoardMapper mapper;

	@Override
	public List<BoardVO> getList() {
		return mapper.getList();
	}

	@Override
	public BoardVO get(Long bno) {
		return mapper.read(bno);
	}
	
	@Override
	public int register(BoardVO vo) {
		return mapper.insert(vo);
	}

	@Override
	public Long registerKey(BoardVO vo) {
		mapper.insertSelectKey(vo);
		return vo.getBno();
	}

	@Override
	public int modify(BoardVO vo) {
		return mapper.update(vo);
	}

	@Override
	public int remove(Long bno) {
		return mapper.delete(bno);
	}
}

이때 @Service는 빈으로 등록하기 위한것으로써(@Controller과 동일) 아래 XML스캔설정까지 완료하면 익스플로러창에 S아이콘이 붙는다


④ XML에서 스캔설정

    ⓐ root-context.xml에서(servlet-context.xml은 웹과 관련된것들만 설정됨) namespaces탭에서 context 체크

    ⓑ <beans></beans>태그 안쪽에 내용 추가
<c 라고 치고 두번째꺼, base-package=""안에 패키지명 입력 ↓↓↓
<context:component-scan base-package="org.zerock.service"></context:component-scan>


⑤ 테스트 패키지 & 클래스 생성

    ⓐ src/test/java 우클릭 → 테스트 패키지 생성 (name:org.zerock.service)

    ⓑ 패키지 안에 클래스 생성(name:BoardServiceTests)

    ⓒ 어노테이션 추가
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j

    ⓓ 멤버변수 + 주입어노테이션 추가
@Autowired
private BoardService service;

    ⓔ 메소드(객체출력하는) + 테스트어노테이션 추가
@Test
public void testPrint() {
	log.info(service);
}

    ⓕ 메소드클릭 후 우클릭 → JUnit실행
org.zerock.service.BoardServiceTests - BoardServiceImpl(mapper=org.apache.ibatis.binding.MapperProxy@27e32fe4)
위와같이 인스턴스(mapper~) 이렇게 나옴

    ⓖ register()등 클래스에 만들어놓은 메소드도 추가해서 테스트 해보기

@Test
public void testGetList() {
	service.getList().forEach(board -> {
		log.info(board);
	});
}

@Test
public void testRegister() {
	BoardVO vo = new BoardVO();
	vo.setTitle("테스트제목1");
	vo.setContent("테스트내용1");
	vo.setWriter("테스트작성자1");
	
	service.register(vo);
}

@Test
public void testRegisterKey() {
	BoardVO vo = new BoardVO();
	vo.setTitle("테스트제목2");
	vo.setContent("테스트내용2");
	vo.setWriter("테스트작성자2");
	
	log.info(service.registerKey(vo));
}

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

표현 계층(화면에 보여주는 계층)


현재 아래 3-tier(티어) 방식 중

Presentation(표현)계층	↔	Business(서비스)계층	↔	Persistence(영속,데이터)계층	↔	DB
Spring MVC			Spring Core			MyBatis

에서 표현 계층을 구현할 예정

----------------------------------------------------------------------------------------------------

웹 계층에서 가장 먼저 설계하는것은 URI의 설계이다
MVC의 목적이라는게 로직이랑 화면을 분리하는건데 로직이라는게 간단하게 표현하면 URL이다
URL처리는 컨트롤러가 담당하고 화면은 나중에 변경을 쉽게 하겠다 이런게 유지보수 측면
아래는 그 설계한 표다

Task(일)		URL		Method	Parameter		From		URL이동

전체 목록		/board/list		GET
등록 처리		/board/register	POST	모든항목		입력화면 필요	이동
조회		/board/read	GET	bno=123
삭제 처리		/board/modify	POST	bno		입력화면 필요	이동
수정 처리		/board/remove	POST	모든항목		입력화면 필요	이동

목록 페이지
등록 입력/처리 페이지
조회 페이지
수정/삭제 페이지

----------------------------------------------------------------------------------------------------

세팅 및 select리스트

① 컨트롤러 추가

    ⓐ src/main/java → org.zerock.controller 에서 클래스 생성(name:BoardController)

    ⓑ 어노테이션, Get메소드 등 내용 추가
@Log4j
@RequestMapping("/board")
@AllArgsConstructor
@Controller
public class BoardController {

	@GetMapping("/list")
	public void list() {
		
		log.info("list.............");
		
	}
	
}


② 컨트롤러테스트 추가

    ⓐ src/test/java → org.zerock.controller 에서 클래스 생성(name:BoardControllerTests)

    ⓑ 클래스 어노테이션 추가
@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration({
  "file:src/main/webapp/WEB-INF/spring/root-context.xml",
  "file:src/main/webapp/WEB-INF/spring/appServlet/servlet-context.xml"})
@Log4j

    ⓒ 내용 추가 before임폴트는 junit으로
@Setter(onMethod_ = {@Autowired} )
private WebApplicationContext ctx;

private MockMvc mockMvc;

@Before
public void setup() {
	this.mockMvc = MockMvcBuilders.webAppContextSetup(ctx).build();
}

@Test
public void testList() throws Exception {
	log.info(
		mockMvc.perform(
		MockMvcRequestBuilders.get("/board/list"))
		.andReturn()
		.getModelAndView()
		.getModelMap()
	);
}

    ⓓ testList클릭 → 우클릭 후 실행
실행시 아래를 포함한 로그들이 찍힘
INFO : org.zerock.controller.BoardController - list.............
INFO : org.zerock.controller.BoardControllerTests - {}


③ 웹에서 실행하기

    ⓐ 서버 시작후 웹주소창에 localhost:board/list쳐서 테스트시 페이지가 안나올것인데,
Server탭 → Modules탭 → 선택 → Edit → /controller 를 / 로 바꾸고, 저장후, 서버 재실행

    ⓑ 웹페이지 새로고침시 jsp를 찾을 수 없다고 나오면 정상, 콘솔창에 list..........가 찍히면 정상


④ jsp인코딩 설정

    ⓐ jsp페이지를 만들기 전에 먼저 jsp 인코딩 설정을 해야함
Window → Preferences → Web → JSP Files → Encoding : "Korean, EUC-KR" → "ISO 10646/Unicode(UTF-8)" 로 바꿔놓기


⑤ jsp파일 만들기

    ⓐ WEB-INF → views에 board폴더 추가 후 그 안에 list.jsp만들기, 내용 아무거나 추가해서 테스트한번더 해보기


⑥ 컨트롤러에서 Model객체에 리스트 담아서 Get방식으로 jsp에다가 주기 (form이 들어간경우만 Post방식)

    ⓐ src/main/java → org.zerock.controller → BoardController.java에서 list메소드에 내용추가
private final BoardService service; //mapper(dao)를 바로 참조하면 안되고 항상 service계층을 거쳐야 함

@GetMapping("/list")
public void list(Model model) {
	log.info("list.............");
	
	model.addAttribute("list", service.getList());
}


⑦ jsp 테스트

    ⓐ jsp에서 EL로 list 출력하기
${list}

    ⓑ Servers탭에서 재시작(Restart the server) 후 웹페이지 새로고침해 결과 확인하기

----------------------------------------------------------------------------------------------------

단일 select

① 컨트롤러에서 Get메소드 추가

    ⓐ src/main/java → org.zerock.controller → BoardController.java 에서 내용 추가
@GetMapping("/get")
public void get(@RequestParam(name = "asd") Long bno, Model model) {
/*Long bno는 bno라는 인수를 받아서, jsp페이지에 model로 전달한다
RequestParam사용할경우 bno라는 변수를 asd란 이름으로 바꿔서 사용할수있다*/
	
	log.info("/get");
	model.addAttribute("vo",service.get(bno));
	
}


② 테스트 추가

    ⓑ src/test/java → org.zerock.controller → BoardControllerTests.java 에서 내용 추가
@Test
public void testGet() throws Exception {
	log.info(
		mockMvc.perform(MockMvcRequestBuilders
			.get("/board/get")
			.param("bno", "2")
		)
		.andReturn()
		.getModelAndView()
		.getModelMap()
	);
}

----------------------------------------------------------------------------------------------------

등록/수정/삭제를 할때 참고

등록/수정/삭제의 최종 처리는 POST방식을 이용한다 이때

1. 별도의 결과 페이지를 만들어서 보여주는 방식
  - 회원가입 완료 페이지 등

2. 목록 페이지로 이동하는 방식
  - 목록 페이지에서 알림메시지를 보여주는 방식

이렇게 두가지가 있는데 이때

'POST방식' and '2번'을 쓴다면 'redirect:/...'를 고려할것


★Model vs RedirectAttributes (addAttribute/addFlashAttribute)

Model은 (url파라미터등으로 받은) 데이터를 처리해서 동일한(어노텐션에 입력한) jsp페이지에 보내줄때 이용하고,
RedirectAttributes는 다른 페이지에 데이터를 보내줄때 이용한다

addAttribute는 get방식처럼 URL로 값을 전달한다. 이때문에 받은값을 다른곳에 또 보낼때 추가코드없이 재활용할 수 있다
addFlashAttribute는 post방식처럼 보이지않게 값을 전달한다. ★el을 사용할 수 있다.

RedirectAttributes.addAttribute/addFlashAttribute 를 쓸때는
보낼 페이지를 리턴하는문이 있어야 한다
return "redirect:/board/list";

addAttribute / addFlashAttribute 차이
addAttribute : 쿼리스트링(url파라미터) 으로 전달함 el 못씀
addFlashAttribute : 눈에 안보이게 전달함 model과 마찬가지로 el ( ${ } ) 로 꺼내쓸수 있음
공통점 : 컨트롤러 req.getAttribute으로 바로는 못읽음. 무조건 jsp를 거쳐야함. 컨트롤러에서 get컨트롤러로 바로 데이터를 보내려면 세션 쓰기

----------------------------------------------------------------------------------------------------

insert

① 컨트롤러에서 Post메소드 추가

    ⓐ src/main/java → org.zerock.controller → BoardController.java 에서 내용 추가
@PostMapping("/register")
public String register(BoardVO vo, RedirectAttributes rttr) {
//다른페이지로 이동위해 void가아닌 String으로 return, 보낼데이터 담을 RedirectAttributes 파라미터 추가
	
	log.info("vo" + vo);
	
	Long bno = service.registerKey(vo);
	
	log.info("BNO: " + bno);
	
	rttr.addFlashAttribute("result", bno);
/*다른페이지로 생성된 데이터의 키값 보내기 위해 addFlashAttribute / addFlashAttribute 로 저장
데이터를 전달할때는 경로를 다 전송하는 addAttribute와, 한번만 사용가능한 addFlashAttribute가 있다*/
	
	return "redirect:/board/list";  //다른페이지로 이동위해 "redirect:보낼전체경로" 리턴
	
}


② src/test/java → org.zerock.controller → BoardControllerTests.java 에서 테스트

    ⓐ 내용 추가
@Test
public void testRegister() throws Exception {
	log.info(
		mockMvc.perform(
		MockMvcRequestBuilders.post("/board/list")
			.param("title", "Test 테스트")
			.param("content", "content 테스트")
			.param("writer", "writer 테스트")
		)
		.andReturn()
		.getModelAndView()
		.getModelMap()
	);
}

----------------------------------------------------------------------------------------------------

update

① 컨트롤러에서 Post메소드 추가

    ⓐ src/main/java → org.zerock.controller → BoardController.java 에서 내용추가
@PostMapping("/modify")
public String modify(BoardVO vo, RedirectAttributes rttr) {
	
	int result = service.modify(vo);
	
	if (result == 1) {
		rttr.addFlashAttribute("result", "success");
	}
	
	return "redirect:board/list";
	
}


② src/test/java → org.zerock.controller → BoardControllerTests.java 에서 테스트

    ⓐ 내용추가
@Test
public void testModify() throws Exception {
	log.info(
		mockMvc.perform(
		MockMvcRequestBuilders.post("/board/modify")
			.param("bno", "96")
			.param("title", "modify 테스트")
			.param("content", "content 테스트")
			.param("writer", "writer 테스트")
		)
		.andReturn()
		.getModelAndView()
		.getModelMap()
	);
}

----------------------------------------------------------------------------------------------------

delete

① 컨트롤러에서 Post메소드 추가

    ⓐ src/main/java → org.zerock.controller → BoardController.java 에서 내용추가
@PostMapping("/remove")
public String remove(Long bno, RedirectAttributes rttr) {
	
	int result = service.remove(bno);
	
	if (result == 1) {
		rttr.addFlashAttribute("result", "success");
	}
	
	return "redirect:board/list";
	
}


② src/test/java → org.zerock.controller → BoardControllerTests.java 에서 테스트

    ⓐ 내용추가
@Test
public void testRemove() throws Exception {
	log.info(
		mockMvc.perform(
		MockMvcRequestBuilders.post("/board/remove")
			.param("bno", "95")
		)
		.andReturn()
		.getModelAndView()
		.getModelMap()
	);
}

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

화면 페이지 만들기

jsp페이지를 만들기 전에 먼저 jsp 인코딩 설정을 해야함
Window → Preferences → Web → JSP Files → Encoding : "Korean, EUC-KR" → "ISO 10646/Unicode(UTF-8)" 로 바꿔놓기

----------------------------------------------------------------------------------------------------

부트스트랩 연결후 부트스트랩 베이스로 list.jsp 구성하기

① 부트스트랩.zip 다운 후 src/main/webapp/resources에 폴더째로 복붙


② pages폴더에 들어있는 견본.html 테스트

    ⓐ 서버 재시작 후 resources부터 테스트할 html경로 입력 (http://localhost:8080/resources/pages/forms.html)

    ⓑ css등 안깨지는거 확인


③ list.jsp에다 옮기기

    ⓐ src/main/java/webapp/WEB-INF/views/board/list.jsp 들어가서 갖다쓸 파일(tables.html) 붙여넣기 <%@ %>(jsp 설정부분)은 지우지말것

    ⓑ 크롬개발자도구 → Network탭 → 새로고침 → css등 경로 확인

    ⓒ 다시 이클립스 와서 ctrl + f 로 경로 일괄변경 ../ → /resources/

WEB-INF안의 파일들은 자바에서 이동시키거나 참조해야함 (html, 직접 주소창으로는 접근불가)


④ header.jsp/footer.jsp 생성, include로 빼기

    ⓐ src/main/webapp/WEB-INF/views 에 폴더 생성 (name:includes)

    ⓐ 만든 includes폴더에 jsp파일 생성 (name:header) , (name:footer)

    ⓑ  <!DOCTYPE html> 부터 <div id="page-wrapper"> 까지 header.jsp로 빼기

    ⓒ list.jsp에서 <%@include file="../includes/header.jsp"%> (상대경로)


⑤ 제이쿼리 버전변경

    ⓐ 제이쿼리 cdn 검색후 code.jquery.com들어가서 minified 복사

    ⓑ footer의 <script 부분에 기존제이쿼리 변경


⑥ 제이쿼리로 디자인 수정 (반응형모바일에서 상단메뉴 내려와있는거 올리기)

    ⓐ footer에서 $(document).ready(function(){ 에 아래내용추가

$(".sidebar-nav")
	.attr("class","sidebar-nav navbar-collapse collapse")
	.attr("aria-expended","false")
	.attr("style","height:1px");


⑦ list.jsp 수정

    ⓐ table에 있는 id="dataTables-example" 제거 (페이징처리 제거)

----------------------------------------------------------------------------------------------------

등록 페이지 만들기

① 컨트롤러에서 Get메소드 추가

    ⓐ src/main/java → org.zerock.controller → BoardController.java 에서 Get방식으로 메소드 추가
(이때 먼저 만들어놓은 @postMapping으로 되어있는 register는 register.jsp페이지에서 submit을 할경우 실행되는 메소드이다,
@getMapping으로 만들어놓은것은 단순히 register.jsp라는 페이지를 띄우기 위함이다,
postMapping만 있고 getMapping이 없으면 405에러가 뜬다)
@GetMapping("/register")
public void registerGET() {
	
}


② jsp 페이지 추가

    ⓐ src/main/webapp/WEB-INF/views/board 에서 register.jsp 추가

    ⓑ 내용은 list.jsp 복붙후 pannel-boay내의 내용만 변경 (table을 form으로) 이때 부트스트랩 견본 (forms.html) 활용
<form method="post" action="/board/register">
/* action을 안넣으면 브라우저의 url로 설정됨. 이름을 register_ok 이렇게 하려면
1. action="/board/register_ok" (form태그 action속성 바꾸고)
2. controller.java에서 @PostMapping("/register")을 @PostMapping("/register_ok") 이렇게 하면 된다 */
	<div class="form-group">
		<label>Title</label>
		<input class="form-control" name="title">
	</div>
	<div class="form-group">
		<label>Content</label>
		<textarea class="form-control" rows="3" name="content"></textarea>
	</div>
	<div class="form-group">
		<label>Writer</label>
		<input class="form-control" name="writer">
	</div>
	
	<button type="submit" class="btn btn-default">Submit Button</button>
	<button type="reset" class="btn btn-default">Reset Button</button>
</form>


③ 값을 입력후 테스트 해보기

    ⓐ 값 모두 넣은후 테스트 해보기 (한글도 항상 테스트 해야함)

----------------------------------------------------------------------------------------------------

한글 안깨지게 설정하기

한글 깨지는 원인 → ★네트워크를 탈때

1. 브라우저에서 서버로 데이터를 보낼때 깨지는 경우
2. 브라우저가 보낸 데이터를 서버에서 받을때 깨지는 경우
3. 서버에서 받아서 DB에 넣을때
4. jsp인코딩설정 안했을때. Window→Preferences→encoding검색→JSP Files→Encoding: ISO 10646/Unicode(UTF-8)로 변경해놔야
jsp페이지 새로 만들때 아래에 있는 내용이 자동으로 추가되는데
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" language="java" %>
jsp페이지마다 첫줄에 위와같은 인코딩설정을 해야함. 없다면 추가하고, 있다면 utf-8로 되어있는지 확인


먼저 브라우저에서 서버로 한글이 전송될때 깨졌을때
브라우저가 보낼때 깨졌는지 서버가 받을때 깨졌는지 확인해야함

확인하는 방법은
src/main/java → org.zerock.controller → BoardController.java에서
@PostMapping("/register") (데이터를 받는 처리를 하는(+결과페이지를 만들 수 있는) 메소드)에 넣어놓은
로그 ↓
log.info("vo: " + vo);
이걸 확인해보면 알 수 있다. 이때 깨져있다면 브라우저에서 보낼때깨짐 or 서버에서 받을때깨짐 둘중 하나다


① 확인하는법

이제 크롬에서 개발자도구를 열고, 등록페이지에서 form을 입력후 submit버튼을 누른후 Network탭에 들어가서
3rd-party requests 체크 해제하고 register를 클릭해보기

그러면
Request Method: POST → GET/POST 어느방식으로 전달됬는지,
Location: /board/list → 이동된 경로는 어디인지 등등 나오는데

맨 밑에 보면 Form Data 항목이 있고 VO 키-값이 있는데

ⓐ 아래값만 한글값만 안나온다면 jsp 인코딩 설정이 잘못된것
title: test
content: (unable to decode value)

ⓑ 한글값이 한글로 제대로 나온다면 아래 xml설정으로 ↓↓↓


② xml 설정

    ⓐ src → main → webapp → WEB-INF → web.xml 에서 아래 내용 <web-app></web-app> 안에 추가
<filter>
	<filter-name>encoding</filter-name>
	<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
	<init-param>
		<param-name>encoding</param-name>
		<param-value>UTF-8</param-value>
	</init-param>
</filter>

<filter-mapping>
	<filter-name>encoding</filter-name>
	<servlet-name>appServlet</servlet-name>
</filter-mapping>

----------------------------------------------------------------------------------------------------

등록 페이지 만들기 계속...

① RedirectAttributes객체에 담아서 "redirect:~" 로 보낸 페이지에서 데이터를 받았는지 확인

    ⓐ 개발자도구 키고 폼 submit 후 Network탭에서, @PostMapping했던 페이지(register)를 클릭,
Response Handers부분에 Location에서 보낼 경로(/board/list) 확인

    ⓑ 그 경로의 jsp페이지(/board/list.jsp)에 들어가서 스크립트 & EL 사용해서 테스트, 이때 개발자도구가 아닌 소스 보기(Ctrl+U)에서 확인가능
<script>
	$(window).load(function(){
		result = "<c:out value='${result}'/>";
	});
</script>


② 모달창 처리(사용자가 글등록을 해서 jsp가 데이터를 받은 상태일 경우에만)
→ result변수로 받은 데이터(=글번호)가 ""이나 null이 아닌 숫자일경우 사용자에게 "N번 글이 등록되었다고 출력

    ⓐ 부트스트랩 modal 복사해서 페이지 맨 마지막, <script> 위에 추가 후 id 하나 주기
<div class="modal" id="myModal" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Modal title</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <p>Modal body text goes here.</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-primary">Save changes</button>
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>

    ⓑ 스크립트 추가 - RedirectAttributes로 돌려받은 뭔가가 있을때만 모달창이 뜨게
$(window).on("load",function(){
	var result = "<c:out value='${result}'/>";
	checkModal(result);
});

function checkModal(result){
	if (parseInt(result) > 0) {
		$(".modal-body").html(result + "번 게시글이 등록되었습니다.")
		
		$("#myModal").modal("show"); //그냥 $("요소").show()가 아니고 $("요소").modal("show") 임 조심
	}
}

    ⓒ 글을 올려서 리스트로 돌아가졌을 때랑 그냥 리스트로 이동했을때랑 차이를 테스트 해보기


③ 등록버튼 만들기

    ⓐ 적당한 위치에 버튼 추가
                        <div class="panel-heading" style="display:flex;justify-content:space-between;align-items:center">
                            DataTables Advanced Tables
                            <button type="submit" id="btnReg" class="btn btn-primary">글쓰기</button>
                        </div>

    ⓑ 버튼눌렀을때 페이지 이동 스크립트 추가
$("#btnReg").click(function(){
	location.href = "register";
});

----------------------------------------------------------------------------------------------------

글정보페이지 만들기

① 아까 만들어둔 get컨트롤러에 연결할 jsp페이지 추가

    ⓐ /../views/board에 get.jsp 추가, 내용은 register.jsp 복사

    ⓑ 제목수정

    ⓒ form태그 제거

    ⓓ value속성에 (url파라미터(쿼리스트링)로 받은 bno로 조회해서 vo객체로 model에 담아 돌려받아) el로
<c:out value='${vo.bno}'/>
<c:out value='${vo.title}'/>
<c:out value='${vo.content}'/> 이런식으로 넣기 이때 <c:out 넣는 이유는 XSS보안 때문임

    ⓔ textarea는 태그사이에 (<textarea>여기에</textarea>)

    ⓕ readonly속성 추가

    ⓖ 브라우저에서 http://localhost:8080/board/get?bno=236 이런식으로 파라미터 붙여서 테스트 해보기

    ⓗ 줄바꿈이 제대로 되나 테스트, 안되면 아래내용 컨트롤러에 잘 추가 (servlet&jsp팁 참조)
vo.setContent(vo.getContent().replace("\r\n","<br>"));


② 리스트에서 제목 클릭시 해당 글페이지로 이동되게

    ⓐ list.jsp에서 제목에 a태그 추가
<td><a href="/board/get?bno=${vo.bno}">${vo.title}</a></td>


③ 히스토리를 클리어 안시켜서 발생하는 오류(앞으로갔다 뒤로갔다 하면 정보가 남아서 모달, 다운로드 등 다시되는것) 제거
(오류 테스트 방법 : list페이지에서 등록버튼 눌러서 글하나 올리고 → 모달창 닫고 → 글 하나 들어갔다가 → 뒤로가기x1 or x3)

    ⓐ list.jsp에서 $(window).load(function(){ 에서, checkModal(result); '다음 줄'에 내용추가
history.replaceState({}, null, null);

    ⓑ checkModal 처음에 if 리턴문 추가
if(history.state){
	return;
}

    ⓒ 오류가 사라졌는지 테스트 해보기

----------------------------------------------------------------------------------------------------

수정&삭제 페이지 만들기

① 컨트롤러 수정

    ⓐ 기존의 'get'메소드의 어노텐션에 "/get"을 {}로 감싸고, /modify를 추가
@GetMapping({"/get", "/modify"})

이러면 /get으로 들어갔을때 get.jsp페이지가 뜨고, /modify로 들어갔을때 modify.jsp페이지가 뜬다


② jsp페이지 생성

    ⓐ /../views/board에 jsp파일추가(name:modify.jsp), 내용은 get.jsp 복사

    ⓑ 감싸는 <form> 태그 추가 (속성은 넣지 말기)

    ⓒ 버튼들 만들고 data- 사용자속성 추가
<button class="btn btn-default" data-oper="modify">Modify</button>
<button class="btn btn-danger" data-oper="remove">Remove</button>
<button class="btn btn-info" data-oper="list">List</button>

    ⓓ 스크립트 추가 (form태그 내 button태그 기본submit 되는거 막고, 버튼에 따라 다르게 처리)
$(".btn").click(function(e){
	e.preventDefault();
	
	var operation = $(this).data("oper");
	
	console.log(operation);
	
	if(operation === "list"){
		location.href = "/board/list";
	}else if(operation === "modify"){
		$("form").attr("method","POST")
		.attr("action","/board/modify")
		.submit();
	}else if(operation === "remove"){
		$("form").attr("method","POST")
		.attr("action","/board/remove")
		.submit();
	}
	
})

    ⓔ 버튼 클릭시 크롬 콘솔에 속성값이 잘 찍히는지 테스트

    ⓕ data- 사용자속성 별로 기능 다르게 하기 (list.jsp)
↓↓↓↓↓
function checkModal(result, type){
↑↑↑↑↑
	if(history.state){
		return;
	}
	if (parseInt(result) > 0) {
		$(".modal-body").html(result + "번 게시글이 등록되었습니다.")
↓↓↓↓↓
		if (type === "r") {
			$(".modal-body").html(result + "번 게시글이 삭제되었습니다.")
		}else if (type === "m") {
			$(".modal-body").html(result + "번 게시글이 수정되었습니다.")
		}
↑↑↑↑↑
	
		$("#myModal").modal("show");
	}
}

    ⓖ 컨트롤러 수정
@PostMapping("/modify")
public String modify(BoardVO vo, RedirectAttributes rttr) {
	
	int result = service.modify(vo);
	
	if (result == 1) {
		rttr.addFlashAttribute("result", vo.getBno());
		rttr.addFlashAttribute("type", "m");
	}
	
	return "redirect:/board/list";
	
}

@PostMapping("/remove")
public String remove(Long bno, RedirectAttributes rttr) {
	
	int result = service.remove(bno);
	
	if (result == 1) {
		rttr.addFlashAttribute("result", bno);
		rttr.addFlashAttribute("type", "r");
	}
	
	return "redirect:/board/list";
	
}

    ⓗ 글정보(get.jsp)페이지에서 글목록(list.jsp)이나 수정&삭제(modify.jsp) 페이지로 이동되게 링크걸기
<a href="/board/list" class="btn btn-default">목록</a>
<a href="/board/modify?bno=${vo.bno}" class="btn btn-default">수정/삭제</a>

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

페이징 처리

----------------------------------------------------------------------------------------------------

하기 전 먼저 대량의 데이터에서 SQL의 쿼리의 성능개선을 위해 명시적으로 힌트 를 통해 실행계획을 변경하는것을 알아야한다
힌트를 쓰는 방법은 /*+ */ 이렇게 주석안에 "+"를 붙여서 힌트절을 실행시킨다

select * from tbl_board order by bno desc; //일반 order by로 처리한 방법(데이터가 많아지면 느려진다)
		| | 거의 비슷하다
select /*+ FULL(tbl_board) */ * from tbl_board; //전체 데이터를 먼저 다 가져온다음 그다음에 정렬을 한다 (느림)


이걸 아래처럼 인덱스를 이용해서 출력한다 (pk_board 순서대로 출력한다)

select /*+ INDEX_DESC(tbl_board pk_board) */ * from tbl_board where bno > 0;
		↑					      ↑
	select와 * 사이에 /*+ INDEX(테이블명 인덱스명) */	   RANGE SCAN

rownum : 도착하는 순위를 메기는것
테이블에서 가장 먼저 엑세스가 된것들이 rownum이 1번이 되는것이다

때문에
select /*+ INDEX_DESC(tbl_board pk_board) */ rownum,bno,title from tbl_board where bno > 0;

이렇게 INDEX_DESC를 하면 뒤에번호가 제일먼저 엑세스되서 제일먼저 rownum이 1이 됨


★★★힌트 쓸때 주의사항 ★★★
select * from
	(
		select /*+ INDEX_DESC(M PK_MEMBER_TL) */ rownum rn, m.*
		from MEMBER_TL M
		where
		MEMBER_SQ > 0 and rownum > 0 and rownum <= 1 * 10
	)
where rn > (1 - 1) * 10;
위처럼 from MEMBER_TL M 이렇게 테이블에 별칭을 붙이려면, 힌트부분에도 테이블명(MEMBER_TL)이 아닌 별칭명(M)으로 바꿔야 힌트가 동작한다.


이제 페이징을 위한 조건을 걸어야하는데

select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer from tbl_board 
where bno > 0 and rownum > 0 and rownum <= 10;
이건 되지만 

select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer from tbl_board 
where bno > 0 and rownum > 0 and rownum >10 and rownum <=20
이건 안되므로

인라인뷰+엘리어스 를 사용해서 처리한다 ↓↓↓
select * from (select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer from tbl_board 
where bno > 0 and rownum > 0 and rownum <= 20) where rn > 10;

이걸 변수(페이지번호)로 처리하기 위해
select * from (select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer from tbl_board 
where bno > 0 and rownum > 0 and rownum <= 10 * 2) where rn > (2-1) * 10;

----------------------------------------------------------------------------------------------------

① (페이지번호, 페이지당 출력될 항목갯수) 변수 처리를 하기위해 DTO를 만든다

    ⓐ src/main/java → org.zerock.domain 에서 자바파일 생성 (name:Criteria)

    ⓑ 필드 및 생성자 및 어노테이션 추가
@Getter
@Setter
@ToString
public class Criteria {
	
	private int pageNum; //현재 내가보고있는 페이지번호
	private int amount; //페이지당 출력될 항목 개수

	public Criteria() {
		this(1,10);
	}

	public Criteria(int pageNum, int amount) {
		super();
		this.pageNum = pageNum;
		this.amount = amount;
	}
	
}


② 인터페이스 추가

    ⓐ src/main/java → org.zerock.mapper → BoardMapper.java 인터페이스에서 메소드머리 추가
List<BoardVO> getListWithPaging(Criteria cri); //객체 받아서 리스트<VO>로 반환


③ XML 추가

    ⓐ src/main/resources → org → zerock → mapper → BoardMapper.xml XML에서 같은 이름으로 기능추가 (★sql문에 세미콜론 빼야함)
<select id="getListWithPaging" resultType="org.zerock.domain.BoardVO">
select * from
(
	select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
	from tbl_board 
	where bno > 0 and rownum > 0 and rownum <= 10 * 2
) 
where rn > (2 - 1) * 10
</select>

    ⓑ 이때 부등호(>, <) 때문에 빨간밑줄이 생기는데, sql문을
<![CDATA[
]]>
로 묶으면 해결된다. 부등호를 &lt, &gt로 쓰는 방법도 있음


④ 테스트 추가 / 실행

    ⓐ src/test/java → org.zerock.mapper → BoardMapperTests.java에서 테스트 추가
@Test
public void testPaging() {
	
	//1페이지, 10개
	Criteria cri = new Criteria();
	
	List<BoardVO> list = boardMapper.getListWithPaging(cri);
	
	list.forEach(b -> log.info(b));
	
	
}

    ⓑ JUnit 실행해서 결과 확인
2페이지가 나오는것을 확인

    ⓒ 다시 XML로 가서 #{XXX} = (getXXX)를 이용해 상수를, Criteria 변수를 불러오도록 바꿔준다
<select id="getListWithPaging" resultType="org.zerock.domain.BoardVO">
<![CDATA[
select * from
(
	select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
	from tbl_board 
	where bno > 0 and rownum > 0 and rownum <= #{pageNum} * #{amount}
) 
where rn > (#{pageNum} - 1) * #{amount}
]]>
</select>


⑤ 서비스 계층 인터페이스 추가

    ⓐ src/main/java → org.zerock.service → BoardService.java에서 리스트를 가져오는 메소드에 파라미터만 추가해서 오버로딩
List<BoardVO> getList(Criteria cri);

    ⓑ src/main/java → org.zerock.service → BoardServiceImpl.java에서 mapper(멤버변수).메소드 로 인터페이스 구현
@Override
public List<BoardVO> getList(Criteria cri) {
	return mapper.getListWithPaging(cri);
}


⑥ 컨트롤러 계층

    ⓐ src/main/java → org.zerock.controller.java에서 원래 있던 'list'메소드를 복사해서 밑에 붙이고 원래건 주석
@GetMapping("/list")
public void list(Model model) {
	log.info("list.............");
	
	model.addAttribute("list", service.getList());
}

    ⓑ 내용 변경
@GetMapping("/list")
public void list(Criteria cri, Model model) {
	log.info("------------------------");
	log.info(cri);
	log.info("list.............");
	
	model.addAttribute("list", service.getList(cri));
}

    ⓒ 브라우저에서 테스트 http://localhost:8080/board/list
1페이지만 나오나 확인, 글도 하나 올려보기

----------------------------------------------------------------------------------------------------

페이징 처리 PageDTO추가구현(현재페이지,데이터개수,이전,다음)

설명
전체개수(int total) : 게시글의 총 개수
페이지당개수(Criteria객체→amount) : 한 페이지당 글 개수
페이지번호(Criteria객체→getPageNum) : 현재 내가보고있는 페이지번호
시작번호(startPage) : 끝 페이지번호로 구한 시작 페이지번호
임시끝번호(int endPage) : 시작번호를 구하기 위한 임시용 끝 페이지번호
최종끝번호(int realEnd) : 시작페이지,글개수를 구한 최종 끝번호
이전(boolean prev) : 이전 페이지가 있는지 여부
다음(boolean next) : 다음 페이지가 있는지 여부

임시끝번호 = (int)Math.ceil(현재페이지번호/10.0) * 10;
시작번호 = 끝번호 - 9;
최종끝번호 = (int)(Math.ceil(전체개수 * 1.0 / 페이지당개수); 120/10 → 12   즉, 20페이지가 아닌 12페이지에서 짤라야 한다
if(최종끝번호 < 임시끝번호)
	임시끝번호 = 최종끝번호;
}


① DTO 생성

    ⓐ src/main/java → org.zerock.domain에 DTO생성(name:PageDTO.java)

    ⓑ 내용 추가
@ToString
@Getter
public class PageDTO {

	private int startPage, endPage; //시작번호/끝번호
	private boolean prev, next; //이전/다음 유무
	
	private int total; //총 개수
	private Criteria cri; //페이지객체
	
	public PageDTO(Criteria cri, int total) {
/*현재 페이지번호 : 3
총 글 개수 : 71
총 페이지 : 8페이지(1~10페이지 구하고 게시글 개수에 따라 8페이지로 축소)*/
		this.total = total;
		this.cri = cri;
//				3 / 10 → 0.3 → 올림 → 1.0 → * 10 → 10.0 → 정수변환 → 10
		this.endPage = (int) Math.ceil(cri.getPageNum() / 10.0) * 10; //현재는 10페이지까지 있는상태(다음 버튼 유)
		
		this.startPage = endPage - 9; //현재는 1페이지부터 있는 상태
		
		this.prev = this.startPage > 1; //이전 버튼 X
//					    71.0 / 10 → 7.1 → 올림 → 8.0 → 정수변환 → 8
		int realEnd = (int)(Math.ceil(total * 1.0 / cri.getAmount())); //8페이지까지
		
		this.endPage = realEnd <= endPage ? realEnd : endPage; //8<10 참이니 8
		
		this.next = this.endPage < realEnd; //다음 버튼 X
		
		
		
	}
	
	
}


② 테스트 추가

    ⓐ src/test/java → org.zerock.mapper → BoardMapperTests.java에서 내용 추가
@Test
public void testPageDTO() {
	
	Criteria cri = new Criteria(); //기본 현재 1페이지,10개씩
	
	PageDTO pageDTO = new PageDTO(cri,250); //글이 250개가 있을때
	
	log.info(pageDTO);
	
}

    ⓑ JUnit실행
로그로 찍은 PageDTO 안의 변수들(시작페이지,끝페이지,이전링크,다음링크)이 정상값으로 잘 찍히나 확인

    ⓒ 세팅을 바꿔서도 실행
	Criteria cri = new Criteria(); //기본 1페이지,10개씩
	cri.setPageNum(11); //내가 현재있는페이지를 11페이지로 변경
	PageDTO pageDTO = new PageDTO(cri,250); //글이 250개가 있을때
[11]부터 [20]까지 보여지고, 이전링크O, 다음링크O 모두 정상인가 확인

    ⓓ 세팅을 바꿔서도 실행 2
	Criteria cri = new Criteria(); //기본 1페이지,10개씩
	cri.setPageNum(21); //내가 현재있는 페이지를 21페이지로 변경
	PageDTO pageDTO = new PageDTO(cri,250); //글이 250개가 있을때
[21]부터 [25]까지 보여지고, 이전링크는 있지만 다음으로 가는 링크는 없는거(false) 확인

    ⓔ 세팅을 바꿔서도 실행 3
		Criteria cri = new Criteria(); //기본 1페이지,10개씩
		cri.setPageNum(25); //내가 현재있는 페이지를 25페이지로 변경
		
		PageDTO pageDTO = new PageDTO(cri,251); //글이 251개가 있을때
[21]부터 [26]까지 보여지고, 이전링크는 있지만 다음으로 가는 링크는 없는거(false) 확인


③ 화면에 전달

    ⓐ src/main/java → org.zerock.controller → BoardController.java에서 'list'메소드에 내용추가
@GetMapping("/list")
public void list(Criteria cri, Model model) {
	
	log.info("------------------------");
	log.info(cri);
	log.info("list.............");
	
	model.addAttribute("list", service.getList(cri));
	model.addAttribute("pageMaker", new PageDTO(cri, 123)); //PageDTO객체 넘겨주는 한줄 추가 (총 게시글 수 : 123개)
}

    ⓑ src → main → webapp → WEB-INF → views → board → list.jsp에서 내용 추가
<!-- /.table-responsive -->

<h3>${pageMaker}</h3>

</div>

    ⓒ 서버 재시작후 브라우저에서 PageDTO 속성들 잘 나오는지 테스트해보기

    ⓓ 브라우저 url에 pageNum파라미터를 전달해서 그에 상응하는 값들이 잘 나오는지 확인하기
http://localhost:8080/board/list?pageNum=11
		↓↓↓
PageDTO(startPage=11, endPage=13, prev=true, next=false, total=123, cri=Criteria(pageNum=11, amount=10))

    ⓔ list.jsp에서 내용 추가 (jstl - for문으로 Model이용해서 jsp로전달한 pageMaper(=PageDTO) 의 내용을 출력 (for문법은 jsp&servlet.txt 참조)
<!-- /.table-responsive -->
                            <h3>${pageMaker}</h3>
                            <div class="pull-right">
                            	<ul>
<c:forEach var="num" begin="${pageMaker.startPage}" end="${pageMaker.endPage}">
                            		<li>${num}</li>
</c:forEach>
                            	</ul>
                            </div>
</div>

    ⓕ url파라미터를 11로 줬을때 화면에 li로 11부터 13까지 출력이 잘 되는지 확인


③ 부트스트랩 적용

    ⓐ 구글에 bootstrap pagination 검색 후 들어가서 클래스 복사해서 ul과 li에 css적용하고 이전/다음 버튼(li) 추가
	<ul class="pagination">
		<li class="page-item"><a class="page-link" href="#">Previous</a></li>
<c:forEach~>
		<li class="page-item"><a class="page-link" href="#">${num}</a></li>
</c:forEach>
		<li class="page-item"><a class="page-link" href="#">Next</a></li>
	</ul>

    ⓑ 이전/다음 버튼이 boolean값에 따라 보이게/안보이게 jstl로 처리 (문법은 jsp/servlet.txt 참고)
<c:if test="${pageMaker.prev}">
                            		<li class="page-item"><a class="page-link" href="#">Previous</a></li>
</c:if>
<c:if test="${pageMaker.next}">
			<li class="page-item"><a class="page-link" href="#">Next</a></li>
</c:if>

    ⓒ active페이지(불들어오게) 처리 ({criteria.pageNum 으로 써도 됨)
<c:forEach~>
	<li class="page-item${pageMaker.cri.pageNum == num ? ' active' : ''}"><a class="page-link" href="#">${num}</a></li>
</c:forEach>


④ 페이징 링크 처리

    ⓐ 페이지 버튼 & 이전/다음페이지 버튼 클릭시 이동되게
<a class="page-link" href="list?pageNum=${num}">${num}</a> 이렇게 링크로도 간단하게 처리할수도 있지만

url파라미터가 쌓이게 하기위해 hidden form태그를 사용함

우선 a태그 href에 그냥 페이지변수만 넣어놓기
href="${num}">${num}</a> → for문속 페이지버튼
href="${pageMaker.startPage - 1}">Previous</a> → 이전버튼
href="${pageMaker.endPage + 1}">Next</a> → 다음버튼

ul감싼 div형제라인(아무데나상관x)에 히든폼 추가
<form method="get" action="/board/list" id="actionForm">
	<input type="hidden" name="pageNum" value="${pageMaker.cri.pageNum}">
	<input type="hidden" name="amount" value="${pageMaker.cri.amount}">
</form>

스크립트도 추가 (a태그 이벤트 막고 폼에 데이터 넣어 submit)
var actionForm = $("#actionForm");

$(".pagination a").on("click",function(e){
	e.preventDefault();
	
	var targetPage = $(this).attr("href");
//	console.log(targetPage);

	actionForm.attr("action","/board/list"); /*마크업에 action="/aaa" 라고 넣어논걸,
버튼을 클릭했을때 스크립트로 /bbb 라고 바꾼다음에 submit으로 넘기게 처리하면,
뒤로가기를 했을때 /aaa로 초기화되는게 아니고 바뀐 /bbb로 남아있게 된다★
그래서 같은 form에서 action을 여러개쓸때는 action속성을 마크업에서 넣지 않고, 스크립트로만 이벤트가 발생했을때 처리하는게 좋은듯함*/
	actionForm.find("input[name='pageNum']").val(targetPage);
	
	actionForm.submit(); //값 바뀌는거 브라우저에서 테스트 먼저 하고 마지막에 추가
	
});

    ⓑ 목록 제목의 링크를 a링크에서 → hidden form으로 수정 (url파라미터가 쌓이게 하기위해)
<td><a href="/board/get?bno=${vo.bno}">${vo.title}</a></td>
이렇게 되있던거 아래처럼 번호만 남기고 지우고 'move'클래스하나 추가
		↓↓↓
<td><a href="${vo.bno}" class="move">${vo.title}</a></td>

이후 스크립트 추가 (form태그에 input추가하고 form태그 action을 /board/get으로 바꾼후 submit)
이때 디테일하게 하려면 뒤로가기를 했을때도 생각해야되는데, /board/get으로 바꾸고 뒤로가기를 하면 바뀌기 전으로까지는 돌아가지지 않아서,
그대로 마크업에 /board/get으로 남아있게된다. 때문에 바뀌기전action은 마크업에서 없애고, 대신 스크립트로 해당 이벤트에 걸기
$(".move").on("click",function(e){
	e.preventDefault();
	
	var targetBno = $(this).attr("href");
//	console.log(targetBno);

	actionForm.find("input[name='bno']").remove(); //클릭했을때 append된게 뒤로가기했을때 그대로 남아있음 방지용★
	actionForm.append("<input type='hidden' name='bno' value='" + targetBno + "'>")
	actionForm.attr("action","/board/get");

	actionForm.submit(); //값 바뀌는거 브라우저에서 테스트 먼저 하고 마지막에 추가
});


⑤ get페이지도 (페이징유지 위해) 부분 수정

    ⓐ src/main/java → org.zerock.controller → BoardController.java수정 ('get'메소드에 파라미터 추가)
public void get(Long bno, @ModelAttribute("cri")Criteria cri, Model model) { //모델어트리뷰트 안쓰면 criteria.으로 써야됨(첫글자소문자)

    ⓑ get.jsp에서 히든폼 추가
<form method="get" action="/board/list" id="actionForm">
	<input type="hidden" name="pageNum" value="${cri.pageNum}">
	<input type="hidden" name="amount" value="${cri.amount}">
	<input type="hidden" name="bno" value="${vo.bno}"> //${param.bno}를 써도 됨(request.getParameter과 동일)
</form>

    ⓒ a태그 클래스추가 및 스크립트 추가
(bno는 list로 돌아갈때 필요없고, 수정/삭제로 갈때는 필요하므로 form태그 안에는 넣어놓되,
list로 돌아가는 submit을 스크립트로 조작해서 input[name="bno"]을 remove() 한다)

<a href="/board/list" class="btn btn-default btnList">목록</a>
<a href="/board/modify?bno=${vo.bno}" class="btn btn-default btnMod">수정/삭제</a>

<script>
	var actionForm = $("#actionForm");

	$(".btnList").click(function(e){
		e.preventDefault();
		actionForm.find("input[name='bno']").attr("disabled","true"); /*이때 input-bno를 remove를 시키면,
bno가 지워진 상태로 리스트로 이동하고, 다시 뒤로가기로 돌아오면 마크업은 여전히 input-bno가 마크업에서 지워진 상태이기때문에
수정/삭제버튼을 클릭하면 오류가 발생함. 그래서 remove말고 disabled로 처리하면,
(뒤로가기후) 수정/삭제를 누른 상황에서는 다시 풀기만 하면되서 수월한듯★ */
		actionForm.submit();
	});
</script>

    ⓓ 상세페이지에서 목록버튼을 눌러 리스트로 돌아갔을때 n페이지로 이동되는지 (URL파라미터가 전달되는지) 확인

    ⓔ 수정/삭제페이지 버튼동작하는 스크립트도 추가
$(".btnMod").click(function(e){
	e.preventDefault();
	actionForm.find("input[name='bno']").removeAttr("disabled");
//만약 리스트버튼을 눌러서 갔다가 다시 뒤로가기로 와서 여전히 disable된 상태로 수정/삭제를 클릭했다면 풀어주기 ★
	actionForm.attr("action","/board/modify"); /*이렇게 분기 처리했으면, 기존 마크업에 있는 action속성 삭제하고,
이것처럼 list로 가는 이벤트에 attr("action","/board/list");스크립트 추가할것. 이유는 뒤로가기시 스크립트 실행전으로 돌아가지않는 문제때문에
수정/삭제버튼을 눌렀다가 뒤로가서 /board/list로 이동하는 버튼 클릭시500오류 발생함★*/
	actionForm.submit();
});

    ⓕ 파라미터 수정페이지까지 가져가지는지 확인


⑥ 수정/삭제 페이지에서 수정/삭제 완료후 목록페이지로 파라미터 추가전달처리

    ⓐ modify.jsp에서 기존 form태그안에 히든태그 추가
<input type="hidden" name="pageNum" value="${cri.pageNum}">
<input type="hidden" name="amount" value="${cri.amount}">

    ⓑ src/main/java → org.zerock.controller → BoardController.java에서 'modify'메소드(post) 에게 Criteria파라미터 추가
public String modify(BoardVO vo, Criteria cri, RedirectAttributes rttr) {

    ⓒ Crireria도 RedirectAttributes로 전달 (이때 addFlashAttribute말고 addAttribute로 '주소창에 보이게' 전달)
if (result == 1) {
	rttr.addFlashAttribute("result", vo.getBno());
	rttr.addFlashAttribute("type", "m");
}
rttr.addAttribute("pageNum",cri.getPageNum());
rttr.addAttribute("amount",cri.getAmount());

    ⓓ 삭제기능도 페이지번호 돌아오게 'remove'메소드(post)도 'modify'메소드랑 똑같이 파라미터받기/보내기 추가
public String remove(Long bno, Criteria cri, RedirectAttributes rttr) {
	
	int result = service.remove(bno);
	
	if (result == 1) {
		rttr.addFlashAttribute("result", bno);
		rttr.addFlashAttribute("type", "r");
	}

	rttr.addAttribute("pageNum",cri.getPageNum());
	rttr.addAttribute("amount",cri.getAmount());
	
	return "redirect:/board/list";
	
}

    ⓔ modify.jsp 스크립트 수정
$(".btn").click(function(e){
	e.preventDefault();
	
	var operation = $(this).data("oper");
	var form = $("form");
//	console.log(operation);
	
	if(operation === "list"){
		form.attr("method","GET")
		form.attr("action","/board/list")
		form.find(input[name='bno']).remove();
		form.find(input[name='title']).remove();
		form.find(textarea[name='content']).remove();
		form.find(input[name='writer']).remove();
		form.submit();
	}else if(operation === "modify"){
		form.attr("method","POST")
		.attr("action","/board/modify")
		.submit();
	}else if(operation === "remove"){
		form.attr("method","POST")
		.attr("action","/board/remove")
		.submit();
	}
	
})


⑦ 전체 데이터 개수 출력 (Criteria를 준 이유는 전체데이터 말고, 좀이따 검색결과데이터들만도 카운트도 처리해야하기때문)

    ⓐ src/main/java → org.zerock.mapper → BoardMapper.java에서 내용 추가
int getTotalCount(Criteria cri);

    ⓑ src/main/resources → org → zerock → mapper → BoardMapper.xml에서 내용 추가
<select id="getTotalCount" resultType="int">
	select count(bno) from tbl_board where bno>0
</select>

    ⓒ src/main/java → org.zerock.service → BoardService.java인터페이스에서 내용 추가
int getTotal(Criteria cri);

    ⓓ src/main/java → org.zerock.service → BoardServiceImpl.java에서 내용 추가(인터페이스 구현)
@Override
public int getTotal(Criteria cri) {
	return mapper.getTotalCount(cri);
}

    ⓔ src/main/java → org.zerock.controller → BoardController.java에서 'list'메소드의 상수(전체데이터개수)를 동적으로 바꾸기
model.addAttribute("pageMaker", new PageDTO(cri, 123));
model.addAttribute("pageMaker", new PageDTO(cri, service.getTotal(cri)));

    ⓕ 서버재시작 후 페이징 13페이지도 이후도 나오나 테스트

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

검색 처리

----------------------------------------------------------------------------------------------------

① 검색기능 구현
mybatis가 편리하긴하나, sql이 고정된다. 따라서 상황에 따라 sql을 동적으로 만들기는 제한이 있기때문에
xml로 상황에 따라 다른 sql을 만들기가 가능하다. https://mybatis.org/mybatis-3/ko/dynamic-sql.html 참고
foreach의 collection속성을 이용하면 컬렉션/기본배열을 순회할 수 있다. 각각 사용법은 아래에서collection검색

    ⓐ src/main/java → org.zerock.mapper → BoardMapper.java에서 내용추가
(Map을 두번 감싼 이유는 xml에서 부를려면 map에다 한번더 담아서 키로 불러야함)

List<BoardVO> searchTest(Map<String, Map<String,String>> map);


    ⓑ src/main/resources → org → zerock → mapper → BoardMapper.xml에서 내용 추가
(foreach태그는 컬렉션(Map,List,Set)을 순회하며 키/값을 다 꺼내는 기능이다.
collection속성의 값으로는 파라미터로 받은 map이름 말고, 그 map안에 key(value로 map을 갖고있는)를 지정해야함
↓↓↓ 좀더 자세히 ↓↓↓
Map<String,String>() map1 = new HashMap<>(); ← 이때 map1말고
Map<String,Map<String,String>() outer = new HashMap<>();
outer.put("asd",map1); ← 이렇게 map1을 put 한 key 즉 "asd"를 collection 속성의 값으로 넣어야됨)

Map에서, index속성은 키가되고 item속성은 값이 된다. 이름은 각각 "key"/"val"로 지정.)

<select id="searchTest" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where
	
	<foreach collection="map" index="key" item="val">
		#{key} #{val}
	</foreach>
	
	<![CDATA[
	rownum < 10
	]]>

</select>

    ⓒ src/test/java → org.zerock.mapper → BoardMapperTests.java에서 테스트 내용 추가
@Test
public void testSearch() {
	Map<String, String> map = new HashMap<>();
	map.put("T","TTT");
	map.put("C","CCC");
	
	Map<String, Map<String, String>> outer = new HashMap<>();
	outer.put("map",map);
	
	List<BoardVO> list = boardMapper.searchTest(outer);
	
	log.info(list);
	
}

    ⓓ JUnit실행해서 (오류) 결과 확인('C','CCC' 와 'T','TTT'가 sql문 안에 정상적으로 들어가진걸 확인할 수 있음)
ERROR: jdbc.sqltiming - 1. PreparedStatement.execute() FAILED! select * from tbl_board where 'C' 'CCC' 'T' 'TTT' rownum < 10 
 {FAILED after 4 msec}
java.sql.SQLSyntaxErrorException: ORA-01745: invalid host/bind variable name

    ⓔ BoardMapper.xml에서 내용 수정 (key가 t일때 → title like '검색어' ← 문장 추가)
<select id="searchTest" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where
	
	<foreach collection="map" index="key" item="val">
↓↓↓↓↓
		<if test="key == 'T'.toString()">
			title like #{val}
		</if>
↑↑↑↑↑
	</foreach>
	
	<![CDATA[
	rownum < 10
	]]>

</select>

    ⓕ BoardMapperTests로 돌아와 JUnit실행해서 (오류) 결과 확인 (이제 여기서 and만 붙이면 완료)
ERROR: jdbc.sqltiming - 1. PreparedStatement.execute() FAILED! select * from tbl_board where title like 'TTT' rownum < 10 
 {FAILED after 5 msec}
java.sql.SQLSyntaxErrorException: ORA-00933: SQL command not properly ended

    ⓖ 다시 BoardMapper.xml에서 내용 추가
(trim의 suffix속성을 이용해서 뒤에다 and를 붙임. prefix는 앞
trim은 내용이 있으면 만들어지고 없으면 안만들어짐. css의 before/after랑 똑같음)

<select id="searchTest" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where
↓↓↓↓↓
	<trim suffix="and">
↑↑↑↑↑
	<foreach collection="map" index="key" item="val">
		<if test="key == 'T'.toString()">
			title like #{val}
		</if>
	</foreach>
↓↓↓↓↓
	</trim>
↑↑↑↑↑
	
	<![CDATA[
	rownum < 10
	]]>

</select>

    ⓗ BoardMapperTests.java로 돌아와 JUnit실행해서 결과 확인 (뒤에 and가 붙음)
select * from tbl_board where title like 'TTT' and rownum < 10

    ⓘ BoardMapperTests.java에서 map내용 변경
map.put("ASD","TTT");
map.put("C","CCC");

    ⓙ JUnit실행해서 결과 확인(title like 'TTT' and 가 없어짐)
select * from tbl_board where rownum < 10

    ⓚ XML에서 내용 추가 (제목,내용,작성자로 검색)
<select id="searchTest" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where
	
	<trim suffix="and">
	<foreach collection="map" index="key" item="val">
		<if test="key == 'T'.toString()">
			title like #{val}
		</if>
↓↓↓↓↓
		<if test="key == 'C'.toString()">
			content like #{val}
		</if>
		<if test="key == 'W'.toString()">
			writer like #{val}
		</if>
↑↑↑↑↑
	</foreach>
	</trim>
	
	<![CDATA[
	rownum < 10
	]]>

</select>

    ⓛ JUnit실행해서 (오류) 결과 확인(조건 사이사이에 or를 추가해야함)
select * from tbl_board where content like 'CCC' title like 'TTT' writer like 'WWW' and rownum < 10 
 {FAILED after 5 msec}
java.sql.SQLSyntaxErrorException: ORA-00933: SQL command not properly ended

    ⓜ XML에서 내용 추가 (separator속성으로 루프 중간에 단어 끼워넣기)
<select id="searchTest" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where
	
	<trim suffix="and">
↓↓↓↓↓
	<foreach collection="map" index="key" item="val" separator="or">
↑↑↑↑↑
		<if test="key == 'T'.toString()">
			title like #{val}
		</if>
		<if test="key == 'C'.toString()">
			content like #{val}
		</if>
		<if test="key == 'W'.toString()">
			writer like #{val}
		</if>
	</foreach>
	</trim>
	
	<![CDATA[
	rownum < 10
	]]>

</select>

    ⓝ JUnit실행해서 결과 확인
select * from tbl_board where content like 'CCC' or title like 'TTT' or writer like 'WWW' and rownum < 10

    ⓞ XML에서 내용 추가 (and때문에 or끼리 괄호로 싸야됨 (and먼저연산되므로))
<select id="searchTest" resultType="org.zerock.domain.BoardVO">
	select * from tbl_board where
	
	<trim suffix="and">
↓↓↓↓↓
	<foreach collection="map" index="key" item="val" separator="or" open="(" close=")">
↑↑↑↑↑
		<if test="key == 'T'.toString()">
			title like #{val}
		</if>
		<if test="key == 'C'.toString()">
			content like #{val}
		</if>
		<if test="key == 'W'.toString()">
			writer like #{val}
		</if>
	</foreach>
	</trim>
	
	<![CDATA[
	rownum < 10
	]]>

</select>

    ⓟ JUnit실행해서 결과 확인
select * from tbl_board where ( content like 'CCC' or title like 'TTT' or writer like 'WWW' ) and rownum < 10

    ⓠ 검색조건이 없을때도 잘 나오나 테스트 (BoardMapperTests에서 아래 내용 주석해보기)
//map.put("T","TTT");
//map.put("C","CCC");
//map.put("W","WWW");

↓↓↓결과 확인↓↓↓
select * from tbl_board where rownum < 10


② 페이징 처리용 Criteria에 검색 기능 추가하기

    ⓐ src/main/java → org.zerock.domain → Criteria.java에서 멤버변수 추가
private String type;
private String keyword;

    ⓑ 메소드도 추가 (type속성을 쪼개서 배열로 반환하는 메소드, null이면 빈 배열)
public String[] getTypeArr() {
	return type == null ? new String[]{} : type.split("");
}

    ⓒ src/main/resources → org → zerock → mapper → BoardMapper.xml에서 'getListWithPaging' id를 갖고있는 태그에 내용 삽입
(방금 만든, 배열을 반환하는 getTypeArr() 메소드를 foreach의 collection속성을 이용해 getter호출할 수 있는데
'get'을 빼고 첫글자는 소문자로 쓰면 된다. 또 Map에서는 key/item을 둘다 쓰는데 기본배열은 item속성만 쓴다
이때 item은 자바 향상된 for문 생각하면됨)

<select id="getListWithPaging" resultType="org.zerock.domain.BoardVO">
<![CDATA[
select * from
(
	select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
	from tbl_board 
	where
]]>
<foreach collection="typeArr" item="type">
	<if test="type == 'T'.toString()">
		title like #{keyword}
	</if>
	<if test="type == 'C'.toString()">
		content like #{keyword}
	</if>
	<if test="type == 'W'.toString()">
		writer like #{keyword}
	</if>
</foreach>
<![CDATA[
	bno > 0 and rownum > 0 and rownum <= #{pageNum} * #{amount}
) 
where rn > (#{pageNum} - 1) * #{amount}
]]>
</select>

    ⓓ src/test/java → org.zerock.mapper → BoardMapperTests.java에서 'testPaging'메소드 복사 붙여넣기 후 내용추가
@Test
public void testSearchPaging() {
	
	//1페이지, 10개
	Criteria cri = new Criteria();
↓↓↓↓↓
	cri.setType("T");
	cri.setKeyword("Test");
↑↑↑↑↑
	List<BoardVO> list = boardMapper.getListWithPaging(cri);
	
	list.forEach(b -> log.info(b));
	
}

    ⓔ JUnit실행 (오류)결과 확인 (title like 이 정상적으로 들어갔고 and가 없어서 오류나는 모습이다)
select * from ( select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
from tbl_board where title like 'Test' bno > 0 and rownum > 0 and rownum <= 1 * 10 ) where 
rn > (1 - 1) * 10 
 {FAILED after 38 msec}
java.sql.SQLSyntaxErrorException: ORA-00907: missing right parenthesis

    ⓕ XML 수정 (trim 써서 앞뒤로 괄호 붙이고 뒤에 and 붙이기)
<select id="getListWithPaging" resultType="org.zerock.domain.BoardVO">
<![CDATA[
select * from
(
	select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
	from tbl_board 
	where
]]>
↓↓↓↓↓
<trim prefix="(" suffix=") and">
↑↑↑↑↑
<foreach collection="typeArr" item="type">
	<if test="type == 'T'.toString()">
		title like #{keyword}
	</if>
	<if test="type == 'C'.toString()">
		content like #{keyword}
	</if>
	<if test="type == 'W'.toString()">
		writer like #{keyword}
	</if>
</foreach>
↓↓↓↓↓
</trim>
↑↑↑↑↑
<![CDATA[
	bno > 0 and rownum > 0 and rownum <= #{pageNum} * #{amount}
) 
where rn > (#{pageNum} - 1) * #{amount}
]]>
</select>

    ⓖ JUnit실행해서 정상으로 동작되는지 확인, 아래 내용 주석했을때 조건이 잘 빠지나도 테스트해보기
//cri.setType("T");
//cri.setKeyword("Test");

    ⓗ 조건이 여러개일때를 위해 XML수정
<select id="getListWithPaging" resultType="org.zerock.domain.BoardVO">
<![CDATA[
select * from
(
	select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
	from tbl_board 
	where
]]>
<trim prefix="(" suffix=") and">
↓↓↓↓↓
<foreach collection="typeArr" item="type" separator="or">
↑↑↑↑↑
	<if test="type == 'T'.toString()">
		title like #{keyword}
	</if>
	<if test="type == 'C'.toString()">
		content like #{keyword}
	</if>
	<if test="type == 'W'.toString()">
		writer like #{keyword}
	</if>
</foreach>
</trim>
<![CDATA[
	bno > 0 and rownum > 0 and rownum <= #{pageNum} * #{amount}
) 
where rn > (#{pageNum} - 1) * #{amount}
]]>
</select>

    ⓘ 조건 여러개(title,content,writer) 넣고 Junit실행. 오류 없이 잘 되나 확인
@Test
public void testSearchPaging() {
	
	//1페이지, 10개
	Criteria cri = new Criteria();
↓↓↓↓↓
	cri.setType("TCW");
↑↑↑↑↑
	cri.setKeyword("Test");
	
	List<BoardVO> list = boardMapper.getListWithPaging(cri);
	
	list.forEach(b -> log.info(b));
	
}

    ⓙ XML수정 (like '%'|| ||'%' 처리)
<select id="getListWithPaging" resultType="org.zerock.domain.BoardVO">
<![CDATA[
select * from
(
	select /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn,bno,title,writer,regdate,updatedate 
	from tbl_board 
	where
]]>
<trim prefix="(" suffix=") and">
<foreach collection="typeArr" item="type" separator="or">
	<if test="type == 'T'.toString()">
↓↓↓↓↓
		title like '%'||#{keyword}||'%'
↑↑↑↑↑
	</if>
	<if test="type == 'C'.toString()">
↓↓↓↓↓
		content like '%'||#{keyword}||'%'
↑↑↑↑↑
	</if>
	<if test="type == 'W'.toString()">
↓↓↓↓↓
		writer like '%'||#{keyword}||'%'
↑↑↑↑↑
	</if>
</foreach>
</trim>
<![CDATA[
	bno > 0 and rownum > 0 and rownum <= #{pageNum} * #{amount}
) 
where rn > (#{pageNum} - 1) * #{amount}
]]>
</select>

    ⓚ test가 포함된 데이터 DB에 넣고 테스트 JUnit해보기

    ⓛ 주석 해보고 한번 테스트 해보기
//cri.setType("TCW");
//cri.setKeyword("Test");


③ 글 전체 개수 구할때도 검색조건을(검색을 했을때를 위해) 넣어놔야한다

    ⓐ XML에서 아까전에 만든 getTotalCount에도 검색기능을 넣어야한다
그대로 복붙해도 되지만, 합쳐서 같이쓰는게 좋기때문에 SQL코드조각을 만든다

<select id="getListWithPaging" 의

<trim prefix="(" suffix=") and">
<foreach collection="typeArr" item="type" separator="or">
	<if test="type == 'T'.toString()">
		title like '%'||#{keyword}||'%'
	</if>
	<if test="type == 'C'.toString()">
		content like '%'||#{keyword}||'%'
	</if>
	<if test="type == 'W'.toString()">
		writer like '%'||#{keyword}||'%'
	</if>
</foreach>
</trim>

를 짤라서(ctrl+x)

맨 위에 (<mapper> 태그 밑에)

<sql id="criteria">
		
</sql>

를 선언하고 안에 붙여넣는다

그리고 아까 짜른데에 가서 다시 include한다
<include refid="criteria"></include>


    ⓑ <select id="getTotalCount" 에서도 만들어놓은 검색기능include하기
<select id="getTotalCount" resultType="int">
	select count(bno) from tbl_board where
	<include refid="criteria"></include>
	bno>0
</select>


④ 화면페이지

    ⓐ list.jsp에서 <h3>${pageMaker}</h3> 출력해놓은거 지우고 그자리에 내용 추가
<form method="get" action="/board/list" id="searchForm">
	<select name="type">
		<option value="">---</option>
		<option value="T">제목</option>
		<option value="C">내용</option>
		<option value="W">작성자</option>
		<option value="TC">제목+내용</option>
		<option value="TCW">제목+내용+작성자</option>
	</select>
	<input type="text" name="keyword">
	<input type="hidden" name="pageNum" value="${pageMaker.cri.pageNum}">
	<input type="hidden" name="amount" value="${pageMaker.cri.amount}">
	<button class="btn btn-default">Search</button>
</form>

    ⓑ 브라우저 list.jsp에서 'type'셀렉트박스 선택, 'keyword'텍스트박스는 'test'라고 입력해서 url에 아래처럼 쿼리스트링이 잘 전달 되는지 확인
http://localhost:8080/board/list?type=T&keyword=test&pageNum=4&amount=10

    ⓒ 스크립트 추가 (submit전에 1페이지로 이동시키는 기능)
var searchForm = $("#searchForm");
searchForm.find("button").on("click",function(e){
	e.preventDefault();

	if (searchForm.find("select[name='type']").val() === "") {
		alert("검색 항목을 선택하세요.");
		return;
	}
	if (searchForm.find("input[name='keyword']").val() === "") {
		alert("검색어를 입력하세요.");
		return;
	}

	searchForm.find("input[name='pageNum']").val(1); //검색시 1페이지로 이동

	searchForm.submit();
});

    ⓓ 검색완료했을때 검색한 내용(select/검색어input-text) 안사라지고 남아있게 유지 시키기 (3항연산자로 처리, 문자열은 ==말고 eq로 = equals)
<form method="get" action="/board/list" id="searchForm">
	<select name="type">
↓↓↓↓↓
		<option value="" ${pageMaker.cri.type == null ? "selected" : ""}>---</option>
		<option value="T" ${pageMaker.cri.type eq 'T' ? "selected" : ""}>제목</option>
		<option value="C" ${pageMaker.cri.type eq 'C' ? "selected" : ""}>내용</option>
		<option value="W" ${pageMaker.cri.type eq 'W' ? "selected" : ""}>작성자</option>
		<option value="TC" ${pageMaker.cri.type eq 'TC' ? "selected" : ""}>제목+내용</option>
		<option value="TCW" ${pageMaker.cri.type eq 'TCW' ? "selected" : ""}>제목+내용+작성자</option>
↑↑↑↑↑
	</select>
↓↓↓↓↓
	<input type="text" name="keyword" value="${pageMaker.cri.keyword}">
↑↑↑↑↑
	<input type="hidden" name="pageNum" value="${pageMaker.cri.pageNum}">
	<input type="hidden" name="amount" value="${pageMaker.cri.amount}">
	<button class="btn btn-default">Search</button>
</form>

    ⓔ 검색결과가 페이징시에도 유지되도록 (list.jsp에서 'actionForm'폼에 'type','keword' 히든태그 추가해서 검색데이터도 전달)
<form method="get" action="/board/list" id="actionForm">
	<input type="hidden" name="pageNum" value="${pageMaker.cri.pageNum}">
	<input type="hidden" name="amount" value="${pageMaker.cri.amount}">
↓↓↓↓↓
	<input type="hidden" name="type" value="${pageMaker.cri.type}">
	<input type="hidden" name="keyword" value="${pageMaker.cri.keyword}">
↑↑↑↑↑
</form>

    ⓕ get.jsp에 갔다가 돌아올시 검색한것 안날라가게 (get.jsp의 form태그에 검색정보 추가)
<form method="get" action="/board/list" id="actionForm">
	<input type="hidden" name="pageNum" value="${cri.pageNum}">
	<input type="hidden" name="amount" value="${cri.amount}">
	<input type="hidden" name="bno" value="${param.bno}">
↓↓↓↓↓
	<input type="hidden" name="type" value="${cri.type}">
	<input type="hidden" name="keyword" value="${cri.keyword}">
↑↑↑↑↑
</form>

    ⓖ 수정/삭제했을때도 검색내용 유지(일단 modify.jsp에서 검색정보 히든태그 추가)
<input type="hidden" name="type" value="${cri.type}">
<input type="hidden" name="keyword" value="${cri.keyword}">

    ⓗ 수정/삭제했을때도 검색내용 유지(BoardController.java에서 'modify' POST 메소드와 'remove' POST 메소드에 대해
다른페이지로 보낼때쓰는 RedirectAttributes.addAttribute 각각 추가)
rttr.addAttribute("type",cri.getType());
rttr.addAttribute("keyword",cri.getKeyword());

    ⓦ 뒤로가기시 파라미터 계속 따라붙는거, 페이지네이션 클릭했는데 get으로 가는거 수정(list.jsp)
window.onpageshow = function (event){
	if(event.persisted || (window.performance && window.performance.navigation.type == 2)){
		window.location.reload(); //뒤로/앞으로 갔을때 새로고침시키기
	}
}

    ⓧ 검색결과 몇건인지 출력 (list.jsp)
${pageMaker.total} 넣으면 됨

----------------------------------------------------------------------------------------------------

사용자가 글을 등록한 후 뒤로가기 해서 다시 등록하면 2개,3개… 계속 도배가 가능한데 이를 막는 방법

register.jsp에서 스크립트로 스위치를 하나 만들어서, submit() 하기 직전에 바꿔서, click이벤트의 상단에 스위치가 바뀌었으면 취소(return;)시킨다
var sw = false;

form.find("#write").on("click",function(e){
	e.preventDefault();

	if(sw)
		return;
	.
	.
	.

	sw = true;

	form.submit();
});

----------------------------------------------------------------------------------------------------

삭제/수정 등을 뒤로가기 방지하려고 location.replace()쓰기위해 ajax로 처리

(modify.jsp)

}else if(operation === "remove"){
	form.attr("method","POST")
	.attr("action","/board/remove")
	.submit();
}

기존의 위 코드에서 아래로 변경↓↓↓

}else if(operation === "remove"){
	$.ajax({
		type:"POST",
		url:"/board/remove/", //필수:: 응답 프로그램 주소(acrion)
		data:form.serialize(), //폼태그 내의 모든폼요소들을 묶어서 문자열로 만듦 ID=aaa&PW=bbb
		async:false, //선택:: true(동기) or false(비동기) (기본값:false)
		success:function(result){ //선택:: 돌려받는 데이터가 있을때만 구현
			//console.log(result);
			location.replace("/board/list?pageNum=" + $("input[name='pageNum']").val() +
					"&amount=" + $("input[name='amount']").val() +
					"&type=" + $("input[name='type']").val() +
					"&keyword=" + $("input[name='keyword']").val() +
					"&bno=" + $("input[name='bno']").val() +
					"&modType=" + "r"
			);
		},
		error:function(a,b,c){//선택:: 예외처리 이벤트(catch절)
			console.log(a,b,c);
		}
	});
}


(컨트롤러 주석)

@PostMapping("/remove")
public String remove(Long bno, Criteria cri, RedirectAttributes rttr) {
	
	int result = service.remove(bno);
	
	if (result == 1) {
		rttr.addFlashAttribute("result", bno);
		rttr.addFlashAttribute("modType", "r");
	}

	rttr.addAttribute("pageNum",cri.getPageNum());
	rttr.addAttribute("amount",cri.getAmount());
	rttr.addAttribute("type",cri.getType());
	rttr.addAttribute("keyword",cri.getKeyword());
	
	return "redirect:/board/list";
	
}

↓↓↓

//	rttr.addAttribute("pageNum",cri.getPageNum());
//	rttr.addAttribute("amount",cri.getAmount());
//	rttr.addAttribute("type",cri.getType());
//	rttr.addAttribute("keyword",cri.getKeyword());

	return "redirect:/board/list";


(list.jsp)

$(window).on("load",function(){
↓↓↓↓↓
	//ajax로 처리하기위한 코드
	const url = new URL(window.location.href);
	const urlParams = url.searchParams;
↑↑↑↑↑

	var result = "<c:out value='${result}'/>";
	var type = "<c:out value='${modType}'/>";

↓↓↓↓↓
	//ajax로 처리하기위한 코드
	if(urlParams.has('bno')) 
		result = urlParams.get('bno');
	if(urlParams.has('modType'))
		type = urlParams.get('modType');
↑↑↑↑↑

----------------------------------------------------------------------------------------------------

① 사용자가 삭제하고 뒤로가기로 get페이지가서 새로고침하면 목록으로 튕겨나게 처리

    ⓐ (get.jsp)
$(document).ready(function(){
	if("${vo.bno}" === ""){
		actionForm.attr("action","/board/null")
		.submit();
	}
});

    ⓑ (컨트롤러)
@GetMapping("/null")
public void nullPage(Criteria cri, Model model) {
	model.addAttribute("cri",cri);
}

    ⓒ(null.jsp 추가)
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" language="java" %>
    
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>


<%@ include file="../includes/header.jsp" %>

	<h2 style="padding:20px 0">잘못된 경로입니다. 목록으로 이동합니다...</h2>
	
	<script>
		$(document).ready(function(){
			setTimeout(function(){
				var url = "/board/list?pageNum=${cri.pageNum}" +
					"&amount=${cri.amount}" +
					"&type=${cri.type}" +
					"&keyword=${cri.keyword}";
				location.replace(url);
			},500);
		});
	</script>


<%@ include file="../includes/footer.jsp" %>


② 사용자가 삭제하고 뒤로가기로 get페이지 가서 수정/삭제버튼 눌러서 이동할시 위와 동일하게 modify.jsp에서 처리
var form = $("form");

$(document).ready(function(){
	if("${vo.bno}" === ""){
		form.attr("action","/board/null")
		.attr("method","GET")
		.submit();
	}
});

----------------------------------------------------------------------------------------------------

세션

비밀번호 등 클라이언트의 민감한 인증 정보를 브라우저가 아닌 서버에 저장
페이지 이동시에도 정보가 사라지지않으며 브라우저가 완전히 다 꺼지면 삭제됨
브라우저자체를 완전히 다 종료시켜야 사라짐. 탭이나 브라우저 창이 하나라도 남아있으면 안됨
브라우저별로 생성됨 크롬시크릿모드의 경우 별개의 브라우저로 봄)
크롬 ctrl+shift+t로 다시 열면 로그인이 유지돼있는거같아도(세션이 제거가 안 된거같아도) 새로고침하면 로그인이 풀린걸 알 수 있음


세션 쓰려면 우선 파라미터에 HttpServletRequest가 필요함

세션 생성 및 정보 저장
public void login_ok(MemberVO vo, HttpServletRequest req){
	HttpSession session = req.getSession();
	MemberVO mem = service.login(vo);
	session.setAttribute("member", mem);
}

request.getSession 메소드에 인수를 안넣으면 true가 기본값임
request.getSession(true): 세션이 있으면 반환, 없을경우 새로운 세션을 생성해서 반환
request.getSession(false): 세션이 있으면 반환, 없을경우 새로운 세션을 생성하지 않고 null을 반환

세션을 만든 페이지(Post/Get Mapping한 jsp페이지) 부터 모든 jsp페이지에서 el로 사용 가능
${member} ore ${member.ID}


세션 조회
public String home(HttpServletRequest req) {
HttpSession session = req.getSession();
System.out.println(Arrays.toString(session.getValueNames()));


특정 jsp페이지에서만 세션 끄기
<%@ page session="false" %>


세션 삭제 (한개/전체)
public String home(HttpServletRequest req) {
HttpSession session = req.getSession();
session.removeAttribute("member"); // 한개 삭제
session.invalidate(); // 전체 삭제

----------------------------------------------------------------------------------------------------

쿠키

사용자의 로컬에 저장되어 브라우저가 완전히 꺼져도 살아있음. (유통기한을 초단위로 설정할수 있음)
개인PC가 아니라면 "보안취약"
쿠키에는 "용량 제한"이 있어 많은 정보를 담을 수 없음
브라우저마다 쿠키에 대한 지원 형태가 다르기 때문에 브라우저간 공유가 불가
아이디 저장, 자동로그인등에 이용
크롬시크릿모드에서는 쿠키를 조회할수도 없고 저장할수도 없음
쿠키는 4kb의 용량제한이 있다

주로 사용하는곳 : 다시 보지 않음 팝업 창 기능

------------------------------

생성

[컨트롤러에서 생성 - HttpServletResponse resp 파라미터 필요]
//loginCookie라는 키로 세션아이디를 담아 쿠키를 생성, 같은이름의 쿠키가 있으면 덮어씀
Cookie testCookie = new Cookie("testCookie","쿠키값");
cookie.setMaxAge(60 * 60 * 24); // 쿠키 유효시간을 초 단위로 설정
response.addCookie(cookie); // 생성한 쿠키를 HTTP 응답에 추가

/* 쿠키를 읽을수 있는 범위 지정한 디렉토리 하위 파일에서만 사용가능함
"/" → 모든 페이지에서 쿠키조회가 가능함
"/member" → /member 하위에 접속했을때만 쿠키조회가 가능함
"/member/list" → /member/list 하위에 접속했을때만 쿠키조회가 가능함
setPath를 안쓰면 기본값으로 현재 페이지가 있는 폴더부터 사용이 가능함*/
testCookie.setPath("/");
loginCookie.setMaxAge(60*60*24*90); //초단위로 쿠키유지기간 설정 (90일)
resp.addCookie(testCookie); //response에 쿠키를담아 클라이언트에게 보낸다

<쿠키 만들때 세션을 넣어서 만들기>
Cookie loginCookie = new Cookie("loginCookie",session.getId());

[자바스크립트에서 생성]
자바스크립트팁.txt에서 참고

------------------------------

조회

[브라우저에서 조회]
크롬개발자도구 → Application탭 → Storage → Cookies 더블클릭하거나 옆에 화살표 클릭 → http://localhost:8080 클릭

[컨트롤러에서 조회]

<방법1>
Cookie[] clist = request.getCookies();
System.out.println(Arrays.deepToString(Arrays.stream(clist).map(e -> new String[]{e.getName(), e.getValue()}).toArray()));

<방법2(안될수도 있음)>
Cookie cookie = WebUtils.getCookie(req, "loginCookie");
String sessionID = cookie.getValue();


[자바스크립트에서 조회]
자바스크립트팁.txt에서 참고

------------------------------

삭제

[개인 브라우저에서 삭제]
ctrl+shift+delete → 인터넷사용기록삭제

[컨트롤러에서 삭제]
(특정 쿠키 제거 - HttpServletResponse resp 파라미터 필요)
Cookie cookic = new Cookie("testCookie", null); // choiceCookieName(쿠키 이름)에 대한 값을 null로 지정
cookic.setPath("/");
cookic.setMaxAge(0); // 유효시간을 0으로 설정
resp.addCookie(cookic); // 응답 헤더에 추가해서 없어지도록 함

(모든 쿠키 제거 - HttpServletResponse resp, HttpServletRequest req 파라미터 필요)
Cookie[] cookies = req.getCookies(); // 모든 쿠키의 정보를 cookies에 저장
if(cookies != null){ // 쿠키가 한개라도 있으면 실행
	for(int i=0; i< cookies.length; i++){
		cookies[i].setPath("/");
		cookies[i].setMaxAge(0); // 유효시간을 0으로 설정
		resp.addCookie(cookies[i]); // 응답 헤더에 추가
	}
}

[자바스크립트에서 삭제]
자바스크립트팁.txt에서 참고

----------------------------------------------------------------------------------------------------

웹 스토리지(로컬 스토리지 / 세션 스토리지)

웹스토리지와 쿠키 모두 클라이언트에 정보를 저장하지만, 쿠키처럼 서버로 전송되지 않음 (꺼내서 명시적으로 전송하는건 가능)
서버에 불필요한 데이터를 저장해달라고 요청하지 않아도 된다
용량이 크다 (5MB, 브라우저마다 차이가 있음)
웹스토리지는 오리진(도메인, 프로토콜, 포트로 이루어진 식별자) 단위로 접근이 제한되는 특성 덕분에 CSRF공격으로부터 안전함
웹스토리지는 데이터를 영구적으로 저장할 수 있다. 쿠키는 만료일자가 넘으면 삭제되고 세션은 서버가 종료되거나 브라우저가 종료되면 삭제되지만,
웹스토리지의 로컬스토리지는 삭제를 할 때까지 유지할 수 있음
토큰을 발급받아서 저장하는 용도로 쓰면 좋음. 웹스토리지를 쓰면 세션을 관리했던 서버의 부담을 덜 수 있음
토큰은 "앱"과 서버가 통신 및 인증할때 가장 많이 사용된다. 왜냐면 웹에는 쿠키와 세션이 있지만 앱에서는 없기 때문


로컬 스토리지 개발자도구에서 확인 : 애플리케이션 → 저장용량 메뉴 → 로컬 스토리지 → 화살표 눌러서 url 클릭
세션 스토리지 개발자도구에서 확인 : 개발자도구 → 애플리케이션 → 저장용량 메뉴 → 세션 스토리지 → 화살표 눌러서 url 클릭

로컬/세션 스토리지는 개발자도구를 켜고 새로고침을 하면 목록이 안나오고,
개발자도구를 끈 상태에서, 새로고침을 먼저 하고, 개발자도구를 켜야만 확인이 가능함
그래도 안나오면 계속 반복

------------------------------

로컬 스토리지

브라우저를 종료해도 계속 남아있음

주로 사용하는곳 : 기간 없이 영구저장할 정보, 쿠키를 이용하지 않는 "앱" 환경에서의 자동로그인, 다크모드와 라이트모드 기능


<자바스크립트>
localStorage.setItem('key', JSON.stringfy(value)) // 저장
JSON.parse(localStorage.getItem('key')) // 조회
localStorage.removeItem('key') // 해당 키가 삭제
localStorage.clear() // 전체삭제

------------------------------

세션 스토리지

새창, 새탭의 단위로 스토리지가 생성되며, 데이터를 공유하지 않음
탭을 닫거나 브라우저를 종료하면 데이터가 사라져 "잠깐의 정보를 저장하기에 용이"함

주로 사용하는곳 : 회원가입 입력폼, 비로그인 장바구니, 일회성 로그인, 상세페이지에서 목록 페이지로 이동할 때 스크롤 위치값


<자바스크립트>
sessionStorage.setItem('key', JSON.stringfy(value)) // 저장
JSON.parse(sessionStorage.getItem('key')) // 조회
sessionStorage.removeItem('key') // 해당 키가 삭제
sessionStorage.clear() // 전체삭제

----------------------------------------------------------------------------------------------------

Token 인증

토큰 기반 인증 시스템은 클라이언트가 서버에 접속을 하면 서버에서 해당 클라이언트에게 인증되었다는 의미로 "토큰"을 부여한다
이 토큰은 "유일"하며 토큰을 발급받은 클라이언트는 또 다시 서버에 요청을 보낼때 요청 헤더에 토큰을 심어서 보낸다
그러면 서버에서는 클라이언트로부터 받은 토큰을 서버에서 제공했던 토큰과의 일치 여부를 체크하여 더이상 DB조회를 안하고도 인증 과정을 처리할 수 있게된다
또한 토큰 자체에 데이터가 들어있어서, 서버는 정보가 필요할때마다 DB조회 할 필요없이 위조여부만 확인하면 된다


토큰 방식의 단점

쿠키/세션과 다르게 토큰 자체의 데이터 길이가 길어, 인증 요청이 많아질수록 네트워크의 부하가 심해질 수 있다
Payload 자체는 암호화되지 않기 때문에 중요한 정보는 담을 수 없다
토큰을 탈취당하면 대처하기 어렵다. (따라서 사용 기간 제한을 설정하는 식으로 극복한다)

----------------------------------------------------------------------------------------------------

JWT(JSON Web Token)

인증에 필요한 정보들을 암호화시킨 JSON토큰
JWT기반인증이란? JWT토큰(Access Token)을 HTTP헤더에 실어 서버가 클라이언트를 식별하는 방식

JWT는 JSON데이터를 Base64 URL-safe Encode를 통해 인코딩하여 직렬화한것이며,
토큰 내부에는 위변조 방지를 위해 개인키를 통한 전자서명도 들어있음

따라서 사용자가 JWT를 서버로 전송하면, 서버는 검증하는 과정을 거치게 되며 검증이 완료되면 요청한 응답들을 돌려준다(DB조회가 필요없음)

※Base64 URL-safe Encode란? 일반적인 Base64 Encode에서 → URL에서 오류없이 사용하도록 '+','/' 를 각각 '-','_'로 표현한 것

------------------------------

JWT 구조

JWT . 를 구분자로 이용한 3가지 문자열의 조합이다
XXXXXX.YYYYYY.ZZZZZZ
좌측에서부터 Header, Payload, Signature를 의미함


Header : JWT에서 사용할 타입과 해시 알고리즘의 종류가 담겨있음
Payload : 서버에서 첨부한 사용자 권한 정보와 데이터가 담겨있음
Signature : Header, Payload를 Base-64 URL-safe Encode를 한 이후 Header에 명시된 해시함수를 적용하고, 개인키(Private Key)로 전자서명이 담겨있음

전자서명에는 비대칭 암호화 알고리즘을 사용하므로 암호화를 위한 키와 복호화를 위한 키다 다르다
암호화(전자서명)에는 개인키를, 복호화(검증)에는 공개키를 사용한다

-----

Header

{
	"alg": "HS256",
	"typ": "JWT"
}

alg : 서명 암호화 알고리즘(ex: HMAC SHA256, RSA)
typ : 토큰 유형

-----

Payload

{
	"jti": "1000",					// Registered Claim
	"exp": "1521430000000",		// Registered Claim
	"http://kevin.tistory.com": true,	// Public Claim
	"name": "chaewon"			// Private Claim
}

토큰에서 사용할 정보들의 조각인 Claim(클레임)이 담겨있다
클래임은 key-value형식으로 이루어진 한 쌍의 정보를 말함

클래임의 종류는 대표적으로 Registered claims, Public claims, Private claims 이렇게 3가지로 나뉜다

Registed claims : 미리 정의된 클레임
	iss : 토큰 발급자(issuer)
	sub : 토큰 제목(subject)
	aud : 토큰 대상자(audience)
	jti : JWT의 고유 식별자로서, 주로 일회용 토큰에 사용한다
	iat : 발행 시각(issued At)
	exp : 토큰의 만료시각(expiraton). 시각은 NumericDate 형식으로 되어있어야 하며,(예: 1480849147370) 항상 현재 시간보다 이후로 설정되어있어야한다.
	nbf : Not Before 를 의미하며, 토큰의 활성 날짜와 비슷한 개념. NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않는다.

Public claims : 사용자가 정의할 수 있는 클레임 공개용 정보 전달을 위해 사용

Private claims : 해당하는 당사자들간의 정보를 공유하기 위해 만들어진 사용자 지정 클레임.
	외부에 공개되도 공개되도 상관 없지만 해당 유저를 특정할 수 있는 정보를 담는다

-----

Signature

시그니처에서 사용하는 알고리즘은 헤더에서 정의한 알고리즘 방식(alg)을 활용한다
시그니처의 구조는 (헤더+페이로드)와 서버가 갖고있는 유일한 key값을 합친 것을 헤더에서 정의한 알고리즘으로 암호화를 한다

HMACSHA256(
	base64UrlEncode(header) + "." +
	base64UrlEncode(payload),
	설정할256비트비밀키
)

------------------------------

jwt 토큰 만들기

방법1. JJWT 이용
JJWT : JWT 토큰 생성 및 JWT 토큰 파싱, 검증을 해주는 라이브러리 입니다.

의존성 추가
implementation 'javax.xml.bind:jaxb-api:2.1'

Date now = new Date();

return Jwts.builder()
		.setHeaderParam(Header.TYPE, Header.JWT_TYPE) // (1)
		.setIssuer("fresh") // (2)
		.setIssuedAt(now) // (3)
		.setExpiration(new Date(now.getTime() + Duration.ofMinutes(30).toMillis())) // (4)
		.claim("id", "아이디") // (5)
		.claim("email", "ajufresh@gmail.com")
		.signWith(SignatureAlgorithm.HS256, "secret") // (6)
		.compact();

1. 헤더의 타입(typ)을 지정할 수 있습니다. jwt를 사용하기 때문에 Header.JWT_TYPE로 사용해줍니다.
2. 등록된 클레임 중, 토큰 발급자(iss)를 설정할 수 있습니다.
3. 등록된 클레임 중, 발급 시간(iat)를 설정할 수 있습니다. Date 타입만 추가가 가능합니다.
4. 등록된 클레임 중, 유효(만료) 시간(exp)을 설정할 수 있습니다. 마찬가지로 Date 타입만 추가가 가능합니다.
5. 비공개 클레임을 설정할 수 있습니다. (key-value)
6. 해싱 알고리즘과 시크릿 키를 설정할 수 있습니다.


방법2.

------------------------------

JWT 토큰이 신뢰성을 가지는 이유


JWT = A(헤더), B(페이로드), C(시그니처)
JWT가 위와 같을때, 임의의 유저가 B를 수정했다고 하면,

1. 다른유저가 B(페이로드)를 임의로 수정
유저JWT = A + B' + C

2. 임의로 수정된 토큰을 서버에 요청을 보내면 서버는 유효성 검사 시행
유저JWT는 A + B' + C 인데,
서버에서 검증 후 생성한 JWT는 A + B' + C'

따라서 대조 결과가 일치하지 않아 유저의 정보가 임의로 조작되었음을 알 수 있음

------------------------------

JWT는 서명(인증)이 목적이다

JWT는 Base64로 암호화를 하기 때문에 디버거를 사용해서 인코딩된 JWT를 1초만에 복호화할 수 있다
복호화하면 사용자의 데이터를 담은 Payload부분이 그대로 노출되어버린다. 그래서 페이로드에는 비밀번호와 같은 민감한 정보는 넣지 말아야 한다
그럼 토큰 인증 방식 자체가 빛 좋은 개살구라고 생각할 수도 있지만, 토큰의 진짜 목적은 "정보 보호"가 아닌, "위조 방지"이다
시그니처에 사용된 비밀키가 노출되지 않는 이상, 데이터를 위조해도 시그니처 부분에서 바로 걸러지기 때문이다

------------------------------

참고

https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC#Session_%EC%9D%B8%EC%A6%9D

https://velog.io/@haerong22/JWT

----------------------------------------------------------------------------------------------------

카카오 로그인

-----

프로세스

① 인가 코드 받기
1. 서비스 서버가 카카오 인증 서버로 인가 코드 받기를 요청합니다.
2. 카카오 인증 서버가 사용자에게 카카오계정 로그인을 통한 인증을 요청합니다.
3. 클라이언트에 유효한 카카오계정 세션이 있거나, 카카오톡 인앱 브라우저에서의 요청인 경우 4단계로 넘어갑니다.
4. 사용자가 카카오계정으로 로그인합니다.
5. 카카오 인증 서버가 사용자에게 동의 화면을 출력하여 인가를 위한 사용자 동의를 요청합니다.
6. 동의 화면은 서비스 애플리케이션(이하 앱)의 동의 항목 설정에 따라 구성됩니다.
7. 사용자가 필수 동의 항목, 이 외 원하는 동의 항목에 동의한 뒤 [동의하고 계속하기] 버튼을 누릅니다.
8. 카카오 인증 서버는 서비스 서버의 Redirect URI로 인가 코드를 전달합니다.

② 토큰 받기
1. 서비스 서버가 Redirect URI로 전달받은 인가 코드로 토큰 받기를 요청합니다.
2. 카카오 인증 서버가 토큰을 발급해 서비스 서버에 전달합니다.

③ 사용자 로그인 처리
1. 서비스 서버가, 발급받은 액세스 토큰으로 사용자 정보 가져오기를 요청해 사용자의 회원번호 및 정보를 조회하여 서비스 회원인지 확인합니다.
2. 서비스 회원 정보 확인 결과에 따라 서비스 로그인 또는 회원 가입 과정을 진행합니다.
3. 이 외 서비스에서 필요한 로그인 절차를 수행한 후, 카카오 로그인한 사용자의 서비스 로그인 처리를 완료합니다.

-----

선작업

1. "Kakao Developers"에 접속
먼저 애플리케이션을 추가하고,
REST API 키를 복사해놓기

2. 로그인 설정
제품 설정 →카카오 로그인 에서 활성화를 시킨 후
Redirect URI 등록 클릭 → 로그인로 넘어가는 페이지로 사용할 url 입력(http 붙여야함)

-----

구현

1. 로그인 버튼 만들기
<a href="https://kauth.kakao.com/oauth/authorize?client_id=${REST_API_KEY}&redirect_uri=${LOGIN_REDIRECT_URI}&response_type=code|">
	<img th:src="@{/images/kakao.png}" style="height:60px"/>
</a>
REST_API_KEY는 아까 내 애플리케이션 화면에서 확인했던 값을 넣으면 되고
redirect_uri는 아까 설정했던 uri을 넣으면 됨
ex)
${REST_API_KEY} = bb0a9f129dbdb7cd854df067659c7267
${REDIRECT_URI} = http://localhost:8080/member/kakao

2. 사용자가 로그인을 함

3. 해당 url로 파라미터로 인가코드가 반환되서 다시 요청되고, 이때 사용자동의 등의 정보들이 POST로 붙어서 요청됨. 이 인가코드를 이용해 토큰을 발급받을 수 있음


4. 토큰으로 사용자 정보 요청

<개인정보>
public Map<String, Object> getUserInfo(String access_token) {
	String host = "https://kapi.kakao.com/v2/user/me";
	Map<String, Object> result = new HashMap<>();
	try {
		URL url = new URL(host);

		HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
		urlConnection.setRequestProperty("Authorization", "Bearer " + access_token);
		urlConnection.setRequestMethod("GET");

		int responseCode = urlConnection.getResponseCode();
		System.out.println("responseCode1: " + responseCode);

		BufferedReader br = new BufferedReader(new InputStreamReader(urlConnection.getInputStream()));
		String line = "";
		String res = "";
		while((line = br.readLine()) != null)
			res += line;

		System.out.println("res = " + res);

		JSONParser parser = new JSONParser();
		JSONObject obj = (JSONObject) parser.parse(res);
		JSONObject kakao_account = (JSONObject) obj.get("kakao_account");
		JSONObject properties = (JSONObject) obj.get("properties");

		String id = obj.get("id").toString();
		String nickname = properties.get("nickname").toString();
		String age_range = kakao_account.get("age_range").toString();

		result.put("id", id);
		result.put("nickname", nickname);
		result.put("age_range", age_range);

		br.close();

	} catch (IOException | ParseException e) {
		e.printStackTrace();
	}

	return result;
}

<동의 여부>
public String getAgreementInfo(String access_token)
{
	String result = "";
	String host = "https://kapi.kakao.com/v2/user/scopes";
	try{
		URL url = new URL(host);
		HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
		urlConnection.setRequestMethod("GET");
		urlConnection.setRequestProperty("Authorization", "Bearer "+access_token);

		BufferedReader br = new BufferedReader(new InputStreamReader(urlConnection.getInputStream()));
		String line = "";
		while((line = br.readLine()) != null)
			result += line;

		int responseCode = urlConnection.getResponseCode();
		System.out.println("responseCode2: " + responseCode);

		br.close();

	} catch (IOException e) {
		e.printStackTrace();
	}
	return result;
}


5. 로그아웃 URL 등록하기
카카오 개발자 페이지 → 내 애플리케이션 → 제품 설정 → 카카오 로그인 → 고급 → Logout Redirect URI 등록

6. 로그아웃 버튼 만들기
<a href="https://kauth.kakao.com/oauth/logout?client_id=${REST_API_KEY}&logout_redirect_uri=${LOGOUT_REDIRECT_URI}">로그아웃</a>

-----

주의사항

인가 코드로 토큰 요청시 같은 인가코드로는 딱 한번만 요청이 가능함

만약 버튼을 눌러서 로그인하지 않고,
한번 보냈던 인가코드로 재요청하면 200이 아닌 400, 401이 반환됨

-----

참고

1. https://velog.io/@dktlsk6/Spring%EC%9C%BC%EB%A1%9C-%EC%B9%B4%EC%B9%B4%EC%98%A4-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0
2. https://suyeoniii.tistory.com/79
3. https://developers.kakao.com/docs/latest/ko/kakaologin/rest-api#request-token

----------------------------------------------------------------------------------------------------

ModelAndView 객체 사용법

// 데이터와 뷰를 동시에 설정이 가능
ModelAndView mv = new ModelAndView();
mv.setViewName("/board/content");// 뷰의 이름
mv.addObject("data", "12341234"); // 뷰로 보낼 데이터 값

----------------------------------------------------------------------------------------------------

경로에 redirect: 를 쓴것과 안쓴것 차이

redirect:가 붙지 않으면 무조건 InternalResourceViewResolver가 설정한 prefix와 suffix 정보가 적용된 .jsp 파일을 찾고, 
redirect:가 붙으면 InternalResourceViewResolver 설정 정보는 무시되고 Context path 위치에서 .jsp 파일을 찾는다. (동적이 되는듯)


ModelAndView.setViewName("/member/login"); 또는
ModelAndView.setViewName("member/login"); 이렇게 하면
/WEB-INF/views/member/login.jsp 를 찾는다


ModelAndView.setViewName("redirect:/member/login"); 이렇게 하면 
/WEB-INF/views/member/login.jsp 를 찾는다

ModelAndView.setViewName("redirect:list"); 이렇게 하면
컨트롤러 클래스선언부에 @RequestMapping("/member") 설정한 경로 밑으로 간다
/WEB-INF/views/member/list.jsp 를 찾는다

루트로 가려면
redirect:/ 이나 /home 이나 home 이렇게 써야됨

----------------------------------------------------------------------------------------------------

ajax 활용법 추가 (자세한 사용법은 servlet/jsp.txt참고)

아이디 중복체크만들때
function idDuplChk() {
	var formData = "chkID="+tmpID.trim();
	

	$.ajax({
		type:'post',
		async: false ,
		url:'/member/list',
		data:formData,
		success:function(asd){
			if (asd === 1){
				idCheckOk(tmpID);
				$('#span_chkID').css({ "color":"blue" }).html('사용 가능한 ID 입니다.');
			}else{
				f.id.value = "";
				$('#span_chkID').css({ "color":"red" }).html('사용 불가능한 아이디 입니다.');
			}
		}
	});
	
}

----------------------------------------------------------------------------------------------------

ajax로 보낸값을 컨트롤러에서 받기

@PostMapping("/getByID")
@ResponseBody
public void getByID(@RequestBody String id){
	log.info("id: " + id);
}

컨트롤러에서 ajax로 응답하기 → @RequestBody, return자료형, return 이용,
pom.xml에서 자바객체↔json간 변환해주는 잭슨 dependency추가
추가 안하면 String자료형 제외하고 int,List,Map,VO등 모두 ajax500에러 (int는 될 때가 있고 안될 때가 있음)
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.10.0.pr3</version>
</dependency>
↓↓↓

컨트롤러에서 ajax로 응답 - List (@ResponseBody를 리턴타입 앞에다 써도 됨)
<VO>

<컨트롤러>
@RequestMapping(value="/register.do", method=RequestMethod.POST)
@ResponseBody 
public List<FruitVO> returnListVO() throws Exception {
	/* logger.info("과일: " + fruit.getName() + " 가격: "+ fruit.getPrice()); */
	
	List<FruitVO> list = new ArrayList<FruitVO>();
	
	list.add(new FruitVO(4000, "단감", "홍시보단 단감"));
	list.add(new FruitVO(1000, "포도", "달고 맛있는 포도"));
	list.add(new FruitVO(2000, "복숭아", "복숭아는 말랑복숭아"));
	
	return list;
}
<ajax>
function request(){
	$.ajax({
		url: "./register.do",
		type: "POST", 
		success : function(data){
			$(data).each(function(){
				alert(this.price + " " + this.name + " " + this.introduce);
				});
			},
		error :function(){
			alert("request error!");
			}
	});
}

컨트롤러에서 ajax로 응답 - Map (@ResponseBody를 리턴타입 앞에다 써도 됨)
<컨트롤러>
@RequestMapping(value="/getByID", method=RequestMethod.POST)
@ResponseBody
public Map<String,String> getByID(){
	Map<String,String> map = new HashMap<String,String>();
	map.put("a","aaa");
	map.put("b","bbb");
	return map;
}
<ajax>
$.ajax({
	type:'post',
	async: false ,
	url:'/member/getByID',
	//data:chkID.trim(),
	success:function(data){
		console.log(data);
		console.log(data.a);
		console.log(data.b);
	}
});

----------------------------------------------------------------------------------------------------

암호화 (DB가 뚫렸을때를 위해 보안, BCrypt 해싱 함수를 이용)
추가후 BCryptPasswordEncoder encoder = new BCryptPasswordEncoder(); 이용 가능

아래 dependency 추가

<!-- security -->
<!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-core -->
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-core</artifactId>
	<version>5.4.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-web -->
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-web</artifactId>
	<version>5.4.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-config -->
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-config</artifactId>
	<version>5.4.2</version>
</dependency>

----------------------------------------------------------------------------------------------------

절대경로 상대경로 (servlet-context.xml에 루트 설정하는부분있음)

(자바컨트롤러)
Mapping("")의 기본경로 /views/
@RequestMapping("/member") 로 절대경로루트 설정가능
상대경로는 쓸일도 없고 쓸수도없는듯

(jsp - include절)
절대경로 : <%@ include file="/asd" %> → src/main/webapp/asd
상대경로 : <%@ include file="./" %> → 현재 jsp페이지가 있는 폴더내 ("./" 또는 "")
상대경로 : <%@ include file="../" %> → 현재 jsp페이지가 있는 폴더의 상위폴더내

(jsp - html/css부)
절대경로 : <img src="/" & background:url("/" → src/main/webapp/
상대경로(X) : ../ 나 ./ 를 한번이라도 쓰면 webapp/으로 점프함 이때는 ../ 'resources/'도 써줘야함

참고로 css/images파일은 resources에 넣어야지 WEB-INF에 넣으면 html/css에서는 참조가 안되서 404에러남

-----

회사

어드민 루트(/) → ~/webapp/
css 루트(/) → ~/resources/

----------------------------------------------------------------------------------------------------

전 페이지의 경로
req.getHeader("REFERER")

이동
String referer = req.getHeader("REFERER");
return "redirect:" + referer;

----------------------------------------------------------------------------------------------------

자동로그인 구현

<컨트롤러>
@PostMapping(value="/login", produces="application/text; charset=UTF-8")
@ResponseBody
public String login_ok(MemberVO vo, HttpServletRequest req, HttpServletResponse resp){
	HttpSession session = req.getSession(); //세션 불러오기
	MemberVO mem = service.login(vo);
	int fail = service.login_pw_fail(vo);
	
	if(mem != null && fail == 0) { // 로그인 성공
		
		// 세션에 회원정보 저장
		session.setAttribute("loginInfo", mem);
		
		// 자동로그인 체크시 처리
		if(vo.isAutoLogin()) {
			Cookie loginCookie = new Cookie("loginCookie", session.getId()); //쿠키 생성. 세션id를 담음
			loginCookie.setPath("/"); //쿠키를 조회 가능한 위치
			loginCookie.setMaxAge(60 * 60 * 24 * 90); //초단위로 쿠키유지기간 설정 (90일)
			resp.addCookie(loginCookie); //response에 쿠키를담아 클라이언트에게 보낸다
			
			vo.setSESSION_ID(session.getId()); //세션id를 vo에 담는다
			int test = service.setSessionKey(vo); //세션id를 db에 update한다
		}
	}else if(fail == 1) { // 비밀번호 틀림
		return "pwfail";
	}else{ // 아이디 틀림
		return "idfail";
	}
	
	return null;
	
}

<xml>
<select id="login" resultType="com.fitper.domain.MemberVO">
	select * from MEMBER_TL where ID = #{ID} and PW = #{PW}
</select>

<select id="login_pw_fail" resultType="int">
	select count(*) from MEMBER_TL where ID = #{ID} and PW != #{PW}
</select>

<클라이언트>
var data = $(document.Frm).serialize();
$.ajax({
	type : "POST",
	async : false ,
	data : data ,
	url  : "/member/login",
	success : function(data) {
		if(data == "pwfail"){
			$('#loginCheck').html("아이디/비밀번호를 확인해주세요.");
		}else if(data == "idfail"){
			$('#loginCheck').html("등록된 정보가 없습니다.");
		}else{ // 로그인 성공
			if(window.location.pathname != "/member/login"){ // 로그인이필요한 페이지를 들어가서 컨트롤러가 튕겨낸경우
				window.location.replace(window.location.href); // 이전페이지로 이동
			}else{ // 로그인이 필요없는 페이지 또는 메인에서 온경우
				window.location.replace(document.referrer); // 이전페이지(현재페이지에 저장된 url)로 이동
			}
		}
	},
	error:function(request,status,error){
		console.log("code:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error);
	}
});

----------------------------------------------------------------------------------------------------

로그아웃

@GetMapping("/logout")
public String logout(HttpServletRequest req,HttpServletResponse resp) {
	HttpSession session = req.getSession();
	session.removeAttribute("loginInfo"); // 로그인세션 삭제
	
	Cookie cookic = new Cookie("loginCookie", null); // choiceCookieName(쿠키 이름)에 대한 값을 null로 지정
	cookic.setPath("/");
	cookic.setMaxAge(0); // 유효시간을 0으로 설정
	resp.addCookie(cookic); // 응답 헤더에 추가해서 없어지도록 함
	
	String referer = req.getHeader("Referer"); // 헤더에서 이전 페이지를 읽는다.
	return "redirect:"+ referer; // 이전 페이지로 리다이렉트
}

----------------------------------------------------------------------------------------------------

자료형 확인
.getClass().getName()

session.getAttribute("loginInfo")).getClass().getName();

----------------------------------------------------------------------------------------------------

ajax로 리스트 넘겨받아 DB에 저장

방법1. form태그 안에 input-hidden으로 받기
방법2. 구분자가있는 문자열로 받기

[input으로 받는 방법]
<클라이언트>
$("#save").click(function(){
	var f = document.Frm;
	var datas = calendar.getEvents();

	// name은 VO의 List객체변수명과 같아야함
	for (var i = 0; i < datas.length; i++) {
		$(f).append('<input type="hidden" name="list[' + i + '].title" value="' + datas[i].title + '">');
		$(f).append('<input type="hidden" name="list[' + i + '].start" value="' + datas[i].start + '">');
		$(f).append('<input type="hidden" name="list[' + i + '].end" value="' + datas[i].end + '">');
	}
	$.ajax({
		type:"POST",
		url:"/my/daily_info?method=save",
		data:$(f).serialize(),
		async:false,
		success:function(data){
			console.log(data);
			if(data){
				alert("저장을 완료했습니다.")
			}
		},
		error:function(a,b,c){
			console.log(a,b,c);
		}
	});
});

<VO>
@Data
public class CalendarVO {
	private String title;
	private String start;
	private String end;
	
	private List<CalendarVO> list;
}

<컨트롤러>
@PostMapping(value="daily_info", params="method=save")
@ResponseBody
public int save(CalendarVO list) {
	log.info("daily_info?method=save,,,,,");
	log.info(list);
	log.info(list.getList());
	
	return service.setCalendarList(list.getList());
}

<Mapper(DAO)>
int setCalendarList(List<CalendarVO> list);

<MyBatis> (다중Insert → update태그와 foreach태그 이용)
<update id="setCalendarList" parameterType="java.util.List">
	<foreach collection="list" item="item" index="index" separator=" " open="INSERT ALL" close="SELECT * FROM DUAL">
	INTO F_CALENDAR_TL(id, MEMBER_SQ, title, start1, end1, allDay, textColor, backgroundColor, borderColor) 
	values(
		F_CALENDAR_SQ.nextval,
		#{item.MEMBER_SQ},
		#{item.title},
		to_date(#{item.start},'YYYY/MM/DD"T"hh24:mi:ss'), 
		to_date(#{item.end},'YYYY/MM/DD"T"hh24:mi:ss'),
		#{item.allDay},
		'orange',
		'skyblue',
		'hotpink'
	)
	</foreach>
</update>

시퀀스가 같은번호로 들어가는 문제때문에 아래 코드로 수정 ↓
<update id="setCalendarList" parameterType="java.util.List">
	INSERT INTO F_CALENDAR_TL(id, MEMBER_SQ, title, start1, end1, allDay, textColor, backgroundColor, borderColor) 
	SELECT F_CALENDAR_SQ.NEXTVAL, A.* FROM(
		<foreach collection="list" item="item" index="index" separator="UNION ALL ">
		SELECT
			#{item.MEMBER_SQ} AS MEMBER_SQ,
			#{item.title} AS title,
			to_date(#{item.start},'YYYY/MM/DD"T"hh24:mi:ss') AS start1, 
			to_date(#{item.end},'YYYY/MM/DD"T"hh24:mi:ss') AS end1,
			#{item.allDay} AS allDay,
			'orange' AS textColor,
			'skyblue' AS backgroundColor,
			'hotpink' AS borderColor
		FROM DUAL
		</foreach>
	) A
</update>

------------------------------

아래처럼도 가능

INSERT INTO DETAIL_INFO
        (
            COT_ID,
            FLD_GUBUN,
            DISPLAY_TITLE,
            CONTENT_BODY,
            SERIAL_NUM
        ) VALUES
        <foreach item="item" collection="list" separator=",">
            (
                #{item.cotid},
                #{item.fldgubun},
                #{item.displaytitle},
                #{item.contentbody},
                #{item.serialnum}
            )
        </foreach>

이 SQL 문장은 MyBatis 프레임워크를 사용하여 "DETAIL_INFO" 테이블에 여러 개의 데이터 행을 삽입하는데 사용됩니다.

이 문장은 MyBatis의 foreach 구문을 사용하여 리스트 컬렉션에 있는 각 아이템을 순회하며 여러 개의 행을 삽입합니다.
각각의 행은 COT_ID, FLD_GUBUN, DISPLAY_TITLE, CONTENT_BODY, SERIAL_NUM 열에 대응되는 값들을 갖고 있습니다.
이 값들은 #{item.cotid}, #{item.fldgubun}, #{item.displaytitle}, #{item.contentbody}, #{item.serialnum} 매개변수를 사용하여
MyBatis 매퍼 XML 파일에서 동적으로 지정됩니다.

즉, 이 SQL 문장은 MyBatis 매퍼 XML 파일에서 리스트 컬렉션을 파라미터로 받아, 리스트의 각 아이템을 DETAIL_INFO 테이블에 여러 개의 데이터 행으로 삽입합니다.

----------------------------------------------------------------------------------------------------

트랜잭션

root-context.xml에서

맨 꼭대기에 beans 속성으로

1. xsi:schemaLocation="~ 부분에 아래 내용 추가
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx-3.0.xsd

2. xmlns:tx="http://www.springframework.org/schema/tx" 추가

3. 맨 아래에 아래내용 추가

<!-- 트랜젝션 매니저 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
	<property name="dataSource" ref="dataSource"></property>
</bean>

<!-- @Transactional 애노테이션을 sacn하기 위한 설정 -->
<tx:annotation-driven/>

-----

이후 ServiceImpl (서비스 구현부)에서 (컨트롤러X)
트랜잭션을 쓸 메소드에 @Transactional 어노테이션만 추가하면 됨

delete&insert / delete&delete 등에 이용

★스프링부트에서는 위 설정들이 필요없고 어노테이션만 걸면됨

----------------------------------------------------------------------------------------------------

object형을 Long으로 바꾸려면 아래와 같이 String.valueOf과 Integer.parseInt로 감싸야함

Integer.parseInt(String.valueOf(

Integer.parseInt(String.valueOf(part.get("EXR_PART_SQ"))) == 10

----------------------------------------------------------------------------------------------------

시퀀스. 되도록 숫자는 Map의 key로 쓰지 말기
el로 값이 안꺼내지는듯 ex) ${map.1}

----------------------------------------------------------------------------------------------------

mybatis에서 resultType/parameterType 쓸때 컬렉션 말고 사용자클래스도 패키지명안붙이고 쓰는법

src/main/webapp/WEB-INF/spring/root-context.xml 에서
sqlSessionFactory 콩(bean) 부분에

<property name="typeAliasesPackage" value="kr.or.first"></property> 패키지 넣어서 추가하면
사용자클래스명을 별칭으로 쓸 수 있다 (첫글자 소문자로 써야됨)

----------------------------------------------------------------------------------------------------

myBatis의 resultMap

수동으로 맵핑(연결)해주는 역할. resultType대신 resultMap을 쓰면

1. 계층형 프로그래밍이 가능해짐
2. DB컬럼명과 다른 이름으로 변수를 매핑해서 쓸 수 있음

<result>와 <id>는 동일.
property가 DTO, column이 DB컬럼
<result> 태그에는 기존 resultType쓸때처럼 속성들을 넣으면 됨
property 속성에는 vo의 필드명 넣고
column 속성에는 가져온 컬럼명 넣기

<association> 태그는 또다른 resultMap을 불러올때 씀


ex) 2개의 날짜데이터는 사용자 클래스에 담아 계층형으로 만들기

<resultMap type="contentVO" id="contentVOMap">
	<id property="id" column="COT_ID" />
	<result property="CONTENT_ID" column="CONTENT_ID" />
	<result property="TITLE22" column="TITLE" />
	<result property="READ_COUNT" column="READ_COUNT" />
	<result property="IMG_ID" column="IMG_ID" />
	<result property="ADDR1" column="CONTENT_ID" />
	<result property="TAG_LIST" column="CONTENT_ID" />
	<association property="event_date" resultMap="eventDateMap" />
</resultMap>

<resultMap type="eventDate" id="eventDateMap">
	<result property="EVENT_START_DATE" column="EVENT_START_DATE" />
	<result property="EVENT_END_DATE" column="EVENT_END_DATE" />
</resultMap>

<select id="getList" resultMap="contentVOMap" parameterType="criteria">
	SELECT
		CM.COT_ID, 
		CM.CONTENT_ID,
	    CM.TITLE,
	    CM.READ_COUNT,
	    DM.FIRST_IMAGE AS IMG_ID,
	    DM.ADDR1,
	    FI.EVENT_START_DATE,
	    FI.EVENT_END_DATE,
	    group_concat(t.TAG_NAME SEPARATOR ',') AS TAG_LIST
	FROM CONTENT_MASTER CM
	INNER JOIN DATABASE_MASTER DM
		ON CM.COT_ID = DM.COT_ID
	INNER JOIN FESTIVAL_INTRO FI
		ON DM.COT_ID = FI.COT_ID
	LEFT OUTER JOIN CONTENT_TAGS ct 
		ON ct.COT_ID = CM.COT_ID
	LEFT OUTER JOIN TAGS t 
		ON t.TAG_ID = ct.TAG_ID 
	<if test="ageLim != ''">
		WHERE FI.AGE_LIMIT = #{ageLimit}
	</if>
	GROUP BY CM.COT_ID
	LIMIT #{offset} , #{amount};
</select>

-----

ex2) Member필드중 Address클래스로 또 여러 필드가 있는 상황에서
	컬럼들을 이름 바꾸고, 하위컬럼인 주소까지 select해올때

<select id="findAll" resultMap="memberMap">
	SELECT *
	FROM MEMBER_TL M
	INNER JOIN STANDARD_REGION_CODE R
	ON M.ADDRESS_ID = R.COD_ID
</select>

<resultMap type="Member" id="memberMap">
	<id property="memberID" column="MEMBER_ID" />
	<result property="email" column="EMAIL" />
	<result property="nickname" column="NICKNAME" />
	<result property="password" column="PASSWORD" />
	<result property="gender" column="GENDER" />
	<association property="address" resultMap="addressMap" />
</resultMap>
<resultMap type="Address" id="addressMap">
	<result property="codID" column="COD_ID" />
	<result property="regionCD" column="REGION_CD" />
	<result property="sigunguCD" column="SIGUNGU_CD" />
	<result property="umdCD" column="UMD_CD" />
	<result property="fullname" column="FULLNAME" />
</resultMap>

----------------------------------------------------------------------------------------------------

vo 필드 자료형으로 다른 vo를 또 쓸때 (계층형vo)

@Getter
@Setter
@ToString
@RequiredArgsConstructor
public class Member {
	
	private Long memberID;
	private String email;
	private String nickname;
	private String password;
	private char gender;
	private Address address;
	
}

and.....

@Getter
@Setter
@ToString
@AllArgsConstructor
public class Address {
	private String codID;
	private String regionCD;
	private String sigunguCD;
	private String umdCD;
	private String fullname;
}

-----

출력
vo.getAddress().getRegionCD()

입력
vo.getAddress().setRegionCD()

-----

mybatis로 insert 시킬때 .(점)으로 연결 (컨트롤러에서 json계층형으로 받을때 그냥 상위객체(vo)로 받으면됨)

<insert id="insert" parameterType="Member">
	INSERT INTO MEMBER_TL(EMAIL,NICKNAME,ADDRESS_ID,PASSWORD,GENDER)
	values(#{email}, #{nickname}, #{address.codID}, #{password}, #{gender});
</insert>

----------------------------------------------------------------------------------------------------

이클립스 패키지를 트리 형태로 보기

Project Explorer → View Menu(세로로 점 3개 아이콘 or 화살표) 클릭 → Package Presentation → Hierarchical

----------------------------------------------------------------------------------------------------

안쓰는 프로젝트 닫기 (quick search 등에 안나옴)

프로젝트폴더 우클릭 → Close Project

----------------------------------------------------------------------------------------------------

컨트롤러에서 URL파라미터를 받는 방법은 두가지가 있음

1. /member?seq=value1
2. /member/{value1}

-----

1번으로 받을때는 그냥 받으면 되고

@GetMapping("member")
public ResponseEntity<Member> get(Long id){
	return ResponseEntity.ok(memberService.fetch(id));
}

-----

2번으로 받을때는

① 어노테이션에 {/{변수명}} 을 추가하고
② @PathVariable를 추가하면된다

@GetMapping("/member/{id}")
public ResponseEntity<Member> get(@PathVariable Long id){
	return ResponseEntity.ok(memberService.fetch(id));
}

-----

다른 변수명을 쓰고싶으면 아래처럼 하면 된다
@GetMapping("/member/{id2}")
public ResponseEntity<Member> get(@PathVariable("id2")Long id){
	return ResponseEntity.ok(memberService.fetch(id));
}

-----

받을때, 값이 없을경우 다른 값을 넣어주고 싶으면

① Request/Get/Post Mapping쪽에{} 넣어주고 변수를 뺀 나머지를 쓴다 ("/")
② required = false를 넣는다

@GetMapping({"/{id2}", "/"})
public ResponseEntity<Member> get(@PathVariable(value = "id2", required = false) Long id){
	System.out.println(1111);
	id = id == null ? 1 : id;
	return ResponseEntity.ok(memberService.fetch(id));
}

----------------------------------------------------------------------------------------------------

 Controller
    - 역할 : 응답 양식과 요청 양식에 대한 정보

- Service
    - 역할 : 기능의 요구사항을 수행한다.

- Repository(Mapper) - 데이터베이스 접근 객체 (DAO)
    - 역할 : 데이터베이스로부터 필요한 데이터를 요청한다.
    - *** sql문이 수행하려하는 일에 대해서만 신경을 쓰자***

----------------------------------------------------------------------------------------------------

백엔드 테스트해주는 프로그램 : Postman

GET 방식 / POST방식 어떤방식으로 보낼지 선택할 수 있음

-----

http header에 내용을 담아야할때는
Header탭에서 입력하면 됨.

항목에 입력한 글자가 url쪽에 url파라미터로 중복으로 붙는 경우가 있는데
ex) https://korean.visitkorea.or.kr/api/v1/trss/lottery?x=xxx
(?x=xxx 부분)

GET요청할때는 상관없지만 POST요청시에는 저걸 꼭 제거해야함.
근데 제거하면 아래 항목에 입력해놓은게 사라지는데,
'잘' 해서 아래 항목에입력해놓은건 남기고 url에 붙은파라미터는 제거해야함

-----

json형으로 데이터를 보낼경우

POST 선택하고 Body탭에서 raw선택, JSON 선택 후 { } 로 감싸진 JSON데이터를 보내면 되는데 key를 ""(따옴표)로 반드시 감싸야함)
{
    "email": "w@w.com",
    "nickname": "nick",
    "size": 10,
    "gender":"M",
    "address": {
        "FULLNAME": "세종특별자치시 소정면 소정리"
    }
}
★★★★★이때 첫번째와 두번째 문자가 "대문자"가 들어간 키를 JSON포맷으로 보낼시, 받을때 값이 제대로 들어가지 않아 출력시 null이 나온다.
이는 Jackson과 관련이 있는데, Jackson이 Json Key를 변환하는데는 일정한 규칙이 있다. 
이때문에 DTO를 스네이크표기법이 아닌 카멜 표기법으로 써야하고, 가령 aCount 이런 2번째에 대문자가 들어가는 변수는 쓰면 안됨

위와 같은 방식으로 보내면 되고 보내기전에
1. POST를 선택
2. form-data 말고 raw→JSON을 선택

그래야 아래와 같은 415오류 없이 받을 수 있음
Resolved [org.springframework.web.HttpMediaTypeNotSupportedException: Content type 'multipart/form-data;boundary=--------------------------772957839711001273062249' not supported]

만약 아래와 같은 오류가 난다면 받은 데이터가 없는것
Resolved [org.springframework.web.HttpMediaTypeNotSupportedException: Content type '' not supported]

받는곳에서는 아래처럼 받기 (GETMapping/POSTMapping 올바른지 확인하기)
@PostMapping(value="join/join_ok", consumes=MediaType.APPLICATION_JSON_VALUE, produces="application/json;charset=utf-8")
public void asd(@RequestBody Member vo){
}

파라미터에 @RequestBody 안넣으면 map으로 값 안 받아짐 (null나옴)
반대로 @RequestBody 를 넣으면 VO로 값 안받아짐 (null나옴)

----------------------------------------------------------------------------------------------------

REST / REST API 란

브라우저에서 봐도 해당 기능이 무슨 기능인지 짐작할 수 있도록
POST / GET / PUT / DELETE 4가지로 CRUD를 구현하는것

PUT - 수정 (POST방식)
DELETE - 삭제 (GET방식)

----------------------------------------------------------------------------------------------------

컨트롤러/서비스/매퍼/xml들을 잠깐 주석하고싶을때 xml은 전체를 주석하면 실행오류가 남.

xml파일은 태그들만 주석하고 맨위에있는 내용들은 남겨놔야함

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.secondproject.repository.StatisticsMapper">

----------------------------------------------------------------------------------------------------

mybatis에서 select쿼리 쓸때 alius과 resultMap을 썼으면 resultMap으로 같은 이름으로 매핑한번 해야함 (안그럼 0이나 null 나옴)

<result property="commentCnt" column="commentCnt"/>
<result property="bookmarkCnt" column="bookmarkCnt"/>

----------------------------------------------------------------------------------------------------

정적 팩토리 메소드

<컨트롤러>
@GetMapping(value="sign-up/check-email")
public ResponseEntity<Map<String,Object>> emailDuplicateCheck(String email) {
	Map<String,Object> map = new HashMap<>();

	map.put("code", 200);
	map.put("data", memberService.emailDuplicateCheck(email));
	map.put("message", "성공");

	return ResponseEntity.ok(map);
}

↓↓↓↓↓

<enum - ResponseCode>
@Getter
@RequiredArgsConstructor
public enum ResponseCode {
	CODE_200(200, "성공");

	private final int code;
	private final String message;
}

<ApiResponse>
@Getter
@Setter
@ToString
@NoArgsConstructor(access = AccessLevel.PRIVATE)
@AllArgsConstructor(access = AccessLevel.PRIVATE)
@Builder
@JsonInclude(value = Include.NON_NULL)
public class ApiResponse<T> {
	private int code;
	private String message;
	private T data;

	/**
	 * {
	 * 	"code": 200,
	 * 	"message": "성공",
	 * 	"data": {data}
	 * }
	 */
	public static <T> ApiResponse<T> valueOf(T data) {
		return of(ResponseCode.CODE_200, data);
	}

	/**
	 * {
	 * 	"code": 200,
	 * 	"message": "성공"
	 * }
	 */
	public static <T> ApiResponse<T> success(){
		return of(ResponseCode.CODE_200, null);
	}

	/**
	 * static factory method (정적 팩토리 메소드)
	 */
	public static <T> ApiResponse<T> of(ResponseCode responseCode, T data) {
		return new ApiResponse<>(responseCode.getCode(), responseCode.getMessage(), data);
	}

}

<컨트롤러>
@GetMapping(value="sign-up/check-email")
public ResponseEntity<ApiResponse<Boolean>> emailDuplicateCheck(String email) {
	return ResponseEntity.ok(
			ApiResponse.valueOf(memberService.emailDuplicateCheck(email))
	);
}

static 메소드를 쓸때는 반환타입 앞쪽에 <T> 를 붙여줘야함 (그게 문법임)

----------------------------------------------------------------------------------------------------

jsp페이지로 넘겨주는 자바파일을 찾는 방법

브라우저에서 개발자도구(f12) 열기 → 페이지 새로고침(ctrl+r) → Network탭

그럼 페이지로 받은 모든 데이터들을 확인할 수 있는데
ALL / Fetch/XHR / JS / CSS / IMG / Media / Font / Doc / WS / Wasm / Manifest / Other
위의 탭에서 Fetch/XHR 에서, 혹은 Doc 탭을 누르면 자바파일과 관련된 목록들이 나오고 그 항목을 클릭하면 Request URL이 나옴
그걸로 이클립스에서 파일검색/퀵서치 하면됨

----------------------------------------------------------------------------------------------------

공용api 불러오기

팁 - 회사&기타 참조

----------------------------------------------------------------------------------------------------

PC / 모바일 체크

서비스메소드(){
	HttpServletRequest request = this.getRequest();
	params.put("deviceType",isMobile(request)? "M":"P");
}

public boolean isMobile(HttpServletRequest req) {
    String header = req.getHeader("user-agent").toUpperCase();
    String[] mobileos = {"IPHONE","IPOD","ANDROID","BLACKBERRY","WINDOWS CE","NOKIA","WEBOS","OPERA MINI","SONYERICSSON","OPERA MOBI","IEMOBILE"};
    for(int i=0 ; i<mobileos.length ; i++) {
    	if(header.indexOf(mobileos[i]) > -1 ){
    		return true;
    	}
    }
    return false;
}

----------------------------------------------------------------------------------------------------

mybatis의 if문

단일조건일 경우 씀

<if test = "조건식">
	내용
</if>

------------------------------

mybatis의 choose when

조건이 여러개일경우 씀
자바의 swtich문과 비슷

<choose>
	<when test="조건식1"> 내용 </when>
    	<when test="조건식2"> 내용 </when>
    	<when test="조건식3"> 내용 </when>
	<otherwise> 내용 </otherwise> // else절 내용은 여기
</choose>

★만약 여러 조건에 해당될경우는 첫번째 when의 내용이 들어감

------------------------------

<foreach> 태그

<foreach collection="sortArr" item="type" open="ORDER BY " separator=",">
	${type}
	<if test="type == 1"> // if문 안에서도 변수 이용 가능
	</if>
</foreach>

1) collection 속성 - 전달받은 인자를 속성값으로 삽입합니다. Map, Array, List, Set, JSONArray 등과 같은 반복 가능한 객체를 전달할 수 있음(받은 변수명을 넣어야함)
2) item 속성 - collection속성에서 전달받은 collection 인자값을 대체할 '이름'을 속성 값으로 삽입
3) open 속성 - 구문이 시작될때 삽입할 문자열을 속성 값으로 삽입
4) close 속성 - 구문이 종료될때 삽입할 문자열을 속성 값으로 삽입
5) separator 속성 - 반복되는 구문 사이에 삽입할 문자열을 속성값으로 삽입
6) index 속성 - index값을 부를 일종의 변수명을 속성값으로 삽입. 태그 내에 #{index}를 통해 호출할 때 0부터 반환됨

------------------------------

<trim> 태그

<trim prefix="WHERE" prefixOverrides="AND | OR ">
</trim>

내부에 컨텐츠가 존재할 때 prefix/suffix안의 키워드를 앞/뒤에 포함시킴
prefixOverrides/suffixOverrides는 시작/끝부분에 특정문자열이(AND/OR/,등) 들어갈 경우 문자열을 삭제 시킨다.

------------------------------

<where> 태그

<where>
</where>

내부에 컨텐츠가 존재할 때만 where 키워드를 포함

------------------------------

<set> 태그

<set>
</set>

내부에 컨텐츠가 존재할 때만 set 키워드를 포함

------------------------------

<bind> 태그

변수를 만들어서 쓸 수 있음

<select id="selectPerson" parameterType="String" resultType="hashmap">
  SELECT * FROM PERSON WHERE FIRST_NAME like #{name.upperCase() + '%'} 
</select> 
↓↓↓
<select id="selectPerson" parameterType="String" resultType="hashmap">
  <bind name="nameStartsWith" value="_parameter.getName().upperCase() + '%'"/>
  SELECT * FROM PERSON WHERE FIRST_NAME like #{nameStartsWith} 
</select>

------------------------------

자세한 설명은 아래 참고
https://atoz-develop.tistory.com/entry/MyBatis-%EB%8F%99%EC%A0%81-SQL-choose%EC%99%80-set%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EB%8F%99%EC%A0%81-SQL-%EB%A7%8C%EB%93%A4%EA%B8%B0

----------------------------------------------------------------------------------------------------

mybatis에서 XML쿼리에 값을 전달할때 2가지 방법이 있는데

1. select count(*) from MEMBER_TL where ID = #{id}
2. select count(*) from MEMBER_TL where ID = '${id}'

1번은 사용자의 입력을 전달할때 sql주입공격 예방하기위해 쓰고
2번은 ' '(따옴표)가 붙지않아서 테이블명이나 컬럼명을 전달할때도 쓸 수 있음

------------------------------

myvatis 파라미터 받을때 파라미터값이 제대로 받아졌는지 확인하는법

<select id="getProbabilityWinningDate" resultType="map">
	#{tnmId}
	SELECT
		*
	FROM TRSS_LOTTERY_CHANCE
	WHERE LT_APLCN_YMD = #{date}
		AND TNM_ID = #{tnmId}
</select>

이런식으로 #{tnmId} 이렇게 맨 위에다가 쓰기. 그럼 오류메시지로 파라미터로 받은값이 출력됨

------------------------------

mybatis 파라미터 받을때


1. Map/VO로 받을때
key만 쓰면 getter가 자동으로 호출됨

ex)
#{type}
<when test='type.equals("R")'>"추천"</when>


2. Map/VO로 안받고 String한개 받을때

변수명은 _parameter로 쓰면 됨
ex)
#{_parameter}
<when test='_parameter.equals("R")'>"추천"</when>

_parameter로 안하고 이름 아무거나 쓰면
There is no getter for property named 'asd' in 'class java.lang.String 에러발생할 수 있음

------------------------------

파라미터 Map으로 받을때 key가 없으면 null이 들어감

-----

#{asdf}

<update id="userUpdate" parameterType="hashMap">
	UPDATE		STAFF	SET
		AC_TYPE_CD = #{acTypeCd},

acTypeCd가 없을경우 AC_TYPE_CD 컬럼은 null로 업데이트됨

-----

key가 없을때 아무동작도 안되게 하려면 아래처럼 if문을 쓰기

<update id="userUpdate" parameterType="hashMap">
	UPDATE		STAFF	SET
	<if test="acTypeCd != null">
		AC_TYPE_CD = #{acTypeCd},

------------------------------

mybatis에서 한글자 eq 비교시 .toString() 붙이거나, 작은따옴표('')말고 큰따옴표("")로 처리해야함


<if test="sortArr!=null and sortArr[0] == 'R'.toString()">
이렇게

안붙이면 제대로 인식하지 못함


또는 따옴표 위치를 바꾸기
<if test="item.TYPE eq 'L'">
↓
<if test='item.TYPE eq "L"'>

------------------------------

mybatis 문자열 비교시 따옴표 주의

문자열은 되도록 큰따옴표("")로 처리하기


<if test="userId == 'hong'"> 이렇게 작은따옴표('')쓰면 NumberFormatException 에러남

싱글쿼테이션과 더블쿼테이션을 잘 보자. ""는 문자열이고 ''는 문자이다.

equals로 비교할 때에는 ''으로 처리할 경우 비교대상 문자가 한글자이면 비교되지 않지만 두글자 이상이면 싱글쿼테이션으로도
비교가 가능하다.

equalsIgnoreCase는 대소문자 비교뿐만 아니라 ''만으로도 문자열 비교가 된다. 단 비교할 문자를 먼저 쓴 경우에는 에러

<if test='userId.equals("hong")'>  (O)
<if test='userId == "hong"'>  (O)
<if test="userId == 'hong'">  (Error)
<if tset='userId == "h"'>  (O)
<if test="'hong'.equals(userId)">  (O)
<if test="'h'.equals(userId)'>  (X)
<if test="userId.equals('h')">  (X)
<if test="userId == 'hong'.toString()>  (O)
<if test="userId eq 'hong'.toString()>  (O)
<if test="userId.equalsIgnoreCase('hong')">  (O)
<if test="userId.equalsIgnoreCase('h')">  (O)
<if test="'h'.equalsIgnoreCase(userId)">  (Error)

----------------------------------------------------------------------------------------------------

값이 없으면 insert, 있으면 update (오라클의 MERGE INTO)

ON DUPLICATE KEY UPDATE

데이터 삽입 시, PRIMERY KEY나 UNIQUE KEY가 중복되었을 경우 지정한 데이터만 UPDATE하는 명령어를 의미한다.
(중복된 키가 없을 경우 INSERT 로직을 수행한다.) 
a,b가 UK인 a,b,c 컬럼을 갖고있는 테이블이 있다고 할때,
a와 b 모두 이미 있는 값이 들어갈경우 (UK가 모두 중복된경우) update문을 수행하고 아니면 insert문을 수행함


ex) UK가 중복되었을시 4개 컬럼 업데이트
<insert id="saveAll" parameterType="curationViewDetailEntity">
	INSERT INTO CURATION_VIEW_DETAIL (
		CVD_ID, CV_ID, VIEW_TYPE_CD, DEVICE, CONT, IMG_ID, UPDUSR_ID, MDFCN_DT
	) VALUES
	<foreach collection="list" item="item" separator=",">
	(
		#{item.id},
		#{item.cvId},
		#{item.viewTypeCode},
		#{item.device},
		#{item.content},
		#{item.imgId},
		#{item.modifyUserId},
		NOW()
	)
	</foreach>
	ON DUPLICATE KEY UPDATE
		PERD_BGNG_YMD = #{start},		// UK가 중복된경우, 여기 적어놓은 컬럼들을 "업데이트" 하는것.
		TOUR_FX_CD = #{plan},				// UK가 중복된경우, 여기 적어놓은 컬럼들을 "업데이트" 하는것.
		PERD_END_YMD = #{end},			// ★이렇게 쓸수도 있고 → 컬럼명 = #{파라미터키}
		CONT = VALUES(CONT),			// ★이렇게 쓸수도 있음 → 컬럼명 = VALUES(컬럼명)
</insert>


ex) List<Map<String,Object> 형태도 가능
<insert id="insertByLetterByDateInfoByGoods" parameterType="list">
	INSERT INTO TRSS_LOTTERY_CHANCE (
	TLC_ID,
	TNM_ID,
	TGM_ID,
	LT_APLCN_YMD,
	LMMT_CNT,
	PZWN_RPBLTY,
	RGTR_ID,
	UPDUSR_ID,
	MDFCN_DT
	) VALUES
	<foreach collection="list" item="item" separator=",">
		(
		#{item.TLC_ID},
		#{item.TNM_ID},
		#{item.TGM_ID},
		#{item.LT_APLCN_YMD},
		#{item.LMMT_CNT},
		#{item.PZWN_RPBLTY},
		#{item.USR_ID},
		#{item.USR_ID},
		NOW()
		)
	</foreach>

	ON DUPLICATE KEY UPDATE
	LT_APLCN_YMD = VALUES(LT_APLCN_YMD),
	LMMT_CNT = VALUES(LMMT_CNT),
	PZWN_RPBLTY = VALUES(PZWN_RPBLTY),
	UPDUSR_ID = VALUES(UPDUSR_ID),
	MDFCN_DT = VALUES(MDFCN_DT)
</insert>

------------------------------

mybatis파라미터로 List가 담긴 Map을 받는것도 가능함

ex) 아래와 같은 Map 데이터가 2개 있고, 두번의 insert를 한다고 할때
map: {
  TNM_ID=9cbad6dc-1c05-44ae-88bc-258ef5e65aaf,
  USR_ID=5a063c3d-856e-11ec-b08c-0050569dc2b9,
  type=L,
  list=[
    {
      LMMT_CNT=1,
      TGM_ID=16855fca-fa97-44af-9f3b-0cbda41b7b30,
      LT_APLCN_YMD=2023-06-10
    },
    {
      LMMT_CNT=2,
      TGM_ID=5704942e-b2ca-489e-a6db-599a741ef450,
      LT_APLCN_YMD=2023-06-10
    }
  ]
}
map: {
  TNM_ID=9cbad6dc-1c05-44ae-88bc-258ef5e65aaf,
  USR_ID=5a063c3d-856e-11ec-b08c-0050569dc2b9,
  type=P,
  list=[
    {
      PZWN_RPBLTY=5,
      TGM_ID=16855fca-fa97-44af-9f3b-0cbda41b7b30,
      LT_APLCN_YMD=2023-06-11
    },
    {
      PZWN_RPBLTY=6,
      TGM_ID=5704942e-b2ca-489e-a6db-599a741ef450,
      LT_APLCN_YMD=2023-06-11
    }
  ]
}

<insert id="insertByLetterByDateInfoByGoods" parameterType="map">
	INSERT INTO TRSS_LOTTERY_CHANCE (
		TNM_ID,
		TGM_ID,
		LT_APLCN_YMD,
		<if test='type eq "L"'>LMMT_CNT,</if>
		<if test='type eq "P"'>PZWN_RPBLTY,</if>
		RGTR_ID,
		UPDUSR_ID,
		MDFCN_DT
	) VALUES
	<foreach collection="list" item="item" separator=",">
		(
		#{TNM_ID},
		#{item.TGM_ID},
		#{item.LT_APLCN_YMD},
		<if test='type eq "L"'>IF(#{item.LMMT_CNT} = '', NULL, #{item.LMMT_CNT}),</if>
		<if test='type eq "P"'>COALESCE(IF(#{item.LMMT_CNT} = '', NULL, #{item.LMMT_CNT}), 0),</if>
		#{USR_ID},
		#{USR_ID},
		NOW()
		)
	</foreach>
	ON DUPLICATE KEY UPDATE
	LT_APLCN_YMD = VALUES(LT_APLCN_YMD),
	<if test='type eq "L"'>LMMT_CNT = VALUES(LMMT_CNT),</if>
	<if test='type eq "P"'>PZWN_RPBLTY = VALUES(PZWN_RPBLTY),</if>
	UPDUSR_ID = VALUES(UPDUSR_ID),
	MDFCN_DT = VALUES(MDFCN_DT)
</insert>

이때 collection=""는 Map의 리스트key를 넣으면 됨. 아예 List나 Set으로 받은경우는 아래처럼 써야함
<insert id="insertTransportDocNumMulti">
	INSERT INTO TRSS_TRS_HST(TTH_ID, TP_ID, TYPE, TRS_MN_CD, WYBL_NO, IP_ADRES, RGTR_ID, REG_DT)
	VALUES
	<foreach collection="set" item="item" open="(" close=")" separator=",">

조건쓸때 ON DUPLICATE KEY UPDATE문에도 if조건을 넣어야함 안넣으면 파라미터값이 안들어온 다른 컬럼이 null로 update됨
예를들어 item.LMMT_CNT는 값이 있고 item.PZWN_RPBLTY는 값이 없을때 값이 없는 PZWN_RPBLTY가 null로 update돼버림
PZWN_RPBLTY컬럼만 update하려면 ON DUPLICATE KEY UPDATE에도 PZWN_RPBLTY만 넣어야함


ex2) parameterType은 넣어도 되고 안넣어도 됨
<insert id="insert" parameterType="java.util.Map">
	INSERT INTO SRCH_IDX_RCMM_KWRD (SRK_ID, KWRD, LINK_TYPE, EXTRL_URL, CRT_DT, COT_ID, USR_ID)
	VALUES
	<foreach item="item" collection="list" separator=",">
		(#{item.srkId}, #{item.kwrd}, #{item.linkType}, #{item.extrlUrl}, NOW(),
		<if test='"I" == item.linkType'>#{item.cotId}</if>
		<if test='"O" == item.linkType'>NULL</if>,
		 #{usrId})
	</foreach>
	ON DUPLICATE KEY UPDATE
		MDFCN_DT = NOW()
</insert>

----------------------------------------------------------------------------------------------------

mybatis에서

빈문자열이 파라미터로 받아질 수 있는 경우
eq '' 혹은 == '' 이렇게 비교를 해야하고,

null이 파라미터로 받아질 수 있는경우
eq null 혹은 == null 이렇게 비교해야함

만약 == 말고 = 을 쓸경우 대입연산자라 변수에 대입이 되어버림


헷갈리면 보내기직전에 찍어보거나(map으로 보낸다면 .get() 메소드 사용해서하면됨)
mybatis에서 <if test="" 로 111 222 ... 넣어서 테스트하기(콘솔 오류에 무슨 숫자들이 들어있는지 확인하면됨)
ex)
<if test="sdate = ''">
	11
</if>
<if test="sdate eq ''">
	22
</if>
<if test="sdate = null">
	33
</if>
<if test="sdate eq null">
	44
</if>
<if test="sdate == null">
	55
</if>
<if test="sdate == ''">
	66
</if>

처음에 클라이언트단에서, map의 key에, 삼항연산자로, 값이 있을경우 값을넣고 없을경우 빈문자열을 넣어 보내면
중간처리과정에서 .containKey() / .has() 메소드로 확인을 할 필요가 없음. 마지막 mybatis에서 빈문자열일경우 처리만 하면 됨

하지만 if로 처리해서 값이 있을때만 key&value를 만든경우
즉, map에 key자체가 없을경우 .containKey() / .has() 등 처리가 필요하고, 어차피 마지막 mybatis에서 null처리까지 해야함

------------------------------

mybatic insert시 파라미터로 null을 받으면 null이 들어가게 처리 (처리를 안하면 null은 안들어가고 오류 발생함)

#{파라미터, jdbcType=자료형}

ex) #{paramAttr1, jdbcType=INTEGER}

------------------------------

VO클래스를 만들때 0으로 말고 null로 처리하는법

자료형을
long, int, float 보다
Long, Integer, Float 이렇게 Wrapper Class로 쓰면 0으로 초기화가 되지 않아서 값이 없을땐 null로 처리가 된다

그럼 0 or null 둘 다 쓸수있음

------------------------------

mybatis에서 부등호 비교시

#{item.LMMT_CNT} &gt; (
	SELECT COUNT(*)
	FROM TRSS_PZWNR P
	JOIN TRSS_GOODS_DTLE D USING(TGD_ID)
	WHERE D.TGM_ID = #{item.TGM_ID}
	AND DATE(P.GIVE_DT) = #{item.LT_APLCN_YMD}
), 0, 1)

이렇게 #{}로 묶어서 비교해야함 ${}로 하면 연산이 안됨.
이유는 ${}는 문자 그대로를 치환하는거라 sql문에서 직접적으로 인식이 안된다고 함

------------------------------

mybatis에서 boolean비교시

0/1로 바뀜

<if test="!permission">

조건문에 이런식으로 넣으면 되고

꼭 boolean타입으로 안보내고 자바스크립트처럼 0 or 0이아닌 숫자 로 보내도 됨

----------------------------------------------------------------------------------------------------

HTTP 요청 메시지

HTTP 메소드	RFC			요청에 Body가 있음	응답에 Body가 있음	안전		멱등(Idempotent)	캐시 가능
GET			RFC 7231	아니요			예				예		예				예
HEAD		RFC 7231	아니요			아니요			예		예				예
POST		RFC 7231	예				예				아니요	아니요			예
PUT			RFC 7231	예				예				아니요	예				아니요
DELETE		RFC 7231	아니요			예				아니요	예				아니요
CONNECT	RFC 7231	예				예				아니요	아니요			아니요
OPTIONS		RFC 7231	선택 사항			예				예		예				아니요
TRACE		RFC 7231	아니요			예				예		예				아니요
PATCH		RFC 5789	예				예				아니요	아니요			예

ex) (Get 요청) comic.naver.com/webtoon/detail?id=318995
	method			endpoint				parameter

------------------------------

url구조

ex) http://www.muisic.naver.com/listen/top100.nhn?domain=OVERSEA&duration=1h#content
프로토콜(Protocol) : http
도메인(domain) : www.music.naver.com
	서브도메인 : www
	호스트명 : music
	도메인명 : naver
	상위 도메인명 : com
경로(Path) : listen/top100.nhn
	페이지 : top100
	확장자 : nhn
파라미터(Parameter) : ?domain=OVERSEA&duration=1h
	파라미터 이름 : domain , duration
	파라미터 값 : OVERSEA , 1h
앵커(Fragment) : #content

----------------------------------------------------------------------------------------------------

응답 메시지

응답 메시지는 다음으로 구성된다.

상태표시 행(status line): 상태코드(status code)와 reason message를 포함한다. (예. HTTP/1.1 200 OK. 클라이언트의 요청이 성공적으로 전달되었음을 표시)
응답 헤더필드 (예.Content-Type: text/html)
빈 줄 (empty line)
기타 메시지

----------------------------------------------------------------------------------------------------

HTTP 응답코드


1xx	Informational		

-----

2xx	Successful


200 OK
가장 일반적인 경우, 요청된 웹 페이지를 돌려줄 경우

-----

3xx	Redirection


301 Moved Permanently
요청된 URL이 (Location: header로 지정된) URL로 완전히 전환된 경우. client는 요청된 URL을 지우던가 새 URL로 바꿔치기 한다

302 Found
인터넷 브라우저에서 사용자가 A라는 페이지를 요청했는데, Url이 B라는 페이지로 변경되었다면 해당 페이지는 리다이렉트가 되었다는 것을 뜻한다.
이럴때, 301 리다이렉트를 한다면 검색엔진 크롤링에서는 B라는 페이지에 대한 수집을 하지만
302 리다이렉트를 한다면, A라는 페이지에 대해서 수집할 것이다.
HTTP/1.0과 초기 HTTP/1.1과 호환성 유지를 위해 남겨진 코드. 원래는 요청된 URL이 301과는 달리 임시로 변경된 것을 나타내는 것이었으나,
실제 구현이 HTTP 규약의 의도를 벗어나서 303과 307로 분리하여 제정

303 See Other
요청된 URL이 잠시 다른 URL로 바뀐 것을 알림. (Location: header로 지정된) 바뀐 URL은 GET method로 접근해야 함

307 Temporary Redirect
요청된 URL이 잠시 다른 URL로 바뀐 것을 알림. (Location: header로 지정된) 바뀐 URL은 GET method로 접근해야 함

-----

4xx	Client Error

400 Bad Request
HTTP 요청, 특히 문법이 잘못된 경우

401 Unauthorized
웹 페이지 접근 시 필요한 인증 자격이 없거나 부족한 경우

403 Forbidden
인증 정보는 있지만 권한이 없는 웹 페이지에 접근했을 경우

404 Not Found
존재하지 않는 페이지에 접근했을 경우

-----

5xx	Server Error

500 Internal Server Error
웹 서버 설정이 잘못 되었거나 서버 프로그램에 오류가 있을 때

503 Service Unavailable
웹 서버에 너무 많은 요청이 몰리거나 웹 서버에 부하가 걸려 응답하지 못할 때

----------------------------------------------------------------------------------------------------

mybatis 로그 출력시키기

동적 SQL문이 실행 조건에 따라 어떻게 달라지는지 확인할 수 있어 디버깅 시 매우 유용함


1. pom.xml에 의존성 추가 (추가 후 maven update 하기)
<dependency>
	<groupId>org.bgee.log4jdbc-log4j2</groupId>
	<artifactId>log4jdbc-log4j2-jdbc4.1</artifactId>
	<version>1.16</version>
</dependency>


<application.yml일 경우>

2. log4jdbc 설정
log4jdbc:
	spylogdelegator:
		name: net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator
	dump:
		sql:
			maxlinelength: 0 # 최대 몇줄 출력에 관한 설정, 0으로 설정하면 제한 없이 설정

3. driverSpy 설정
spring:
	datasource:
		driver-class-name: org.mariadb.jdbc.Driver
위를 아래처럼 변경
spring:
	datasource:
		driver-class-name: net.sf.log4jdbc.sql.jdbcapi.DriverSpy

4. datasource 설정
spring:
	datasource:
		url: jdbc:mariadb://61.98.130.164:3306/KTO
위를 아래처럼 변경
spring:
	datasource:
		url: jdbc:log4jdbc:mariadb://61.98.130.164:3306/KTO

5. log level 설정
logging:
	level:
		jdbc:
		sqlonly: OFF
		sqltiming: INFO
		resultsettable: INFO
		audit: OFF
		resultset: OFF
		connection: OFF


<application.properties일 경우>

2. log4jdbc 설정
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator
log4jdbc.dump.sql.maxlinelength=0 # 최대 몇줄 출력에 관한 설정, 0으로 설정하면 제한 없이 설정

3. driverSpy 설정
driver-class-name=org.mariadb.jdbc.Driver
를 아래처럼 변경
driver-class-name=net.sf.log4jdbc.sql.jdbcapi.DriverSpy

4. datasource 설정
spring.datasource.url=jdbc:oracle:~~
를 아래처럼 변경
spring.datasource.url=jdbc:log4jdbc:~~

5. log level 설정
logging.level.jdbc.sqlonly=OFF
logging.level.jdbc.sqltiming=INFO
logging.level.jdbc.resultsettable=INFO
logging.level.jdbc.audit=OFF
logging.level.jdbc.resultset=OFF
logging.level.jdbc.connection=OFF


이클립스 쓸경우 톰캣 설정 변경해야함

서버 더블클릭 → Open launch configuration → Arguments탭 → VM arguments 입력란에 아래 추가
-Dlog4jdbc.drivers=com.tmax.tibero.jdbc.TbDriver

----------------------------------------------------------------------------------------------------

applitation.yml 파일에 작성한 내용을 가져와서 쓰는법

<방법1>
@Component
public class C1 implements ApplicationListener<ApplicationStartedEvent> {
	private final Environment env;

	@Autowired
	public C1(Environment env) {
		this.env = env;
	}

	@Override
	public void onApplicationEvent(ApplicationStartedEvent event) {
		String username = env.getProperty("test.username");
		String password = env.getProperty("test.password");
		System.out.println("username = " + username);
		System.out.println("password = " + password);
	}
}

3. 내용은 디버그모드로 실행해보면 env객체안에 propertySources → propertySourceList → 배열중 OriginTrackedMapPropertySource@~ → source
안에 application.properties에서 작성한 속성들이 있음

------------------------------

<방법2: 타입 지정해서 받기>

@Value만 쓰면 되고, ApplicationListner는 굳이 쓸 필요없음(ApplicationListner는 단순히 이벤트(어플리케이션이 시작될때)를 사용하기위함)>

@Component
public class C1 implements ApplicationListener<ApplicationStartedEvent> {
	@Value("${test.username}")
	private String username;

	@Value("${test.password}")
	private int password;

	@Override
	public void onApplicationEvent(ApplicationStartedEvent event) {
		System.out.println("username: " + username);
		System.out.println("password: " + password);
	}
}

------------------------------

<방법3: 커스텀 객체를 만들어두고 필요한곳에서 의존성 주입해서 쓰기>

지정한 설정값이 test.~~이므로 "test"를 입력
test.test2.~~ 이면 "test.test2" 이렇게 입력
★Getter/Setter 를 롬복을 쓰면 안되고 직접 입력해야함. 롬복쓰면 아래오류 발생(getter를 찾을수없다고 나옴)
↓↓↓
cannot find symbol
symbol:   method get~~~()

@Component
@ConfigurationProperties("test")
public class C3 {
	private String username;
	private int password;

	public String getUsername() {
		return username;
	}

	public void setUsername(String username) {
		this.username = username;
	}

	public int getPassword() {
		return password;
	}

	public void setPassword(int password) {
		this.password = password;
	}
}

@Component
public class C3Run implements ApplicationListener<ApplicationStartedEvent> {
	private final C3 c3;

	public C3Run(C3 c3) {
		this.c3 = c3;
	}

	@Override
	public void onApplicationEvent(ApplicationStartedEvent event) {
		System.out.println("username7: " + c3.getUsername());
		System.out.println("password8: " + c3.getPassword());
	}
}

------------------------------

<설정파일이 여러개일때(설정파일을 여러개로 분리한경우)>

사용할 클래스에 아래 어노테이션 붙이고 배열에 properties파일명 넣기 (기본 application.properties 는 안써도 됨)
@PropertySource(value = {"application2.properties"})

아래처럼 설정파일을 여러개 가져올수도 있음
@PropertySource(value = {"application2.properties", "application3.properties"})

------------------------------

<또다른방법>

pom.xml에 의존성 추가
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-configuration-processor</artifactId>
	<optional>true</optional>
</dependency>


이후 application파일에 원하는 속성이름/속성값 작성후
works-api:
  base-url: aaa
  domain-id: 111


필요한 클래스에 아래 어노테이션 넣기
@ConfigurationProperties("XXX")

빨간줄 뜨면 아래 어노테이션도 추가
@Configuration

Re-run Spring Boot Configuration Annotation Processor to update generated metadata
위같은 경고가 뜨면 File → Invalidate Caches... 로 캐시 다 지우기

------------------------------

.yml 파일의 경우

yml의 경우에는 PropertySource에 yml을 read할 수 있는 factory가 없기 때문에 임의로 생성을 해주어야함

1. 클래스 생성
public class YamlPropertySourceFactory implements PropertySourceFactory {
	@Override
	public PropertySource<?> createPropertySource(@Nullable String name, EncodedResource resource) throws IOException {
		YamlPropertiesFactoryBean factory = new YamlPropertiesFactoryBean();
		factory.setResources(resource.getResource());
		Properties properties = factory.getObject();
		return new PropertiesPropertySource(resource.getResource().getFilename(), properties);
	}
}

2. 가져오기
마찬가지로 배열이라 yml파일을 여러개 넣을수 있음
@Component
@PropertySource(value = {"application.yml"}, factory = YamlPropertySourceFactory.class)
public class C5 implements ApplicationListener<ApplicationStartedEvent> {
	@Value("${test.aaa}")
	private String aaa;

	@Override
	public void onApplicationEvent(ApplicationStartedEvent event) {
		System.out.println("aaa: " + aaa);
	}
}

----------------------------------------------------------------------------------------------------

ajax success 응답데이터 받은거 확인할때 참고

success블럭에
alert과 location.href을 같이 쓰면 alert때문에 이동이 안되고 멈춰있는데
그때 개발자도구로 보면 받은 데이터가 없음

location.href 를 주석하고 테스트해야함

-----

location이 걸려있을때 간단한 분기문 분석같은건 console.log 말고 alert 으로 테스트 하면 편함

----------------------------------------------------------------------------------------------------

HTTP Request를 보내는 3가지 방법

------------------------------

RestTemplate 이용 (HttpClient를 감싼것)


private static void getEmployees()
{
    final String uri = "http://localhost:8080/springrestexample/employees.xml";

    RestTemplate restTemplate = new RestTemplate();
    String result = restTemplate.getForObject(uri, String.class);

    System.out.println(result);
}

------------------------------

RestTemplate 이용 (다른 정보들과 함께 보내는 방법)


HashMap<String, Object> result = new HashMap<String, Object>();

String jsonInString = "";

try {

	HttpComponentsClientHttpRequestFactory factory = new HttpComponentsClientHttpRequestFactory();
	factory.setConnectTimeout(5000); //타임아웃 설정 5초
	factory.setReadTimeout(5000);//타임아웃 설정 5초
	RestTemplate restTemplate = new RestTemplate(factory);

	HttpHeaders header = new HttpHeaders();

	// 인증정보필요할시 추가	
	// String clientCredentials = "develop" + ":" + "uniess1208";
	// String base64ClientCredentials = new String(Base64.encodeBase64(clientCredentials.getBytes()));
	// header.setContentType(MediaType.APPLICATION_FORM_URLENCODED);
	// header.add("Authorization", "Basic " + base64ClientCredentials);

	HttpEntity<?> entity = new HttpEntity<>(header);

	String url = "http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json";

	UriComponents uri = UriComponentsBuilder.fromHttpUrl(url+"?"+"key=430156241533f1d058c603178cc3ca0e&targetDt=20120101").build();

	List<HttpMessageConverter<?>> messageConverters = new ArrayList<>();
	MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
	converter.setSupportedMediaTypes(Collections.singletonList(MediaType.ALL));
	messageConverters.add(converter);
	restTemplate.setMessageConverters(messageConverters);

	//이 한줄의 코드로 API를 호출해 MAP타입으로 전달 받는다.
	ResponseEntity<Map> resultMap = restTemplate.exchange(uri.toString(), HttpMethod.GET, entity, Map.class);
//			result.put("statusCode", resultMap.getStatusCodeValue()); //http status code를 확인
	result.put("header", resultMap.getHeaders()); //헤더 정보 확인
	result.put("body", resultMap.getBody()); //실제 데이터 정보 확인

	//데이터를 제대로 전달 받았는지 확인 string형태로 파싱해줌
//			ObjectMapper mapper = new ObjectMapper();
//			jsonInString = mapper.writeValueAsString(resultMap.getBody());

	System.out.println(resultMap.getBody());


} catch (HttpClientErrorException | HttpServerErrorException e) {
//			result.put("statusCode", e.getRawStatusCode());
	result.put("body"  , e.getStatusText());
	System.out.println(e.toString());


} catch (Exception e) {
	result.put("statusCode", "999");
	result.put("body"  , "excpetion오류");
	System.out.println(e.toString());
}

참고로 url에 특수문자가 들어갈 경우 인코딩이 되어버리기때문에 정상적인호출이 안될수도있는데
이럴때는 String이 아닌 URI 객체로 해야함 (java.net.URI)

------------------------------

WebClient 이용 (스프링 5버전 이상에서 지원)

@Bean
public WebClient localApiClient() {
    return WebClient.create("http://localhost:8080/api/v3");
}
@Service
public class UserService {

    private static final Duration REQUEST_TIMEOUT = Duration.ofSeconds(3);

    private final WebClient localApiClient;

    @Autowired
    public UserService(WebClient localApiClient) {
        this.localApiClient = localApiClient;
    }

    public User getUser(long id) {
        return localApiClient
                .get()
                .uri("/users/" + id)
                .retrieve()
                .bodyToMono(User.class)
                .block(REQUEST_TIMEOUT);
    }

}

----------------------------------------------------------------------------------------------------

css 파일 불러올때 파라미터를 붙이는 이유

일반적으로 브라우저는 css파일을 처음 로드할때, 해당 파일을 캐시(cache)에 저장함
이후에 동일한 페이지를 로드할 때, 브라우저는 캐시된 css파일을 다시 로드하여 서버에서 가져오는 것이 아닌, 캐시된 파일을 이용함
이렇게 함으로써, 페이지 로드 속도가 향상되고 네트워크 대역폭도 절약됨

그러나 css파일이 변경되어 내용이 업데이트될 경우, 이전에 캐시된 파일을 사용하게 되면 변경된 내용이 반영되지 않음
이러한 문제를 해결하기 위해, css파일 뒤에 파라미터를 추가해 새로운 버전을 강제로 로드하도록 지시할 수 있음

<link rel='stylesheet' src='/test.css?v=1'>

위 예시에서, "?v=1"은 css파일 버전을 나타내는 파라미터임
이 파라미터를 추가함으로써 브라우저는 이전에 캐시된 파일과 구분하여 새로운 파일을 다시 로드하게 됨

보통 이 파라미터는 css파일의 수정일자, 빌드 번호 등을 사용하여 자동으로 생성되며, 파일이 변경될 때마다 자동으로 새로운 버전이 생성됨
이렇게 함으로써, 변경된 css파일이 즉시 반영되고, 동일한 파일이 캐시된 상태에서도 새로운 파일을 로드할 수 있음

★사용자는 캐시삭제를 하지 않고도 변경된 css파일을 즉시 반영되게 할 수 있음


단, 파라미터가 새로운 값이 아닌 같은 값이면 (css파일 url 뒤에 추가된 파라미터의 값이 변경되지 않으면)
이전에 캐시된 파일을 사용함.

따라서, 같은 값인 경우에는 css파일을 새로 불러오지 않고 캐시된 파일을 사용함

예를들어, 이전에 "test.css?v=1"을 로드하여 캐시에 저장했다면, 같은 URL("test.css?v=1")을 사용하여 다시 요청하면 캐시된 파일을 사용함


따라서 변경된 파일을 즉시 적용하기 위해서는 날짜나 버전파라미터를 붙이는게 좋고,
css 수정이 여러번 필요할때는 그냥 랜덤uuid를 넣어놓는것도 방법임

----------------------------------------------------------------------------------------------------

api 요청 테스트 사이트 (json 데이터가 응답됨)

1. json샘플 데이터 응답 사이트(https://jsonplaceholder.typicode.com/)
아래처럼 요청하면 됨
https://jsonplaceholder.typicode.com/todos/1

2. 공공데이터포털(https://www.data.go.kr/)

----------------------------------------------------------------------------------------------------

junit  테스트


test폴더에 똑같은 이름의 패키지로, 클래스명뒤에 Test 를 붙인 클래스를 만들고,

메소드에 @Test를 붙이면 실행을 시킬 수 있음


실행을 시켰을때 결과가 같으면 실행창에 초록색으로 정상실행되지만, 다를경우 에러를 띄워줌

import org.junit.jupiter.api.Assertions;
Assertions.assertEquals(비교값1, 비교값2);

or

import org.assertj.core.api.Assertions;
Assertions.assertThat(비교값1).isEqualTo(비교값2)

opt + enter로
Add on-demand static import for 'org.assertj.core.api.Assertions' 를 누르면 static import돼서 Assertions생략하고 assertThat만 쓸 수 있음


장점은 클래스or패키지레벨에서 동시에 여러개의 테스트를 실행시킬 수 있음

------------------------------

각 메소드가 끝날때마다 실행되는 메소드 만들기 (테스트끼리는 서로 의존관계 없이 설계되어야함)

하나의 테스트가 끝날때마다 저장소나 공용데이터들을 다시 깔끔하게 지워놔야함

@AfterEach
public void afterEach(){
	repository.clearStore();
}

<MemoryMemberRepository.java>
public class MemoryMemberRepository implements MemberRepository{
	.
	.
	public void clearStore(){
		store.clear();
	}
}

----------------------------------------------------------------------------------------------------

test패키지에서 말고 그냥 코드패키지에서 테스트 편하게 하는법

클래스에서 cmd + shift + t → enter
테스트할 메소드들 선택후 ok

그러면 test패키지안에 테스트 껍데기가 자동으로 만들어짐

자동으로 만들면 org.junit.jupiter.api.Assertions.*; 가 import되어있음

----------------------------------------------------------------------------------------------------

테스트 코드는 한글로 적어도됨 (직관적)

테스트코드는 빌드될때 실제코드에 포함되지 않음

----------------------------------------------------------------------------------------------------

DAO / Repository

DAO와 Repository는 비슷한 역할을 한다

그러나 일반적으로 DAO는 데이터 액세스 계층에서 데이터베이스와 상호 작용하는 데 사용되는 클래스이고,
Repository는 애플리케이션의 데이터 저장소에 대한 추상화 계층으로, 애플리케이션과 데이터 저장소 간의 인터페이스를 제공하는 클래스 또는 인터페이스입니다.

그렇다면 DAO와 Repository의 차이는 무엇일까요? DAO는 데이터 액세스 계층에서 데이터베이스와 상호 작용하는 데 사용되는 클래스이며,
데이터베이스와 직접적으로 상호 작용하기 때문에 SQL 쿼리와 같은 데이터베이스 관련 로직이 포함될 수 있습니다.
반면에 Repository는 애플리케이션의 데이터 저장소에 대한 추상화 계층으로, 데이터베이스와 직접적으로 상호 작용하지 않습니다.
대신, 애플리케이션의 비즈니스 로직과 데이터 저장소 간의 인터페이스를 제공합니다.

그러므로 Repository는 애플리케이션에서 데이터 저장소를 추상화하는 데 중점을 두며, DAO는 데이터베이스와 상호 작용하는 데 중점을 둡니다.
이러한 차이점을 이해하면 DAO와 Repository를 적절하게 사용하여 애플리케이션의 데이터 액세스 계층을 설계할 수 있습니다.

----------------------------------------------------------------------------------------------------

mybatis로 Set을 파라미터로 받아서 다중 insert or (insert or update) 하는법 (mysql에 다중insert 문법이 있음. mybatis는 그냥 코드를 반복해서 생성하는것뿐)

<insert id="insertTransportDocNumMulti" parameterType="java.util.Set">
	INSERT INTO TRSS_TRS_HST(TTH_ID, TP_ID, TYPE, TRS_MN_CD, WYBL_NO, IP_ADRES, RGTR_ID, REG_DT)
	VALUES
	<foreach collection="collection" item="item" open="(" close=")" separator="),(">
		#{item.TTH_ID},
		#{item.TP_ID},
		#{item.TYPE},
		(SELECT COD_ID FROM CODE WHERE VALUE = #{item.TRS_MN}),
		#{item.WYBL_NO},
		#{item.IP_ADRES},
		#{item.RGTR_ID},
		NOW()
	</foreach>
</insert>

parameterType="java.util.Set" 는 넣어도 되고 안넣어도 됨

------------------------------

다중 update / delete도 가능함

DELETE FROM SRCH_IDX_RCMM_KWRD
WHERE SRK_ID IN
<foreach item="item" collection="list" separator="," open="(" close=")">
	#{item.id}
</foreach>

----------------------------------------------------------------------------------------------------

sqlSession 의

select 는 selectList의 별칭임. selectList로 안쓰고 select로 써도 아무상관없음

selectOne : 1개
select / selectList : N개
insert / delete / update : 삽삭갱

----------------------------------------------------------------------------------------------------

조건이 여러개일때는 != null 이걸 써야함

<if test="title">

↓↓↓↓↓

조건이 추가된 경우

<if test="title and title != ''">

↓↓↓↓↓

널 체크를 명시적으로 해야함

<if test="title != null and title != ''">

----------------------------------------------------------------------------------------------------

mybatis 반환타입

java.lang.String / java.math.BigDecimal / java.lang.Integer / Long
반환 가능

문자열은 String, 숫자는 Integer, 실수는 BigDecimal 로 반환됨

단, 아래의 집계함수는 특정 타입으로 반환됨
COUNT() - Long
AVG() - BigDecimal
SUM() - BigDecimal
MIN() / MAX() - 자료형에 따라 Long / BigDecimal

더 정확히 알고싶다면

.getClass()
로 찍어보기

이후
instanceof 자료형
으로 비교하면됨

----------------------------------------------------------------------------------------------------

ibatis는 mybatis의 과거버전임

----------------------------------------------------------------------------------------------------




















