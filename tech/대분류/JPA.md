JPA 어노테이션

@Entity : 클래스를 엔티티로 만듦

@Id : 필드를 PK로 인식시킴

@Table : 테이블 제어

@Column : 컬럼 제어 / ddl 생성기능

@GeneratedValue : 순차적인 값을 자동으로 할당(오라클=시퀀스, mysql=오토인크리먼트)
@SequenceGenerator : 시퀀스 속성 변경
@TableGenerator : 테이블로 시퀀스를 관리

@Temporal : 자바의 Date 자료형을  db에서 날짜시각 자료형으로 바꿔서 넣고싶을때 사용

@Enumerated : enum 관련 제어

@Lob : 매우 큰 숫자/문자열을 넣고 싶을때 씀

@Transient : 필드의 특정속성에 대해 엔티티 매핑을 해제

@OneToOne : 1대 1 관계일때
@ManyToOne : 1 대 N 관계일때 N쪽 엔티티의 필드에 삽입
@OneToMany : 1 대 N 관계일때 1쪽 엔티티의 필드에 삽입
@JoinColumn : 1 대 N 관계일때 N쪽 엔티티의 필드에 삽입

@ManyToMany : N 대 N 관계일때 (실무에서 사용X. 주문시간/수량 같은 추가데이터가 들어올 수 있음. 연결테이블(조인테이블/중간테이블) 쓰기)
@JoinTable : ManyToMany 쓸때 연결테이블을 만들어줌

@Inheritance(strategy=InheritanceType.XXX) : 엔티티가 상속관계일때 씀. 부모 엔티티에 삽입
@DiscriminatorColumn : 엔티티가 상속관계일때 자식테이블을 표시하기위해 씀. 부모 엔티티에 삽입
@DiscriminatorValue("XXX") : 엔티티가 상속관계일때 자식테이블을 표시하기위해 씀. 자식 엔티티에 삽입

@MappedSuperclass : 공통 매핑 정보가 있을때 씀. 공통적인 속성이있는 부모클래스에 삽입

----------------------------------------------------------------------------------------------------

오류모음

ddl.auto 를 create 로 했는데 drop이 안되고 아래와 같은 오류날떄
Cannot drop "MEMBER" because "FKPSJMEA2E134AB3X3GSDOYXEPG" depends on it; SQL statement:
↓↓↓
하이버네이트 버전 변경
<dependency>
	<groupId>org.hibernate</groupId>
	<artifactId>hibernate-entitymanager</artifactId>
	<version>5.3.10.Final</version>
</dependency>
↓↓↓
<dependency>
	<groupId>org.hibernate</groupId>
	<artifactId>hibernate-entitymanager</artifactId>
	<version>5.4.13.Final</version>
</dependency>


Cannot drop "ITEM" because "FKABGE9EQALSPCEJIJ53RAT7PJH" depends on it
↓↓↓
버전을 변경해야함
hibernate는 5.4.22.Final
h2는 1.4.200 로 변경
https://www.h2database.com/html/download-archive.html
추가로 로컬에 남아있는 h2데이터베이스도 삭제해야함 (user폴더에 있는 test.mv.db 이런거)


Referential integrity constraint violation: "FKL7WSNY760HJY6X19KQNDUASBM: PUBLIC.MEMBER FOREIGN KEY(TEAM_ID) REFERENCES PUBLIC.TEAM(TEAM_ID) (1)"; SQL statement:
↓↓↓
@GeneratedValue를 쓴 속성에 값을 임의로 set해서 발생


Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@1929425f] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
org.hibernate.TransientPropertyValueException: object references an unsaved transient instance - save the transient instance before flushing : hellojpa.Member.team -> hellojpa.Team
↓↓↓
persist로 영속성컨텍스트에 안넣은 객체를 다른 객체에 담아서 persist후 flush/commit 하려고 했을때 발생

ex)
Team t1 = new Team();
t1.setName("asd");

Member member1 = new Member();
member1.setUsername("hello");
member1.setTeam(t1);
em.persist(member1);


org.h2.jdbc.JdbcSQLIntegrityConstraintViolationException: Referential integrity constraint violation: "FKQTRFKXTU92RLLEPI09F1MWVLS: PUBLIC.CHILD FOREIGN KEY(PARENT_ID) REFERENCES PUBLIC.PARENT(PARENT_ID) (1)"; SQL statement:
↓↓↓
외래키 제약조건 (부모를 먼저 수정/삭제하려고 한 경우)


----------------------------------------------------------------------------------------------------

JPA란

자바 ORM 기술에 대한 API 표준 명세
즉 인터페이스의 모음

이러한 JPA인터페이스를 구현한 대표적인 프레임워크가 하이버네이트 이다

JPA는 애플리케이션과 JDBC사이에서 동작한다

----------------------------------------------------------------------------------------------------

하이버네이트(Hibernate)

JPA를 구현한 프레임워크 중 사실상 표준. 오픈소스 소프트웨어
JPA는 기술 스펙이고 하이버네이트는 이 기능을 구현하여 공급해주는 역할


웹 통신 그리고 기술의 발전으로 인해 DB의 중요성이 점점 더 높아졌고, 각 언어들에서도 DB와 연동할 수 있는 기술들이 필요하게 됐다
그래서 처음에는 단순한 DB Connection을 위한 프레임워크들이 나오기 시작했다

하지만 인간이 쿼리를 하나하나 치기에는 너무 귀찮으며 실수가 많을 수 밖에 없다
그래서 나온것이 SQLMapper 시리즈 중 하나인 MyBatis이다

MyBatis는 xml을 이용해 쿼리를 통제하고자 했다
기존에는 자바 코드에서 문자열(String)을 이용하여 쿼리를 입력하고있었기때문에 오타가 많이 나는 문제가 있었다

그래서 관심사를 분리하여 XML파일로 쿼리를 분리하였다

근데 이렇게 SQL을 위주로 설계하다 보니, 객체 지향적으로 설계할 수 없게 되었다
SQL에 의존적인 개발을 할수밖에 없었다

연관관계가 있는 A테이블과 B테이블이 있다고 할때

테이블에 삽입하기 위해서는
각각의 테이블에 따로따로 insert문을 보내야 하고

테이블을 조회하기 위해서는
A와 B의 JOIN쿼리를 만들어서 가져온결과를 가지고
테이블별로 객체들을 생성해서 값을 다 채워넣고 반환해줘야함
테이블이 늘어나면 또 같은 작업을 반복해야함
→ 엄청 번잡해짐

위 작업들을 자바 컬렉션에서 한다고 하면
저장 → list.add(B) 하면 끝남
조회 → Album album = list.get(albumId);
부모타입으로 업캐스팅 한다고 하면
Item item = list.get(albumId)
이렇게 하면 되기때문에 매우 간편함

또 List의값을 변경할때
list.add()를 하면 따로 변경된 list를 다시 저장할필요가 없는데
JPA는 이런식으로 컬렉션처럼 비슷하게 동작함 (일일이 DB↔객체 간에 맵핑하는 번잡한 과정이 필요없음)

----------------------------------------------------------------------------------------------------

Spring Data JPA

스프링에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트(모듈)이다

Spring Data JPA의 목적은 예상가능하고 반복적인 코드들을 대신 작성해줘서 코드를 줄여주는것
이는 JPA를 한단계 추상화 시킨 Repository라는 인터페이스를 제공함으로써 이루어짐

스프링 데이터 JPA는 JPA공급자(JPA Provider) 가 아님
단지 데이터 계층에 접근하기 위해 필요한 뻔한 코드들의 사용을 줄여주는 인터페이스이며

반드시 기억해야할점은 Spring Data JPA는 항상 하이버네이트와 같은 JPA공급자(JPA Provider)가 필요하다는 것

----------------------------------------------------------------------------------------------------

JPA 역사

EJB(엔티티 빈, 자바 표준)
옛날부터 있던 ORM인데 문제는 인터페이스도 엄청 구현해야하고 속도도 느리고 기능도 잘 안동작함
거의 잘 안쓰였음
↓
하이버네이트
EJB를 쓰던 SI개발자 게빈킹이 답답해서 ORM 프레임워크를 만듬
거기에 많은사람들이 동참하고 해서 오픈소스가 되고 열었는데 EJB는 완전 망하고 하이버네이트가 뜸
↓
JPA
자바진영에서 반성하고 거친 오픈소스 하이버네이트를 복붙해서 다듬고 용어정리해서 표준 스펙으로 만든게 JPA
JPA는 인터페이스의 모음으로 스펙이다. (껍데기)

----------------------------------------------------------------------------------------------------

JPA 동작

저장
MemberDAO
↓
PERSIST
↓
JPA에서
- Entity 분석
- INSERT SQL 생성
- JDBC API 사용
- 패러다임 불일치 해결
그리고 JDBC API로 DB에 저장시킴


