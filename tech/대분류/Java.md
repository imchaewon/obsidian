자바 애노테이션


@SuppressWarnings("옵션") : 해당 메소드/클래스에서 오류검사를 하지 않음

rawtypes : 제너릭을 사용하는 클래스 매개 변수가 불특정일 때의 경고
unchecked : 검증되지 않은 연산자 관련 경고
deprecation : 더이상 사용되지 않는것 관련 경고
unused : 참조되지 않는 코드 관련 경고


@Target : 메타 애노테이션, 사용자 애노테이션 생성시 애노테이션을 어느곳에 부착을 가능하게 할지 지정
@Retention : 메타 애노테이션, 사용자 애노테이션 생성시 애노테이션을 언제까지 유지하게 할건지 지정
@Documented : 메타 애노테이션, 사용자 애노테이션 생성시 해당 애노테이션을 Javadoc(Java문서)에 포함시킴

------------------------------

롬복 애노테이션

@Getter : 게터 생성

@Setter(onMethod_ = {@Autowired}) : 세터 생성

@ToString : toString 재정의
	상속을 받은 경우에, 부모와 나의 속성을 모두 출력하고싶을때 부모와 자식에 모두 @Tostring을 붙이면 자식속성만 출력됨
	이를 해결하려면 부모클래스에 @ToSting을 넣고, 자식클래스에 @ToString(callSuper = true) 이속성을 넣으면 부모&자식 필드가 모두 출력됨
@ToString.Exclude : 특정 필드만 toString 재정의를 하지 않음(해제)

@AllArgsConstructor : 클래스에 작성, new()를 (객체를 생성)해준다 (모든 필드에 대해)
	모든필드값을 파라미터로 받는 생성자를 만들어줌

@RequiredArgsConstructor : 멤버변수에 final을 붙이고 클래스에 작성, new()를 (객체를 생성)해준다 (초기화되지않은final 필드와 @NonNull에 대해)
	final이나 @NonNull인 필드 값만 파라미터로 받는 생성자를 만들어줌
	final이나 @NonNull을 같이 쓸 경우에만 쓰기

@NoArgsConstructor : 파라미터가 없는 기본 생성자를 만들어줌
	AllArgsConstructor을 쓰면 기본생성자가 안만들어지는데, 이 때문에 같이 씀

@EqualsAndHashCode

@Data : VO클래스에 부착, getter, setter, toString, requiredArgsConstructor, equalsAndHashCode 들을 생성해줌

@NonNull : 메소드 파라미터에 사용시 null이 들어온 경우 NullPointerException예외를 발생시켜준다
	필드에도 사용가능하고 이때는 예외는 안발생시킴

@Builder : DTO클래스or생성자에 선언. 자동으로 해당 클래스에 빌더를 추가해줌.
클래스에 달면 @AllArgsConstructor도 같이 쓴것과 같다.
사용은 아래처럼 할수있음
Resturant resturant2 = Resturant.builder()
	.id(0L)
	.description("강남역 11번 출구 쪽에 있는 자매수산 입니다.")
	.name("자매수산")
	.build();

@Log4j : 클래스에 부착, System.out.println() 대신 이용할 수 있고 앞에 패키지명과 파일명이 붙음, 찍어놓은 log들이 안보이게 일괄 설정가능

------------------------------

jackson 애노테이션

@JsonCreator : 생성자 or 팩토리메서드에 부착
@JsonProperty : 생성자 파라미터 or DTO의 필드 에 삽입.
	@JsonCreator는 Json객체를 deserialize(역직렬화)하여 객체 mapping 시 사용할 생성자를 지정할 수 있도록 도와준다.
	@JsonProperty는 @JsonCreator의 파라미터 필드에 정의되어 Mapping을 위한 property값을 정의한다.
	멤버 필드와 json key이름이 일치하지않을떄,인수로 기존 key이름을 넣어서 새 변수명으로 치환 가능하고,
	★ 이름이 일치한다고 하더라도 @JsonProperty("key이름") 을 넣어야 함
	그 이유는 함수가 컴파일되면 파라미터가 'var0', 'var1'과 같이 임의의 이름으로 바뀌기때문에
	key/value 를 얻어와도 어떤 필드에 값을 적용해야 되는지 알 수 없기 때문이다
	그렇기 때문에 각 파라미터마다 @JsonProperty애노테이션을 붙여야만 property 이름에 맞는 필드를 찾고 Reflection API로 setting 해줄 수 있다

	DTO의 필드에 붙이면 직렬화(객체→json문자열)시 별칭을 쓸 수 있음. 즉, 응답데이터의 key를 해당 별칭으로 수 있음
	@JsonProperty("itemPath")
	@Column(name = "custom_log_path")
	private String customLogPath;


@JacksonInject : 필드에 삽입. 선언된 필드가 json데이터가 아닌 inject 될것임을 알려줌
@JsonAnySetter : 엔티티 메서드에 부착. properties를 Map으로 deserialize 함
	만약 필드 속성명과 이름이 일치하는 key가 있다면 해당속성에 담고, 이외에 다른 key/value가 있으면 → 모두 Map 필드에 담김

@JsonSetter : VO/DTO세터메서드에 부착
@JsonDeserialize : unmarshalling 과정에 custom deserializer를 사용하도록 지정한다. @JsonSerialize와 반대의 역할을 하는 애노테이션
@JsonAlias : 하나 혹은 그 이상의 대체 property 이름으로 deserialize 되도록 해준다.

------------------------------

jUnit 애노테이션

@Test : 메소드에 붙이면 Junit으로 테스트가 가능해짐. 테스트패키지에서 씀

------------------------------

ibatis 애노테이션

@Alias("XXX") : vo클래스에 쓰고, mybatis의 resultType 등에서 cccc이런식으로 쓸 수 있음

------------------------------

스프링 애노테이션

@SpringBootApplication : 스프링부트 애플리케이션의 진입점(entry point) 클래스에 부착, 여러 다른 스프링 애노테이션의 조합으로
	스프링부트 애플리케이션을 빠르게 구성하고 실행하기 위해 씀
@Value : application.yml 에서 등록한 값을 가져올 수 있음
@SpringBootTest : 클래스에 부착, 테스트시 스프링부트 환경에서 테스트를 실행할 수 있게 해줌

@Controller : 클래스에 부착, 스프링 MVC 컨트롤러로 인식
@RestController : 클래스에 부착, @Controller + @ResponseBody. 모든 메소드에 @ResponseBody를 붙여줌
@Service : 클래스에 부착, 스프링 비즈니스 로직에서 사용. 특별한 처리를 하진 않지만 개발자들이 핵심 비즈니스로직이 여기에 있겠구나 라고 비즈니스계층을 인식하는데 도움이 됨
	스프링의 AOP를 사용해 메서드 실행 전후에 특정 기능을 추가할 수 있음. 스프링AOP에서는 @Service 애노테이션이 붙은 클래스에 대해서만 AOP 프록시를 생성함
@Repository : 클래스에 부착, 스프링 데이터 접근계층에서 사용. 데이터 계층의 예외를 스프링 예외로 변환해줌

@Configuration : 클래스에 부착, 스프링 설정 정보로 인식. 스프링 빈이 싱글톤을 유지하도록 추가처리를 함. @Component를 포함하므로 해당클래스도 빈으로 등록됨
	보통 개발자가 직접 제어가 불가능한 외부 라이브러리 또는 설정을 위한 클래스를 Bean으로 등록할 때 씀
@Bean : 메서드에 부착. 반환되는 객체를 스프링 빈으로 등록시킴. @Component와 같이 사용함
	개발자가 직접 수정할 수 없는 외부라이브러리 or 내장 클래스의 경우 @Configuration + @Bean 애노테이션을 이용해 bean으로 등록해 사용
	또한 메소드에 이 애노테이션을 쓸 경우, 스프링 프로젝트가 실행될때 처음에 같이 실행됨.
	이를 이용해 기본main메소드는 static인데 static을 안쓰고도 프로젝트 실행이 가능해짐

@Component : 의존 관계인 모든 클래스에 부착, 개발자가 직접 작성한 클래스를 빈으로 등록할 수 있음. @Controller/@Service/@Repository/@Configuration 에 포함되어있음
	스프링의 빈으로 등록하기 위한 자바파일/xml로 수동설정하는방법과 애노테이션으로 자동설정하는 방법중 애노테이션으로 하는 방법 (컴포넌트스캔 필요)
	위에서 말한 애노테이션들에도 모두 @Component가 들어있지만, 알아보기쉽게 명칭을 다르게 하는것. 물론 각 애노테이션마다 부가기능이 있음
@ComponentScan: 클래스에 부착. 현재클래스가 있는 패키지를 루트패스로, 모든 @Component가 붙은 클래스를 스캔함
	탐색할 루트패키지 지정가능. @SpringBootApplication에 포함되어있음
@ComponentScan.Filter : @ComponentScan 의 속성에 삽입, 컴포넌트 스캔에서 제외시킬 수 있음

@Qualifier("XXX") : 빈이 중복되었을때(상위 클래스로 가져왔다든가, 빈 이름이 중복됐다든가 할 때)
	@Qualifier 를 이용해서 추가적으로 구분자를 쓸 수 있음. 빈 생성부/호출부 두군데에 똑같이 @Qualifier("XXX")를 넣기
@Primary : 클래스에 부착. 빈이름이 중복되었을경우 이 애노테이션이 붙은 빈이 우선권이 있음

@Autowired : 타입에 맞는 의존성을 주입해줌
@Nullable : 자동주입할 대상이 없을 경우 null을 받을 수 있음

@Scope : 클래스에 부착. 스코프 설정
@PostConstruct : 메소드에 부착. 빈 생성 완료 후 실행
@PreDestroy : 메소드에 부착. 빈 소멸 직전 실행

@RequestMapping("/경로") : 클래스위에 삽입할시 해당클래스 url의 공통된 부분을 묶어주는 역할을 하고
@RequestMapping(value="/getByID", method={RequestMethod.POST}) : 메서드에 부착할시
	value와 method속성으로 @GetMapping / @PostMapping과 동일한 효과를 낼수있다.
	주소창에서 "경로"의 요청이 왔을때 실행하겠다는 의미이다
	클래스와 메소드에 둘다 사용 가능
	,produces="application/json;charset=utf-8" 속성을 추가하면 컨트롤러에서 ajax로 map객체를 json으로 보낼 수 있다.
@GetMapping("/경로") : 메소드에 작성, Get방식 //여러개 묶어서 같이쓸때는 중괄호({"/경로1", "경로2"})
	속성을 쓰고싶을경우 경로를 value=""안에 넣고 필요한 속성을 추가하면된다
@PostMapping("/경로") : 메소드에 작성, Post방식
	속성을 쓰고싶을경우 경로를 value=""안에 넣고 필요한 속성을 추가하면된다

Request/Get/Post Mapping 속성 중
value="daily_info" : 해당 url로 들어갔을경우 실행
params="method=data" : 해당 파라미터가 있는 url로 들어갔을경우 실행

@RequestParam("XXX") : 메서드에 부착. 파라미터로 특정키에 해당하는 값을 받을 수 있음. 받을 url파라미터의 속성명 명시 or 변경
	ex) public void remove(@RequestParam("id")String id,~) {
	여러개를 한꺼번에 받으려면 VO/Map 활용

@PathVariable: 컨트롤러의 메소드의 파라미터에 부착, @GetMapping("asd/{xxx}") 로 받은 데이터를 파라미터와 연결해 가져옴
ex)
@GetMapping("asd/{xxx}")
public void asd(@PathVariable String xxx){
}

@ModelAttribute("XXX") : 메서드에 부착. url파라미터의 특정키를 Model에 안담고도 그대로 jsp로 보내서 el로 쓸 수 있음
	ex) public void content(String id, @ModelAttribute("cri") Criteria cri) {

★Model 인터페이스 : 파라미터에 삽입. 메소드 본문에서 model.addAttribute("키","값")으로 넣어놓으면 연결된 jsp에서 쓸 수 있음

@ResponseBody : 컨트롤러 메서드에 부착. 기존 String으로 리턴시켰을때 view로 보내는 기능이 해제되는 대신,
	문자열이라면 StringConverter, 객체라면 JsonConverter로 json으로 변환해서, 요청했던 서버/웹브라우저로 응답하는 기능이 활성화됨 (xml도가능)
	(viewResolver 대신에 HttpMessageConverter 가 동작함). 컨트롤러의 모든 메서드에 이 애노테이션을 붙이면 클래스에 @RestController 를 붙인것과 동일함
@RequestBody : 메서드에 부착. 가져올 파라미터에 이 애노테이션을 추가하면 ajax→컨트롤러로 vo객체로받기 이외의 데이터도 받아올 수 있으며
	컨트롤러→ajax 로 데이터 리턴시 객체를 json형태로 바꿔준다. (정확히는 Request의 Body를 받아서 그것을 특정한 객체로 변환 하는 것이다.
	'form/data' 말고 'json'으로 보낸걸 받을때만 써야함)

@RequestHeader : 메서드에 부착. HTTP헤더로 받은 정보를 가져올 수 있음 (주로 인증 관련 정보)
	public void aaa(@RequestHeader("X-MEMBER-ID") String bbb) {

@ExceptionHandler : 예외처리(bean안에 메소드에서 발생하는에러 만들기) ex) "이미 존재하는 사용자 아이디입니다"
@ControllerAdvice /
@ExceptionHandler(예외클래스 리터럴) : 전역 예외처리기 정의. 예외가 발생하면 해당 메서드가 실행되고, 그 메서드에서 클라이언트에게 오류 응답을 생성할 수 있음
ex)
@ControllerAdvice
public class GlobalExceptionHandler extends CommonResponse {
	@ExceptionHandler(Exception.class)
	protected ResponseEntity<?> handle(Exception e) {
		e.printStackTrace();
		log.error("Exception - message:{}", e.getMessage(), e);
	
		// 현재 사용중이 profile정보를 확인하는 로직
		Environment environment = context.getEnvironment();
		String[] activeProfiles = environment.getActiveProfiles();
		String activeProfile = Arrays.stream(activeProfiles).findFirst().orElse("default");
		if("dev".equals(activeProfile) || "stg".equals(activeProfile)){
			IncomingWebhook.sendToJandi(e, activeProfile, logAspect.getRequestId());
		}
	
		return this.resFail(HttpStatus.INTERNAL_SERVER_ERROR, e.getMessage());
	}
	@ExceptionHandler(Exceptions.NotFoundAuth.class)
	protected ResponseEntity<?> handle(Exceptions.NotFoundAuth e) {
		log.error("not found auth info - message:{}", e.getMessage(), e);
		return this.resFail(HttpStatus.UNAUTHORIZED, e.getMessage());
	}
	...
}

@Lazy : 지연 로딩

@NonNull : 필드에 null이 들어가면 안된다는걸 명시, 해당 필드에 null이 들어갈 수 있는 상황에 null체크를 안할 경우 경고(노란밑줄)를 발생시킴
	메소드에도 사용 가능하고 마찬가지로 경고를 띄워줌,
	메소드 파라미터에도 사용가능하나 이때는 lombok의 NonNull을 쓰는게 더 좋음(롬복은 경고+예외까지 발생시킴)

@RepositoryRestResource
의존성주입받아야 사용가능. 컨트롤러를 만들지 않아도 내부적으로 Rest Api가 만들어진다고 함
(collectionResourceRel = "XXX", path = "XXX") 옵션을 준다면 localhost:8080/XXX 으로 들어갈 수 있다고 함
<!-- https://mvnrepository.com/artifact/org.springframework.data/spring-data-rest-core -->
<dependency>
	<groupId>org.springframework.data</groupId>
	<artifactId>spring-data-rest-core</artifactId>
	<version>3.7.2</version>
</dependency>

------------------------------

JPA 애노테이션

@Column : DB컬럼명과 필드변수명을 매핑 (두 변수명이 똑같을경우에는 안써도됨)
	@Column(name="DB컬럼명")
	private char gender;

@Entity(name ="")의 경우 말그대로 엔티티의 이름을 정할때 사용됩니다. 이는 HQL에서 엔티티를 식별할 이름을 정합니다.

@Table(name ="")의 경우 Database에 생성될 table의 이름을 지정할때 사용됩니다.
	@Table이 없고 @Entity(name ="")만 존재하는 경우, @Entity의 name 속성에 의해, Entity와 Table 이름이 모두 결정됩니다.
	즉 @Entity만 사용할 경우 자동으로 Entity+Table 기능을 수행하고
	@Entity + @Table 을 따로 사용하면 각자 설정 값에 따라 작동하는 것


@Enumerated	: 자바 enum 타입을 엔티티 클래스의 속성으로 사용할 수 있음
두가지 속성이 존재
EnumType.ORDINAL : enum 순서 값을 DB에 저장
EnumType.STRING : enum 이름을 DB에 저장

enum Gender {
    MALE,
    FEMALE;
}
enum이 위와 같을때
ORDINAL로 지정하고 gender속성에 Gender.MALE 값을 세팅하면 DB에 저장되는 값은 1 이다
ORDINAL로 지정하고 gender속성에 Gender.FEMALE 값을 세팅하면 DB에 저장되는 값은 2 이다
STRING으로 지정하면 DB에는 MALE, FEMAIL 문자열 자체가 저장된다

----------------------------------------------------------------------------------------------------

프로젝트 빨간엑스 or 오류날때 (윈도우컴에서 오류모음으로 이동시키기)

프로젝트 우클릭 → Build Path → Configure Build Path... → JRE 버전 확인 후 제거/추가 → Apply and Close
프로젝트 속성 → Java Compiler → 자바 버전 확인 후 변경 → Apply and Close

----------------------------------------------------------------------------------------------------

★초기 설정
JDK및 이클립스 설치
d:class\java 폴더 생성
이클립스 워크스페이스 지정
window > preference > encoding검색 > workspace > Text file encoding > UTF-8
폰트변경
기타 설정 변경
Java Project 생성 > "JavaTest"
패키지 생성 > "com.test.java"

----------------------------------------------------------------------------------------------------

★환경 세팅

1. 개발환경 세팅
	- 운영체제(OS) - 윈도우 , 리눅스 , 맥OS
	- SDK(자바에서는 JDK) + Runtime(자바에서는 JRE)
2. 개발도구 세팅
	- 편집 프로그램 : 이클립스 , 에디트플러스 , 서브라임텍스트 등

----------------------------------------------------------------------------------------------------

★개발도구나 프로그램 설치시

되도록 최신 버전 지양 > 이유 : 안전성 입증받지 못함 > 누군가가(기업) 먼저 사용해서 성공사례 발생시 사용되는데 그게
보통 최신 버전이 나온 후  1~2년 - 5~10년 걸린다함
(아직까지는 jdk는 주로 8버전을 많이 사용함)

----------------------------------------------------------------------------------------------------

★자바 jdk (+jre)

www.oracle.com > Product > Java > Download Java > Java SE 8(1.8버전) 찾아서 > JDK Download > Windows x86 or x64

JDK(Java Development Kit)
- 자바 프로그래밍 도구
- 자바 언어를 사용해서 프로그램을 만드는데 필요한 도구의 모음
- JDK는 JVM, JRE를 포함하고 있다
- JDK 8 설치

JRE(Java Runtime Environment)
- JVM이 자바 프로그램을 동작시킬때 필요한 라이브러리 파일들과 기타 파일을 가지고 있다(JVM을 포함한다)
- 자바 프로그램을 실행시키기 위해서 반드시 설치해야한다

JVM(Java virtual machine)
- 운영체제의 종류에 상관없이 알아서 그에 맞게 자바프로그램(.class파일)을 실행할 수 있게 해준다
- JVM이 없으면 자바프로그램을 실행할 수 없다
- JVM을 사용하려면 JRE가 필요하다

1. 소스 파일을 작성한다.
- 명령어의 집합 > 특정 언어의 규칙에 따라 작성한다. > 특정 언어(자바)의 규칙(문법)에 따라 작성한다.
- 아직 프로그램이 아니다.

2. 컴퓨터가 알아들을 수 있는 표현으로 번역을 한다.
- javac.exe //번역 프로그램(사람언어 →컴퓨터 언어)
- 컴파일(compile) : 번역작업
- 컴파일러(compiler) :번역 프로그램 > java compiler
- C:\Program Files\Java\jdk1.8.0_261\bin
전체번역 > 컴파일러 > javac.exe
실시간 번역 > 인터프리터 > java.exe

- C:\Program Files\Java\jdk1.8.0_261\bin
- javac.exe 소스파일의 경로와 이름
- ex) D:\class\java\> javac.exe hello.java
- 컴파일의 산출물 발생 : Hello.java → (컴파일) → Hello.class
- Hello.class : 실행파일(프로그램)  → 독립 실행이 불가능하다.

3. 실행파일을 실행한다.
- java.exe //실행 프로그램(번역 프로그램, 2차 번역기)
- ex) > java.exe Hello
	           ↑
	     이 이름이

public class Hello {
	     ↑
              클래스 이름임

4. 실행 결과가 콘솔창에 보여진다.

----------------------------------------------------------------------------------------------------

★설치가 잘 됐는지 확인하는 방법
cd c:\program files\java\jdk1.8.0_261\bin 이렇게 javac.exe파일이 들어있는 jdk폴더경로 입력 후 엔터 → javac 입력
'javac.exe'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다. → JDK 설치안됨
뭔가 좌라락 나오면 → JDK 설치됨

cd c:\program files\java\jre1.8.0_261\bin 이렇게 java.exe파일이 들어있는 jre폴더경로 입력 후 엔터 → java 입력
'java.exe'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다. → JRE 설치안됨
뭔가 좌라락 나오면 → JRE 설치됨

----------------------------------------------------------------------------------------------------

★환경변수 등록
시스템속성 → 고급 시스템 속성 → 환경 변수 → 시스템변수 새로만들기

변수이름 : JAVA_HOME
변수 값 : JDK폴더들어가서 경로 복붙

변수이름 : JRE_HOME
변수 값 : JRE폴더들어가서 경로 복붙

오타있나 주의★★★

했으면

변수에서 Path 찾아서 환경변수편집(윈10)/시스템변수편집(윈7) → %JAVA_HOME%\bin 추가하기

오타있나 주의★★★

했으면

콘솔창(cmd) 닫았다 다시 띄운 후

javac 혹은 javac.exe 혹은 javac.exe -version 쳐보기

----------------------------------------------------------------------------------------------------

이클립스 플러그인 에러

Help - Install new software... 에서 주소 삽입후 Finish눌렀는데 An error occurred while collecting items to be installed 오류 발생시
Install new software... 창에서 Manage... 버튼 클릭 → 설치할 항목만 남기고 모두 체크 해제하기(다른플러그인 지워지는거 아님)
→ Apply and Close → Finish


이클립스 켤때 node.js 관련 경고알림창 뜰때
http://download.eclipse.org/wildwebdeveloper/snapshots 플러그인 설치

----------------------------------------------------------------------------------------------------

★이클립스
eclipse.org → Download → Download 버튼밑에 조그만 글씨로 Download Packages 클릭 → 우측하단에 MORE DOUNLOADS →
Eclipse 2020-06 (4.16) → Eclipse IDE for Enterprise Java Developers(톱니바퀴모양) → 운영체제에 맞게 다운

★이클립스를 다운받지않고 다른컴에서 복사했는데, 안켜지고 에러나면 99%이클립스폴더에 있는 eclipse.ini파일 경로 문제. -vm , lombok.jar 등 모두 수정

★이클립스 설정
1. Window → Preferences 검색창 encoding → utf8로 변경
2. Window → Preferences 검색창 font → size12
폰트는 1,l,I,| / 0,O,D 등이 서로 구분이 가도록 가독성이 좋아야함
①bitstream_vera_mono ②D2Coding ③NanumGothicCoding ④Consolas
3. Window → Perspective → Open Perspective → Java (웹개발시에는 Java EE)
4. 배경색 바꾸려면 Window → Preferences 검색창 appearance → Theme

★이클립스 플러그인 설치 방법
1. 마켓에서 설치 HELP - Eclipse Marketplace
2. 직접설치 HELP - Install New Software

  검색 플러그인 : quick search , http://dist.springsource.com/release/TOOLS/eclipse-integration-commons →
    Core / Eclipse Integeration Commons 체크 → Next반복 → Finish
    설치하면 단축키는 ctrl + shift + L 이나 ctrl + alt + shift + L 로 저장 되는데 바꾸는법은
    Preference → General → Keys → Quick Search → Binding → Ctrl + Shift + L → 저장
    (기존기능:Show Key Assist을 ctrl + alt + shift + L로)

  어두운 플러그인 - https://marketplace.eclipse.org/content/darkest-dark-theme#group-details
	(안되면 Marketplace에서 받아보기, 자바8버전이하는 지원이 안됨★)

  테마 변경 플러그인 : Install New Software → Work with에 http://eclipse-color-theme.github.com/update 입력후 add →
  Next → Finish → 이클립스 껏다키기 → preference → theme 검색 후 설정 (Retta/Vibrant Ink)

★이클립스
1. 모든 작업을 작업실 내에서만 해야 한다. (workspace)
2. 파일 1개를 다루더라도 반드시 프로젝트를 통해서 해야한다.

★이클립스는 실시간으로 javac.exe와 연동해서 문법을 검사한다.

★jar - 배포단위 , java에서 자주 사용하는 소스들을 만들어서 모아놓은 압축 파일
★src - source , 소스파일을 관리하는 폴더
★pakege - 자바파일을 담기 위한 폴더
★class - 자바파일을 추가

★이클립스 메소드 자동 분리기능 - 단축키 alt + shift + m
밖으로 뺄 줄들을 드래그하고 우클릭 > Refactor > Extract Method
제목입력후 확인

★이클립스 Tasks창
앞에 TODO가 붙은 주석의 폴더위치/포커스 w표시해줌
창 - Window → Show View → Tasks
설정 - Window → Preference → task 검색

todo는 이렇게 쓴다
//TODO 메모메모메모

★이클립스 단축키 설정
Preference → Keys 검색 → 검색창에 찾고자하는 기능(ex.generate gett)검색
Binding : 사용할 단축키
Conflicts : 입력한단축키를 이미 사용중인 기능
When : 어느 상황에 단축키를 사용할지 (ex.Editing Java Source)

previous tab / next tab 단축키 → ctrl+tab / ctrl+shift+tab으로 바꾸기

★Package Explorer 탭에서 양방향화살표아이콘(link with Editor) 클릭시 현재 파일 위치가 표시됨(혹은 alt+shift+w+p / opt+cmd+w+p)

★이클립스 넓게보기 하는방법
작업소스창 아무데나 한번 클릭하고 ctrl + m
이러면 작업창,콘솔창만 남고 나머지는 사라짐

안되면↓
Window → Perspective → Reset Perspective 로 리셋 → 
Window → Show View → Other → Console → Open →
console 드래그해서 작업창·편집창(edit)의 탭(파일이름들과 나란히)에 한번 붙였다가 바로 밑으로 떼기 →
이후 ctrl+m 누르면 작업창과 콘솔창 두개가 붙어있음


★이클립스 같은단어표시 안될때
상단 메뉴아이콘들중 Toggle Mark Occurrences (붓모양아이콘) 클릭 후 재시작

----------------------------------------------------------------------------------------------------

★이클립스 단축키 모음

1.  단축키 확인
  - Window > Preference > General > Keys 메뉴에서 확인
  - 단축키 보기 Hint : Ctrl + Shift + L

2. 실행
  Ctrl + F11 : 실행(바로 전에 실행했던 클래스(Run파일) 실행).
	※ 에러 났을때 디버깅을 하거나 중지점을 지정하고 검토할때는 f11,
	디버깅 모드로 강제진입을 원치않을때는 컨트롤을 붙이면 됨

3. 디버그 ★★
  F11 : 디버그 모드로 실행
  F5 : step into(현재의 명령문이 호출되는 메소드 속으로 진행하여, 그 첫 문장을 실행하기 전에 멈춘다.
        하지만 자바 라이브러리 클래스 수준까지 들어가므로 단계필터 사용을 체크(Shift + F5)를 하면
        필터를 설정한 클래스에 대하서는 Step Over 기능과 같은 기능을 수행한다.)
  F6 : step over(현재의 명령문을 실행하고 다음 명령문 직전에 다시 멈춘다.)
  F8 : 멈추어 있던 쓰레드를 다시 계속 실행한다.(Resume)
  Ctrl + Shift + B : 현재커서위치에 Break point설정 또는 해제
  Ctrl + R : 현재 라인까지 실행(Run to Line)
    Display view(표시) : Window > Show View > Other > Debug > Display를 선택하여 소스상에서
    필요한 부분을 선택해서 실행시켜 볼 수 있다.  한 순간의 값만 필요할 때 볼 수 있는 반면에 아래는 계속적으로 값이 변하는 것을 확인 할 수 있다.

4. 소스 네비게이션
  Ctrl + 객체클릭(혹은 F3) : 클래스나 메소드 혹은 멤버를 정의한 곳으로 이동(Open Declaration) ★★★
	이거 안되면 Attach Source... 버튼 클릭 후 External location > External File > jdk경로에 src.zip을 선택 > 열기
  Ctrl + Shift + G : 클래스의 메소드나 필드를 Reference하고 있는 곳으로 이동 (한개밖에없는경우 엔터) ★★★
  Ctrl + O : 해당 소스의 메소드 리스트를 확인하려 할때
  F4 : 클래스명을 선택하고 누르면 해당 클래스의 Hierarchy 를 볼 수 있다.
  Alt + Shift + R : 변수 및 메소드 일괄 변경(변경할 변수 포커스 잡고 변경 후 엔터) ★★★
  Alt + Shift + W + P + enter : 현재 파일 위치 찾아가기 ★★★
  Alt + Enter : 파일 속성창 열기

5. 소스 편집
  Ctrl + spacebar : 자동 완성 기능. 어휘의 자동완성(Content Assistance) ★★★
  Ctrl + Shift + O : 패키지(클래스) 자동으로 import 하기(사용하지 않는 Class는 삭제) ★★★
  Ctrl + Shift + M : 캐럿이 위치한 대상에 필요한 특정클래스 import
  Shift + Alt + S R : getter/setter 자동 생성 ★★★
  Ctrl + Shift + Space : 메소드 파라미터 힌트 (메소드에 입력해야 하는 파라미터 정보가 표시된다.)
  F2 : 에러의 원인에 대한 힌트 (에러 라인에 커서를 위치시키고...)
  Ctrl + Shift + / : 블록 주석(/*..*/) 추가
  Ctrl + Shift + \ : 블록 주석 제거
  Ctrl + / : 한줄 또는 선택영역 주석처리 또는 제거(//)
  Alt + Shift + J : 설정해 둔 기본주석 달기(JavaDoc 주석)
  Ctrl + S : 저장 및 컴파일
  Ctrl + Shift + F4 : 열린 파일 모두 닫기
  Ctrl + Shift + W : 열린 파일 모두 닫기
  Ctrl + W : 창 닫기
  Ctrl + Q : 마지막 편집위치로 가기 (Ctrl+클릭과 연계해서 DTO가서 멤버변수 복사해올때 사용)★★★
  Ctrl + L : 특정줄번호로 가기. 로컬 히스토리 기능을 이용하면 이전에 편집했던 내용으로 변환이 가능하다.
  Ctrl + O : 현재 편집 화면의 메소드나 필드로 이동하기
  CTRL + 휠 : 페이지 단위 이동 ★
  Ctrl + D : 한줄삭제 ★★★
  Ctrl + I : 들여쓰기 자동 수정
  Ctrl + Shift + F : 소스 정리 ★
  Alt + Up(Down) : 위(아래)줄과 바꾸기 ★★★
  Ctrl + Alt + ↑↓(상/하) : 한줄(블럭) 복사 ★★★
  변수/메소드 드래그 : 동일 지역내 동일이름 변수/메소드 위치 보기 ★
  Alt + Shift + R : 동일 지역내 동일이름 변수/메소드 일괄수정★★★
  Alt + Shift + 방향키 : 블록 선택하기 ★
  Ctrl + M : 전체화면 토글 ★★★
  Ctrl + Z / Ctrl + Y : Undo / Redo
  Ctrl + , or . : 이전 또는 다음 annotation(에러, 워닝, 북마크 가능)으로 점프
  Ctrl + T : 하이어라키 팝업 창 띄우기(인터페이스 구현 클래스간 이동시 편리)
  Ctrl + F6 : ULTRAEDIT나 EDITPLUS 의 Ctrl +TAB 과 같은 기능인데 ctrl+pgup을 바꿔서 쓰는게 낫다.
  Alt + ←→(좌/우) : 이후, 이전(뷰 화면의 탭에 열린 페이지 이동)
  Ctrl + Shift + R : Open Resource ★★
  Ctrl + Shift + ↑↓(상/하) : 다음/이전 메소드로 이동
  Ctrl + Shift + E : Switch to Editor (탭에 열려있는 Editor 이동)
  Ctrl + Shift + G : 클래스의 메소드나 필드를 Reference하고 있는 곳으로 이동
  Ctrl + 1  : Quick Fix(구현하지 않은 메소드 추가, 로컬 변수 이름 바꾸기, 행둘러싸기(if, while, for emd))
  Ctrl + 2 + R : Rename(리팩토링)
  Alt + Shift + Y : 코드 한줄보기 / 자동 줄바꿈 토글 ★★

6. 문자열 찾기
  Ctrl + K : 찾을 단어에 드래그 한후 사용하면 다음 같은 단어로 이동 ★
  Ctrl + Shift + K : 찾을 단어에 드래그 한후 사용하면 이전 같은 단어로 이동 ★
  Ctrl + J : 사용하고 문자열을 입력하면 실시간 다음 문자열 찾기
  Ctrl + Shift + J : 사용하고 문자열을 입력하면 실시간 이전 문지열 찾기
  Ctrl + F : 찾기 + 바꾸기
  Ctrl + H : 프로젝트에서 찾기

7. 템플릿 사용
  sout/syso + Ctrl + Space → System.out.println();
  try + Ctrl + Space → try-catch 문
  for + Ctrl + Space → for 문

8. 에디터 변환
  Ctrl + PgDw : 다음탭(Next Tab) → Ctrl + Tab 으로 바꾸는거 추천 ★★★
  Ctrl + PgUp : 이전탭(Previous Tab) → Ctrl + Shift + Tab 으로 바꾸는거 추천 ★★★
  Ctrl + F7 : 뷰간 전환
  Ctrl + F8 : 퍼스펙티브간 전환
  Ctrl + E : 뷰 화면의 탭에 열린 페이지 이동 ★★
  Ctrl + F6 : 열린 페이지 이동
  F12 : 에디터로 포커스 이동

9. 기타 설정
  Ctrl + w + p : Preferences

----------------------------------------------------------------------------------------------------

★(파일 내) 클래스(class) - 한가지 목적을 갖고있는 코드의 집합
	          ↓
  public class className{

클래스를 자료형(Data Type)으로 사용하는 이유는 원하는 기능만 사용하기 위함이
클래스 = 데이터 타입 생성기 (클래스도 결국 자료형이고 사용자가 정의했을 뿐이다)
String도 기본형타입이 아닌 클래스다(참조형타입)


★메소드(method) - 클래스가 갖고있는 기능, 클래스 안에 속해 선언되는 함수를 말한다

이때 입력값을 매개변수라고 하고,결과값을 리턴값이라고 합니다.
인수( Argument ) 는 어떤 함수를 호출시에 전달되는 값을 의미한다.
매개 변수( Parameter ) 는 그 전달된 인수를 받아들이는 변수를 의미한다.

----------------------------------------------------------------------------------------------------

초기화 블럭

클래스 초기화 블럭 : 클래스변수의 복잡한 초기화에 사용 (클래스가 메모리에 처음 로딩될 때 한번만 수행됨)
인스턴스 초기화 블럭 : 인스턴스변수의 복잡한 초기화에 사용 (생성자처럼 인스턴스를 생성할 때마다 수행됨. 생성자보다 먼저 수행됨.
	인스턴스 변수의 초기화는 주로 생성자를 쓰는데, 모든생성자에서 공통으로 수행돼야하는 코드를 여기에 넣으면 됨)


ex)
public class Run {
	public static void main(String[] args) {
		System.out.println(111);
		new C1();
		System.out.println(222);
		new C1();
	}
}

class C1{
	static{
		// 클래스 초기화 블럭
		System.out.println("static{}");
	}
	{
		// 인스턴스 초기화 블럭
		System.out.println("{}");
	}

	public C1(){
		System.out.println("생성자");
	}
}

결과
111
static{}
{}
생성자
222
{}
생성자

-----

ex) 스태틱메소드 사용

public class Run {
	public static void main(String[] args) {
		System.out.println(111);
		C1.m1();
		System.out.println(222);
		C1.m1();
	}
}

class C1{
	static{
		// 클래스 초기화 블럭
		System.out.println("static{}");
	}
	{
		// 인스턴스 초기화 블럭
		System.out.println("{}");
	}

	public C1(){
		System.out.println("생성자");
	}

	static void m1(){
		System.out.println("m1");
	}
}

결과
111
static{}
m1
222
m1

-----

ex) 내부클래스
class BlockTest{
	public static void main(String[] args) {
		System.out.println(111);
		BlockTest bt = new BlockTest();
		System.out.println(222);
		BlockTest bt2 = new BlockTest();
	}
	static{
		// 클래스 초기화 블럭
		System.out.println("static{}");
	}
	{
		// 인스턴스 초기화 블럭
		System.out.println("{}");
	}

	public BlockTest(){
		System.out.println("생성자");
	}
}

결과
static{}
111
{}
생성자
222
{}
생성자

----------------------------------------------------------------------------------------------------

클래스 확인하는 메소드 (기본 자료형에는 못씀)

Integer i1 = 123;

l1.getClass() → class java.lang.Integer
i1.getClass().getName() → java.lang.Integer
i1.getClass().getSimpleName() → Integer

----------------------------------------------------------------------------------------------------

★괄호/들여쓰기 스타일
1. K&R
public static void main(String[] args){
	dddasdf
	dasdasd
}
2. BSD , Allman → 가독성이 K&R보다 좋으나 , 불필요한 라인 추가됨
public static void main(String[] args)
{
	dddasdf
	dasdasd
}

----------------------------------------------------------------------------------------------------

타입(형) / 자료형 차이

기본형은 저장할 '값(data)'의 종류에 따라 구분되므로 기본형의 종류를 얘기할 떄는 '자료형(data type)'이라는 용어를 씀

그러나 참조형은 항상 '객체의 주소(4 byte 정수)'를 저장하므로 값(data)이 아닌, 객체의 종류로 구분되므로
참조형 변수의 종류를 구분할때는 '형(type)'이라는 용어를 사용함

'형(type)이' '자료형(data type)'을 포함하는 보다 넓은 의미의 용어이므로 굳이 구분하지 않고 타입만 써도 됨

----------------------------------------------------------------------------------------------------

★자료형 , Data Type - 데이터의 형태, 길이(범위)등을 미리 정의하고 분류시켜놓은 규칙

자바의 자료형
- 원시형(Primitive Type) = 값형(Value Type) = 기본형 / 참조형(Reference Type)
- byte < short, char < int < long < float < double

1. 값형(기본형, Primitive, 8개. 계산을 위한 실제 값을 저장한다)
    a. 숫자형
        ① 정수형
            ⓐ byte : 1byte (-128~127)
            ⓑ short : 2byte (-32768~32767)
            ⓒ int : 4byte (-2147483648~2147483647) -21억~21억
            ⓓ long : 8byte (-9223372036854775808~9223372036854775807) -922경~922경
        ② 실수형
            ⓐ float : 4byte(-1.40239846e-45~3.40282347e+38) 10의38승, 저장가능한수가 무수히 많으므로
                정밀도라는 표현을 사용, 수가 길어지면 뒤에 0으로 바뀌어져 손실분이 발생 (소수 이하 7자리까지 유효)
            ⓑ double : 8byte(-4.94065645841246533e-324~1.79769313486231570e+308)
                유효숫자를 저장할수 있는 양이 증가되어, float 보다 정밀도 증가 (소수 이하 16자리까지 유효)
    b. 문자형
        ① char(character) : 2byte (\u0000 ~ \uffff) 모든 종류의 데이터 저장 가능 , 대입할때 반드시
            '(홑따옴표)사용 , 1글자만 저장가능 ex)char c1 = 'g'; 여러 글자 출력시
            ex)System.out.println("" + name1 + name2 + name3); 따옴표('')를 감싸면 문자로 인식, 안 감싸면 숫자코드로 인식함
    c. 논리형
        ① boolean : 1byte (true/false. 1bit로 충분하지만 1byte인 이유는 자바에서 데이터를 다루는 최소단위가 byte이기 때문)

2. 참조형 (8개의 기본형을 제외한 나머지 타입. 객체의 주소를 저장한다(객체가 저장된 메모리주소))
    a. 문자열
        ① String : 문자열 상수(문자열 리터럴) → "(쌍따옴표 사용)
    b. 배열
    c. 클래스
        날짜시간
            ① Date 클래스 (구세대)
            ② Calendar 클래스 ☆
            ③ 다음 세대 클래스

★String은 다른 클래스와 다르게 new를 사용하지 않고 사용할 수 있는데 이때..

String str1 = "asd"
String str2 = "asd"
참조되는 값이 동일할경우 참조되는 값은 1개이다
참조변수끼리 ==비교연산을 하면 서로 같은것을 참조하는지 비교하는데 이때 true가 나온다

String str1 = new String();
String str2 = new String();
위처럼 str1과 str2는 new를 통해 각각 새로운 인스턴스를 만들어 참조하는데 이때는
저장되는 값은 같지만 str1변수와 str2변수는 서로 다르다.
==비교연산자로 연산할경우 참조하는 주소가 다르기 때문에 false가 나온다 (이떄는 equals메소드로 연산)


★클래스를 이용해서 자료의 최댓값/최소값 구하기
  byte b3 = Byte.MAX_VALUE;
  int b3 = Integer.MIN_VALUE;
                       ↑              ↑
	클래스       속성

------------------------------

★상수와 리터럴 구분 (리터럴 → 변수의 값)

상수: 변하지 않는 변수
리터럴: 변하지않는 값

int year = 2014
      변수    리터럴
final int MAX_VALUE = 100;
                    상수              리터럴

------------------------------

★자바프로그램은 리터럴을 만날시 4바이트인 int로 임의의 메모리에 저장된다
  때문에 백억이 넘는값(4바이트를 넘는값)은 상수로 저장을 못하는데
  long l2 = 10000000000L;
  이렇게 int(21억)을 초과하는 리터럴 뒤에 L을 붙이면 상수가 4바이트 대신 8바이트의 메모리에 저장되기때문에 4바이트가 넘는 값도 입력이 가능함

  같은 원리로 실수형에도 float에 넣을 숫자는 뒤에F를 붙이고,
  같은 원리로 실수형에도 double에 넣을 숫자는 뒤에D를 붙여도 되고 안붙여도 된다

  float f1 = 3.14F;
  double d1 = 3.14D;

★빈문자열(Empty String) : 프로그램상에서 필요에 따라 초기화하는 용도로 사용

★자바에서는 (지역)변수를 초기화하지 않은 상태에서는 사용(연산 , 출력 등) 할 수 없다.
  int m3; //변수를 생성하고 난 직후 , NULL상태 → 無
  System.out.println(m3);

★이스케이프 시퀀스(Escape Sequence) - 컴파일러에게 미리 약속된 행동을 하기로 미리 약속한 문자
\n - enter(개행 문자)
\r - carriage return : 캐럿(커서)의 위치를 현재 라인의 첫번째 열로 이동 = home
\t - tab
\b - backspace
\" , \' , \\ - 문자 그대로 출력

★단항 연산자 : ++ , -- , + , ~ , ! , (type)
  증감 연산자 : ++ , --
    피연산자는 숫자를 가진다
    ++num , --num : 전치 연산자(전위 연산자) : 연산자 우선 순위가 최상이 된다
    num++ , num-- : 후치 연산자(후위 연산자) : 연산자 우선 순위가 최하가 된다
    하나의 문장안에 증감 연산자와 다른 연산자를 같이 쓰지 말자!!

★산술&문자열 연산자
+ : 더하기
- : 빼기
* : 곱하기
/ : 나눈 몫 (정수만 나온다, 실수전체가 나오게 하고싶으면 둘중 아무 값이나 double로 캐스팅하기)
% : 나눈 나머지 (엑셀mod와 동일)

int a = 10;
int b = 20;
System.out.println(a + b); ← 산술 연산자
System.out.println("a" + "b"); ← 문자열 연산자
System.out.println(a + "b"); ← 문자열 연산자
System.out.println("a" + b); ← 문자열 연산자
앞에서부터 결합되어 연산되서  a+b=ab더한값
이렇게 출력하고 싶으면
a+b=(a+b) 이런식으로 작성해야함


★비교 연산자 : < , > , <= , >= ,== , != , instanceof


★비트연산자 : & , | , ^ , ~ , << , >>
1 | 2 : 2진수 or연산
1 & 2 : 2진수 and연산
1 ^ 2 : 2진수 xor연산
~1 : 2진수 not연산
x<<y : 왼쪽 쉬프트 연산. 정수x를 2진수로 바꾼후 y자리만큼 왼쪽으로 이동시킴
x>>y : 오른쪽 쉬프트 연산. 정수x를 2진수로 바꾼후 y자리만큼 오른쪽으로 이동시킴 (★빈자리는 최상위 부호비트와 같은 값으로 채워짐)
x>>>y : 오른쪽 쉬프트 연산. 정수x를 2진수로 바꾼후 y자리만큼 오른쪽으로 이동시킴 (★빈자리는 0으로 채워짐)


★논리연산자 : &&(and) , ||(or) , !(not) , ^(xor , exclusive or , 베타적 논리합)
- 피연산자를 대상으로 특정 규칙에 따라 정해진 결과값을 반환
- && , || : 2항 연산자
- ! : 1항 연산자
- 피연산자의 자료형은 bollean을 가진다
- 연산의 결과는 bollean을 반환한다
- 논리 연산자를 주로 비교 연산자와 함께 사용한다

System.out.println(age >=19 && age < 60);
System.out.println(!(age<19 || age>=60));		=위와동일

if문에서 ||(or연산자) 사용시 1항이 true이면 그 뒤의 항이 실행되지않으며
ex)
int i=0;
if( true || i++ == 99 || (i=i+2) == 999){ // 1항만 실행됨
}
System.out.println(i); // 0
if( true && i++ == 99 || (i=i+2) == 999){ // 모두 실행됨
}
System.out.println(i); // 3
if( false && i++ == 99 || (i=i+2) == 999){ // 2항은 실행되지않음
}
System.out.println(i); // 5

★조건 연산자(삼항 연산자)
조건식?참일때:거짓일때;

ex1)
int x = 15;
System.out.printf("x=%2d,10 < x && x < 20 = %s%n",x,(10 < x && x < 20)?"참":"거짓");

ex2)
int s1 = 2;
System.out.println(s1==1?1:s1>=4?"4이상":"4미만");


★복합 대입 연산자(누적 연산자) : = , += , -= , *= , /= , %= , <<= , >>= , &= , ^= , |=
- Lvalue(변수) = Rvalue(상수or변수)
- Lvalue와 Rvalue의 자료형은 반드시 동일해야 한다.

ex) 하나라도 false가 있는경우 false, 전부 true인경우 true
boolean result = true;
for (MaterialCheckBox item:weekday){
	result &= item.getValue();
}

ex) 하나라도 true가 있는경우 true, 전부 false인경우 fasle
boolean result = false;
for (MaterialCheckBox item:weekday){
	result |= item.getValue();
}

ex) &= 과 !로 널(true)체크시 응용 (하나라도 널이 있으면 true 반환)
private boolean timeCheckNull(MaterialTimePicker sTime, MaterialTimePicker eTime) {
	return !(sTime.getValue() == null && sTime.getValue() == null);
}
ex) &= 과 !로 널(false)체크시 응용 (하나라도 널이 있으면 true 반환)
private boolean weekCheckNull(MaterialCheckBox ...weekday) {
	boolean result = true;
	for (MaterialCheckBox item:weekday){
		result &= item.getValue();
	}
	return !result;
}


★연산자 우선순위 높은순
단항 > 산술(*,/,%) > 산술(+,-) > 시프트 > 관계(<,<=,>,>=) > 비트 > 논리(&&, ||) > 삼항 > 대입 > 후위증감

----------------------------------------------------------------------------------------------------

StringBuffer 클래스

문자열에 +연산을 할경우 내부적으로 StringBuffer클래스가 호출되고
더하는 값이 append()메소드로 더해지게 된다 이후 toString()메소드로 String형으로 리턴된다
String s1 = "가나" + "다라";
String s2 = new StringBuffer().append("가나").append("다라").toString()

때문에 문자열을 반복문내에서 더할경우 +연산자로 하기보다
직접 StringBuffer객체를 하나 만들어서 그객체에 append()로 계속 추가시키는게 성능에 좋다

----------------------------------------------------------------------------------------------------

진법(진수) 변환

Integer.parseInt / Integer.toString / Integer.toBinaryString / Integer.toOctalString / Integer.toHexString

진법이 자동 변환되는 경우 : 숫자 앞에 0이나 0x가 붙을때 8진수나 16진수로 입력받고 출력은 무조건 10진수로 된다
int num = 10; → 10진수
int num = 010; → 8진수
int num = 0x10; → 16진수
∴연산할때 빼고 상품번호 , 전화번호 , 주민등록번호 등은 문자열로 처리해야함 (String)
  (나이 → 숫자 혹은 문자열)

-----

★n진수를 10진수로 변환

n진수 → 10진수 : Integer.parseInt("n진수값", 바뀌기 전 진수)

ex) 2진수 1010을 10진수로
Integer.parseInt("1010", 2) → 10

ex) 16진수 A를 10진수로
Integer.parseInt("A", 16) → 10

-----

★10진수를 n진수로 변환

방법1.
10진수 → n진수 : Integer.toString(10진수값, 바뀐 이후 진수)

방법2.
10진수(&실수) → 2진수 : (String) Integer.toBinaryString(n)
10진수(&실수) → 8진수 : (String) Integer.toOctalString(n)
10진수(&실수) → 16진수 : (String) Integer.toHexString(n)

----------------------------------------------------------------------------------------------------

★주석 단축키
단일라인 : ctrl + /
단일라인 해제 : ctrl + /
다중라인 : ctrl + shift + /
다중라인 해제 : ctrl + shift + \

★코드조각(Code Template) 단축키 (만약 한번에 안되고 두번을 눌러야 나오고 이러면... 이클립스 재설치가 가장 빠른 답)
main 혹은 ma까지만 치고 ctrl + space 후 엔터
syso 혹은 sout 치고 ctrl + space 시 자동완성

Preferences > template 검색 후 다시 General 말고 Java를 찾기 > Editor > Templates

ex)
Name : bfread
Context : Java statements //새로운 파일을 만들때 입력되있게 할건지, ctrl+space로 입력할건지
Description : 버퍼드 읽기세팅
Pattern : BufferedReader reader = new BufferedReader(new FileReader(PATH));

${} 이걸로 묶으면 포커스가 그어져있게 만들 수 있음★
${DATA_TYPE} ${DATA_TYPE} ${c2} (여러개 동시에도 가능, 이름 다르게 하면 탭으로 이동가능하게 자동설정됨)

insert Variable... 버튼클릭시 아래 내용 등을 변수로 추가되게 할수 있다★

${class_name} → 클래스명 (Member_list)
${file} → 파일명 (Member_list.java)
${enclosing_method_arguments} → 메소드명
${enclosing_method_arguments} → 메소드 파라미터
${enclosing_package} → 패키지명
${enclosing_project} → 프로젝트명 (Context Root Path를 지정했다면 꼭 수정해야함)
${cursor} → 커서만
${date} → 현재날짜
${time} → 현재시간


★인텔리센스(Code Asist)
System치고 .찍으면  관련항목이 목록으로 나옴
녹색 선이 나올때 탭 누르면 녹색선으로 이동됨


★개발환경 세팅 내보내기/불러오기

1. 내보내기
File>Export>General>Preferences>저장될 경로 및 이름 지정

2. 불러오기
File>Import>General>Preferences
브라우저버튼 클릭해서 파일 찾고
피니쉬 버튼 클릭

----------------------------------------------------------------------------------------------------

★프로젝트 불러오기
파일탐색기에서 프로젝트 폴더를 수동으로 넣은다음
이클립스에서 File → Import → Existing Projects into Workspace → Browse...버튼 → 프로젝트폴더 부모폴더 폴더선택 → Finish

----------------------------------------------------------------------------------------------------

★변수 초기화 : 변수를 선언 후 값을 처음 할당하는 것

★변수 선언시 선언과 초기화를 한번에 작성하는것
byte aa;
aa = 3;
      ↓
byte aa = 3;

byte a1 = 3;
byte a2 = 3;
         ↓
byte a1 = 3 , a2 = 3;

----------------------------------------------------------------------------------------------------

★변수명 사용시
1. 영문자 , 숫자 , _ , $ 만 사용
2. 숫자 시작 X
  1abc → _1abc
3. 예약어 사용불가 (문법에서 사용하는 특정 단어)
4. 의미있게 (웬만하면 약자말고 풀네임으로)

----------------------------------------------------------------------------------------------------

★변수표기법

1. 헝가리안 표기법 - 접두어로 해당 자료형을 표시하는 방법
  ex) int number; → int inumber/ int i_number; / int int_number;
  주사용처 : 인터페이스
  그러나 변수에 마우스 갖다댈시(hover) 자료형이 나오기때문에 요즘은 잘 안씀

2. 파스칼 표기법 - 첫문자를 항상 대문자 표기
  식별자가 2개 이상의 단어로 만들어지면 각 단어의 첫문자도 대문자로 표시
  ex) int notesize; → int NoteSize;
  주사용처 : 클래스명

3. 카멜 표기법 - 단어 결합시 첫글자 대문자표기 (낙타모양이라)
  ex) int notesize; → int noteSize;
  주사용처 : 변수명 , 메소드명 (클래스명과 구분을 위해 사용)

4. 스네이크 표기법/팟홀 표기법/언더바 표기법 - 단어 결합시 _(언더바) 사용 (_가 뱀모양이라)
  ex) int notesize; → int serial_number;
  주사용처 : 카멜 대용/기타등등

5. 케밥 표기법 - 단어 결합시 -(하이픈/대쉬) 사용 (-가 꼬챙이(케밥)모양이라) ★자바에서는 -가 연산자로 인식되기때문에 못씀 , 웹에선 가능
  ex) int notesize; → int serial-number;

----------------------------------------------------------------------------------------------------

★출력 명령어
  ① System.out.println();	print line - 출력+개행(내용물을 출력한 뒤에 개행(줄바꿈)을 한다)
           ↑        ↑        ↑
       클래스 필드 메소드
  ② System.out.print();	print - 출력 (내용물 출력만)
  ③ System.out.printf();	print format - 출력 (형식문자열을 이용해서 형식을 변경해서 출력하는데 편리한 메소드 , 구문은 c언어와 동일)
	String name = "한가인";
	System.out.printf("안녕하세요. %s님. 반갑습니다. %s님.\n",name,name);

★printf 형식문자열 종류
    1. %s : String
    2. %d : Decimal(byte , short , int , long)
    3. %f : Float (float , double)
    4. %c : Char - 형식문자 %c는 숫자를 전달하면 해당 숫자의 문자를 출력한다
    5. %b : Bollean
    6. %n : New Line

System.out.println(kor + " + " + eng + " + " + math + " = " + (kor + eng + math));
System.out.printf("%d + %d + %d = %d\n",kor,eng,math,kor + eng + math);

★형식 문자 추가 기능

1. 넓이 지정
%와 d 사이에 +- 정수를 넣어 박스크기를 지정
+(박스우측정렬)
-(박스좌측정렬)
System.out.printf("가나다%-10d라마바사",123) → 넓이 10의 박스안에 123을 좌측정렬

2. %d , %f 에 통화형식(3자리마다 콤마) 지정 가능
% 뒤에 ,(콤마) 넣기
System.out.printf("%,d",1200);
System.out.printf("%,4d",1200); → n번째마다 컴마찍기

3. %f 사이에 .0 .1 .2 이렇게 넣으면 소수 자리수 조절 가능
System.out.printf("%,.3f",3.141592);

4. %d , %tT 등 사이에 0n을 넣으면 n만큼 빈자리에 숫자 0이 생김 (= 엑셀/엑세스 표시형식 0)
System.out.printf("%02d:%02d:%02d",8:14:7)

★숫자 표기시 반드시 단위 명시!

----------------------------------------------------------------------------------------------------

줄바꿈 escape 문자

\n - unix
\r - mac
\r\n - windows

한가지를 사용하면 시스템에 따라 줄바꿈이 되지 않을 수도 있음

----------------------------------------------------------------------------------------------------

★입력(input) 명령어
  ① read() : 잘안씀
    - 입력한 문자의 문자코드값을 가져오는 메소드(x)
    - read메소드는 입력 버퍼 안에 들어있는 문자를 가져오는 메소드(o)
    - 한번 실행에 1글자만 반환한다.
    - 바이트 단위의 읽기도구 (한번에 1byte씩만 읽는다.)
  ② BufferedReader 클래스 : 실사용 (Enter로만 구분 가능, 데이터가 String으로 고정, 작업속도가 빠르다)
  ③ Scanner 클래스 : 실사용 (Enter, Space로 구분 가능)

System.in.read(); 입력 대기 상태 → 블럭 걸렸다.

입력을 하면 System.in.read() 이 문장이 입력받은 값으로 바뀜
그래서 앞에 변수를
int data = System.in.read();
이처럼 미리 앞에 적어주면 사용자가 적은 문장이 변수에 대입되게 된다

System.in.read();
reader.read(); 문자코드 1개를 '숫자값으로' 반환 - 입력받은 문자의 문자 코드값이 필요한 경우 사용
reader.readLine(); 문자열을 통째로 '문자값으로' 반환 -  입력받은 문자의 문자 코드값이 필요하지않은 경우 사용

ex) String data1 = reader.readLine();

★※주의 : 스캐너가 이상하면 이전에 스캐너가 읽고 난 뒤 엔터가 남아있어서 nextLine을 무시하고 통과해버리는 거라고함
scanner.nextLine();
빈 nextLine() 혹은
scanner.nextInt();
scan.skip("\r\n");
를 추가해서 엔터를 없애야함

그리고 웬만하면 문자로 받아서 숫자로 바꾸는게 좋음(숫자받기 문자받기 섞어쓰는것도 안좋음) 웬만하면 오직 문자로만 받기

입력받자마자 바로 숫자형으로 바꾸기
int data = Integer.parseInt(reader.readLine());

★문자코드 암기
A(65) ~ Z(90) 26개
a(97) ~ z(122) 26개
0(48) ~ 9(57) 10개
A(65) , a(97) , 0(48) ← 이건 꼭 암기
가(44032) ~ 힣(55203) : 11,171 (완성형한글에 등록되어있는 한글 개수)

★scanner 사용시
Scanner scanner = new Scanner(System.in);

System.out.println("문자열입력: ");
String str = scanner.nextLine();
System.out.println(str);

System.out.println("정수입력: ");
int i = scanner.nextInt();
System.out.println(i);

System.out.println("실수입력: ");
double j = scanner.nextDouble();
System.out.println(j);


★scanner next()사용해서 한 단어씩 공백으로 읽기

Scanner scan = new Scanner(System.in);

System.out.print("입력 : ");
String data = "";
while(scan.hasNext()){
	data = scan.next();
	System.out.println("출력 : " + data);
}


★split으로 문자열 끊어서 읽기 - String[] 반환

split("정규식")

Scanner scan = new Scanner(System.in);

System.out.print("입력 : ");
String data = scan.nextLine();
String[] result = data.split(",");

for (String str : result) {
	System.out.println(str);
}


한글자씩 끊어읽기
"asd".split("")
결과 : [a,s,d]


+ 나 . 등의 기호을 쓸때는 \\+ 이런식으로 써야함 or 대괄호 안에 넣거나

----------------------------------------------------------------------------------------------------

StringTokenizer, 문자열 끊어읽기(split와 달리 빈 문자열을 토큰으로 인식하지 않음)

String s1 = "사과 배 복숭아   밤 대추, 포도   . 참외      ";
StringTokenizer st1 = new StringTokenizer(s1); //기본적으로 Space와 Tab을 구분기호로 사용
StringTokenizer st1 = new StringTokenizer(s1,",. \t\r\n"); //쉼표,점,공백,탭,엔터를 구분자로 사용
StringTokenizer st1 = new StringTokenizer(s1,",. \t\r\n",true); //구분자까지 출력

st1.hasMoreTokens() //다음 읽을 문자열이 있으면 true, 없으면 false 반환
st1.nextToken() //다음 토큰 반환

-----

String s = "100,,,200,300";

이런 문자열이 있다고 했을때

String[] split = s.split(",");
으로 할경우 [100, , , 200, 300] 이 나오지만

StringTokenizer tokenizer = new StringTokenizer(s, ",");
로 하면 100, 200, 300 만 나오게 할 수 있음

----------------------------------------------------------------------------------------------------

.toUpperCase() : 문자열을 대문자로 반환
.toLowerCase() : 문자열을 소문자로 반환

----------------------------------------------------------------------------------------------------

문자를 char로 반환

char c = "a".charAt(0);

----------------------------------------------------------------------------------------------------

★toCharArray

문자열을 char 배열로 반환

문자열.toCharArray()

ex)
char[] arr = "asd".toCharArray();
System.out.println(arr[0]); → a 
System.out.println(arr[1]); → s

----------------------------------------------------------------------------------------------------

★chars

문자열을 int(문자코드) IntStream으로 반환

문자열.chars()

ex)
"asd".chars().toArray() → [97, 115, 100]

----------------------------------------------------------------------------------------------------

char를 int(문자코드)로 변환 후 출력 (c언어는 printf %d로 바로 출력 가능)

char c = 'a';
System.out.println((int)c); → 97

이것도 되긴함
System.out.println(c+'0'-'0'); → 97

----------------------------------------------------------------------------------------------------

숫자char를 int(자료형만)로 변환

char c = '5';
System.out.println(c == 5); → false
System.out.println(c-'0' == 5); → true (원리 : 53-48 == 5) (빼기(-)연산이므로 상황에따라 ()괄호로 감싸 먼저 연산시켜야함)
System.out.println(Character.getNumericValue(c) == 5); → true

----------------------------------------------------------------------------------------------------

char를 String으로 변환 / 비교

(char) 97 → a
Character.toChars(97) → a

(c+"").equals("a") → true

----------------------------------------------------------------------------------------------------

버퍼드 출력 (println 보다 빠름)

BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

String s1 = "가나다라";
bw.write(s1); //.append도 있으나 write와 거의 비슷함
bw.flush(); //출력
bw.close(); //종료

----------------------------------------------------------------------------------------------------

★자료형을 변화시키는 메소드

문자열 → byte : Byte.parseByte("10")
문자열 → short : Short.parseShort("10")
문자열 → int : Intger.parseInt("10") ★가장 많이 사용
문자열 → long : Long.parseLong("10")

문자열 → float : Float.parseFloat("10")
문자열 → double : Double.parseDouble("10")

문자열 → boolean : Boolean.parseBoolean("10")

int → 문자열 : Integer.toString(100)
int → 문자열 : String.valueOf(100)
int → 문자열 : 100 + "" ★가장 많이 사용

char c1 = 'A';
String c2 = "A";
컴파일러는 위의 두 A는 다른 문자라고 인식 ( 1과 "1"이 다른 것처럼 자료형이 달라서)


★문자코드 1글자 알고싶을때
System.out.println(int = 'd');

★문자코드를 문자로 출력
System.out.printf("%c",65);

★예외처리 코드 - 제대로된 사용법을 지키지 않아 발생한 오류를 처리하기 위한 코드 (보통 if문 사용)

★charAt - 위치로 문자값 1개 추출(반복문과 활용가능)
- String(문자열)을 ★char(문자) 또는 int(문자코드)로 반환 (주로 유효성검사시 for문과 함께 한글자씩 검사할때 사용)
String txt = "ABCDEF";
(char or int) c1 = txt.charAt(1) → (B or 66)

★마지막 글자값(char) 구하기 - 글자수에서 1을 빼면 됨 (0번지부터 시작하기 때문)
txt.charAt(str.length()-1)

★substring - 위치로 문자 1개 이상 추출 (String으로 반환) ★substring(inclusion,exclusion)
- string 형으로 반환된걸 다시 int로 변경가능하기때문에, char형으로 반환받는 charAt대신 유용하게 사용가능
String txt = "가나다라마바사";
txt.substring(3,4) → 라
위처럼 앞 숫자(1)는 추출대상에포함되고 뒤 숫자(3)는 포함되지 않음 (-1까지 포함)
☆length()는 1부터 시작하기때문에 자동으로+1이라서 substring의 두번째 인수에 넣기 좋음

★indexOf - 글자의 위치 구하기 (못찾으면 -1 반환)   ★indexOf(찾을문장,[검색을 시작할 위치])
String txt = "안녕하세요안녕"
int index = txt.indexOf("하"); → 결과:2
int index = txt.indexOf("하세"); → 결과:2 (문자가 2글자이상인경우 문장의 시작위치)
int index = txt.indexOf("안",1); → 결과:4
☆indexOf / lastIndexOf는 0부터 시작하기때문에 substring의 첫번째 인수에 넣기 좋음

★뒤에서부터 단어/글자 찾기 lastIndexOf
String txt = 감자돌멩이감자튀김;
lastIndexOf(txt.lastIndexOf("감자") → 5

★contains - 문자열에 특정 문자열이 포함되어 있으면 true 반환
"ab6CDE443fgh".contains("6CD") → true

★replace - 문자열 치환(바꾸기)
- String형으로 반환
- indexOf 와 달리 모두교체
- 업데이트가 아닌 복제라서 변수 만들거나 원본데이터 변수에다 대입해야함

String txt = "안녕하세요. 한가인입니다.";
txt = txt.replace("한가인","박수진"); → 안녕하세요. 아무개입니다.

삭제할때 자주 사용
relplace("하세요","");
relplace(" ",""); → 모든공백제거


★replaceAll - replace와 동일하나 정규식 사용 가능(특정 문자여러개를 변경가능)
my_string.replaceAll("[a-zA-Z]","")
replaceAll("^ \\+ ","") → " + " 로 시작하는 문자열을 제거

★trim 메소드 - 양끝 공백 제거
txt1.trim()

★띄어쓰기 구분없이 검색하는 방법
if (content.replace(" ","").indexOf(word.replace(" ",""))>-1) {}


★matches - 정규식 이용 가능 (문자열이 문자인지 숫자인지 판별 가능)
문자열.matches("정규식")

아래처럼 써도 됨
java.util.regex.Pattern 클래스의 정적 메소드인 matches() 메소드
boolean result = Pattern.matches("정규식", "검증할 문자열");

----------------------------------------------------------------------------------------------------

정규식

------------------------------

Pattern 클래스

String pattern = "^[0-9]*$"; // 숫자만 등장하는지
String str = "123321";

boolean result = Patern.metches(pattern, str)
System.out.println(result); // true


Pattern 메소드
compile(String regex) : 정규표현식으로 패턴 생성
matcher(CharSequence input) : 대상 문자열이 패턴과 일치할 경우 true 반환
asPredicate() : 문자열을 일치시키는데 사용할 수 있는 Predicate 작성
pattern() : 컴파일된 정규표현식을 String형태로 반환
split(CharSequence input) : 문자열을 주어진 인자값 CharSequence 패턴에 따라 분리

------------------------------

Matcher 클래스


Pattern pattern = Pattern.compile("정규식");

String str = "asdf";

Matcher matcher = pattern.matcher(str);

System.out.println(matcher.find());


Matcher 메소드
matches() : 대상 문자열과 패턴이 일치하는 경우 true 반환
find() : 대상 문자열과 패턴이 일치하는 경우 true 반환하고 그 위치로 이동
find(int start) : start 인자로 받은 위치부터 매칭 체크
start() : 매칭되는 문자열의 시작 위치를 반환
start(int group) : 지정된 그룹이 매칭되는 시작 위치 반환
end() : 매칭되는 문자열의 끝 바로 다음 위치를 반환
end(int group) : 지정된 그룹이 매칭되는 끝 바로 다음 위치를 반환
group() : 매칭된 부분 반환
group(int group) : 매칭된 부분 중 group번째 그루핑 매칭부분을 반환
groupCount() : 패턴내 그룹핑한 전체 개수를 반환

------------------------------

정규식 문법

^		: 문자열의 시작
$		: 문자열의 끝
.		: 임의의 한 문자
*		: 문자가 0번 이상 발생
+		: 문자가 1번 이상 발생
?		: 문자가 0번 혹은 1번 발생
[]		: 문자의 집합 범위를 나타냄. 괄호 안에서 ^를 쓰면 부정의 의미가 됨
{}		: 횟수 또는 범위를 의미
()		: 소괄호 안의 문자를 하나의 문자로 인식
|		: or 조건
\		: 확장 문자의 시작
\b		: 단어의 경계
\B		: 단어가 아닌 것의 경계
\A		: 입력의 시작 부분
\G		: 이전 매치의 끝
\z		: 입력의 끝
\Z		: 입력의 끝이지만 종결자가 있는 경우
\s		: 공백 문자
\S		: 공백 문자가 아닌 나머지 문자
\w		: 알파벳이나 숫자
\W		: 알파벳이나 숫자를 제외한 문자
\d		: [0-9]와 동일
\D		: 숫자를 제외한 모든 문자

------------------------------

자주 사용하는 정규식

숫자			: ^[0-9]*$
영문자		: ^[a-zA-Z]*$
한글			: ^[가-힣]*$
이메일 주소	: \\w+@\\w+\\.\\w+(\\.\\w+)?
전화번호		: ^\d{2,3}-\d{3,4}-\d{4}$
휴대폰번호	: ^01(?:0|1|[6-9])-(?:\d{3}|\d{4})-\d{4}$
주민등록번호	: \d{6} \- [1-4]\d{6}
우편번호		: ^\d{3}-\d{2}$

html모든 태그	: <(/)?([a-zA-Z]*)(\\s[a-zA-Z]*=[^>]*)?(\\s)*(/)?>
(<br>, <p>, </p> 등등)

-----

색상 코드가 아닌(16진수가 아닌) 문자들을 제거

inp.addKeyUpHandler(e -> {
	String txt = inp.getText();
	String cleanedTxt = txt.replaceAll("[^0-9a-fA-F]", "");
	if (cleanedTxt.length() > 6)
		cleanedTxt = cleanedTxt.substring(0, 6);
	inp.setText(cleanedTxt);
});

----------------------------------------------------------------------------------------------------

★"아이린"을 문서내에서 계속 찾기
int idx = -1;
while(true) {
	idx = txt.indexOf("아이린",idx);
	if (idx == -1) {
		break;
	}
	System.out.printf("%d번째에서 발견",idx);
	idx += "아이린".length();
}

★유효성검사 (한글/숫자/영문소문자/영문대문자 만 입력받기) → 잘못된걸 찾는게 편함 → 잘못된걸 찾으면 for문 탈출(뒤에 남은 문자는 검사할 가치가 없기때문)

문자열(String) → X
문자(char) → O

String txt = "testjavaDSFSDFㄴㅁㅇㅁㄴㅇ";
result=false;
for (int i=0; i<txt.length(); i++) {
	char c = txt.charAt(i);
	if ((c<'0' || c>'9') && (c<'a' || c>'z') && (c<'A' || c>'Z') && (c<'가' || c>'힣')){
		result=false;
		break;
	}
}
if(result == flase){
	System.out.println("잘못된 문자를 입력하셨습니다");
}


★유효성 검사 - 금지어
String txt = reader.readLine();
		
String ben = "바보";
if (txt.indexOf(ben) == -1) {
	System.out.println("글쓰기 완료");
}else {
	System.out.println("글쓰기 불가");
}

★대소문자 변환 toUpperCase / toLowerCase
String content = "우리가 배우는 과목은 java입니다.";
String word = "jAva";
content = content.toUpperCase();
word = content.toUpperCase();
if (content.indexOf(word) == -1) {
	System.out.println("없슴");
}else{
	System.out.println("있슴");
}

★첫번째 문자 / 마지막 문자 판별 (논리값반환)
System.out.println(name.startsWith("아"));
System.out.println(name.endsWith("린"));

System.out.println(name.charAt(name.length()-1)==('린'));
System.out.println(name.indexOf("린") == name.length()-1);
이것도 가능


★전체경로에서 파일명 구하기
String path = "E:\\class\\java\\JavaTest\\src\\com\\test\\String.java";
int index = path.lastIndexOf("\\");
String fileName = path.substring(index+1,path.length());
System.out.println(fileName);

index = fileName.lastIndexOf(".");
String ext = fileName.substring(index);
System.out.println(ext);

String fileNameWithoutExt = fileName.substring(0,index);
System.out.println(fileNameWithoutExt);

int no=1;
System.out.println(fileNameWithoutExt + "[" + no + "]" + ext);

no ++;
System.out.println(fileNameWithoutExt + "[" + no + "]" + ext);


★String.format() - 형식문자열 (printf와 문법 동일)
String name = "이다희";
String result = String.format("이름 : %s", name);
ex) 왼쪽에 0으로 채워서 6자리로 맞추기
String.format("%06d", 1234)


★메소드의 대부분은 상호 배타적이다 (다른 메소드가 한 일의 경과를 자신의 일과 연관짓지 않는다)
	indexOf는 검색어가 여러개 발견되도 무조건 첫번째 검색어의 위치를 반환하다.

----------------------------------------------------------------------------------------------------

★형변환(casting)
- 값형간의 가능. int → double
- 참조형간의 가능. A → B
- 값형과 참조형간의 변환은 불가능. String → int , int → String

암시적인 형변환(자동 타입 변환) 작은것에서 큰것으로(문제가발생하지않으니 형변환연산자를 안적어도됨) 하지만 암시적인 형변환이여도 적는게 좋다!
- 큰타입 = 작은타입
- 100% 안전

명시적인 형변환(강제 타입 변환) - 큰것에서 작은것으로(이 작업은 문제가 발생할 소지가 있기때문에 개발자 네가 반드시 정신차리고 봐라 라는뜻)
- 작은타입 = 큰타입
- 경우에 따라 다름
- 명시적인 형변환이 발생할만한 복사에서는 원본의 값이 복사본 타입의 범위를 벗어나는지 반드시 확인한다!!!!

byte b1 = 10;
short s1 = (short)b1;

★형변환은 참조변수의 타입을 변환하는 것이지 인스턴스를 변환하는 것은 아니기 때문에 참조변수의 형변환은 인스턴스에 아무런 영향을 미치지 않는다.
단지 참조변수의 형변환을 통해서, 참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위(개수)를 조절하는 것뿐이다.

★조상타입의 인스턴스를 자손타입의 참조변수로 참조하는 것은 허용되지 않음

----------------------------------------------------------------------------------------------------

멤버

클래스의 구성요소
멤버에는 3가지 종류가 있다

1. 필드(Field) : 객체의 데이터가 저장되는곳
2. 생성자(Constructor) : 객체 생성시 초기화 담당
3. 메소드(Method) : 객체의 동작에 해당되는 실행 블록

멤버들은 생략되거나 복수개가 작성될 수 있음

----------------------------------------------------------------------------------------------------

업캐스팅(UpCasting)

자식 클래스가 부모 클래스 타입으로 형변환되는것
업캐스팅은 캐스팅 연산자 괄호를 생략할 수 있음
단, 부모의 클래스로 캐스팅된다는것은 멤버의 갯수 감소를 의미하는데, 이는 곧 자식 클래스에만 있는 속성과 메소드는 실행하지 못한다는 뜻
업캐스팅을 하고 메소드를 실행할 때, 만일 자식 클래스에서 오버라이딩한 메소드가 있을경우, 부모클래스의 메소드가 아닌 오버라이딩된 메소드가 실행되게 됨

업캐스팅 하는 이유
공통적으로 할 수 있는 부분을 만들어 간단하게 다루기 위함. 서브클래스가 몇 개든 하나의 인스턴스로 묶어서 관리가 가능

------------------------------

다운캐스팅(DownCasting)

거꾸로 부모클래스가 자식클래스로 형변환되는것
다운캐스팅은 괄호를 생략할 수 없다

-----

다운캐스팅의 목적

부모클래스로 업캐스팅된 자식클래스를 복구하여, 본인의 필드와 기능을 회복하기 위해 있는 것이다
즉, 원래 있던 기능을 회복하기 위해 다운캐스팅을 하는것

-----

주의사항

다운캐스팅의 목적은 "업캐스팅한 객체를 되돌리는"데 있다
그래서 업캐스팅되지 않은 생 부모 객체를 다운캐스팅하면 오류가 발생한다(java.lang.ClassCastException)
무분별한 다운캐스팅은 컴파일오류는 안나도 런타임오류를 발생시킬 가능성이 있다
따라서 다운캐스팅을 다룰 때에는 다운캐스팅할 객체가 오리지날 부모 객체인지, 업캐스팅된 부모 객체인지 항상 머릿속에서 다운캐스팅이 가능한지 생각해볼 필요가 있다

다행인 점은 이렇게 혼동되는 객체를 구별하기 위해 도움을 주는 연산자를 자바에서 지원해준다 → instanceof 연산자

참조캐스팅을 잘못했다가 런타임환경에서 에러가 나 프로그램이 종료돼 버리면 서비스에 크나큰 차질이 생기게 된다
따라서 코드 디버깅을 많이 하며 미리 예방하는게 베스트지만, 이마저도 부족하면 업캐스팅/다운캐스팅 유무를 검증하여 참조 캐스팅 동작을 결정하면 된다

ex) 사용예시
자식객체 instanceof 부모클래스

사용시 주의할 점은 instanceof 연산자는 객체에 대한 클래스(참조형) 타입에만 사용할 수 있다는 점이다(int, double같은 원시형(primitive타입)에는 사용 불가능)

----------------------------------------------------------------------------------------------------

모든 정수형 자료는 int로 바뀌기때문에
byte b1 = 10;
이렇게 해도
byte b1 = (byte)10;
이처럼 10이라는 값이 int로 저장되고 다시 byte로 바뀌어 저장된다

그래서 대부분이 int를 주로 씀

★모든 실수형 자료는 double로 바뀌는데
float f1 = 3.14F;
이것도 원래는 double형을 float로 바꾼
float f1 = (float)3.14;
이문장인데 매번 적기 번거롭기 때문에 끝에 F를 붙이는걸로 대신하게되었음

★실수를 정수형으로 바꿀때
int m1;
double m2 = 3.14;

m1 = (int)m2;

이런식으로 하면 뒤의 소수값이 날아가고 정수값만 남게된다.


★자료 길이 순서는 byte < short <int < long < float < double
  float는 4바이트지만 표현할수 있는 수는 long보다 훨씬 많다
  char은 short와 int 중간쯤에 위치 , char는 문자이지만 숫자취급하기때문에 , 형변환을 통해 문자를 문자코드로 바꾸거나 문자코드를 문자로 바꿀 수 있다
  char을 문자코드로 상호 변환할 때는 반드시 int를 사용해야 한다 (short X)

★연산자의 종류
1. 산술 연산자 : - , + , * , / , %(mod)
  - 2항 연산자
  - 피연산자를 숫자로 가진다(정수 , 실수)

★나누기 연산자는 모든 산술 연산의 결과 자료형은 두 연산자의 자료형 중 "더 큰 자료형"으로 반환된다
정수/정수 = 정수
실수/정수 = 실수
정수/실수 = 실수
실수/실수 = 실수
System.out.println(10 / 3); → int / int		→ 3
System.out.println(10.0 / 3); → double / int	→ 3.333…
System.out.println(10 / 3.0); → int / double	→ 3.333…

★연산에 의해서 표시할수 있는 값의 범위를 초과할 수 있다 = overflow:위로 넘치는 현상 / underflow:아래로 넘치는 현상 → 둘 다 overflow라고 표현
int n1 = 2000000000; → 20억
int n2 = 2000000000; → 20억
System.out.println(n1 + n2); → 21억 초과
때문에 둘중 하나를 long으로 만들어야함
System.out.println(n1 + (long)n2);

+ : 신경 쓸 것
- : 신경 쓸것
* : 더욱 신경 쓸 것
/ : 전혀 신경 안 써도 됨

----------------------------------------------------------------------------------------------------

메모리 영역(구역)

★Heap(Managed Heap) 영역

문자열을 저장하면 값이 자료형에 따라 heap에 생성되고 그 값이 들어간 주소가 stack영역에 담김
값이 비교되는게 아니라 값이 있는 번지수만 비교됨

배열은 연속된 공간에 저장돼있고 배열의 값이 참조형일경우 또 참조함

객체를 new연산자로 만들면 값이 heap영역에 생성되고 그 값이 들어있는 주소가 stack영역에 담김

heap에 저장된 데이터가 더이상 필요없어지면 메모리 관리를 위해 JVM에 의해 알아서 해제됨(가비지컬렉션)
몇개의 Thread가 존재하든 단 하나의 heap영역만 존재

-----

★Stack 영역

Heap영역에 생성된 Object타입 데이터의 참조변수가 할당된다
원시타입의 데이터가 저장되는 공간

지역변수와 매개변수가 저장됨

메소드가 호출될때 생성되고 메소드실행이 끝나면 제거됨
LIFO구조로, 변수에 새로운 데이터가 할당되면 이전 데이터는 지워짐

각 Thread는 자신만의 stack을 가진다

-----

★static 영역

필드에 선언된 변수(전역번수)와 정적 멤버변수(static이 붙은 자료형)는 static에 저장됨.

static영역의 데이터는 프로그램의 시작부터 종료까지 메모리에 남아있게됨 (어디서든 사용 가능)
무분별하게 사용시 메모리가 부족할 우려가 있음

----------------------------------------------------------------------------------------------------

equals() 메소드


Object클래스의 메소드임

==연산자는 피연산자가 primitive type(원시형)(int, char, double, boolean, ...)일 때는 값이 같은지 비교하고,
피연산자가 그 외 객체, reference type(참조형)일 때는 같은메모리인지(Constant Pool내의 주소)를 비교함


문자열(String)의 내용을 비교할때  ==연산자를 쓰면 안됨
두 객체가 다른주소를 가르키더라도, 같은문자열이면 동일하게 판단하기 위해, 각 자리마다 비교하도록 재정의된 equals메소드를 사용해야함

ex1)
String s1 = "가나다";
String s2 = new String("가나다");
System.out.println(s1 == s2); → false

ex2)
String s4 = "이";
String s5 = "이열음";
s4 = s4 + "열음";
System.out.println(s4 == s5); → false

==로 비고하면 true가 나와야 하는데 주소가달라서 false가 나옴


본디 equals메소드는 그냥 == 한것과 같이 주소값끼리 비교하지만
String클래스에서는 기본적으로 equals가 재정의되어있어서, a.equals(b) a와 b의 주소값이같거나,
주소값이 다르더라도 a와 b의 한글자한글자가 모두 일치한다면 true를 반환함

또 클래스에서 equals메소드를 재정의 해줄경우 특정 필드값이 같을경우 true가 반환되도록 할 수 있음.

이때 hashCode메소드도 같이 재정의 하는것이 좋은데

hashCode메소드까지 같이 재정의해야 hash기반 컬렉션(HashMap,HashSet,HashTable)에서 동등 비교를 할 수가 있음.
(참고로 이때 hashCode만 재정의하면 안되고 equals도 해야함)

추후에 hash컬렉션을 쓸 수도 있어서 hashCode메소드도 꼭 같이 재정의 해주는게 좋음

------------------------------

equalsIgnoreCase

equals() 랑 같으나 대/소문자를 무시함

mybatis에서도 쓸 수 있음
<choose>
	<when test="tbl.equalsIgnoreCase('COURSE_INFO')">

----------------------------------------------------------------------------------------------------

hashCode(해시)
객체를 식별하는 정수값. 객체의 유일한 주소값을 얻기 위해 씀

System.identityHashCode(객체); → 객체가 메모리에서 가진 고유한 hash주소값 리턴
hashCode() → 모든객체의 부모클래스인 Object에 정의되어있으며 하위 클래스들은 Override 가능함.
객체의 특성이 동일하다는 것을 표현하기 위해서 이 메소드를 Override 함.
서로 다른 객체이지만 hashCode가 동일한 경우 존재.
예를들어 String의 hashCode가 같다면 객체는 달라도 문자열은 동일하다는것을 의미


String의 경우 문자코드*31^(자리수-1) 구해진값이 자리마다 더해져서 나옴
aaa 이면
97*(31^0) + 97*(31^1) + 97*(31^2)
97*1 + 97*31 + 97*31*31 = 96321 이 나옴


때문에 String에서는 해시코드가 중복될 수 있으며(특정 문자열 조합에서 동일한 정수값을 가짐)
ex)
String a = "Z@S.ME";
String b = "Z@RN.E";

이때문에 String 클래스에는 equals메소드를 재정의해서, hashcode가 같더라도

-----

hashCode() 메소드 재정의


equals() & hashCode() 를 재정의하지 않았을경우 같은 값이라도 다른 hashCode가 반환됨

hashCode 재정의 하는법
@Override
public int hashCode() {
	return Objects.hash(필드1, 필드2, ...);
}


ex) HashSet이용시 재정의를 했을경우와 하지않았을 경우 비교

★equals/hashCode재정의 안했을 경우

<C1.java>
String name;

public C1(String name) {
	this.name = name;
}

<Run.java>
C1 o1 = new C1("aa");
C1 o2 = new C1("bb");
C1 o3 = new C1("aa");

Set<C1> set = new HashSet<>();
set.add(o1);
set.add(o2);
set.add(o3);

System.out.println(set);			// [com.example.test.class_.hash.set.C1@1d81eb93, com.example.test.class_.hash.set.C1@2f4d3709, com.example.test.class_.hash.set.C1@4e50df2e]
System.out.println(set.size());	// 3


★equals/hashCode재정의 했을 경우

<C1.java>
.
.
@Override
public boolean equals(Object o) {
	if (this == o) return true;
	if (o == null || getClass() != o.getClass()) return false;
	C1 c1 = (C1) o;
	return Objects.equals(name, c1.name);
}

@Override
public int hashCode() {
	return Objects.hash(name);
}

<Run.java>
.
.
System.out.println(set);			// [com.example.test.class_.hash.set.C1@c3f, com.example.test.class_.hash.set.C1@c5f]
System.out.println(set.size());	// 2

-----

ex) hashMap도 마찬가지로 비교

★equals/hashCode재정의 안했을 경우

<Run.java>
Map<Object,String> map = new HashMap<>();

map.put(new C1("aa"),"a");
map.put(new C1("bb"),"b");
map.put(new C1("aa"),"c");

System.out.println(map);		// {com.example.test.class_.hash.map.C1@1d81eb93=c, com.example.test.class_.hash.map.C1@2f4d3709=a, com.example.test.class_.hash.map.C1@4e50df2e=b}
System.out.println(map.size());	// 3


★equals/hashCode재정의 했을 경우

<Run.java>
.
.
System.out.println(map);		// {com.example.test.class_.hash.map.C1@c3f=c, com.example.test.class_.hash.map.C1@c5f=b}
System.out.println(map.size());	// 2

-----

String을 ""로 생성했을때와 new 연산자로 생성했을때의 차이


자바에는 heap영역이라는 저장공간이 있는데 이 heap안에 string pool이 존재함

""리터럴로 String을 만들면 그 값은 이 string pool 안에 들어가는데,
들어가기 전 이미 중복된 문자열이 있는지 확인하고 있다면 해당 주소값을 공유하게됨

반면 new 연산자를 사용해 객체를 생성하면 똑같이 heap영역이지만 string pool밖에 생성되며 (다른 객체들과 똑같이 생성됨)
같은 글자를 갖는 String객체가 있더라도 새로운 독립된 개체를 생성하게 된다
따라서 new 연산자를 이용해서 객체를 만들었다면 갖고있는 값이 모두 같더라도 주소는 모두 다르게 될 것이다

----------------------------------------------------------------------------------------------------

★유효성 검사(사용자로부터 문자열을 받아서 숫자로 변환해 검사하는 방법)

1. charAt(0);
2. reader.read(); → 둘다 true이면 해당
  소문자검사
  System.out.println(data >= 'a');
  System.out.println(data <= 'z');

  한글검사
  System.out.println(data >= '가');
  System.out.println(data <= '힣');

  숫자검사
  System.out.println(data >= '0');
  System.out.println(data <= '9');

  아래가 되는 이유 : 값형끼리는 비교연산이 가능(숫자끼리)
  System.out.println('박' <= '김');
  아래가 안되는 이유 : 참조형끼리는 비교연산이 불가능(문자끼리)
  System.out.println("박" >= "김");
  아래가 안되는 이유 : 값형과 참조형과는 비교연산이 불가능(숫자와 문자)
  System.out.println('박' >= "김");

----------------------------------------------------------------------------------------------------

★영문 표기 (ppt등 할때 같은 말이라도 영어로 읽으면 우리나라에서는 뭔가 다르게 본다고...)

~(tild),!(exclamation mark),@(at sine),#,$,\(won sine),%,^(carret,xor),&,*,(,),
-(hyphen/dash(대쉬가하이픈보다더길다고함)),_(underline),,,.,?,'(apostrophe),
"(quotation mark),`(back quote/grave),|(vertical line)

(),[],{},<>(다이아몬드괄호,화살표괄호)

A > B
A greater then B
A >= B
A greater than equal B

A < B
A less than B

----------------------------------------------------------------------------------------------------

★메소드, 메소드 , Method - 특정 목적을 갖고 행동하는 코드의 집합
- 메소드(Method) , 함수(Function) , 프로시저(porcedure) , 서브루트(Sub Routine) 등.. 비슷한 말
- 재사용이 가능한 단위 요소

1. 메소드 선언하기(정의하기)
public static void hello(){
	system.out.println("test");
}
접근지정자 정적키워드 반환자료형 메소드명(인자리스트or매개변수){ //메소드 헤더,메소드 시그니처(Signature)
	실행코드 //메소드 바디, 구현부
}

클래스 내부에서만 선언가능
선언된 메소드들끼리의 순서는 상관없다
메소드명 : 카멜표기법

2. 메소드 호출하기(사용하기)
hello();
코드 재사용 높음 → 효율성
유지 보수성 높음 → 수정하기 편함


★메인 메소드
- 특수메소드
- 메소드명이 예약어이다
- 메인 메소드 개발자호출 하는 용도 X. 자바(JVM)이 호출하는 메소드(자동으로 호출되는것처럼 보인다.) → 시스템이 호출하는 메소드
→ 콜백 메소드(Callback Method)
- 트리거 역할을 하는 메소드(모든일의 시발점 역할)
- main() 메소드 : 프로그램 시작점 역할(Entry Point) ~ 프로그램 종착점 역할(End Point)


★코드가 어떤식으로 실행되는 순서(제어의 흐름)
책읽듯이 읽는다 (위쪽에서 아래쪽으로 , 왼쪽에서 오른쪽으로)

main메소드부터 시작되어 , substract();같은 메소드를 만나면  substract메소드가 선언되어있는곳으로 점프(제어 이동)
→ 끝나면 원래 위치로 돌아오고 substract()는 사라진다 → 이후 다음 코드를 계속 실행한다


★메소드 인자 리스트 - 파라미터(Parameter)/인자(Argument)/매개변수/가인자&실인자(FormParameter&RealParameter)

public static void main(String[] args) {
	hello("이열음");
	hello("권나라");
}

public static void hello(String name){
	System.out.printf("%s님 안녕하세요\n",name);
}

or

public static void hello(String name){
	System.out.println(name + "님 안녕하세요");
}

매개변수 메소드를 만들때는 호출부에 값을 필수로 입력해야함
매개변수는 초기화를 할 수 없다.
메소드의 쓰임새가 다양해진다 → 활용도가 높아진다 → 가용성이 높아진다

매게변수메소드를 사용할때는

인자의 개수가 맞아야 하고,
인자의 순서가 맞아야 한다

----------------------------------------------------------------------------------------------------

지역변수(Local Variable)
- 해당 변수의 지역(영역,scope)이 존재한다
- 메소드내에서 해당 선언된 변수를 말한다
-지역 변수의 영역은 해당 변수가 선언된 메소드를 말한다.

변수의 생명 주기, Life Cycle
- 변수는 특정 시점에 태어나서 특정 시점에 소멸된다
- 변수는 특정 시점에서 메모리에 할당되었다가 특정 시점에 메모리에서 해제된다

지역 변수의 태어나는 시점
- 전언문이 실행될 떄

지역변수의 소멸되는 시점
- 선언문이 포함된 블럭에서 제어가 빠져나가는 순간

지역변수는 지역이 다르면 동일한 이름의 변수를 만들 수 있다
매개변수도 지역변수중 하나

----------------------------------------------------------------------------------------------------

★메소드 반환값

- return문 이용
- 메소드가 일을 하고 난 뒤 호출했던 곳으로 돌려주는 값
- return값은 1개밖에 돌려줄수없음
- 사용시 반환자료형(void) 공간에 결과자료형 지정
- return은 보이는 즉시 끝나기때문에 반복문 안에서도 탈출가능하고 break/continue보다 훨씬 높음

return num; 메소드를 종료하고 호출했던 곳으로 돌아감 + num을 가지고 돌아감

public static void main(String[] args) {
	String result = m1();
	System.out.println(result);
}

public static String m1() {
	String num = "하나";
	return num;
}

----------------------------------------------------------------------------------------------------

★메소드 오버로딩(Method Overloading)
- 메소드가 인수 리스트를 다양한 형태로 가질 수 있는 기술
- 이를 통해 같은 이름의 메소드를 여러개 선언하는 기술

★메소드 시그니쳐(Method Signature)
-메소드의 헤더 부분

★메소드 오버로딩 조건 O
1. 인수의 개수
2. 인수의 타입
3. 리턴값의 유무

★메소드 오버로딩 조건 X
1. 인수의 이름
2. 리턴값의 타입

★오버로딩을 하는 이유
개발자 편의성(개발자를 위한 기술)
기억해야할 메소드의 이름을 줄여준다☆☆☆

println()도 오버로딩 기술 없었으면 → println1 , println2 , print3 ...  or printlnString , printlnInt , printBoolean
등등 엄청나게 불편하게 되었을것

https://docs.oracle.com/javase/8/docs/api/에서 확인가능
All Classes → System → Method Summary → Method and Description열에서 println

----------------------------------------------------------------------------------------------------

★이클립스 Rename

고칠 단어위에 포커스 두고
ctrl + shift + r
or
ctrl + 1 → enter

----------------------------------------------------------------------------------------------------

★이클립스 BrakePoint (버그를 잡기위한 도구 , 공부할때 좋은 도구)

원하는라인에 올려놓고
ctrl+alt+b 이후 f11

배경색으로 표시가 생기는데 어디까지 실행됬는지 나옴
Debug

f8(resume)을 누르면 다시 계속 실행되고, ctrl+f2(terminate)를 누르면 종료되고

f5(Step Into)를 누르면 한문장씩 실행되어 Variables에 변수가 실시간으로 표시된다
어떤 순서로 실행되는지 한눈에 볼 수 있음

★이클립스 우측 창에 outline
메소드 왔다갔다 이동하면서 찾을때 편함

★이클립스 소스코드 원본 보는방법
String 이런문장에 포커스를 두고 f3을 누르고 Attach Source 버튼 클릭
External location 라디오 버튼 체크 → External File 누르고 Program Files/Java/jdk1.8.0_261/src.zip 선택
이후 다음번에 f3을 눌렀을때 모든 소스들을 볼 수 있다

★이클립스 ui 붙박이 말고 창 모드로 하는법
최대화 풀고 이클립스 밖으로 콘솔창 등 드래그

ui초기화 : Window → Perspective → Reset Perspective

----------------------------------------------------------------------------------------------------

★클래스명과 파일명은 꼭 같아야 한다(오류남)

대문자로 만들어야하는데 소문자로 잘못 만들었을경우
f2눌러서 대문자로 고치면 이클립스에서 대소문자 바뀐걸 눈치 못채고 옛날 이름으로 되어있어서
에러날 부분이없는데 계속 에러날 일이 없는데 에러가 날 가능성이 있음

그렇게 되면 이클립스를 깨끗이 청소해야함
메뉴 → Project → Clean

이걸로도 안되는 경우 그냥 마냥 기다리거나
파일을 새로 만들어서 복붙해야함

----------------------------------------------------------------------------------------------------

★컴파일 렉걸릴때 이클립스 껏다키기

----------------------------------------------------------------------------------------------------

System.currentTimeMillis() / System.nanoTime() 메소드
1970년 1월 1일 00:00:00.000을 기준으로 현재시간과의 차이를 long형으로 반환한다

long l1 = System.currentTimeMillis(); → 틱(1/1000초)
long l2 =  System.nanoTime(); → 나노 초(1/1000000000초)

----------------------------------------------------------------------------------------------------

★날짜/시간 연산
틱(Tick),에포크(Epoch , 타임 스탬프 : 픅정 시각으로부터 흐른 누적 시간

시각 + 시각 : X
시각 - 시각 = 시간 : O

시간 + 시간 = 시간 : O
시간 - 시간 = 시간 : O

시각 + 시간 : O
시각 - 시간 : O

-----

Date 쓰는법 (현재시각 간편하게 구할때씀)

Date d1 = new Date(); ← 잘 안씀, Date클래스는 지역화를 지원하지 않기때문 (국가별로 현재날짜와 시간이 다른걸 지원못함)
빨간밑줄 클릭 ctrl + 1
Import 'Date' (java.util) 클릭

현재 시각
System.out.println(new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.S").format(new Date()));

현재 시각 밀리초
System.currentTimeMillis()
or
Calendar.getInstance().getTimeInMillis()

-----

★날짜/시간 형식 변경하는법

Date date = new Date(); // 현재 날짜&시각
SimpleDateFormat dateFmt = new SimpleDateFormat("yyyy.MM.dd HH:mm:ss"); // 날짜&시각 포맷설정
String fday = dateFmt.format(date); // 포맷 변경


★스트링을 원하는 형식의 날짜형으로 변환

Scanner sc = new Scanner(System.in);
String strDate = sc.nextLine();

SimpleDateFormat dFmt = new SimpleDateFormat("HH:mm:ss");
SimpleDateFormat dFmt2 = new SimpleDateFormat("mm");

Date orginDate = originFormat.parse(strDate);
String newDate = newFormat.format(orginDate);

System.out.println(originFormat.format(orginDate));
System.out.println(newDate);

-----

데이터포맷(DateFormat)

DateFormat dateFormat = new SimpleDateFormat("yyyyMMdd");
String dateString = "20230101";
Date date = dateFormat.parse(dateString);  // Date로 변환

// 현재날짜가 지정일보다 이후이면
if(new Date().after(date)){
	System.out.println("이후");
}

// 현재날짜가 지정일보다 이전이면
else if(new Date().before(date)){
	System.out.println("이전");
}

------------------------------

Date ↔ Calendar 변환

-----

1. Calendar를 Date로 변환

Calendar c = Calendar.getInstance();
Date d = new Date(c.getTimeInMillis());

-----

2. Date를 Calendar로 변환

Calendar c = Calendar.getInstance();
c.setTime(new Date());

------------------------------

Calendar 쓰는법

Date클래스의 문제를 해결하기 위한게 Calendar클래스이다

★캘린더에서 원하는 값만 끌어오기 ※꼭 필요한 값만 끌어오기 , 시간계산은 캘린더 안쓰고 정수형 변수로만 계산가능하다고는함
Calendar cal1 = Calendar.getInstance();
System.out.println(cal1.get(1)); → 년
System.out.println(cal1.get(2)); → 월
System.out.println(cal1.get(3)); → 몇주차

보통은 아래처럼 사용

System.out.println(cal1.get(Calendar.YEAR));

cal1.get(Calendar.YEAR)
cal1.get(Calendar.MONTH) → ★0부터시작임. 1월=0, 12월=11
cal1.get(Calendar.DATE)
cal1.get(Calendar.HOUR)
cal1.get(Calendar.MINUTE)
cal1.get(Calendar.SECOND)
cal1.get(Calendar.MILLISECOND) → 1/1000초
cal1.get(Calendar.AM_PM) → 오전:0 오후:1
cal1.get(Calendar.DAY_OF_MONTH) → 일
cal1.get(Calendar.DAY_OF_YEAR) → 올해 며칠
cal1.get(Calendar.DAY_OF_WEEK) → 이번주 며칠(=요일) ★1=일요일, 7토요일
cal1.get(Calendar.HOUR_OF_DAY) → 24시표기 ★
cal1.get(Calendar.WEEK_OF_YEAR) → 올해 몇주차
(tmi:월과 요일을 0부터 시작하는 이유 : 월과 요일이 문자라서 최초에 배열로 사용되었어서,
나머지는 수치로써 사용되는 데이터이므로 시작이 1이다)

Calendar 클래스의 데이터를 출력하려면 time의 약자인 t가 붙은 컨버전을 이용해야 한다.
%tY: 현재의 날짜를 년도를 생략없이 출력한다. (ex. 2014)
%ty: 현재의 날짜를 년도를 앞자리 생략하여 출력한다. (ex. 14)

%tm: 현재의 날짜를 01~12(월) 형식으로 출력한다.
%th: 현재의 날짜를 1~12(월) 형식으로 출력한다.
%tb: 현재의 날짜를 영문 약자(월) 형식으로 출력한다. (한글 환경에서는 '숫자+월'로 출력되며 %tB와 차이가 없다.)
%tB: 현재의 날짜를 영문(월) 형식으로 출력한다. (한글 환경에서는 '숫자+월'로 출력되며 %tb와 차이가 없다.)

%td: 현재의 날짜를 01~31(일) 형식으로 출력한다.
%te: 현재의 날짜를 1~31(일) 형식으로 출력한다.
%tj: 현재의 날짜를 001~366(일) 형식으로 출력한다. (올해를 기준으로 몇 일이 경과했는지가 출력된다.)

%ta: 현재의 날짜를 요일 영문 약자 형식으로 출력한다. (한글 환경에서는 '월/화/수/목/금/토/일'로 출력된다.)
%tA: 현재의 날짜를 요일 영문 형식으로 출력한다. (한글 환경에서는 '월/화/수/목/금/토/일+요일'로 출력된다.)

%tD: 현재의 날짜를 %tm/%td/%ty(월/일/년) 형식으로 출력한다.
%tF: 현재의 날짜를 %tY-%tm-%td(년/월/일) 형식으로 출력한다.
%tc: 현재의 날짜와 시간을 %ta %tb %td %tT %tZ %tY(요일 월(영문) 일(숫자) 몇시:몇분:몇초 타임존 년도)로 출력한다.

%tH: 현재의 시간을 00~23(시) 형식으로 출력한다.
%tk: 현재의 시간을 0~23(시) 형식으로 출력한다.
%tI: 현재의 시간을 01~12(시) 형식으로 출력한다.
%tl: 현재의 시간을 1~12(시) 형식으로 출력한다.

%tM: 현재의 시간을 00~59(분) 형식으로 출력한다.
%tS: 현재의 시간을 00~60(초) 형식으로 출력한다.
%tz: 현재 시간의 타임 존을 출력한다.

%tR: 현재의 시간을 %tH:%tM(몇시:몇분) 형식으로 출력한다.
%tT: 현재의 시간을 %tH:%tM:%tS(몇시:몇분:몇초) 형식으로 출력한다.


빈숫자 0추가(표시형식)
int hour = now.get(Calendar.HOUR_OF_DAY);int min = now.get(Calendar.MINUTE);int sec = now.get(Calendar.SECOND);
System.out.printf("%s:%s:%s\n",hour<10?"0"+hour:hour+"",min<10?"0"+min:min+"",sec<10?"0"+sec:sec+"");

보다간편한코드
int hour = now.get(Calendar.HOUR_OF_DAY);int min = now.get(Calendar.MINUTE);int sec = now.get(Calendar.SECOND);
System.out.printf("%02d:%02d:%02d\n",hour,min,sec);

자바가만든 가장간편 형식문자열
System.out.printf("%tF",now); → 현재날짜
System.out.printf("%tT",now); → 현재시각


★특정 날짜/시각 만들기

Calendar birthday = Calendar.getInstance();
	
birthday.set(Calendar.YEAR,1968);
birthday.set(Calendar.MONTH,4); ★1월=0, 12월=11
birthday.set(Calendar.DATE,10);
System.out.printf("%tF",birthday);

년/원/일 한번에 set하는법 ★★★
birthday.set(1998,9,5); // 10월
System.out.println("%tF",birthday);


★현재시각에 날짜/시간 더하고 빼기 ★
Calendar now = Calendar.getInstance();
now.add(Calendar.DATE,100); → 덮어쓰기(수정) ※업데이트, 복사해서 사용해야할시 Calendar expirationTime = (Calendar)creationTime.clone();
System.out.printf("%tF",now);

Calendar now = Calendar.getInstance();
now.add(Calendar.MONTH,-3); → 덮어쓰기(수정) ※업데이트, 복사해서 사용해야할시 Calendar expirationTime = (Calendar)creationTime.clone();
System.out.printf("%tF",now);

★특정 월에 몇일까지 있는지 불러올때 (윤년 계산가능)
Calendar now = Calendar.getInstance();
now.set(2020,1,1); → 구하고자하는 월에서 1을 빼야함
System.out.println(now.getActualMaximum(Calendar.DATE));

★틱 tick으로 '시각 - 시각' 구하기
틱 / 1000 = 초
틱 / 1000 / 60 = 분
틱 / 1000 / 60 / 60 = 시
틱 / 1000 / 60 / 60 / 24 = 일
틱 / 1000 / 60 / 60 / 24 /365 = 년

Calendar now = Calendar.getInstance();
Calendar birthday = Calendar.getInstance();
birthday.set(1999,2,6,3,0,0);

long nowTick = now.getTimeInMillis();
long birthdayTick = birthday.getTimeInMillis();

long gap = nowTick - birthdayTick;

System.out.println(gap / 1000 / 60 / 60 / 24);

★정수로 시간(분) 더하기 - 1시간당 60을 곱해 분에다 더해 처리하면 편리함
int hour = 2;
int min = 30;

min = min + 50;

hour = hour + min / 60;
min = min % 60;

★정수로 시간(분) 빼기 - 1시간당 60을 곱해 분에다 더해 처리하면 편리함
int hour = 5;
int min =10;

int calcH = min - 150 < 0 ? hour - (150 / 60) : hour;
int calcM = min - 150 < 0 ? 60 + (min - 150) % 60 : min - 150;

----------------------------------------------------------------------------------------------------

값형 복사시 : 원본(값)을 복사함 (원본의 heap데이터가 변경되어도 값을 복사한거니 복사해둔값은 데이터가 바뀌지 않음)
참조형 복사시 : 원본(주소)를 복사함 (원본의 heap데이터가 변경되면 주소를 복사한거니
	        복사해둔값도 자연스럽게 바뀐 데이터를 참조하게 됨 사이드이펙트 발생)

그렇기 때문에 참조형 복사시엔 clone메소드 사용

----------------------------------------------------------------------------------------------------

★메소드 자동으로 생성 단축키
불러오는 부분 m1(); 만들고 ctrl+1 목록 선택

${todo}로 시작하는 주석/내용 삭제/변경
Window > Preferences > Java > Code Style > code Templates > Code > Method body


Try Catch
try {
	${line_selection}${cursor}
} catch (${Exception} ${exception_variable_name}) {
	System.out.println("${primary_type_name}.${enclosing_method}()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

★이클립스 자동 줄바꿈
https://blog.naver.com/sheis0/220200415740
https://blog.naver.com/ungahah/40108578239

----------------------------------------------------------------------------------------------------

★하나의 변수 안에서 여러가지 형식을 출력하는것은 불가능
ex) int 변수 안에서 string + int 불가능

----------------------------------------------------------------------------------------------------

★if나 for안에 있는 변수 밖으로 빼기
String s1 = "";
if(0<=1){
	s1 = "하나";
}else {
}

초기화가 안되있는(초기값이없는) 변수를 출력하려고 하면 에러가 발생하니
위처럼 초기값이 null이나 0으로 초기화 되어있어야 함!!

----------------------------------------------------------------------------------------------------

★제어문 종류

조건문
	1. if(***) - 조건을 제시한 후 코드의 흐름을 분기 시키는 제어문 (조건 : boolean)
	2. switch(*) - [] : 생략가능   x : 여러번가능   default : if문에서의 else   ★switch의 조건은 정수와 문자열을 사용가능 (실수,bollean X)  
		if문과 같은 용도로 쓸려면 case마다 break; 꼭 넣어야함. 마지막에는 break를 넣을필요없음. 보통 default를 마지막에씀(=if문의 else)

		switch(조건){
			case 값:
				실행코드;
				break;
			[case 값:
				실행코드;
				break;] x N
			[default:
				실행코드;
				break;]
		}

	ex) 여러조건 같은결과 나오게하고싶을때
	case 0:
	case 1:
	case 2:
		실행코드;
	break;
	
	ex) 레벨에 따라 권한의 개수를 차등부여하고싶을때. break를 고의로 뺌
	switch(level){
		case 3:
			grantDelete(); // 삭제권한 부여
		case 2:
			grantWrite(); // 쓰기권한 부여
		case 1:
			grantRead(); // 읽기권한 부여
	}


반복문
	1. for(***) - 일련의 실행코드를 개발자가 원하는만큼 반복실행해주는 제어문 - for(초기식;조건식;증감식){}
		for (int i = 0; i < 10; i++) {
			int n = 10;
			System.out.println(n);
			n++;
			System.out.println(n);
		}
		초기식에 넣은 'i'변수는 루프가 되도 살아있고,
		루프문 안에서 초기화한 'n'변수는 루프가 될때마다 할때마다 죽었다가 살아난다 (이전 값이 초기화된다)

		int sum = 0;
		for (int i = 1; i <= 10; i++) {
			sum = sum + i;
		}
		System.out.println(sum);
		'sum'은 밖에서 초기화했기때매 for문이 끝나도 살아있다. 'sum'이란 '누적변수'는 초기화시 0으로 초기화 한다.

	2. while(***) - for문 유사 , 조건에 따라 반복제어를 하는 제어문 (반복되는 if문) 선조건 → 
	    후실행(조건을 만족해야 실행) 무한루프 만들때 편함(조건에 true)
		int num=1;
		
		while(num <= 10) {
			System.out.println(num);
			num++;
		}

	3. do while - while문의 머리와 몸통의 위치가 바뀐것   선실행 → 후조건(조건을 만족하지 못하더라도 최소 1회는 실행)
		do{
			실행코드;
		}while(조건);

	4. enhanced for(foreach) (***) - 향상된 for (배열) ★읽기만가능 수정X
		- 루프 변수가 없다.
		- 스스로 배열의 첫번째~마지막방까지를 '순차적'으로 탐색 (순서제어불가)
		- 처음부터 끝까지 다 가져온다(예외없음)
		- 안정성 높음
		- 코드 간결
		- 속도 빠름
		for (자료형 item : 배열명) {
			System.out.println(item);
		}

		.forEach(람다식) 도 있다 (★컬렉션객체한테만 쓸 수 있고, 자료형을 생략가능함, break 사용불가.
		배열명.forEach(item -> System.out.println(item))

		배열명.forEach(item -> { // item이 람다의 매개변수임)
			System.out.println(item);
		});

		배열명.forEach(System.out::println);

		★★★배열의 요소들을 메소드의 인수로 보내는 방법 (받을 메소드에서 파라미터를 배열의 요소의 자료형과 일치하도록 선언해야함)
		배열명.forEach(this::메소드명)
		


	★무한 루프 - 조건식을 안쓰거나 true로 설정
	1. 인위적  작성하는경우
	2. 실수로 작성하는경우
	for(;;){
		System.out.println("무한루프");
	}

	for(int 1=1;;){
		System.out.println("무한루프");
	}

	for(int 1=1;;i++){
		System.out.println(i);
	}

무한루프를 처리하다가 보면 Unreachable에러가 나오는데
오류난 위치까지 도달할 수가 없다는 뜻 (=도달하기전에서 계속 무한루프가 나거나 , 도달하기전에서 break로 빠져나가버리는경우)


분기문	1. break(**) - 자신 속한 제어문을 탈출(종료)한다. = if문을 제외한 바로 상위 제어문까지만 탈출한다
		while(true){
			System.out.printf("배열의 길이 : ");
			range = Integer.parseInt(reader.readLine());
			if (range<=20) {
				if (range % 2 == 0) {
					break;
				}
				System.out.println("짝수를 입력하세요.");
			}else {
				System.out.println("20이하로 입력하세요");
			}
		}
	2. continue(**) - 무조건 하던일 멈추고 반복문의 시작으로 돌아간다. → 스킵
		for (int i=1; i<=30; i++) {
			if(i==16 || i==18 || i==21) {
				continue;
			}
			System.out.printf("선생님이 %d번 학생을 상담합니다.\n",i);
		}
	3. goto (JDK 1.5 폐지)



특정 키 입력시까지 무한루프 ?????????

BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

System.out.println("아래에 입력하세요.");

String total="";
for (;;) {
	String data = reader.readLine();
	if (data.equals("")) {
		System.out.println("아무것도 안침!!!!!!!!!!!!");
		break;
	}
	total += data + "\n";
}

System.out.println(total);


★이름붙은 반복문 (부모for문 탈출용)
Loop1: for(i=0;;i++){
	for(j=0;;i++){
		continue Loop1;
		break Loop1;
	}
}

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

배열

같은 성격 + 같은 자료형 데이터들을 모아놓은 집합. 자바의 모든 타입은 배열을 만들 수 있음
배열의 길이는 불변이다 (한번 만들어진 배열의 방 개수를 변경할 수 없다, 배열을 만들때 반드시 데이터의 개수를 충분히 예상해야 한다)

- 타입[] 배열명 = new 자료형[길이]
- [] : 차원
int mum = 10; //변수를 만들어서 그안에 데이터를 넣어라
int[] kor = new int[3]; //변수를 만들어서 그안에 데이터를 넣어라
kor → int 배열([])입니다.
	// int x 3

int[] nums = new int[10]; → 주로 사용
int nums[] = new int[10]; → 사용 안함


★초기화 방법
int[] a1 = new int[3];
nums1[0] = 1;
nums1[1] = 2;
nums1[2] = 3;

int[] a2 = new int[] {1,2,3};

int[] a3 = {1,2,3};

int[] a4 = new int[]{1,2,3}; // 변수에 안담고 무명배열 생성가능(메소드의 인수로 배열을 담아 전달할때 씀)

int[] a5 = new int[]{}; // 출력시 [ ] 빈 배열이 출력됨

int[] a6 = {}; // 출력시 [ ] 빈 배열이 출력됨

int[] a7 = null; // 출력시 null이 출력됨


서수(index)
- Zero-based Index (0부터시작)
- 주로 C계열 언어에서 잘 사용
0 0  0 0 0 0 0 0 → 0
0 0  0 0 0 0 0 1 → 1
0 0  0 0 0 0 1 0 → 2

Basic 계열 언어 (1부터시작)
- One-based Inndex


기본용법

int[] nums = new int[10];

for (int i=0; i<nums.length; i++) {
	nums[i] = i+1;
}

for (int i = 0; i < nums.length; i++) {
	System.out.printf("nums[%d] = %d\n",i,nums[i]);
}


배열의 길이(방)
System.out.print(list1.length);

------------------------------

★배열을 복사한 뒤에 한쪽을 수정하면 나머지 배열도 같이 수정된다.(=사이드이펙트)
- 주소값 복사   - 얕은영역에서 복사가 이루어졌다고 해서 얕은복사, Shallow Copy(기본방식)
- heap=깊은영역 , stack=얕은영역

-----

얕은복사 : 배열이 가지는 방의 ★'주소'를 복사   (깊은복사보다 더 주로 사용)
String[] s1 = new String[3];
s1[0] = "한가인";
String[] temp = s1;
System.out.println(temp[0]);	→ "한가인"을 복제했는데
s1[0] = "손가인";		→ s1의 내용이 손가인으로 바뀌니
System.out.println(temp[0]);	→ 결과는 "손가인"

-----

깊은복사 (값형 → 값형 : 데이터 복사) : 배열이 가지는 방끼리 직접 복사를 한다 (사이드이펙트X)   ★'값'을 복사


방법1. for문 & 대입 연산자

int[] arr = {1,2,3};
int[] arr2 = new int[3];

for (int i=0; i<nums1.length; i++)
	arr2[i] = arr[i];

arr2[2] = 4;

System.out.println(Arrays.toString(arr2));
System.out.println(Arrays.toString(arr));


방법2. Arrays.copyOf / Arrays.copyOfRange

int[] arr = {1,2,3};
int[] arr2 = Arrays.copyOf(arr, arr.length); // 2번째 인수: 새로운 배열의 방길이 지정
arr2[2] = 4;

System.out.println(Arrays.toString(arr2));
System.out.println(Arrays.toString(arr));


방법3. System.arraycopy

int[] arr = {1,2,3};
int[] arr2 = new int[3];
System.arraycopy(arr, 0, arr2, 0, arr.length); // arr[0]에서 arr2[0]으로 arr.length개의 데이터를 복사
arr2[2] = 4;

System.out.println(Arrays.toString(arr2));
System.out.println(Arrays.toString(arr));

------------------------------

★배열은 생성된 직후에 각 방들이 특정한 값으로 초기화된다.
1. 정수 배열 → 0
1. 실수 배열 → 0.0
3. 문자 배열 → \0(null 문자, 문자코드값(0))
4. 논리 배열 → false
5. 참조형 배열 → null

----------------------------------------------------------------------------------------------------

배열함수

★Arrays.sort(기본배열) : 오름차순 정렬 (원본을 정렬시킴)
★Arrays.sort(기본배열, Collections.reverseOrder()) : 내림차순 정렬. int[]는 안되고 Integer[] 이어야하고, print() 안에서 바로 쓰면 안됨
Integer[] what = stream(arr).boxed().toArray(Integer[]::new);

★Arrays.toString() - 배열 출력 (1차원 배열을 문자열로 반환)
- 개발자 배열 확인용으로 사용 (import필요)
- dump 메소드
System.out.println(Arrays.toString(nums));

ex) toString오버라이딩
@Override
public String toString() {
	String temp="";
	temp+="\n";
	temp+= String.format("list: %s\n",Arrays.toString(this.list));
	temp+= String.format("index: %s\n",this.index);
	temp+= String.format("length: %s\n",this.list.length);
	temp+="\n";
	return temp;	
}

Arrays.copyOf(배열)
★Arrays.copyOfRange(배열, 시작index(포함), 끝index(미포함)) - 배열에서 원하는 범위 지정해서 배열로 반환

★Arrays.stream(배열).average().orElse(0) - 배열의 평균 구하기

★Arrays.stream(String.valueOf(n).split("")).mapToInt(Integer::parseInt).sum() - int의 각 자리를 더하기

★Arrays.binarySearch(배열, 찾을수) - 값에 해당하는 index 반환. 반드시 정렬이 되어있어야함. 없을경우 n보다 큰 최초의 수를 찾아 * -1 - 1 을 한 결과를 반환함

★Arrays.fill - 배열의 모든방을 특정값으로 채우기. 방에 값이 있어도 무시하고 덮여짐
Arrays.fill(배열, 값);

★deepToString - n차원 배열출력
- toString과 사용법 동일

하지만
for (int i = 0; i < nums.length; i++) {
	for (int j = 0; j < nums.length; j++) {
		System.out.printf("%3d",nums[i][j]);
	}
	System.out.println();
}
이런식으로 출력하는것이 가독성은 더 좋다고 함


★배열의 요소 추가/삭제
추가 - 우측 시프트 발생(Right Shift) → 우측에서 좌측로 카피작업이 이뤄져야함
int[] nums = {5,3,8,2,1,7,9,4,6,10};

int index = 3;
int value = 100;

for (int i = nums.length-2; i >= index; i--) {
	System.out.println(Arrays.toString(nums));
	nums[i+1] = nums[i];
}
nums[index] = value;

System.out.println(Arrays.toString(nums));


삭제 - 좌측 시프트 발생(Left Shift) → 좌측에서 우측로 카피작업이 이뤄져야함
int[] nums = {5,3,8,2,1,7,9,4,6,10};

int index = 3;

for (int i = index+1; i < nums.length; i++) {
	System.out.println(Arrays.toString(nums));
	nums[i-1] = nums[i];
}
nums[nums.length-1] = 0;

System.out.println(Arrays.toString(nums));


★1,2,3···n차원 배열

1차원배열
int[] nums1 = new int[3];
nums1[0] = 100;
출력시 Arrays.toString(배열명) 사용가능

2차원배열
int[][] nums2 = new int[2][3];
nums2[1][2] = 100;

(2차원이상)바로 대입하는경우
int[][] a4 = {{1,2,3,4},{1,2}};
출력시 Arrays.deepToString(배열명) 사용가능


3차원배열
int[][][] nums3 = new int[2][3][4];
nums3[1][0][3] = 300;

n차원배열 출력 (for문을 늘린다)
for (int i = 0; i<2; i++) {
	for (int j = 0; j<3; j++) {
		System.out.printf("nums1[%d][%d] = %d\n",i,j,nums2[i][j]);
	}
}

n차원배열 length - 사람이 생각하는 3차원은 컴퓨터세계에서 선형구조로 되어있기때문에 계속 0번째의 0번째 길이를 출력시키면 됨
System.out.println(nums3[0][0].length);

-----

n차원배열 초기화

int[][] nums2 = new int[][] {{10,20,30},{40,50,60}};
줄여서↓
int[][] nums2 = {{10,20,30},{40,50,60}};

------------------------------

배열의 자료형

int num;
int[] num1 = new int[3];
int[][] num2 = new int[2][3];
		
num의 자료형 → int
num1의 자료형 → int[] (인티저배열) or (인티저 1차원배열)
num2의 자료형 → int[][] (인티저배열) or (인티저 2차원배열)
num1[0]의 자료형 → int
mun2[0][0] → int
num2[0] → int[]

------------------------------

깊은복제

collection (List/Map등 인터페이스말고 ArrayList/HashMap등 클래스에 쓸 수 있음. jdk 제공)
복제할컬렉션객체 = 원본컬렉션객체.clone();

기본배열 (jdk 제공)
복제할배열 = Arrays.copyOf(원본배열,원본배열.length);

------------------------------

배열에서 index찾기

List 로 변경후 찾아야함

Arrays.asList(arr).indexOf(값) → non primitive 타입에 대해서만 가능함
or
Arrays.stream(array).boxed().collect(Collectors.toList())
or
Collections.arrayToList(배열).indexOf(값) → jjwt라이브러리추가해야함

----------------------------------------------------------------------------------------------------

2차원 배열 정렬

{{2, 6}, {1, 5}, {1, 3}}
위 배열이 있을때

{{1, 5}, {1, 3}, {2, 6}}
위와같이 정렬되게 하는 방법 (배열의 첫번째값을 기준으로 정렬, 비교 기준이 같으면 입력의 순서대로 저장)
Arrays.sort(arrs, Comparator.comparingInt(o1 -> o1[0]));

{{1, 3}, {1, 5}, {2, 6}}
첫번째 값이 같으면 두번째 요소까지 고려하여 정렬하는 방법
Arrays.sort(arrs, (o1, o2) -> o1[0] == o2[0] ? Integer.compare(o1[1], o2[1]) : Integer.compare(o1[0], o2[0]));

내림차순 정렬 (첫번째 인수와 두번째 인수 순서만 서로 바꾸면 됨)
Arrays.sort(arrs, (o1, o2) -> o1[1] == o2[1] ? Integer.compare(o2[0], o1[0]) : Integer.compare(o1[1], o2[1]));


스트림에서도 똑같이 정렬 가능
.sorted((t0, t1) -> Integer.compare(t1[1], t0[1]))


만약 내부배열에 내림차순정렬을 해서 .boxed()를 썼으면 Object가 되기때문에 정렬이 안됨
.mapToInt(Integer::intValue).toArray() 로 내부배열을 int배열로 바꾸기


만약 내부배열내에서 정렬하고싶으면
Arrays.stream(sizes).map(a -> Arrays.stream(a).sorted().toArray()).toArray();

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

Math 클래스 - 수학계산을 위한 클래스
객체를 생성할 수 없지만 모든 메소드/속성이 static으로 정의돼있기때문에 객체를 생성하지 않고도 사용할 수 있음
메소드 사용시 Math.메소드() 이렇게 사용

[int] abs(int) : 절대값
[double] random() : 랜덤
[double] sqrt(double) : 제곱근
[double] Math.pow(double d1, double d2) : d1의 d2제곱
[int] Math.max(int i1, int i2) : i1과 i2중 큰값

기타 min, cos, sin, tan 등

----------------------------------------------------------------------------------------------------

★난수(랜덤) - 임의의 수
1. [Double] Math.random() (메소드 방식)
2. new Random() (클래스 방식)

1번방식

0.0 ~ 0.99999999999사이의 double값 반환
0(inclusive) ~ 1(exclusive)

0~9 사이의 정수
System.out.println(Math.random());
System.out.println((int)(Math.random() * 10)); ← 형변환 시킴으로 소수 이하 수를 버림
0.000 ~ 0.999 → 0
1.000 ~ 0.999 → 1
2.000 ~ 0.999 → 2
…
8.000 ~ 0.999 → 8
9.000 ~ 0.999 → 9

1~n 사이의 정수
System.out.println((int)(Math.random() * n)+1);


2번 방식

Random rnd = new Random();
inport 필요

System.out.println(rnd.nextInt()); → int 형의 난수를 발생 (-2147483648~2147483647)
System.out.println(rnd.nextDouble()); → double 형의 난수를 발생 = Math.random() 와 동일 (0.xxxxx ~ 0.99999)
System.out.println(rnd.nextBoolean()); → boolean형의 난수를 발생 (true/false)
System.out.println(rnd.nextInt(10)); → 0~9까지의 난수를 발생 = (int)Math.random()*10 와 동일

배열내 값들을 랜덤화
Random rnd = new Random();
String[] colors = {"red","yellow","blue","orange","green"};
return colors[rnd.nextInt(colors.length)];

----------------------------------------------------------------------------------------------------

★math함수 (double형)

반올림 : Math.round(n)
	소수점 n자리에서 반올림 하고싶으면 먼저 *n^10 하고 함수 적용한다음 다시 /n^10.0 해야함

반올림 & 포맷 : (String) String.format("포맷", n)
	ex) String round = String.format("%.2f", 123.456); →123.46 // Double.parseDouble 로 실수로 변경 가능
	ex) String d3format = String.format("%,.2f", 1234567.456); → 1,234,567.46 // Double.parseDouble 로 실수로 변경 불가

올림 : Math.ceil(n)
내림 : Math.floor(n)
절삭 : *n^10 → (int) 형변환 → /n^10.0
	ex) double cut = (int)(123.456 * 100) / 100.0; → 123.45

★나누기 시 .0을 붙이는 이유는 실수 / 정수 하면 정수가 되기때문에 double로 받아도 123.45 이런식으로 안되고 123일케나옴

----------------------------------------------------------------------------------------------------

숫자와 숫자사이가 몇개인지 (랜덤수 만들때 참고)

5~20 (5부터 20까지)
5이상 20이하일때 (=작은수와 큰수 둘다 포함되게 할때) : 큰수 20에서 작은수 5를 뺀다 (=15) 거기에서 1을 더한다 (=16)
5이상 20미만일때 (=작은수에서 큰수까지 차이를 구할때) : 큰수 20에서 작은수 5를 뺀다 (=15)
5초과 20미만일때 (=작은수와 큰수 사이에 있는 값만 구할때) : 큰수 20에서 작은수 5를 뺀다 (=15) 거기에서 1을 뺀다 (=14)

----------------------------------------------------------------------------------------------------

★자리수(길이) 구하기

문자열 - 문자열을 구성하는 문자의 개수(글자 수)
int len = txt.length()

숫자
int length = (int)(Math.log10(num)+1);


★제곱 구하는 메소드
Math.pow(10,0) → 1.0
Math.pow(10,1) → 10.0
Math.pow(10,2) → 100.0

★n번째 값 구하기 - charAt(int index) (subString보다 속도가 빠르다)   ★0번지부터 연산   ★값을 받을때 int(문자코드) char(문자) 중 선택가능
String temp = "ABCDEFG";
System.out.println(temp.charAt(4));
결과값 : E

★문자열의 마지막 문자 (true/false값 반환) - endsWith(String)
String temp = "ABCDEFG";
System.out.println(temp.endsWith("G"));
결과값 : true

★문자열 자르기(엑셀의mid, 자스의slice) - substring(int index, int index)   ★0번지부터 연산
String temp = "ABCDEFG";
System.out.println(temp.subString(0, 3));
결과값 : ABC

----------------------------------------------------------------------------------------------------

★메소드 접두어

-setXXX() : 값 대입(쓰기)
-setXXX() : 값 반환(읽기)
-isXXX() : 확인. true/false 반환

----------------------------------------------------------------------------------------------------

★디버깅
ctrl + shift + b 로 마크한 상태로 f11눌러서 디버그모드 진입 → f5 또는 f6으로 한 라인씩 이동하면서 확인

----------------------------------------------------------------------------------------------------

★문자열 세자리 콤마 (문자열로 받기때문에 글자수 제한없음)

System.out.print("숫자 : ");
String str= reader.readLine();
String str2="";
int count=0;
for(int i=str.length()-1; i>=0; i--) {
	char c1=str.charAt(i);
	str2+=c1;
	count++;
	if(i==0) {
		break;
	}
	if(count==3) {
		str2+=",";
		count=0;
	}
}
for(int i=str2.length()-1; i>=0; i--) {
	char c1= str2.charAt(i);
	System.out.print(c1);
}

----------------------------------------------------------------------------------------------------

객체 깊은복사

1. 객체가 속한 클래스에서 Cloneable를 implements 한다
@ToString
@AllArgsConstructor
public class C1 implements Cloneable {
	public String name;
	public int age;

2. 복제 메소드를 생성한다 (이때 clone()메소드가 반환하는 Object클래스를 현재 클래스로 형변환 해야함)
public C1 getC1() {
	C1 clone = null;
	try {
		clone = (C1) clone();
	} catch (Exception e) {
		System.out.println("C1.clone()");
		e.printStackTrace();
	}
	return clone;
}
↑ 동일한 코드. 메소드명을 clone으로 쓰고싶을경우 아래처럼 쓰기 ↓
public C1 clone() {
	C1 clone = null;
	try {
		clone = (C1) super.clone();
	} catch (Exception e) {
		System.out.println("C1.clone()");
		e.printStackTrace();
	}
	return clone;
}
↑ 동일한 코드 ↓
public C1 clone() throws CloneNotSupportedException {
	return (C1) super.clone();
}


3. 객체 복제가 필요한곳에서 객체에 메소드 쓰기

C1 c1 = new C1("김준수",11);
System.out.println(c1);

C1 c2 = c1.clone();
System.out.println(c2);


4. 객체의 속성을 변경해도 원본 데이터가 바뀌지 않음을 확인
c2.name = "유아인";
System.out.println(c1);
System.out.println(c2);


CloneNotSupportedException
Cloneable 인터페이스 implement 해야함

----------------------------------------------------------------------------------------------------

객체와 인스턴스 차이

둘다 비슷한 말이나,

객체는 "실체"
인스턴스는 "관계"

에 초점을 맞춘다

★클래스가 붕어빵 틀이라면 그 틀을 통해 생성된 붕어빵(객체) 하나하나를 해당 클래스의 인스턴스(Instance)라고 부른다

자바 프로그램 실행시 클래스는 JVM메모리의 클래스 영역(Class Area)에 로드되고,
이 클래스를 사용하여 힙 영역(Heap Area)에 새로운 인스턴스(객체)를 생성할 수 있다

----------------------------------------------------------------------------------------------------

JVM의 메모리 구조

응용프로그램이 실행되면
JVM은 시스템으로부터 프로그램을 수행하는 데 필요한 메모리를 할당받고
JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다

그중 3가지 주요영억(method area, call stack, heap) 가 있음


1. 메소드 영역(method area)
프로그램 실행 중 어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스파일(*.class)을 읽어서 분석하여 클래스에 대한 정보(클래스 데이터)를
이곳에 저장한다. 이 때, 그 클래스의 클래스변수(class variable)도 이 영역에 함께 생성된다

2. 힙(heap)
인스턴스가 생성되는 공간. 프로그램 실행 중 생성되는 인스턴스는 모두 이곳에 생성된다
즉, 인스턴스변수(instance variable)들이 생성되는 공간이다

3. 호출 스택(call stack 또는 execution stack)
호출스택은 메소드의 작업에 필요한 메모리 공간을 제공한다
메소드(main메소드 포함)가 호출되면, 호출스택에 호출된 메소드를 위한 메모리가 할당되며,
이 메모리는 메소드가 작업을 수행하는 동안 지역변수(매개변수 포함)들과
연산의 중간결과 등을 저장하는 데 사용된다. 그리고 메소드가 작업을 마치면 할당되었던 메모리공간은 반환되어 비워진다

----------------------------------------------------------------------------------------------------

클래스 멤버변수
	인스턴스 변수
		인스턴스가 생성될때마다 생성되는 변수
		static이 안붙은 변수
		객체를 생성해야 사용이 가능함
		객체마다 다른값을 가져야할때 씀
	클래스 변수
		인스턴스를 생성하지 않고도 쓸 수 있음
		static이 붙은 변수
		모든 인스턴스가 공통적으로 같은 값을 유지해야하는 속성
		클래스변수는 객체.변수 이렇게 하는것보다는 클래스.변수 이렇게 쓰는게 바람직함(클래스변수를 인스턴스변수로 오해할 수도 있기 때문)
		모든 인스턴스가 하나의 저장공간을 공유하므로 항상 같은 값을 공유한다
		인스턴스가 생성될 때 만들어지는게 아님

지역 변수
	메소드 안에서 선언된 변수
	제어문 안에서 선언된 변수

밖에서 만든걸 안에서 사용하는것은 가능 , 안에서만든걸 밖으로 들고 나가는것은 불가능

------------------------------

클래스 메소드 vs 인스턴스 메소드

변수와 마찬가지로
메소드 앞에 static이 붙어있으면 클래스메소드, 붙어있지 않으면 인스턴스 메소드다


인스턴스 메소드
인스턴스 변수와 관련된 작업을 하는, 즉 메소드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메소드

클래스 메소드(static메소드)
인스턴스와 관계없는(인스턴스 변수나 인스턴스 메소드를 이용하지 않는) 메소드

------------------------------

클래스를 설계할때, 멤버변수 중 모든 인스턴스에 공통으로 사용하는 것에 static을 붙인다
	생성된 각 인스턴스는 서로 독립적이기 때문에 각 인스턴스의 변수는 서로 다른 값을 유지한다
	그러나 모든 인스턴스에서 같은 값이 유지되어야 하는 변수는 static을 붙여서 클래스 변수로 정의해야한다

클래스 변수(static변수)는 인스턴스를 생성하지 않아도 사용할 수 있다
	static이 붙은 변수(클래스변수)는 클래스가 메모리에 올라갈 때 이미 자동적으로 생성되기 때문이다

클래스 메소드(static메소드)는 인스턴스 변수를 사용할 수 없다
	인스턴스변수는 인스턴스가 반드시 존재해야만 사용할 수 있는데, 클래스 메소드(static이 붙은 메소드)는 인스턴스 생성 없이 호출가능하므로
	클래스메소드가 호출되었을때 인스턴스가 존재하지 않을 수도 있다. 그래서 클래스 메소드에서 인스턴스변수의 사용을 금지한다
	반면에 인스턴스변수나 인스턴스메소드에서는 static이 붙은 멤버들을 사용하는것이 언제나 가능하다
	인스턴스변수가 존재한다는 것은 static변수가 이미 메모리에 존재한다는 것을 의미하기 때문이다

메소드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려한다
	메소드의 작업내용 중에서 인스턴스변수를 필요로 한다면, static을 붙일 수 없다.
	반대로 인스턴스변수를 필요로 하지 않는다면, static을 붙이자. 메소드 호출시간이 짧아지므로 성능이 향상된다.
	static을 안 붙인 메소드(인스턴스메소드)는 실행 시 호출되어야할 메소드를 찾는 과정이 추가적으로 필요하기 때문에 시간이 더 걸린다

참고로 random()과  같은 Math클래스의 메소드는 모두 클래스메소드이다. Math클래스에는 인스턴스변수가 하나도 없거니와
작업을 수행하는데 필요한 값들을 모두 매개변수로 받아서 처리하기 때문이다.

----------------------------------------------------------------------------------------------------

기본형 매개변수 vs 참조형 매개변수

기본형 매개변수 : 변수의 값을 읽기만 할 수 있음(read only). 8개 기본자료형(primitive type)이 해당
참조형 매개변수 : 변수의 값을 읽고 변경할 수 있음(read & write). 배열을 포함한 그외 나머지 타입(reference type)이 해당


public class Run {
	public static void main(String[] args) {

		int i = 0;
		System.out.println(i);

		m1(i);
		System.out.println(i);

		System.out.println("------------------------------");

		C1 c1 = new C1();
		System.out.println(c1.i1);

		m2(c1);
		System.out.println(c1.i1);

		System.out.println("------------------------------");

		int[] arr = {0};
		System.out.println(Arrays.toString(arr));

		m3(arr);
		System.out.println(Arrays.toString(arr));

	}

	private static void m1(int i) {
		i = 10; // 기본형 매개변수는 값을 복사해오기때문에 복사한 값을 변경해도 기존값에 영향을 미치지 못함
	}

	private static void m2(C1 c1){
		c1.i1 = 10; // 참조형 매개변수는 주소를 가져오기때문에 값 변경가능
	}

	private static void m3(int[] arr) {
		arr[0] = 10; // 배열도 마찬가지로 주소를 가져오기때문에 값 변경가능
	}
}

class C1{
	int i1;
}

----------------------------------------------------------------------------------------------------

1. 절차 지향 프로그래밍
	- 순서를 중요
	- C

02. 객체 지향 프로그래밍
	- 객체를 중심
	- C++ ,  Java , C# , JavaScript

3. 함수형 프로그래밍
	- F# , Kotlin , Java(일부)

객체, Object
	- 캡슐화, Encapsulation
	- 상속, Inheritance
	- 다형성, Polymorphism

	- 데이터, Data
	- 행동, Behavior
	- 상태, State
	- 은닉화
	- 인터페이스
	- 추상화
	- 독자성

	- 인식/구별 가능 (사물/생물/미생물)
	프로그램업무
	ex) 	사람 직접 업무 → 전산화
		식당 종업원 → 키오스크(프로그램)

클래스, Class
	- 코드의 집합 (생김새만 보면)
	- container 역할만 하는게 아니고 (비중적음)
	- 객체 생성 (가장 큰 역할) 그에따른 자료형 역할
		class ClassName {
			/*설계 내용 → 클래스 멤버
			1. 맴버 변수 → 데이터 , 상태(State) , 성질 ★★★
			2. 멤버 메소드 → 기능 , 행동(Behavior) ★
			3. 변수(데이터) + 메소드(행동)집합 ★★★★★
			*/
		}

	- 접근 지정자(접근 제어자), Access Modifier
	- public / private / protected / default
	- 클래스를 경계로 내부의 멤버(변수, 메소드)를 외부에 공개할지를 결정하는 보안 단계
		1. private : 같은 클래스 내에서만 접근 가능
		2. default : 같은 패키지 내에서만 접근 가능
		3. public : 접근 제한이 전혀 없음
		4. protected : 상속받은 클래스 또는 같은 패키지에서만 접근가능
		
	멤버 변수의 접근지정자는 항상 private로 한다

	public static void main(String[] args){
		Dog puppy = new Dog();
		
		puppy.setName("퍼피");
		puppy.setAge(23);
		System.out.println(puppy.getName());
		System.out.println(puppy.getAge());
	}

	class Dog{
		private String name;
		private int age;
		private String color;
		// - setXXX : setter(세터) , 쓰기용도
		public void setName(String name) {
			this.name = name;
		}
		public void setAge(int age) {
		if (age>0 && age<25) {
				this.age = age;
			}else {
				System.out.println("강아지 나이로 올바르지 않습니다.");
			}
		}
		// - getXXX : getter(게터) , 읽기용도
		public String getName(){
			return this.name;
		}
		public int getAge(){
			return this.age;
		}
	}

ex1)
붕어빵틀 → 붕어빵 → 객체 사용
		클래스 → 객체 / 인스턴스
		1	2	3
		설계도
ex2)
클래스 :
	삼성 휴대폰공장의 설계도 (한가지 이상의 휴대폰을 만들기위해 공통적으로 필요한 속성과 기능들을 모아놓은것)
	제품명, 제품의 크기, 제품의 무게 등(특성→속성)
	패턴잠금, 생체인식기술 등(기능→메소드)

객체 :
	- 소프트웨어 세계 안에서 구현해야할 대상
	- 갤럭시 s20, s30 등
	- 선언한 객체는 아직 어떠한 메모리도 차지하지 않음 (아직 사용은불가)
	samsungPhone Galaxy20, Galaxy30;

인스턴스 :
	- 객체가 실제로 구현된 실체
	- 실제로 메모리에 할당된 상태
	- 객체와 같거나 객체에 포함되는 말
	samsungPhone Galaxy20 = new samsungPhone();
	samsungPhone Galaxy30 = new samsungPhone();


setter/getter 자동생성 : 객체에 포커스 두고 단축키 alt + shift + s r →Select All 이나 원하는 항목 선택 후
Insertion point에서 위치 지정 후 Generate
★세터/게터를 이용하면 변수를 static변수로 만들지 않고도 쓰고 부르기가 가능해진다
ex)
public class UsedPC {
	private String usedPoint;
	private String usedCoupon;
	
	public UsedPC(String usedPoint, String usedCoupon) { ★①
		super();
		this.usedPoint = usedPoint;
		this.usedCoupon = usedCoupon;
	}
	
	public String getUsedPoint() {
		return usedPoint;
	}
	public void setUsedPoint(String usedPoint) {
		this.usedPoint = usedPoint;
	}
	public String getUsedCoupon() {
		return usedCoupon;
	}
	public void setUsedCoupon(String usedCoupon) {
		this.usedCoupon = usedCoupon;
	}
}
이렇게 ①번처럼 메소드로 값을 넣을수있게 해놓고 (이걸 생성자 오버로딩이라고 한다)
이러면 UsedPc used = new UsedPc() 이방법으로는 객체를 만들수없고
만들고싶으면 UsedPc클래스에 빈 UsedPc used = new UsedPc(){} 메소드를 오버로딩하기

다른곳에서 UsedPc used = new UsedPc(point, coupon); 이렇게 객체 만든다음 setter안쓰고 객체의 값을 입력(저장)한후
Payment.main(userInfo, movieInfo, used); 이런식으로
다른곳으로 넘겨서 used.getUsedPoint() , used.getUsedCoupon()
이런식으로 객체의 값 꺼내기가능

보통 하나의 파일에 하나의 클래스만 사용
파일내에서 여러개의 클래스를 선언하는 경우, 반드시 1개의 클래스를 public으로 선언하고 그 클래스명이 파일명이 된다
1. 코드관리 + 가독성 > 목적이 같은 코드를 물리적 분리
2. 재사용 편의

인스턴스, Instance


배열 과 클래스 차이점
	- 배열 : 첨자 사용 > 순환 용이
	- 클래스 : 멤버변수명 사용 > 가독성 높음
	- 배열 : 같은 자료형 + 모든 멤버가 동일한 성격의 데이터
	- 클래스 : 다른 자료형 + 각각의 멤버가 서로 다른 성격의 데이터

----------------------------------------------------------------------------------------------------

this

인스턴스 자신을 가리키는 참조변수
인스턴스의 주소가 저장되어 있다
모든 인스턴스메소드에 지역변수로 숨겨진 채로 존재한다


this(), this(인수)

같은 클래스의 다른 생성자를 호출할 경우, 생성자의 첫줄에서 사용함

------------------------------

super - 부모클래스의 메소드/멤버변수를 자식클래스에서 호출할때 사용
super.멤버변수 : 부모클래스의 멤버변수를 호출 (메소드에서 같은이름의 파라미터와 자기멤버변수를 구분할때 this.멤버변수
	이렇게 사용하듯이 부모의 멤버변수를 사용해야할때 자기 멤버변수와 구분하기 위해 사용)
super.메소드() : 부모클래스의 메소드를 호출


super() : 부모클래스의 생성자/또다른 생성자(파라미터가 있는) 를 호출 (자식클래스 생성자속 첫줄에서 한번만 사용 가능,
	클래스 생성자에 this()또는 super()를 안넣을시 컴파일러가 생성자 맨 위에 자동적으로 "super()"을 호출함
	파라미터가 있으면 super(파라미터1,파라미터2...) 이렇게 사용


만약 부모클래스의 생성자를 기본으로 하지 않고 변경했을경우 ex)String을 매개변수로 받는 생성자
자식클래스에서는 부모의 기본생성자를 자동으로 호출하기 때문에 (컴파일러가 자동호출함)
ex)부모에 name, 자식에 ton 속성이 있을때
자식클래스의 생성자에서
public Truck(String name, int ton) {
	super(name);
	this.ton = ton;
}
이런식으로 직접 부모의 또다른 생성자를 연결해주어야한다

----------------------------------------------------------------------------------------------------

★생성자(constructor)
- 특수한 목적을 가지는 메소드
- 객체의 멤버를 초기화하는 목적을 가지는 메소드
- 사용법이 일반 메소드와는 상이함
- 객체 생성을 사용자(개발자) 편의에 맞게 다양하게 하기 위해서
- 하지만 사용시 먼저 상위클래스/상위클래스들에 대한 완벽한 이해가 필요

- ex) 클래스명 객체명 = new 클래스명();
	          ↑     ↑	    ↑
	          ③     ①	    ②
① 객체생성연산자, new키워드 - '클래스를 메모리에 올려주세요' 라는 뜻,
	이렇게 메모리에 올라간 클래스를 인스턴스라고 한다
② 생성자 - 객체 생성 시 초기화 작업을 위한 함수로써, 객체를 생성할 때 반드시 호출되고, 제일 먼저 실행된다
③ 메모리에 올라간 인스턴스를 가리키는 변수, 참조하는 변수, 레퍼런스하는 변수
	변수가 인스턴스를 가지고 있는것이 아닌, 참조(가리킴)한다

기본 생성자
- 개발자가 명시적으로 선언하지 않아도 컴파일러가 만들어주는 생성자
- 멤버 변수를 초기화하는 역할

멤버변수 자동 초기값
1. 정수 → 0
2. 실수 → 0.0
3. 문자 → \0
4. 논리 → false
5. 참조 → null

-----

★객체 생성후 만들어진 객체를 변수에 대입 안하고 익명으로 바로 쓸 수도 있음
클래스1 변수 = new XXX()
메소드1(변수);				// 이렇게 선언한다음 보내지않고
메소드1(new XXX())		//이런식으로

return new XXX()			// 이것도 당연히 가능

-----

★생성자를 선언한 클래스에 있는 "protected/private"말고 "public"으로 선언된 메소드를 바로 쓸 수 있음 (상속받아온 클래스에있는 메소드도 쓸 수 있음)
이때 메소드 반환타입이 객체가 아닐경우 객체로 받을 수 없음 (반환타입이 String이나 int등이면 XXX = new XXX() 이렇게 못받는다는뜻)

new XXX().메소드1()

-----

★자기 클래스를 반환하면 메소드 체인형식으로 쓸 수 있음

public 자기클래스 title(String title) {
	this.sheet = this.workbook.createSheet(title); // 하고싶은 기능을 수행하고
	return this; // 자기 자신을 반환
}

그러면 아래처럼 줄줄이 쓸 수 있음

new C1("aaa",12).m2().m3().parent_m1();

----------------------------------------------------------------------------------------------------

★스태틱(static) - 클래스 멤버에게 붙이는 키워드
1. 멤버 변수
2. 멤버 메소드

같은 틀(클래스)에서 찍어낸 인스턴스들이
서로 다른 값을 가지는 경우(각자만의 개성) - 객체 안에 생성된다고 해서 객체멤버변수 (instance)
공통된 값을 가지는 경우(그룹) - static 영역에 해당 클래스영역에 생성됨

접근지정자와 자료형 사이에 static 추가 (정적메소드)
private static String brand;

★프로그램 실행 순서
1. 클래스 로드 : 클래스 선언 코드를 미리 읽고 내용을 파악하는 작업
  - 시스템이 static 키워드 가진 멤버를 만나면 > siatic 영역에 할당시킴
2. main() 메소드 실행


★인스턴스 개수세기 (여러가지 방법중 이 방법이 가장 효율적)
System.out.println(Robot.count);

class ddd{
	public static int count;

	public Robot(){
		Robot.count++;
	}
}

----------------------------------------------------------------------------------------------------

★프로젝트(Project)

하나의 실행파일 단위
하나의 실행파일을 생성하기 위한 단위라고 할 수 있음
워크스페이스의 하위 폴더로 생성됨

프로젝트 명명규칙
- 대소문자 구분없이 시작 가능
- 첫 문자를 비롯해 모든 단어는 대문자 시작을 권장


프로젝트 구현시

- 프로젝트 할 때 데이터양은 많을수록 좋다
- 진짜 데이터 다량 확보

데이터 직접 만들기
프로젝트 구현 → 더미 데이터 → 서비스 오픈 최소 2~3개월 지났을 때의 데이터 분량 확보

회원 관리 프로그램
- 회원정보 x 1000명
- a 이름 : 문자열
- b 나이 : 숫자
- c 성별 : 숫자(1.남자, 2.여자)
- d 주소 : 문자열

----------------------------------------------------------------------------------------------------

★패키지(package) - 패키지가 다르면 클래스의 이름이 중복되도 상관없다
- 클래스를 기능별로 묶어둔 물리적인 폴더
- 클래스 관리, 클래스 용도를 명확하게 알아보게 하기 위함
- 소스코드를 저장하는 .java 파일의 패키지는 프로젝트 폴더 아래 src 폴더에 저장됨
- .java파일을 컴파일해서 생성된 .class 파일의 패키지는 프로젝트 폴더 아래 bin 폴더에 저장됨
ex) java.io.BufferedReader

패키지 명명법(이름짓는법)
- 모든 문자를 소문자로 작성한다
- 공백 금지, 숫자 금지, 특수문자 금지 = 모두 영소문자로만
- 전세계의 모든 패키지와 비교해서 중복되지 않도록
  - 주로 도메인을 사용 ex) com.naver.xxx / com.google.xxx
  - 최소 3단계 이상을 사용
    - ex) test : 1단계 패키지
    - ex) com.test : 2단계 패키지
    - ex) com.test.java : 3단계 패키지 (권장)

★inport - 다른 패키지의 클래스를 인식하게 만드는 도구 (반드시 같은 프로젝트 내에 있는 패키지(클래스)만 인식 가능
import com.test.aaa.Desk;

현재 패키지의 클래스와 다른 패키지의 클래스를 동시에 사용하고 싶을때
SmartPhone s1 = new SmartPhone(); → 현재 패키지 사용
com.test.aaa.SmartPhone s2 = new com.test.aaa.SmartPhone(); → 다른 패키지 사용


★'수정 불가, 사용만 가능' 배포파일 만들기
다른사람이 만든 소스원본 말고 컴파일된걸 가져다 쓸때 사용하는 기능

배포방법
프로젝트우클릭 → Export → Java → JAR file → Next → 배포할 패키지만 선택하고 나머지는 선택해제 → 우측에 클래스가 보임 → 원하는 클래스 선택 후 →
아래 Browse.. 버튼 클릭 → 원하는 폴더 / 파일이름 지정 → 저장

받는방법
파일탐색기에서 jar파일 압축해제 → 프로젝트에 lib 폴더 하나 생성후 → 프로젝트에서 우클릭 → Build Path → Configure Build Path
→ 상단 탭에서 Libraries → Add JARs → 폴더 찾아서 OK → Apply and Close
다 되면 Package Explorer창에 Referenced Libraries폴더가 생기고 그 안에 jar파일이 들어있음

참고 : https://hamait.tistory.com/351

----------------------------------------------------------------------------------------------------

클래스

비슷한 유형의 메소드(함수)와 변수를 모아놓은 코드
실제로 작성된 가장 하위의 소스코드 파일
클래스의 파일명은 클래스명과 동일해야함

------------------------------

클래스 명명 규칙

대문자로 시작
명사로 시작
파스칼 케이스 권장

----------------------------------------------------------------------------------------------------

메소드

클래스에 정의되어있는 함수
패키지A.패키지B.클래스C.메소드(argument)의 형태로 불러와서 실행함

------------------------------

메소드 명명 규칙

소문자로 시작
동사로 시작
카멜 케이스 권장

----------------------------------------------------------------------------------------------------

포함되는 구조

프로젝트 > 패키지 > 클래스 > 메소드 > 코드

----------------------------------------------------------------------------------------------------

★상속(inheritance) - 클래스와 클래스간에 재산을 물려주는 행위
  - 재산 : 클래스가 소유하고 있는 코드(멤버 변수, 멤버 메소드)
  - '부모 클래스가 가지고 있는 코드를 자식 클래스에게 물려준다'
  - 장점 : 코드 재사용가능
  - 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다
  - 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다

class Parent{
	public int a;
	public int b;
	public void ccc() {
		System.out.println("ccc");
	}
}

class Child extends Parent{
	public int d;
	public int e;
}

부모클래스 = 슈퍼클래스
자식클래스 = 서브클래스

------------------------------

포함관계 (Composite)

상속을 통해 클래스 간에 관계를 맺어주는 방법이 있는데,
상속 외에도 클래스를 재사용하는 방법이 있음. 포함관계를 맺으면 됨

★한 클래스의 멤버변수로 다른 클래스 타입의 참조변수를 선언하는 것을 뜻함


ex) 재사용이 가능한 멤버를 따로 빼서, 멤버변수에서 생성자로 초기화해서 쓰기

public class Run {
	public static void main(String[] args) {
		Circle c = new Circle();
		System.out.println(c.p.x);
		System.out.println(c.p.y);
		System.out.println(c.z);
	}
}

class Circle{
//	int x;
//	int y;
	Point p = new Point();
	int z = 3;
}

class Point{
	int x = 1;
	int y = 2;
}

------------------------------

상속관계를 맺을건지 포함관계를 맺을건지 헷갈리면 아래에 대입해 문장을 만들어서 어떤게 성립하는지 생각해보기

~는 ~다 (is-a) → 상속관계
~는 ~를 가지고 있다 (has-a) → 포함관계

-----

ex) 원(Circle) / 점(Point)
1. 원(Circle)은 점(Point)이다. - Circle is a Point.
2. 원(Circle)은 점(Point)을 가지고 있다. - Circle has a Point.

원은 원점(Point)과 반지름으로 구성되므로 위의 두 문장을 비교해 보면 1번문장보다 2번문장이 더 옳다는 것을 알 수 있다
때문에 Circle클래스와 Point클래스간의 관계는 상속관계보다 포함관계를 맺어주는 것이 더 옳다

-----

ex) 자동차(Car) / 스포츠카(SportCar)
1. 스포츠카는 자동차다.
2. 자동차는 스포츠카를 가지고 있다.

2번보다 1번과 같이 문장을 만드는 것이 더 옳기때문에, 이 두 클래스는 Car클래스를 조상으로 하는 상속관계를 맺어 주어야 한다

-----

ex) 카드(Card) / 덱(Deck)
1. 덱은 카드다
2. 덱은 카드를 가지고 있다

2번 문장이 더 옳기때문에 Deck클래스에 Card클래스를 포함시켜야 한다

-----

ex) 점(Point)과 도형(Shape)이 있고 이 두 클래스를 재활용해서 원(Circle) 클래스와 삼각형(Triangle) 클래스를 정의

1. 원은 도형이다
2. 원은 도형을 가지고 있다
3. 원은 점이다
4. 원은 점을 가지고 있다

2번보다는 1번이, 3번보다는 4번이 자연스러우므로
원과 도형은 상속관계로, 원과 점은 포함관계로 한다

------------------------------

프로그램의 모든 클래스를 분석하여, 가능한 많은 관계를 맺도록 노력해서, 코드의 재사용성을 높여야 한다

----------------------------------------------------------------------------------------------------

일반 클래스 = 변수 + 메소드
추상 클래스 = 변수 + 메소드 + 추상 메소드
인터페이스 = 모든 메소드가 추상 메소드

상속의 구성원이 될 수 있는 요소
- 일반클래스, 추상클래스, 인터페이스
        자식		     부모
1. 일반클래스	일반클래스 : O
2. 일반클래스	추상클래스 : O
3. 일반클래스	인터페이스 : O
4. 추상클래스	일반클래스 : O(절대 사용 안함) 자식은 구체화,부모는 추상적이여야한다
5. 인터페이스	일반클래스 : X(절대불가능),구현된 멤버를 상속하기 떄문 (인터페이스는 추상멤버만 가질 수 있음)
6. 추상클래스	인터페이스 : O(추상클래스도 추상메소드를 가질 수 있어서)
7. 인터페이스	추상클래스 : X(5번과 동일) 인터페이스는 일반변수를 가질수없기때문
8. 인터페이스	추상클래스 : O
9. 인터페이스	인터페이스 : O
10. 일반클래스 → 일반클래스 → 추상클래스 → 추상클래스 → 인터페이스 → 인터페이스

----------------------------------------------------------------------------------------------------

abstract - 추상의, 미완성의

------------------------------

추상 클래스 = 변수 + 메소드 + 추상 메소드

- 거의 공통적인 구조를 갖고있을때 사용
- 목적이 일반 클래스와 다름
- 일반 클래스의 목적 : 객체 생성
- 객체 생성 불가능 객체의 행동을 표준화★★★
- 추상 클래스는 객체 생성은 불가능하지만, 상속 관계에서 클래스 부모역할은 가능하다
- 추상 메소드를 자식들에게 강제로 만들라고 시키려고 → 추상클래스의 하위클래스들은 모두 사용법이 동일해진다

------------------------------

추상 메소드(abstract method)
- abstract methods do not specify a body
- 메소드 구현부를 가질 수 없다

//추상멤버선언
public abstract void on();

ex)
abstract class keyboard{
	public int num;
	public void test() {
		
	}
	public abstract void vvv();
}

----------------------------------------------------------------------------------------------------

메소드 오버라이드(method override)(재정의)

- 메소드 제정의(기존의 메소드를 무시하고 새로 구현한다)
- 메소드 헤더(시그니처) + 메소드 바디(구현부)
- 메소드 헤더를 그대로 두고, 메소드 바디를 재정의
- 상속에서 발생 → 자식 클래스에서 발생
- 부모가 물려준 메소드를 그대로 명시적 선언을 하면 부모메소드를 감춘다 → 부모 메소드와 자식 메소드를 공존하게 해준다

System.out.println(t1.info());//다른개발자가 이게 어던 기능인지 몰라
System.out.println(t1); //전세계 개발자가 이 결과가 뭔지 알고 있음
System.out.println(t1.toString()); //전세계 개발자가 이 결과 뭔지 알고 있음

----------------------------------------------------------------------------------------------------

final 변수 , (이름이 있는)상수
한번 초기값을 설정하면 변경불가

int NUM = 10; ← X
final int age = 20; ← X

상수는 대문자 , 일반 변수는 소문자로 표기

final 메소드 - 상속시 발생하는 안전성 문제때문에
상속받을때 내용을 변경하지 못함
잘 모르겠으면 final로 만들라

final 클래스 - 상속 불가



★참조형 형변환
- 클래스끼리 가능
- 상속 관계를 맺은 클래스끼리만 가능☆☆ 즉 부모자식관계에서만 가능
자식클래스 → 부모클래스 : 암시적 , 업캐스팅 , 100%안전
부모클래스 → 자식클래스 : 명시적 , 다운캐스팅

AA a1 = new AA();//자기 타입
AA a2 = new BB();//부모 = 자식 , 업캐스팅
AA a3 = new CC();//할아버지 = 자식 , 업캐스팅
AA a4 = new DD();//증조할아버지 = 자식 , 업캐스팅

Object o1 = new Object();
Object o2 = new AA();
Object o3 = new BB();
Object o4 = new CC();
Object o5 = new DD();
Object o6 = new Random();
Object o7 = Calendar.getInstance();
Object o8 = new Date();
Object o9 = new int[5];
Object o10 = "한채아";

현존하는 모든 클래스의 최상위에는 Object 클래스가 있다.
Object 변수는 값형 데이터도 담을 수 있다(만능주머니)
→업캐스팅은 세대수와 상관없이 가능하기 떄문에 결국 자바에 존재하는 모든 클래스는 Object 참조변수에 넣을 수 있다.☆☆☆


Human human = new Human("asd",12,132.4f);
Wrapper wrapper = human.clone();
Clone clone = (Clone) wrapper;
위 코드 실행시
↓↓↓
~~~.Wrapper cannot be cast to ~~~.Clone
이렇게 공통된 부모클래스에서 다운캐스팅을 할때 위와같은 예외가 발생하는 이유는
Wrapper로 감싸도 실제 인스턴스는 Human 객체이기 때문이다 (이경우에는 Wrapper로 받거나 copyProperties메소드를 사용해야함)

----------------------------------------------------------------------------------------------------

@Override //어노텐션(annotation) - 컴파일러가 인식하는 주석 (필수는 아니고 안전장치같은 키워드)

----------------------------------------------------------------------------------------------------

인터페이스 - 회원이 가져야할 (행동)규칙 (사용법은 똑같지만 구조가 다른경우)

------------------------------

쉬운 설명

만약에 못을 박는것이 목적이라면 조수에게 "공구함에서 망치를 가져와라" 라고 말하면 그만이지,
굳이 공구함에서 길이가 약 30cm 가량이고 무게 1kg정도 되는 목재의 손잡이로 된 망치를 들고와라" 라고 말 할 필요가 없다

목공이 조수에게 부탁을 할 때나, 개발자가 코드를 짤 때나 의도를 명확하고 간결하게 표현하는 것은 중요하다
목적이 못을 박는 것이고, 순서가 보존되는 컬렉션에 값을 보관하는 것이라면 그냥 '망치' 또는 'List' 라고 하면 그만이다

그 밖에 망치의 손잡이가 목재로 되어있다거나 List의 인터페이스가 배열을 기반으로 구현되었다거나 하는 것은 모두 '구현상 디테일'에 해당하는 부분임
그런 부분을 불필요하게 강제하면 의도를 오해할 수 있고,
또 실제 길이가 좀 짧은 망치나 'LinkedList' 같은 인스턴스가 이미 있음에도 조건을 충족하지 못해서 바로 원하는 작업을 실행할 수 없는 경우도 있음

따라서 특히 인터페이스나 공요클래스 등의 시그니처에 표현되는 유형은
가능하면 의도를 명확하게 할 수 있는 선에서 최대한 일반적인 상위 유형을 명시하는 것이 좋은 습관이라고 할 수 있음

------------------------------

인터페이스 = 추상 메소드
난이도 ☆☆

public static void main(String[] args) {
	AAA a = new AAA(); → 인터페이스는 객체를 못만듬
	BBB b = new BBB();
	b.test();
	b.output();
	
	AAA c = new BBB(); //업캐스팅
	c.test();
	c.output(); → 불가
}

interface AAA {
	//추상 메소드만 올 수 있다
	//인터페이스의 멤버는 무조건 공개를 원칙으로 한다 (public)

	//일반 멤버 변수는 못만든다
	public int aaa;

	//일반 멤버 메소드는 못만든다
	public void dasd() {
		
	};

	public abstract void aaa();
	void bbb(); //public abstract void bbb();

	default int test2(int a) { // 기본 메소드. 재정의를 해도 되고 안해도 됨. interface에서만 쓸 수 있음
		return a + 2;
	}
//	int test2(int a); // default메소드와 일반 메소드를 동시에 쓰는건 불가
}

class BBB implements AAA{
	@Override
	public void test() {
		System.out.println("인터페이스 구현 객체의 test() 메소드");
	}
	
	public void output() {
		System.out.println("본인이 직접 구현한 output() 메소드");
	}
}

----------------------------------------------------------------------------------------------------

여러 클래스에서 하나의 변수 가져오기

Var.java 클래스파일 하나 만들고 setter/getter 만든다음 (다른 패키지도 괜찮음)

필요한 파일에서
import data.Var; 이렇게 가져오기

----------------------------------------------------------------------------------------------------

열거형(enumeration)

- 클래스의 일종
- 열거값을 가지는 자료형(=제시한 값 중에서 선택해서 사용해는 자료형)


case 1. 주관식
- 오타가능성
- 구현하기 편함
- 가독성 좋음
- 유효성 검사 필수
String color = "blue";
if(color.equals("blue")){}

case 2. 객관식
- 구현하기 편함
- 가독성 낮음(코드상)
- 유효성 검사
- 많이 사용
int color2 = 2;
if(color2 == 2){}

case 3. 열거형 (enum)
- 객관식에 높은 방식
- 가독성 높음(코드상에서)
- 유효성 검사 필요 없음
- equals를 안쓰고 ==를 쓸 수 있음

Color color3 = Color.RED;
System.out.println(color3);

enum Color{
	RED,
	BLUE,
	YELLOW
}

열거형을 문자열로 변환
String name = Direction.WEST.name();
System.out.println(name.equals("WEST"));

문자열을 열거형으로 변환
Direction d = Direction.valueOf("WEST");
System.out.println(d == Direction.WEST);

----------------------------------------------------------------------------------------------------

오브젝트(Object)
- 장점
  - 모든 자료형을 넣을 수 있다 > 코드비용 감소
- 단점
  - 데이터를 꺼내어 활용할 떄 어떤 자료형의 데이터가 들어 있었는지 알기 힘들다.
  - 잘못된 형변환을 할 수 있다 > 예외발생 > 프로그램 안전성 감소

WrapperObject o1 = new WrapperObject(200); //업캐스팅
System.out.println(o1);
System.out.println((int)o1.getData()*2); //다운캐스팅 → Object * int

WrapperObject o2 = new WrapperObject("아무개"); //업캐스팅
System.out.println(o2);
System.out.println(((String)o2.getData()).length()); //다운캐스팅 → Object * int

class WrapperObject{
	private Object data; //주인공, 클래스의 중심요소
	
	public WrapperObject(Object data) {
		this.data = data;
	}
	
	public void setData(Object data) {
		this.data = data;
	}
	
	public Object getData() {
		return this.data;
	}
	
	@Override
	public String toString() {
		return this.data+"";
	}
}

----------------------------------------------------------------------------------------------------

제네릭 클래스 (동적 타입)

class Box<T>

Box<T> : 제네릭 클래스. 'T 의 Box' 또는 'T Box' 라고 읽는다.
T : 타입 변수 또는 타입 매개변수. (T는 타입 문자)
Box : 원시 타입

Box<String> b = new Box<String>();
위처럼 타입 매개변수에 타입을 지정하는 것을 '제네릭 타입 호출' 이라고 하고,
지정된 타입 'String'을 '매개변수화된 타입' 이라고 한다.
매개변수화된 타입이라는 용어가 좀 길어서, 이 용어 대신 '대입된 타입' 이라는 용어를 사용하기도 함

------------------------------

Bag<Integer> b1 = new Bag<Integer>();
		
b1.a = 10;
b1.b = "문자열";
b1.c = 213213;

class Bag<T> {
	public int a;
	public String b;
	public T c;
	public T d;
}

------------------------------

wrapper클래스에서, 쓸 자료형을 지정할수 있게 <T>로 선언해놓고,
그 클래스를 인자값이나 리턴타입으로 쓸 때, 혹은 생성할때(ArrayList등 컬렉션을 생각) 아래 예제와 같이 쓴다
참고로 <? extends Class1는> Class1이나 Class1의 자식을 모두 쓸 수 있게 한다는 뜻

Class1.java
@ToString
public class Class1<T> {
	public T asd;

	public void zzz(T param) {

	}

	public T xxx() {
		return asd;
	}

}

Parent.java
public class Child {

}

Child.java
public class Child extends Parent {

}

Run.java
public class Run {
	public static void main(String[] args) {

		List<Child> list = new ArrayList<>();
		m1(list);

		Class1<Child> p2 = new Class1<>();
		m2(p2);

		System.out.println(m3());

		System.out.println(m4());

	}

	private static void m1(List<? extends Parent> p) { // List인데 Parent를 상속받는 자료형을 쓰겠다
		System.out.println(1111);
	}

	private static void m2(Class1<? extends Parent> p) {
		System.out.println(p.asd);
	}

	private static Class1<Integer> m3() {
		Class1<Integer> c1 = new Class1<>();
		return c1;
	}

	public static <T>Class1<T> m4(String s1) { // 뭔가 데이터를(s1) 받아서 of메소드로 Class1의 객체를 만들고 돌려줌(정적 팩토리 메소드 구조)
		Class1<T> c1 = of( s1);
		return c1;
	}
	public static <T> ApiResponse<T> of(ResponseCode responseCode, T data) {
		return new ApiResponse<>(responseCode.getCode(), responseCode.getMessage(), data);
	}
}

------------------------------

static 메소드에서는 타입 매개변수를 사용할 수 없고, 아래처럼 해야함

<? extends 타입> : 와일드카드의 상한 제한. 타입과 그 자손들만 가능
<? super 타입> : 와일드카드의 하한 제한. 타입과 그 조상들만 가능
<?> : 제한없음. 모든 타입이 가능. Object랑 동일


ex) Widget과 같거나 하위 타입만 받고, 해당 타입으로 리턴
public static <T extends Widget> T setCSSRt(T mw, String style){
	setCSS(mw, style);
	return mw;
}
장점은 T타입으로 들어온 mw를 Widget으로 형변환 하지않고 사용이 가능함
public static Widget T setCSSRt(Widget mw, String style){


ex) Widget과 같거나 하위 타입만 받고, Widget으로 리턴 (잘 안쓰고 위에걸 더 많이씀. [제네릭 타입매개변수 선언부] [리턴타입] 위치는 리턴타입 앞에옴)
public static <T extends Widget> Widget setCSSRt(T mw, String style){


ex) 이러면 아무런 의미도 없음
public static <T extends Widget> T setCSSRt(Widget mw, String style){
	setCSS(mw, style);
	return (T) mw;
}


참고로 지네릭 클래스와 달리 와일드 카드에는 &를 사용할 수 없다. 즉, <? extends T & E>와 같이 할 수 없다

----------------------------------------------------------------------------------------------------

gof 디자인패턴

------------------------------

생성

팩토리 메소드 패턴(Factory method pattern) : 필드가 적은 클래스에 주로 씀
빌더 패턴(Builder Pattern) : 필드가 많은 클래스에 씀
싱글톤 패턴(Singleton Pattern) : 클래스의 인스턴스를 하나만 쓸 경우 씀. 메모리가 절약됨

사용하는곳에서 생성자(new연산자)를 쓰지 않고, 메소드로 객체를 만들 수 있음

-----

생성자 이용

@ToString
@AllArgsConstructor
public class Obj {
	private int age;
	private String gender;
}

public static void main(String[] args) {
	System.out.println(new Obj(4,"남자"));
}

-----

팩토리 메소드 패턴

@Setter
@Getter
@ToString
public class Obj {
	private int age;
	private String gender;

	public static Obj of(int age, String gender) {
		Obj o = new Obj();
			o.setAge(age);
			o.setGender(gender);
		return o;
	}
}

이런식으로 스태틱 메소드로 객체를 만들어서 돌려줌

public static void main(String[] args) {
	System.out.println(Obj.of(3, "중성"));
}

-----

빌더 패턴으로 하면 (@Build 애노테이션 이용)

@Builder
@AllArgsConstructor
@ToString
public class Obj {
	private int age;
	private String gender;
}

public static void main(String[] args) {
	System.out.println(Obj.builder()
		.age(1)
		.gender("남자")
		.build());
}

이때 마지막에 build()메소를 쓰기 전에 아래처럼도 받을 수 있음
클래스명.클래스명Builder 
ex) Bicycle.BicycleBuilder bicycleBuilder = Bicycle.builder().wheel(2).company("메리다").price(10000)

그렇게 Builder객체로 받은걸 수정도 가능함
bicycleBuilder.price(20000)

-----

싱글톤 패턴

전역 변수를 사용하지 않고 객체를 하나만 생성 하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴
문제점 : 다중 스레드에서 Printer 클래스를 이용할 때 인스턴스가 1개 이상 생성되는 경우가 발생할 수 있다.

public class Car {
	private static final Car car = new Car(); // static 메소드or필드 클래스의 뭔가가 호출될때 (=클래스 로딩시점에) 객체가 생성됨

	private Car(){} // 외부에서 객체를 new 연산자로 생성할 수 없게 하기

	public static Car getInstance(){
		return car;
	}

	private boolean isUse = false;

	public void drive(){
		isUse = true;
		System.out.println("start driving");
	}

	public void parking(){
		isUse = false;
		System.out.println("parking");
	}

	public boolean isEnableUseCar(){
		return !isUse;
	}

}

public static void main(String[] args) {

	Car car = Car.getInstance();
	if (car.isEnableUseCar()){
		car.drive();
//			car.parking();
	}

	Car car2 = Car.getInstance();
	if (car.isEnableUseCar()){
		car.drive();
	}else{
		System.out.println("wait");
	}

}

------------------------------

구조 패턴

-----

파사드(facade) : 많은 서브시스템(내부구조)를 거대한 클래스(외벽)로 만들어서 감싸서 편리한 인터페이스를 제공해줌

------------------------------

행위 패턴

-----

옵저버(Observer) : 객체의 값 변화를 감지

Subject : 변화하는 녀석
Observer : 변화를 감시하는 녀석

인터페이스로 구현. notify 메소드는 자바의 Object에 이미 있기때문에 update 메소드로 쓰는것이 관습임
public interface Observer {
	void update(); // notify
}

----------------------------------------------------------------------------------------------------

에러, Error
- 오류(error) , 버그(Bug) , 예외(Exception) 등

1. 컴파일 오류(Compile Error) (=빨간 밑줄)
- 소스코드 → 기계어 , 이진코드
- 컴파일러가 번역을 할 때 문법이 올바른지 확인하는 과정에서 발견
- 컴파일 작업을 중단(번역 중지)
- 난이도 가장 낮음 → 발견 쉬움 → 고치기 쉬움
- 컴파일러가 어떤 오류가 발생했는지를 알려준다.

2. 런타임 오류(Runtime Error) : 예외(Exception) - 실행중 오류 , 사용자가 입력했을때 발생한 오류 ex)게임에서는 '오픈 베타'를 통해 테스트함
- 컴파일 작업때는 발생이 안됐는데 실행중에 발견되는 오류
- 발견 난이도 중급. 복불복
  java.lang.ArithmeticException: / by zero
  산술연산시 발생된 오류 : / 0으로 나눔
- 모든 경우의 수를 미리 예측해서 테스트를 해야 한다. → 어떻게든 미리 발견!!
※ 발생하지 않게 하기위해서는↓↓
- 1. 사람을 동원
- 2. 프로그램(테스트용 프로그램)

3. 논리 오류(Logical Error)
- 문법도 틀린곳이 없고, 실행도 잘되는데 결과가 이상할때..
- 발견 힘듬. 수정 난이도 높음
System.out.println(10 - 20); +를 입력해야하는데 -를 잘못 입력한 경우
결과값이 30이 나와야 한다고 생각하는데 -10이 나옴
- 논리 오류는 자기 눈에는 안보임 → 남의 눈에는 보임
- 피말리는에러 , 사람잡는에러
- 자신만의 기준을 잡고(30분) 못찾겠으면 다른 사람에게 도움을 부탁해야함

4. 시스템 오류(System Error)
- 프로그램 동작 중에 운영체제 또는 하드웨어에 문제가 발생해 프로그램이 정상적으로 동작하지 않는 경우에 발생
- 메모리 부족(OutofMemoryError)이나 스택오버플로우(StackOverflowError)
이러한 에러는 개발자가 예측하기도 쉽지 않고 처리할 수 있는 방법도 없습니다.

★에러 메세지를 모두 정리해놓을것 = 에러메세지를 안보고 에러를 고치는것 : 바보
★중요도 : 암기 < 이해 < 체화(습득)

------------------------------

★예외처리

예외 처리 종류

Exception / RuntimeException

Exception(Checked Exception) : 예외처리 필요, 외부 영향으로 발생할 수 있는 것들(사용자 동작, 운영체제 등), 컴파일 중 확인, 트랜잭션 롤백안됨
	예외 발생 이후 로직이 그냥 수행됨
RuntimeException(UncheckedException) : 예외처리 안해도 됨, 프로그래머의 실수에 의해서 발생, 런타임 중 확인, 트랜잭션 롤백진행

Object
	Throwable
		Error
			LinkageError
			ThreadDeath
			VirtualMachineError
		Exception
			RuntimeException (=언체크예외 Unckecked Exception)
				ClassCastException : 적절치 못하게 클래스를 형변환하는경우
				ArithmeticException : 정수를 0으로 나눈 경우
				NullPointerException : 널(null) 객체를 참조했을 경우
				IllegalArgumentException : 메소드에 유형이 일치하지않는 파라미터를 전달하는 경우
				IndexOutOfBoundsException : 객체의 범위를 벗어난 인덱스를 사용하는 경우
				ArrayIndexOutOfBoundsException : 배열을 참조하려는 인덱스가 잘못된 경우
				ArrayStoreException : 배열 유형이 허락하지 않는 객체를 배열에 저장하려는 경우
				NegativeArraySizeException : 배열의 크기가 음수인 경우
			ClassNotFoundException (=체크예외 Ckecked Exception)
			CloneNotSupportedException (=체크예외 Ckecked Exception)
			InstantiationException (=체크예외 Ckecked Exception)
			IOException (=체크예외 Ckecked Exception)
				EOFException
				FileNotFoundException
				UnterruptedIOException

체크예외(CheckedException) : Exception클래스의 서브(자식)클래스이면서 RuntimeException클래스를 상속하지 않은것들. try/catch등이 사용되었는지 확인 필요
	ex) 존재하지 않은 파일의 이름으르 입력,실수로 클래스의 이름을 잘못적음 등이 해당
언체크예외(UnCheckedException) : RuntimeException을 상속한 클래스. try/catch등이 사용되었는지 확인 필요하지 않음
	ex) ArithmeticException(0으로 나누기), IndexOutOfBoundsException(배열범위) 등이 해당

throws : 예외 미루기
throw : 예외 고의로 발생시키기

-----

사전 대비 방식

↓↓↓↓↓

int num = 10;

가독성 좋은코드
if (num!=0) {
	//비즈니스 코드(업무 코드)
	System.out.printf("100/%d = %d\n",num,100/num);
}else {
	//예외 처리 코드
	System.out.println("0입니다");
}
int num = 10;

가독성 나쁜코드 (보편적으로 true절에 맞는결과를 넣는다고 생각하기때문이라고함)
if (num==0) {
	//예외 처리 코드
	System.out.println("0입니다");
}else {
	//비즈니스 코드(업무 코드)
	System.out.printf("100/%d = %d\n",num,100/num);
}

-----

오류가 나면 대응하는 방식(조직적인 방식이라 권장 , 오류가 나도 프로그램이 뻑 나지 않는 안정적인 방식임)
try/catch문을 이용

↓↓↓↓↓

try {
	System.out.println("하나"); → 실행
	System.out.printf("100/%d = %d\n",num,100/num);  → 오류가 나는 시점부터 실행X
	System.out.println("둘");  → 실행X
} catch (Exception e) {
	System.out.println("0을입력하면안됩니다");
}

-----

try/catch 동작 순서

1. try블록 안의 코드가 실행됨. 
2. 오류가 없다면 try안의 마지막 줄까지 실행되고, catch 블록은 건너뜀
3. 오류가 있다면 try안 코드의 실행이 중단되고, catch(e) 블록으로 제어 흐름이 넘어감.
이때 e는 예외 객체로, 예외와 관련된 정보를 제공 (error의 약자. 아무 이름이나 쓸수있음)

이렇게 try 블록 안에서 예외가 발생해도 catch에서 오류를 처리하기때문에 프로그램은 중단되지않음

-----

★다중 try catch 방식

try {
	int[] nums = {10,20,30};
	nums[0] = 100; //ArrayIndexOutOfBoundsException
	//ClassCastException e = new ClassCastException(); //야구공
	//throw e;
		
	Random rnd = null;//new Random();
	System.out.println(rnd.nextInt()); //NullPointerException
	
	Object o1 = "문자열";
	System.out.println((int)o1); //ClassCastException
}catch(ArrayIndexOutOfBoundsException e){	
	System.out.println("방번호 오류");
}catch(NullPointerException e) {
	System.out.println("널참조");
}catch(ClassCastException e) {
	System.out.println("형변환 오류");
}catch(Exception e) {
	System.out.println("예외 발생");
}

------------------------------

throw(강졔 예외 발생시키기)

상속받고있는데 return을 써서 부모에서 처리하기가 애매한 상황일경우 쓰면 아주 좋음

@Override
public void save() {
	if (!(rdSetWT.getValue() || rdSetP.getValue())){
		MaterialToast.fireToast("노출 시간/기간을 선택하세요");
		try {
			throw new Exception("강제예외발생시킴");
		} catch (Exception e) {
			throw new RuntimeException(e);
		}
	}
}

------------------------------

ex1) 커스텀예외를 던진후, 예외메시지 출력

<CustomException.java>
public class CustomException extends Exception{

	CustomException(String message){
		super(message);
	}

}

<Run.java>
public class Run {
	public static void main(String[] args) {

		try {
			test();
		} catch (CustomException e) {
			System.out.println("커스텀 예외 테스트");
			System.out.println(e.getMessage());
			e.printStackTrace();
		}
	}

	public static void test() throws CustomException{
		throw new CustomException("예외 테스트 입니다.");
	}

}

-----

ex2) 특정 상황에서의 커스텀 예외 메시지

<MyBusinessException.java>
class BadBankingException extends Exception{

	public BadBankingException(String s) {
		super(s);
	}

}

<Account.java>
public class Account {

	String name;
	int current;

	public Account(String name, int current) {
		super();
		this.name = name;
		this.current = current;
	}

	void withdraw(int money) throws BadBankingException{
		if (money > current) {
			throw new BadBankingException("잔액이 부족합니다");
		} else {
			current = current - money;
		}
	}

}

<Run.java>
public class Run {
	public static void main(String[] args) {

		Account kimAccount = new Account("김미진", 200);
		try {
			kimAccount.withdraw(150);
		} catch (Exception e) {
			System.out.println(e.getMessage());
		}

		System.out.println(kimAccount.current);

	}
}

------------------------------

assert 로도 예외를 발생시킬 수 있음

assert 키워드 뒤에 boolean값을 넣을 수 있는데
그 boolean값이 false이면 오류를 발생시킴.

String[] names = {"John", "Mary", "David"};
assert names.length == 2; // java.lang.AssertionError 발생
System.out.println("There are "+names.length + "  names in an array");


실행할때는 -ea 또는 -enableassertions 옵션을 넣어야함
방법은 2가지가 있음

<실행 명령어를 직접 입력>
java -ea 파일명.java
이렇게 터미널로 경로찾아가서 직접 실행시켜도 되고

or

<IDE 환경설정에서 옵션 추가>
인텔리제이 실행 버튼 옆에 셀렉트박스 클릭하면 나오는 "Edit Configurations...(구성편집...)" 에서
Modify options(옵션 수정) → Add VM options 눌러서 추가해도됨

------------------------------

예외 미루기 throws

메소드 선언부 끝에 작성.
메소드에서 처리하지 않은 예외를, 메소드를 호출한 곳으로 떠넘기는 역할

ex)
리턴타입 메소드명(매개변수선언1, ...) throws 예외클래스1, 예외클래스2, ... {
    ...
}

ex) 상위 예외클래스로 한번에 처리
리턴타입 메소드명(매개변수선언1, ...) throws Exception {
    ...
}

try-catch문의 catch절에서 떠넘겨받은 예외를 처리해야하며
예외를 처리하지 않고 throws 키워드로 다시 떠넘길 수 있다

끝까지(main메소드까지) 예외를 미뤘을 경우 (main() 메소드에서 throws를 선언할 경우),
main() 메소드는 JVM에서 호출하는 것이므로 예외 처리를 하지 않은 것과 마찬가지가 됨

------------------------------

사용자 예외 만들기

public class BadBankingException extends Exception{
	public BadBankingException(String message){
		super(message);
	}
}

쓸때는 조건문으로 다음과 같이 발생시키고,
try-catch문으로 오류났다는메시지나 e.printStackTrace(); 오류메시지를 띄우거나
이나 throws로 미룰 수 있음.

void withdraw(int money) throws BadBankingException{
	if (money > current) {
		throw new BadBankingException("잔액이 부족합니다");
	} else {
		current = current - money;
	}
}

------------------------------

예외처리를 try/catch로 처리했을경우 프로그램 실행이 중지되지 않고 계속 실행됨.

catch절에서
} catch (IOException e) {
	throw new RuntimeException(e);
}
이렇게 예외를 발생시키면 예외가 try문 밖으로 다시 빠져나감
그럼 밖으로 나간 예외를 또다시 처리해야함 (처리를 안하면 프로그램 중지됨)

------------------------------

예외로 인해 프로그램이 중지되는것을 방지하면서, 오류 메시지만 확인하는법

-----

방법1. System.out.println 으로 예외메시지 제목만 확인

catch문 안에서 무언가를 System.out.println() 으로 출력한경우
출력한 내용은 원래 순서에 맞게 그대로 출력됨
System.out.println(e) 이렇게 출력하는것도 가능함

-----

방법2. .printStackTrace() 메소드 사용

예외객체.printStackTrace() 메소드를 쓰면 오류메시지제목+상세내용이 출력되는데,
만약 .printStackTrace() 메소드를 System.out.println() 메소드와 함께 쓸경우,

} catch (IOException e) {
	System.out.println("Run.m1()");
	e.printStackTrace();
}
이때 .printStackTrace()로 찍은 오류메시지는 순서 상관없이 프로그램의 모든 출력이 끝나고 맨마지막에 찍힘

-----

만약 catch문안에 아무것도 넣지 않을 거라면

} catch (Exception ignored) {
}
위처럼 ignored라는 변수명으로 매개변수를 받는게 관습임

----------------------------------------------------------------------------------------------------

컬렉션 프레임워크(collection)
- 자료를 다룰 수 있는 '자료구조(자료를 저장할수 있는 구조) 클래스'
- 다양한 자료들을 다양한 방식으로 관리하기 위한 방법을 제공
- 배열을 감싼 클래스(물리적 구조 상)
- 배열의 길이가 가변(실행 중 늘리거나 줄이는게 가능)

1. Collection 인터페이스
	- List와 Set의 부모
	- 중복도 허용하고 자료가 저장되는 순서는 기억하지 못하는게 특징
	- 저장된 자료를 하나씩 꺼낼수있는 Iterator인터페이스를 반환
	- Iterator에 의존
	- [boolean] add(Object)
	- [iterator] iterator()
	- [int] size()
	
2. List 인터페이스
	- ArratList☆☆☆, Stack☆☆☆, LinkedList☆☆☆, Vector, Queue
	- 순서가 있는 집합★★★
	- 방번호가 있다(첨자(index) 사용) → 요소 접근
	- 때문에 데이터 중복을 허용합니다 → 방번호가 유일하기 떄문에 같은 데이터도 방번호를 통해서 구분할 수 있습니다
	
3. Set 인터페이스
	- HashSet☆☆☆, TreeSet
	- 순서가 없는 집합★★
	- 방번호가 없다(첨자 없음)
	- 데이터 중복을 허용 안한다★★★
	- [boolean] add(Object) : 같은자료가 있으면 false, 없으면 true 반환
	
4. Map 인터페이스
	- HashMap☆☆☆, TreeMap, HashTable, Properties
	- 순서가 없는 집합. 그러나 LinkedHashMap 은 순서가 보장됨
	- 키와 값을 사용하는 배열입니다 → 연관배열,딕셔너리
	- 키(key) : 식별자 역할 (방을 구분하는 방번호) → 유일해야 한다. → 중복 허용안함 → Set
	- 값(value) : 데이터 역할 → 중복 허용함 → List
	- keySet 메소드로 Set객체로 만든 후 iterator로 탐색(출력)가능
		ex) Iterator<E> i1 = map객체.ketSet().iterator(); //이터레이터메소드로 이터레이터객체를 만든후
		while(i1.hasNext()){
			String key = i1.next();
			String value = map객체.get(key); //map객체에서 get메소드로 value를 꺼내기
			System.out.println(key + ":" + value);
		}

vactor,HashTable,Properties : 사용 안함 Legacy Class - 예전 시스템의 호환성을 위해서 남겨놓은 문법 →
언젠가 버전업이 되면서 사라질 수도 있는 문법(사용지양)
Vactor(동기화 지원) → ArrayList(동기화 미지원)
HashTable → HashMap
Properties → 폐기 → XML, JSON 기술로 대체


★ArrayList 메소드 사용법 (get과 set은 반환값을 받을 수 있음)
- 마음대로 추가할수 있다
- 향상된 for문 사용가능

참고: 제네릭에서 컬렉션 내 요소들은 E(Element), 그 외는 T(Type)라고 쓰는 관습이 있음

(boolean) .add(값) → 값 맨 뒤에 추가
(void) .add(int index, T element) → 값 원하는 위치에 넣기 ☆방이 늘어나므로 Right쉬프트 발생!(해당방 다음(오른쪽) 방들은 한칸씩 오른쪽으로 이동됨)
(E) .get(인덱스) → 값 불러오기
(E) .set(인덱스, 값) → 값 수정. 수정하기 전 값 저장
(E) .remove(인덱스) → 방 삭제. 방이 줄어듬으로 Left쉬프트 발생(해당방 다음(오른쪽) 방들이 한칸씩 왼쪽으로 이동됨) (해당방이없으면 에러). 삭제하기 전 값 반환
	Integer List에서 특정값을 제거하고싶으면 .remove(indexOf(값)) 이렇게 하기
(boolean) .remove(값); → 번호말고 요소를 검색가능 (첫번째 검색되는 값만 지워짐) (해당값이없으면 아무 반응 안일어남) 삭제되면 true, 없으면 false 반환
(boolean) .contains(값) → 값이 있으면 true , 없으면 false 반환
(int) .indexOf(T values) → 인덱스 반환 , 값이 없으면 -1 반환
(int) .lastIndexOf(T values) → 거꾸로 인덱스 반환, 값이 없으면 -1 반환
(void) .clear(); → 전부 삭제(초기화) (같은 변수로 다시 대입하는 방법도 있음) list = new ArrayList<T>();
(boolean) .isEmpty(); → 리스트가 비어있으면 true, 있으면 false 반환
(void) Collections.reverse(list); → 뒤집기 ex) [1,2,3] → [3,2,1]
(void) Collections.sort(list); → 오름차순 정렬 (숫자와 문자 대상으로 정렬가능,  import 필요)
(void) list.sort(Integer::compareTo) → 이렇게도 오름차순 정렬가능
(void) Collections.sort(list) & Collections.reverse(list); → 내림차순 정렬은 먼저 오름차순 정렬을 한 후에 reverse로 뒤집는방법이 있고
(void) list.sort(Comparator.reverseOrder()); → 이렇게도 내림차순 정렬가능
(List<E>) list.subList(인덱스1(inclusive), 인덱스2(exclusive)); → 원하는 구간 빼서 복사

(boolean) .addAll : 리스트에 다른 컬렉션(List, Set) 붙이기
스트림의 flatMap() 으로도 가능 (flatMap의 장점은 원본 List를 유지시킬 수 있음)

(Onject[]) .toArray() → List를 기본배열로 반환 (primivice자료형은 쓸 수 없음. .stream().mapToInt(Integer::intValue).toArray() 쓰기)

(T) Collections.max(list); → 최대값
(T) Collections.min(list); → 최솟값

(void) Collections.swap(list, idx1, idx2); → List의 요소를 서로 바꾸기

(int) Collections.frequency(list, 값) → 리스트내 값의 개수를 반환. 스트림의 map이나 filter와 응용 가능

(String) String.join("", list) → String리스트를 하나의 문자열로 합쳐서 반환 (""를 꼭 써야함, 안쓰면 List가 아닌 "a","b","c" 이렇게 쉼표로구분한 것만 합칠 수 있음)

-----

(List<T>) Arrays.asList("가","나","다"); → 리터럴들을 리스트로 변환
(List<E>) List.of("가","나","다"); → 리터럴들을 리스트로 변환. null값을 가질 수 없음. Thread-Safe함 (jdk9)

Integer arr = {1,2,3};
List<Integer> list = Arrays.asList(arr); → 일반 배열을 리스트로 변환(int[]는 스트림으로 해야함)
(원본 배열의 주소를 참조하기때문에 컬렉션이나 배열 둘중 하나를 바꾸면 같이 바뀜)

리스트를 생성할때 Arrays.asList만 쓰면 원소가 고정되어 추가나 삭제가 안됨
원소를 고정시키지 않고싶으면 만들때 new 연산자를 사용해야함
ex)
List<Integer> list = Arrays.asList(1,2,3);
list.add(1); // UnsupportedOperationException
↓↓↓
List<Integer> list = new ArrayList<>(Arrays.asList(1,2,3));

-----

l1.addAll(컬렉션) → 컬렉션을 리스트에 연결해서 붙임

또는 배열을 리스트로 만든 후 리스트에 연결해서 붙임
Integer arr = {1,2,3};
l1.addAll(Arrays.asList(arr));

-----

① Object 버전으로 할때 (구형)
- object라서 아무 자료형이나 넣기 가능하지만 처음넣은 한가지 자료형만 넣기!

ArrayList list = new ArrayList();
list.add(100); //마지막에 추가(append)
list.add(200); //마지막에 추가(append)
for (int i = 0; i < nums2.size(); i++) {
	System.out.println(nums2.get(i));
}

(int)nums2.get(0)*100
Object값이기때문에 연산시 형변환(int) 해야함

② Generic 버전으로 할때 (신형)
- 처음 자료형을 세팅 → 마치 int 배열처럼 사용 가능
ArrayList<Integer> list2 = new ArrayList<Integer>();
list2.add(100);
System.out.println(list2.get(0)*2);

nums2.get(0)*100
형변환이 필요가 없음

------------------------------

List 수정 막기

(List<T>) Collections.unmodifiableList(리스트)

반환값을 리스트에 대입해야함. 반환값이 void가 아님

List<Character> list = new ArrayList<>();
list.add('a');
list.add('b');
list.add('c');
list.add('d');

try {
	list.forEach(System.out::println);
	list = Collections.unmodifiableList(list);  // 추가, 삭제행위를 금지시킴
	list.remove(1);  // 오류발생
	list.add('e');   // 오류발생
} catch (Exception e) {
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

★사전 구조(Dictionary). 맵(Map). 연관 배열
  - 방번호 없음
  - 요소들의 순서가 없음
  - 키(key)와 값(value)으로 데이터를 관리
  - 일괄 접근 불가능(for) → 일괄 접근 안함
  - 요소의 의미를 알기 쉽다☆☆
  - 키는 유일해야 한다☆☆

------------------------------

선언과 동시에 초기화 하는 법

List<Integer> list = new ArrayList<>(){
	{
		add(1);
		add(2);
		add(3);
	}
};

Map<String,String> map = new HashMap<String,String>(){
	{
		put(".-","a");
		put("-...","b");
		put("-.-.","c");
	}
};

List와 Set은 Arrays 클래스도 이용가능
List<Integer> list = Arrays.asList(1,2);
Set<Integer> set = new HashSet<>(Arrays.asList(1,2));

-----

Java9 이상의 버전을 사용한다면 Map.of()를 이용하는 방법이 있습니다. (★10개까지로 개수 제한이 있음)
Map<String, Object> map = Map.of(
    "name", "junho85",
    "nickname", "June Kim"
);

------------------------------

메소드
map.put("키이름",값); → 요소 추가 / 요소 수정 (같은 이름으로 저장시 덮어씀) (중복키없는 유일키)
Object xxx = map.put("키","값"); → 요소 수정하기 전의 값 반환
map.size(); → 키 개수
map.containsKey("키"); → 키 존재여부
map.containsValue(값); → 값 존재여부
map.get("키"); → 키에 해당하는 값
map.getOrDefault("키",-1); → 키에 해당하는 값 반환. 키가 없을경우 2번째인수 반환
map.remove("키"); → 키/값 삭제
map.clear(); → 초기화
map.keySet() → 모든 키를 Set으로 반환
map.values() → 모든 값을 Set으로 반환
map.entrySet() → 모든키/값을 Set<Map.Entry<String, Object>>으로 반환

ex)
HashMap<String,Integer>score2 = new HashMap<String,Integer>();
score2.put("kor", 100);
System.out.println(score2.get("eng"));

------------------------------

활용
Scanner scan = new Scanner(System.in);

System.out.print("응시자명:");
String name = scan.nextLine();
if (result.get(name) != null) {
	if (result.get(name)) {
		System.out.println(name + ": 합격");
	}else {
		System.out.println(name + ": 불합격");
	}
}else {
	System.out.println("명단에 없는 이름");
}

활용2
for (String item:participant) {
	hm.put(item,hm.getOrDefault(item, 0) + 1) → 해당 키가 있으면 키값을 반환, 없으면 0을반환 후 +1
}

----------------------------------------------------------------------------------------------------

★Iterator - 순차 탐색 방법
- 컬렉션 프레임워크에서 저장된 요소를 읽어오는 방법을 표준화하기 위한 역할
- List Set 계열 지원
- 읽기 전용
- 향상된 for문과 유사
- iterator를 지원하는 컬렉션은 iterator() 라는 메소드가 인식됨

[boolean] hasNext() : 다음 방에 값이 있으면 True / 없으면 false 반환
[Object] next() : 다음 방의 값을 반환

<사용법>
ArrayList<String> list = new ArrayList<String>();
list.add("사과");
list.add("포도");
list.add("바나나");

Iterator<String> iter = list.iterator();
while(iter.hasNext()){
	System.out.println(iter.next());
}

Cursor	BOF(Begin of File)
         →사과
	포도
	바나나
	EOF(End of File)

전진 커서 : 일방(후진불가)
커서가 EOF까지 가서 데이터를 모두 소진했을시 다시읽는 방법
커서를 BOF로 옮긴다 → iterator를 새로 생성해야 커서를 다시 생성해야 한다 (or 복사해놓고 쓰거나)

iter = list.iterator();
while(iter.hasNext()){
	System.out.println(iter.next());
}

<HashMap에서 사용시>
HashMap<String,String> map = new HashMap<String,String>();	
map.put("과장","한가인");
map.put("부장","박수진");
map.put("대리","이열음");

Set<String> keys = map.keySet(); //키들만 모아놓은 배열
Collection<String> values = map.values(); //값들만 모아놓은 배열

Iterator<String> iter = keys.iterator();
while(iter.hasNext()){
	String key = iter.next();
	System.out.print(key + "-");
	System.out.println(map.get(key));
}


ListIterator
- Iterator : 단방향 > 전진 커서
- ListIterator : 양방향 > 전진 + 후진 커서

ListIterator 보다 Iterator 선호하는 이유
1. 속도 차이
2. ListIterator는 List전용(Set은 지원안함)

ArrayList<String> list = new ArrayList<String>();
list.add("사과");
list.add("포도");
list.add("바나나");
list.add("딸기");
list.add("복숭아");

ListIterator<String> iter = list.listIterator();

while(iter.hasNext()) {
	System.out.println(iter.next());
}

System.out.println();

//System.out.println(iter.hasPrevious()); hasNext()반대
//System.out.println(iter.previous()); hasNext()반대

while(iter.hasPrevious()) {
	System.out.println(iter.previous());
}

----------------------------------------------------------------------------------------------------

★HashSet
- 순서가 없는 배열
- 방번호(index)가 없음 = 개별요소탐색 불가능
- 중복값을 가질 수 없음★(ArrayList는 허용)
- HashSet, TreeSet
- iterator를 통한 탐색만 가능

System.out.println(set.contains(7));

System.out.println(set.add("사과")); → true
System.out.println(set.add("딸기")); → true
System.out.println(set.add("바나나")); → true
System.out.println(set.add("사과")); → false(값이 버려짐)
System.out.println(set.add("바나나")); → false(값이 버려짐)

System.out.println(set.size()); → 5가 아닌 3이 반환


TreeSet - Tree구조를 가지는 Set
- 중복값X, 순서X
- 이진 트리 구조를 기반으로 자동 정렬이 되는 set
1. 중복값 없는 정렬
2. 부분 검색 능함 (

TreeSet<Integer> set = new TreeSet<Integer>();

set.add(5);
set.add(3);
set.add(1);
set.add(2);
set.add(7);
set.add(9);
set.add(3);
set.add(5);
set.add(8);

System.out.println(set.size());
System.out.println(set);


배열을 Set으로 (기본형(primitive)은 Arrays.AsList를 사용할 수 없음)
Set<Integer> integerHashSet = new HashSet<>(Arrays.asList(ints));
↓↓↓
stream이나 for문으로 해야함
Set<Integer> set = Arrays.stream(nums).boxed().collect(Collectors.toSet());

----------------------------------------------------------------------------------------------------

스택(stack) - 후입선출, LIFO(Last Input First Output

Stack<String> stack = new Stack<String>();
stack.push(값) → 추가
(int) stack.size() → 길이
(Boolean) stack.empty() → 스택 비어있는지 유무
(Object) stack.pop() → 조회 및 삭제됨(꺼내기) (스택은 꺼낼값이 없으면 오류발생하니 예외처리 하기) → if(stack.size()>0{} or if(!stack.isEmpty()){}
(Object) stack.peek() → 조회만 되고 삭제되지않음
(int) stack.search(값) → 값이있는 주소 반환. 못찾으면-1반환 (1-Based Numbering)
(void) stack.clear() → 초기화

-----

큐(Queue) - 선입선출, FIFO First Input First Output

Queue<String> queue = new LinkedList<String>()
(boolean) queue.add(값) → 추가(저장공간이 부족하면 예외발생)
(boolean) queue.offer(값) → 추가(실패시 false반환)
(int) queue.size() → 길이
(Object) queue.poll() → 조회 및 삭제됨(꺼내기). 비어있으면 null반환
(Object) queue.peek() → 조회만 되고 삭제되지않음
(void) queue.clear() → 초기화

while(queue.size()>0) {
	System.out.println(queue.poll());
}

-----

LinkedList - List계열(ArrayList와 사용법은 비슷 + 구현 내부가 서로 다르다)

LinkedList 종류
1. 단일 연결 리스트(Singly Linked List)
2. 이중 연결 리스트(Doubly Linked List)
3. 원형(환형) 연결 리스트(Circular Linked List)
4. 이중 원형(환형) 연결 리스트(Doubly Circular Linked List)

----------------------------------------------------------------------------------------------------

리스트
- Array : 배열 구조
- Linked : 링크 구조

세트 / 맵
- Hash : Hash 알고리즘 사용
- Tree : 이진 트리 사용
	자동 정렬, 범위 검색 용이
	키만 이진 트리로 관리
	값은 리스트로 관리

----------------------------------------------------------------------------------------------------

중복값 없는 집합
1. 자동정렬/범위 검색 필요 → TreeSet
2. 넣은 순서대로 → LinkedHashSet
3. 그외 나머지 → HashSet

중복값 있는 집합 → List vs Map ?
1. 뭐가 뭔지 잘 모름 → ArrayList
2. 첨자(index), 방번호 존재 → List
	조작이 심하다 → LinkedList
	조작이 덜하다 → ArrayList
	선입선출 → Queue(LinkedList)
	후입선출 → Stack
3. 키를 사용 → Map
	정렬/범위 검색 → TreeMap
	나머지 → HashMap


List계열에서 잘 모르겠으면 ★ArrayList
Map계열에서 잘 모르겠으면 ★HashMap
Set계열에서 잘 모르겠으면 ★HashSet

1순위
- ArrayList, HashMap, HashSet
2순위
- LinkedList, Queue,Stack, TreeSet
3순위
- TreeMap, Properties, (Vector), (HashTable)

----------------------------------------------------------------------------------------------------

★파일
1. 파일 접근(참조)하기 → 파일 참조 객체 만들기
2. 파일 정보(속성) 보기

경로
final String PATH = "C:\\class\\java\\file\\test.txt";

파일 참조 객체 생성하기 (파일 불러오기)
File file = new File(PATH);
System.out.println(file.exists());
System.out.println(file.getAbsolutePath()); //exists에서 false가 나올시 파일 경로 확인용, 잘 안된다면 복붙 말고 손으로 경로입력

if(file.exists()) { ★(파일or폴더)가 존재하는지 boolean값 반환(항상 체크하기)
	System.out.println(file.getName()); → test.txt (파일명)
	System.out.println(file.isFile()); → true (파일인지?)
	System.out.println(file.isDirectory()); → false (폴더인지?)
	System.out.println(file.length()); → 16 (파일크기 단위:byte)
	System.out.println(file.getPath()); → C:\class\java\file\test.txt (참조 당시 경로)
	System.out.println(file.getParent() → C:\class\java\file (부모 경로)
	System.out.println(file.getAbsolutePath()); → C:\class\java\file\test.txt (절대 경로)
	↑자주 사용↑ ↓잘 안사용↓
	System.out.println(file.lastModified()); → 1605053974995 (마지막 수정일자 단위:틱) , 캘린더 이용해서 날짜/시간 변환 가능
	System.out.println(file.canRead()); → true (읽기 가능한지)
	System.out.println(file.canWrite()); → true (쓰기 가능한지)
	System.out.println(file.isHidden()); → false (숨김 파일인지)
}else {
	System.out.println("파일이 존재하지 않습니다.");
}

★폴더(파일이랑 동일하고 경로만 다름)
String path = "D:\\class\\java\\file";
File dir = new File(path);
if(dir.exists()) {
	System.out.println(dir.getName()); → file (이름)
	System.out.println(dir.isFile()); → false (파일인지?)
	System.out.println(dir.isDirectory()); → true (폴더인지?)
	System.out.println(dir.length()); → 0 (크기 ★폴더는 크기가 없다 → 내부 파일들크기의 합을 구해야함)
	System.out.println(dir.getPath()); → C:\class\java\file (경로)
	System.out.println(dir.getAbsolutePath()); → C:\class\java\file (경로)
	System.out.println(dir.listFiles()); → ★폴더내 모든 파일/폴더 File[]로 반환
}else {
	System.out.println("파일이 없습니다");
}

★renameTo(File개체→File개체) - 파일/폴더 이름 바꾸기
final String PATH = "C:\\class\\java\\file\\test.txt";
File file = new File(PATH);

final String PATH2 = "C:\\class\\java\\file\\aaa.txt";
File file2 = new File(PATH2);

이름만 바꿀 뿐이지만 위처럼 미리 두 객체를 만들어 놓아야함

if (file.exists()) {
	boolean result = file.renameTo(file2); //result는 성공적으로 바뀌었으면 true를 반환
	System.out.println(result);
}else {
	System.out.println("파일없슴");
}

★파일/폴더 이동시키기
이름 바꾸기랑 똑같이 resameTo메소드쓰면되고 객체 경로만 바꾸면 됨 , 이동과 이름변경을 동시에도 가능(move같은메소드 없음!)

★delete - 파일/폴더 삭제 (휴지통으로 '이동'안되고 '삭제'됨)
★폴더는 빈폴더만삭제가능 → 파일이 들어있는 폴더를 지울때는 내부의 파일을 먼저 지워지게 한다음 폴더를 지워야 함

final String PATH = "C:\\class\\java\\file\\aaa.txt";
File file = new File(PATH);
if (file.exists()) {
	boolean result = file.delete();
	System.out.println(result?"성공":"실패");
}

★mkdir - 폴더 만들기
final String PATH = "C:\\class\\java\\file\\ccc";
File dir = new File(PATH);

if (!dir.exists()) {
	System.out.println(dir.mkdir());
}else {
	System.out.println("같은이름의 폴더가 이미 있습니다");
}

폴더를 동시에 여러개 만들고싶을때는 mkdirs
String path = "C:\\class\\java\\file\\ddd\\eee";
dir = new File(path);

System.out.println(dir.mkdirs());

ex) 회원별 개인 폴더 만들기
String[] member = {"한가인","박수진","아이린","이다희"};

for (String name:member) {
	path = String.format("C:\\class\\java\\file\\member\\[개인폴더]%s님",name);
	dir = new File(path);
	dir.mkdirs();
	
	System.out.println(name + "님 개인폴더 생성 완료");
}

ex) 2020-01-01 ~ 2020-12-31 (366개) 만들기
Calendar c1 = Calendar.getInstance();
c1.set(2020,0,1);

for (int i = 0; i<366; i++) {
	System.out.printf("%tF\n",c1);
	c1.add(Calendar.DATE,1);
	
	path = String.format("C:\\class\\java\\file\\todo\\%tF",c1);
	dir = new File(path);
	dir.mkdirs();
}

★listFiles - 디렉토리(폴더)의 파일/폴더 모두 불러오기 (File[]로 반환) → 배열 요소도 String이 아닌 File개체임
String path = "C:\\eclipse";
File dir = new File(path);

if (dir.exists()) {
	File[] list = dir.listFiles();
	
	for (File file:list) {
		if (file.isDirectory()) {
			System.out.println("폴더:" + file.getName());
		}else {
			System.out.println("파일:" + file.getName());
		}
	}
}

★폴더내 파일+폴더 개수(따로는 for문 + isDirectory나 isFile메소드 사용)
String path = "~~~"
f1 = new File(path)
File[] dd = f1.listFiles();
System.out.println(dd.length);

★CSV(Comma Separated Values)
- 몇 가지 필드를 쉼표(,)로 구분한 텍스트 데이터 및 텍스트 파일 , 쉼표말고 다른걸로 구분해서 쓰기도 함
- 플레인 텍스트이기 때문에 보안이 강한 곳에서도 쓸 수 있음
ex)
1,아이린,20,서울시
2,박수진,22,부산시
2,아이유,22,인천시

----------------------------------------------------------------------------------------------------

★재귀 메소드
- 재귀 호출 구조를 가지는 메소드
- 메소드 구현부에서 자신을 호출하는 메소드

public static void main(String[] args) {
//	팩토리얼
//	4! = 4*3*2*!
	
	int n = 4;
	int result = factorial(n);
	System.out.printf("%d! = %d\n",n,result);
}

private static int factorial(int n) {
	if(n==1) {
		return 1;
	}else {
		return n * factorial(n-1);
	}
}

----------------------------------------------------------------------------------------------------

★인코딩/디코딩 규칙
1. ISO-8859-1
2. EUC-KR
3. ANSI
4. UTF-8
5. UTF-16
6. MS949

ANSI(ISO-8859-1,EUC-KR,MS949)
1. 영어 : 1byte
2. 한글 : 2byte

UTF-8
1. 영어 : 1byte
2. 한글 : 3byte

UTF16
1. 영어 : 2byte
2. 한글 : 2byte

----------------------------------------------------------------------------------------------------

★파일 읽기

- 바이트 단위 읽기 (1글자씩) 버전
- System.in.read()와 동일
try {
	FileReader reader = new FileReader("C:\\class\\java\\file\\test2.txt");
	
	int code = -1;
	while ((code = reader.read())!=-1) {
		System.out.print((char)code);
	}

	reader.close();
	
} catch (Exception e) {
	System.out.println("Ex75_File.m6()");
	e.printStackTrace();
}


BufferedReader 버전
final String PATH = "C:\\class\\java\\file\\파일_입출력_문제\\이름수정.dat";
try {
	BufferedReader reader = new BufferedReader(new FileReader(PATH));
	
	String line = null;
	while((line = reader.readLine()) != null){
		System.out.println(line);
	}
	
	reader.close();
} catch (Exception e) {
	e.printStackTrace();
}

ReadLine()은 적을때마다 계속 줄이 내려가기때문에
같은 줄을 계속 체크하고 싶을때는 변수를 사용해야함 → String line = ReadLine();

if (reader.readLine()==null) {
	loadSerial.add(rnd.nextInt(3)); //랜덤배열에 임의값추가
}else {
	loadSerial.add(Integer.parseInt(reader.readLine().split(",")[0]));
}

↓↓↓

String line = reader.readLine();
if (line==null) {
	loadSerial.add(rnd.nextInt(3)); //랜덤배열에 임의값추가
}else {
	loadSerial.add(Integer.parseInt(line.split(",")[0]));
}

----------------------------------------------------------------------------------------------------

★파일 쓰기
- 바이트 단위 쓰기
- 1바이트씩 저장

파일에 데이터 저장하기(쓰기)
1. 스트림 객체 생성하기(열기)
2. 스트림 객체 사용하기(쓰기)
3. 스트림 객체 닫기

- 스트림모드
1. 생성모드(Creat Mode)
  - 기본방식
  - 파일이 없으면 새로 만든다
  - 파일이 있으면 무조건 덮어쓰기를 한다★FileOutputStream stream = new FileOutputStream(file,false); 기본값.
2. 추가 모드(Append Mode)
  - 파일이 없으면 새로 만든다
  - 파일이 있으면 기존 내용을 이어쓰기를 한다★FileOutputStream stream = new FileOutputStream(file,true);

try {
	FileWriter writer = new FileWriter("C:\\class\\java\\file\\test.txt");
	Scanner scan = new Scanner(System.in);
	
	while(true) {
		System.out.print("입력 : ");
		String data = scan.nextLine();
		
		writer.write(data);
		
		if (data.equals("exit")) {
			break;
		}
	}
	writer.close();

	System.out.println("저장완료");
	
} catch (Exception e) {
	System.out.println("Ex75_File.m5()");
	e.printStackTrace();
}


BufferedWriter 버전
try {
	BufferedWriter writer = new BufferedWriter(new FileWriter(PATH));

	for (int i = 0; i < list.size(); i++) {
		writer.write(String.format("%s\r\n",(String)list.get(i))); ★\n만 해서는 줄바꿈이 제대로 되지않으니 \r\n으로 하기
	}
	
	writer.close();
	
} catch (Exception e) {
	System.out.println("Ex75_File.m8()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

데이터를 안버려도 되는건 버릴 필요가 없음 (사용자에게 보여지지만 않게) = 비용적으로 경제적임

----------------------------------------------------------------------------------------------------

익명 객체(Anonymous Object)(익명 클래스(Anonymous Class))

클래스 정의와 동시에 객체를 생성하는것
따로 클래스 정의 없이 메소드 내에서 바로 클래스를 생성해 인스턴스화할 수 있으며,
이렇게 클래스의 선언과 객체의 생성을 동시에 하기 때문에 단 한번만 사용될 수 있고,
익명을 정의된 클래스는 일회용으로 사용되고 버려진다

그래서 만일 어느 메소드에서 부모 클래스의 자원을 상속받아 재정의하여 사용할 자식클래스가 딱한번만 사용되고 버려질거라면,
굳이 클래스를 정의하기보다는, 지역변수처럼 익명 클래스로 정의하고 스택이 끝나면 삭제되도록 하는 것이
유지보수면에서나 프로그램 메모리 면에서 이점을 얻을 수 있다

즉, 익명 클래스는 재사용할 필요가 없는 일회성 클래스를 굳이 클래스를 정의하고 생성하는것이 비효율적이기 때문에,
익명클래스를 통해 "코드를 줄이는 일종의 기법"이라고 말 할수 있다


public class Animal {
	void bark(){
		System.out.println("동물이 웁니다");
	}
}

public class Run {
	public static void main(String[] args) {

		Animal cat = new Animal(){
			@Override
			void bark(){
				System.out.println("야옹");
				jump(); // 오버라이딩한 메소드 말고, 새로 생성한 메소드는 익명클래스 내부에서만 사용 가능
			}

			void jump(){
				System.out.println("점프하기");
			}
		}; // 단 익명클래스는 끝에 세미콜론은 반드시 붙여야 한다

		cat.bark();
//		cat.jump(); // 오버라이딩한 메소드 말고, 새로 생성한 메소드는 외부에서 사용불가

	}
}

-----

주의사항 1

기존의 부모클래스를 상속한 자식클래스에서는 부모클래스의 메소드를 재정의할 뿐만 아니라 새로운 메소드를 만들어 사용할 수 있다
하지만 익명클래스 방식으로 선언한다면 "오버라이딩한 메소드"만 사용가능하고, 새로 정의한 메소드는 외부에서 사용이 불가능하다

-----

주의사항 2

익명 클래스도 내부 클래스의 일종이기 때문에, 외부의 지역 변수를 이용하려고 할때 똑같이 내부 클래스의 제약을 받게 된다.
따라서 내부 클래스에서 가져올 수 있는 외부 변수는 final 상수인 것만 가져와 사용할 수 있다.

------------------------------

익명클래스 선언 위치

public class Animal {
	void bark(){
		System.out.println("동물이 짖는다");
	}
}

위 (부모가 될)클래스가 있다고 할때

-----

1. 클래스 필드로 이용

클래스 내부에서, 여러 메소드에서 이용될 때 고려해 볼 만하다

class Creature {
	// 필드에 익명자식객체를 생성하여 이용
	Animal dog = new Animal(){
		public void bark(){
			System.out.println("멍멍");
		}
	};

	public void m1(){
		dog.bark();
	}

	public void m2(){
		dog.bark();
	}
}

-----

2. 지역 변수로서 이용

메소드에서 일회용으로 사용하고 버려질 클래스라면 적당하다

class Creature{
	void m1(){
		Animal dog = new Animal(){
			String bark(){
				return "멍멍";
			}
		};
		dog.bark();
	}
}

-----

3. 메소드 인수로 이용

만일 메소드 매개변수로서 클래스 자료형이 이용된다고 할 때 일회성으로만 사용된다면 인수로 익명객체를 넣으면 된다

public class Run {
	public static void main(String[] args) {

		Run r = new Run();

		r.m1(new Animal(){
			public void bark(){
				System.out.println("멍멍");
			}
		});

	}

	public void m1(Animal dog){
		dog.bark();
	}
}

------------------------------

익명 클래스 컴파일

내부 클래스를 컴파일 하면 $ 기호가 들어간 "클래스명$내부클래스명.class" 파일을 얻게된다

익명클래스도 내부클래스의 일종이니 마찬가지다

Main.java파일에서 Animal클래스의 익명 객체를 정의했다면,
컴파일시 Main.class, Animal.class, Main$1.class 이렇게 3개의 클래스 파일이 생기게 된다

익명클래스 파일부분이 Animal$1.class인데,
Animal클래스를 이용해 만든 익명클래스를 이름이 없는 자식클래스니까 $1로 표현한 것이다

익명객체를 2개 정의했다면 Animal$1.class, Animal$2.class 이런식으로 자바파일명${익명객체정의된순번}.class 규칙으로 클래스파일이 생기게 된다.
익명객체끼리는 아무리 내용이 똑같다고 하더라도, 서로 전혀 다른 객체이기때문에 별개로 취급되기 때문이다

실제로 코드상에서 익명객체.getClass().getName() 이렇게 클래스의 이름을 확인하면 위에서 말한대로 출력되게된다

------------------------------

인터페이스 익명 구현 객체

사실 실무에서 멀쩡한 클래스를 놔두고 익명클래스를 사용하는일은 거의 없다
하지만 자바의 익명클래스의 진가는 "인터페이스를 익명 객체로 선언"하여 사용할 때이다

추상화 구조인 인터페이스를 일회용으로 구현하여 사용할 필요가 있을때, 익명 구현 객체로 선언해서 사용하면 매우 시너지가 잘 맞게 된다

★쉽게말하면, 이미 구현까지 되어있는메소드를 다시 덮어쓰는(overwrite) 것보다, 정의만되어있는(머리만있는) 인터페이스를 구현(implement)하는게 더 쓸모있음
덮어쓰나 구현하나 둘다 똑같이, 새로 정의 한게 아닌 @Override라서 익명클래스에 적용이 가능함(위에써있듯 새로 만든메소드는 익명클래스 외부에서 사용 불가)

interface IAnimal{
	public String bark();
	public String jump();
}

public class Run {
	public static void main(String[] args) {

		IAnimal cat = new IAnimal() {
			@Override
			public String bark() {
				return "야옹";
			}

			@Override
			public String jump() {
				return "폴짝";
			}
		};

		cat.bark();
		cat.jump();
	}
}

당연히 추상클래스(abstract class)도 이런식으로 익명구현객체 생성이 가능하다

원래는 클래스가 인터페이스를 구현한 후 인터페이스를 구현한 클래스로 객체를 만들어야하는데,
위의 코드는 인터페이스를 바로 구현해서, 인터페이스를 구현한 클래스명없이 객체를 만들기때문에 이를 "익명 구현 객체" 라고 부른다

일반 클래스가 클래스를 상속하는 익명객체와 다르게 인터페이스는 강제적으로 메소드 정의를 통해 사용해야하는 규약이 있기 때문에,
"규격화에 도움"이 된다

ex) Runnable, Thread

----------------------------------------------------------------------------------------------------

★문자를 n번 반복시키기 (jdk1.5이상)

repeated = new String(new char[n]).replace("\0", s); → 문자열 s을 n번 반복

System.out.println(new String(new char[10]).replace("\0","-"));

----------------------------------------------------------------------------------------------------

문자열은 불변이다.(Immutable)

문자열 값이 같으면 같은 주소값을 참조한다 (똑같은 문자열이 여러개 있으면 메모리를 너무 많이차지하므로
같은 값이면 그 번지를 공유한다) 하지만 연산에 의한 결과는 다른 공간에 저장된다 → equals메소드를 이용해야하는 이유

String s1 = "이열음";
String s2 = "이열음";

값형 = 공간의 크기가 변하지 않음(고정) (stack영역에 딱딱맞춰서 저장됨)
참조형 = 공간의 크기가 변함(가변) (heap영역에 값을 넣고 번지수로 참조)

stack영역 = 질서정연 , 관리가 어려움
heap영역 = 자유분방 , 관리가 쉬움

----------------------------------------------------------------------------------------------------

★자바 프로그램 강제 종료
System.exit(0);

----------------------------------------------------------------------------------------------------

★문자열 널 비교시
if(qwer.equals(null)) → X
if(qwer.equals("")) → O

----------------------------------------------------------------------------------------------------

★quick search
Ctrl + Shift + L
Ctrl + Alt + Shift + L

----------------------------------------------------------------------------------------------------

★주민등록번호 유효성검사

951220-1021547

7 : 유효성 번호

0215 : 출생 신고 주민센터 고유 번호

4 : 출생 신고 날짜에 등록한 순서(남녀따로)

1 : 남자(1900년대생)
2 : 여자(1900년대생)
3 : 남자(2000년대생)
4 : 여자(2000년대생)
5 : 남자(귀화 외국인)
6 : 여자(귀화 외국인)
7 : 남자
8 : 여자
9 : 남자(1800년대생)
0 : 여자(1800년대생)


7  0   0   1   0   1  -  1  0  1  0  1  0  4
x  x   x   x
2  3   4   5   6   7     8  9  2  3  4  5  (마지막 검사자리는 포함하지않음)

14 +       5 +     7 +   8 +   2 +   4  = 40

40을 11로 나눈다 -> 몫(3) 나머지(7)

11 - 나머지(7) = 4(유효성 번호)

결과가 10이상일경우 → 다시 10으로 나눔 ↓↓
11 - 0 = 11 -> 1(유효성 번호)
11 - 1 = 10 -> 0(유효성 번호)

↓↓↓↓↓↓↓↓↓↓

public static void main(String[] args) throws IOException {

	BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

	String number = "";
	while(true) {
		System.out.print("주민 번호 입력 : ");
		number = reader.readLine();
		if(number.length() == 14) {
			break;
		}
		System.out.println("'-' 포함 14자리로 입력하세요");
	}
	
	int[] chk = {2,3,4,5,6,7,0,8,9,2,3,4,5};
	int total = 0;

	for(int i = 0; i < 13; i++) {
		if(i == 6) {
			continue;
		}
		total += chk[i] * Integer.parseInt(number.substring(i, (i + 1)));
	}
	
	int calc = 11 - total % 11;
	calc = calc % 10;
	if(calc == Integer.parseInt(number.substring(13,14))) {
		System.out.println("올바른 주민등록번호입니다");
	}
	else {
		System.out.println("올바르지 않은 주민등록번호입니다");
	}
}

----------------------------------------------------------------------------------------------------

중복값 제거 배열

int[] nums = new int[5];
for (int i = 0; i < nums.length; i++) {
	int rand = (int) (Math.random()*9+1);

	nums[i] = rand;

	System.out.printf("%d→%s\n",i,Arrays.toString(nums));

	//이미 들어있는 방까지 검사(i-1)
	for (int j = 0; j < i; j++) {
		if (rand==nums[j]) {
			System.out.println("중복값 발생");
			i--; //마지막 방을 다시 덮어쓰기
			break;
		}
	}
}
System.out.println(Arrays.toString(nums));

----------------------------------------------------------------------------------------------------

n의자리구하기

10의자리
int temp = 1234567
int temp = num % 100 / 10

----------------------------------------------------------------------------------------------------

한줄씩 끊어서 배열로 한방에 저장

try {
	File text = new File("C:\\FileLineTest\\testFile.txt");
	FileReader textRead = new FileReader(text);
	BufferedReader bfReader = new BufferedReader(textRead);
	String line = "";
	List<String> lineArray = new ArrayList<String>();
	// null 이 아닐때까지 반복한다.
	while ( (line = bfReader.readLine()) != null ) {
	// System.out.println(line); 출력
	// 리스트 배열에 line 한줄한줄씩 추가.
	lineArray.add(line);
	}
	for(int i=0; i<lineArray.size(); i++) {
	System.out.println(lineArray.get(i));
	}
} catch (FileNotFoundException e) {
	// 파일 없거나 이름 안맞으면 여기걸림.
	e.printStackTrace();
	System.out.println("파일이 존재하지않습니다. 경로를 확인해주세요");
} catch (IOException e) {
	e.printStackTrace();
}

컬렉션프레임워크 타입(배열방)의 길이 = lineArray.size()

참고 https://jeong-pro.tistory.com/69

----------------------------------------------------------------------------------------------------

입출력 예제

public static void main(String[] args) {
	
	ArrayList<String> name = new ArrayList<String>();
	ArrayList<Integer> kor = new ArrayList<Integer>();
	ArrayList<Integer> eng = new ArrayList<Integer>();
	ArrayList<Integer> math = new ArrayList<Integer>();
	ArrayList<Boolean> result = new ArrayList<Boolean>();
	
	final String PATH = "C:\\Users\\임채원\\Searches\\MoaTmp\\Desktop\\일\\파일_입출력_문제\\성적.dat";
	try {
		BufferedReader reader = new BufferedReader(new FileReader(PATH));
		
		String[] div = new String[10];
		String line = "";
		while ((line = reader.readLine())!=null) {
			div = line.split(",");
			
			name.add(div[0]);
			kor.add(Integer.parseInt(div[1]));
			eng.add(Integer.parseInt(div[2]));
			math.add(Integer.parseInt(div[3]));
			result.add(null);
		}
		
		reader.close();
		for (int i = 0; i < name.size(); i++) {
			int sum = kor.get(i) + eng.get(i) + math.get(i);
			if (sum>=60*3 && kor.get(i)>=40 && eng.get(i)>=40 && math.get(i)>=40) {
				result.add(i,true);
			}else {
				result.add(i,false);
			}
//				System.out.printf("%s : ",name.get(i));
//				System.out.println(result.get(i));
		}
	
	} catch (Exception e) {
		System.out.println("Q01.main()");
		e.printStackTrace();
	}
	
	try {
		String replace1 = PATH.replace(PATH,PATH.substring(0,PATH.lastIndexOf(".")));
		String PATH_convert = replace1 + PATH.replace(PATH.substring(0,PATH.lastIndexOf(".")),"_변환");
		BufferedWriter writer = new BufferedWriter(new FileWriter(PATH_convert));
		
		for (int i = 0; i < name.size(); i++) {
			writer.write(String.format("%s : %s\r\n",name.get(i),result.get(i)?"합격":"불합격"));
		}
		
		writer.close();
		
		System.out.println("변환성공");
		
	} catch (Exception e) {
		System.out.println("Q01.main()");
		e.printStackTrace();
	}
}

----------------------------------------------------------------------------------------------------

객체 정렬
Comparator - 정렬 알고리즘 : 퀵정렬
참고 : '정렬 알고리즘folka' 검색

ArrayList<Book> books = new ArrayList<Book>();

books.add(new Book("자바의 정석",999,"프로그래밍"));
books.add(new Book("오라클 데이터베이스",555,"데이터베이스"));
books.add(new Book("HTML5 기초",345,"웹프로그래밍"));
books.add(new Book("CSS디자인",543,"웹프로그래밍"));
books.add(new Book("JavaScript",819,"웹프로그래밍"));

System.out.println(books);

books.sort(new Comparator<Book>() {

	@Override
	public int compare(Book o1, Book o2) {
		return o1.pages - o2.pages;
	}
	
});


class Book{
	public String title;
	public int pages;
	public String category;
	
	public Book(String title, int pages, String category) {
		this.title = title;
		this.pages = pages;
		this.category = category;
	}

	@Override
	public String toString() {
		return "{title=" + title + ", pages=" + pages + ", category=" + category + "}\n";
	}
}

----------------------------------------------------------------------------------------------------

기호(문자) 글자수만큼 반복하기 (String) , (String,Double) , (String,String,Double)

public class MsgBox {
	public static void msg(String msg) {
		double n = 0;
		for (int i = 0; i < msg.length(); i++) {
			if (msg.charAt(i)>=44032 && msg.charAt(i)<=55203) {
				n+=1.35;
			}else {
				n++;
			}
		}
		System.out.println(new String(new char[(int)n]).replace("\0","-"));
		System.out.println(msg);
		System.out.println(new String(new char[(int)n]).replace("\0","-"));
	}
	public static void msg(String msg, double n) {
		double k = 0;
		for (int i = 0; i < msg.length(); i++) {
			if (msg.charAt(i)>=44032 && msg.charAt(i)<=55203) {
				k+=1.35;
			}else {
				k++;
			}
		}
		int j = (int)((n*1.35-k)/2);
		String blank = new String(new char[j]).replace("\0"," ");
		System.out.println(new String(new char[(int)n]).replace("\0","-"));
		System.out.println(blank + msg);
		System.out.println(new String(new char[(int)n]).replace("\0","-"));
	}
	public static void msg(String msg, String s) {
		double n = 0;
		for (int i = 0; i < msg.length(); i++) {
			if (msg.charAt(i)>=44032 && msg.charAt(i)<=55203) {
				n+=1.35;
			}else {
				n++;
			}
		}
		System.out.println(new String(new char[(int)n]).replace("\0",s));
		System.out.println(msg);
		System.out.println(new String(new char[(int)n]).replace("\0",s));
	}
	public static void msg(String msg, String s, double n) {
		double k = 0;
		for (int i = 0; i < msg.length(); i++) {
			if (msg.charAt(i)>=44032 && msg.charAt(i)<=55203) {
				k+=1.35;
			}else {
				k++;
			}
		}
		int j = (int)((n*1.35-k)/2);
		String blank = new String(new char[j]).replace("\0"," ");
		System.out.println(new String(new char[(int)n]).replace("\0",s));
		System.out.println(blank + msg);
		System.out.println(new String(new char[(int)n]).replace("\0",s));
	}
}

----------------------------------------------------------------------------------------------------

로또 번호  6개(1~45)
Random rnd = new Random();
ArrayList<Integer> lotto = new ArrayList<Integer>();
for (int i = 0; i < 6; i++) {
	boolean flag = false;
	int n = rnd.nextInt(45) + 1;
	// 검증
	for (int j = 0; j < i; j++) {
		if (n == lotto.get(j)) {
			flag = true;
			break;
		}
	}
	if (flag) {
		// 중복값
		i--;
	} else {
		lotto.add(n);
	}
}
Collections.sort(lotto);
System.out.println(lotto);


Set 구현
Random rnd = new Random();
HashSet<Integer> lotto2 = new HashSet<Integer>();
while(lotto2.size()<6) {
	lotto2.add(rnd.nextInt(45) + 1);
}
System.out.println(lotto2);

----------------------------------------------------------------------------------------------------

객체가 다르더라도 값이 같으면 같은 값으로 처리하고 싶을 때 - hashCode , equals 재정의

Person p3 = new Person("호호호",28);
Person p4 = new Person("호호호",28);

System.out.println(p3.equals(p4));


class Person {
	
	public String name;
	public int age;
	
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}

	@Override
	public String toString() {
		return "{name=" + name + ", age=" + age + "}";
	}
	
	
	@Override
	public int hashCode() {
		
//		"권나라20" → 12345
//		"한채아22" → 23423
//		"한가인20" → 12345
		return (this.name + this.age).hashCode();
	}
	
	@Override
	public boolean equals(Object obj) {
		//참조 주소값의 비교 → 상태값 비교
//		p1.equals(q2)
		
		Person p = (Person)obj;
		
		//return this == obj;
		return this.name.equals(p.name) && this.age == p.age;
	}
	
}

----------------------------------------------------------------------------------------------------

도큐먼트 주석 (단축키 Alt + Shift + J)

public 한테만 주석 달것
주석을 달고싶은 메소드나 클래스 위에
/**하고 엔터 치고 주석 안의 내용을 입력한다

1번기능
해당 메소드위에 마우스오버시 주석으로 단 설명,파라미터,리턴값 등이 나옴

2번기능
프로젝트폴더에 우클릭 → Javadoc → Configure버튼 → jdk폴더\bin\javadoc.exe 열기 → Next → Finish
탐색기 → 프로젝트 폴더 들어가보면 → doc폴더가 생성되어있음 → 들어가면 index.html이있는데
여기서 모든 도큐먼트와 함께 주석내용을 보기가능

----------------------------------------------------------------------------------------------------

실행중인 프로그램 종료하기

실행(f11)시키고 종료를 안한 프로그램이 많으면 부하가 걸려 렉걸리므로
결과를 다 확인는데 프로그램이 종료되지 않았다면

콘솔창에서 빨간네모(정지) 버튼 누르고
바로 옆에있는 X아이콘(Remove Launch) 클릭해서 하나씩 지우거나

ctrl + f2 눌러서 하나씩 지우거나


한번에 지우는 방법은
Window → Show View → Debug창을 열고

Debug창의 아무데나 우클릭 → Terminate/Disconnect All

이후 종료된 프로그램 Debug창에서 제거하기위해 (생략해도 됨)
Console창의 XX아이콘(Remove All Terminated Launches) 을 클릭한다


----------------------------------------------------------------------------------------------------

문자가 차지하는 넓이(길이/여백) 고정으로 바꿔주는 메소드 (문자,넓이)
public static String fixedLengthString(String string, int length) {
	return String.format("%1$"+length+ "s", string);
}

----------------------------------------------------------------------------------------------------

페이징 처리

main(){
	showPageList(list,0,0);
}

private static int showPageList(ArrayList<StudentDTO> list,int listNo, int j) {

	showHeader(listNo, (list.size()/15)+1);	// \t\t제목 [ listNo / Total ]		

	for (int i=listNo; i<listNo+1 ;i++) {	//한페이지만 보여줄 예정

		for (j=i*15;j<(15+i*15);j++) {

			if (j>=list.size()) 	// 목록보다 인덱스가 크면
				break;						// 	출력 중단
			else 
				System.out.printf("\t%s   ",fixedLengthString(list.get(j).getSeqStudent(),3));
				System.out.printf(""
						+ "%s\t%s\t%s\t%s\t%s\t",
//							j+1,
						list.get(j).getName(),
						list.get(j).getId(),
						list.get(j).getPhone(),
						list.get(j).getEmail(),
						list.get(j).getSeqRegCourse()
				);
				System.out.printf("%s\t",fixedLengthString(list.get(j).getEmploymentField(),7));
				System.out.printf(""
						+ "%s\t%s\n",
						list.get(j).getFirstRegistrationDate(),
						list.get(j).getName_b()
				);

		}	//2중 for
	}	//1중 for

	listNo = showMenu(list,listNo);

	if(listNo == 100 || listNo == -100)
		return listNo;
	else
		showPageList(list, listNo, 0);

	return listNo;

}

public static int showMenu(ArrayList<StudentDTO> list,int i) {

	int num=0;
	
	System.out.println("\t============================================================");
	System.out.println("\t\t1.이전 목록\t\t2.다음 목록");
	System.out.println("\t\t3.교육생 선택\t\t4.뒤로 가기");
	System.out.println("\t\t5.종료");
	System.out.println("\t============================================================");
	System.out.printf("\t\t메뉴선택 : ");	
	int selectMenu = scanner.nextInt();

	System.out.println();
	if (selectMenu==1) { // 이전목록 선택
		System.out.println("이전목록 보기");
		if(i==0){	//1페이지일때
			System.out.println("이전 목록이 없습니다.");
			return i;
		}else{		//2페이지부터
			return i-1;
		}
	}else if (selectMenu==2){ // 다음목록 선택
		if(i+1 > list.size()/15)	{// 다음목록이 존재하지 않으면
			System.out.printf("%d 다음 목록이 존재하지 않습니다.\n",i);
			return i;
		} else {
			return i+1;
		}
	}else if (selectMenu==3) { // 교육생 선택
		System.out.print("\t\t교육생번호 선택 :");
		num = scanner.nextInt()-1; 

		if(num>list.size()||num<0) {	// 그 페이지에서의 번호
			System.out.println("잘못된 번호 입력입니다.");
			return i;
		}else{	//교육생 선택완료
			return -100;
		}
	}else if (selectMenu==4) { // 뒤로가기
		return 100;
	}else if (selectMenu==5) { // 프로그램 종료
		System.exit(0);
	}else {
		System.out.println("잘못된 메뉴 선택입니다.");
	}

	return i;
}

public static void showHeader(int i, int total) {
	System.out.println("\t============================================================");
	System.out.printf("\t교번   성명\t아이디\t전화번호\t이메일\t수강번호\t희망분야\t가입일\t수강과정명 (%d/%d)\n",i+1, total);
	System.out.println("\t============================================================");
}

----------------------------------------------------------------------------------------------------

null에 빈문자열을 더했을때 문자 "null"로 바뀐다

String s = null + "";

System.out.println("[" + s + "]"); → false
System.out.println(s == ""); → false
System.out.println(s == null); → false
System.out.println(s == "null"); → false
System.out.println(s == null + ""); → false
System.out.println(s.equals("")); → false
System.out.println(s.equals(null)); → false
System.out.println(s.equals("null")); → true
System.out.println(s.equals(null + "")); → true
System.out.println(s.equals(""+null)); → true

----------------------------------------------------------------------------------------------------

이클립스 특정 워크스페이스에서 문제 생길 때

해당 workspace 경로\.metadata\.plugins\org.eclipse.e4.workbench.swt 폴더 하위의 dialog_settings.xml 삭제

----------------------------------------------------------------------------------------------------

저장시 자동 import (ctrl+shift+o)

Window → Preferences → Java → Editor → Save Actions →
Perform the selected actions on save 체크 → Organize imports 체크 → Apply and Close

(이때 Format source code 는 저장시 코드자동정렬임)

----------------------------------------------------------------------------------------------------

import static

static필드와 메소드를 앞에 "클래스." 을 안붙이고 쓸 수 있음

Math.abs(-123)를
abs(-123) 이렇게 쓸 수 있음

사용법
import static 패키지명.클래스명.*
or
import static 패키지명.클래스명.[필드명 or 메소드명]

ex)
import static com.example.java_.import_.t2.C1.*; // 지양
import static java.lang.System.out; // 권장
import static java.lang.Math.abs; // 권장

import한 클래스들중 겹치는 이름의 필드/메소드가 있을때는 컴파일 오류를 발생시켜줌

----------------------------------------------------------------------------------------------------

리스트 복사하기 (for문 내부에 List를 선언, clear() 쓰면 안됨)

List<Map<String, String>> partList = service.getExrPartList();
List<ExrVO> exrList = service.getExrList();

Map<String,List<ExrVO>> map = new HashMap<String,List<ExrVO>>(); // 부위별 운동
for(Map<String, String> part:partList){
	List<ExrVO> list = new ArrayList<ExrVO>();
	for(ExrVO exr:exrList){
		if (part.get("CODE").equals(exr.getPART())) { 
			list.add(exr);
		}
	}
	map.put(part.get("CODE"), list);
}
log.info(map);

model.addAttribute("map",map);

----------------------------------------------------------------------------------------------------

빌더 패턴
- 일반 생성자로 하면 가독성저하 및 불필요한 데이터를 적어야되고, 순서를 바꾸기 힘든 단점이 있음.
	때문에 getter로 하는데, getter와 빌더패턴의 차이점은 getter는 생성이 이미 되고 값을 수정을 하는것이고,
	빌더패턴은 객체를 생성할때 값을 넣어서 생성한다. 때문에 값을 변경하지 못하도록 동결시킬때 쓴다(불변객체를 생성하기 위한 패턴)

public class Resturant {
	private Long id;
	private String name;
	private String description;
	private double latitude;
	private double longitude;
	private String address;
	private String tel;
	private String category;
	
	public static Builder builder() {
		return new Builder();
	}

	public static class Builder {
		private Long id;
		private String name;
		private String description;
		private double latitude;
		private double longitude;
		private String address;
		private String tel;
		private String category;
		
		public Builder id(Long id) {
			this.id = id;
			return this;
		}
		public Builder name(String name) {
			this.name = name;
			return this;
		}

		public Builder description(String description) {
			this.description = description;
			return this;
		}
		
		public Resturant build() {
			return new Resturant(id, name, description, latitude, longitude, address, tel, category);
		}
	}
}

-----

@Builder 애노테이션을 이용 하면 간단해짐 (@AllArgsConstructor도 같이 넣어주기(기본생성자))

@Builder
@AllArgsConstructor
public class Resturant {
	private Long id;
	private String name;
	private String description;
	private double latitude;
	private double longitude;
	private String address;
	private String tel;
	private String category;
}

-----

생성할때

Resturant resturant = Resturant.builder()
	.id(0L)
	.description("강남역 11번 출구 쪽에 있는 자매수산 입니다.")
	.name("자매수산")
	.build();

----------------------------------------------------------------------------------------------------

가변인자(varargs)

자바에 점세개 ( . . . 자바스크립트에서는 전개연산자 / 가변인자)

보통 varargs 또는 가변인자 / 가변 매개변수 라고 함.
★String 객체가 "0개"부터 여러개까지 매개변수로 올수 있다는 뜻 (String 배열도 가능)
System.out.printf 메소드가 대표적

n개의 인수를 배열로 받을 수 있음

★가변인자를 마지막 인수로 받아야함
m1(String s1, int... i1){ → 이건 가능하지만
m1(int... i1, String s1){ → 이건 불가능
안되는 이유는 가변인자인지 아닌지를 구별할 방법이 없기때문에 허용하지 않는것


public void myMethod(String... strings){
    // method body
}
위의 예에서는

myMethod(); // Likely useless, but possible
myMethod("a");
myMethod("a", "b");
myMethod(new String[]{"a", "b", "c"});
이런식으로 다양하게 쓸수 있음. 중요한건 가변인자는 항상 배열일 필요없이 인자를 전달하지 않아도! 되고 인자 값이 한개도 가능하다는 것이다

또 위의 식으로 메소드에 전달했을 때

public void myMethod(String... strings){
    for(String whatever : strings){
            //가변인수에 전달된 객체를 각각 접근
    }

    // 위의 코드와 동일 각각 접근가능 
    for( int i = 0; i < strings.length; i++){
        // strings[i]형식으로 배열에 각각 접근가능하다.
    }
}

------------------------------

가변인자 vs 매개변수 타입을 배열로 하는것의 차이

가변인자는 내부적으로 배열을 이용하는데,
매개변수의 타입을 배열로 하면 반드시 인수를 넣어야하기때문에 인수를 생략이 불가능하다
그래서 null이나 길이가 0인 배열을 넣어줘야함

void m1(String[] str){
}

m1(null)
(or)
m1(new String[0])

------------------------------

가변인자를 오버로딩할 때 주의사항

private static String concatenate(String delim, String... args) {
	String result="";

	for (String str : args) {
		result += str + delim;
	}

	return result;
}

private static String concatenate(String... args){
	return concatenate("-", args);
}

위처럼 오버로딩을 하면 아래처럼 실행했을때 구별을 할 수 없기때문에 컴파일오류가 발생함. 가능하면 가변인자를 사용한 메소드는 오버로딩 하지 않는 것이 좋다

String[] strArr = {"100", "200", "300"};

System.out.println(concatenate("", "100", "200", "300"));
System.out.println(concatenate("-", strArr));

----------------------------------------------------------------------------------------------------

람다
기존 클래스에 메소드를 만들고 객체화 한 뒤에 끌어쓰는 방식이 아니라, 그때그때 바로 만들어서 사용하는것 (이름을 안짓고(정의하지않고 = 익명함수) 1번만 쓰고 버릴때 씀)
인터페이스를 통해 메소드를 만들 수 있도록 만들어 두고 아래처럼 쓰면 된다

인터페이스명 메소드명 = (매개변수) -> 수행할 코드;};

람다의 핵심은,
(파라미터) -> {수행할 코드}
를 통해 메소드를 정의하지 않고도 메소드처럼 쓸 수 있다는 것. 메소드와 같은 기능이지만 정의하지 않고도 사용한다는 점이 장점.

매개변수와 내용이1줄이냐에 따라서 문법이 바뀜(세미콜론, 괄호, 매개변수, return등을 생략이 가능해짐)

예제)
public interface Lamd {
	public int call(String val);
}
public static void main(String[] args){
	Lamd l = (s) -> s.length();
	System.out.println(l.call("asdf"));
}


람다 forEach로 List 출력
→ 현재문서 위쪽에 향상된 for 참고


람다 forEach로 Map 출력
ex)
Map<String, Integer> map = new HashMap<>();

map.put("aaa",10);
map.put("bbb",20);
map.put("ccc",30);

map.forEach((key,val) -> {
	if (val >= 20) {
		System.out.println("20이상!");
	}else {
		System.out.printf("key:%s value:%d\n", key, val);}
	}
);


더 자세한내용은 람다.txt 참고

----------------------------------------------------------------------------------------------------

★스트림

- 람다를 활용할 수 있는 기술중 하나로 배열과 컬렉션을 함수형으로 처리
- 간단하게 병렬처리(multi-threading)가 가능
- 생성 / 가공 / 결과만들기 세가지로 나뉨
- 스트림을 쓰는 이유는 배열이나 컬렉션(List,Set,Map)으로 원하는 값을 얻을 때 for문 도배를 방지하기 위해서임
ex) int형 배열을 중복을 제거하고 내림차순정렬하고 List형태로 반환하려고 하면..
	배열 내용을 가지고 for를 돌리면서 set에 값을 밀어넣은 후 set의 내용을 Iterator에 담아 다시 for를 돌리면서 Iterator의 값을 리스트에 넣은후
	List를 역정렬 후 반환해야하는데... Stream을 쓰면 한줄로 끝남

- 스트림 객체를 생성안하고 쓸수 있음. 스트림객체를 생성할경우 딱 한번만 소비(메소드 적용) 가능하고 그 이후에 또 적용시 IllegalStateException 발생

------------------------------

★생성

Arrays.stream(배열) : 기본배열을 Stream<String> / Stream<Long> / IntStream / DoubleStream 객체로 만듦
Arrays.stream(배열, [인덱스(포함)], [인덱스(미포함)]) : 잘라서 스트림 객체로 반환(기본배열만가능)
Stream.of(...values); : 리터럴들을 Stream<T>객체로 반환
Stream.of(배열) : 배열을 Stream<T>객체로 반환
리스트.stream() : 컬렉션을 Stream<E>객체로 반환

Stream.builder() : 스트림을 직접 만들 수도 있음
ex)
Stream<String> builderStream = Stream.<String>builder()
	.add("java").add("python").add("c++").add("html is not programming lang")
	.build(); // builderStream : "java", "python", "c++", "html is not programming lang"

------------------------------

★가공 (Stream객체를 받아서 다시 Stream으로 반환함)

map : 요소들을 특정조건에 해당하는 값, 또는 원하는대로 으로 가공(변환)해줌
	요소들에게 각각 연산, 대,소문자 변형 등 의 작업을 하고 싶을떄 사용 가능
	ex1) list.stream().map(s -> s.toUpperCase())
	ex2) list.stream().map(String::toUpperCase) // 참고로 ::를 쓴 뒤쪽부터는 .을 찍어도 힌트가 안나옴

mapToInt / mapToDouble / mapToLong : map과 같으나 반환형을 Stream이 아닌 IntStream / DoubleStream / LongStream 으로 반환시켜 집계함수를 사용할 수 있게 함

mapToObj : map과 같으나 반환형을 Stream으로 반환함. int(IntStream)가 String(Stream)으로 바뀔때 씀. (.map() + .boxed() 와 같음)
ex) Arrays.toString(IntStream.of(1, 2, 3).mapToObj(c -> c + "a") // [1a, 2a, 3a]

ex) String배열각각의 길이를 구해서 int배열로 반환
System.out.println(Arrays.toString(Arrays.stream(new String[]{"asd", "aa", "asdf"}).mapToInt(String::length).toArray()));

map에서 builder를 이용해서 다른클래스의 객체로 만들 수 있음
즉, List<Class1> 를 List<Class2> 로 바꾸는걸 for문 안쓰고도 쉽게 할 수 있음
ex)
List<Human> humans = ~~~~~~
List<Human2> humans2 = humans.stream().map(i -> Human2.builder()
		.no(i.no)
		.name(i.name)
		.weight(i.weight)
		.build()
).collect(Collectors.toList());


flatMap : 계층 구조를 평탄화 시킴
.flatMap(Arrays::stream) // 배열
.flatMap(Collection::stream) // 컬렉션
ex)
List<Integer> list = new ArrayList<>(Arrays.asList(1,2,3));
Set<Integer> set = new HashSet<>(Arrays.asList(4,5,6));
Stream.of(list, set) // [[1, 2, 3], [4, 5, 6]]
	.flatMap(Collection::stream) // [1, 2, 3, 4, 5, 6]
ex)
.flatMapToInt(arr -> IntStream.rangeClosed(arr[0] + 1, arr[1] - 1))

ex) 2차원배열에서 2번째 값들만 추출
Arrays.stream(arr).flatMapToInt(a -> IntStream.of(a[1])).toArray();


filter : 요소들을 조건에 따라 걸러내는(조건에 맞는것만 담기) 작업을 해줌
	길이의 제한, 특정문자포함 등 의 작업을 하고 싶을때 사용 가능
	ex) .filter(i -> i % 2 == 0)
	ex) .filter(result -> result.containsKey("body"))	"body"키가 있는것들만 필터링

.sorted() : 요소 정렬 (primitive Stream에는 boxed() 필요)
	ex.오름차순) .sorted()
	ex.내림차순) .sorted(Comparator.reverseOrder())
	ex.사용자 정렬) boxed().sorted((a, b) -> Integer.compare(a~~, b~~)) // .mapToInt(Integer::intValue).toArray() or .collect(

숫자 비교
(o1, o2) -> Integer.compare(o1, o2)

특정 상황에서 아래처럼 쓸 수 있음 (빼기(-) 연산자만 가능, 내림차순은 순서 바꾸면 됨)
(o1, o2) -> o1 - o2

문자열 비교
o1.compareTo(o2)


.distinct() : 요소 중복값 제거

.limit(n) : 요소 앞에서부터 n개 가져옴

.skip(n) : 앞에서부터 n개 제거하고 가져옴
.skip(배열길이 - 1).findFirst().get() : 마지막 값을 가져와서 Optional에 담음. Optional메소드인 .get()로 꺼낼 수 있음

.boxed() : primitive Stream을 Stream으로 만듦 (primitive Stream에 .collect() 하기 전에 필요)
	ex) [기본배열스트림객체].boxed()

.findFirst() : 첫번째 값을 가져와서 Optional에 담음. Optional메소드인 .get()로 꺼낼 수 있음
.findAny() : findFirst와 동일하나, 병렬로 처리할때는 달라짐. stream의 요소 순서와 상관없이 가장 먼저 찾은 요소를 리턴함
ex)
IntStream.range(0,100).parallel().filter(i -> i * 2 > 5).findAny().orElse(0) // 65
IntStream.range(0,100).parallel().filter(i -> i * 2 > 5).findFirst().orElse(0) // 3

.anyMatch() : 하나라도 true면 true반환
.allMatch() : 모두 true일때 true반환
.noneMatch() : 모두 flase일때 true반환

.sum : 값을 구해서 int로 반환
.max() / .min() : 값을 구해서 OptionalInt로 반환
.average() : 값을 구해서 OptionalDouble로 반환
.count() : 길이를 구해서 long으로 반환

.mapToDouble(Integer::doubleValue).average() : 평균을 가져와서 Optional에 담음. OptionalDouble메소드인 getAsDouble()로 꺼낼 수 있음

.mapToInt(Integer::intValue) : Stream을 primitive Stream으로 변환. 집계함수를 사용할 수 있게 해줌
ex) Arrays.asList(1,2,3,4,5).stream().mapToInt(Integer::intValue).sum()

.map(val -> Math.round(val*10)/10.0).collect(Collectors.toList()) : 반올림 등 가능

.map(val -> val = val + 10).collect(Collectors.toList()) : 값마다 10 더하기

Arrays.stream(s1).filter(s -> Arrays.asList(s2).contains(s)).toArray(String[]::new) : 두 String 배열에서 일치하는 값들을 새로운 배열로 만듬

리스트를 stream으로 만든경우 집계함수 사용시 아래와 같이 Integer::compareTo를 인수로 넣거나 
list.stream().max(Integer::compareTo)
or
mapToInt(Integer::intValue)로 primitive Stream으로 만들어야함
System.out.println(list.stream().mapToInt(Integer::intValue).max()

long에서 int는 .mapToInt(Long::intValue).max()

--------------------

★결과 만들기

.collect() : 요소들의 가공이 끝났다면 반환할 결과를 만듦. IntStream등 primitive stream은 먼저 .boxed()를 이용해 Stream으로 만들어야함


.collect(Collectors.toList()) : List로 변환
.collect(Collectors.joining()) : 요소들을 합쳐서 하나의 문자열로 반환
.collect(Collectors.joining("구분자")) : 요소들을 합칠때 구분자를 넣음
.collect(Collectors.collectingAndThen(Collectors.toSet(), arr -> Integer.min(arr.size(), 123))) : 컬렉션으로 만들고 만든 컬렉션으로 이후 작업까지 수행함


.collect(Collectors.groupingBy()) : 각 요소들을 묶음. Map<String, List<String>> 으로 반환함

ex) 같은 글자끼리 그룹화
(Map<String, List<String>>) Arrays.stream(s.split("")).collect(Collectors.groupingBy(i -> i)))
(Map<Character, List<Character>>) s1.chars().mapToObj(c->(char)c).collect(Collectors.groupingBy(s -> s))

ex) 같은 글자가 몇개씩 있는지 그룹화 해서 int[][]로 반환
.boxed()).collect(Collectors.groupingBy(n -> n)).entrySet().stream().map(arr -> new int[]{arr.getKey(), arr.getValue().size()}).toArray(int[][]::new);

entrySet : Map의 메소드. Map을 Set으로 만듦. 이 Set을 다시 .stream() 으로 스트림화할 수 있음. key와 value에 각각 연산을 할 수 있음. groupingBy와 연계하기 좋음
(Set<Map.Entry<K, V>>) 맵객체.entrySet()

ex) 한 번만 등장한 문자들 찾아서 정렬
String s = "abcabcaxdck";
Arrays.stream(s.split(""))
	.collect(Collectors.groupingBy(i->i))
	.entrySet()
	.stream()
	.filter(i -> i.getValue().size() == 1)
	.map(Map.Entry::getKey)
	.sorted()
	.collect(Collectors.joining());

new ArrayList에 넣어서 Set을 List로 만들 수 있음
new ArrayList<>(~~.entrySet())

-----

toArray : 기본배열로 반환


.toArray()
	// Stream<String> → String[]
	// IntStream → int[]

.toArray(String[]::new) // Stream<Object> or Stream<String> → String[]

.mapToObj(String::valueOf).toArray() // IntStream → Stream<String> → String[]

.mapToInt(Integer::parseInt).toArray(); // Stream<String> → IntStream → int[]
or
.mapToInt(Integer::valueOf).toArray(); // Stream<String> → IntStream → int[]

-----

2차원 배열 만들기

.map(i -> new double[]{
	Arrays.stream(i).average().orElse(0),
	idx.getAndIncrement()
}).toArray(double[][]::new);

-----

reduce : 데이터를 변환하지 않고, 더하거나 빼는 등의 연산을 수행하여 하나의 값으로 만들어서 Optional객체로 반환함

1번쨰 인수 : 0번지값, 두번째부터는 누적값(return되는 값)이 들어감
2번째 인수 : 1번지값, 2번지값...

(OptionalInt) 인트스트림.reduce((left, right) -> left + right)

최초의 left는 인트스트림의 0번지 값이 들어가고, right는 인트스트림의 1번지값이 들어감.
이후 배열을 반복하며 left는 0번지와 1번지의 두 값이 연산된 값이 들어가고, right는 2번지, 3번지, 4번지... 값이 들어감. 실행횟수는 최종적으로 length - 1


Stream<Integer> numbers = Stream.of(1,2,3,4,5,6,7,8,9,10);
Optional<Integer> sum = numbers.reduce((x, y) -> x + y);
sum.ifPresent(System.out::println);

아래처럼 Integer::sum으로도 쓸 수 있음
Optional<Integer> sum = numbers.reduce(Integer::sum);

초기값을 넣을때는 아래처럼 그냥 int로 받아야함 (Optional로 안받음)
int sum = numbers.reduce(10, (i, j) -> i + j);

초기값 있는 연산도 마찬가지로 아래처럼 함수형인터페이스로 쓸 수 있음
int sum = numbers.reduce(10, Integer::sum);

배열끼리 더하기 가능
Arrays.stream(arrs).reduce((arr1, arr2) -> new int[]{
				arr1[0] + arr2[0],
				arr1[1] + arr2[1]
		}).orElse(new int[]{});
↓↓↓
{1,2} + {10,11} → {11,13}

배열내부요소들끼리 더하기
return Arrays.stream(arrs).reduce(((ints, ints2) -> new int[]{
	Arrays.stream(ints).sum(), Arrays.stream(ints2).sum()
})).orElse(new int[]{});
{1,2,3} {10,11,12} → {1+2+3} {10+11+12} → {6, 33}

------------------------------

병렬처리

list.stream().parallel().reduce(0, (i, j) -> i - j));
그러면 (+1++2)+(+3++4)+(+5)... 이렇게 병렬로 연산되서 성능이 향상됨.

그러나 빼기(-)연산일 경우에는

// -1-2 - -3-4 - -5-6... → -1-2+3-4+5-6...
이렇게 되어서 원하는 결과가 안나오기때문에

// 1-2 + -3-4 + -5-6...
병렬처리된 결과들끼리는 합하라는 규칙을 추가해야함. 3번째 인수를 추가하면됨

list.stream().parallel().reduce(0, (i, j) -> i - j, (k, l) -> k + l);
list.stream().parallel().reduce(0, (i, j) -> i - j, Integer::sum); 도 가능

------------------------------

★요소반복
forEach : 요소마다 작업을 할 수 있게 해줌
	ex) [스트림객체].forEach(System.out::println)
forEach람다식에서 특정 조건에서는 건너뛰게하고싶으면 continue가 아닌 return을 넣어야함
스트림객체를 소비할때는 한번만 가능, 두번하면 java.lang.IllegalStateException 오류남


예제)
List<SampleDTO> SampleDTOList = new ArrayList<>();
SampleDTOList.add(new SampleDTO(2,"aaa","male"));
SampleDTOList.add(new SampleDTO(5,"bbb","female"));
SampleDTOList.add(new SampleDTO(7,"ccc","male"));
SampleDTOList.add(new SampleDTO(8,"ddd","female"));
SampleDTOList.add(new SampleDTO(10,"eee","male"));
SampleDTOList.add(new SampleDTO(20,"fff","female"));

List<String> list = SampleDTOList.stream()
        /** 람다를 인수로 받아, 스트림에서 특정 요소를 제외시킨다. 아래는 idx가 10 이상인 데이터를 선택한다. */
        .filter(a -> a.getIdx() < 10) // idx가 10보다 작은 데이터 선택
        .sorted(Comparator.comparing(SampleDTO::getIdx)) // idx 순서로 정렬
        /** 람다를 이용해서 한 요소를 다른 요소로 변환하거나 정보를 추출한다. */
        .map(SampleDTO::getName) // 이름 추출
        .limit(3) // 선착순 3개만 선택
        .collect(Collectors.toList()); // 리스트로 저장

/* 병렬 */
List<String> parallelList = SampleDTOList.parallelStream()
		.filter(a -> a.getIdx() < 10) // idx가 10보다 작은 데이터 선택
		.sorted(Comparator.comparing(SampleDTO::getIdx)) // idx 순서로 정렬
		.map(SampleDTO::getName) // 이름 추출
		.collect(Collectors.toList()); // 리스트로 저장

list.forEach(System.out::println);
parallelList.forEach(System.out::println);

----------------------------------------------------------------------------------------------------

flatMap 예제

스트림으로 List<aaaEntity> 를 aaaEntity안에 포함된 List<bbbEntity> 로 바꾸기

aaaEntity 안에 필드로
private List<bbbEntity> bbbbb;
이렇게 있으면 getter쓰듯이 변수첫글자대문자로 쓰면 됨

List<aaaEntity> entities = new ArrayList<>();
.
.
.
parkingAdditionalMapper.insertBulk(
		entities.stream()
		.flatMap(entity -> entity.getBbbbb().stream())
		.collect(Collectors.toList())
);

-----

null이 아닌것들만 모아서 담기 (null예외처리)

List<Bbb> changeList = list.stream()
.filter(item -> Objects.nonNull(item.getBbbbb()))
.flatMap(item -> item.getBbbbb().stream())
.collect(Collectors.toList());

----------------------------------------------------------------------------------------------------

스트림 내에서 인덱스 사용

AtomicInteger index = new AtomicInteger();index.getAndIncrement()
IntStream.of(1,2,3,4,5).map(i -> index.getAndIncrement())

----------------------------------------------------------------------------------------------------

map 내에서 중첩해서 stream을 쓸 수 있음

ex) 2차원배열의 평균을 구한후 랭킹화
Arrays.stream(score).map(arr -> Arrays.stream(arr).average().orElse(0)).mapToInt(n -> Arrays.stream(score).map(arr -> Arrays.stream(arr).average().orElse(0)).sorted(Comparator.reverseOrder()).collect(Collectors.toList()).indexOf(n) + 1).toArray();

----------------------------------------------------------------------------------------------------

IntStream

지정한 범위를 배열로 생성해 각각 연산할 수 있음

IntStream / Stream<Integer> / Stream<String> 이 3가지는 다 다름

가령 .collect(Collectors.joining())은 Stream<String>에만 쓸 수 있음.
IntStream 일경우는 .mapToObj(String::valueOf) 로,
Stream<Integer> 일경우는 .map(String::valueOf) 을 이용해 Stream<String>으로바꿔야함


생성

of / range / rangeClosed

(IntStream) IntStream.of(1,2,3,4,5) // 1,2,3,4,5
(IntStream) IntStream.of(new int[]{1,2,3,4,5}) // 1,2,3,4,5

(IntStream) IntStream.range(시작값(inclusive),끝값(exclusive))
ex) IntStream.range(0,5) // 1,2,3,4

(IntStream) IntStream.rangeClosed(시작값(inclusive),끝값(inclusive))
ex) IntStream.rangeClosed(0,5) // 1,2,3,4,5

-----

iterate( & limit) : 데이터를 점진적으로 만듦

(IntStream) IntStream.iterate(초기값, 계산식)

limit과 함께 사용해야함
ex) 0부터 3의 배수로 증가, 5개만 가져옴
(IntStream) IntStream.iterate(0, i -> i + 3).limit(5) // 0, 3, 6, 9, 12

ex) 역순으로 생성
int start = 0;
int end = 5;
IntStream.iterate(end - 1, i -> i -1).limit(end - start)

ex) 0과 1을 반복
IntStream.iterate(0, i -> (i + 1) % 2).limit(10)

ex) distinct()와 같이쓸경우 limit에 도달하지 못하고 계속 지워지기 때문에 무한루프에 빠지게 됨
IntStream.iterate(0, i -> (i + 1) % 2).distinct().limit(10).toArray()

ex) 아래와 같이 함수의 순서를 바꾸면 해결 가능
IntStream.iterate(0, i -> (i + 1) % 2).limit(10).distinct().toArray()

ex) cpu 혹사시키기
IntStream.iterate(0, i -> (i + 1) % 2).parallel().distinct().limit(10).toArray();

------------------------------

parallel

병렬처리. 스트림을 생성한 이후 parallel() 라는 signature method 만 추가해주면 됨

IntStream.range(0, 10).parallel().forEach(index -> {
	System.out.println("Starting " + Thread.currentThread().getName() + ",    index=" + index + ", " + new Date());
	try {
		Thread.sleep(5000);
	} catch (InterruptedException e) { }
});

------------------------------

가공

(IntStream) 인트스트림.filter(i -> i % 2 == 1) // 조건에 해당하는것들만 반환

(IntStream) 인트스트림.map(i -> i + 1) // 각각의 항목에 연산

(IntStream) 인트스트림.peek(System.out::println) // 중간 결과 확인가능. 결과/출력 메소드가 없을경우 실행되지않음

(IntStream) 인트스트림.sorted() // 오름차순 정렬
(Stream<Integer>) 인트스트림.boxed().sorted(Collections.reverseOrder()); // 내림차순 정렬 (★.boxed() 필요)

(IntStream) 인트스트림.distinct() // 중복값 제거

(IntStream) 인트스트림.skip(개수) // 지정한 index부터 시작함(지정한 개수를 건너뜀)

(IntStream) 인트스트림.limie(개수) // 방 길이를 지정한 길이로 잘라냄

(IntStream) IntStream.concat(인트스트림1, 인트스트림2) // 인스트스트림 두개를 연결함
ex) {1,2,3}, {4,5,6} → {1,2,3,4,5,6}

------------------------------

IntStream 결과 변환/출력

(int) 인트스트림.sum()
(long) 인트스트림.count()
(OptionalDouble) 인트스트림.average()
(OptionalInt) 인트스트림.max()
(OptionalInt) 인트스트림.min()

(boolean) 인트스트림.anyMatch(i -> i % 2 == 1) // 하나라도 조건에 맞으면 True
(boolean) 인트스트림.allMatch(i -> i % 2 == 1) // 모두 조건에 맞을때만 True
(boolean) 인트스트림.noneMatch(i -> i % 2 == 1) // 모두 조건에 안 맞을때만 True

(int[]) 인트스트림.toArray()

(Stream<Integer>) 인트스트림.boxed()

(List) 인트스트림.boxed().collect(Collectors.toList())

(void) 인트스트림.forEach(System.out::print)

(Longstream) 인트스트림.asLongStream // 다른 스트림으로 변환

------------------------------

Optional 결과 변환/출력

(int) Optional객체.orElse(0)

(void) Optional객체.ifPresent(System.out::println)

<T> Optional객체.orElseGet(() -> 메소드 or null인 경우 대체할 값);

------------------------------

사용예시

for (int i = 0; i < 10; i++) {
	System.out.println(i);
}

↓↓↓

IntStream.range(0, 10).forEach(System.out::println);


int answer = 0;
for (int i = 1; i <= n; i++) {
	if(n % i == 0) answer++;
}
return answer;

↓↓↓

(int) IntStream.rangeClosed(1,n).filter(i -> n % i == 0).count();


중복값 개수 구하는법
.count() - .distinct().count()

중복값 개수 구하는법 (HashSet, filter 이용)
Arrays.stream(lines).flatMapToInt(arr -> IntStream.rangeClosed(arr[0], arr[1])).filter(n -> !set.add(n)).count();

중복값이 있는지 찾는법 (HashSet, allMatch 이용. HashSet객체를 여러번생성할것같지만 1번만 생성되고, 중복값을 발견할경우 바로 종료됨)
Arrays.stream(lines).flatMapToInt(arr -> IntStream.rangeClosed(arr[0]+1, arr[1]-1)).allMatch(new HashSet<>()::add);


{2022=[9, 11, 12], 2023=[1, 2]} 이런 Map<Integer, Set<Integer>> 데이터가 있을때, 월들만 TreeSet에 모으기
Set<Integer> monthSet = groupedData.values().stream().flatMap(Set::stream).collect(Collectors.toCollection(TreeSet::new));

----------------------------------------------------------------------------------------------------

★Optional 쓰는법 (Optional 객체에는 .map()메소드를 쓸 수 있음)

1. null체크를 if문으로 나눠서 메소드를 사용하지 않고 간결하게 할 수 있음
2. null이 들어갈 경우 특정 값을 반환할 수 있음

Optional.empty() : Optional 빈 객체 생성
Optional.of(T) : 객체를 Optional로 Wrapping해줌. T타입의 객체가 null 이면 오류남. 절대 null이 아닐때만 쓰기
Optional.ofNullable(T) : 객체를 Optional로 Wrapping해줌. T타입의 객체가 null이면 Optional.empty를 반환함

optional.get() : Optional로 wrapping된 객체를 가져옴
optional.ifPresent() : Optional로 wrapping된 객체가 비어있지 않을 경우 실행
	ex) o2.ifPresent(s -> {
			System.out.println(s);
		});
optional.isPresent() : Optional로 wrapping된 객체가 있으면 true, 비었으면 false 반환.
if문에 넣어서 null체크해주면 getAsInt / getAsDouble 사용시 노란밑줄이 생기지 않음.
ex)
OptionalDouble o = Arrays.stream(arr).average();
if(o.isPresent())
	answer = o.getAsDouble();

optional.orElse(T) : Optional로 wrapper된 객체가 null이면 인수를 반환. isPresent 쓸필요없이 간단하게 널일때처리 가능
optional.orElseGet() : null인경우 메소드를 실행하거나 특정 값을 반환
Optional<T> optional = Optional.of(t);
optStr.orElse(Store::new);	// null 이면 Store 객체 반환
★ null이던 null이 아니던 orElse() 값을 실행

ptional.orElseGet() : Optional로 wrapper된 객체가 null이면 orElseGet() 안의 값을 반환
Optional<T> optional = Optional.of(t);
optStr.orElseGet(Store::new);	// null 이면 Store 객체 반환
★ null일 경우에만 orElseGet() 값을 실행

null일 경우에만 orElseGet() 값을 실행합니다.

optioanl.orElseThrow() : Optional로 wapping된 객체가 null이면 orElseThrow() Exception을 반환

-----

OptionalInt / OptionalDouble : 수학함수가 적용되면 Optional클래스가 아닌 OptionalInt / OptionalDouble 객체로 반환됨.
orElse 또는 getAsInt / getAsDouble 로 꺼낼 수 있고
만약 위 클래스에서  Optional<Integer> 객체로 바꾸고싶으면 Optional.of() 로 감싸면됨


자세한사용법참고: https://escapefromcoding.tistory.com/246

-----

orElseThrow 쓰는법

public Member findById(String memberId){
	return memberRepository.findById(memberId).orElseThrow(() -> new RuntimeException("회원이 없습니다."));
}

----------------------------------------------------------------------------------------------------

json객체로 변환

★org.json

1. 자바컬렉션을 json객체로 변환 (org.json.JSONObject / org.json.JSONArray 이용)

Map<String, Object> map1 = new HashMap<>();
map1.put("a", 1);
map1.put("b", 2);

Map<String, Object> map2 = new HashMap<>();
map2.put("c", 3);
map2.put("d", 4);

JSONObject jsonObj1 = new JSONObject(map1);

System.out.println("map::: " + map1);
System.out.println("jsonObj::: " + jsonObj1);


List<Map<String,Object>> list = Arrays.asList(map1, map2);

JSONArray jsonArr = new JSONArray(list);

System.out.println("list::: " + list);
System.out.println("jsonArr::: " + jsonArr);


2. 문자열을 json객체로 변환 (org.json.JSONObject / org.json.JSONArray 이용)

String jsonStr = "{\"result\":[{\"COMP_ORDER\":0},{\"COMP_ORDER\":1}]}";

JSONObject obj = new JSONObject(jsonStr);

JSONArray arr = (JSONArray) obj.get("result");


★ get("")으로 찾은게 객체라면 (JSONObject)로 형변환까지 하는 메소드. 객체가 아니면 오류나니 주의. get("") 대신 쓰면 됨
.getJSONObject("")

★ put 메소드 말고 append 메소드는 배열을 추가할때 사용함.

-----

★ org.json.simple

1. 문자열(String)을 json객체로 변환 (org.json.simple.JSONObject / org.json.simple.parser.JSONParser / org.json.simple.parser.ParseException 이용)

Object jsonStr = "{\"result\":[{\"COMP_ORDER\":0},{\"COMP_ORDER\":1}]}";

<JSONObject로 변환>
JSONParser parser = new JSONParser();
JSONObject obj = null;
try {
	obj = (JSONObject) parser.parse(jsonStr);
} catch (ParseException e) {
	e.printStackTrace();
}

<JSONArray로 변환>
JSONParser parser = new JSONParser();
JSONArray arr = null;
try {
	arr = (JSONArray) parser.parse(jsonStr);
} catch (ParseException e) {
	e.printStackTrace();
}

(V) put(K key, V value) : 입력
(V) get(Object key) : 출력

-----

★ com.google.gwt.json.client

1. 문자열(String)을 json객체로 변환 (com.google.gwt.json.client~ 이용, 깡통 프로젝트에서는 xml추가해도 테스트 불가)

JSONObject jsonObj = (JSONObject) JSONParser.parseStrict(JSON.stringify((JsObject)jsonStr));
call로 받은거 불러올떄는 위처럼 하는데..

직접 만든 문자열로 쓸때는 아래처럼 stringify를 빼고 써야함
Object o = "{\"이름\":\"나나나\"}";
JSONObject topObj = JSONParser.parseStrict((String) o).isObject();

객체 탐색
System.out.println(((JSONObject)jsonObj).get("result").isArray().get(0).isObject().containsKey("COMP_ORDER"));


(JSONValue) put(String key, JSONValue jsonValue) : 입력
(JSONValue) get(String key) : 출력


"키" 가 존재하는지 유무 boolean으로 반환하는 메소드

org.JSONObject → obj.has("XXX")
gwt.JSONObject → containsKey("XXX")


JSONObject를 Map으로 변환해주는 메소드 / JSONArray를 List로 변환해주는 메소드
.toMap() / .toList()

----------------------------------------------------------------------------------------------------

ObjectMapper

------------------------------

"json문자열 / json문자열을 응답하는 URL객체"를 JsonNode로 만들어서 탐색 하는 방법

.readTree()


ObjectMapper mapper = new ObjectMapper();

JsonNode node = mapper.readTree(json문자열 or json문자열을 응답하는 URL객체)

------------------------------

"json문자열 / json문자열을 응답하는 URL객체"를 컬렉션으로 만드는 방법

.readValue()
&
TypeReference


ObjectMapper mapper = new ObjectMapper();

Map<String, Object> map = mapper.readValue(json문자열 or json문자열을 응답하는 URL객체, new TypeReference<>(){});
or
List<Map<String, Object>> map = mapper.readValue(json문자열 or json문자열을 응답하는 URL객체, new TypeReference<>(){});

------------------------------

JsonNode를 컬렉션으로 만드는 방법

.readValue()
&
TypeReference

기존 JsonNode객체를 문자열로 바꾼 후 .readValue() & TypeReference를 사용해야함


ObjectMapper mapper = new ObjectMapper();
JsonNode item = root.findPath("item");
mapper.readValue(item.toString(), new TypeReference<Map<String, Object>>() {});

------------------------------

POJO를 JsonNode로 만드는 방법

.valueToTree()
or
.convertValue()


School school = new School();

JsonNode jsonNode1 = objectMapper.valueToTree(school);
or
JsonNode jsonNode2 = objectMapper.convertValue(school, JsonNode.class);

------------------------------

JsonNode에서 탐색하는 방법

.findPath()

제이쿼리의 .find() 와 동일

JsonNode root = mapper.readTree(...)
JsonNode item = root.findPath("nickName");

----------------------------------------------------------------------------------------------------

json 응답 샘플 사이트

https://jsonplaceholder.typicode.com/comments

----------------------------------------------------------------------------------------------------

클래스 객체를 탐색하는 방법
com.fasterxml.jackson.databind.JsonNode

valueToTree / convertValue

(JsonNode) get(key) : 키가 없을경우 null반환
(JsonNode) path(key) : 키가 없을경우 MissingNode객체반환. 이 객체 뒤에 .isMissingNode() 메소드를 붙이면 true를 반환
(JsonNode) findPath(key) : 아래로 끝까지 내려가면서 찾음. 없으면 MissingNode 반환. (제이쿼리의find와 동일)

.IllegalArgumentException: No serializer found for class ~~~ and no properties discovered to create BeanSerializer
↓↓↓
아래 내용 추가
objectMapper.setVisibility(PropertyAccessor.FIELD, JsonAutoDetect.Visibility.ANY);

ex)
Student student = new Student();
student.name = "최낙범";
Teacher teacher = new Teacher();
teacher.human = new Human("김준수",20);
teacher.gender = "m";
School school = new School();
school.student = student;
school.teacher = teacher;
school.schoolFlower = "개나리";

ObjectMapper objectMapper = new ObjectMapper();
objectMapper.setVisibility(PropertyAccessor.FIELD, JsonAutoDetect.Visibility.ANY);

JsonNode jsonNode1 = objectMapper.valueToTree(school);
JsonNode jsonNode2 = objectMapper.convertValue(school, JsonNode.class);

System.out.println(jsonNode1);
// {"student":{"age":0,"name":"최낙범"},"teacher":{"human":{"name":"김준수","age":20},"gender":"m"},"schoolFlower":"개나리"}

System.out.println(jsonNode2);
//{"student":{"age":0,"name":"최낙범"},"teacher":{"human":{"name":"김준수","age":20},"gender":"m"},"schoolFlower":"개나리"}


System.out.println(jsonNode1.findPath("teacher")); // {"human":{"name":"김준수","age":20},"gender":"m"}
System.out.println(jsonNode1.findPath("gender")); // "m"
System.out.println(jsonNode1.findPath("name")); // "최낙범" (이름이 같은 키가 있을경우 부모계층의 값이 반환됨)

System.out.println(jsonNode1.get("name")); // null
System.out.println(jsonNode1.get("teacher")); // {"human":{"name":"김준수","age":20},"gender":"m"}
System.out.println(jsonNode1.get("teacher").get("human")); // {"name":"김준수","age":20}

System.out.println(jsonNode1.findPath("asd").toString().equals("")); // true
System.out.println(jsonNode1.get("asd")); // null
System.out.println(jsonNode1.path("asd").getClass()); // class com.fasterxml.jackson.databind.node.MissingNode
System.out.println(jsonNode1.path("asd").isMissingNode()); // true

----------------------------------------------------------------------------------------------------

직렬화(Serialization) & 역직렬화(Deserialize)


직렬화 : 객체에 저장된 데이터를 스트림에 쓰기(write)위해 연속적인(serial) 데이터로 변환하는 것

말그대로 객체를 직렬화하여 전송 가능한 형태로 만드는 것을 의미한다. 객체들의 데이터를 연속적인 데이터로 변형하여 Stream을 통해 데이터를 읽도록 해준다.
이것은 주로 객체들을 통째로 파일로 저장하거나 전송하고 싶을 때 주로 사용된다.
POJO → byte형태 or JSON문자열 등

CSV, XML, JSON 직렬화
	사람이 읽을 수 있는 형태. 저장공간의 효율성이 떨어지고, 파싱하는 시간이 오래걸림
	데이터의 양이 적을때 주로 사용함
	최근에는 JSON을 많이 사용
	모든 시스템에서 사용이 가능함

Binary 직렬화
	사람이 읽을 수 없는 형태
	저장공간을 효율적으로 사용할 수 있고, 파싱하는 시간이 빠름
	데이터의 양이 많을 때 주로 사용함
	모든 시스템에서 사용이 가능함 ex) 프로토콜, Apache Avro 등

------------------------------

역직렬화 : 스트림으로부터 데이터를 읽어서 객체를 만드는것

직렬화된 파일 등을 역으로 직렬화하여 다시 객체의 형태로 만드는 것을 의미한다. 저장된 파일을 읽거나 전송된 스트림 데이터를 읽어 원래 객체의 형태로 복원한다.
byte형태 or JSON문자열 등 → POJO

------------------------------

직렬화 & 역직렬화시 Serializable 마커 인터페이스 구현 필요(마커 인터페이스: 아무런 메소드도 선언하지 않은 인터페이스)

@ToString
@AllArgsConstructor
public class Animal implements Serializable{
	String name;
	int age;

	String bark(){
		return "동물이 짖는다";
	}
}

class Run{
	public static void main(String[] args) throws IOException {

		// 직렬화(Serialization)
		FileOutputStream fos = new FileOutputStream("objectfile.ser");
		ObjectOutputStream oos = new ObjectOutputStream(fos);
		oos.writeObject(new Animal("navi", 12));
		oos.flush();

		// 역직렬화(Deserialization)
		Animal a1 = null;
		try (FileInputStream fis = new FileInputStream("objectfile.ser");
			ObjectInputStream ois = new ObjectInputStream(fis)) {
			a1 = (Animal) ois.readObject();
		} catch (ClassNotFoundException e) {
			throw new RuntimeException(e);
		}
		System.out.println(a1);
	}
}

----------------------------------------------------------------------------------------------------

json직렬화

writeValueAsString, writeValue 메소드 사용시 VO/DTO에 getter가 있어아함

ex)
@AllArgsConstructor
@Getter
public class Person {
	String name;
	int age;
	String address;
}


public class Run {
	public static void main(String[] args) throws IOException {

		ObjectMapper objectMapper = new ObjectMapper();

		Person person = new Person("zooneon", 25, "seoul");

//		objectMapper.writeValue(new File("person.json"),person);
		String jsonString = objectMapper.writeValueAsString(person);
		System.out.println(jsonString); // json문자열로 출력

		jsonString = objectMapper.writerWithDefaultPrettyPrinter().writeValueAsString(person);
		System.out.println(jsonString); // 예쁘게 출력

	}
}

------------------------------

json역직렬화(Deserialization)

json데이터의 key와 필드명이 같다면 잭슨애노테이션 없이 ObjectMapper의 readValue메소드만으로 POJO에 매핑을 할 수 있음
1. 생성자가 아예 없거나, 빈 객체를 만들 수 있는 빈 생성자(@NoArgsConstructor) 가 있어야 함
2. 게터(getter)가 있어야함
3. JSON문자열에는 있지만 필드에는 없는 키가 있을경우
@JsonIgnoreProperties(ignoreUnknown = true) 를 클래스에 붙여주기

ex)
@ToString
@Getter
@JsonIgnoreProperties(ignoreUnknown = true)
public class Univ {
	String school;
	List<Human> list;

	@ToString
	@Getter
	@JsonIgnoreProperties(ignoreUnknown = true)
	static class Human{
		String name;
		int age;
		int height;
		float weight;
	}
}

String obj = SampleJSONData2.getData().toString();
System.out.println(obj);

ObjectMapper mapper = new ObjectMapper();

try {
	Univ univ = mapper.readValue(obj, Univ.class);
	System.out.println(univ);
} catch (JsonProcessingException e) {
	throw new RuntimeException(e);
}


★Convert "JSON Array String" to "Java List"
String jsonArr = "[{\"name\":\"Ryan\",\"age\":30},{\"name\":\"Jake\",\"age\":20}]";
List<User> users = objectMapper.readValue(jsonArr, new TypeReference<>() {});
 
★Convert "JSON String" to "Java Map"
String jsonArr = "{\"name\":\"Ryan\",\"age\":30}";
Map<String, Object> user = objectMapper.readValue(jsonArr, new TypeReference<>() {});

만약 익명함수 내에서 쓰는 경우는 new TypeReference<>() 이렇게 <>(빈꺽새) 는 못쓰고
new TypeReference<Map<String, Object>>() 이런식으로 써야함

-----

UnrecognizedPropertyException : Unrecognized field "XXX"
key와 필드명이 다를 경우 발생

MismatchedInputException: Cannot construct instance of~~~
생성자가 있고, 빈 생성자가 없을 경우 발생 (@NoArgsConstructor)

MismatchedInputException: Cannot deserialize value of type `java.util.ArrayList<클래스>` from Object value (token `JsonToken.START_OBJECT`)
List로 변환할 json이 배열이 아닐경우 발생

------------------------------

@JsonCreator
@JsonProperty

Jackson이 deserialize 과정에서 별도의 설정이 없을 때 처리되는 동작은 다음과 같다.
1. 기본 생성자를 이용해서 생성
2. 필드가 public이면 직접 할당
3. 필드가 private이면 setter 사용

우선 jackson의 ObjectMapper클래스를 이용해
ObjectMapper mapper = new ObjectMapper(); 로 객체매퍼 객체를 생성하고

json데이터를 엔티티(VO/DTO) 객체로 변환시킨다

이때 변경전 json데이터의 키이름을 엔티티(VO/DTO)의 생성자에 @JsonProperty("XXX") 이 안에 넣으면
readerFor와 readValue메소드가 객체를 생성한다

ex)
@ToString
class Student {
	public int id;
	public String name;

	@JsonCreator
	public Student(@JsonProperty("rollNo") int rollNo, @JsonProperty("theName") String name){
		this.id = rollNo;
		this.name = name;
	}

//	팩토리메소드를 만들고 @JsonCreator을 붙여도 똑같이 Deserialization됨. (팩토리메소드가 static이어야 함. @AllArgsConstructor도 필요)
//	@JsonCreator
//	public static Student asd(@JsonProperty("rollNo") int rollNo, @JsonProperty("theName") String name){
//		return new Student(rollNo,name);
//	}

}

public class Run {
	public static void main(String[] args) throws JsonProcessingException {
		String json = "{\"rollNo\":11,\"theName\":\"Mark\"}";
		ObjectMapper mapper = new ObjectMapper();
		Student student = mapper
				.readerFor(Student.class)
				.readValue(json);
		System.out.println(student);
	}
}

-----

원하는 key만 가져오기(VO/DTO 필드에 있는 속성만 매핑하기)

getter 필요

아래 문장 필요 (필드에 없는 key는 안넣겠다는 뜻)
objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);

내부 클래스로 만들면 불필요한 파일 개수를 줄일 수 있음

ex)
@Getter
@ToString
@NoArgsConstructor
public class Person {
	private String name;
	private Contact contact;
	private Job job;

	@Getter
	@ToString
	@NoArgsConstructor
	@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
	public class Contact {
		String phoneNumber;
		String email;
	}

	@ToString
	@Getter
	public class Job {
	}

}

public class Run {
	public static void main(String[] args) throws JsonProcessingException {

		String jsonStr = "{\n" +
				"  \"name\": \"zooneon\",\n" +
				"  \"age\": 25,\n" +
				"  \"address\": \"seoul\",\n" +
				"  \"contact\": {\n" +
				"    \"phone_number\": \"0102222\",\n" +
				"    \"email\": \"foo@google.com\"\n" +
				"  },\n" +
				"  \"job\": {\n" +
				"    \"working\": true,\n" +
				"    \"workplace\": {\n" +
				"      \"name\": \"Sejong Univ.\",\n" +
				"      \"position\": \"student\"\n" +
				"    }\n" +
				"  }\n" +
				"}";

		ObjectMapper objectMapper = new ObjectMapper();
		objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);

		Person person = objectMapper.readValue(jsonStr,Person.class);
		System.out.println(person.getName());
		System.out.println(person.getJob());
		System.out.println(person.getContact());

	}
}

-----

@JacksonInject

ex)
@Getter
@ToString
class Student {

	@JacksonInject
	private int id;

	private String name;

}

public class Run {
	public static void main(String[] args) throws JsonProcessingException {
		String json = "{\"name\":\"My bean\"}";

		InjectableValues inject = new InjectableValues.Std().addValue(int.class, 1); // id값으로 1 주입
		Student bean = new ObjectMapper().reader(inject).forType(Student.class).readValue(json);

		System.out.println(bean);


	}
}

-----

@JsonAnySetter

ex)
@ToString
@Getter
public class Student {
	public String name;
	private Map<String, String> properties = new HashMap<>();

	@JsonAnySetter
	public void add(String key, String value) {
		properties.put(key, value);
	}

}

public class Run {
	public static void main(String[] args) throws JsonProcessingException {
		String json = "{\"name\":\"My bean\",\"attr1\":\"val1\",\"attr2\":\"val2\"}";

		Student bean = new ObjectMapper()
				.readerFor(Student.class)
				.readValue(json);

		System.out.println(bean);

		System.out.println(bean.getProperties().get("attr1"));

	}
}

-----

@JsonSetter

ex)
@ToString
@Getter
public class Student {
	public String name;
	private int age;

	@JsonSetter("theName")
	public void setTheName(String name) {
		this.name = name;
	}

	@JsonSetter("age")
	public void setTheAge(int age) {
		this.age = age;
	}

}

public class Run {
	public static void main(String[] args) throws JsonProcessingException {
		String json = "{\"theName\":\"My bean\",\"age\":11}";

		Student bean = new ObjectMapper()
				.readerFor(Student.class)
				.readValue(json);

		System.out.println(bean);

	}
}

-----

@JsonAlias
필드에서 바로 원본키를 입력해 원하는 필드명으로 바꿀 수 있음

ex)
private Integer projectId;
private String userId;
private List<Object> commits;

@JsonAlias("before")
private String asd;

그런데 만약 엘리어스를 쓰려는 키이름을 똑같이 다른용도로 쓰고싶으면
ex)
private String id;
@JsonAlias("id")
private String pushId;
위처럼 쓰면 JsonAlias는 무시돼서 pushId에 들어가는게 아니라 id속성에 들어감

-----

JSON데이터 중에 배열을 받을때는

List<DTO클래스> 로 하면 안되고
List<Object> 로 해야 받아짐★

같은 선상에 있는 key만 @JsonSetter / @JsonAlias등으로 읽을 수 있음

----------------------------------------------------------------------------------------------------

null / 빈문자열 예외처리시

문자열화 된건(toString) 반드시 equals로 따옴표("") 안에서 비교해야함.
1. ""
2. "null"
3. "[]"

객체는 null과 비교
or
toString한 후 equals() 메소드 로 "" or "null" 등과 비교

-----

빈값/널 체크


★gwt.JSONObject

1. 키는 있는데 값이 있는지
obj.get("XXX").toString() == "\"\""

2. 키가 있는지
obj.containsKey("XXX");


★org.json.JSONObject

1. 키가 있는데 값이 없을때
obj.get("XXX").toString().equals("");

2. 키가 있는지
obj.has("XXX");

----------------------------------------------------------------------------------------------------

boolean값에 문자열을 붙여 문자로 만들어 출력시

붙인 문자는 안나오고, 무조건 false가 찍힘

boolean 테스트시 무조건 오로지 해당 boolean값만 단독으로 출력해야함

----------------------------------------------------------------------------------------------------

StringBuilder

문자열을 원하는대로 만들때 유용한 클래스
String끼리 더하는 방법은 메모리 할당과 해제를 발생시키는데, 덧셈 연산이 많아진다면 성능적으로 좋지 않음

생성
StringBuilder sb = new StringBuilder();

(StringBuilder) sb.append(문자열) : 문자열을 맨 뒤에 붙이기
(StringBuilder) sb.insert(인덱스, 문자열) : 원하는 index로 문자열 삽입
(StringBuilder) sb.reverse() : 뒤집기. 원본 스트링빌더를 뒤집음 주의
(StringBuilder) sb.delete(인덱스1(inclusive), 인덱스2(exclusive)) : 인덱스1부터 인덱스2전까지 제거함 abc에서 delete(1,2) 하면 b가 사라짐
(int) indexOf(문자열) : 문자열 검색
(StringBuilder) sb.deleteCharAt(인덱스) : 인덱스의 문자 한글자 제거
(StringBuilder) sb.replace(인덱스1(inclusive), 인덱스2(exclusive), 문자열) : 인덱스1부터 인덱스2전까지 제거후 문자열삽입
(int) sb.length() : 길이
(StringBuilder) sb.setCharAt(인덱스, '문자') : 문자 한글자 교체 (길이내에서만 가능(새로 추가 불가))
(void) sb.setLength(10) : 길이 설정

그외 substring, lastIndexOf 등 문자열 함수 사용 가능

----------------------------------------------------------------------------------------------------

null은 "-"로, 양 끝 ""(큰따옴표,Quotation) 제거

private String chkTxt(Object object) {
	return object == null ? "-" : removeQuot(object.toString());
}

public static String removeQuot(Object o) {
	String txt = o.toString();
	if (txt.substring(0,1) == "\"" && txt.substring(txt.length()-1, txt.length()) == "\"") {
		return txt.substring(1, txt.length()-1);
	}else {
		return txt;
	}
}

----------------------------------------------------------------------------------------------------

반복문 내에서 전역변수 쓸때는 잘 생각해보고 쓰기

마지막 반복이후에 값만 전역변수에 들어가짐.
변수를 만들어서 다른곳에 넘겨야할때는 전역변수 말고, 파라미터로 반복해서 넘겨주기

----------------------------------------------------------------------------------------------------

이클립스 퀵서치 - 와일드카드

in: 입력란에 *.java *.js, *.jsp 이런식으로 입력하면
원하는 텍스트가 포함된 파일명만 찾을 수 있음

? 로 글자수 검색도 가능

----------------------------------------------------------------------------------------------------

sTime.getValue() != null && eTime.getValue() !& null

를 아래처럼 바꿀 수 있음

!(sTime.getValue() == null || eTime.getValue() == null)

----------------------------------------------------------------------------------------------------

프레임워크 / 라이브러리 / API 차이


프레임워크(Framework) : 어떤 물건을 만드는데 필요한 틀, 뼈대라고 이해했다. 컴퓨터 본체로 생각한다면 케이스라고도 볼 수 있을 것 같다.

-----

라이브러리(Library) : 프레임워크와 비슷한 느낌(?)이라 혼동할 수 있지만, 라이브러리는 특정 기능에 대한 도구나 함수를 모아둔 집합이다.

흔히 스패너, 망치...등이 들어있는 공구박스가 라이브러리라고 볼 수 있을 것 같다.
못을 박을 땐 망치를, 너트를 죄거나 풀때는 스패너를... 처럼 상황에 따라 단순 활용이 가능한 도구들의 집합

-----

API(Application Programming Interface) : 응용 프로그램을 작성할 때 필요한 매개체

라이브러리와 API에서의 공구박스 활용 위치를 살펴보자.
라이브러리에서는 나무판자에 못을 박기 위해서는 망치가 필요해 내 공구박스에 있는 망치를 사용했다.
하지만 API에서는 나는 나무판자와 못만 상대방에게 주고 상대방이 공구박스의 망치를 이용해 못이 박힌 나무판자를 만들어 준 것이다.
둘의 차이는 망치가 나에게 있느냐 없느냐, 그 망치로 내가 작업을 했냐이다. 

-----

다른 해설

프레임워크
범용 기능들을 제공해줌으로써 애플리케이션을 개발하기 쉽도록 해주는 소프트웨어이다.
덕분에 개발자는 핵심 로직에만 집중할 수 있음
Java로 Web 애플리케이션을 개발할 경우 Servlet 관련 로직들을 구현해야 하지만, Spring 프레임워크를 사용하면 이러한 부분들을 추상화시키고 @RequestMapping 같은 기능으로 쉽게 구현할 수 있게 편의성을 제공해줌
제어의 흐름을 개발자가 아닌 프레임워크가 가지고 있음
즉, 프레임워크가 개발자가 작성한 코드를 제어하고 대신 실행
대표적인 프레임워크로 Java 기반의 Spring, Python 기반의 장고, Javascript 기반의 노드 JS가 존재

상호협력하는 클래스와 인터페이스의 집합
응용 프로그램이 수동적으로 프레임워크에 의해 사용된다.
Vue, Junit, Spring Frameowrk
(리액트는 프레임워크인 이유 https://canoe726.tistory.com/23)


라이브러리
개발자가 사용할 수 있는 API들을 종류나 목적에 따라서 나누어 정의한 API 묶음
재사용 가능한 코드들의 집합
정렬 알고리즘을 사용할 때 직접 구현해서 사용해도 되지만 이는 상당히 번거로움
실제로 우리는 정렬이 필요할 경우 java.util 패키지에 존재하는 정렬 메소드를 사용함
이처럼 자주 사용될 수 있는 기능들을 구현하여 모아놓은 것이 라이브러리
또한, 직접 sort() 메소드를 가져와서 실행하는 것처럼 개발자가 직접 제어의 흐름을 담당 → 프레임워크와 라이브러리의 가장 큰 차이점
독립성을 가진다. 다른 라이브러리를 의존하지 않는다.
응용 프로그램이 능동적으로 라이브러리를 사용한다. 다시 말해서 개발자가 개발할 때 필요한 부분에 능동적으로 라이브러리를 호출해서 사용한다.
ex) Lombok, jQuery
 

API
Application Programming Interface의 약자로써 응용프로그램에서 사용할 수 있도록 운영체제나 다른 프로그램이 제공하는 기능을 제어할 수 있게 만든 인터페이스
인터페이스이기 때문에 구현 로직은 없고 사양만 정의되어 있음
사람 - 리모컨(API) - TV 관계를 생각하면 쉬움
구글 지도를 사용하려면 구글 지도를 사용하는 로직을 구현할 필요 없이 구글 지도 API로 요청해서 사용
실제로 어떻게 구현되어 동작하는지는 알 필요 없으며, 사양에 맞게 적절히 요청하면 됨
즉, 두 프로그램을 연결해주는 다리 역할
라이브러리와 API의 차이는 구현 로직의 유무

uri 를 통해 데이터를 받는 형태가 많음
구현과 독립적으로 사양(사용법)만 정의되어 있다
API에 따라 접근 권한이 필요할 수 있다.
ex) Kakao Map API, java API, 여러 기업들의 오픈 API
어떤 기능이 필요할 때 API를 찾아서 사용한다.


Library와 API 차이점은 구현 로직의 유뮤이다.
Library와 Framework의 차이점은 응용 프로그램의 흐름 주도권을 누가 가지고 있냐의 차이 → 누가 누구를 컨트롤 하는가


-----

다른 해설

Framework: 요리사인 '나'는 손님들의 입맛에 맘에 드는 음식을 만들기 위해 정해진 레시피대로 따라 만들어야한다.
주어진 재료와 레시피대로 요리를 해야하며 이것을 벗어나면 안되고, 이를 따르면 손님들이 보다 더 만족할만한 좋은 요리를 만들 수 있다.

Library: '나'는 의자를 만들기위해 망치,톱,못 등등 여러 공구를 가져다 놓고 만들기 시작했다.
이후 추가 공구를 더 가져올지는 내가 자유롭게 선택할 수 있다.

API: '나'는 올해 가구 배치를 하며 집을 꾸미기로 했다.
의자와 책상 같은 건 제작할 수 있었지만 침대,소파 같은 가구는 만들기엔 어렵다고 판단했다.
그래서 나는 주문제작을 하기로하고 내가 원하는 사이즈를 담은 주문내역을 작성하고 침대를 만드는 업체에 부탁을 했다.

-----

API와 라이브러리 차이 https://whwl.tistory.com/87

API / 라이브러리 / 프레임워크 차이 https://rlakuku-program.tistory.com/19

API / 라이브러리 / 프레임워크 차이 (또다른블로그)
https://doozi0316.tistory.com/entry/%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%ACFramework-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%ACLibrary-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8Plug-in-%EB%AA%A8%EB%93%88Module%EC%9D%98-%EC%B0%A8%EC%9D%B4

----------------------------------------------------------------------------------------------------

Function<T,R>

함수형 인터페이스


파라미터와 리턴타입이 각각 1개인 함수 생성 후

Function 생성
Function<파라미터자료형, 리턴자료형> 함수명 = 변수명 -> 변수명 * 10; // 구현할 기능

apply - 이용
함수명.apply(인수)

andThen - 연달아 이용
.andThen(다음에 실행할 함수).apply(인수)

compose - 함수 병합
Function<시작함수 파라미터자료형, 끝함수 리턴자료형> 함수명 = 끝함수명.compose(시작함수명);


ex) apply & andThen
Function<Integer,Integer> func1 = i -> i * i;
Function<Integer,String> func2 = s -> "result: " + s;
func1.apply(10); // func1 이용시
func1.andThen(func2).apply(10); // func1 이용해 나온값을 func2에 사용

ex) compose
Function<Integer, Double> add = n -> n + 2.0;
Function<Double, Double> multiply = n -> n * 5.0;
Function<Integer, Double> addAndMultiply = multiply.compose(add);
Double result = addAndMultiply.apply(1);
System.out.println(result);

----------------------------------------------------------------------------------------------------

클래스의 모든 필드명 가져오기

Field[] fields = 클래스(or객체).class.getFields();


필드 개수

Field[] fields = 클래스(or객체).class.getFields().length;

----------------------------------------------------------------------------------------------------

동적 setter

key의 첫글자를 대문자로 바꾼후 .getMethod() 이용

method =  domain.getClass().getMethod(
               "set" + newColumnName,
               new Class[] { String.class });

https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=joypheonix&logNo=100067619468

----------------------------------------------------------------------------------------------------

람다표현식 에서 증감변수 쓰는법 (automic / 배열)

int i = 0;
for (String s : list) {
	i++;
}
System.out.println(i);

↑ 동일한 코드 ↓

AtomicInteger i = new AtomicInteger();
list.forEach(item -> {
	i.getAndIncrement();
});
System.out.println(i.get());

초기값 지정은 생성자 파라미터에 int 넣으면 됨
값 대입은 set(int)로

↑ 동일한 코드 ↓

final int[] i3 = {0};
list.forEach(item -> {
	i3[0]++;
});
System.out.println(i3[0]);

----------------------------------------------------------------------------------------------------

instanceof

비교연산자중 하나로
좌변의 인스턴스가 우변의 클래스에 속하는지를 확인한다
instanceof연산의 결과가 true라는 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻함

public boolean m1(Object obj) {
if (obj instanceof AAA)
	return name.equalsIgnoreCase((AAA) obj);

이런식으로 자료형 형변환을 하기 전에 검사하기위해 주로 씀

----------------------------------------------------------------------------------------------------

정수를 heap에 집어넣는데 걸리는 시간 (heap size = 2048MiB)

1000만개
ArrayList 2~3초 (집어넣는시간 제외 출력하는데 걸리는 시간 2초)
LinkedList 5~6초 (집어넣는시간 제외 출력하는데 걸리는 시간 4초) (추가/수정/삭제할 일이 많을때 좋음)
HashSet 4~5초 (집어넣는시간 제외 출력하는데 걸리는 시간 4~7초) (순서 보장X, 내부적으로 HashMap을 이용)
TreeSet 6~7초 (집어넣는시간 제외 출력하는데 걸리는 시간 2초) (오름차순으로 데이터를 정렬, 내부적으로 TreeMap을 이용)
LinkedHashSet 3~4초 (집어넣는시간 제외 출력하는데 걸리는 시간 2~3초) (입력한 순서를 저장, 내부적으로 LinkedHashMap을 이용)

1억개
기본배열 137~234밀리초
ArrayList 41~46초
LinkedList OutOfMemoryError: GC overhead limit exceeded

715000000개
기본배열 1.7초
ArrayList OutOfMemoryError

10억개
OutOfMemoryError

----------------------------------------------------------------------------------------------------

json테스트데이터

{data:[
	{
		"ID":"b79e55f5-c751-43ba-90ec-96f7ccde20fa",
		"NAME":"아이유",
		"BIRTH":"930516",
		"HEIGHT":"162",
		"ADDRESS":"성남시 분당구 판교동"

		"CREATE_DATE":"2022-04-24 12:24:31"
	},
	{
		"ID":"79e670a0-00e3-431a-901b-4bdb57390f7e",
		"NAME":"한가인",
		"GENDER":"F",
		"BIRTH":"820202",
		"HEIGHT":"167",
		"WEIGHT":"48.1",
		"ADDRESS":"인천광역시 동구 송림동 42-215"
	},
	{
		"ID":"9ef3e81f-ef5c-4837-8769-dc4952d0a7c2",
		"NAME":"이열음",
		"GENDER":"F",
		"BIRTH":"960216",
		"HEIGHT":"165",
		"WEIGHT":"45.2",
		"ADDRESS":"서울특별시 중구 장충동1가 54-1"
	}
]}

----------------------------------------------------------------------------------------------------

this를 메소드 파라미터로 보내면

그 메소드에서 this클래스의 public 필드/메소드를 쓸 수 있음

----------------------------------------------------------------------------------------------------

자바 크롤링(Crawling)

자바 크롤링 라이브러리인 JSoup을 사용

https://jsoup.org/download


1. pom.xml에 의존성 추가
<dependency>
	<!-- jsoup HTML parser library @ https://jsoup.org/ -->
	<groupId>org.jsoup</groupId>
	<artifactId>jsoup</artifactId>
	<version>1.15.2</version>
</dependency>


2. 아래 코드로 URL에 해당하는 html소스를 가져올 수 있음
try {
	String URL = "https://www.mma.go.kr/hall/listsearch.do";
	Document doc = Jsoup.connect(URL).get();
	System.out.println(doc.text());    // HTML에서 텍스트만 불러옴 (자바스크립트 코드는 생략된다.)
	System.out.println(doc.html());    // HTML 자체를 가져옴
} catch (Exception e) {
	System.out.println("Run.main()");
	e.printStackTrace();
}


★아래와 같이 class로 가져올 수 있음
Elements imageUrlElements = doc.getElementsByClass("sp_list");
	for (Element element : imageUrlElements) {
	System.out.println(element);
}

★아래와 같이 id로 가져올 수 있음
Element areaListElement = doc.getElementById("areaList");
System.out.println(areaListElement);

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

쓰레드

 ★ 쓰레드

- 프로세스 내에서 실제로 작업을 수행하는 주체를 의미
- 모든 프로세스는 한개 이상의 쓰레드가 존재하여 작업을 수행함
- 두개 이상의 쓰레드를 가지는 프로그램을 멀티 쓰레드 프로세스라고 함

- 생성 방법은 두가지가 있음.
	1. Runnable 인터페이스를 구현하는 방법
	2. Thread 클래스를 상속받는 방법

두 방법 모두 쓰레드를 통해 작업하고 싶은 내용을 오버라이딩된 run()메소드 구현부에 작성하면 됨
★ Thread클래스를 상속받으면 다른 클래스를 상속받을 수 없기 때문에 Runnable인터페이스를 구현하는 방법을 주로 씀

쓰레드를 시작시키는 방법은
쓰레드객체.start() 메소드를 쓰면 됨
쓰레드객체.run() 메소드는 구현한걸 그냥 호출하는 거라서 싱글스레드로 동작함. (쓰레드를 쓰는 의미가 없음)

같은 쓰레드 객체는 동시에 실행됨

-----

ex1) Thread를 상속받아 구현

public class Run extends Thread{
	public void run() { //쓰레드를 상속하면 run 메소드를 구현하기
		System.out.println("Thread Run..");
	}

	public static void main(String[] agrs) {
		Run r = new Run();
		r.start();
	}
}

-----

ex2) Thread를 상속받아 쓰레드 실행 후 종료
public class Run extends Thread{
	int seq;

	public Run(int seq) {
		this.seq = seq;
	}

	public void run() {
		System.out.println(this.seq + "쓰레드 시작");
		try {
			Thread.sleep(1000); // 1초 대기함
		} catch (Exception e) {
		}
		System.out.println(this.seq + "쓰레드 종.료");
	}

	public static void main(String[] args) {
		for (int i = 0; i < 10; i++) { // 총 10개의 쓰레드를 생성하여 실행함
			Thread t = new Run(i);
			t.start();
		}
		System.out.println("메인 메소드 종료");
	}
}

-----

ex3) Thread를 상속받아 쓰레드 실행후, join메소드를 써서 메인메소드가 종료 된 후 종료

public class Run extends Thread{

	int seq;

	public Run(int seq) {
		this.seq = seq;
	}

	public void run() {
		System.out.println(this.seq + "쓰레드 시작");
		try {
			Thread.sleep(1000);
		} catch (Exception e) {
		}
		System.out.println(this.seq + "쓰레드 종료");
	}

	public static void main(String[] args) {

		ArrayList<Thread> threads = new ArrayList<>();

		for (int i = 0; i < 10; i++) {
			Thread t = new Run(i);
			t.start();
			threads.add(t);
		}

		for (int i = 0; i < threads.size(); i++) {
			Thread t = threads.get(i);
			try {
				t.join(); // 쓰레드가 종료될 때까지 기다림
			} catch (Exception e) {
			}
		}

		System.out.println("메인 메소드 종료");

	}
}

-----

ex4) Runnable 인터페이스를 구현해서 쓰레드 생성

public class Sample implements Runnable{

	int seq;

	public Sample(int seq) {
		this.seq = seq;
	}

	public void run() {
		System.out.println(this.seq + "쓰레드 시작");
		try {
			Thread.sleep(1000);
		} catch (Exception e) {
		}
		System.out.println(this.seq + "쓰레드 종료");
	}

	public static void main(String[] args) {

		ArrayList<Thread> threads = new ArrayList<>();

		for (int i = 0; i < 10; i++) {
			Thread t = new Thread(new Sample(i)); // 쓰레드의 생성자로 Runnable인터페이스를 구현한 객체를 넣을 수 있음
			t.start();
			threads.add(t);
		}

		for (int i = 0; i < threads.size(); i++) {
			Thread t = threads.get(i);
			try {
				t.join();
			} catch (Exception e) {
			}
		}

		System.out.println("메인 메소드 종료");

	}

}

-----

ex5) Runnable 인터페이스를 구현한 익명 객체로 쓰레드 생성

Thread t1 = new Thread(new Runnable() {
	@Override
	public void run() {
		try {
			Thread.sleep(1000);
			System.out.println("Thread 1 is completed.");
		} catch (Exception e) {
			System.out.println("Run.main()");
			e.printStackTrace();
		}
	}
});

-----

ex6) Runnable 인터페이스를 구현한 익명 객체로 쓰레드 생성 (람다식 사용)

Thread t1 = new Thread(() -> {
	try {
		Thread.sleep(1000);
		System.out.println("Thread 1 is completed.");
	} catch (Exception e) {
		System.out.println("Run.main()");
		e.printStackTrace();
	}
})

Thread t2 = new Thread(() -> {
	try {
		Thread.sleep(2000);
		System.out.println("Thread 2 is completed.");
	} catch (Exception e) {
		System.out.println("Run.main()");
		e.printStackTrace();
	}
})

t1.start();
t2.start();

System.out.println("주 스레드가 조인 없이 완료되었음")

try(try {
	t1.join(); // join메소드를 호출한 쓰레드에 t1이 끝날때까지 블록(대기)이 걸림
	t2.join(); // join메소드를 호출한 쓰레드에 t2가 끝날때까지 블록(대기)이 걸림
} catch (Exception e) {
	e.printStackTrace();
	System.out.println("Run.main()");
})

System.out.println("주 스레드가 조인을 사용하여 완료되었음")

-----

ex7) ExecutorService(스레드 풀을 관리하고 스레드를 사용해 작업을 할수있도록 지원하는 인터페이스) 를 사용해서 일괄처리 구현

public abstract class AbstractSimpleModule extends AbstractModule {
	final String[] MAPPER;
	public AbstractSimpleModule(String ... mapper){
		MAPPER = mapper;
	}
	@Override
	protected void beforeRun(JSONObject resultHeaderObject, JSONObject resultBodyObject) {

	}

	@Override
	protected void afterRun(JSONObject resultHeaderObject, JSONObject resultBodyObject) {

	}

	@Override
	public void run(JSONObject resultHeaderObject, JSONObject resultBodyObject) {
		try {
			int result = 0;
			Map<String, Object> param = parameterObject.toMap();
			param.put("usrId", super.getRequest().getSession().getAttribute("usrId").toString());

			ExecutorService executorService = Executors.newFixedThreadPool(MAPPER.length);

			List<Future<Integer>> futures = new ArrayList<>();

			for (String mapper : MAPPER) {
				Callable<Integer> task = () -> sqlSession.insert("kr.or.visitkorea.system." + mapper, param);
				futures.add(executorService.submit(task));
			}

			executorService.shutdown();
			executorService.awaitTermination(60, TimeUnit.SECONDS); // 모든 쓰레드의 작업이 완료되거나 제한 시간이 경과될때까지 여기서 대기

			for (Future<Integer> future : futures)
				result += future.get();

			if(result > 0) {
				resultHeaderObject.put("proces", "success");
				resultBodyObject.put("result", result);
			}else
				fail(resultHeaderObject);
		} catch(Exception e) {
			e.printStackTrace();
			fail(resultHeaderObject);
		}
	}

	private void fail(JSONObject obj) {
		obj.put("process", "fail");
	}
}

+++

ex) 트랜잭션 이용한 롤백처리(쓰레드중 하나라도 실패하면(오류가 발생해서 catch문에 걸리면) ROLLBACK)

public void run(JSONObject resultHeaderObject, JSONObject resultBodyObject) {
	try {
		Map<String, Object> param = parameterObject.toMap();
		ExecutorService executorService = Executors.newFixedThreadPool(MAPPER.length);
		List<Future<Integer>> futures = new ArrayList<>();
		int result = 0;

		param.put("usrId", super.getRequest().getSession().getAttribute("usrId").toString());
		sqlSession.getConnection().setAutoCommit(false);
		for (String mapper : MAPPER) {
			Callable<Integer> task = () -> sqlSession.insert("kr.or.visitkorea.system." + mapper, param);
			futures.add(executorService.submit(task));
		}
		executorService.shutdown();
		executorService.awaitTermination(60, TimeUnit.SECONDS);
		for (Future<Integer> future : futures)
			result += future.get();
		if(result > 0) {
			resultHeaderObject.put("proces", "success");
			resultBodyObject.put("result", result);
			sqlSession.getConnection().commit();
			sqlSession.getConnection().setAutoCommit(true);
		}else
			fail(resultHeaderObject);
	} catch(Exception e) {
		e.printStackTrace();
		try {
			sqlSession.getConnection().rollback();
			sqlSession.getConnection().setAutoCommit(true);
		} catch (SQLException ex) {
			ex.printStackTrace();
		}
		fail(resultHeaderObject);
	}
}

private void fail(JSONObject obj) {
	obj.put("process", "fail");
}

+++

ex) 쓰레드 안쓴경우 ( sqlSession.getConnection().setAutoCommit(false); 만 사용 )

public void run(JSONObject resultHeaderObject, JSONObject resultBodyObject) {
	try {
		List<Object> ids = parameterObject.getJSONArray("delList").toList();
		List<Object> imgIds = sqlSession.selectList("kr.or.visitkorea.system.SearchIndexMapper.selectRcmmKwrdImgId", ids);
		sqlSession.getConnection().setAutoCommit(false);
		int result = sqlSession.delete("kr.or.visitkorea.system.SearchIndexMapper.deletePplrTrvdtUnity", ids);
		sqlSession.delete("kr.or.visitkorea.system.SearchIndexMapper.deletePplrTrvdtUnityImg", imgIds);
		if(result > 0) {
			resultHeaderObject.put("proces", "success");
			sqlSession.getConnection().commit();
			sqlSession.getConnection().setAutoCommit(true);
		}else
			fail(resultHeaderObject);
	} catch (Exception e) {
		e.printStackTrace();
		fail(resultHeaderObject);
	}
}
private void fail(JSONObject obj) {
	try {
		sqlSession.getConnection().rollback();
		sqlSession.getConnection().setAutoCommit(true);
	} catch (SQLException ex) {
		throw new RuntimeException(ex);
	}
	obj.put("process", "fail");
}

----------------------------------------------------------------------------------------------------

쓰레드풀

쓰레드풀, 메모리풀, 캐쉬풀, 커넥션풀, 객체풀 (자바에서 객체풀은 사용을 지양합니다. 메모리를 할당하는 작업이 C/C++보다 빠름) 등등이 있습니다.
"풀"어서 말하면 미리 만들어두고 돌려막기로 사용하자 라고 볼 수 있는데요.
미리 만들어 두는 방식 / 쓰레드가 태스크를 처리하는 방식에 따라서 다양한 풀의 구현체들이 있을 수 있습니다.
이 글에서는 openJDK8 기준의 자바에서 구현된 newFixedThreadPool 를 해부해보도록 하겠습니다.  

쓰레드풀은 동일하고 서로 독립적인 다수의 작업을 실행 할 때 가장 효과적이다.
실행 시간이 오래 걸리는 작업과 금방 끝나는 작업을 섞어서 실행하도록 하면
풀의 크기가 굉장히 크지 않은 한 작업 실행을 방해하는 것과 비슷한 상황이 발생한다.
또한 크기게 제한되어 있는 쓰레드 풀에 다른 작업의 내용에 의존성을 갖고 있는 작업을 등록하면 데드락이 발생할 가능성이 높다.
다행스컯게도 일반적인 네트웍 기반의 서버 애플리케이션 (웹서버,메일서버,파일서버등)은 작업이 서로 동일하면서 독립적이어야 한다는 조건을 대부분 만족한다. 
-  Java concurrency in practice  책 발췌 전설의 개발자들이 참여한 저 엄청난 책은 자신들이 참여한 java.util.concurrent 패키지를 기준으로 한다.
근데 이 책이 2006년에 JDK1.5 기준으로 쓰여졌기 때문에 "동일하고 서로 독립적인 다수의 작업" 이라고 한정지었는데,
후에 JDK1.7에서 FORK-JOIN 풀이 나오면서 기존 풀들에서는 할 수 없었던 분할 수행작업을 효율적으로 할 수 있는 보완재가 되었다.

-----

ExecutorService 쓰는법 (자바 8 기준)

ex1) 쓰레드명 + 1~10 출력
ExecutorService executor = Executors.newFixedThreadPool(10);
IntStream.range(0, 10).forEach(n -> executor.execute(() -> {
	try {
		TimeUnit.MILLISECONDS.sleep(300);
		String threadName = Thread.currentThread().getName();
		System.out.println("hello " + threadName);
		System.out.println("num:" + n);

	} catch (Exception e) {
		System.out.println("Run.main()");
		e.printStackTrace();
	}
}));

ex2) 1~5 합계 출력
ExecutorService executor = Executors.newFixedThreadPool(2);
final List<Integer> integers = Arrays.asList(1, 2, 3, 4, 5);
Future<Integer> future = executor.submit(() -> {
	TimeUnit.MILLISECONDS.sleep(5000);
	int result = integers.stream().mapToInt(i -> i.intValue()).sum();
	return result;
});

try {
	Integer result = future.get();
	System.out.print("result: " + result);
	executor.shutdownNow();
} catch (InterruptedException e) {
	e.printStackTrace();
} catch (ExecutionException e) {
	e.printStackTrace();
}

//		쓰레드풀에 쓰레드를 10개를 뛰어놀게 한다.
//		쓰레드풀에 하나의 일을 시킨다. (쓰레드풀안의 쓰레드 하나가 선택되어 일처리를 할것이다)
//		submit메소드를 사용했다. 이 메소드는 future 를 리턴한다. 즉 일처리를 시키기고, 그에 따른 결과를 보고받을 것이다.
//		구현내용은 5000밀리초를 기다렸다가 리스트안의 숫자들의 합을 리턴한다.
//		리턴 받은 future 로 부터 값을 얻는다. 여기서 get()메소드는 블럭된다. (타임아웃을 매개변수로 넣을 수도 있다)
//		아마 일처리를 하는 쪽의 쓰레드에서 일을 다 끝내고 set() 같은 것을 해 줄 때가지 블럭될 것이다.

newFixedThreadPool메소드는 ThreadPoolExecutor 객체를 대신 만들어주고 있는데, 매개변수는 순서대로 다음과 같다

- corePoolSize : 풀 안에 유지되는 쓰레드 개수 (시작시)
- maximumPoolSize : 풀에 유지되는 최대 쓰레드 개수
- keepAliveTime : corePoolSize 보다 쓰레드 개수가 많아 질 때, 새로운 테스크를 기다리기 위한 시간. 시간이 지나면 쓰레드를 없애서 corePoolSize 를 유지한다.
- unit :  keepAliveTime 시간단위
- workQueue : 실행 되기전에 홀드시켜 두는 태스크를 유지하는 큐. 쓰레드가 남지 않을 경우 여기 태스크를 넣는다.

----------------------------------------------------------------------------------------------------

Thread 와 Runnable 차이


Thread를 상속받은 클래스
public class C1 extends Thread{

	public int num;

	@Override
	public void run(){
		try {
			Thread.sleep((int)(Math.random()*1000));
		} catch (InterruptedException e) {
			throw new RuntimeException(e);
		}
		System.out.println(num);
	}
}

public static void main(String[] args) {
	for (int i = 0; i < 10; i++) {
		C1 c1 = new C1();
		c1.num = i;
		c1.start();
	}
}


Runnable을 상속받은 클래스
public class C1 implements Runnable{

	public int num;

	@Override
	public void run(){
		try {
			Thread.sleep((int)(Math.random()*1000));
		} catch (InterruptedException e) {
			throw new RuntimeException(e);
		}
		System.out.println(num);
	}
}

public static void main(String[] args) {
	for (int i = 0; i < 10; i++) {
		C1 c1 = new C1();
		c1.num = i;
		Runnable runnable = c1;
		Thread t = new Thread(runnable);
		t.start();
	}
}


Thread를 상속받으면 start() 메소드를 쓸 수 있지만
Runnable을 상속받으면 start() 메소드가 없다

그래서 Runnable을 상속받은 클래스의 객체를
Runnable 로 받고, (이 과정은 생략 가능)
그 받은 Runnable 객체를 Thread의 생성자에 넣어서
Thread객체에 start메소드를 쓰면 됨

----------------------------------------------------------------------------------------------------

ExecutorService / Executors.newFixedThreadPool / Runnable / Callable / Future 쉽게 설명

ExecutorService 객체는 쓰레드들을 한번에 실행시키기 위해 사용됨. ExecutorService 객체에는 메소드가 있는데
execute(Runnable객체) 메소드는 실행만 시킬때 Runnable객체를 실행시키기 위해서 쓰는것이고
submit(Callable객체) 메소드는 메소드를 실행시킨후 결과를 Future객체로 반환받기위해 씀
	메소드를 실행하려면 Callable객체에 담아서 return받아야하는데 그 반환받은 Callable객체를 벗겨내기위해 submit메소드를 쓰는것이고,
	submit메소드를 Future객체를 만들어서 담지 않고 그냥 .get()으로 꺼낼 수도 있음
	ex) executor.submit(thread2()).get();
	Future의 .get()을 쓸때는 예외처리 필요
ExecutorService executor = Executors.newFixedThreadPool(n) 생성자메소드안에 쓰인 숫자만큼 executor객체의 메소드들을 한번에(동시에) 실행(병렬 처리)할 수 있음


public static void main(String[] args) {

	ExecutorService executor = Executors.newFixedThreadPool(2); // 2로 하면 아래 두개 쓰레드가 동시에 실행됨

	executor.submit(thread1());

	Future<List<Integer>> future = executor.submit(thread2());
	try {
		System.out.println(future.get());
	} catch (InterruptedException | ExecutionException e) {
		throw new RuntimeException(e);
	}

}

// Runnable은 실행만
static Runnable thread1(){
	return () -> {
		for (int i = 0; i < 5; i++) {
			try {
				Thread.sleep(500);
			} catch (Exception e) {
				System.out.println("Run.m1()");
				e.printStackTrace();
			}
			System.out.println(i);
		}
	};
}

// Callable은 값 반환이 필요할때
static Callable<List<Integer>> thread2(){
	return () -> {
		List<Integer> list = new ArrayList<>();
		for (int i = 0; i < 5; i++) {
			try {
				Thread.sleep(500);
			} catch (Exception e) {
				System.out.println("Run.m1()");
				e.printStackTrace();
			}
			list.add(i);
		}
		return list;
	};
}

------------------------------

익명 함수로도 쓸 수 있음

실행만(execute)

executor.execute(()->{
	for (int i = 0; i < 3; i++) {
		try {
			Thread.sleep(500);
		} catch (Exception e) {
			System.out.println("Run.m1()");
			e.printStackTrace();
		}
		System.out.println(i);
	}
});


반환값 있을때(submit)

Future<List<Integer>> future = executor.submit(() -> {
	List<Integer> list = new ArrayList<>();
	for (int i = 0; i < 5; i++) {
		try {
			Thread.sleep(500);
		} catch (InterruptedException e) {
			throw new RuntimeException(e);
		}
		list.add(i);
	}
	return list;
});

----------------------------------------------------------------------------------------------------

쓰레드 이름 확인법

Thread.currentThread().getName()

메인 쓰레드는 'main' 이라는 이름을 갖고
직접 생성한 쓰레드는 자동으로 'Thread-n' 이라는 이름으로 설정된다

thread.setName('쓰레드명') 메소드로 다른 이름으로 변경 가능

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

StringUtils

hasLength : 길이가 있으면 true 반환 공백(" ") 포함

hasText : 글자가 있으면 true 반환

----------------------------------------------------------------------------------------------------

AES256 암호화/복호화

Secret Key 가 “0123456789abcdefghij0123456789ab”일 때 encryptAES 메소드를 사용하면 평문 “Hello World!” 가 아래와 같이 AES256 암호화 됨

Secret Key는 원하는 32자리 문자열을 사용하면 되고 암호화할때의 Secret Key와 복호화할때의 Secret Key가 일치하기만 하면 됨

키의 길이가 32 이면 AES-256 이라 부르고, 키의 길이가 24 이면 AES-192, 키의 길이가 16 이면 AES-128 이라 부름


ex) AES256 으로 평문을 암호화하고, 암호화된 값을 평문으로 복호화하는 예제
참고로 Base64 는 org.apache.commons.codec.binary.Base64 패키지를 import 해야 한다.

1. dependency 추가
<!-- https://mvnrepository.com/artifact/commons-codec/commons-codec -->
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.9</version>
</dependency>

2. 내용은 아래와 같음
public static void main(String[] args) {
	AES256Util aesUtil = new AES256Util();

	String originText = "Hello World!";
	System.out.println("originText : " + originText);

	String encText = aesUtil.encryptAES("0123456789abcdefghij0123456789ab", originText, false);
	System.out.println("encText (encodeBase64) : " + encText);

	encText = aesUtil.encryptAES("0123456789abcdefghij0123456789ab", originText, true);
	System.out.println("encText (encodeBase64URLSafeString) : " + encText);

	String decText = aesUtil.decryptAES("0123456789abcdefghij0123456789ab", encText);
	System.out.println("decText : " + decText);
}

public String encryptAES(String keyString, String plainText, boolean bUrlSafe) {
	String cipherText = "";
	if ((keyString == null) || keyString.length() == 0 || (plainText == null) || plainText.length() == 0) {
		return cipherText;
	}

	// 키의 길이는 16, 24, 32 만 지원
	if ((keyString.length() != 16) && (keyString.length() != 24) && (keyString.length() != 32)) {
		return cipherText;
	}

	try {
		byte[] keyBytes = keyString.getBytes("UTF-8");
		byte[] plainTextBytes = plainText.getBytes("UTF-8");

		Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
		int bsize = cipher.getBlockSize();
		IvParameterSpec ivspec = new IvParameterSpec(Arrays.copyOfRange(keyBytes, 0, bsize));

		SecretKeySpec secureKey = new SecretKeySpec(keyBytes, "AES");
		cipher.init(Cipher.ENCRYPT_MODE, secureKey, ivspec);
		byte[] encrypted = cipher.doFinal(plainTextBytes);

		if (bUrlSafe) {
			cipherText = Base64.encodeBase64URLSafeString(encrypted);
		} else {
			cipherText = new String(Base64.encodeBase64(encrypted), "UTF-8");
		}

	} catch (Exception e) {
		cipherText = "";
		e.printStackTrace();
	}

	return cipherText;
}

public String decryptAES(String keyString, String cipherText) {
	String plainText = "";
	if ((keyString == null) || keyString.length() == 0 || (cipherText == null) || cipherText.length() == 0) {
		return plainText;
	}

	if ((keyString.length() != 16) && (keyString.length() != 24) && (keyString.length() != 32)) {
		return plainText;
	}

	try {
		byte[] keyBytes = keyString.getBytes("UTF-8");
		byte[] cipherTextBytes = Base64.decodeBase64(cipherText.getBytes("UTF-8"));

		Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
		int bsize = cipher.getBlockSize();
		IvParameterSpec ivspec = new IvParameterSpec(Arrays.copyOfRange(keyBytes, 0, bsize));

		SecretKeySpec secureKey = new SecretKeySpec(keyBytes, "AES");
		cipher.init(Cipher.DECRYPT_MODE, secureKey, ivspec);
		byte[] decrypted = cipher.doFinal(cipherTextBytes);

		plainText = new String(decrypted, "UTF-8");

	} catch (Exception e) {
		plainText = "";
		e.printStackTrace();
	}

	return plainText;
}

----------------------------------------------------------------------------------------------------

리플렉션(Reflection)

구체적인 클래스 타입을 알지 못해도 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API.
런타임에 지금 실행되고 있는 클래스를 가져와서 실행해야 하는 경우.
동적으로 객체를 생성하고 메소드를 호출할 수 있음
자바의 리플랙션은 클래스, 인터페이스, 메소드들을 찾을 수 있고, 객체를 생성하거나 변수를 변경하거나 메소드를 호출할 수 있다

-----

사용되는 상황

코드를 작성할 시점에는 어떤 타입의 클래스를 사용할지 모르지만, 런타임 시점에 지금 실행되고 있는 클래스를 가져와서 실행해야 하는경우.
ex) intelliJ의 자동완성 기능, 스프링의 어노터이션이 리플랙션을 이용한 기능임.

-----

사용법

class Person {
	String gender;
	int age;

	Person() {
		this.age = 27;
	}

	Person(int age) {
		this.age = age;
	}

	int getAge() {
		return this.age;
	}
}

★객체 생성(패키지명까지 쓰는 방식) &
★생성자 찾기
Class<?> clazz = null;
try {
	clazz = Class.forName("com.example.java_.reflection.t1.Person");
	Constructor<?> constructor = clazz.getDeclaredConstructor();

	System.out.println(constructor);

} catch (ClassNotFoundException | NoSuchMethodException e) {
	throw new RuntimeException(e);
}


★객체 생성(클래스명만 바로 쓰는 방식) &
★메소드 찾기 &
★메소드 실행
Class<Person> clazz2 = Person.class;
Method[] methodList = clazz2.getDeclaredMethods();
try {
	System.out.println(methodList[0].invoke(clazz2.newInstance())); // 27이 출력됨
} catch (IllegalAccessException | InvocationTargetException | InstantiationException e) {
	throw new RuntimeException(e);
}


★필드 불러오기 &
★필드값 변경
Field[] fields = clazz.getDeclaredFields();
System.out.println("field2: " + Arrays.toString(fields));
System.out.println("field2[0].getName(): " + fields[0].getName());

Person person = new Person();
try {
	fields[1].set(person, 17);
	System.out.println(fields[1].get(person));  // 17이 출력됨
	for (Field field1 : fields) {
		System.out.printf("%s: %s\r\n", field1.getName(), field1.get(person));
	}
} catch (IllegalAccessException e) {
	throw new RuntimeException(e);
}

-----

invoke() 의 첫번째 인수로는 실행할 메소드의 객체를 넣으면 되고,
두번째 인수로는 메소드에 들어갈 인수를 넣으면됨


invoke() 메소드는 3가지 예외를 발생시킨다

IllegalAccessException | InstantiationException | InvocationTargetException

이중에 InvocationTargetException은 예외 랩퍼 클래스인데, 이유는 null이 들어갈 수 있어서임
.getTargetException() 메소드로 확인이 가능함

----------------------------------------------------------------------------------------------------

1.1 + 0.1 == 1.2 가 false인 이유 → 데이터 세그먼트

이는 대부분의 프로그래밍 언어들이 마찬가지인데
float / double 등과 같은 실수 자료형은

메모리에 저장되는 방식이 있음.
방법은 먼저 bit를 32(4byte=float) or 64(8byte=double)개 만들어놓고
( 이때 float는 32bit중 부호비트 1자리 / 지수부 2~9자리 (8) / 가수부 10~32자리 (23)
	double은 64bit중 부호비트 1자리 / 지수부 2~12자리(11) / 가수부 13~64자리(52) )

ex) 5.125를 float으로 메모리에 채우는 원리
1. 첫번째 칸에 부호를 저장함 (양수는0 음수는1)
0xxxxxxxxx
xxxxxxxxxx
xx

2. 변환할 숫자를 2진법으로 변환 ex) 5.125 → 101.001
3. 부호(.)를 왼쪽으로 끝까지 이동(첫번째 수 뒤로) 1.01001
4. 부호가 이동했으니 이동한만큼 * 2^2 도 붙여줌
5. 소수점 좌측부분을 정수(significand)부, 우측 부분을 mantissa(가수)부이라고 함. 예시에서 exponent(지수)부는 왼쪽으로 2이동했으니 -2 가 됨
6. mantissa(가수)부를 남은 31칸중 뒤에서 23칸까지 차지시키고, 앞에서부터 채움 → 01001을 채움
0xxxxxxxx  .
. . . . . . . . . .
. . . . . . . . . .
. .
↓↓↓
0xxxxxxxx 0
1001. . . . . .
. . . . . . . . . .
. .

7. 지수부 2에 127을 더해서 129 → 2진수로 변환 → 10000001 8자리를 맨 앞에 채움
이때 127을 더하는 이유는 지수가 -127까지 나올 수 있어서 라고 함 (IEEE 부동소수점 규약)

8. 완성
0100000010
1001. . . . . .
. . . . . . . . . .
. .

9. 만약 가수부가 23칸을 벗어나면 짤림



위처럼 딱 떨어지는 실수면 괜찮은데 순환소수가 발생할경우 오차가 생김

무한한 수를 저장할 수 있는 저장공간은 없으므로 자리수를 벗어난 나머지 숫자들은 짤리게 됨

때문에 오차가 생기니 돈계산 할떄는 무조건 정수로 해야함.
5.1 달러 이런식으로 소수가 나올때는 일부러 100을 곱해서 510센트 이런식으로 해야함


overflow현상 / Not a Number / Infinity
모두 같은 원리


해결책
1. 정수를 쓴다
2. 반올림을 쓴다
3. 소수를 좀 더 정확하게 저장할 수 있는 double을 씀 (단점 : 메모리 용량 2배 필요)
4. 부동소수점 계산을 근사치로 하기 때문에 if문으로 비교할때는 == 말고 >= 등 범위로 비교한다

----------------------------------------------------------------------------------------------------

로그 레벨 낮은 순서 (라이브러리마다 다름)

ALL - TRACE - DEBUG - INFO - WARN - ERROR - FATAL - OFF

INFO로 세팅하면 WARN, ERROR, FATAL 는 기록됨


TRACE : 디버그 레벨이 너무 광범위한 것을 해결하기 위한 좀 더 상세한 이벤트

DEBUG : 개발시 디버그 용도로 사용하는 메시지

INFO : 어떠한 상태 변경과 같은 정보성 메시지

WARN : 프로그램의 실행에는 문제가 없지만, 향후 시스템 에러의 원인이 될 수 있는 경고성 메시지

WARN에서도 2가지의 부분에선 종료가 일어남

명확한 문제 : 현재 데이터를 사용 불가, 캐시값 사용 등
잠재적 문제 : 개발 모드로 프로그램 시작, 관리자 콘솔 비밀번호가 보호되지 않고 접속 등


ERROR : 어떠한 요청을 처리하는 중 문제가 발생한 상태.
프로그램 동작에 큰 문제가 발생했다는 것으로 즉시 문제를 조사해야 하는 것 (DB를 사용할 수 없는 상태, 중요 에러가 나오는 상황)

FATAL : 아주 심각한 에러가 발생한 상태

------------------------------

log4j & slf4j

<root level="info">
	<appender-ref ref="CONSOLE" /> <!-- 콘솔에 출력 -->
	<appender-ref ref="FILE" /> <!-- 파일에 출력 -->
</root>

----------------------------------------------------------------------------------------------------

copyProperties

스프링 전역메소드로, 원본 클래스와 복사대상 클래스간의 일치하는 필드 내에서 값이 그대로 복사됨

원본 클래스에 getter, 붙여넣을 클래스에 setter 필요


쓰는법

copyProperties([원본 객체], [복사후 객체])

ex)
@ToString
@Getter
@AllArgsConstructor
public class Human {
	String name;
	int age;
	float weight;
}
@ToString
@Setter
public class Clone {
	String name;
	int age;
}
public class Run {
	public static void main(String[] args) {
		Human human = new Human("asd",12,132.4f);

		Clone clone = new Clone();
		copyProperties(human,clone);

		System.out.println(human); // Human(name=asd, age=12, weight=132.4)
		System.out.println(clone); // Clone(name=asd, age=12)
	}
}

-----

클래스 내부에서 자신객체을 다른 클래스의 객체로 변환도 가능(마찬가지로 원본 클래스에 getter, 붙여넣을 클래스에 setter 필요)

@ToString
@Getter
@AllArgsConstructor
public class Human{
	String name;
	int age;
	float weight;

	public Clone doClone(){
		Clone clone = new Clone();
		copyProperties(this,clone);
		return clone;
	}

}

----------------------------------------------------------------------------------------------------

내부클래스 (inner class)

클래스 내에 또 클래스가 있는것.
두 클래스가 서로 긴밀한 관계가 있을때 씀.
내부 클래스에서 외부클래스의 멤버들을 쉽게 접근할 수 있어 코드의 복잡성 감소

★한눈에 자원 상관 관계 파악에 도움됨


메소드는 기본이 private이고, static으로 하면 기본이 public임 (클래스도 static으로 하기)
public static 로 만들면 다른 클래스에서도 C1.C2 이런식으로 쓸 수 있음
private static 로 만들면 C1에서 C1.C2 이렇게 쓸 수 있음

public class C1{
	private class C2{
	}
}

내부(inner) 클래스는 중첩(nested) 클래스로 분류되기도 한다.

------------------------------

내부클래스에서 바깥클래스의 필드/메소드 참조

바깥클래스.this.필드
바깥클래스.this.메소드()

클래스/필드/메소드가 static이 아닐때 쓰기

----------------------------------------------------------------------------------------------------

HTTP 요청 보내기

InputStram

URL클래스를 이용해
서버에서 데이터를 읽어올 수 있음 (http요청)

------------------------------

방법1. url객체.openStream() 으로 바로 받기

url만 가지고 InputStreamReader에 스트림을 보내서 처리한다
이런방식은 심플하지만, 커넥션의 문제 등이 발생할수 있고 여러가지 추가설정을 할 수 없기때문에 잘 쓰이지 않는 방식이다


URL url = new URL("https://ctgs.ktovisitkorea.com/api/visitkorea/lc01/7601e8b78aed45ec852059cc5b766947/api.do");
BufferedReader in = new BufferedReader(new InputStreamReader(url.openStream(), "UTF8"));
String inputLine;
while ((inputLine = in.readLine()) != null)
	System.out.println(inputLine);
in.close();

------------------------------

방법2. HttpURLConnection 이용

POST 방식도 사용가능
Timeout 설정, UserAgent 설정들이 사용가능해 보다 사용자가 원하는대로 구현할 수 있게 해줌

openConnection() 메소드는 실제 네트워크 연결을 설정하지 않고, 단지 URLConnection클래스의 인스턴스를 반환한다.
네트워크 연결은 connect() 메소드를 호출할때 명시적으로 이루어지거나,
헤더 필드를 읽거나, 입력스트림/출력스트림을 가져올때 암시적으로 이루어진다

URL의 openConnection() 메소드는 I/O오류가 발생하면 IOException을 발생시킨다


StringBuilder urlBuilder = new StringBuilder("http://api.data.go.kr/openapi/tn_pubr_prkplce_info_api"); /* URL */
urlBuilder.append("?" + URLEncoder.encode("serviceKey", "UTF-8") + "=elZJClL%2BcPyzL%2FwCk5Z3AtxWcAm6m%2FHITT9Uo8kvMuX6OEvsLeT9qBgSYFR1wpSVWM%2FQrzoItQZlAWU%2Fh1x5LA%3D%3D"); /* Service Key */
urlBuilder.append("&" + URLEncoder.encode("pageNo", "UTF-8") + "=" + URLEncoder.encode("1", "UTF-8")); /* 페이지 번호 */
urlBuilder.append("&" + URLEncoder.encode("numOfRows", "UTF-8") + "=" + URLEncoder.encode("100", "UTF-8")); /* 한 페이지 결과 수 */
urlBuilder.append("&" + URLEncoder.encode("type", "UTF-8") + "=" + URLEncoder.encode("json", "UTF-8")); /* XML/JSON 여부 */

URL url = new URL(urlBuilder.toString());
HttpURLConnection conn = (HttpURLConnection) url.openConnection();
conn.setRequestMethod("POST");
conn.setRequestProperty("Content-type", "application/json");
//conn.setReadTimeout(1000); // 타임아웃
//conn.setDoOutput(true); // 데이터 기록 알려주기
System.out.println("Response code: " + conn.getResponseCode());
BufferedReader rd;
if (conn.getResponseCode() >= 200 && conn.getResponseCode() <= 300)
	rd = new BufferedReader(new InputStreamReader(conn.getInputStream()));
else
	rd = new BufferedReader(new InputStreamReader(conn.getErrorStream()));
StringBuilder sb = new StringBuilder();
String line;
while ((line = rd.readLine()) != null)
	sb.append(line);
rd.close();
conn.disconnect();
System.out.println(sb);


참고
https://blueyikim.tistory.com/2199

----------------------------------------------------------------------------------------------------

Comparable 과 Comparator

Comparable는 자기 자신과 , 파라미터로 들어오는 객체를 비교하는것
Comparator는 자신의 상태가 어떻던 상관없이 두 파라미터의 객체를 비교하는것

비교한다는 것 자체는 같지만, 비교 대상이 다르다는 것이다.

또 다른 차이점이라면 Comparable은 lang패키지에 있기 때문에 import 를 해줄 필요가 없지만, Comparator는 util패키지에 있다.


Comparable 인터페이스는 객체를 정렬하는데 사용되는 메소드인 compareTo() 메소드를 정의하고 있음
자바에서 같은 타입의 인스턴스를 서로 비교해야만 하는 클래스들은 모두 Comparable 인터페이스를 구현하고 있음
Boolean을 제외한 래퍼 클래스나 String, Time, Date같은 클래스의 인스턴스는 모두 정렬 가능
기본 정렬순서는 오름차순 정렬

----------------------------------------------------------------------------------------------------

자바 동적변수가 안되는 이유

변수명은 컴파일시 컴파일러에게 알려져야 하는데
X라는 변수명은 실행시에 결정되기 떄문에
앞단에 있는 과정이 뒷단에서 결정되는 사항을 알 수 없음

동적으로 쓰고싶으면 Map을 활용해서 처리 해야함

----------------------------------------------------------------------------------------------------

Short Circuit Evaluation
: 논리 연산자 중 and 와 or 연산자는 이미 결과가 확정되면 뒤 문장을 검사 하지않음


&&, || : 결과가 확정되면 검사 안함

int a = 0;
int b = 0;
if(a++ > 10 && b++ > 10);
System.out.printf("%d %d\r\n", a, b); // 1 0
a = 0;
if(a++ > 10 & b++ > 10);
System.out.printf("%d %d\r\n", a, b); // 1 1


&, | : 결과 확정과 상관없이 검사 함 (비트연산자와 기호만 똑같고 쓰임이 다름)

int a = 0;
int b = 0;
if(a++ < 10 || b++ < 10);
System.out.printf("%d %d\r\n", a, b);
a = 0;
b = 0;
if(a++ < 10 & b++ < 10);
System.out.printf("%d %d\r\n", a, b);

----------------------------------------------------------------------------------------------------

프로젝트를 maven → gradle로 변경

1. 그래들 설치
gradle install gradle

2. 프로젝트 폴더로 이동후 아래 명령어 입력
gradle init

3. 인텔리제이에서 Load Gradle Project 클릭

4. build.gradle에서 아래코드 추가
plugins {
	id 'war'
추가 안하면 아래와같은 오류 남
A problem occurred evaluating root project 'spring-boot-project'.
> Could not find method providedCompile() for arguments [org.springframework.boot:spring-boot-starter-tomcat:2.6.4] on object of type org.gradle.api.internal.artifacts.dsl.dependencies.DefaultDependencyHandler.

5. builde.gradle에서
implementation 'org.projectlombok:lombok:1.18.22' 아래에
annotationProcessor 'org.projectlombok:lombok:1.18.22' 추가
추가 안하면 롬복에서 오류남

6. pom.xml 삭제


gradle → maven으로 바꾸려고
gradle.build를 삭제했는데도 gradle메뉴가 안없어지고, 실행했는데 이거 뜨면
Directory '~~~' does not contain a Gradle build.
해당프로젝트폴더에 있는 .idea 디렉토리 삭제하면 됨

----------------------------------------------------------------------------------------------------

최대 공약수 (유클리드 호제법)

while문
int gcd(int a, int b){
	while(b != 0){
		int r = a % b;
		a = b;
		b = r;
	}
	return a;
}

재귀함수
int gcd(int a, int b){
	return a % b == 0 ? b : gcd(b, a % b);
}

------------------------------

최소 공배수 (최대 공약수 이용)

a * b / a와 b의 최대공약수

int lcm(int a, int b)
	return a*b / gcd(a,b);
}

a, b는 0이면 안됨

------------------------------

소인수 분해

public Set<Integer> factor(int b){
	Set<Integer> set = new LinkedHashSet<>();
	int n = 2;
	while(n <= b)
		if(b % n == 0){
			set.add(n);
			b /= n;
		}else
			n++;
	return set;
}

------------------------------

소수 판별

public static boolean isPrime(int num){
	for(int i = 2; i * i <= num; i++)
		if(num % i == 0) return false;
	return true;
}

------------------------------

주어진 수까지 모든 소수 구하기(에라토스테네스의 체 이용)

int number = 100; // 구하고자 하는 소수의 범위
int[] primeNum = new int[number + 1];

// primeNum 배열 초기화
for (int i = 2; i <= number; i++)
	primeNum[i] = i;

for (int i = 2; i <= Math.sqrt(number); i++){
	// primeNum[i] 가 0이면 이미 소수가 아니므로 continue
	if (primeNum[i] == 0)
		continue;
	// i*k (k<i) 까지의 수는 이미 검사했으므로 j는 i*i 부터 검사해준다.
	for (int j = i * i; j <= number; j += i)
		primeNum[j] = 0;
}

System.out.println(Arrays.toString(primeNum));

----------------------------------------------------------------------------------------------------

숫자 판단 메소드

Character.isDigit('ㅇ') → 문자가 숫자일경우 true

----------------------------------------------------------------------------------------------------

InputStream / InputStreamReader / BufferedReader

Byte Type = InputStream
Char Type = InputStreamReader
Char Type 의 직렬화 = BufferedReader
(String 도 따지고 보면 char의 배열 형태이니.. 직렬화라는 말이 어렵다면 String이라고 봐도 큰 문제는 없을 것 같다.)

----------------------------------------------------------------------------------------------------

인텔리제이 자바버전 확인법

preferences → 빌드, 실행, 배포 → Java 컴파일러

or

cmd + ; (프로젝트 구조) → 프로젝트 설정 → 프로젝트

----------------------------------------------------------------------------------------------------

CLI로 컴파일 하는법 (.class파일을 생성하는법)

javac 명령어를 이용

cd 로 해당 프로젝트로 이동 후
javac 클래스경로/클래스명.java


com/example/java_/class_/constructor/t2/ 안에
Run / Parent / Child 이렇게 클래스들이 있고, Run파일에서 Parent, Child 클래스를 쓴다고 가정했을때
-cp옵션을 안쓸경우 각각의 파일들을 모두 적어야함 (안그러면 클래스를 찾을 수 없다고 cannot find symbol 오류남)

javac src/main/java/com/example/java_/class_/constructor/t2/Child.java src/main/java/com/example/java_/class_/constructor/t2/Run.java src/main/java/com/example/java_/class_/constructor/t2/Parent.java


이때 cp옵션을 이용하면 필요한 클래스들을 별도로 안적어도 됨
javac -cp src/main/java src/main/java/com/example/java_/class_/constructor/t2/Run.java


그럼 각각의 .java파일이 있는 각각의 경로에 .class파일이 생성됨


-d 옵션을 이용해 .class파일이 생성될 디렉터리를 지정가능

javac -d asdf src/main/java/com/example/java_/class_/constructor/t2/Child.java src/main/java/com/example/java_/class_/constructor/t2/Run.java src/main/java/com/example/java_/class_/constructor/t2/Parent.java

현재 폴더의 asdf폴더 안에 com/example~~ 폴더가 만들어지고 그 안에 .class들이 생김

------------------------------

컴파일된 .class파일 실행하는법

java 명령어를 이용

실행할 클래스이름을 .으로 구분하고, .class 확장자를 붙이지 않음

ex)
java -cp src/main/java com.example.java_.class_.constructor.t2.Run

cd src/main/java 한다음 java com.example.java_.class_.constructor.t2.Run 이렇게 해도 됨
근데 java src.main.java.com.example.java_.class_.constructor.t2.Run 는 안됨

이유는 src/main/java 까지는 디렉토리이기는 하지만, 패키지가 아니기 때문 (자바소스에서 package 키워드 이후에 나오는게 패키지임)

-cp옵션으로는 패키지가 정의된 디렉토리의 경로를 지정해야함

----------------------------------------------------------------------------------------------------

import문 선언시

import 패키지명.*;

이렇게 쓰면

컴파일러는 해당 패키지에서 일치하는 클래스명을 찾아야 하는 수고를 더 해야 할 것이다. 단지 그 뿐이다

실행 시 성능상의 차이는 전혀 없다


클래스 이름 대신 * 를 사용하는 것이 하위 패키지의 클래스까지 포함하는 것은 아니다

import java.util.*;
import java.text.*;

위 두문장을

import java.*

이렇게 쓸 수는 없음

----------------------------------------------------------------------------------------------------

static import문

import문을 사용하면 클래스의 패키지명을 생략할 수 있는 것과 같이
static import문을 사용하면 static멤버를 호출할 때 클래스 이름을 생략할 수 있음


import static java.lang.Integer.*; // Integer클래스의 모든 static메서드
import static java.lang.Math.random; // Math.random()만. ★괄호 안붙임
import static java.lang.System.out; // System.out을 out만으로 참조 가능

System.out.println(Math.random());
↓
out.println(random());

----------------------------------------------------------------------------------------------------

slf4j 사용법


1. slf4j 라이브러리 추가
<dependencies>
	<dependency>
		<groupId>org.slf4j</groupId>
		<artifactId>slf4j-api</artifactId>
		<version>1.7.30</version>
	</dependency>
</dependencies>


2. 로깅 코드 작성
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MyClass {
	private static final Logger logger = LoggerFactory.getLogger(MyClass.class);

	public void myMethod() {
		logger.info("This is an info log message.");
		logger.warn("This is a warning log message.");
		logger.error("This is an error log message.", new Exception("Something went wrong!"));
		logger.debug("asd: {}", 변수);
	}
}

3. 로깅 시스템 설정
마지막으로 로깅 시스템을 설정한다. slf4j는 자체적으로 로그를 출력하지 않음
대신, 다른 로깅 시스템 (log4j, java.util.logging 등)을 사용함
따라서, 로깅 시스템의 설정에 따라 로그가 출력됨. 로깅 시스템의 설정은 해당 시스템의 문서를 참조하여 설정할 수 있음
위의 간단한 예제는 slf4j의 기본 사용법을 보여줌. 더 많은 기능과 옵션에 대해서는 slf4j 문서를 참조

----------------------------------------------------------------------------------------------------

모든 세션 키/값 조회

HttpSession session = request.getSession(); // 세션 객체 가져오기

Enumeration<String> attributeNames = session.getAttributeNames(); // 모든 세션 속성 이름 가져오기

while (attributeNames.hasMoreElements()) { // 모든 세션 속성에 대해 반복
    String attributeName = attributeNames.nextElement();
    Object attributeValue = session.getAttribute(attributeName);
    System.out.println(attributeName + " = " + attributeValue); // 각 세션 속성 이름과 값을 출력
}

----------------------------------------------------------------------------------------------------

한글 깨질때

String fileName = "abc가나다ㄹ.xlsx";

try {
	fileName = URLEncoder.encode(fileName, "UTF-8");
} catch (UnsupportedEncodingException e) {
	throw new RuntimeException(e);
}

----------------------------------------------------------------------------------------------------

중첩 if문 작성시

바깥쪽 if에 else를 써야하는 경우 바깥쪽 true절을 블럭으로 만들어야함 (안그러면 당연히 안쪽 if문에 else가 걸림)

if(firstMenuArray.get(i).isObject().get("permission") instanceof JSONObject)
	if (!"7ed72c3b-5ad9-4859-b33d-3d8d150bfabf".equals(firstMenuArray.get(i).isObject().get("permission").isObject().get("uuid").isString().stringValue()))
		filteredArray.set(i, firstMenuArray.get(i));
else
	filteredArray.set(i, firstMenuArray.get(i));

↓↓↓

if(firstMenuArray.get(i).isObject().get("permission") instanceof JSONObject) {
	if (!"7ed72c3b-5ad9-4859-b33d-3d8d150bfabf".equals(firstMenuArray.get(i).isObject().get("permission").isObject().get("uuid").isString().stringValue()))
		filteredArray.set(i, firstMenuArray.get(i));
}else
	filteredArray.set(i, firstMenuArray.get(i));

----------------------------------------------------------------------------------------------------

스레드간의 데이터 경합상태(race condition)

여러 스레드가 공유된 데이터에 동시에 접근하고 변경하는 상황에서 발생할 수 있는 문제

시나리오
스레드 A가 count 값을 읽습니다. → 0
스레드 B가 count 값을 읽습니다. → 0
스레드 A가 count 값을 증가시키고 저장합니다. → 1
스레드 B가 count 값을 감소시키고 저장합니다. → -1

경합 조건은 스레드 동기화를 통해 방지해야 함
스레드 동기화는 임계 영역을 설정하거나 동기화 메커니즘을 사용하여 여러 스레드의 접근을 순차화하여 데이터 일관성을 보장함


스프링 컨트롤러에서도 스레드 경합(race condition) 상황이 발생할 수 있음
스프링 컨트롤러는 여러 클라이언트의 요청을 동시에 처리하기 위해 여러 스레드를 사용함
따라서 여러 스레드가 동시에 같은 데이터나 리소스에 접근할 수 있으며, 이로 인해 경합 상황이 발생할 수 있음

스프링 컨트롤러에서 스레드 경합이 발생하는 일반적인 상황은 다음과 같음
1. 여러 클라이언트가 동시에 같은 리소스를 변경하는 요청을 보냅니다.
2. 요청을 처리하는 스레드들이 동시에 해당 리소스에 접근하고 변경 작업을 수행합니다.
3. 동시에 변경 작업을 수행하려는 스레드들 사이에서 경합 상황이 발생할 수 있으며, 이로 인해 일관성이 없는 결과가 발생할 수 있습니다.

예를 들어, 여러 클라이언트가 같은 계좌에서 동시에 출금 요청을 보내는 경우를 생각해본다
스프링 컨트롤러는 각 요청을 처리하는 스레드를 생성하여 해당 계좌의 잔액을 확인하고 출금 작업을 수행함
여러 스레드가 동시에 잔액을 확인하고 출금 작업을 수행하려고 할 때
잘못된 잔액 계산이나 출금 금액이 중복으로 감소하는 등의 경합 상황이 발생할 수 있음

이러한 경우에도 적절한 동기화 메커니즘을 사용하여 경합 상황을 방지할 수 있음

스프링 프레임워크에서는 synchronized 키워드 외에도 Lock 인터페이스를 활용한 동기화, synchronized 메서드, synchronized 블록 등 다양한 동기화 방법을 제공함
이를 통해 스레드 경합 상황을 해결하고 데이터의 일관성과 안전한 접근을 보장할 수 있음

----------------------------------------------------------------------------------------------------

각기 다른 조건을 비교할때

if(val.containsKey("LMMT_CNT"))
	~~~
if(isDdln)
	~~~

이렇게 쓰는 경우가 있고

if(val.containsKey("LMMT_CNT"))
	~~~
else if(isDdln)
	~~~

이렇게 하나의 if문으로 쓰는 경우가 있는데

하나의 if문으로 쓰면 첫 조건이 true이면 다음 조건은 실행하지 않는다. 주의 (그냥 if문을 2개 쓰는게 좋음)

----------------------------------------------------------------------------------------------------

(getRequest() == null ? req : getRequest()).getSession()

를 간단하게 표현 가능

Optional.ofNullable(getRequest()).orElse(req).getSession()

----------------------------------------------------------------------------------------------------

익명함수내에서 현재클래스를 참조하고싶으면

this가 아니라 현재클래스명.this를 써야함

ex)
new HashMap<String, Object>(){{
	put("parent", RandomBoxStockTable.this);
}}

----------------------------------------------------------------------------------------------------

맵에 entrySet() 사용시

제네릭 붙여야 getKey, getValue를 쓸 수 있음
ex. Map<String, Object>

Map<KeyType, ValueType> map = ...; // Map 객체를 초기화하거나 얻어온다.

map.entrySet().forEach(entry -> {
	KeyType key = entry.getKey();
	ValueType value = entry.getValue();
});

----------------------------------------------------------------------------------------------------

엑셀업로드(아파치 POI) 할때 문자로 읽고싶은데 숫자로 읽혀서 지수 표기법으로 나올때 셀 내용을 문자열로 읽게 하기

public void run(JSONObject resultHeaderObject, JSONObject resultBodyObject) {
	try {
		String fileName = this.getFileName();
		String filePath = this.getFilePath();
		String saveName = this.getsaveName();
		String uuid = UUID.randomUUID().toString();
		XSSFSheet sheet = this.getWorkSheet(uuid, fileName, filePath);
		JSONArray rowArray = new JSONArray();

		if (sheet == null) {
			resultHeaderObject.put("process", "fail");
			resultHeaderObject.put("ment", "엑셀 워크시트를 찾을 수 없습니다.");
			return;
		}

//			DataFormatter dataFormatter = new DataFormatter();

		for (int i = sheet.getFirstRowNum(); ; i++) {
			XSSFRow row = sheet.getRow(i);
			JSONArray cellArray = new JSONArray();
			if (row == null)
				break;
			for (int j = row.getFirstCellNum(); ; j++) {
				XSSFCell cell = row.getCell(j);
				if (cell == null)
					break;
				String value = getValue(cell);
				cellArray.put(value);
			}
			rowArray.put(cellArray);
		}
		if (rowArray.length() == 0) {
			resultHeaderObject.put("process", "fail");
			resultHeaderObject.put("ment", "오류가 발생했습니다. 관리자에게 문의해주세요");
		} else {
			resultBodyObject.put("process", "success");
			resultBodyObject.put("resultArr", rowArray);
		}
	} catch (Exception e) {
		e.printStackTrace();
	}
}

public static String getValue(XSSFCell cell){
	NumberFormat f = NumberFormat.getInstance();
	f.setGroupingUsed(false); // 세자리콤마 해제
	String value = "";
	if (cell != null) {
		//타입 체크
		switch (cell.getCellType()) {
			case FORMULA:
				value = cell.getCellFormula();
				break;
			case STRING:
				value = cell.getStringCellValue();
				break;
			case NUMERIC:
				value = f.format(cell.getNumericCellValue()); // 지수로 안나오게 설정
				break;
			case BOOLEAN:
				value = String.valueOf(cell.getBooleanCellValue());
				break;
			case ERROR:
				value = String.valueOf(cell.getErrorCellValue());
				break;
			case BLANK:
			default: value = "";
		}
	}
	return value;
}


만약 그냥 숫자를 문자열로 받아오려고 한 경우 아래와 같은 오류가 남 (숫자셀을 문자열로 바꿀수 없다는 뜻)
java.lang.IllegalStateException: Cannot get a STRING value from a NUMERIC cell

----------------------------------------------------------------------------------------------------

xml 파일의 내용을 읽어오기

ClassLoader classLoader = Call.class.getClassLoader();
SAXBuilder builder = new SAXBuilder();

try {
	
	bizDocument = builder.build(new File(classLoader.getResource("kr/or/visitkorea/admin/server/application/BusinessMapping.xml").getFile()));
	
	sysProps = new Properties();
	InputStream inputStream = classLoader.getResource("kr/or/visitkorea/admin/server/application/system.properties").openStream();
	sysProps.load(inputStream);

} catch (JDOMException e ) {
	e.printStackTrace();
} catch ( IOException e) { 
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

"null" 이 반환될때

null 을 특정 클래스로 형변환을 하고, 그걸 String.valueOf() 로 감싼 경우 "null"이 반환됨

String.valueOf((C1) null).equals("null") → true

----------------------------------------------------------------------------------------------------

현재 메소드명 가져오기

public TermsHistogramResponse searchLatest(String indexName, TermsHistogramRequest req) throws Exception {
	String methodName = new Object(){}.getClass().getEnclosingMethod().getName();
}

현재 메소드명인 "searchLatest" 를 반환함

----------------------------------------------------------------------------------------------------

구현체가 딱 하나일때는 클래스명뒤에 Impl을 붙이는게 관례

ex) MemberService인터페이스를 구현한 구현체클래스가 1개일 경우 MemberServiceImpl 라는 이름으로 씀

public class MemberServiceImpl implements MemberService{

----------------------------------------------------------------------------------------------------

어노테이션들을 조합해서 어노테이션 만들기

@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Operation(summary = "User list")
@ApiResponses({
		@ApiResponse(responseCode = "200", description = "OK", content = @Content(
				mediaType = "application/json",
				examples = @ExampleObject(value = "{'error': '200 OK', 'message': ''}")
		)),
		@ApiResponse(responseCode = "204", description = "NO CONTENT", content = @Content(
				mediaType = "application/json",
				examples = @ExampleObject(value = "{'error': '204 NO CONTENT', 'message': '결과가 존재하지 않습니다.'}")
		)),
		@ApiResponse(responseCode = "400", description = "BAD REQUEST", content = @Content(
				mediaType = "application/json",
				examples = @ExampleObject(value = "{'error': '400 Bad Request', 'message': '잘못된 요청입니다.'}")
		)),
		@ApiResponse(responseCode = "404", description = "NOT FOUND", content = @Content(
				mediaType = "application/json",
				examples = @ExampleObject(value = "{'error': '404 Not Found', 'message': '요청한 리소스를 찾을 수 없습니다.'}")
		)),
		@ApiResponse(responseCode = "500", description = "INTERNAL SERVER ERROR", content = @Content(
				mediaType = "application/json",
				examples = @ExampleObject(value = "{'error': '500 Internal Server Error', 'message': '서버에서 오류가 발생했습니다.'}")
		))
})
public @interface SwaggerAnnotation {
	@AliasFor(annotation = Operation.class, attribute = "description")
	String title() default "";
	String summary() default "";
}


설명

@AliasFor을 이용하면 다른 애노테이션의 description값은 유지한 채, @Operation 의 description 속성만 파라미터값으로 넣을 수 있음

default 연산자를 이용하면 애노테이션을 사용하는쪽에서 속성을 필수로 안넣어도 되게끔 할 수 있음

참고로 summary는 @Operation의 속성임

----------------------------------------------------------------------------------------------------

FeignClient (페인 클라이언트)

HTTP 요청을 인터페이스로 쉽게 할수있게 해주는 라이브러리

Request Body json 데이터를 파라미터DTO로 보내면 됨

Java애플리케이션에서 원격 HTTP서비스에 대한 HTTP 요청을 보내고 응답을 처리하는데 사용됨

스프링 안에 기본적으로 포함되어있음

----------------------------------------------------------------------------------------------------