조회
MemberDAO
↓
find(id)
↓
JPA에서
- SELECT SQL 생성
- JDBC API 사용
- ResultSet 매핑
- 패러다임 불일치 해결
그리고 JDBC API로 DB에서 결과를 가져와서
↓
Entity Object로 DAO에게 반환해줌

----------------------------------------------------------------------------------------------------

지연로딩 & 즉시로딩

연관된 테이블을 SELECT하는 과정에 차이가 있음

지연로딩: 실제 객체가 사용될때 로딩
즉시로딩: JOIN SQL로 한번에 연관된 객체까지 미리 조회

지연로딩
Member member = memberDAO.find(memberId); → SELECT * FROM MEMBER
Team team = member.getTeam();
String teamName = team.getName(); → SELECT * FROM TEAM

즉시 로딩
Member member = memberDAO.find(memberId); → SELECT M.*, T.* FROM MEMBER JOIN TEAM
Team team = member.getTeam();
String teamName = team.getName();

위 예시에서 지연로딩은 Member와 Team이 연관되어있을때 Member를 꺼낼때는 Member만 SELECT해옴
그리고 member.getTeam()으로 Team객체를 가져오고, Team객체의 어떤 값을 딱 건들때(실제 필요한 시점에)
그때 JPA가 Team에 대한 쿼리를 날려서 맞는 teamName을 반환해줌

지연로딩은 쿼리가 두번 나가서 네트워크를 두번탐
개발하면서 보니까 99% Member을 조회하면 Team을 같이쓴다
↓
Member를 조회할때 무조건 Team을 같이 가져오는 즉시로딩이 더 좋음

Member를 쓸때는 Member밖에 안쓰고 Team은 어쩌다 한번씀
↓
지연로딩 전략이 훨씬 좋음

어플리케이션 개발을 다해놓은상태에서 중간에 튜닝을 할때
쿼리를 분리를 해놨는데 A와 B는 맨날 같이쓰니까 합친다고 가정한다.
이때 MyBatis로 하면 코드를 정말 많이 갈아내야한다
SQL 다시짜고 중간에 맵핑하는 코드 다 다시짜야됨
↓↓↓
JPA에서는 그거를 옵션 하나로 끄고켜고 튜닝이 됨

지연로딩으로 쭉 짜놓은다음
뭔가 최적화가 필요할때만 골라서 즉시로딩으로 바꾸는게 좋음

----------------------------------------------------------------------------------------------------

javax.persistence. → JPA 표준을 지키는 라이브러리
hibernate. → 하이버네이트 전용 라이브러리

JPA 자체가 표준이여서 구현체로 하이버네이트도 있고 이클립스 링크라는것도 있고 여러가지가 있음
javax는 하이버네이트 말고 다른 구현라이브러리를 써도 쓸 수 있음

----------------------------------------------------------------------------------------------------

JPA 구동 방식

JPA에는 Persistence라는 클래스가 있는데 여기서 시작함.

Persistence에서 META-INF/persistence.xml 설정정보를 읽어서
EntityManagerFactory라는 클래스를 만듦

만들어진 EntityManagerFactory라는 공장에서
필요할 떄마다 EntityManager를 찍어내서 돌리면 됨

----------------------------------------------------------------------------------------------------

실습

1. h2 DB 다운
https://www.h2database.com/

2. 터미널로 다운받은 h2폴더로 가서
/bin/
./h2.sh 실행

그러면 웹에서 DB가 열림

이후에 다시 들어가고싶으면 localhost:8082 로 들어가면 됨


3. 사용자 생성
JDBC URL: jdbc:h2:~/test
사용자명: sa
비밀번호: 없음

4. src/main/resources/META-INF/persistence.xml 만들고 DB/하이버네이트 설정내용 추가
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.2"
			 xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd">
	<persistence-unit name="hello">
		<properties>
			<!-- 필수 속성 -->
			<property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
			<property name="javax.persistence.jdbc.user" value="sa"/>
			<property name="javax.persistence.jdbc.password" value=""/>
			<property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/>			
			<property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/> <!-- SQL별로 방언이 있는데 그걸 모아놓은 라이브러리를 가져와야함-->

			<!-- 옵션 -->
			<property name="hibernate.show_sql" value="true"/>
			<property name="hibernate.format_sql" value="true"/>
			<property name="hibernate.use_sql_comments" value="true"/>
			<!--<property name="hibernate.hbm2ddl.auto" value="create" />-->
		</properties>
	</persistence-unit>
</persistence>

5. pom.xml에 의존성 추가후 maven 업데이트
<dependencies>
	<!-- JPA 하이버네이트 -->
	<dependency>
		<groupId>org.hibernate</groupId>
		<artifactId>hibernate-entitymanager</artifactId>
		<version>5.3.10.Final</version>
	</dependency>
	<!-- H2 데이터베이스 -->
	<dependency>
		<groupId>com.h2database</groupId>
		<artifactId>h2</artifactId>
		<version>1.4.199</version>
	</dependency>
</dependencies>


6. src/main/java/hellojpa/JpaMain.java 만들고 메인메소드 만들고 다음 코드 입력
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

resources/META-INF/persistence.xml 에 있는 persistence-unit name속성값을 쓰면 됨
EntityManagerFactory를 만드는순간 DB랑 연결도 다 되고 웬만한게 다 됨

실행했을때 커넥션과 관련된 정보들이 막 올라가면 된거


7. EntityManager 꺼내기
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();
// DB처리코드가 들어갈 자리
em.close();

emf.close();


8. h2에서 설정한걸 /src/main/resources/META-INF/persistence.xml에 똑같이 맞추기
<property name="javax.persistence.jdbc.user" value="sa"/>
<property name="javax.persistence.jdbc.password" value=""/>
<property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/>


9. h2사이트에서 테이블 만들기
아래의 sql문을 실행시켜 만들면 되고
create table Member(
    id bigint not null,
    name varchar(255),
    primary key(id)
);
sql문을 다 지운다음 만들어진 MEMBER테이블을 클릭하면 SELECT쿼리가 생김
테이블이 잘 SELECT되는지 확인하기


10. /src/main/java/hellojpa/Member.java 만들고 내용 입력
@Entity
public class Member {

	@Id
	private Long id;
	private String name;

}

@Entity (클래스에 삽입)
어노테이션이 있어야 JPA를 사용하는 애구나 하고 관리해야겠다라고 인식함

@Id (PK속성에 삽입)
JPA에게 PK가 뭔지 알려주기위해 PK컬럼에 어노테이션 붙이기


11. Getter/Setter 만들기


12. ★추가(INSERT) 하기
EntityManagerFactory → 애플리케이션 로딩시점에 딱 하나만 만들어야하고,
EntityManager → DB처리하는 트랜잭션 단위 = 일관적인 단위 작업을 할때마다 꼭 만들어야함
(ex. 고객에 들어와서 어떤 행위를 하고 나감, 상품을 장바구니 담기)

<JpaMain.java>
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();

Member member = new Member();
member.setId(1L);
member.setName("HelloA");
em.persist(member);

em.close();

emf.close();

위 코드를 실행하면 오류가 나는데,
JPA에서 데이터를 변경하는 모든 작업은 꼭 트랜잭션 안에서 작업해야함


13. 트랜잭션 만들기
EntityManager객체에 .getTransaction() 메소드를 이용해 트랜잭션을 얻을 수 있음
DB커넥션을 받았다고 생각하면 된다고 함.
begin() 메소드로 시작 시키고 DB작업 후 commit() 메소드로 커밋하기

<JpaMain.java>
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction(); // 트랜잭션 가져오기
tx.begin(); // 얻은 객체에 .begin() 메소드를 쓰면 DB트랜잭션이 시작됨

Member member = new Member();
member.setId(1L);
member.setName("HelloA");
em.persist(member);

tx.commit(); // DB 커밋

em.close();

emf.close();


14. 실행시키기
콘솔창에 insert 쿼리문이 출력되면 성공

/src/main/resources/META-INF/persistence.xml 에서

<property name="hibernate.show_sql" value="true"/>
는 sql문이 출력하는 역할

<property name="hibernate.format_sql" value="true"/>
는 sql문을 이쁘게 정렬하는 역할

<property name="hibernate.use_sql_comments" value="true"/>
는 쿼리가 왜 나왔는지 주석으로 알려주는 역할

DB에 잘 저장됐는지도 확인하기

DB의 테이블명/컬럼명 과 클래스명/속성명 의 이름이 다를 경우는 이름을 맵핑해주면됨
클래스(테이블) : @Table(name="DB테이블명")
필드(컬럼) : @Column(name="DB컬럼명")


15. 예외처리 하기
DB에 데이터를 저장하는 과정에서 오류가 나면 이후 코드들이 실행이 안되므로 예외처리가 필요함

<JpaMain.java>
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {
	Member member = new Member();
	member.setId(2L);
	member.setName("Hello");
	em.persist(member);
	tx.commit(); // 정상적이라면 커밋
} catch(Exception e) {
	tx.rollback(); // 예외가 발생하면 롤백
} finally {
	em.close(); // 작업이 다 끝나면 엔티티매니저를 닫기
}

emf.close(); // 전체 애플리케이션이 모두 끝나면 엔티티매니저팩토리 까지 닫기


16. ★조회(SELECT) 하기
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {

	Member findMember = em.find(Member.class, 1L);
	System.out.println("findMember: " + findMember); // Member{id=1, name='HelloA'}
	System.out.println("findMember.id: " + findMember.getId()); // 1
	System.out.println("findMember.name: " + findMember.getName()); // HelloA

	tx.commit();
} catch(Exception e) {
	tx.rollback();
} finally {
	em.close();
}

emf.close();

EntityManager를 자바 컬렉션이라고 생각하면됨

17. ★삭제(DELETE) 하기
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {

	Member findMember = em.find(Member.class, 1L);

	em.remove(findMember);

	tx.commit();
} catch(Exception e) {
	tx.rollback();
} finally {
	em.close();
}

emf.close();


14. ★수정(UPDATE) 하기
EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");

EntityManager em = emf.createEntityManager();

EntityTransaction tx = em.getTransaction();
tx.begin();

try {

	Member findMember = em.find(Member.class, 1L);
	findMember.setName("HelloJPA");

	tx.commit();
} catch(Exception e) {
	tx.rollback();
} finally {
	em.close();
}


em.persist(member); 로 저장을 하지 않아도 UPDATE가 됨
JPA를 통해서 엔티티를 가져오면 그 엔티티는 관리가 됨
그리고 변경이 됐는지 안됐는지 트랜잭션을 커밋하는 시점에서 다 체크를 함.
뭐가 바뀌었다면 커밋되기전에 업데이트 쿼리를 만들어서 날림


EntityManagerFactory는 딱 하나만 생성해서 애플리케이션 전체에서 공유
EntityManager는 쓰레드간에 공유X (사용하고 버려야함)
JPA의 모든 데이터 변경은 트랜잭션 안에서 실행 (단순 조회는 상관없음)

RDB는 내부적으로 트랜잭션 개념을 다 가지고있음 (insert/update등 쿼리가 올떄마다 트랜잭션이 동작됨)


18. ★쿼리를 직접 작성해 리스트로 조회(SELECT)하기
List<Member> result = em.createQuery("select m from Member as m", Member.class).getResultList();
System.out.println(result); // [Member{id=1, name='HelloJPA'}, Member{id=2, name='HelloB'}]

쿼리가 날라간것을 잘 보면 주석에는 JPQL이 적혀있고, 쿼리문은 엔티티를 선택한거라고 보면 됨


19. 페이징 처리도 간단하게 가능
List<Member> result = em.createQuery("select m from Member as m", Member.class)
		.setFirstResult(5)
		.setMaxResults(8)
		.getResultList();

이렇게 하면 쿼리를 각 DB 방언에 맞춰서 번역해서 만듦
mysql은 limit ? offset ? 으로
oracle은 rownum 으로

JPA는 SQL을 추상화해서 특정 데이터베이스SQL에 의존하지 않는 JPQL이라는 쿼리 언어를 제공함
기본적으로 ANSI-SQL에서 지원하는 SELECT, FROM, WHERE, GROUP BY, HAVING, JOIN 지원
SQL은 데이터베이스 테이블을 대상으로 한다면,
JPQL은 엔티티 객체를 대상으로 하는 객체지향 쿼리라고 보면 됨

조건을 걸려면 where절 쓰면 됨
List<Member> result = em.createQuery("select m from Member as m where m.name = 'asd'", Member.class)

----------------------------------------------------------------------------------------------------

JPA를 이해하려면 영속성 컨텍스트를 이해해야함

JPA에서 가장 중요한 2가지
★객체와 관계형 데이터베이스 매핑하기(Object Relational Mapping)
★영속성 컨텍스트


엔티티 매니저 팩토리와 엔티티 매니저를 이해해야함

				EntityManagerFactory
				↓				↓
				↓ 생성			↓ 생성
				↓				↓
고객이 요청→→→EntityManager1	EntityManager2 ←←← 고객이 요청
				↓				↓
				↓ 사용			↓ 사용
				↓				↓
			DB커넥션풀		DB커넥션풀
			(conn, conn ...)	(conn, conn ...)
				↘				↙
					↘		   ↙
						 DB

EntityManager는 내부적으로 DB커넥션을 사용해서 DB를 사용하게됨

----------------------------------------------------------------------------------------------------

영속성 컨텍스트(PersistenceContext)

JPA를 이해하는데 가자 중요한 용어
"엔티티를 영구 저장하는 환경" 이라는 뜻

EntityManager.persist(entity);
위 구문은 사실 DB에 저장한다는게 아니라 영속성 컨텍스트를 통해서 엔티티를 영속화한다
.persist() 메소드는 DB에 저장하는게 아니라 엔티티를 영속성컨텍스트 라는데에 저장한다는 뜻이다


영속성 컨텍스트는 논리적인 개념
눈에 보이지 않음
엔티티매니저를 통해서 영속성 컨텍스트에 접근

'엔티티매니저"를 생성하면 1:1 로 눈에 보이지않는 "영속성컨텍스트"가 생성됨

-------------------------

엔티티의 생명주기

비영속(new/transient)
영속성 컨텍스트와 전혀 관계가 없는 새로운 상태

영속(managed)
영속성 컨텍스트에 관리되는 상태

준영속(detached)
영속성 컨텍스트에 저장되었다가 분리된 상태

삭제(removed)
삭제된 상태

------------------------------

비영속 상태

Member member = new Member();
member.setId("member1");
member.setUsername("회원1");

JPA와 관련이 없이 객체만 생성한 상태

-----

영속 상태

em.persist() 로 집어넣은 상태
or
em.find() 로 가져온 상태


Member member = new Member();
member.setId("member1");
member.setUsername("회원1");

EntityManager em = emf.createEntityManager();
em.getTransaction().begin();

em.persist(member);

객체를 저장한 상태
em.persist()는 실제로 DB에 데이터를 저장하지 않는다

System.out.println("=== BEFORE ===")
em.persist(member);
System.out.println("=== AFTER ===")
앞뒤로 이렇게 찍어보면
쿼리문이 === AFTER === 다음에 출력되는걸 확인할 수 있음

영속상태가 된다고 해서 바로 DB에 쿼리가 날라가는게 아님
트랜잭션을 커밋하는 시점에 영속성컨텍스트에 있는애가 DB에 날아감
tx.commit()


em.find() 이때도 DB에서 데이터를 가져오는 시점에 영속상태로 관리하게 됨

-----

준영속 상태

영속상태였다가 영속성 컨텍스트에서 분리(detached)된 상태
영속성 컨텍스트가 제공하는 기능을 사용 못함

em.detach(member)
위처럼 detach메소드를 쓰면 영속성 컨텍스트에서 다시 지워짐


em.detach(엔티티) : 특정 엔티티만 준영속 상태로 전환
em.clear() : 영속성 컨텍스트를 완전히 초기화
em.close() : 영속성 컨텍스트를 종료


ex) 아래처럼 하면 영속성 컨텍스트에서 해제되었기때문에 아무일도 일어나지않음 (select쿼리만 실행되고 update쿼리는 실행되지않음)
Member member = em.find(Member.class,200L);
member.setName("zzzzzzzzzz");

em.detach(member);

tx.commit();


ex) 아래처럼 하면 1차캐시에있는 엔티티가 지워졌기 때문에 select쿼리가 2번 나감
Member member = em.find(Member.class,200L);

em.clear();

Member member2 = em.find(Member.class,200L);


★1차캐시 이런거 관계없이 테스트케이스를 작성하거나 할때, 눈으로 보고싶을때 주로 씀

-----

삭제

em.remove(member);

DB에서 DELETE쿼리로 날린다

------------------------------

영속성 컨텍스트의 이점

애플리케이션 ↔ 중간계층(영속성컨텍스트) ↔︎ DB

•1차 캐시
•동일성(identity) 보장
•트랜잭션을 지원하는 쓰기 지연(transactional write-behind)
•변경 감지(Dirty Checking)
•지연 로딩(Lazy Loading)

중간에서 버퍼링을 하고 캐싱을 하고 이런걸 할 수 있음

-----

1차캐시

한번조회했던거 또 조회하면 DB에 쿼리 안날라감 (동일한 트랜잭션 내에서)
고객에 10명이 동시에 접근하면 각각 별도의 1차캐시를 가짐(사실 성능상 얻을 수 있는 이점이 크진 않음. 성능보다는 매커니즘을 통해서 얻을 수 있는 이점들이 있음)

영속성 컨텍스트 ≒ EntityManager
그리고 1차 캐시인 Map이라고 생각하면됨

key : @Id 로 지정한 컬렴의 값 = "member1"
value : Entity = member객체

em.find(Member.class, "member1")
를 했을때, member1이라는 id(key)로 1차 캐시에서 조회한다

만약 있다면?
DB에 갔다올 필요없이 1차 캐시에 있는 객체(value)를 그냥 가져옴

만약 없다면?
1. DB에서 조회함
2. 1차 캐시에 저장
3. 반환

-----

동일성(identity) 보장

== 비교를 해도 같다고 나온다 (1차캐시에서 가져온걸로 쓰기때문에)

Member member1 = em.find(Member.class, 1L);
Member member2 = em.find(Member.class, 1L);

System.out.println(member1 == member2); // true가 나옴

1차캐시로 반복가능한 읽기(REPEATABLE READ) 등급의 트랜잭션 격리 수준을 데이터베이스가 아닌 애플리케이션 차원에서 제공함
같은 트랜잭션 안에서 == 비교를 하면 true가 나옴

-----

트랜잭션을 지원하는 쓰기지연 (transactional write-behind)

버퍼링, write를 모았다가 한번에 보내는거

em.persist(memberA);
em.persist(memberB);
// 여기까지 INSERT SQL을 DB에 보내지 않음

// 커밋하는 순간 DB에 INSERT SQL을 보낸다
transaction.commit();

-----

변경감지 (Dirty Checking)

update를 할때 변경된 엔티티를 JPA가 자동으로 인식하는것

엔티티의 값이 수정되면 .update()를 안해도 commit을 하면 update문이 자동으로 나감 (자바 컬렉션처럼)

DB에 아래와같은 데이터가 있다고 할때
ID  	NAME 
1	asd

setter로 객체의 값을 변경하면
Member member1 = em.find(Member.class, 1L);
member1.setName("asd222");

DB가 아래처럼 바뀜
D  	NAME  
1	asd222


동작원리는
1차캐시 안에는 db에서 읽어온 시점(최초시점)의 상태를 스냅샷으로 떠 놓게 됨
@Id		Entity		스냅샷
11		memberA	memberA 스냅샷
22		memberB	memberB 스냅샷

위 상태에서 memberA를 변경해놓으면 
1. 트랜잭션이 commit()메소드가 호출되는 시점에 내부적으로 flush() 가 호출되면서
2. JPA가 1차캐시 안의 Entity와 스냅샷을 비교함
3. 만약 Entity값이 바뀌었다면? → update쿼리를 쓰기지연 SQL저장소에 만듦
4. 만든 쿼리를 데이터베이스에 반영됨
5. commit됨

-----

지연로딩 (Lazy Loading)

실제 필요할때 쿼리를 날리는것

----------------------------------------------------------------------------------------------------

플러시(flush)

영속성컨텍스트의 변경내용을 DB에 반영(동기화)하는것 (★영속성 컨텍스트를 비우는게 아님)

DB트랜잭션이 commit()될때 flush가 일어남
쌓여있던 INSERT / DELETE / UPDATE SQL들이 DB에 날라감

영속성컨텍스트의 변경사항과 DB를 똑같게 맞추는 작업

em.flush() : 직접호출(쓸일 거의 없음, 알아두면 테스트할때 좋음)
트랜잭션 커밋 : 플러시 자동 호출
JPQL 쿼리 실행 : 플러시 자동 호출


날라가는 쿼리를 미리 보고싶을때 아래와 같이 쓸 수 있음
Member member = new Member(200L, "member200");
em.persist(member);
em.flush(); // 강제 호출
System.out.println("==============================");

이렇게 하면 쿼리가 DB에 바로 반영됨 (=====전에 반영됨)

이제 transaction.commit() 전에
transaction.rollback() 하면 쿼리를 실제로 안날리고 쿼리를 확인할 수 있음

JPQL은 쿼리가 실행되기전에도 플러시가 발동됨
이를 옵션으로 끌 수 있지만 잘 안씀. 웬만하면 손대지 말고 AUTO로 쓰기
FlushModeType.AUTO : 커밋이나 쿼리를 실행할 때 플러시 (기본값)
FlushModeType.COMMIT : 커밋할 때만 플러시

----------------------------------------------------------------------------------------------------

엔티티 매핑

객체와 테이블 매핑: @Entity, @Table
필드와 컬럼 매핑: @Column
기본 키 매핑: @Id
연관관계 매핑: @ManyToOne, @JoinColumn

-----

@Entity

@Entity가 붙은 클래스는 JPA가 관리, 엔티티라 한다
@Entity가 붙지 않으면 JPA랑은 전혀 관계없는, 그냥 내가 마음대로 쓰고싶은 클래스
JPA를 사용해서 테이블과 매핑할 클래스는 @Entity 필수

<주의사항>
★★★기본 생성자 필수(파라미터가 없는 public 또는 protected 생성자)★★★
final 클래스, enum, interface, inner 클래스에는 사용할 수 없음
저장할 필드에 final 사용하면 안됨

<속성 종류>
name: JPA가 엔티티를 구분하는 이름을 변경할 수 있음 (쓸일은 거의 없음)

-----

@Table

엔티티와 매핑할 테이블을 지정

<속성 종류>
name : 테이블명을 적으면 이름을 다르게 해서 쓸 수 있음 → 쿼리가 지정한 이름으로 나감
catalog : 데이터베이스 catalog 매핑. catalog라는게 있는 DB에서 사용
schema : 데이터베이스 schema 매핑. DB마다 다르긴한데 schema를 구분하고자 할때 사용
uniqueConstraints(DDL) : DDL 생성시에 유니크 제약조건 생성

ex) name속성
@Table(name = "MBR") // DB의 "MBR"이라는 테이블과 매핑
public class Member {

----------------------------------------------------------------------------------------------------

데이터베이스 스키마 자동 생성 (CREATE / UPDATE / DROP)

•DDL을 애플리케이션 실행 시점에 자동 생성해줌
	애플리케이션 로딩시점에 CREATE문으로 DB를 테이블을 생성하고 시작하게 할 수 있음

•테이블 중심 → 객체 중심
•DB 방언에 맞게 적절한 DDL이 생성됨 (mysql→varchar, 오라클→varchar2 등)
•이렇게 생성된 DDL은 개발서버에서만 사용
•생성된 DDL은 운영서버에서는 사용하지 않거나 적절히 다듬은 후 사용
•운영 장비에는 절대로 create, create-drop, update를 사용하면 안됨
	(update도 데이터가 몇천만건 있는상태에서 alter를 잘못 하면 락이걸려서 시스템이 몇분동안 중단될 수 있음)
	개발 초기단계는 create 또는 update
	테스트 서버는 update 또는 validate
	스테이징과 운영서버는 validate 또는 none

src/main/resources/META-INF/persistence.xml 파일에서 설정 가능함

<property name="hibernate.hbm2ddl.auto" value="옵션명" />

create: 기존 테이블 삭제 후 다시 생성(DROP + CREATE)
create-drop: create와 같으나 종료시점에 테이블 DROP
update: 변경된 것만 반영 (ALTER)
validate: 엔티티와 테이블이 정상 매핑되었는지만 확인
none: 사용하지 않음


★create
drop table Member if exists → Member 라는 테이블이 있으면 drop하고
create table Member ( ... → Member 라는 테이블을 만듦

DB에 변경한 필드가 컬럼에 반영되어있음


★create-drop
drop table Member if exists
create table Member ( ...
drop table Member if exists → 마지막에 테이블을 drop함

★update
필드(컬럼)을 추가한경우 drop&create가 아닌 alter문으로 추가됨
alter table Member 
       add column age integer not null

반대로 필드(컬럼)를 삭제한건 반영이 안됨(아무일도 일어나지 않음)
필드(컬럼) 이름을 바꾸면 바뀐 이름의 컬럼이 추가되고 이전 컬럼도 그대로 살아있음 


★validate
컬럼이 DB와 정상적으로 매핑되었는지(일치하는지) 확인할때만 씀
엔티티에는 컬럼이 있는데 DB에는 컬럼이 없을경우 다를경우는 아래와같이 예외가 발생함
SchemaManagementException: Schema-validation: missing column [zzzzz] in table [Member]

★none (사실 none이라는것은 없지만 none으로 적는게 관례)
기능을 사용하지 않음. 옵션을 안넣은것과 동일함
이경우는 필드가 어떻든 DB에 DDL(CREATE / ALTER / DROP)이 전송되지 않음

----------------------------------------------------------------------------------------------------

@Id - 기본 키 매핑 (uuid를 쓰거나, 데이터를 조합해서 직접 id를 만들거라면 씀)

----------------------------------------------------------------------------------------------------

@GeneratedValue - 순차적인 값을 자동으로 할당(오라클=시퀀스, mysql=오토인크리먼트)

이 어노테이션을 쓸때는 해당 컬럼에 값을 set 하면 안됨

<속성 종류>
strategy = GenerationType.AUTO : DB방언에 맞춰서 자동으로 생성이 됨 (기본값)
strategy = GenerationType.IDENTITY : 기본 키 생성을 DB에 위임. 주로 mysql에서 씀
	쿼리 로그중 일부 → id integer auto_increment

	해당 컬럼에 값을 넣으면(set하면) 안됨. 그리고 db에서 null로 값이 넘어오는순간 auto-increment로 값을 세팅해줌
	그렇기 때문에 db로 넘어가기 전까지 생성된 id를 모름. db에 값이 들어간 이후에 id를 알 수 있음

	문제는 JPA는 @Id필드값으로 엔티티를 관리하는데 id가 없으니 관리를 못함.
	그래서 예외적으로 IDENTITY전략일때만 persist 메소드가 호출될때 DB에 insert가 됨 (원래는 commit 메소드 호출되는 시점에 insert)
	그래서 뭔가 모아서 insert하는게 IDENTITY전략에서는 불가능

	참고사항: h2최신버전에서 id에는 null이들어갈수없다는 버그가 있는데 그럴때는 persistence.xml에서 MODE=LEGACY" 붙이면 됨
	<property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test;MODE=LEGACY"/>
	안되면 GenerationType.SEQUENCE 쓰기

strategy = GenerationType.SEQUENCE : 주로 oracle에서 씀
	persist 메소드가 호출될때 DB에서 시퀀스를 조회한 후, 영속성컨텍스트에 만들어진 id를 넣어 관리를 시작하고, commit이 될때 insert
	시퀀스에 이름을 넣고 싶으면 class에 @SequenceGenerator 어노테이션도 쓰기

----------------------------------------------------------------------------------------------------

@SequenceGenerator

@generatedValue(strategy=GenerationType.SEQUENCE) 를 쓸때, 시퀀스 속성을 변경하고싶을경우 씀.
@GeneratedValue 의 generator 속성에 이름을 만든 name값을 넣으면 됨

<속성 종류>
name : 식별자 생성기 이름
sequenceName : DB에 등록되어있는 시퀀스명 (기본값: hibernate_sequence)
initialValue : DDL생성시에만 사용됨. 시퀀스 DDL을 생성할때 처음 시작할 수를 지정 (기본값: 1)
allocationSize : 시퀀스 한번 호출에 증가하는 수. 성능 최적화에 사용됨. DB시퀀스 값이 1씩 증가하도록 설정되어있으면 이 값도 반드시 1로 설정해야함 (기본값: 50)
catalog, schema : 데이터베이스 catalog, schema 이름

ex) generator 생성
@Entity
@SequenceGenerator(
	name = "MEMBER_SEQ_GENERATOR",
	sequenceName = "MEMBER_SEQ",
	initalValue = 1,
	allocationSize = 1
)
public class Member{

ex) 만든 generator 사용
@GeneratedValue(Strategy = GenerationType.SEQUENCE, generator = "MEMBER_SEQ_GENERATOR")
private Long id;

----------------------------------------------------------------------------------------------------

@TableGenerator

테이블로 시퀀스를 관리 (잘 안씀)

@TableGenerator(
	name = "MEMBER_SEQ_GENERATOR",
	pkColumnValue = "MEMBER_SEQ",
	allocationSize = 1
)
public class Member{
	@GeneratedValue(strategy = GenerationType.TABLE, generator = "MEMBER_SEQ_GENERATOR")
	private Long id;

그럼 테이블이 아래처럼 생성되고 insert할때마다 숫자 증가함
SEQUENCE_NAME  	NEXT_VAL  
MEMBER_SEQ		22

----------------------------------------------------------------------------------------------------

@Column - DDL 생성기능

DDL생성기능은 DDL을 자동 생성할때만 사용되고 JPA의 실행로직에는 영향을 주지 않는다

<속성 종류>
name : DB컬럼명을 넣어서 이름을 따로 쓸 수 있음

length : 최대 자리수
	ex) length=10

inupdatable : update가 작동될시 해당 컬럼은 절대 반영되지않게 할 수 있음. 기본값 true
	ex) updatable=false

updatable : update가 작동될시 해당 컬럼은 절대 반영되지않게 할 수 있음. 기본값 true
	ex) updatable=false

nullable : nullable=false로 설정시 DDL생성시 not null 제약조건이 들어감

unique : 유니크. 제약조건명이 알아보기힘든값으로 들어가고, 복합도 안됨 따라서 @Table에서
	@Table(uniqueConstraints = ) 이속성으로 설정하는게 좋음

columnDefinition : 컬럼 정의를 문자열로 직접 넣을 수 있음
	ex) @Column(columnDefinition = "varchar(100) default 'EMPTY'")
↓↓↓자동쿼리↓↓↓
create table Member(
	name varchar(100) default 'EMPTY'

percision, scale : BigDecimal 자료형인경우 사용. percision은 소수자리를 포함한 전체 자리수, scale은 소수의 자리수다 (= mysql의 decimal)
	ex) @Column(percision=5, scale=2)


ex) 글자수 제한, 유니크 제약조건
@Column(unique=true, length=10)
private String name;

↓↓↓자동쿼리↓↓↓
.
.
name varchar(10),
.
.
alter table Member 
	add constraint UK_ektea7vp6e3low620iewuxhlq unique (name)

-----

@Temporal(TemporalType.TIMESTAMP)

자바의 Date 자료형을  db에서 날짜시각 자료형으로 바꿔서 넣고싶을때 사용.
자바에는 Date 자료형에 날짜/시각이 다 포함되어있어서 속성을 넣어야함.
안쓰면 mysql : datetime, 오라클 : timestamp 로 들어감
속성을 DATE / TIME / TIMESTAMP 로 하면 날짜 / 시각 / 날짜시각으로 들어감
mysql : date / time / datetime
oracle : date / date / timestamp

참고 : LocalDate / LocalDateTime 을 쓰면 이 어노테이션을 쓸 필요가 없음 (하이버네이트 최신버전에서 지원)
LocalDate / LocalDateTime 를 쓰면 아래와같이 들어감
mysql : date / datetime
oracle : date / timestamp

ex) 
@Temporal(TemporalType.TIMESTAMP)
private Date lastModifiedDate;

-----

@Enumerated(EnumType.String)

enum 쓸때 씀

자바에는 enum 타입이 있지만
DB에는 enum 타입이 없는데 그럴때 씀

<속성 종류>
Enumtype.STRING : enum의 이름을 저장
Enumtype.ORDINAL : enum의 순서를 저장 (기본값). 이 옵션으로 설정하면 DDL에서 숫자형으로 컬럼이 생성됨
	이걸 쓰면 안되고 STRING을 써야하는 이유는 enum의 값들의 순서가 변경되거나, 값이 앞쪽에 추가되면 → 뭐가 뭔지 알 수 없어 엉망이 되기때문

ex)
@Enumerated(EnumType.STRING)
private RoleType roleType;

-----

@Lob

매우 큰 숫자/문자열을 넣고 싶을때 씀
mysql : String으로 하면 longtext, 나머지로 하면 longblob로 들어감
oracle : String으로 하면 clob, 나머지로 하면 blob로 들어감

ex)
@Lob
private String description;

-----

@Transient

매핑을 해제

DB와 관계를 해제하고 자바 메모리상에서만 임시로 어떤값을 보관하고싶을때

-----

@JoinColumn

외래키를 매핑할 떄 사용

name : 매핑할 외래키 이름
referencedColumnName : 외래키가 참조하는 대상 테이블의 컬럼명 (기본값: 참조하는 테이블의 기본키 컬럼명)
foreignKey(DDL) : 외래 키 제약조건을 직접 지정할 수 있음. 이 속성은 테이블을 생성할 때만 사용

아래속성들은 @Column의 속성과 같다
unique
nullable
insertable
updateable
columnDefinition
table

-----

@ManyToOne

다대일 관계 매핑

optional : false로 설정하면 연관된 엔티티가 항상 있어야 한다 (기본값: TRUE)
fetch : 글로벌 페치 전략을 설정한다 (기본값: @ManyoToOne=FetchType.EAGER @OneToMany=FetchType.LAZY)
cascade : 영속성 전이 기능을 사용한다
targetEntity : 연관된 엔티티의 타입 정보를 설정한다. 이 기능은 거의 사욯하지 않는다. 컬렉션을 사용해도 제네릭으로 타입 정보를 알 수 있다(제네릭이 없는시절에 썼음)

@ManyToOne에는 mappedBy속성이 없음. 그 뜻은 다대일을 쓰면 연관관계의 주인이 돼야 한다는뜻

----------------------------------------------------------------------------------------------------

1:N , N:1 매핑

① 객체를 DB 테이블에 맞춘 데이터 중심의 설계
public class Team{
	private Long id
	private Long memberid;

테이블은 외래키로 조인을 해서 연관된 테이블을 찾음
객체는 참조를 사용해서 연관된 객체를 찾음
참조가 없으므로 UML도 잘못됨


② 객체지향스러운 설계
public class Team{
	private Long id
	private Member member;

------------------------------

@OneToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "DB 외래키 컬럼명")
1 : N 관계일때 주 테이블(주로 엑세스하는 테이블) 엔티티의 필드에 삽입

@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "DB 외래키 컬럼명")
1 : N 관계일때 N쪽 엔티티의 필드에 삽입

@OneToMany(mappedBy = "N쪽 엔티티클래스의 필드속성명")
1 : N 관계일때 1쪽 엔티티의 필드에 삽입


ex) ManyToOne
public class Member {
	@Id
	@GeneratedValue
	@Column(name = "MEMBER_ID")
	private Long id;

	@ManyToOne
	@JoinColumn
	private Team team;

public class Member {
	@Id
	@GeneratedValue
	@Column(name = "MEMBER_ID")
	private Long id;

	@Column(name = "NAME", nullable = false)
	private String username;

	@ManyToOne
	@JoinColumn(name = "TEAM_ID")
	private Team team;
}

public class JpaMain {
.
.
Team team = new Team();
team.setName("team1");
em.persist(team);

Member member = new Member();
member.setUsername("member1");
member.setTeam(team); // 이때 JPA가 자동으로 team객체의 PK값을 가져와서 TEAM_ID컬럼의 값으로 사용함
em.persist(member);


그리고 em.flush로 쿼리를 DB에 날린 후
em.clear로 영속성컨텍스트를 초기화하면

Member findMember = em.find(Member.class, member.getId());
Team findTeam = findMember.getTeam();
System.out.println(findTeam.getName());

위처럼 조회를 했을때, 영속성컨텍스트에서 못가져오게돼서, 아래처럼 새로 select쿼리를 DB에 날리는데

select
    member0_.MEMBER_ID as MEMBER_I1_0_0_,
    member0_.TEAM_ID as TEAM_ID3_0_0_,
    member0_.NAME as NAME2_0_0_,
    team1_.TEAM_ID as TEAM_ID1_1_1_,
    team1_.name as name2_1_1_ 
from
    Member member0_ 
left outer join
    Team team1_ 
        on member0_.TEAM_ID=team1_.TEAM_ID 
where
    member0_.MEMBER_ID=?

만약 @ManyToOne(fetch = FetchType.LAZY) 로 할경우 아래처럼 select 쿼리가 2번 DB로 날라감

select
    member0_.MEMBER_ID as MEMBER_I1_0_0_,
    member0_.TEAM_ID as TEAM_ID3_0_0_,
    member0_.NAME as NAME2_0_0_ 
from
    Member member0_ 
where
    member0_.MEMBER_ID=?

select
    team0_.TEAM_ID as TEAM_ID1_1_0_,
    team0_.name as name2_1_0_ 
from
    Team team0_ 
where
    team0_.TEAM_ID=?


ex) OneToMany
@Entity
@Getter
@Setter
@ToString
public class Team {
	@Id
	@GeneratedValue
	@Column(name = "TEAM_ID")
	private Long id;
	private String name;

	@OneToMany(mappedBy = "team") // N쪽 엔티티클래스의 @ManyToOne이 걸려있는 필드속성명을 넣어서 연결
	private List<Member> members = new ArrayList<>();
}

★ mappedBy속성을 안넣으면 연결이 되지 않아서, 해당 필드를 getter로 가져와서 출력해봐도 [](빈배열) 이 나옴
★ 양방향 연결시 주의사항이 있는데, ToString 재정의를 양쪽 엔티티 모두의 참조필드에 하고 실행하면 무한루프가 발생함
	엔티티의 참조필드는 @ToString.Exclude 어노테이션을 붙여서 toString재정의에서 제외시켜야함

	참고로 한쪽(Member)만 하면 아래처럼 나옴
	[Member(id=2, username=member1, team=hellojpa.Team@df1cff6)]

----------------------------------------------------------------------------------------------------

DB테이블과 JPA엔티티 차이

테이블
	외래키 하나로 양쪽 조인 가능
	사실 방향이라는 개념이 없음

객체
	참조용 필드가 있는 쪽으로만 참조 가능
	한쪽만 참조하면 단방향
	양쪽이 서로 참조하면 양방향

----------------------------------------------------------------------------------------------------

JPA에서 양방향 참조는 단방향 참조가 2개 있는것이다

<Member>						<Team>
Team team	ㅡㅡㅡㅡㅡㅡㅡㅡㅡ→	id
id 								name
username	←ㅡㅡㅡㅡㅡㅡㅡㅡㅡ	List members

이때문에
Member의 team과
Team의 members중
어떤걸 변경했을때 DB에 쓰기를 할건지 정해야 하는데(누가 주인인지)

외래키가 있는쪽, 1:N에서 N쪽을 주인으로 생각하면 됨
MEMBER테이블의 TEAM_ID(FK) 를 바꿀때는 Member엔티티의 team을 주인으로 생각하면 됨

@OneToMany(mappedBy = ) 가 있는 쪽은 읽기만 됨

ex)
<주인 - DB의 외래키를 insert/update 가능>
@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "TEAM_ID")
@ToString.Exclude
private Team team;

<읽기만 됨>
@OneToMany(mappedBy = "team")
@ToString.Exclude
private List<Member> members = new ArrayList<>();

-----

★주의★ 이렇게 하면 안됨
Member member = new Member();
member.setUsername("member1");
em.persist(member);

Team team = new Team();
team.setName("TeamA");
team.getMembers().add(member);
em.persist(team);

tx.commit();

연관관계의 주인이아닌 가짜에 set을 했기때문에 db에 반영이 되지 않음 (insert 쿼리만 날라가고 DB에서 보면 데이터가 없음)

올바른 예시 (member엔티티에 team엔티티를 넣어야함)
Team team = new Team();
team.setName("team1");
em.persist(team);

Member member = new Member();
member.setUsername("member1");
member.setTeam(team);
em.persist(member);

------------------------------

양방향 관계에서 주의사항

Team team = new Team();
team.setName("team1");

em.persist(team);

Member member = new Member();
member.setUsername("member1");
member.setTeam(team);
em.persist(member);

em.flush();
em.clear();

Member findMember = em.find(Member.class, member.getId());

System.out.println("findMember.getTeam().getMembers()...............");
System.out.println(findMember.getTeam().getMembers());


위 코드에서
em.flush()와 em.clear() 가 없으면 em.find(Member.class, member.getId()).getTeam().getMembers() 가 조회되지않음

em.flush() 를 해서 쿼리를 db로 날리고,
em.clear() 을 해서 영속성컨텍스트를 지워야
em.find() 를 호출했을때 영속성 컨텍스트에 없으니 db에 select 쿼리를 날려서 새로 조회하게 됨

그러면 다시 조회해왔기때문에 JPA가 외래키가 있다는것도 알고 해서 members도 다시 조회해야겠다는 매커니즘이 내부적으로 동작함

하지만 실무에서는 em.flush, em.clear()를 직접 호출하는 경우는 거의 없음.

순수객체상태를 고려해서 항상 양쪽에 값을 세팅해야함

flush()와 clear() 를 쓰는 대신에 다른 방법이 있음


그 방법은
member.setTeam(team) 이것만 넣는게 아닌
team.getMembers().add(member); 이것도 같이 넣어야함


두번씩 추가하는걸 깜빡할 수 있기때문에 '연관관계 편의 메소드' 를 만드는게 좋음

Member클래스의 setTeam 메소드에
team.getMembers().add(this);
를 추가하면
그 다음부터는 team.getMembers().add(member)를 안써도 됨

(외래필드속성으로 자신클래스를 담아놓은 List를 get하는 메소드를 호출한다음 거기에 add메소드로 this를 담은 것임)

참고로 getter/setter 관례가 있어서 setTeam말고 changeTeam이렇게 메소드명을 다르게 하는 사람도 있음


연관관계 편의 메소드는 비즈니스 로직이 복잡하면 if문도 넣는 등 더 복잡하게 써야될수도 있다고 함

연관관계 편의 메소드는 1쪽에 넣어도 되고 N쪽에 넣어도 된다고 함
Team클래스에
public void addMember(Member member){
	member.setTeam(this);
	members.add(member);
}
둘 중 한쪽에서만 쓰는게 좋다고 함


★양방향 매핑시 무한루프 주의
toString(), JSON생성 라이브러리

------------------------------

단방향 매핑만으로 설계가 다 끝나야함

양방향 매핑은 반대 방향으로 조회기능이 추가된 것 뿐

JPQL에서 역방향으로 탐색할 일이 많음

단방향 매핑을 잘 하고 양방향 매핑은 필요할때 추가해도 됨

-----

연관관계의 주인을 정하는 기준

비즈니스 로직을 기준으로 연관관계의 주인을 선택하면 안됨

연관관계의 주인은 테이블 외래키의 위치를 기준으로 정해야함

-----

연관관계를 잘 설계하는게 중요

회원 테이블과 주문 테이블이 있다고 할때

한 회원이 주문한 목록을 출력하려고 할때,
회원 엔티티에서 List<orders> 를 하는건 안좋은 방법이고
주문 엔티티에서 member를 조회하는게 더 좋은 방법이다

Member가 굳이 Orders 를 알 필요는 거의 없음

----------------------------------------------------------------------------------------------------

@ManyToMany
N 대 N 관계일때 DB는 연결테이블이고 엔티티만 N대N으로 할 수 있음
그러나 주문시간/수량 같은 추가데이터가 들어올 수 있으므로 엔티티도 연결엔티티 쓰기 (@ManyToOne & @OneToMany)

@JoinTable(name = "연결테이블명",
	joinColumns = @JoinColumn(name = "현재테이블과연결하는FK")
	inversJoinColumns = @JoinColumn(name = "반대테이블과연결하는FK")
)
@ManyToMnay일때 연결테이블과 매핑해줌


ex) @ManyToMany
@Entity
public class Category {
	@Id
	private Long id;
	@ManyToMany
	@JoinTable(name = "CATEGORY_ITEM",
		joinColumns = @JoinColumn(name = "CATEGORY_ID"),
		inverseJoinColumns = @JoinColumn(name = "ITEM_ID")
	)
	private List<Item> items = new ArrayList<>();
}

@Entity
public class Item {
	@ManyToMany(mappedBy = "items")
	private List<Category> categories = new ArrayList<>();
}


ex) @ManyToMany 대신 연결테이블 쓴 예시
@Entity
public class MemberProduct{
	@Id @GeneratedValue
	private Long id;

	@ManyToOne
	@JoinColumn(name = "MEMBER_ID")
	private Member member;

	@ManyToOne
	@JoinColumn(name = "PRODUCT_ID")
	private Product product;

	private int count;
	private int price;
	private LocalDateTime orderDateTime;
}

@Entity
public Member{
	@OneToMany(mappedBy="member")
	private List<MemberProduct> memberProducts = new ArrayList<>();
}

@Entity
public Product{
	@OneToMany(mappedBy="product")
	private List<MemberProduct> memberProducts = new ArrayList<>();
}

----------------------------------------------------------------------------------------------------

상속관계 매핑

공통적인 속성이 있다고 할때
엔티티 상속 매핑이 가능.

부모 엔티티는 abstract로 만들어 주고, 자식엔티티에서 extends 하면
Id는 안넣어도 되고 @Entity만 쓰면됨

실행해보면 create될때 부모 테이블로 모두 합쳐지는데,
부모 클래스에서 @Inheritance 로 설정 변경 가능


@Inheritance(strategy=InheritanceType.XXX)
	JOINED : 조인 전략 → 공통적인 속성은 부모테이블에, 각자의 속성은 자식테이블에 넣음
		(insert시 데이터가 두 테이블에 각각 들어가고, select시 inner join해서 가져와짐)
	SINGLE_TABLE : 단일 테이블 전략 (기본값) → 부모테이블에 모든 자식속성을 넣어버림
		(insert시 부모테이블에만 값이 들어가고, select시 DTYPE로 어떤 자식인지 구분됨. @DiscriminatorColumn을 안넣어도 구분컬럼이 생김.
		다른 자식컬럼들의 값은 null로 들어감. 성능상 이점이 있음)
	TABLE_PER_CLASS : 구현 클래스마다 테이블 전략 → 자식 테이블들에 부모 속성과 각각의 속성을 넣음. 자식테이블들에 부모 컬럼을 중복으로 만듦
		부모 엔티티를 abstract로 하면 부모테이블은 만들어지지 않음. @DiscriminatorColumn는 필요없음
		(insert시 자식테이블에만 들어감.
		find를 자식엔티티 말고 부모엔티티로 찾는다면 id를 모든 자식테이블을 다 가져와서 찾게 됨. 어느테이블에 있는지 모르기 때문)
@DiscriminatorColumn(name="DTYPE")
@DiscriminatorValue("XXX")


@DiscriminatorColumn
부모테이블에 삽입
자식 테이블명을 넣을 수 있는 속성이 추가되고 insert되면 해당 자식테이블명이 값으로 들어감 (컬럼명 기본값: DTYPE)
없어도 무방하지만 있는게 좋음. 이걸 안넣으면 어느자식때문에 값이 들어왔는지 부모테이블만 보고선 모르기 때문


@DiscriminatorValue("XXX")
자식테이블에 삽입
@DiscriminatorColumn 컬럼의 값으로 이름을 직접 지정할 수가 있음


JOINED 전략
장점 : 정규화가 돼있음. 제약조건을 부모엔티티에 걸어서 맞출 수 있음. 공통 속성으로 뭔가를 조회 하려면 부모 테이블만 보면 됨
	외래 키 참조 무결성 제약조건 활용 가능
	저장 공간의 효율화
단점 : 조회시 조인을 많이 사용, 성능 저하
	조회 쿼리가 복잡함
	데이터 저장시 insert 쿼리 2번 호출
사실 위에 단점들은 괜찮음. 관리가 복잡한게 단점. 조회시 성능저하도 잘 조인하면 그렇게 저하되지않음.
저장공간이 효율화되기때문에 어떤측면에서는 성능이 더 잘나옴. 정석이라고 생각하면됨
비즈니스적으로 중요하고 복잡할때 씀

SINGLE_TABLE 전략
장점 : 조인이 필요없어서 조회 성능이 빠름. 조회 쿼리가 단순함
단점 : 자식 엔티티가 매핑한 컬럼은 모두 null 허용 (데이터 무결성측면에서 볼떄는 애매한게 있음).
	단일테이블에 모든것을 저장하므로 테이블이 커질 수 있고, 상황에 따라서 조회성능이 오히려 느려질 수 있음. 일반적으로는 빠름
데이터도 많지 않고, 확장가능성도 없고, 단순할때 씀

TABLE_PER_CLASS 전략
장점 : 서브 타입을 명확하게 구분해서 처리할 때 효과적(insert/select). not null 제약조건 사용 가능
단점 : 여러 자식테이블을 함께 조회할 때 성능이 느림(UNION 쿼리). 자식 테이블을 통합해서 쿼리하기 어려움
쓰면 안되는 전략. 이 전략은 데이터베이스 설계자들과 ORM전문가들 둘 다 추천하지 않음. 뭔가 묶이는게 없기 떄문

----------------------------------------------------------------------------------------------------

@MappedSuperclass

엔티티들에 공통된 속성이 있을때 (id, name 등)
공통된 속성이 있는 부모테이블을 만들고 @MappedSuperclass를 삽입
공통되는 컬럼은 자식클래스에서는 지우고 @MappedSuperclass가 삽입된 부모클래스를 extends 하면 됨

테이블과 관계 없고, 단순히 엔티티가 공통으로 사용하는 매핑 정보를 모으는 역할

상속관계 매핑이 아님
엔티티가 아님. 이 어노테이션이 붙은 클래스는 테이블과 매핑되지않음 (테이블이 생기지 않음)

조회, 검색 불가(상속엔티티처럼 em.find(BaseEntity.class, ) 불가)

직접 생성할 일이 없으므로 추상클래스(abstract) 권장

주로 등록일, 수정일, 등록자, 수정자 같은 전체 엔티티에서 공통으로 적용하는 정보를 모을 때 사용


★참고로 엔티티는 엔티티나(상속관계매핑 이거나) @MappedSuperclass로 지정한 클래스(속성만 상속)만 상속(extends) 가능

----------------------------------------------------------------------------------------------------

프록시

연관관계가 걸려있는 엔티티들을 조회할때, 가져올필요가 없는 사용하지 않는 엔티티가 가져와지면 손해임. 최적화가 안됨

<Member>와 연관관계인 <Team>이 있다고 할때
Member와 Team을 동시에 조회해야하는 상황이 있고,
Member만 조회해야 하는 상황이 있음.

Member member = em.find(Member.class, 1L);
위 find메소드가 실행될떄 Member와 Team을 둘다 가져오면 Member와 Team을 같이 출력할떄는 유리하겠지만,
Member만 딱 출력하는 케이스를 생각해보면 되게 낭비임.

JPA는 이런걸 지연로딩이나 프록시로 해결이 가능함


em.find() : DB를 통해서 실제 엔티티 객체 조회
em.getReference() : 데이터베이스 조회를 미루는 가짜(프록시) 엔티티 객체 조회

getReference() 를 호출하는 시점에는 DB에 SELECT 쿼리를 안날림
getReference() 로 반환받은 객체에 .class를 찍어보면 아래처럼 ~$hibernateProxy$~ 이런식으로 가짜 엔티티 객체인걸 알 수 있음
class hellojpa.Member$HibernateProxy$8lGoRJlz

프록시는 실제 클래스를 상속 받아서 만들어짐
실제 클래스와 겉 모양이 같다
사용하는 입장에서는 진짜 객체인지 프록시 객체인지 구분하지 않고 사용하면 됨(이론상)

------------------------------

프록시 객체의 초기화

1. getName()
2. 프록시가 영속성컨텍스트로 초기화 요청
3. DB조회
4. 실제 엔티티 생성
5. Member target
target.getName() 이렇게 값을 복사해서 1번으로 반환해줌

한번 조회하면 target에 값이 들어가기때문에 계속 DB조회할 일은 없음

프록시 객체는 처음 사용할 때 한번만 초기화

프록시 객체를 초기화 할 때, 프록시 객체가 실제 엔티티로 바뀌는 것은 아님. 초기화 되면 프록시 객체를 통해서 실제 엔티티에 접근 가능

프록시 객체는 원본 엔티티를 상속받음. 따라서 타입 채크시 주의해야함( == 비교 실패, 대신 instance of 사용 )

영속성 컨텍스트에 찾는 에티티가 이미 있으면 em.getReference() 를 호출해도 실제 엔티티 반환

영속성 컨텍스트의 도움을 받을 수 없는 준영속상태일때 프록시를 초기화하지못하는 문제 발생
org.hibernate.LazyInitializationException: could not initialize proxy [hellojpa.Member#1] - no Session

------------------------------

프록시 인스턴스의 초기화(실제엔티티 주소참조지정) 여부 확인

emf.getPersistenceUnitUtil().isLoaded(프록시객체)

프록시 클래스 확인 방법
프록시객체.getClass().getName() 출력(..javasist.. or HibernateProxy...)

프록시 강제 초기화
Hibernate.initialize(프록시객체); (org.hibernate.Hibernate.initialize)

참고: JPA 표준은 강제 초기화 없어서 아래처럼 아무 get메소드를 써야함
프록시객체.getXXX()

----------------------------------------------------------------------------------------------------

엔티티 A를 조회할때 엔티티 B도 같이 조회 해야할까?

지연로딩 LAZY 를 써서 프록시로 조회 가능

@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "TEAM_ID")
private Team team;

위처럼 하면 team을 프록시로 조회함

member.getTeam()을 했을때는 프록시객체를 가져오고
이때 member.getTeam().getClass() 로 프록시 객체를 출력해 확인해 볼 수 있음
member.getTeam().getXXX() 뭔가 게터를 쓰거나 Hibernate.initialize(member.getTeam()) 를 쓰는 순간
Team테이블에 대한 select쿼리가 나가면서 프록시객체가 초기화가 됨


반면에 즉시로딩은 A를 조회할때 B까지 join으로 같이 가져옴

Member를 조회할때는 거의 Team을 항상 같이 조회한다 → EAGER
Member와 Team을 거의 같이 조회하지않고 Member만 조회하고 Team은 어쩌다가 조회함 → LAZY

가급적 모든 연관관계에서 지연 로딩만 사용
실무에서 즉시 로딩을 사용하지 말것

즉시 로딩은 JPQL에서 N+1 문제를 일으킴 (EAGER로 설정해도 select쿼리가 두번 나감 (join이 안됨) )
em.find() 는 PK를 찾아서 가져오는거기때문에 JPA가 내부적으로 최적화를 할 수 가 있으나, JPQL은 그대로 sql로 번역이 되기 떄문에
List<Member> select_m_from_member_m = em.createQuery("select m from Member m", Member.class).getResultList();
위 JPQL을 실행하면 Member만 가져오게 됨. 가져오고 보니 Member 클래스 필드의 Team이 즉시로딩(EAGER) 이다?
그러면 Member의 개수만큼 Team을 가져오기 위한 아래와 같은 쿼리가 별도로 나감. 언제? → 즉시
select * from Team where TEAM_ID = XXX

N + 1 인 이유는
결과 행이 N , 처음 쿼리를 날린 횟수 1

@ManyToOne, @OneToOne 은 기본이 즉시로딩 (~toOne)
@OneToMant, @ManyToMany 는 기본이 지연로딩 (~ToMany)

----------------------------------------------------------------------------------------------------

영속성 전이(CASCADE)

특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶을때

ex) 부모 엔티티를 저장할 때 자식 엔티티도 함께 저장

Child child1 = new Child();
Child child2 = new Child();

Parent parent = new Parent();
parent.addChild(child1);
parent.addChild(child2);

em.persist(parent);
em.persist(child1);
em.persist(child2);

원래는 이렇게 persist를 3번 해야되는데
Parent를 중심으로 코드를 짜고싶다, Parent를 persist할때 Child도 persist됐으면 좋겠다 할때

em.persist(parent);
만 쓸 수 있게 하기 위한게 cascade이다

@OneToMany 속성에
@OneToMany(mappedBy = "parent", cascade = CascadeType.ALL)
ALL이라고 넣으면 Parent만 persist해도 (casecade로 선언한 컬렉션(List) 안에 있는) Child들까지 persist됨

------------------------------

영속성 전이는 연관관계를 매핑하는 것과 아무 관련이 없음

엔티티를 영속화할 때 연관된 엔티티도 함께 영속화 하는 편리함을 제공할 뿐

------------------------------

CASECASE의 종류

ALL : 모두 적용 (라이프 사이클 다 맞출거면 이걸로)
PERSIST : 영속 (삭제하면 안될때, 저장할때만 라이프사이클 맞출거면 이걸로)
REMOVE : 삭제
MERGE : 병합
REFRESH: 리프래쉬
DETACH : 분리

------------------------------

써도 되는 경우 : 하나의 부모가 자식들을 관리할떄 ( = 소유자가 하나일때 )

ex) 게시판에서 첨부파일테이블의 데이터 (첨부파일의 경로가 들어있는)
첨부파일들은 하나의 게시물에서만 관리하기때문


쓰면 안되는 경우 : 파일을 여러군데에서 관리할떄. 다른 엔티티에서 관리할때 (이때는 운영이 너무 힘들어짐)

ex) Child1을 Parent1에서만 말고 다른데서도 쓸때


단일 엔티티에 완전히 종속적일 때만 쓰기

----------------------------------------------------------------------------------------------------

고아 객체

고아 객체 제거 : 부모 엔티티와 연관관계가 끊어진 자식 엔티티를 자동으로 삭제 (고아가 되면 지워지는 것)

참조가 제거된 엔티티는 다른곳에서 참조하지 않는 고아 객체로 보고 삭제하는 기능

@OneToMany(orphanRemoval = true)
private List<Child> childList = new ArrayList<>();

Parent parent1 = em.find(Parent.class, id);
parent1.getChildren().remove(0); // 자식 엔티티를 컬렉션에서 제거함

그러면 DELETE 쿼리가 나감
DELETE FROM CHILD WHERE ID=?


참조하는 곳이 하나일 때 사용해야함!

특정 엔티티가 개인 소유할때 사용

@OneToOne, @OneToMany만 가능

참고: 개념적으로 부모를 제거하면 자식은 고아가 된다. 따라서 고아 객체 제거 기능을 활성화 하면, 부모를 제거할 때 자식도 함께 제거된다
이것은 CascadeType.REMOVE처럼 동작한다


ex)
Child child1 = new Child();
Child child2 = new Child();

Parent parent = new Parent();
parent.addChild(child1);
parent.addChild(child2);

em.persist(parent);

em.flush();
em.clear();

Parent parent1 = em.find(Parent.class, parent.getId());
parent1.getChildList().remove(0);

----------------------------------------------------------------------------------------------------

종속되지않고 스스로 생명주기를 관리하는 엔티티라면 em.persist()로 영속화, em.remove()로 제거할 수 있다

그런데 영속성 전이(cascade) & 고아 제거(orphanRemoval) 두 옵션을 같이 쓴다면?
@OneToMany(mappedBy = "XXX", cascade = CascadeType.ALL, orphanRemoval = true)

cascade와 orphanRemoval을 모두 활성화 한 상태라면 부모 엔티티를 통해서 자식의 생명주기를 관리할 수 있음

도매인 주도 설계(DDD)의 Aggregate Root개념을 구현할 때 유용

----------------------------------------------------------------------------------------------------

com.querydsl.jpa.impl.JPAQueryFactory 의 .select(...)와 .selectOne(...)의 차이

.selectOne(...) : 단일 필드 선택할때 씀
.select(...) : 여러 필드 선택할때 씀

------------------------------

.fetchOne() : 단일 레코드 선택할때 씀
.fetch() : 여러 레코드 선택할때 씀

----------------------------------------------------------------------------------------------------




































