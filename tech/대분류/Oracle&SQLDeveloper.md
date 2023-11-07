ORA-06550: 줄 1, 열282:PLS-00905: HEALTH.EDIT_MY_INFO 오브젝트가 부당합니다
커서 안잡고 CTRL+ENTER을 눌러서 전체실행되는 에러가 났는데 이때 프로시저 실행하면 이렇게 뜸. 프로시저 다시 만들어야(컴파일해야)함

java.sql.SQLException: ORA-06550: 줄 7, 열3:PLS-00103: 심볼 ")"를 만났습니다 다음 중 하나가 기대될 때: ( - + case
mybatis xml에 ,(쉼표) 잘못 썼을때 발생

Caused by: org.springframework.beans.factory.BeanCreationException: 
Error creating bean with name 'memberMapper' defined in file [D:\ws\.metadata\.plugins\org.eclipse.wst.server.core
\tmp2\wtpwebapps\healthAssistor\WEB-INF\classes\com\fitper\mapper\MemberMapper.class]: 
Invocation of init method failed; nested exception is java.lang.IllegalArgumentException: org.apache.ibatis.builder.BuilderException: 
Error parsing Mapper XML. The XML location is 'com/fitper/mapper/MemberMapper.xml'. 
Cause: org.apache.ibatis.builder.BuilderException: Error resolving JdbcType. Cause: java.lang.IllegalArgumentException: 
No enum constant org.apache.ibatis.type.JdbcType.NUMBER
자료형 틀린경우

----------------------------------------------------------------------------------------------------

함수모음

★round - 반올림 함수 (엑셀 round)
- number round round(컬럼명) - 정수
- number round round(컬럼명,소수자리수) - 실수
- number round round(컬럼명,0) - 정수

★floor,trunc - 내림(버림/절삭)함수
floor(값) - 정수 내림
trunc(값,소수자리수) - 실수 내림

★ceil - 올림 함수
ceil(값) - 정수 올림

★trim / ltrim / rtrim - 양끝공백 제거 함수 , 한쪽만 제거 가능

★lpad / rpad - padding함수 
- lpad(값,총 자리수,'채울 문자')
- 총 자리수보다 값이 길면 내용이 짤림(주의)

★length - 문자열 길이
length(ID)
select first_name, length(first_name) from employees where length(first_name)>8; --where절에 이용
select first_name, length(first_name) from employees order by length(first_name) desc; --order by절에 이용

★upper,lower - 대소문자 변환 (=엑셀)
검색율 향상에 이용

★substr - 문자열 추출 (=엑셀mid)
substr(ID,2)	2글자부터 끝까지
substr(ID,2,4)	2글자부터 4글자까지
substr(ID,-4)	뒤에서 4글자
substr(ID,-4,2)	뒤에서 4글자로 나온결과에서 앞에서 2글자

★instr - 문자열 검색 (=엑셀find랑 비슷 , =자바indexOf 비슷)
instr(ID,'im')
첫글자가 1
못찾으면 0 반환

★replace - 문자열 치환
replace(ID,'im','kim')
replace(replace(substr(ssn,8,1),1,'남자'),2,'여자')

★decode - 다중 문자열 치환
- replace와는 달리 값이 없을경우 '원본'이 아닌 'null'이 된다★
- replace와는 달리 찾는 값이 원본값과 모두 일치해야 바뀐다★
decode(값,'문자열','바꿀문자열','문자열','바꿀문자열',…)
select
    count(decode(job,'학생','1')) as 학생수,
    count(decode(job,'건물주','1')) as 건물주수
from tbladdressbook;

★sysdate 현재날짜 yy/mm/dd
round(sysdate - ibsadate) as 몇일차이인지

★months_between - 날짜 차이 월단위로 구하기
round(months_between(sysdate,ibsadate)) as 월차이

★add_months - 날짜 개월단위로 더하기/빼기
add_months(sysdate,2)
add_months(sysdate,-2)

----------------------------------------------------------------------------------------------------

★숫자 형식문자열 구성요소
9 : 숫자1개를 문자1개로 (빈자리는 버림)
0 : 숫자1개를 문자1개로 (빈자리 0)
$ : 통화 기호 표시(달러)
L : 통화 기호 표시(원) (정확히는 locale, 국가 통화기호를 표시함)
. : 소수점 표시
, : 자릿수 표시

★날짜 형식문자열 구성요소
yyyy , yy , month , mon , mm , day , dy , ddd , dd , d , hh , hh24 , mi , ss , am(pm)
select to_char(sysdate,'yyyy')from dual; --2020
select to_char(sysdate,'yy')from dual; --20

select to_char(sysdate,'month')from dual; --11월(풀네임)
select to_char(sysdate,'mon')from dual; --11월(약어)
select to_char(sysdate,'mm')from dual; --11 (★★★)

select to_char(sysdate,'day')from dual; --목요일(풀네임 ★★★)
select to_char(sysdate,'dy')from dual; --목(약어 ★★★)

select to_char(sysdate,'ddd')from dual; --331(1년중 몇일)
select to_char(sysdate,'dd')from dual; --26(이번달중 ★★★)
select to_char(sysdate,'d')from dual; --5(일주일중 ↔ 요일 ★★★)

select to_char(sysdate,'hh')from dual; --10 (시간 12시 표기★★★)
select to_char(sysdate,'hh24')from dual; --10 (시간 24시 표기★★★)
select to_char(sysdate,'mi')from dual; --04 (분 ★★★★★★★★★★mm이아니라 mi임 주의)
select to_char(sysdate,'ss')from dual; --18 (초 ★★★)

select to_char(sysdate,'am')from dual; --오전
select to_char(sysdate,'pm')from dual; --오전


★to_char

※기능1)날짜/시간→문자열 (날짜(또는컬럼),형식문자열)	(=엑셀text)

  ex)to_char(sysdate,'yyyy-mm-dd hh24:mi:ss')
  ex)to_char(sysdate,'#!@%mm-!@%&!@%=mi') → 날짜→문자 변환시 중간에 기호는 마음대로 넣을 수 있으나 숫자나 문자는 넣을수없음
					→ 때문에 '글자'|| 이렇게 사이에 붙여야함 숫자는 to_char 내에서 문자 넣기가 가능★

where ibsadate between '2010-01-01' and '2010-12-31';
  →  이렇게 하면 될 수도 있지만 된다고 해도 2010-01-01 00시 ~ 2010-12-30 23:59까지
    → 12월31일의 00시 이후 (1시 등)은 포함이 안됨. 그래서 이렇게 말고 to_date도 말고 to_char을 사용하기)
ex) select * from animal_outs where datetime between to_date('2016.03%27','yyyy,mm$dd') and to_date('2016.03-29','yyyy,mm.dd');


※기능2)숫자→문자열 (숫자(또는컬럼),형식문자열)	(=엑셀text함수)

select '"'||to_char(1000,'000')||'"' from dual; → "####"
정수자리 overflow되면 ###(샾)에러발생★★★ 그렇기때문에 엑셀처럼 말고 수동으로 자리수대로 적거나,
또는 넉넉하게 9나0을 많이 적으면 공백이 생기는데 이때 ltrim으로 공백 제거하기

select to_char(123456789,'999,999,999') from dual; → 123,456,789

select ltrim(to_char(80,'999')) || '점' from dual; → 80점

소수 이하는 overflow가 되도 오류는 안나고 반올림된다
to_char(345.678,'999.9')


★to_date() : 문자열(또는컬럼)→날짜
  ex) select to_date('2018.06,25-11:14','yyyy,mm,dd,hh24,mi,ss') from dual;
	날짜문자열은 구분기호를 뭘 쓰던 상관없음 (띄어쓰기도됨. &만아니면됨. 20000102 이렇게 8자리로 입력하면 구분기호를 아예 안써도 됨)
  ex) to_date('2022.1.5T4:49:00','YYYY/MM/DD"T"hh24:mi:ss')
	위처럼 중간에 기호가 아닌 문자로 구분되어있을경우 "구분문자열" 이렇게 큰따옴표로 감싸 넣으면 됨
  ex) select to_date(06,'dd') from dual; → 년,월은 현재 시간으로 들어가고 일자만 입력한대로들어감 , 시간은 00:00:00 으로 들어감

ex) 날짜 상관없이 09:00 ~ 19:59까지 조회
select * from animal_outs where datetime between to_date('09:00','hh24,mi') and to_date('19:59','hh24,mi')
  → 이런 식으로 to_date로 하는게 아님, ★특히 위처럼 년월일 등 지정을 안하면 현재(sysdate) 날짜를 기준으로 입력안한값이 지정되기때문에 안되고
  → 조건대상컬럼을 to_char로, 문자열로 만들어 그 값을 비교해야함
  → select * from animal_outs where to_char(datetime,'hh24mi') between 900 and 1959;
ex+) 시간별 조회
  select substr(to_char(datetime,'hh24mi'),1,2),count(*) from animal_outs where to_char(datetime,'hh24mi') between 900 and 1959
  group by substr(to_char(datetime,'hh24mi'),1,2) order by 1;

★to_mumber() : 문자열(또는컬럼)→숫자(=엑셀value함수) (자동으로 암시적 형변환되기때문에 1+'2'이것도 원래 가능, 때문에 잘 안쓴다)

----------------------------------------------------------------------------------------------------

sql 연습사이트 : https://www.jamjalee.com/oracle-tutorial-video/
오라클 연습사이트 : https://goodthings.tistory.com/9

★오라클(Oracle)
- 회사명, 제품명
- 데이터베이스(Database) → 데이터베이스 관리 시스템(Database Management System)
- 관계형 데이터베이스(Relational Database) → RDBMS


★다운로드

1.오라클
  - 데이터베이스
  - OracleXE112_Win64.zip (https://www.oracle.com/database/technologies/xe-prior-releases.html)
  - 11g Express Edition 다운 (Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production)
  - 대부분의 데이터베이스 프로그램들은 인터페이스 환경을 제공하지 않거나 CLI(Command Line Interface)환경으로만 제공한다.
  - 서비스 프로그램 (눈에안보이는 알맹이)
  - Win+R > "services.msc"
    - OracleServiceXE, OracleXETNSListener 두개가 실행되고있는지 확인

2. 클라이언트 툴
  - sqldeveloper-20.2.0.175.1842-x64.zip(https://www.oracle.com/tools/downloads/sqldev-downloads.html)
  - (눈에 안보이는 알맹이를 조작하는 GUI환경의 툴)


★관계형 DBMS 종류
1. Oracle
  - Oracle
  - 기업용
2. Ms-SQL
  - Microsoft
  - 기업용
3. MySQL
  - Oracle에 인수됨
  - 개인용 + 기업용
4. MariaDB
  - MySQL 기반
  - 무료
5. PostgreSQL
  - 개인용 + 기업용
  - 무료
6. DB2
  - IBM
  - 메인프레임(대규모)
7. Access
  - Microsoft
  - 개인용 + 소규모
8. 티베로
  - 티맥스(TMax)
  - 제우스(웹서버) → Apache Tomcat

★클라이언트 툴
1. SQL Developer
  - 무료
  - Oracle
2. Toad☆☆
3. SQLGate
4. DataGrip(JetBrain)
5. SQL*PLUS
  - 오라클 설치 시 같이 설치되는 클라이언트 프로그램
  - CLI

★오라클 버전
- Oracle 1.0 : 1977년
- Oracle 9i : internet
- Oracle 10g : grid ☆
- Oracle 11g : grid ☆☆
- Oracle 12c : cloud
- Oracle 18c : cloud ☆
- Oracle 19c : cloud

★오라클 에디션
1. Oracle Enterprise Edition (상용) , CPU무제한
2. Oracle Standard Edition (상용) , CPU 최대 4개 지원
3. Oracle Standard Edition One (상용) , CPU 최대 2개 지원
4. Oracle Personal Edition (상용)
5. Oracle Express Edition (상용, 무료) CPU 1개 지원, 데이터베이스 크기 11GB까지, 메모리 점유율 최대 1GB까지☆☆
, 소규모 회사 / 학습용, 개발자 입장에서 상용버전과 큰 차이가 없음


- OracleServiceXE
  - 데이터베이스
- OracleXETBSListener
  - 오라클과 클라이언트 프로그램을 연결해 주는 서비스
(둘다 services.msc에서 실행중 이여야함, 시작유형 수동으로 해놓으면 실행할때만 실행됨
중지누르면 종료되고 StopDatabase아이콘누른것과 동일, 시작누르면 다시 시작)


★ sql디벨로퍼에서 일단 system계정 먼저 등록
ctrl + n → 데이터베이스 계층 → 확인 → Name : localhost.system, 사용자 이름 : system, 비밀번호 : 오라클설치했을때비밀번호


★cmd 또는 sql디벨로퍼에서 계정추가하기 - 참고) https://m.blog.naver.com/PostView.nhn?blogId=isaac7263&logNo=221359434614&proxyReferer=http:%2F%2F210.91.57.208%2F
생성법 : cmd → sqlplus system/오라클설치했을때비밀번호 → Connected to~ 접속된거 확인 → create user 유저이름 identified by 비밀번호;
ORA-65096 - 오라클 12c 이후부터는 계정명앞에 c##을 붙여야 공통사용자 	생성,수정이 가능한데 이걸 해소하기위해
시스템계정으로 아래 코드 실행. 이후부터는 c##을 안붙여도 계정생성/권한수정이 가능하다
alter session set "_ORACLE_SCRIPT"=true;


db에 생성된 계정 확인 :
select * from all_users; --모든 계정에 대한 정보 확인
select * from dba_users; --모든 계정에 대한 정보 확인
select username from all_users; --모든 계정에 대한 이름 확인
select username from aba_users; --모든 계정에 대한 이름 확인

비밀번호 변경 : alter user 유저이름 identified by 새로운비밀번호;
권한 부여 : 관리자계정으로 접속 → grant 권한명 to 계정이름;
시스템 권한 종류 :
create user : 데이터베이스 유저 생성 권한
select any table : 모든 유저의 테이블 조회 권한
create any table : 모든 유저의 테이블 생성 권한
create session : 데이터베이스 접속 권한
create table : 테이블 생성 권한
create view : 뷰 생성 권한
create proced user : 프로시저 생성 권한
create sequence : 시퀀스 생성 권한
sysdba : 데이터베이스를 관리하는 최고 권한
sysoper : 데이터베이스를 관리하는 권한

★오라클 SEQ Developer에서 계정 불러오기
새접속 or 새 데이터베이스 접속
Name : IP주소.계정명
Name : 도메인.계정명
Name : 127.0.0.1
Name : localhost.system
사용자 이름 : system
비밀번호 : java1234
비밀번호 저장 : 체크O
호스트 이름 : localhost
포트 : 1521
SID : xe
모두 입력후 테스트버튼 누르면 창 좌측하단에 '상태:성공' 이라고 나옴(안나오면 프로그램제거 → 'McAfee' 삭제후 PC재부팅)
성공이라고 나왔다면 접속 버튼 클릭

★오라클에서 ststem계정으로 계정(사용자,user) 만들고 권한부여
create user [유저명] identified by [비밀번호]; --유저생성 (비밀번호 특수문자 넣을때는 ""로 묶기)
grant connect,resource to [유저명]; --권한부여
grant create view to [유저명]; --권한부여
alter user [유저명] account unlock; --락 해제 (안하면 ORA-01017)

alter user [유저명] default tablespace users quota unlimited on users; --테이블스페이스 메모리설정(12c 이상부터), 안하면 1kb도 insert할수없다 ORA-01950

----------------------------------------------------------------------------------------------------

글꼴 변경법
도구 → 환경설정 → 코드 편집기 → 글꼴 (D2Coding)

localhost.system아이콘에서 우클릭 → SQL워크시트 열기
워크시트 or 스크립트파일(*.sql)
오라클 데이터베이스에게 내릴 명령어를 작성하는 파일

Shift 방향키로 드래그 후 Ctrl + Enter : 드래그한영역만 실행
          or
f5 : 전체실행

-- 단일라인 주석
/**/ 다중라인 주석

★관계형 데이터베이스
- 데이터를 표형태로 저장/관리한다
- 데이터끼리의 관계를 표시한다
1. 데이터
  - 단편적인 정보
2. 테이블
  - 데이터의 입출력을 위한 데이터 구조
  - 표
3. 스키마
  - 테이블, 뷰 등이 저장된 데이터의 집합 저장소
  - 오라클(사용자 계정)
  - 사용자 게정을 새로 만들면, 오라클은 사용자가 취급할 자원들이 저장될 공간을 할당한다 (=스키마)
4. 데이터베이스
  - 여러개의 스키마의 집합 저장소
  - Oracle XE는 1개의 데이터베이스만 생성 가능
5. 열(Column)
  - 열(컬럼)-관계형데이터베이스, 필드(Filed)-파일시스템, 속성(Attribute)-모델링, 특성(Property)
  - 테이블의 열로 구성된다(=구조)
6. 행(Row)
  - 행(로우)-관계형데이터베이스, 레코드(Record)-파일시스템, 튜플(Tuple)-모델링
  - 테이블에 저장된 데이터 1건
  - 객체(Object)


클라이언트 툴 → 섭버 접속
1. 접속명
  - 자유롭게 가능
  - 서버주소.계정명
2. 사용자 이름
  - 접속할 계정명(아이디)
  - 관리자 계정 : sys, system, 우리가 만들 계정들..
  - 사용자 계정 : scott(tiger), hr(human resources), 우리가 만들 계정들..
3. 비밀번호
  - 주시적으로 변경
4. 호스트 이름
  - 오라클 서버 IP주소 or 도메인명
  - localhost(127.0.0.1) or 팀 서버 IP(211.63.89.31)
5. 포트번호
  - 1521 (보안상 다른걸로 변경한다)
  - 네트워크 프로그램이 외부와의 데이터 입출력을 위해서 사용하는 통로 번호
  - 65535
  - 독점
6. SID
  - Service ID
  - 오라클 서버 프로그램의 식별자
  - xe
  - orcl

sysytem 계정 안쓰고 hr 사용
권한이 있는 계정으로만 명령 가능(system)
1. 활성화 → alter user hr account unlock; 블럭후 실행
2. 비밀번호 변경 → alter user hr identified by java1234;

접속 → 새접속
Name:localhost.hr
사용자이름hr
비밀번호 java1234
테스트 → 성공 나오면 접속

접속창 사라졌을때
창 → 팩토리 설정으로 창 재설정

왼쪽에
localhost.hr
localhost.sysytem
둘다 접속되있나 확인

select * form tabs; --실행하면 50개

오른쪽 위에 localhost.hr로 바꾸고 다시 실행하면
select * form tabs; --7개

스크립트 파일은 사용자 계정에 종속적이지 않다


오라클 → 데이터베이스 → 클라이언트 툴 + 명령어(SQL)

SQL(Structured Query Language)
  - 구조화된 질의 언어
  - 사용자(클라이언트 툴)가 관계형 데이터베이스와 대화할때 사용하는 언어
  - 자바에 비해 자연어에 가깝다

1. DBMS 제작사와 독립적이다
  - SQL은 모든 DBMS제작사와 독립적으로 개발된다

2. 표준 SQL(ANSI SQL)
  - 표준 SQL발표 → 각 DBMS제작사에서 자기 제품에 적용
  - SQL은 모든 DBMS에 호환된다
  - SQL-86... SQ-92... SQL2011

3. 대화식 언어이다
  - 질문 → 답변 → 질문 → 답변 … 반복

1. ANSI SQL
  - 표준 SQL
2. PL/SQL
  - 오라클에서만 적용되는 명령어 (다른DBMS에서는 사용불가)


★ANSI SQL 종류
1. DDL : Data Definition Language
  - 데이터 정의어
  - 테이블, 뷰, 인덱스, 트리거, 프로시저, 제약사항, 유저 등의 객체를 생성/수정/삭제하는 명령어
  - create 생성 / drop 삭제 / alter 수정
  - 데이터베이스 관리자 / 데이터베이스 담당자가 사용 , 프로그래머는 일부회사(db파트부서가 없는회사)에서 사용

2. DML : Data Manipulation Language ★★★
  - 데이터 조작어
  - 데이터베이스의 데이터를 추가/수정/삭제/조회하는 명령어
  - select 읽기★/ insert 추가 / update 수정 / delete 삭제
  - 데이터베이스 관리자 / 데이터베이스 담당자가 사용 , 프로그래머

3. DCL : Data Control Language
  - 데이터 제어어
  - 계정, 보안, 트렌젝션 등을 제어
  - commit / rollback / grant / revoke
  - 데이터베이스 관리자 / 데이터베이스 담당자가 사용 , 프로그래머는 잘안쓴다

4. DQL : Data Query Language
  - DML중에 select만을 부른다

5. TCL
  - DCL중에 commit, rollback만을 이렇게 부른다

6. CRUD(Create, Update, Read, Delete)
  - 가장 많이 사용하는 네가지를 이렇게 부른다


★테이블 생성
create table tblMemo(
   컬럼명 자료형(길이) [제약사항],
   …
);


★제약사항(Constraint)
- 해당 컬럼에 들어갈 데이터(값)에 대한 조건(규제)
- 조건을 만족하지 못하면 에러를 발생시킨다 = 유효성검사 도구
not null - 필수값
primary key(PK) - 기본값 (기본값이 없는 테이블은 생성할 수는 있지만 문제가 많다)
  - 단일 기본키(기본키) → 1개의 컬럼이 PK역할
  - 복합 기본키(복합키) → 2개 이상의 컬럼이 모여서 PK역할
  - 중복값 가질수없음
  - null값 가질수없음 (not null 안적어도 된다)
foreign key - 외래키
unique - 중복X , null값을 가질 수 있음 , 식별자로 사용불가(null때문에)
check - where절에서 사용했던 조건 =선택쿼리
default - ex)default 기본값 , 설정하면 insert로 값을 넣지 않아도 자동으로 기본값이 들어간다

1.컬럼수준에서 정의 - 컬럼을 만들때 제약사항도 같이정의
create table tblMemo(
	seq number primary key,
	staff number not null references tblstaff(seq),
	gender check(gender='M' or gender='F')
}

2. 테이블수준에서 정의 - 컬럼을 다 만들고 제약사항만 따로 분리해서 정의 (not null은 컬럼수준에서밖에 걸지못함)
create table tblMemo(
	seq number(3),
	name varchar2(30),
	seqBook number,

	constraint tblmemo_seq_pk primary key(seq),
	constraint tblmemo_memo_ck check(length(memo)>20),
	constraint tblmemo_mame_uq unique(memo)
	CONSTRAINT tblBasicSubject_seqBook_fk FOREIGN KEY(seqBook) REFERENCES tblBook(seqBook)
	--seqBook를 외래키로 지정하고, tblBOOK라는 테이블의 seqBook를 참조
)

3. ALTER TABLE로 정의
ALTER TABLE MEMBER_TL
	ADD
		CONSTRAINT PK_MEMBER_TL
		PRIMARY KEY (
			MEMBER_SQ
		);

제약사항 확인법
SELECT * FROM    ALL_CONSTRAINTS
WHERE    TABLE_NAME = '테이블명';

복합키 만들기
create table tblScore(
    num number,             --학번
    subject varchar2(50),   --과목
    name varchar2(50),                  --이름
    score varchar2(2),                  --성적
    constraint tblscore_num_subject_pk primary key(num,subject) --복합키(Composite Key)
);

★FK 걸려있어도 (자식이 있어도) 강제삭제 (권장안함)
drop table 테이블명 cascade constraints purge; //puarge는 휴지통(recyclebin)으로 보내지말고 완전삭제

★레코드(튜플/행) 추가
insert into 테이블명(컬럼명,컬럼명,컬럼명…) values (값,값,값…);

insert into tblMemo(seq,name,memo,regdate) values (seqMemo.nextVal,'아이린','메모입니다ddd',null); --명시적 null대입(default값이있을때도 null저장)
insert into tblMemo(seq,name,memo) values (seqMemo.nextVal,'아이린','메모입니다ddd'); --암시적 null대입(default값이있으면 default값저장)

insert into tblMemo(seq,memo) values (seqMemo.nextVal,'메모입니다ddd'); --default값 넣기 1번째방법(아예 비운다)
insert into tblMemo(seq,name,memo) values (seqMemo.nextVal,default,'메모입니다ddd'); --default값 넣기 2번째방법(default상수)

insert into tblMemo values (seqMemo.nextVal,default,'메모입니다ddd');
컬럼리스트를 생략하려면 반드시 값리스트는 테이블 컬럼순서대로만 작성해야한다 , 값리스트를 비울 수 없다. (=편할것같지만 불편함)

insert into tblMemoCopy select * from tblMemo; --복사된 테이블을 만들고, 실행하면 복사된다

create table tblComedianMale
as select * from tblComedian where gender='m'; --제약사항이 복사가 안된다(테스트시만 사용)★


★update문 - 원하는 레코드의 원하는 필드(컬럼)값을 수정
- update 테이블명 set 컬럼명 = 수정할 값;
- update 테이블명 set 컬럼명 = 수정할 값 [, 컬럼명 = 수정할 값]*N [where절];
- where절에서 되도록 중복값이 없는 기본키로 제어하기
- 일할때 가장 중요한것 where절 확인★★★★★★★★★★(백업필수)
- PK는 되도록 수정하지 말것 (수정한다면 연관되어있는 모든데이터를 수정해야한다)
- UPDATE [테이블] SET [열] = '변경할값' WHERE [조건]
- ex) update tblCountry set area=area+10,POPULATION=POPULATION*1.2 where name='대한민국';

★delete - 레코드(행/튜플) 삭제
- delete [from] 테이블명 [where절]		//(오라클은 "from"을 생략 가능, mariaDB는 생략 불가능)
- where절 확인★★★★★★★★★★
- where절에서 되도록 중복값이 없는 기본키로 제어하기
- ex) delete from tblcountry where name='대한민국';

★테이블의 데이터를 모두 삭제해야하는경우
1. drop (테이블까지 삭제)
  - DDL
  - 주로 많이 사용된다
  - 상황에따라 더 힘들어지는 경우가 발생(테이블 관계 형성시
  - 독립된 테이블에 적용
  - ex) drop table tbltemp;
2. where절 없는 delete
  - DML
  - 트렌젝션 로그가 남는다 (지워도 되나 확신이 안될때 사용)
  - 확신을 못할때
  - ex) delete from tbltemp;
3. truncate
  - DDL
  - 트렌젝션 로그가 안남는다 (지워도 된다 확신이 들때, 다른사람이나 누군가가 되돌리면 안될때 사용)
  - ex) truncate table tblTemp;

★rollback; - 되돌리기

★commit; - 저장하기

★group by절(=엑세스에서 그룹화)
- 레코드들을 특정 컬럼값(1개 or 그 이상)을 기준으로 그들을 나누는 역할
- 나눠진 그룹에 각각 집계함수를 적용하기 위해서(count/sum/agv/max/min)
- group by 사용시 select 뒤에는 '집계함수(컬럼명)' 만 올 수 있다★
- ex) select buseo,count(*),avg(basicpay),sum(sudang) from tblinsa group by buseo;
- 위 예시에서 buseo컬럼은 그룹화의 대상인 항목이기때문에 집계함수없이 단독으로 불러오기가 가능함, 나머지는 불가
-ex)
select
    case
        when substr(ssn,8,1)=1 then '남자'
        else '여자'
    end,
    count(*)
from tblinsa group by substr(ssn,8,1);
그룹의 기준으로는 컬럼의내용말고 연산,함수의 결과도 가능함

-ex)
select
    to_char(ibsadate,'yyyy'),
    count(*)
from tblinsa group by to_char(ibsadate,'yyyy') order by to_char(ibsadate,'yyyy');

ex)
select
    round(weight / 10)*10||'kg',
    count(*)
from tblAddressBook
group by round(weight / 10);

ex)
select * from tblinsa;
select jikwi,count(*) from tblinsa where buseo='개발부' group by jikwi order by
case
    when jikwi='사원' then 1
    when jikwi='대리' then 2
    when jikwi='과장' then 3
    when jikwi='부장' then 4
end desc;

ex)
select
    buseo,
    count(*),
    count(decode(jikwi,'부장',1)) as 부장,
    count(decode(jikwi,'과장',1)) as 과장,
    count(decode(jikwi,'대리',1)) as 대리,
    count(decode(jikwi,'사원',1)) as 사원
from tblinsa
group by buseo;

ex) 2차(n차)그룹
select
    buseo,
    jikwi,
    count(*) as 인원
from tblinsa
group by buseo,jikwi
order by buseo;

★having절
- 그룹화된 집계결과에서 출력된 '결과컬럼'을 대상으로 또 조건을 걸고 싶을때 씀
- 집계결과가 아닌 컬럼을 HAVING절에서 쓸 수는 있으나 그럴거면 WHERE절에 넣는게 더 효율적임

ex) select buseo,count(*) as 인원수 from tblinsa where city='서울' group by buseo having count(*)>5;
해설) tblinsa테이블에서 city가 서울인 부서 컬럼을 가져와 개수로 그룹화시키고 그 그룹의 총개수가 5개 이상인것만 출력

ex) Alias
SELECT SUM(TRUE) AS C1
FROM TGPR_LOG
WHERE STATS_DIV_CD=4
GROUP BY COOKIE_VAL
HAVING C1 > 3

ex) Alias 를 안쓰고 그대로 집계함수를 써도 됨
SELECT SUM(TRUE)
FROM TGPR_LOG
WHERE STATS_DIV_CD=4
GROUP BY COOKIE_VAL
HAVING SUM(TRUE) > 3


★listagg (오라클만 지원(PL/SQL)) - 그룹안에있는 값을 가져옴 (dustinct불가)
ex)
select
    buseo,
    listagg(name,',')within group(order by name asc) as name
from tblinsa
group by buseo;

ex)
select
    buseo,
    listagg(name,',')within group(order by name asc) as name,
    listagg(jikwi,',')within group(order by name asc) as jikwi
from tblinsa
group by buseo;


★select문
- DML , DQL
- 사용 빈도가 가장 높다.
- 데이터베이스로부터 원하는 데이터를 가져오는 명령어(읽기)

문법 [] : 생략가능하다는뜻
[whit <sub query>]
select 컬럼명 → 컬럼끼리의 구분은 쉼표로
from 테이블이름
[where 검색조건]
[group by 그룹대상]
[having 그룹검색조건]
[order by 정렬대상 [asc | desc]]

select 컬럼리스트
from 테이블
-----이하부터 생략가능-----
where 절
group by 절
having 절
order by 절

★조건절 연결
from절 = where절
group by절 = having절

★select를 구성하는 모든 절들은 실행 순서가 있다
form절 → where절 → group by절 → having by절 → select절 → order by절
form절 : 데이터를 가져올 테이블을 지정한다
where절 : 행(레코드)으로 걸러내는 필터역할
select절 : 가져올 테이블의 컬럼을 지정한다 (지정된 컬럼만 갖고온다)
group by절 : 행들을 소그룹화
having by절 : 그룹핑된 값에서 조건에 맞는것만 추출
order by절 : 출력된 결과값을 조건에 맞게 정렬한다, 컬럼 index로 정렬가능

★테이블 구조를 보는방법
1. SQL Developer 기능 사용
2. desc 테이블명
3. 스크립트(SQL)

★현재 오라클에만들어져있는 모든 계정목록
select * from sys.dba_users;
system으로 실행

★SQL은 대소문자를 구분하지 않는다 (오라클은 식별자를 저장할때 모두 대문자로 변환해서 저장한다)
관습화 패턴 → 프로젝트 내 결정 ex)키워드-대문자, 식별자-소문자
SELECT * FROM tabs;

★대소문자 일괄변경 → Alt + ' (홑따옴표)
계속 눌러 아래 순서대로 형식을 전환할 수 있음 (카멜표기/파스칼표기 등 구분없이 그냥 통일됨, '값'은 제외하고 바뀜)
1. 모두 소문자
2. 키워드-대문자, 식별자-소문자
3. 키워드-소문자, 식별자-대문자
4. 키워드-대문자, 식별자-소문자 (=3번)
5. 첫글자 대문자 나머지 소문자
6. 모두 대문자

★select문 컬럼명 *안쓰고 하나하나 가져올때
컬럼명 직접 타이핑하지말고 select결과에서 '선택된 열 멀머리글 복사' 이용해서 복붙 (혹은 ERD에서 복사해오거나)

★오라클 기본 인코딩
- ~8i버전 : EUR-KR
- 9i버전 ~ : UTF-8

★사용자 식별자 생성 시 주의점 : 최대 30byte 이하
create table aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa(
	num number
);

오라클에서는 문자열결합 연산자를 + 대신 || 로 한다 ex↓
select name,'국가명:' || name , length(name)
from tblCountry;

★에러메세지 나올시 코드명으로 검색
ORA-00904: "GENDER222": invalid identifier → ORA-00904 검색

★ANSI-SQL 자료형
1. 숫자형
  a. number★
    - 정수 + 실수
    - (유효자리) 38자리 이하의 숫자를 표현하는자료형
    - 5~22byte
    - 1*10-130 ~ 9.9999*10+125 (거의무한)
    - number(precision,scale)
      1.precision : 소수 이하를 포함한 전체 자릿수(1~38)
      2.scale : 소수점 이하 자릿수(0~127자리)
      - ex)number : 유효자리 38자리까지 표현가능 모든 숫자(정수,실수)
      - ex)number(3) : 3자리까지 표현 가능 숫자(정수,-999~999)
      - ex)number(5,2) : 5자리까지 표현 가능 숫자(실수, -999.99~999.99)

2. 문자형
  - 문자형 + 문자열
  - 자바의 String과 유사
  a. char
    - 고정 자릿수 문자열
    - char(n) : n바이트 문자열
    - 최소크기 : 1바이트
    - 최대크기 : 2000바이트
    - ex) char(2000) : 최대 2000바이트 문자열을 저장 (영어2000자 , 한글666자 utf-8이라서) (영어는1바이트 한글은3바이트)
    - 고정 자리수(최대자리수가 10바이트인데 3바이트를 넣어도 무조건 10바이트 , 바차2보다 속도빠름 , 저장공간많이 소모)
    - 데이터 길이가 고정인 경우 사용 : 사람이름 , 성별
  b. varchar2★(오라클의 바차2가 다른언어의 바차와 동일)
    - variable charactor2 (바차2)
    - char과 동일
    - 최대크기 : 4000바이트
    - 가변 자리수(최대자리수가 10바이트인데 3바이트를 넣으면 나머지는 버림 , 속도느림(but 요즘엔 속도빠름) , 저장공간 적게소모)
    - 데이터 길이가 가변인 경우 사용 : 주소 , 인삿말
  c. nchar
    - n : national → 유니코드 지원 → UTF-16으로 동작
    - nchar(n) : n글자 문자열
    - 최소 크기 : 1글자(2바이트)
    - 최대 크기 : 1000글자(2000바이트)
    - ex) nchar(3) : 영어(3글자) , 한글(3글자) (영어든 한글이든 2바이트)
    - 영어위주떄는X 한글위주때는O
  d. nvarchar2
    - varchar2와 동일
    - 바이트X 문자수O
  e. clob, nclob (잘 안씀)
    - 롭
    - large Object
    - 대용량 텍스트 저장
    - 128TB
    - 참조형

3. 날짜/시간형
  a. date★
    - 년월일시분초
    - 기원전 4712년 1월 1일 ~ 기원후 9999년 12월 31일
  b. timestamp
    - 년원일시분초+밀리초/나노초
  c. interval → number 사용
    - 시간
    - 틱값

4. 이진 데이터형(잘안씀)
  - 비텍스트형 데이터
  - 이미지, 영상, 음악 등..
  - 인코딩/디코딩 발생하므로 해당 파일을 특정 폴더에 저장 + 데이터베이스에는 파일명만 저장
  a. blob
    - 최대 128TB
잘 안쓰는 이유는 호스팅(렌트)시
- 웹 호스팅
- 서버 호스팅
- 클라우드 호스팅
파일저장용량 → 1TB → 월1만원
- DB 호스팅  → 100MB → 월1만원 (비싸다)

-----

모든 테이블 조회
SELECT * FROM ALL_TABLES; (관리자일 경우)
SELECT * FROM USER_TABLES; (관리자 아닐 경우)
SELECT * FROM TAB; (관리자 아닐 경우)
SELECT * FROM ALL_TABLES WHERE OWNER = 'PROJECT'; 이렇게 해도 됨

소유자(OWNER) 조회
SELECT * FROM ALL_TABLES WHERE OWNER LIKE '%OWNER명%';

테이블명 포함 된 조회
SELECT * FROM USER_TABLES WHERE TABLE_NAME LIKE '%테이블명%'; 

테이블스페이스 이름으로 조회
SELECT * FROM USER_TABLES WHERE TABLESPACE_NAME LIKE '%테이블스페이스명%';

-----

테이블의 자세한 목록
select * from sys.dba_tab_columns where owner = 'HR' and table_name = 'TBLCOUNTRY'; 를 줄이면
→ desc tblCountry;

★count(*) 모든 행을 다 카운트한다, 레코드의 모든 속성이 null이여도★카운트한다(null을 포함시켜 카운트를 얻고싶을때 여기서 뺀다)
  null을 포함하지 않고싶을때는 count(컬럼명) 또는 where 컬럼명 is not null

★테이블의 컬럼목록 궁금할때

1. select * from tblCountry; 이렇게 다 불러와서 보거나

2. desc tblCountry; 이렇게 구조를 보거나

3. from절을 먼저 적고 위에 'select '까지 적고 ctrl+space를 누르면 해당 테이블의 컬럼들이 나온다
select (여기서 ctrl+space)
from tblCountry;


★현재 날짜
sysdate

★산술 연산자
+ , - , * , /
나머지는 %가 아닌 mod

★문자열 연산자
문자열 + 문자열 X
문자열 || 문자열 O
name||'님'

★비교 연산자
> , >= , < , <= , = , <> , != , ^= (!= , ^= 은 <>로 자동 변환된다)
ANSI-SQL에는 논리 자료형이 없어서 표현 불가능 → select의 결과로 사용할 수 없고→where에서 사용가능

★논리 연산자
and , or 마찬가지로 where에서 사용가능

★대입 연산자
컬럼에 값을 넣을때 사용
update문에서 사용(추가,수정)

★SQL 연산자
in , between , like , is , any , notin , some , exists

3항 연산자 , 복합 대입 연산자 , 증감 연산자 등은 없음 → 제어 흐름이 없기때문에(문장 단위의 독립실행이기 때문에)

★(null) : 결과없음

★행개수 세기
select count(*) from tblCountry;


★컬럼명 별명 붙이기 (Alias)

연산이나 함수처리가 된 컬럼은 표현식 자체가 컬럼명이 된다
때문에 유효한 식별자로 수정(컬럼명의 별칭을 만들기)해야 한다
컬럼의 별칭, 테이블의 별칭은 선택이 아닌 개명이다, 무조건 별칭으로 사용해야함 ★ex) select name,item,c.seq,s.seq from tblcustomer c cross join tblsales s;

select name,weight,weight+10 from tblMen;
select name,weight,weight+10 as 증가된몸무게,age from tblMen;

띄어쓰기,기호등 삽입시에는 "(쌍따옴표)를 붙이면되긴하는데, 이런 행동은 유효성을 떨어뜨리는 행위이므로 사용 금지
프로그램으로 java나 oracle이 읽을 수 있도록 ★절대사용금지
select name as 이름,weight as "몸무게(kg)" from tblMen;


★where 레코드 필터 (엑세스에서 쿼리 → 조건)

select name from tblCountry where AREA>=100;
select * from tblInsa where CITY='서울' and BUSEO='기획부'; --and/or 연산
select * from tblInsa where basicpay + sudang >=2000000 and city='서울';
select name from tblInsa where name like '한%'; --like 연산 (시작/중간/끝글자)
select * from tblInsa where ssn like '%-2%';--like 연산 (중간에 -2가 껴있을경우
select name from tblInsa where name like '한__'; --like 연산 (글자수 지정)
select name from tblInsa where name like '_가_'; --like 연산 (글자수 지정)
select * from tblInsa where basicpay between 1000000 and 2000000; --between 연산 (첫값,끝값 모두포함 / and연산자보다 가독성 향상 / 속도는 더 느림)
select * from tblInsa where JIKWI in('부장','대리'); --in 연산
select * from tblInsa where name > '한가인'; --문자코드값 비교
select * from tblInsa where ibsadate > '2010-01-01'; --날짜비교
select * from tblInsa where city in('서울','인천','경기') and substr(ibsadate,0,2) between '08' and '10%' ;

★like연산 - 부분 일치 검색 (not을 붙여도 null은 안찾으므로 null까지 구하고싶으면 전체count(*)에서 조건의 반대를 빼기)
like '%d'
like 'd%'
like '%d%'
like '_d__s_'

★null
- null상수로 직접 표현 가능
- 오라클및 대다수의 언어에서 null은 피연산자가 될 수 없다
- is null / is not null 이용
- ex) select * from tblCountry where population is null;
- ex) select * from tblCountry where population is not null;
- ex) select * from tblCountry where not population is null; (이렇게도 이용 가능)

★distinct - 중복값 레코드 제거
- 컬럼 리스트에서 사용
- distinct 컬럼명
- ex) select distinct buseo from tblInsa;
- ex) select distinct buseo,jikwi from tblInsa; n개의 데이터를 중복제거 하였을경우, n개의 데이터를 하나로 합친다음 모두 중복일때만 제거함
- ex) select distinct * from tblInsa; 모두 중복되면 제거 (모두중복되지않았을경우 제거가 안됨)

★if문
IF 조건 THEN
	처리문
ELSIF 조건2 THEN
	처리문
ELSE
	처리문
END IF;

★case문 (엑세스에서 쿼리 → 필드추가)
- 컬럼 리스트에서 조건을 주고싶을때 사용
- 자바에서의 switch
- 조건에 맞으면 then뒤에있는값을 반환
- 조건을 만족하지 못하는 행은 null을 반환★
- 같은 자료형을 반환시키도록 만들어야함
select
    name,
    case
        when continent = 'AS' then '아시아'
        when continent = 'EU' then '유럽'
        when continent = 'AF' then '아프리카'
        else continent --'else 기타'
    end as 지역
from tblCountry;

case부터 end 까지가 조건에 맞는 결과로 치환된다
else '기타' 
상수 대신
else continent 이런식으로 column제목을 입력하면 원본값이 나옴
then이나 else 뒤에 =붙이지 말기★


★order by - 정렬 [asc|desc]
작성 순서 : select - from - where - order by

select * from tblCountry order by name desc;
select * from tblInsa order by buseo asc , jikwi desc; --여러개 정렬
select * from tblInsa order by 2 asc , order by 1 asc , order by 3 asc; --컬럼제목대신 열번호 사용가능★★★
select * from tblInsa order by (basicpay+sudang) desc; --더한값으로 정렬

직급별 등으로 정렬 시 이런식으로 새로운 정렬용 속성(열)을 만들고
select name,jikwi,
    case	
        when jikwi = '부장' then 4
        when jikwi = '과장' then 3
        when jikwi = '대리' then 2
        when jikwi = '사원' then 1
    end as 직위순서
from tblInsa
order by 직위순서;

그걸로 정렬 가능

아래는 정렬용 열은 안보이게 order by절에 직접 case절 추가

select name,jikwi
from tblInsa
order by
case
    when jikwi = '부장' then 4
    when jikwi = '과장' then 3
    when jikwi = '대리' then 2
    when jikwi = '사원' then 1
end

-----

switch문 방식

SELECT
	ename
	, deptno
	, CASE deptno 
	WHEN 10 THEN
		'New York'
	WHEN 20 THEN
		'Dallas'
	ELSE 'Unknown'
	END AS loc_name
FROM scott.emp
WHERE job = 'MANAGER'

-----

★집계 함수 - 레코드들을 한군데 모아 결과를 구한다 (+ - * / mod 이런 연산자는 레코드 각각의 결과를 구하는거이므로 이거랑은 다르다)
count() / sum() / avg() / max() / min() (=엑셀)

select count(name) from tblCountry; --name의 레코드(행) 개수 (null은 카운트하지않는다 , null까지 계산하고싶으면 count(*)에서 조건의 반대(not)를 빼기)
select count(distinct buseo) from tblInsa; --부서의 종류수
select --count(*) as 전체인원수 ,
    count(
    case
        when gender='m' then 1
    end) as 남자수,
    count(
    case
        when gender='f' then 2
    end) as 여자수
from tblComedian;
--남자/여자 수

select count(*),sum(sudang),max(sudang),avg(sudang) from tblinsa; --집계함수끼리는 같이쓸 수 있다
select count(name),name from tblinsa; --집계함수 결과,레코드들 같이 출력 불가능
select * from tblinsa where basicpay>avg(basicpay); --where절에 집계함수 사용불가능

sum은 숫자형에만 적용가능(문자,날짜 X)

select
    sum(population) / count(population),avg(population), --균등(null을 포함안하고 평균을 구함)
    sum(population) / count(*) --차등(null을 포함하고 평균을 구함)
from tblcountry;

★집계함수만 where절, orderby절 등에서 이용 불가, 나머지함수들은 사용가능

★레코드 1개짜리 테이블 : dual - 무언가를 계산해볼때 이용 ex)select to_char(1203,'0,000') as 날짜 from dual;

★cmd에서 sql실행하는방법
sql있는폴더에서 shift+우클릭 → 여기서 명령창 열기(win10;여기에 PowerShell창 열기) → sqlplus 입력 → hr(=사용자아이디)입력
→ java1234(=비밀번호)입력 → sql 명령어 입력하면 그대로 실행가능 (@파일명.sql 엔터 치면 sql파일이 실행됨)


★테이블 검색
1. ALL_TABLES
- 로그인 된 계정의 권한으로 접근할 수 있는 모든 테이블들
- 예 ) 테이블명에 "테스트"를 포함한 테이블 검색 : 
  SELECT * FROM ALL_TABLES WHERE LIKE '%테스트%';

2. USER_TABLES
- 로그인 된 계정이 소유하고 있는 테이블들 
  SELECT * FROM ALL_TABLES WHERE OWNER = '로그인된계정' 과 같다.

3. ALL_TAB_COLUMNS
- 로그인 된 계정의 권한으로 접근할 수 있는 모든 테이블 내의 컬럼들
- 예 ) 컬럼명에 "테스트"를 포함한 컬럼 검색
  SELECT * FROM ALL_TAB_COLUMNS WHERE COLUMN_NAME LIKE '%테스트%'

4. USER_TAB_COLUMNS
- 로그인된 계정이 소유하고 있는 테이블들
  SELECT * FROM ALL_TAB_COLUMNS WHERE OWNER = '로그인된계정' 과 같다.


★시퀀스(Sequence) - 일련번호 기능 (my sql의 IDENTITY)
- 데이터베이스 객체 중 하나
- 식별자를 생성하는 역할(도구) → 주로 PK컬럼에서 많이 사용한다

시퀀스 생성하기
- create sequence 시퀀스명;

시퀀스 조회하기
- SELECT * FROM USER_SEQUENCES;

시퀀스 삭제하기
- drop sequence 시퀀스명;

시퀀스 사용하기
- 시퀀스명.nextVal : 다음 수 넣기
- 시퀀스명.currVal : 현재 시퀀스값 확인할때 사용(시퀀스 생성 초기에는 값이 없어서 에러남)

ex)
create sequence seqNum;
select seqNum.nextVal from dual;
select name, buseo, jikwi, seqNum.nextVal from tblinsa;

ex2)
create sequence seqProduct;
select 'A'||ltrim(to_char(seqProduct.nextVal,'000')) from dual;

이빠짐이 생길 수 있음. 이빠짐이 생기면 안되는 경우라면 시퀀스 말고 max()+1 이용

★시퀀스 리셋시키는 방법
1. 삭제후 재생성
2. alter sequence ~ (start with는 안됨)

★시퀀스 옵션
increment by N : 증감값(기본값1)
start with N : 시작값(기본값1)
maxvalue N : 최대값, 넘으면 에러
minvalue N : 최소값, 넘으면 에러
cycle : max/minvalue에 도달하면 시작값으로 돌아감 max
cache N : 20이 기본값이고 1~20→21 21~40→41  이런식으로 20개를 한번에 하드에서 가져온다 (속도향상을위해)
☆최대값이 20 이하일때 사이클 사용하려면 캐시를 먼저 20미만으로 바꿔야 가능 → create sequence seqScholarship cycle maxvalue 20 cache 19;
nocycle : 사이클 취소

★서브쿼리
메인쿼리 - 하나의 select(insert, update, delete)로만 구성된 쿼리
서브쿼리 - 메인쿼리에서 1개이상의 select를 추가한 쿼리
  - 삽입 위치 : select절, from절, where절, order by절
  - 가져온 데이터만 꺼내 사용할수있다(select할수있다)
SELECT절 서브쿼리(스칼라 서브쿼리) : 이 서브쿼리는 반드시 단일행을 리턴해야함, 집계함수(sum,count,min,max)가 많이 쓰임
FROM절 서브쿼리(인라인 뷰) : 뷰처럼 결과가 동적으로 생성된 테이블 형태로 사용할 수 있음
WHERE절 서브쿼리(중첩 서브쿼리)

★서브쿼리의 용도
  1. 조건절에서 비교값으로 사용
    a. 반환값이 1행 1열 → 스칼라 쿼리(행이1개,열이1개) → 단일값 반환 → 연산자 사용
        ex)급여를 가장 많이받는 사람정보 (& 맨 아래에 있는 모든 예제 포함)
        select * from tblinsa where basicpay = (select max(basicpay) from tblinsa);
    b. 반환값이 n행 1열
        ex)급여를 260만원 이상 받는 사람이 근무하는 부서의 모든 직원 명단
        select * from tblinsa where buseo in(select buseo from tblinsa where basicpay>=2600000);
    c. 반환값이 1행 n열
        ex)'박수진'과 같은 지역에 거주+'박수진'과 같은 부서 사람
        select * from tblinsa where city=(select city from tblinsa where name='박수진') and buseo=(select buseo from tblinsa where name='박수진');
        위 내용을 아래처럼 작성가능
        select * from tblinsa where (city,buseo)=(select city,buseo from tblinsa where name='박수진')
    d. 반환값이 n행 n열 - b와c를 합친 방법을 사용
        예제 없음

ex) 인구수가 가장 많은 나라의 이름
select max(population) from tblcountry; --가장 많은 인구수
select name from tblcountry where population = 120660; --인구수가 가장 많은값과 일치하면 이름을 출력

select name from tblcountry where population = max(population) → 불가능(where절에는 집계함수가 올 수 없다)

select name from tblcountry where population = (select max(population) from tblcountry); → 가능(괄호로 묶어야한다)

ex) 나이 28세, 키177cm 여자의 남자친구 키
select height from tblmen where couple=(select name from tblwomen where age='28' and height='177');

ex) 평균 이상의 급여를 받는 사람목록
select * from tblinsa where basicpay > (select avg(basicpay) from tblinsa);

ex) 부서가 이열음과 같은 부서인 사람목록
select buseo from tblinsa where name='이열음';
select * from tblinsa where buseo = (select buseo from tblinsa where name='이열음');

  2. 컬럼리스트에서 사용 → 스칼라쿼리(행이1개,열이1개)를 사용한다
    a. 정적쿼리(모든행에 동일한 값이 반환)
      ex) select name,buseo,basicpay,(select avg(basicpay) from tblinsa) from tblinsa;
    b. 상관 서브 쿼리(서브쿼리의 값과 바깥쪽 메인 쿼리간의 관계를 형성)★
      select * from employees; --직원테이블
      select first_name,last_name,department_id from employees;
      select * from departments; --부서테이블
      select first_name,last_name,department_id,(select department_name from departments where department_id=90) from employees;
      select first_name,last_name,department_id,(select department_name from departments where department_id=employees.department_id) from employees;

----------------------------------------------------------------------------------------------------

★유니온(union) - 테이블 컬럼을 합치기(합집합)
- 중복된 데이터는 자동으로 제거된다
- union대신 union all을 적으면 중복되는 행까지 유지된다
- 컬럼리스트 개수와 자료형이 일치해야함
- 자료형이 일치하더라도 데이터의 의미까지 일치해야한다

select name,age from tblmen union select name,age from tblwomen;

보기쉽게 작성하려면

select name,age from tblMen
union
select name,age from tblWomen;
union
select name,age from tblTransgender;
이렇게 작성

select name,age from tblmen union select name,height from tblwomen;
이런것이나
select name,age from tblmen union select name,age,height from tblwomen;
이런것은 안됨

★인터섹트(intersect) - 중복되는 행만 가져오기(교집합)

★마이너스(minus) - 차집합

----------------------------------------------------------------------------------------------------

★테이블명.컬럼명 - 테이블의 컬럼을 조건절에 쓰고싶을때 사용
- ex) select * from tbladdressbook where substr(address,1,2)=tbladdressbook.hometown;

★관계형 데이터베이스에서 지양해야할것
1. null상태의 셀이 다량으로 발생하는 상태
2. 동일한 데이터가 2군데 이상 동시에 존재하는것(=중복값)
3. 하나의 셀에 분리가 가능한 데이터가 들어있는 것(=원자화)

★조인쿼리 (=엑세스 조인쿼리)
- 연관있는 테이블끼리 기본키⊃외래키를 통해 연결시키는것
- 테이블을 만들때는 부모테이블(참조될 기본키)을 먼저 만들어야함
- 테이블을 지울때는 자식테이블(참조하는 외래키)을 먼저 지워야함
- 부모테이블에 없는 값은 외래키에서 생성불가, 외래키가 참조하고있는 부모키는delete 불가,
- 테이블(결과셋)을 합치는 기술)
- union : 세로 병합
- join : 가로 병합
- (서로 관계를 맺고 있는) 2개(1개) 이상의 테이블의 내용을 가져와서 1개의 결과셋으로 만드는 작업
- select 결과셋 + select 결과셋 = 결과셋

조인의 종류

1. 단순 조인(cross join), 카티션 곱(데카르트 곱) - 다량의 데이터 필요할때, 테스트용 더미 생성용
  - ex) select * from tblcustomer cross join tblsales;
	아래처럼 쓰는것과 동일함
	select * from tblmen,tblwomen;
  - 행개수 : A테이블행 * B테이블행

2. 내부 조인(inner join) ★★★
  - 단순 조인에서 유효한 레코드만을 추출하는 조인 → 조인 결과셋을 유효하게 만든다.
  - 조인속성이 일치하는것만 조회함
  - ex)
	select 컬럼리스트
	from 테이블A
	inner join 테이블B
	on 테이블A.컬럼 = 테이블B.컬럼;

	select * from tblcustomer a
	inner join tblSales b
	on a.seq=b.cseq;

3. 외부 조인(outer join) ★★★★★
  - 내부조인 + 부모테이블
  - 내부 조인 + 조인되지 못한 나머지행
  - left/right 방향을 화살표라고 생각하고, right면 오른쪽에 있는 테이블이 주가 된다(오른쪽테이블에 따라 
	오른쪽 테이블에 전체행이 조회되며, 왼쪽테이블에 있는 조인컬럼이 null이여도 null이라고 출력된다)
    → left/right로 가르키는 테이블을 기준으로 출력함
  - ex)
	select 컬럼리스트
	from 테이블A
	left||right outer join 테이블B
	on 테이블A.컬럼=테이블B컬럼
	
	select * from tblstaff s
	left outer join tblproject p
	on s.seq=p.staff;

4. 셀프 조인(self join)
  - 1개의 테이블을 사용해서 조인
  - 단순 조인 + 셀프 조인
  - 내부 조인 + 셀프 조인
  - 외부 조인 + 셀프 조인
  - 자기가 자기를 참조하는 외래키를 가진 테이블을 대상으로 한다.
  - 자주 쓸일 없음
  - 내부조인과 비슷하나 자신을 참조함
	select
	    s1.name as 직원명,
	    s1.department as 부서명,
	    s2.name as 상사명
	from tblself s1 --직원테이블
	inner join tblself s2 --상사테이블
	on s2.seq = s1.super;
	--사장이 안나오는 결과

5. 전체 외부 조인(full outer join)
	- left, right 다출력. mysql에서는 지원안하니 union쓰기 (SELECT * FROM A UNION SELECT * FROM B)
	- 행개수 : A테이블행 + B테이블행

보통 쇼핑몰에서 회원탈퇴구현시 delete를 하는게 아닌 null로 update를 한다 (부모키 관련해서 꼬이기때문)

관계를 맺고 있는 2개의 테이블을 조작하면 발생하는 일
- 이 규칙이 꺠지면 데이터 무결성(유효성)이 깨진다 → 데이터의 가치가 상실된다
1. 부모테이블 조작
  a. 행 추가(insert) : 아무 영향 없음
  b. 행 수정(update) : 아무 영향 없음
  c. 행 삭제(delete) : 자식 테이블에 자신을 참조하는 행이 존재하는지 반드시 사전 체크 → FK
2. 자식테이블 조작
  a. 행 추가(insert) : 자신이 참조하는 대상이 실제로 존재하는 값인지 사전 체크 → FK
  b. 행 수정(update) : 수정할 컬럼이 FK가 아니면 아무 영향 없음. 수정할 컬럼이 FK이면 a와 동일
  c. 행 삭제(delete) : 아무 영향 없음


★전체조회(*)시 임의의 컬럼값 추가하기
select tblinsa.* from tblinsa; --이렇게 원래 테이블명을 쓰던지
select a.*,'test' from tblinsa a order by weight desc; --table에 alias를 줘서 검색하도록 한다


★의사 컬럼(Pseudo Column)
- 실제 컬럼이 아닌데 컬럼처럼 행동하는 객체
- 오라클 전용, MS-SQL(top),MySQL(limit)
- rownum
- 서브쿼리를 많이 의존해서 사용한다 (가져오고 싶은(select하고싶은) 데이터가 있으면 계속 가지고 와야한다 *(전체)로 가져오든 그 항목만가져오든)
- from절 실행 시 rownum만들어진다
- rownum을 조건으로 사용시 반드시 조건에 1이 포함되어야 한다★(이유는 select를 시킬때마다 rownum이 재계산되어 동적으로 생성 되기때문에)
- 1이 아닌 조건을 찾고싶을때는 엘리어스(as) 이용해서 변하는rownum을 상수로 고정시킨후 바깥쪽테이블을 하나더 만든다음 거기서 불러서 사용

select name,buseo,rownum from tblinsa;
select name,buseo,rownum from tblinsa where rownum=1;
select name,buseo,rownum from tblinsa where rownum<=10;
select name,buseo,rownum from tblinsa where rownum=3; --null이 나옴
select name,buseo,rownum from tblinsa where rownum>=5 and rownum<=10; --null이 나옴
select name,basicpay,rownum from tblinsa order by basicpay desc; --order by적용시 rownum값이 뒤죽박죽 된다

select name,rownum --2
from tblinsa --1
order by basicpay; --3

원하는대로 정렬 후 rownum을 할당하게 하려면 서브쿼리를 사용한다
select * from (select name,basicpay,rownum from tblinsa order by basicpay desc);
이때의 from은 서브쿼리를 대상으로 한다 (원본이 아님)

select name,basicpay,rownum from(select * from tblinsa order by basicpay desc); --선 정렬시킨 후, 그걸 가져와 rownum을 붙인다★(방법1)
select * from(select name,basicpay from tblinsa order by basicpay desc); --미리 조건을 지정하고 전체부르기(방법2)

select name,basicpay,rownum,rrum from (select name,basicpay,rownum as rrum from tblinsa order by basicpay desc);
기존의 rownum은 자식에게 override되어 안보이는데, 이걸 엘리어스를 통해 불러내기도 가능

select job,cnt,rownum from(select job,count(*) as cnt from tbladdressbook group by job order by count(*) desc);
group과 연계해서 사용시 엘리어스(as) 사용 잘 하기

select c2.*,rownum from(select c.* from tblcomedian c order by weight desc)c2 where rownum=1;
rownum 활용예시

select name,basicpay,rnum,rownum from(select name,basicpay,rownum as rnum from(select name,basicpay from tblinsa order by basicpay desc)) where rnum=3;
1이 포함안된 조건을 걸고싶을때 : 엘리어스(as) 이용해서 상수로 고정시킨후 바깥쪽테이블을 하나더 만든다음 거기서 불러서 사용

select
    (select 급여 from (select a.*,rownum as rnum from (select basicpay+sudang as 급여 from tblinsa where ssn like '%-1%' order by basicpay+sudang desc) a) where rnum=3)
    -
    (select 급여 from (select a.*,rownum as rnum from (select basicpay+sudang as 급여 from tblinsa where ssn like '%-1%' order by basicpay+sudang desc) a) where rnum=9) as 결과
from dual;
이렇게 n번째 값끼리 연산하고싶을때 select문에서도 사용 가능하다

기본키없는 테이블에서 rowid로 특정행 삭제 ex) delete tblmen where rowid='AAAE6EAAEAAAALnAAB';
이건 rownum으로는 불가

----------------------------------------------------------------------------------------------------

★뷰(view) - 가상테이블, 테이블 복사본(복제가 아닌 복사, 원본이 바뀌면 같이 바뀐다)

- DB Object중 하나(테이블, 시퀀스, 제약사항, 뷰..)
- 실제 테이블처럼 취급★
- 뷰를 이용하면 코드 비용 절약 + 가독성 향상
- 자주 사용하는 select의 결과를 저장하는 용도
- 개발자입장에서 코드비용절약 + 가독성 향상 + 생산성 향상
- 데이터 통신비용 및 서버에서 해야할 번역작업의 일부가 생략되어 절약됨(네트워크 트래픽 감소 + 서버처리 일부 생략 = 비용감소+시스템처리속도 향상)
- 뷰는 결과 복사가 아니라 select 쿼리 자체를 저장하는 객체이다★★★★★
- 뷰는 읽기 전용으로 사용한다★★★★★select만 사용
- 조인쿼리,유니온 등 '복합 뷰' 사용가능(테이블과도 결합 가능)

뷰의 종류
1. 단순 뷰
  - 하나의 테이블을 사용해서 만든 뷰
2. 복합 뷰
  - 두개 이상의 테이블을 사용해서 만든 뷰
  - join, union, subquery

뷰 생성하기
create view 뷰이름
as
select문;
↓
create view vwInsa
as
select * from tblInsa;

뷰 호출하기(사용하기)
select * from tblInsa;

뷰 삭제하기
drop view 뷰이름

뷰 수정하기
create or replace view vwInsa
as
select * from tblInsa;

----------------------------------------------------------------------------------------------------

★alter - 테이블 수정
  - 테이블 수정할 상황을 사전에 안만드는게 중요함

<컬럼 추가>
alter table tblEdit
    add(SESSION_ID VARCHAR2(30) NOT NULL);

NOTNULL 제약요소를 넣으려면 default로 임시값을 채워넣은다음 update로 다시 수정해야함
alter table tblEdit
    add(c1 varchar2(100) default 임시값 not null);

<컬럼 제약사항 수정> (null 허용도 이걸로)
alter table 테이블명
modify 컬럼명 varchar2(100);

<컬럼명 수정>
alter table 테이블명
rename column 바꿀컬럼명 to 새로운 컬럼명;

<컬럼 삭제>
alter table 테이블명
drop column 컬럼명;


제약사항 추가
ex)PK추가하기
alter table tblEdit
    add constraint tbledit_seq_pk primary key(seq);
ex)check제약 추가
alter table tblEdit
    add constraint tbledit_color_ck check(color in('노랑','빨강','파랑')); 
ex) 제약사항 삭제
alter table tblEdit
    drop constraint tbledit_color_ck;

↓↓↓ 되도록 사용 금지, 설계 미스 → 꼭 해야한다면 테이블을 삭제한후 다시 만드는게 더 나음
컬럼 자료형 수정 ex)
--3-2 컬럼의 자료형 바꾸기
alter table tblEdit
    modify(seq varchar2(100));

↓↓↓ 되도록 사용 금지
--3-3 컬럼명 바꾸기
alter table tblEdit
    rename column data to name;

----------------------------------------------------------------------------------------------------

★계층형 쿼리(Hierarchical Query)
  - 레코드간의 관계가 서로 상하 수직 구조의 관계를 이루는 경우 → 적당한 구조의 결과셋을 만들어 주는 역할
  - 부모와 자식 역할이 있는 레코드로 구성된 테이블에 사용
  - 오라클 전용
  - 트리 구조
  - start with절 connect by절
  - 계층형 쿼리를 사용할 떄만 사용 가능한 의사 컬럼을 제공한다

create table tblComputer(
    seq number primary key,                         --식별자(PK)
    name varchar2(50) not null,                     --부품명
    qty number not null,                            --수량
    pseq number null references tblComputer(seq)    --부모부품(FK) 셀프참조
);

insert into tblcomputer values(1,'컴퓨터',1,null);  --루트(사장)

insert into tblcomputer values(2,'본체',1,1);
insert into tblcomputer values(3,'모니터',1,1);
insert into tblcomputer values(4,'프린터',1,1);

insert into tblcomputer values(5,'메인보드',1,2);
insert into tblcomputer values(6,'그래픽카드',1,2);
insert into tblcomputer values(7,'랜카드',1,2);
insert into tblcomputer values(8,'CPU',1,2);
insert into tblcomputer values(9,'메모리',1,2);

insert into tblcomputer values(10,'보호필름',1,3);

insert into tblcomputer values(11,'잉크카트리지',1,4);
insert into tblcomputer values(12,'A4용지',100,4);

select * from tblcomputer c
    start with seq=1
        connect by prior seq=pseq;
        
select name,level from tblcomputer c
    start with seq=1
        connect by prior seq=pseq;

select lpad(' ',(level-1)*3)||name,level,seq from tblcomputer c
    start with seq=1 --루트지정
        connect by prior seq=pseq;
        
select lpad(' ',(level-1)*3)||name,level,seq from tblcomputer c
    start with seq=(select seq from tblcomputer where name='컴퓨터')
        connect by prior seq=pseq;

select lpad(' ',(level-1)*3)||name,level,seq from tblcomputer c
    start with pseq is null --부모가 없는 부품을 루트로
        connect by prior seq=pseq;



select
    lpad(' ',level*2) || name as 부품명,
    prior name as 부모부품명,
    level as 단계
    ------여기까지가 베이스
    ,
    connect_by_root name as 루트부품명,
    connect_by_isleaf as 리프노드,
    sys_connect_by_path(name,'▷')
from tblcomputer
start with pseq is null
connect by pseq=prior seq
--order by name asc;
order siblings by name asc; --같은 레벨을 가진 그룹내에서만 정렬됨

----------------------------------------------------------------------------------------------------

★트랜잭션(Transaction) 처리하는 방법
  - 오라클에서 발생하는 1개 이상의 명령어들을 하나의 논리 집합으로 묶어놓은 단위 → 트랜젝션 → 제어 → 트랜젝션 처리
  - 트랜젝션에 포함되는 명령어 : insert/update/delete
  - 상호 유기적으로 연결되어있는 작업들을 묶어서 트랜젝션이라는 하나의 단위로 만듦
  - 트랜젝션 처리한다 = 트랜젝션 내부 작업(DML) 하나하나가 모두 성공하면 데이터베이스에 반영, 하나라도 실패시 앞선 작업(DML)들은 모두 취소된다
1. commit
2. rollback
3. savepoint - DML작업사이사이에 savepoint a; savepoint b; 이런식으로 만들어 놓고 rollback to b; rollback to a; 이렇게 돌아갈수있음 (순서가 중요)

동시간대에 트랜잭션은 유일하게 존재한다. 시간대별로 별도의 트랜잭션이 존재할 수 있다.

1. 클라이언트가 접속 직후
2. commit 실행 직후
3. rollback 실행 직후

현재 트랜잭션이 끝나는 경우
1. commit 실행 → 현재 트랜잭션을 DB에 반영함
2. rollback 실행 → 현재 트랜잭션을 DB에 반영안함
3. 클라이언트가 접속 종료하는경우
  a. 정상적인 종료
    대부분의 툴이 선택하라고 함(commit or rollback)
  b. 비정상적인 종료
    rollback
4. DDL(create/alter/drop)이 실행될때 (DDL + commit)
  - 자동 커밋(Auto commit)
  - 구조에 변화를 주는 명령어 → 이전의 데이터 조작을 작업 완료 할 수 있도록 자동 commit 처리 발생

----------------------------------------------------------------------------------------------------

데이터베이스 구축

- 프로젝트 진행 → 다량의 데이터 발생 → 저장하기 위한 조직화된 구조 필요 → 설계 → 구조 생성 → 데이터 생성 + SQL

  1.데이터베이스 모델링
    - 가장 초반에 하는 작업
    - 가장 중요한 작업
    - 설계도 작업★★
    - 아이템 선정 → 요구분석 → 데이터베이스 구성을 위한 정보(Raw) 수집 → 분석 → 조직화된 저장 구조 → 도식화(설계도) → ERD(최종 산출물)
    - 아직 이 단계에서는 DBMS의 종류는 결정되지 않는다(특정 DB를 위한 그림X → 모든 DB에 공통적인 그림)

  2. 데이터베이스 설계
    - 실제 사용할 DBMS를 결정한다 → 오라클
    - 모델링 결과물(ERD) → 구체화하는 작업(오라클에 맞게 수정 + 상세화)
    - 객체 식별자 생성, 자료형 지정, 제약사항 추가 등...
    - 데이터베이스 설계의 결과물 → 스크립트(*.sql) = DDL(create/alter/drop)

  3. 데이터베이스 구축
    - 1,2결과 토대 → 현실화 → 물리적으로 만드는 작업
    - 오라클에 테이블(각종 객체)이 생성되는 작업

  4. 데이터 추가
    - 더미용 데이터 추가(김긱곽) → 프로그램 → 90%이상
    - 정확한 테스트용 데이터(한가인) → 수기 작성 → 10%내외

  5. 업무 SQL 작성
    - 프로그램에 사용될 모든 SQL을 미리 작성
    - 이 단계를 진행하는 과정에 1~3까지의 문제점이 발견된다
    - ex) 게시판
      a. 요구분석.. ERD... 테이블 구현.. 더미 데이터 작성
      b. 자바 프로그램 작성(자바+SQL)

      a. 요구분석.. ERD... 테이블 구현.. 더미 데이터 작성
      b. SQL 작성
      c. 자바 프로그램 작성(자바)

----------------------------------------------------------------------------------------------------

데이터베이스 모델링

1. ERD, Entity Relation Diagram
  - 엔티티간의 관계를 표현한 그림
  - 데이터베이스 모델링 기법 중에 하나 → 대표적 방법
  - 손, 오피스, 전문툴(eXERD,SQL Developer, ER-WIN)

2. Entit, 엔티티
  - 다른 Entity와 분류(구분)될 수 있고, 다른 Entity에 대해서 정해진 관계를 맺을 수 있는 데이터 단위
  - 객체(속성의 집합) : 자바의 인스턴스(객체)
  - erd의 테이블
  ex) 회사 관리 프로그램
    a. 사원 정보 관리
      - 정보 : 사원명, 나이, 연락처, 주소, 사원번호 등..
      - (사원명, 나이, 연락처, 주소, 사원번호) → '사원' 이라는 앤티티(=테이블)
    b. 부서 정보 관리
      - 정보 : 부서명, 부서번호, 사무실번호, 내선번호 등..
      - (부서명, 부서번호, 사무실번호, 내선번호) → '부서' 라는 엔티티(=테이블)

3. Entity Relationship, 엔티티 관계
  - 엔티티간의 관계
  - 테이블과 테이블의 관계

4. Attribute, 속성
  - 엔티티가 가지는 속성(특성, 성질)
  - 엔티티를 만들기 위해서 하나로 모였던 각각의 정보들
  - 컬럼, 자바 클래스의 멤버 변수 역할
  - ex) 사원 엔티티 = 사원명 속성 + 사원번호 속성 + 연락처 속성 + 주소 속성 등..

5. Tuple, 튜플
  - 엔티티에 정의된 규칙에 따라 실제 만들어진 데이터
  - 레코드, 행, 객체
  - ex) 실체화된 속성의 집합 → 테이블 레코드1줄

----------------------------------------------------------------------------------------------------

ERD안에서 Entity, Attribute, Relation 등을 표현하는 방법(그림 그리는 방법)

1. Entity
  - 사각형으로 표시
  - 이름을 작성(한글, 영어 등)
  - 엔티티명은 하나의 ERD내에서는 유일
  - 보통 단수로 표기

2. Attribute
  - 엔티티 안에 표기(목록 형태)
  - 파스칼 표기 or 전부 소문자 표기
  - 보통 단수로 표기
  - 추가 표기 사항(속성에 대한 특징 기술)
    a. NN(Not null) - 해당 속성을 비워둘 수 없다(=필수값)
    b. ND(Not duplicate - 해당 속성은 중복될 수 없다(=유니크)

  - 중복되면 안되고, 생략되면 안된다(NN,ND) : #* 속성명
  - 생략되면 안된다(NN) : * 속성명
  - 중복되면 안된다(ND) : # 속성명
  - 중복,생략 모두 가능(ND) : 속성명 / o 속성명 (o=optional)

3. Relationship
  - 가장 중요하게 작업해야 할 단계
  - 엔티티와 엔티티의 관계 → 레코드와 레코드의 관계 → PK와 FK의 관계
  - 관계의 패턴(종류)
    A엔티티 : B엔티티
    a. 1:1 - 1개의A는 1개의B와 관계
    b. 1:0 - 1개의A는 0개의B와 관계 //무관계
    c. 1:N - 1개의A는 1개이상의B와 관계
    d. 1:N - 1개의A는 0개 이상의B와 관계
    e. N:N - N개의A는 N개의B와 관계 → 파괴 1:N N:1

----------------------------------------------------------------------------------------------------

키(Key)
- 속성, 컬럼
- 역할을 부여한 속성

1. 기본 키(Primary key)
  - 레코드(행)을 다른 레코드(행)과 구분하는 역할
  - 식별자★★
  - NN + ND
  - 테이블에는 반드시 기본키가 존재해야 한다
2. 후보키(Candidate key)
  - 레코드(행)을 다른 레코드(행)과 구분할수 있는 키
  - 후보키들 중 대표로 선발된 키 → 기본키
3. 대체키(Alternate key)
  - 후보키들 중 기본키를 제외한 나머지 키
4. 슈퍼키(Super key)
  - 복합키(Composite key)
  - 1개 키만을 가지고 식별자 역할이 불가능한 경우 → 2개 이상의 키를 조합해서 기본키 역할
5. 외래키(Foreign key)
  - 부모테이블의 기본키를 참조하는 키
  - ex)genre number not null reference tblGenre(seq) : tblVideo테이블의 genre컬럼(FK)이 tblGenre테이블의 seq컬럼(PK)를  참조한다
  - 테이블 간의 관계를 만드는 역할★★
6. 일반키

먼저 태어나는 엔티티 : 부모
나중에 태어나는 엔티티 : 자식
95% 맞다고

----------------------------------------------------------------------------------------------------

ERD 종류

1. 논리 다이어그램(Logical Diagram)
  - 업무를 설명하기 위한 ERD → 데이터의 성격

2. 물리 다이어그램(Physical Diagram)
  - 논리 다이어그램을 기반으로 실제 데이터베이스 반영하기 위해 구체적인 표현을 추가한 다이어그램(ERD)
  - 모든 식별자 → 오라클에 적합하게 만들기(영어로)
  - 자료형 명시
  - 재약사항 명시

----------------------------------------------------------------------------------------------------

eXRD프로그램 사용법

테이블과 테이블사이 관계선 클릭하고 space
테이블과 클릭하고 space
일반탭 - 테이블 물리 이름 ex)tblMember
컬럼탭 - 속성 물리이름/데이터타입/제약 등 설정 , 속성클릭후 주석탭에서 주석입력가능
논리모드/물리모드 토글 = f3키
컬럼 보기설정 아이콘 클릭 - 주석,반대모드 이름 표시함으로, 도메인 표시안함으로

eXERD→포워드 엔지니어링 : 모든 erd그림을 자동으로 ddl로 만들 수 있다 (쓰는 곳과 안쓰는곳 케바케)
eXERD→리버스 엔지니어링 : exrd, 즉 설계도가 없을때 사용 (물리구조를 보는거라 활용 빈도가 높진 않음)
(프로젝트 선택 → '오라클' 확인 → 다음 → 설정관리 → 새연결 → 이름아무거나 입력 → 
파일선택 → 오라클경로선택(C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib\파일선택) →
호스트(localhost)/포트(1521)/sid(xe)/사용자(hr)/비밀번호) → 연결테스트 → 확인 → 선택 후 확인 → 만든거 선택 → 테스트 → 확인 →
다음 → 테이블을 오른쪽으로 이동시키면 선택해제 (다 선택할거면 그대로 완료) → 완료

----------------------------------------------------------------------------------------------------

정규화(Normalization)

- 자료의 손실이나 불필요한 정보를 없애고, 데이터의 일관성을 유지하고, 데이터의 종속을 최소화하기 위해 자료구조(ERD)를 수정하는 작업
- 우리가 만든 테이블(비정형, 비정규화 상태) → 정규화 → 정규화된 구조
- 제 1정규화 → 제 2정규화 → 제 3정규화

관계형 데이터베이스 시스템이 지향하는 데이터베이스의 상태
1. 최대한 null상태의 셀을 가지지 않는다.
2. 중복값을 저장하지 않는다 → 동일한 성격의 데이터가 2개 이상 발생하게 하지 않는다
3. 하나의 셀에 단일값 저장(원자화)

정규화 목적
1. null 제거
2. 중복값 제거
3. 자료 삽입, 갱신, 삭제에 따른 이상현상 제거 → 데이터 무결성 보장

이상 현상
1. 삽입이상(Insertion Anomaly)
  - 특정 테이블에 데이터를 삽입할 때 원하지 않는 데이터까지 같이 넣어야 하는 사오항)
2. 갱신 이상(Update Anomaly)
  - 동일한 데이터가 2개 이상의 테이블에 존재 → 그 중 1개는 수정했지만, 다른 1개를 수정 못했을때
    두 데이터간의 이상 오류가 발생 → 2개 데이터 중 어떤 데이터가 올바른 데이터인지 구분 못하는 상황
3. 삭제 이상(Deletion Anomaly)
  - 특정 테이블에서 데이터를 삭제할 때 원하지 않는 데이터까지 같이 지워야 하는 상황

함수 종속(Function Dependency)
  - 하나의 테이블내 컬럼끼리의 관계를 표현
  - 정규화는 '부분 함수 종속'이나 '이행 함수 종속'을 모두 없애고, 모든 컬럼의 관계를 '완전 함수 종속'으로 만드는 작업이다.
1. 완전 함수 종속(Full Functional Dependency)
2. 부분 함수 종속(Partial Functional Dependency)
  - 일부컬럼이 '복합키' 모두에게 종속되는 것이 아니라, 일부에게만 종속되는 현상
3. 이행 함수 종속(Transitive Functional Dependency)
  - 키본키가 아닌 

정규화
- 1NF ~ 3NF (Normal Form)
- 1개 테이블  → 정규화 작업 → 2개 이상의 테이블로 쪼개짐

제 1정규화(1NF)
  - 모든 컬럼(속성)이 원자값을 가진다
  - 여러개로 분리 가능한 값을 1개의 컬럼안에 넣지 않는다
제 2정규화(2NF)
  - 복합키를 사용할때만 해당될 수 있음
  - 부분 함수 종속을 발견해서 부분 함수 종속을 제거한다
제 3정규화(3NF)
  - 이행 함수 종속을 발견해서 이행 함수 종속을 제거한다
  - 기본 키(복합키)가 아닌 모든 컬럼은 기본키(복합키)에 완전 함수 종속이어야 한다

역정규화
  - 정규화로 쪼개놓은것보다 정규화전 테이블에 대한 엑세스가 많을때
  - 다시 정규화 하기 전으로 합치는 작업

열거형은 무조건 테이블을 분리시키라고
거주형태(번호,형태명) 내부컬럼-자택,자취,기숙사
성별(번호,성별) 내부컬럼-남자,여자

----------------------------------------------------------------------------------------------------

PL/SQL
- 절차지향 → 문장을 구분할 필요가 있다. → 문장 종결자(;) 필수
- Procedural Language Extensions to SQL

ANSI-SQL
- 비 절차성 언어(명령어간의 순서가 없다. 연속적이지 않다.) → 제어 흐름이 없다. 문장 단위의 독립적인 언어
- 비절차지향 → 문장을 구분할 필요가 없다. 문장 종결자(;) 필수 아님
- ANSI-SQL + 절차적 기능 추가 → 오라클 → PL/SQL

프로시저(Procedure) : 일련의 쿼리들을 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합
- 메소드, 함수, 서브루틴 등 모두 같은 말
- 수행결과(return)가 단일이면 사용자정의함수(function), 2개이상이면 프로시저(procedure)
- 순서가 없는 코드의 집합

1. 익명 프로시저 → 1회용
2. 실명 프로시저 → 반복 사용 가능

PL/SQL 프로시저 블럭 구조(골격)
4개의 키워드로 구성
  - declare
  - begin
  - exception
  - end;

1. declare
  - 선언부
  - 프로시저에서 사용할 변수, 객체 등을 선언하는 영역
  - 생략 가능

2. begin
  - 실행부(구현부)
  - begin ~ end : 블럭 역할 ({ })
  - 프로시저의 구현 코드를 작성하는 영역 (메소드의 body역할)
  - 생략 불가능
  - ANSI-SQL + 연산, 제어 등을 구현★★
  - try절 역할

3. exception
  - 예외 처리부
  - catch절 역할
  - 예외 처리 코드를 작성하는 영역
  - 생략 가능

4. end;
  - 실행부(구현부)
  - 생략 불가능


PL/SQL 블럭은 중첩이 가능하다.
begin
  ANSI-SQL + 제어
  begin
    begin
    end;
  end;

  bigin

  end;
end;

----------------------------------------------------------------------------------------------------

프로시저: 일련의쿼리들을 마치 하나의 함수처럼 실행하기위한 쿼리의 집합 (반환을 여러개 할 수 있음)
	(IN/OUT/INOUT) IN은 프로시저로 받기, OUT은 돌려주기, INOUT은 둘다
사용자 정의함수 : 일련의 SQL처리를 수행하고, 수행 결과를 단일 값으로 반활할 수 있는 절차형SQL (IN만 됨)
	★핵심 : SELECT, WHERE, HAVING 절에 사용자 정의 함수를 사용할 수 있음
	★핵심2 : 프로시저는 리턴값이 없어도 되지만 사용자 정의함수는 꼭 있어야 한다
트리거 : INSERT/UPDATE/DELETE 등 이벤트 발생시 실행 (COMMIT, ROLLBACK 못씀)
	OLD	NEW
INSERT	  NULL	삽입된값
UPDATE	갱신전값	갱신후값
DELETE	삭제전값	  NULL

주의사항
1. 대소문자★★★★★★★★★★★★★★★★★★★★★★★★
2. 변수선언, SQL문, END IF 에 세미콜론 꼭 넣어야함 (다음줄에서 빨간줄생기면 세미콜론오류인것)★★★
3. 오류생기면 중간중간 DBMS_OUTPUT.PUT_LINE('AAAAAAA') 등 로그 막찍어놓고 실행시켜서 확인하기
4. PL/SQL 중간에서도 SQL문 드래그후 CTRL+ENTER로 실행할 수 있음. 굳이 밖으로 빼서 테스트 하지 말고 안에서 바로 테스트하기
	a. 테스트할 줄 복붙해서
	b. 변수 → 테스트상수로 바꾸고,
	c. SELECT문의 INTO 변수1 이런 ANSI SQL 문 이외의것들 빼고 실행하기

5. SELECT로 돌려받을 행이 0개면 (결과가 없으면. NULL말고) 변수에 대입이 안된다. 이때 5가지 방법이 있는데 방법은 아래와 같음

DECODE 함수 이용하기
컬럼이 NULL이면 'Y' 그렇지 않으면 'N'
SELECT DECODE(NULL, NULL, 'Y', 'N') FROM DUAL; -- Y
SELECT DECODE(NULL, 'TEST', 'Y', 'N') FROM DUAL; -- N

EXCEPTION 이용하기
BEGIN
	SELECT 컬럼명1 INTO 변수명1 FROM 테이블명 WHERE 조건
EXCEPTION
	WHEN NO_DATA_FOUND THEN 변수명1 := null;
END

MAX 이용하기 (추천.)
SELECT MAX(컬럼명1) INTO 변수명1 FROM 테이블명 WHERE 조건

IF 변수명 IS NULL THEN

ELSE


DUAL 이용하기 (안씀)
SELECT (SELECT 컬럼명1 INTO 변수명1 FROM 테이블명 WHERE 조건) FROM DUAL


5. dbms_output.put_line(); 에 조건식 넣을수 없음

6. exception문은 맨 마지막에 넣어야함

7. 오류가 어디서 나는지 안나오면 사용자 system으로 바꿔보기. 어디서 오류가나는지 나올수도 있음

8. 트리거 생성시 PLS-00201: 'MEMNBER_TL' 식별자가 정의되어야 합니다 오류나면
	a. if문 조건에 딸랑 테이블명만 썼는지
	b. :old / :new 식별자 오타 확인
	c. 트리거에서 쓸 컬럼이 해당 테이블에 모두 있는지 확인
	d. 권한 부여
GRANT CREATE TRIGGER TO 사용자명;
GRANT CREATE ANY TRIGGER TO 사용자명;
GRANT ALTER ANY TRIGGER TO 사용자명;

-----

★프로시저세팅 (되도록 유지보수위해? PL/SQL 쓰지말고 스프링에서 처리하기)
만들기 전에 먼저 프로시저 디버깅 권한 부여↓ 이후 접속탭→계정명→프로시저→디버깅할 프로시저명 들어간다음 ctrl+shift+f10으로 디버깅 가능
GRANT DEBUG CONNECT SESSION TO 계정명;
GRANT DEBUG ANY PROCEDURE TO 계정명;
디버깅 기능을 써야 어디서 오류가 났는지 알 수 있음 (중간에 DBMS_OUTPUT.PUT_LINE(); 막 찍어보기)
디버깅시에도 프로시저는 실제 실행되니 DB안날라가게 조심하기

CREATE [OR REPLACE] PROCEDURE 프로시저명(
	파라미터명1 [IN | OUT | INOUT] 자료형 -- 자료형은 VARCHAR / NUMBER 로 통일
	파라미터명2 [IN | OUT | INOUT] 자료형 -- 자료형은 VARCHAR / NUMBER 로 통일
)
IS
	변수명1 자료형; -- 세미콜론 필수, 자료형은 VARCHAR / NUMBER 로 통일
BEGIN
	--명령부
	DBMS_OUTPUT.PUT_LINE(파라미터명1); -- 중간중간 로그 찍어보기
	IF 파라미터명1 < '20000101' THEN
		SET 파라미터명1 := '20200101'; -- 변수값 변경
	END IF

	--SQL(SELECT문)로 변수에 값 대입
	SELECT SUM(컬럼명1)
	INTO 변수명1 --변수에 SELECT문 결과를 넣는다★★
	FROM 테이블명
	WHERE 컬럼명2 = 파라미터명1;

	--예외부
	EXCEPTION
	WHEN NO_DATA_FOUND THEN -- SELECT문의 결과가 없을때(아무런 행을 반환하지 않을때)
	SET 변수명1 := 0; -- 변수값 변경

	--SQL(INSERT/UPDATE문)로 기능 실행 (변수 넣을수 있음)
	INSERT INTO ASD_TL(컬럼명1,컬럼명2)
	VALUES(파라미터명1,변수명1)

	DBMS_OUTPUT.PUT_LINE(변수명1); -- 중간중간 로그 찍어보기
	-- COMMIT; -- 테스트 완벽히 해보고 추가하기 WHERE ID=ID 이렇게 실수하면 대참사남 → ID=P_ID
		근데 커밋 안했는데 프로시저 실행시 커밋될때도 있음 조심
END;

<호출법> (스프링에서 호출은 밑에)
EXCUTE 프로시저명('123');


★사용자정의함수세팅
CREATE [OR REPLACE] FUNCTION 함수명(
	파라미터명1 IN 자료형  -- 자료형은 VARCHAR / NUMBER 로 통일
)
RETURN 자료형 -- 반환시킬 자료형 지정
IS
	변수명1 자료형;  -- 자료형은 VARCHAR / NUMBER 로 통일
	변수명2 자료형;  -- 자료형은 VARCHAR / NUMBER 로 통일
	변수명3 자료형;  -- 자료형은 VARCHAR / NUMBER 로 통일
BEGIN
	DBMS_OUTPUT.PUT_LINE(파라미터명1); -- 중간중간 로그 찍어보기
	IF 파라미터명1 >'30000' THEN
		파라미터명1 = '20200101';
	END IF;
	SELECT TO_CHAR(SYSDATE,'YYYY'),
		SUBSTR(파라미터명1,1,4)
	INTO 변수명1,
		변수명2 --변수에 SELECT문 결과를 넣는다
	FROM DUAL;
	
	변수명3 = TO_NUMBER(변수명1) - TO_NUMBER(변수명2);

	DBMS_OUTPUT.PUT_LINE(변수명1); -- 중간중간 로그 찍어보기
	DBMS_OUTPUT.PUT_LINE(변수명2); -- 중간중간 로그 찍어보기
	DBMS_OUTPUT.PUT_LINE(변수명3); -- 중간중간 로그 찍어보기

	RETURN 변수명3;
END;

<호출법>
SELECT 함수명('123') FROM DUAL;
UPDATE 테이블명 SET 컬럼명1 = 함수명(컬럼명2) WHERE 컬럼명1 = '123';


★트리거세팅
CREATE OR REPLACE TRIGGER 트리거명

AFTER UPDATE OR DELETE
ON EMPLOTEE -- 원본 테이블명
FOR EACH ROW -- 매번 변경되는 데이터 행의 수만큼 실행
BEGIN
IF UPDATING THEN -- 테이블1에 UPDATE연산 발생시 (dml중 한개만 지정할시 if문 자체를 쓰지 말기★)
	INSERT INTO EMPLOYEE_HIST(ID, NAME, BUSEO) VALUES(:OLD.ID, :NEW.NAME, '부서이동') -- EMPLOYEE_HIST 테이블에 내용 추가
ELSIF DELETING THEN -- 테이블1에 DELETE연산 발생시
	INSERT INTO EMPLOYEE_HIST(ID, NAME, STATUS) VALUES(:OLD.ID, :OLD.NAME, '퇴사') -- EMPLOYEE_HIST 테이블에 DELETE전 내용 추가
END IF;
END;


만든 프로시저 mybatis에서 쓰는법

↓↓↓↓↓

<PL/SQL>
-- 회원추가정보 추가 / 회원 정보 수정
CREATE OR REPLACE PROCEDURE EDIT_MEMBER_INFO(
    P_ID IN VARCHAR,
    P_GNDR IN VARCHAR,
    P_AMR IN NUMBER,
    P_WAY IN VARCHAR,
    P_BMR IN NUMBER,
    P_HGHT IN NUMBER,
    P_WGHT IN NUMBER,
    
    R_RESULT OUT VARCHAR
)
IS
    V_HGHT NUMBER;
    V_BMR NUMBER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('P_GNDR:' || P_GNDR);
    DBMS_OUTPUT.PUT_LINE('P_AMR:' || P_AMR);
    DBMS_OUTPUT.PUT_LINE('P_WAY:' || P_WAY);
    DBMS_OUTPUT.PUT_LINE('P_BMR:' || P_BMR);
    DBMS_OUTPUT.PUT_LINE('P_HGHT:' || P_HGHT);
    DBMS_OUTPUT.PUT_LINE('P_WGHT:' || P_WGHT);

    SELECT MAX(HGHT) INTO V_HGHT FROM MEMBER_MORE_INFO_TL --저장된 키/몸무게 정보가 없을경우 V_HGHT에 NULL 입력
    WHERE MEMBER_SQ = (SELECT MEMBER_SQ FROM MEMBER_TL WHERE ID = P_ID);

    SELECT MAX(BMR) INTO V_BMR FROM MEMBER_MORE_INFO_TL --저장된 기초대사량 정보가 없을경우 V_BMR에 NULL 입력
    WHERE MEMBER_SQ = (SELECT MEMBER_SQ FROM MEMBER_TL WHERE ID = P_ID);

    DBMS_OUTPUT.PUT_LINE('=');
    DBMS_OUTPUT.PUT_LINE('V_HGHT:' || V_HGHT);
    DBMS_OUTPUT.PUT_LINE('V_BMR:' || V_BMR);

    IF P_WAY = 'BMR' THEN --BMR로 입력 받았을때
        IF V_BMR IS NULL AND V_HGHT IS NULL  THEN  --저장된 추가정보가 아예 없을때 ('키/몸무게'는 '키'로 판단)
            DBMS_OUTPUT.PUT_LINE(1111);
            INSERT INTO MEMBER_MORE_INFO_TL(MEMBER_MORE_INFO_SQ, MEMBER_SQ, WAY, BMR)
            VALUES(
                MEMBER_MORE_INFO_SQ.NEXTVAL,
                (SELECT MEMBER_SQ FROM MEMBER_TL WHERE ID = P_ID),
                'BMR',
                P_BMR
            );
        ELSE -- 저장된 추가정보가 있을때
            DBMS_OUTPUT.PUT_LINE(2222);
            UPDATE MEMBER_MORE_INFO_TL SET
				WAY = 'BMR',
                BMR = P_BMR
            WHERE MEMBER_SQ = (SELECT MEMBER_SQ FROM MEMBER_TL M WHERE M.ID = P_ID);
        END IF;
    ELSIF P_WAY = 'HNW' THEN
        IF V_HGHT IS NULL AND V_BMR IS NULL THEN --저장된 추가정보가 아예 없을때 ('키/몸무게'는 '키'로 판단)
            DBMS_OUTPUT.PUT_LINE(3333);
            INSERT INTO MEMBER_MORE_INFO_TL(MEMBER_MORE_INFO_SQ, MEMBER_SQ, WAY, HGHT, WGHT)
            VALUES(
                MEMBER_MORE_INFO_SQ.NEXTVAL,
                (SELECT MEMBER_SQ FROM MEMBER_TL WHERE ID = P_ID),
				'HNW',
                P_HGHT,
                P_WGHT
            );
        ELSE -- 저장된 추가정보가 있을때
            DBMS_OUTPUT.PUT_LINE(4444);
            UPDATE MEMBER_MORE_INFO_TL SET
				WAY = 'HNW',
                HGHT = P_HGHT,
                WGHT = P_WGHT
            WHERE MEMBER_SQ = (SELECT MEMBER_SQ FROM MEMBER_TL M WHERE M.ID = P_ID);
        END IF;
    END IF;

    DBMS_OUTPUT.PUT_LINE(5555);
    UPDATE MEMBER_TL SET -- 추가정보와 관계없이 기본정보 수정
        GNDR = P_GNDR,
        AMR = P_AMR
    WHERE ID = P_ID;

    R_RESULT := 'success';
	
	COMMIT;
	
EXCEPTION
	WHEN OTHERS THEN
	R_RESULT := 'fail';

END;

<XML>
<!-- map/VO로 주고받을 수 있음. return문으로 받는게 아니라 파라미터로 받은 map에 자동'추가'되며 key이름은 호출부에 #{}에 입력한대로 생성됨
Map<String,String> map = new HashMap<String,String>(); service.deleteInfo(map); 이렇게 실행시켰으면 map.get("result"); 그냥 이렇게 받으면 됨
(VO로 주고받으려면 return받을 key를 VO필드에 필히 만들어놔야함)
리턴받을게 없을때는 VO가 편하고 리턴받을게 있을땐 MAP이 편함
태그는 무조건 select로 쓰기
속성 안쓰면 오류 → 인덱스에서 누락된 IN 또는 OUT 매개변수:: 2) -->
<select id="EDIT_MEMBER_INFO_PROCEDURE" parameterType="map" statementType="CALLABLE">
	{ CALL EDIT_MEMBER_INFO (
		#{ID}, → 파라미터1 (모드/자료형 안써도됨★)
		#{GNDR}, → 파라미터2 (모드/자료형 안써도됨★)
		
		#{R_RESULT, mode=OUT, jdbcType=VARCHAR, javaType=String}, → out리턴1
		#{R_TITLE, mode=OUT, jdbcType=VARCHAR, javaType=float} → out리턴2

		<!-- #{out_cursor_table, mode=OUT, jdbcType=CURSOR, javaType=ResultSet, resultMap=editMyinfo_MAP} → 커서 -->
	)}
</select>

<MAPPER>
// [DBMapper.xml 쿼리에서 선언한 변수 개수 및 타입에 맞게 파라미터 선언]
void EDIT_MEMBER_INFO_PROCEDURE(Map map); // [void 설정]

<컨트롤러>
service.modify(map); ← 실행시킨 후

log.info(map) ← 그냥 다시 찍어보면 return키-값들이 별다른 설정 없이도 들어가있음

-----

★프로시저 결과 나오게 하기 (시작 할때마다 한번씩 실행 해야한다)
set serveroutput on; ★★★
set serveroutput off;

★출력 메세지
dbms_output.put (=자바 print)
dbms_output.put_line(=자바 println)

----------------------------------------------------------------------------------------------------

PL/SQL → 변수 생성 가능
1. 자료형
- ANSI-SQL와 동일(확장)
2. 변수 선언하기
- 변수명 자료형[not null] [default 값]
- 변수는 주로 질의의 결과★나 인자값을 저장하는 용도로 사용
3. 대입 연산자
- 컬럼명 = 값(ANSI)
- 변수명 := 값(PL/SQL)


--익명 프로시저 → 익명 (PL/SQL)블럭
begin

end;


declare
    vbuseo varchar2(15);
begin
    --PLS-00428: an INTO clause is expected in this SELECT statement
    --PL/SQL 블럭 안에서는 select문을 그냥 사용할 수 없다.★★★
    select buseo into vbuseo from tblInsa where name='이순신';
    dbms_output.put_line(vbuseo); --select의 컬럼값을 출력할 수 없다. 반드시 PL/SQL의 구성 요소만 출력할 수 있다.
end;

변수의 주 용도 → select 결과값을 담는 용도 (into로)
결과가
1. 1행 1열
  - 1:1 관계 → 컬럼 1개를 변수 1개에 저장
2. 1행 N열
  - N:N 관계 → 컬럼 N개를 변수 N개에 저장
3. N행 1열
  - 불가능 → 커서 사용
4. N행 N열
  - 불가능 → 커서 사용

--참조 자료형
--- 테이블로부터 직접 자료형을 알아내는 방법
--- 생산성 + 유지 보수성
1.%type
  - 사용되는 테이블의 특정 컬럼 자료형을 그대로 참조해서 적용 ex) vnum tblInsa.num%type;
  - 복사되는 정보
  a. 자료형
  b. 길이
  c. nut null
ex)
declare
    vbuseo varchar2(15); 
    vjikwi tblInsa.jikwi%type; --vjikwi carchar2(15)
begin
    select buseo,jikwi into vbuseo,vjikwi from tblinsa where name='이순신';
    dbms_output.put_line(vbuseo);
    dbms_output.put_line(vjikwi);
end;

2. %rowtype
  - 행 참조
  - %type의 집합형

----------------------------------------------------------------------------------------------------

PLSQL조건문

declare
    vnum number := -10;  -- 1. 변수생성 + 초기화
begin
    if vnum>0 then -- 2. 조건
        dbms_output.put_line('양수'); -- 3. 출력
    elsif vnum<0 then
        dbms_output.put_line('음수');
    else
        dbms_output.put_line('0');
    end if;
end;

elseif가아닌 elsif임 주의

----------------------------------------------------------------------------------------------------

PLSQL반복문 (1씩증가나 1씩 감소만 가능)

1. loop (
  - 무한루프
  - 무한루프 + 조건 탈출 (자바break)
 ex)
declare
    vnum number := 1;
begin
    loop
        dbms_output.put_line(to_char(sysdate,'hh:mm:ss'));
        vnum := vnum + 1;
        
        --if → break
        exit when vnum > 10;
    end loop;
end;

2. for loop
  - 지정 횟수 반복(자바for)
ex)
--for loop
begin
    -- i : 루프변수
    -- i : 초기값
    -- 10 : 최대값
    -- .. : 증가
    for i in 1..10 loop
        dbms_output.put_line(i);
    end loop;
end;

1씩 감소 ex) for n in reverse 1..10 loop

3. while loop
  - 조건 반복(자바while)
ex)
declare
    vnum number := 1;
begin
    while vnum<=10 loop
        dbms_output.put_line(vnum);
        vnum := vnum + 1;
    end loop;
end;


ex)10000개의 더미데이터생성
create table tblLoop(
    seq number primary key,
    data varchar2(30) not null
);

create sequence seqLoop;

declare
    vnum number := 1;
begin
    loop
        insert into tblLoop(seq,data) values(seqLoop.nextVal,'데이터'||vnum);
        vnum := vnum +1;
        
        exit when vnum > 10000;
    end loop;
end;

----------------------------------------------------------------------------------------------------

PL/SQL

- ANSI-SQL의 결과를 PL/SQL 변수에 대입가능

1. select into 절 사용
- 결과셋의 레코드가 1개일때만 사용 가능한 방법
- 결과셋의 컬럼은 1개 이상
ex)
declare
  변수 선언;
begin
  select 컬럼 into 변수 from 테이블;
end;

2. cursor 사용
- 결과셋의 레코드가 0개 이상일때 사용 가능한 방법
- 결과셋의 레코드가 2개 이상일때 사용 추천
- 커서변수에 들어간 컬럼수랑 into 뒤에 오는 컬럼수랑 일치해야함 (안그럼 에러남)
ex)
declare
  커서 선언; --결과셋 참조 객체(=자바Iterator)
begin
  커서 열기;
    loop
      레코드 접근 + 커서 참조 → 데이터 조작
    end loop;
  커서 닫기;
end;

ex)
declare
    vname tblInsa.name%type;
    cursor vcursor is select name into vname from tblInsa;
begin
    open vcursor; --커서 열기(커서가 가지고있는 select문이 이때 실행된다. 그리고 결과셋을 참조한다.)
        loop --커서가 실행한 select의 결과 → 결과셋의 레코드를 탐색하는 도구
            --select 컬럼 into 변수
            --fetch 커서 into 변수
            fetch vcursor into vname; --현재 커서가 가리키고 있는 레코드의 값을 가져와서 vname에 넣어라 + 커서 전진(다음 레코드)
            exit when vcursor%notfound;
            dbms_output.put_line(vname);
        end loop;
    close vcursor; --커서 닫기
end;

ex2)
create or replace procedure chkStudent(pid varchar2)
is
    cursor vcursor
    is
        select * from tblStudent where upper(id) like '%'||upper(pid)||'%'; --like 사용시 이렇게 작은따옴표로 감싸야함
        vrow tblStudent%rowtype;
begin
    open vcursor;
        loop
            fetch vcursor into vrow;
            exit when vcursor%notfound;
            dbms_output.put_line(
                vrow.name||','||vrow.id||','||vrow.ssn||','||vrow.phone||','||vrow.email||','||to_char(vrow.firstRegistrationDate,'yyyy-mm-dd')||','||vrow.employmentField
            );
        end loop;
    close vcursor;
end;

ex3) join쿼리 사용시
create or replace procedure chkStudent(pid varchar2)
is
    result number:=0;
    cursor c1
    is
        select
            s.name as name_s,id,ssn,phone,email,firstRegistrationDate,employmentField,b.name as name_b
        from tblstudent s
            left outer join tblRegCourse r
                on s.seqStudent=r.seqStudent
            left outer join tblOpenCourse o
                on o.seqOpenCourse=r.seqOpenCourse
            left outer join tblBasicCourseInfo b
                on b.seqBasicCourseInfo=o.seqBasicCourseInfo
        where upper(s.id) like '%'||upper(pid)||'%'
        order by 1;
    vrow c1%rowtype;
begin
    open c1;
        loop
            fetch c1 into vrow;
            exit when c1%notfound;
            dbms_output.put(
                vrow.name_s||','||vrow.id||','||vrow.ssn||','||vrow.phone||','||vrow.email||','||to_char(vrow.firstRegistrationDate,'yyyy-mm-dd')||','||vrow.employmentField
            );
            if vrow.name_b is not null then
                dbms_output.put(','||vrow.name_b);
            end if;
            dbms_output.put_line('');
            result:=result+1;
        end loop;
    close c1;
    dbms_output.put_line(result||'건 조회 완료.');
end chkStudent;

----------------------------------------------------------------------------------------------------

★예외처리
https://docs.oracle.com/cd/E11882_01/timesten.112/e21639/exceptions.htm#TTPLS199
(예외 코드→이름 사이트)

declare
    --선언부
    vdata number;
begin
    --구현부(실행부)
    dbms_output.put_line('시작');
    
    --ORA-06502: PL/SQL: numeric or value error: character to number conversion error
    select basicpay into vdata from tblInsa where num=1005; --이름 → number변수
    dbms_output.put_line(vdata);
    
    --ORA-01476: divisor is equal to zero
    vdata := 0;
    dbms_output.put_line(100/vdata);
    
    dbms_output.put_line('끝');
exception
    --예외 처리부
    
    when VALUE_ERROR then
        dbms_output.put_line('자료형 불일치');
    when ZERO_DIVIDE then
        dbms_output.put_line('0으로 나누려고함');
    when others then --catch(Exception e) 동일 : 모든 예외를 잡는다
        dbms_output.put_line('기타 예외처리');
end;

----------------------------------------------------------------------------------------------------

-- 익명 프로시저 선언
[declare
    변수 선언;
    커서 선언;]
begin
    구현부;
[exception
    예외처리;]
end;

ex)
declare
    vnum number;
begin
    vnum := 100;
    dbms_output.put_line(vnum);
end;


-- 저장 프로시저 선언
create [or replace] procedure 프로시저명
is(as)
    [변수 선언;
    커서 선언;]
begin
    구현부;
[exception
    예외처리;]
end [프로시저명];

ex)
create or replace procedure procTest
is
    vnum number;
begin
    vnum := 100;
    dbms_output.put_line(vnum);
end procTest;


★호출방법

PL/SQL 블럭에서 호출하기
begin
    procTest;
end;

스크립트 환경(select * from tblInsa;그냥 이렇게 쓰는곳)에서 호출하기
execute procTest();
또는
exec procTest();
또는
call procTest();

----------------------------------------------------------------------------------------------------

기본값 사용 default

create or replace procedure procTest(
    width number,
    height number default 10
)
is
    vresult number;
begin
    vresult := width * height;
    dbms_output.put_line(vresult);
end procTest;

begin
    procTest(10,20);
    procTest(30);
end;

----------------------------------------------------------------------------------------------------

/*매개변수 모드

1. in 모드 → 기본 모드
2. out 모드
3. in out 모드*/

create or replace procedure procTest(
    vnum1 in number,
    vnum2 in number,
    vresult out number, --반환 매개변수(리턴값)
    vresult2 out number,
    vresult3 out number
)
is
begin
    vresult := vnum1 + vnum2;
    vresult2 := vnum1 * vnum2;
    vresult3 := vnum1 / vnum2;
end;

declare
    vaaa number;
    vbbb number;
    vccc number;
begin
    procTest(10,20,vaaa,vbbb,vccc);
    dbms_output.put_line(vaaa);
    dbms_output.put_line(vbbb);
    dbms_output.put_line(vccc);
end;

----------------------------------------------------------------------------------------------------

SQL 처리 순서

1. ANSI-SQL or 익명 프로시저
  : 클라이언트 구문 작성(select) → 실행(ctrl+Enter) → 명령어가 오라클 서버에 전달
    → 서버에서 명령어를 수신 → 구문 분석(파싱) → 컴파일 → 실행 → 결과 도출
    → 결과셋을 클라이언트에게 반환
  : 한번 실행했던 명령어를 다시 실행 (위의 과정을 다시 처음부터 끝까지 재실행한다)
  : 첫번째 실행 비용 = 다시 실행 비용

2. 저장 프로시저(PL/SQL)
  : 클라이언트 구문 작성(select) → 실행(ctrl+Enter) → 명령어가 오라클 서버에 전달
    → 서버에서 명령어를 수신 → 구문 분석(파싱) → 컴파일 → 실행 → 결과 도출
    → 결과셋을 클라이언트에게 반환
  : 한번 실행했던 명령어를 다시 실행 → "구문 분석(파싱) → 컴파일" 과정이 생략된다. (★이 부분의 비용이 감소)
  : 재실행 비용 < 첫번째 실행 비용

---------------------------------------------------------------------------------------------------

자식 테이블 찾기

SELECT fk.owner, fk.constraint_name , fk.table_name
FROM all_constraints fk, all_constraints pk
WHERE fk.R_CONSTRAINT_NAME = pk.CONSTRAINT_NAME
AND fk.CONSTRAINT_TYPE = 'R'
AND pk.TABLE_NAME = 'TBLUSER'
ORDER BY fk.TABLE_NAME;

복붙해서 테이블부분만 변경 (대문자로 저장되기때문에 대문자로 입력해야함)

---------------------------------------------------------------------------------------------------

★저장함수(Stored Function)
함수, Function
: 반환값이 반드시 원자값이여야 한다. → 값 1개만을 반환하는 프로시저
: 함수에서도 in, out 사용할 수 있다 → 절대로 out 파라미터를 사용하면 안된다(함수개념X)

create or replace function fnSum(
    pnum1 number,--받을 자료형
    pnum2 number--받을 자료형
)return number --돌려줄 자료형
is
begin
    return pnum1+pnum2;
end;

함수 생성이 끝났으면
declare
    vresult number;
begin
    vresult := fnSum(100,200);
    dbms_output.put_line(vresult);
    
    dbms_output.put_line(fnSum(300,400));
end;
이렇게 PL/SQL로 호출하거나

ANSI-SQL에서 부르기 가능
select height,weight,height+weight,fnSum(height,weight) from tblcomedian;


ex2)
--성별(남자|여자)
select name,buseo,jikwi,
    case
        when substr(ssn,8,1)='1' then '남자'
        when substr(ssn,8,1)='2' then '여자'
    end as gender
from tblinsa;
이렇게 써야 했던걸

create or replace function fnGender(
    pssn varchar2  --받을 자료형
)return varchar2 --돌려줄 자료형
is
begin
    return case
        when substr(pssn,8,1)='1' then '남자'
        when substr(pssn,8,1)='2' then '여자'
    end;
end;

select name,buseo,jikwi,fnGender(ssn) from tblinsa;

이렇게 함수화 처리 가능 (함수부분먼저 만들고 저장해야함)

---------------------------------------------------------------------------------------------------

반환값(out) 프로시저 (함수X)
- 단일값
1. number
2. varchar2
3. date
다중값
4.cursor ★

---------------------------------------------------------------------------------------------------

★트리거(Trigger)
- 프로시저의 한 종류
- 개발자의 호출이 아닌, 미리 지정한 특정 사건이 발생하면 자동으로 실행되는 프로시저(예약+이벤트)
- 특정 테이블 지정 -> 감시 -> insert or update or delete -> 미리 준비해놓은 프로시저가 자동 실행
- 트리거가 많아지면 시스템 속도가 느려진다.

create or replace trigger trgInsa
    before 또는 after --삭제되기 전/후
    delete on tblinsa
begin
    dbms_output.put_line('트리거가 실행되었습니다.');
    if to_char(sysdate,'dy')='목' then
        -- 현재 진행하려던 업무를 없었던 일로 만들기 → 강제로 예외 발생(에러 발생) = 자바의 throw new Exception();
        -- (-20000 ~ -29999)
        raise_application_error(-20001,'목요일에는 퇴사가 불가능합니다.');
    end if;
end;


ex) tblLogMen테이블을 만들어서 tblMen에서 수정된 로그가 tblLogMen안에 저장되게 하기
select * from tblMen;
create table tblLogMen(
    seq number primary key,
    message varchar2(1000) not null,
    regdate date default sysdate not null
);
create sequence seqLogMen;

create or replace trigger trgLogMen
    after
    insert or update or delete on tblMen
declare
    vmessage varchar2(1000);
begin
    if inserting then
        vmessage := '새 남자가 추가되었습니다';
    elsif updating then
        vmessage := '특정 남자의 정보가 수정되었습니다';
    elsif deleting then
        vmessage := '특정 남자가 삭제되었습니다';
    end if;
    
    insert into tblLogMen values(seqLogMen.nextVal,vmessage,default);
end;

select * from tblLogMen;
select * from tblMen;

insert into tblMen values('한가인',25,100,80,null);
insert into tblMen values('박수진',26,100,80,null);
delete from tblMen where name='아이린';
update tblMen set weight=80 where name='배수지';


ex) 레코드(행)단위로 계속 실행되도록 하기(사건마다 실행) - for each row 추가
create or replace trigger trgMen
    after
    delete on tblMen --n개의 테이블 삭제됨
    for each row
begin
    dbms_output.put_line('레코드가 삭제됩니다.'); --n번이 출력된다
end;

delete from tblMen;


★for each row 사용하는 경우
- 상관관계(:old, :new)를 사용한다 → 가상 행(prior)
1. insert
  - 트리거내에서 방금 insert된 레코드의 컬럼값을 참조할 수 있다.
  - :new → 방금 추가된 행
  - :new.컬럼명 → 방금 추가된 행의 컬럼
  - 주로 after 트리거에서 사용한다.
2. update
  - 트리거내에서 방금 update된 레코드의 전,후 컬럼값들을 참조할 수 있다.
  - :new → 방금 수정된 행
  - :old → 방금 수정되기 전 행
3. delete
  - 트리거에서 방금 delete된 레코드의 컬럼값들을 참조할 수 있다.
  - :old → 방금 삭제된 행
  - 주로 before 트리거에서 사용한다.

ex)
create or replace trigger trgDeleteStaff
    before --2.직원이 삭제되기 전
    delete on tblStaff --1.직원의 삭제를 감시하다가
    for each row --3.해당 직원의 정보를 사용해서
begin
    --4.아래 내용을 실행하겠다
    update tblProject set
    staff=6
    where staff = :old.seq; --:old.seq 방금 삭제하려는 직원의 seq
end;

delete from tblStaff where seq=2;

---------------------------------------------------------------------------------------------------

데이터 2배(두배) 늘리기

insert into 테이블명(컬럼명1, 컬럼명2, 컬럼명3…) (select 시퀀스명.nextval, 컬럼명2, 컬럼명3… from 테이블명);

---------------------------------------------------------------------------------------------------

11g 이후 시퀀스가 2부터 시작되는 현상이 있는데 이를 방지하기 위한 방법으로 2가지 방법이 있다

1. 테이블 생성시 마지막에 추가
CREATE TABLE MEMBER_TL (
	seq NUMBER PRIMARY KEY, /* 번호 */
	.
	.
	.
)SEGMENT CREATION IMMEDIATE;

2. 시퀀스 생성시 마지막에 추가 (이건이상한듯 1부터 시작했다가 0부터 시작했다가...)
CREATE SEQUENCE MEMBER_SQ
increment by 1 start with 0 minvalue 0;
increment by:몇칸씩갈건지 start with:시작값 MINVALUE:최소값

---------------------------------------------------------------------------------------------------

★ 테이블을 분리할때(정규화)
1. 한 속성(column)내의 값은 없거나(null) 1개여야한다 (1NF, 제1정규화)
2. 복합키/슈퍼키(2개이상의 후보키가 아닌 속성이 모여 기본키)를 쓸때,
  복합키가 아닌 다른 속성이, 복합키중 1개속성에만 의해서도 값이 정해질경우(2개이상 속성의 같은값이 서로 똑같은경우),
  그 컬럼들을 묶어 새 테이블로 분리한다 (2NF, 제2정규화)
3. 2개이상 묶을 수 있는(2개이상 속성의 같은값이 서로 똑같은경우) 속성(column)끼리는 묶어서 새 테이블로 빼야한다 (3NF, 제3정규화)
4. 여러 테이블에 똑같은 컬럼들 있을때 같이 써도 되는건 한테이블로


★ 외래키 연결할때 참고 (1:N / N:1 / N:M)

<관계 맺을때>
ERD를 그릴때 외래키를 연결해야할지 말아야 할지 모르겠으면
한 데이터를 다른 테이블에서 필요로 하는지, 한 데이터를 수정/삭제할경우 다른 데이터가 같이 지워지는 등 영향을 받는지(원글의 댓글 등) 생각해보기

<1:N / N:1 관계에서 어떤게 부모이고 어떤게 자식인지 구분법>

① 나중에 생긴쪽이 자식(1:N에서 N)이다
  예를들어 [게시글]테이블이 있고 [댓글]테이블이 있을때, 원글이 부모, 댓글이 자식(1:N에서 N)이다
(데이터가 먼저 생기는게 부모, 늦게 생기는게 자식이라고 생각하면 대부분 맞다. (원글이 있어야 댓글이 있을 수 있으니까)).
부모테이블의 행(값들)이 있어야 자식테이블의 행(값들)이 있을 수 있다고 생각. (게시글이 있어야 첨부이미지도 있는것. 첨부이미지만 있을 순 없음)

② 다른테이블에 있는 데이터를 끌어다가 쓰는쪽이 자식(1:N에서 N)이다
  예를들어 [운동종류]테이블이 있고 [오늘 할 운동]테이블이 있을때, 오늘 할 운동은 무슨운동을 할지
운동종류를(운동을 어떻게하는지를) 알아야 운동을 할수있므로(운동종류 테이블에서 끌어다 써야하므로) 운동이 부모(1:N에서 1)이고
오늘 할 운동은 자식(1:N에서 N)이다. 반대로 [운동종류]는 [오늘 할 운동]테이블의 컬럼이 없어도 문제가 없이 단독으로 테이블을 활용할 수 있다

③ 여러 행이 하나로 모이는 쪽이 부모(1:N에서 1)다 (②와 같은말)
여러개의 행(값들)을 다른 테이블에서 쓰면 쓰는쪽이 1이니까 부모테이블이다. 뭔말인지 모르겠다면 엑셀에 속성이랑 값을 2행만 직접 그려보기

④ ★부모자식이라는 말보다는, 그냥 단순하게, 내 테이블에서(내 입장에서) 필요한 컬럼들이 무엇인지 생각하기
  예를들어 회원이 어느 한 날짜에 했던 운동을 기록하는 [일별운동]테이블이 있다고 할때, 이 테이블은 회원이 반드시 필요하다.
무슨 뜻이냐면 이 [일별운동]테이블에서의 컬럼은 번호(PK), 운동번호(FK), 회원번호(FK), 운동횟수, 세트수, 날짜
이렇게 회원번호가 꼭 있어야 한다.

만약 그게 아니고 [일별운동]테이블에 {번호(PK), 운동번호(FK), 운동횟수, 세트수, 날짜} 이렇게 회원번호가 없는 상태라면
[일별운동]의 튜플들은 누가 한 운동인지를 알수없는(부모가없는) 쓰레기값들이 모여있게 된다
ex)
{1번,1번,10회,5세트,해당날짜}
{2번,2번,15회,4세트,해당날짜}
{3번,3번,20회,3세트,해당날짜}
위처럼 말이다

이걸 다른곳에서 갖다 쓸라 해봤자 누가 운동을 했는지 모르기때문에,
테이블에 데이터를 한번 담갔다가 바로 빼서 사용하고 다음번에 필요할땐 못찾는(저장 기능을 못하는) 1회용으로밖에 못쓴다(거의 DTO/VO 수준)
[일별정보]라는 다른 테이블에서 [일별운동]을 끌어다 쓰려고할경우 말이 안된다. 왜냐면 운동을 누가 했는지 구분이 안가기 때문이다


<관계선을 연결하는 방법>
eXERD에서 연결할때는 두가지 방법이 있음

① 먼저 부모에서 자식으로 연결선을 잇고 → 만들어진 컬럼을 변경
일단 연결을 하면 외래키컬럼이 자동 추가되는데, 추가된 외래키컬럼명을 변경한다

② 먼저 필요한 모든 컬럼들을 만들고 → 그 컬럼들 중에서 외래키를 지정
(eXERD에서는 연결선 클릭하고 space누르고 변경하면 됨. 자동으로 만들어진 컬럼은 제거)

예를 들어서
[회원]테이블, [게시글]테이블, [댓글]테이블 이 있을때

[게시글]에서 필요한요소를 {작성자명, 제목, 내용, 작성일, 첨부파일} 이렇게 구성했다고 하고,
[댓글]에서 필요한요소를 {원글번호, 작성자명, 내용} 이렇게 구성했을때

[게시글] 테이블에서는..
작성자명은 작성자 번호를 알면 회원테이블에서 매치시켜서 가져올수 있기때문에
컬럼은 {번호(기본키), 작성자번호, 제목, 내용, 작성일, 첨부파일} 이렇게 만들어진다

[댓글] 테이블에서는..
작성자명도 작성자번호를 알면 매치시켜 가져올수 있기때문에
컬럼은 {번호(기본키), 원글번호, 작성자번호, 내용} 이렇게 구성할 수 있다.

이제 회원과 게시글을 연결하고, 회원과 댓글을 연결하는데

부모(1:n관계에서 1)는 [회원]테이블이 돼야 하고,
자식(1:n관계에서 n)은 [게시글],[댓글]이 돼야 하며 외래키를 원게시글/댓글 의 작성자번호로 지정하면된다

그리고 원글과 댓글도 당연히 연결해주어야하는데
[게시글]과 [댓글]을 연결하고 [댓글]에서 [원글번호]를 외래키로 지정하면된다


★ 다대다(N:M) 관계인지 쉬운 구별법
한개의 테이블안에있는 행이 다른 테이블안에 있는 여러개의 행을 가질 수 있는지 문장을 만들어서 이상한지 생각해보기

ex) [운동] [운동부위]
1개의 운동이 여러가지 부위를 가질 수 있고,
1개의 부위가 여러가지 운동을 가질 수 있다.
(한가지 운동으로 여러가지 부위를 쓸 수 있고, 한부위에도 여러가지 운동방법이 있으므로 N:M관계가 성립)

ex) [회원] [게시글]
하나의 회원이 여러개의 게시글을 작성가능하지만,
하나의 게시글은 여러개의 회원을 필요로 하지 않으므로 N:M관계가 아니라 그냥 1:N관계임


eXERD에서 다대다(N:M) 관계를 표현하려면 아래와 같이 연결하면 된다

 ㅡㅡㅡㅡ        ↗  ㅡㅡㅡㅡㅡㅡㅡㅡ  ↖       ㅡㅡㅡㅡㅡ
|   운동   | ㅡㅡ→   | 운동_운동부위 |   ←ㅡㅡ | 운동부위 |
 ㅡㅡㅡㅡ        ↘  ㅡㅡㅡㅡㅡㅡㅡㅡ  ↙       ㅡㅡㅡㅡㅡ

---------------------------------------------------------------------------------------------------

주로 쓰는 명명법

① snake case + 대문자 (DB)
USER_NAME

② snake case + 소문자 (DB)
user_name

③ camel case (주로 미들?)
userName

④ kebab case (주로 프론트?)
user-name

⑤ pascal case
UserName

⑥ hungarian notation (사장)

⑦ 기타
한글로.. 사번 → sabun

테이블등 오브젝트명은 보통 풀네임으로 표기
TBL_EXR, EXR_TL
↓
TBL_EXERCISE , EXERCISE_TL

---------------------------------------------------------------------------------------------------

데이터 물리삭제와 논리삭제

물리삭제 : DELETE명령으로 실제로 행을 제거하는것
논리삭제 : UPDATE명령으로 삭제 플래그를 이용하여 데이터가 삭제된것처럼 가정하는 방법

# 논리삭제 장점
- 데이터를 삭제하지 않기 때문에 삭제되기 전의 상태로 간단히 되돌릴 수 있음

# 논리삭제 단점
- 삭제해도 DB 저장공간이 늘어나지 않음 (DB 크기가 증가하면 검색속도가 떨어짐)
- 애플리케이션 측 프로그램에서는 DELETE 명령임에도 불구하고 UPDATE 명령을 실행하므로 혼란을 야기할 수 있음

사용자의 개인정보를 다루는 시스템에서는 사용자가 탈퇴한 경우 데이터를 삭제한다.
이때 개인정보를 취급하는 마스터 테이블에서 삭제할 경우에는 물리삭제를 하는 편이 안전할 것이다.
개인정보 유출을 미연에 방지하는 측면에서도 좋은 선택이라고 할 수 있다.

쇼핑 사이트의 경우 사용자가 주문을 취소할 경우에도 데이터를 삭제한다.
이러한 경우에는 논리삭제 방법을 많이 사용한다. 주문이 취소되었다고해도 발주는 된 것으로,
해당 정보가 완전히 불필요한 것이라고는 말할 수 없다. 이러한 데이터는 특히 주문 관련 통계를 낼 때 유용하게 사용할 수 있기 때문이다.

---------------------------------------------------------------------------------------------------

예약어를 컬럼명/테이블명으로 사용하려면 큰따옴표("")로 묶으면 된다 (mysql은 ``로 묶어야함)
SELECT “DATE”, UPDATE_DT FROM “YEAR”

---------------------------------------------------------------------------------------------------

eXERD에서 포워드엔지니어링 화면 복사해서 .SQL로 저장하기전 먼저..

1. 날짜sysdate 등 default값 있는건 도메인탭에서 설정하는게 좋음 (기본값이 없어도 데이터타입 비슷한건 도메인 쓰면 편함)

2. 테이블선택 → 스페이스바 → 제약사항 → 일반탭 → 조건란에 체크제약 적기 ex) GNDR in('M','F')
  컬럼에 적으면 안되고, 세미콜론적으면 안됨

3. 빠진거 없는지 한번더 확인 (아래 체크리스트 체크해보기)
  ⓐ 데이터타입, 널 허용유무 설정 안한거 있는지
  ⓑ 컬럼명 오타가 있는지
  ⓒ 테이블이름, 시퀀스이름 서로 불일치하는거 있는지 (아웃라인탭에서 위에서부터 하나씩 선택후 이름 복사해서 엑셀로 가져가 left,len,if함수로 대조)
  ⓓ 언더바(_) 썼을경우 __이렇게 실수로 두번쓴거 있는지
  ⓔ 물리명과 논리명(영어와 한글)이 서로 바뀐 테이블·컬럼이 있는지
  ⓕ 모델탭에서 안쓰는 테이블들(다이어그램에 없는 테이블) 삭제한번 해주기 (이 과정은 생략해도됨)
  ⓖ 컬럼명에 예약어를 사용했는지 ex)DATE 등.. "(큰따옴표)로 묶고 써도 되지만 안쓰는게 좋음. 예약어목록참고:https://fightingmamoru.tistory.com/18

4. eXERD → 포워드 엔지니어링
기본적으로 다 체크해제하고
테이블 --- 테이블 생성, 테이블 삭제(이건 drop문끼리 별도파일로 빼기), 
제약 사항 --- Primary Key Constraint 생성, Unique Constraint 생성, Foreign Key Constraint 생성, Check Constraint 생성
코맨트 --- 코맨트를 생성하지 않음

이렇게 세팅후(제약사항 설정 안한건 빼도됨) → 다음 → 다이어그램으로 선택 체크(안쓰는테이블 추가 안하기) → 다음 → ctrl+a(전체선택) →
복사 (jdbc 연결해서 해도 되지만 소스코드 재사용을 위해 그냥 복사만 하기)


5. 서브라임으로 일괄처리
서브라임 새창(이하 1번창) 열어서 붙여넣기 → ctrl+f → "_TO_" 입력 → esc → alt+f3(동일문자열 전체선택)
→ 왼쪽 오른쪽 이동하면서(ctrl+좌우방향키/alt+좌우방향키/home/end 들을 적절하게 이용) 테이블약어 ('_TL' 이런거)
각각 제거 → (외래키 제약사항명이 테이블명+테이블명으로 합쳐지는데, 30글자를 넘어가면 오류나므로 수정하는것)
ctrl+shift+p → "Indentation:Convert to Tabs" 복붙후 엔터 →
"CREATE TABLE" 잡고 alt+f3 → 아래화살표 → ctrl+m → 오른쪽화살표 → "SEGMENT CREATION IMMEDIATE" 복붙 (시퀀스1부터시작하게하는것)

6. DROP문 빼기
페이지 위쪽에 DROP TABLE문들 잘라서 새창(이하 2번창) 열고 붙여넣기,
  조작해서 DROP SEQUENCE로 바꾸고, 테이블물리명→시퀀스물리명으로 수정 한 다음, 조작해서 ;(세미콜론) 뒤에 논리명 주석 달기 (--한글명)

7. CREATE SEQUENCE 만들기
6번에서 만든 DROP SEQUENCE 들을 복사해서 처음 붙여넣었던 1번창으로 가서 제일 하단에 붙여넣은 후, DROP→CREATE로 수정

8. SQL파일로 두페이지 create&alter.sql, drop.sql로 저장하기

9. SQL디벨로퍼 열고 접속탭에서 계정 더블클릭해서(이미 접속돼있으면 계정우클릭→재접속) 접속해서 새창 열고 그페이지에
윈도우탐색기에서 파일2개 드래그앤드랍해서 가져와 열기(파일→열기로 열어도 됨)
create&alter 파일 f5눌러서 오류나는지 만들어(실행시켜)보기

10. DML(insert문) 샘플 만들기
서브라임으로 다시 가서 create&alter.sql에서 'CREATE TABLE'드래그 → alt+f3 → ↓(한칸 내리기) → ctrl+shift+m → ctrl+c →
ctrl+n → ctrl+v → 
탭문자열잡고(드래그하고) alt+f3 → (※만약탭문자열이 없으면 ctrl+a(전체선택) → tab눌러서 내용이 있는줄들을 한칸 밀어주고 드래그)
delete → ctrl+우측화살표 → shift+end → ,(쉼표) → delete → space → end → ctrl+backspace →
home → "INSERT INTO " 복붙 후 커서유지 (커서를 딴데 눌러버렸다면 ctrl+u)

11. drop.sql로 가서 "DROP TABLE" 잡고 alt+f3 → 우측방향키 x2 → shift+end → 좌측화살표 → ctrl+c →
이전창으로 다시 돌아가기 → ctrl+v →
(이때 만약 창이 엄청 늘어나면서 한곳에 여러개가 들어가면 개수가 안맞아서 그런것. 실행취소 후 양쪽 개수 다른거 확인하고 빠진거 넣고 다시하기)
"(" 추가(괄호) → ctrl+shift+우측화살표 → ctrl+c → end → ")" 추가(괄호) → ctrl+v → ctrl+좌측화살표 → " VALUES(" 복붙 → end → ".NEXTVAL);" 복붙

12. insert_sample.sql이나 insert_sample.txt로 일단 한번 저장

13. 한글컬럼명 + 쉼표 넣어놓기
create&alter.sql에서 "CREATE TABLE" 잡고 alt+f3 → 아래화살표 → ctrl+shift+m → ctrl+c →
ctrl+n → ctrl+v → "/*" 잡고 alt+f3 → shift+home → delete X 4 → end → backspace X 3 →
첫번째가 아닌 테이블의 첫번째컬럼명 앞에 커서 놓고 → shift+위쪽화살표x2 → alt+f3 → delete → enter → tab →
shift+home → alt+f3 → ,(쉼표) → space → end → delete → home → ctrl+delete x2 → shift+end → ctrl+x →
insert_sample.sql에서 'NEXTVAL'잡고 alt+f3 → 우측화살표 → ctrl+v

(컬럼명 없이 쉼표 개수만 엑셀로 맞추는방법)
먼저 ctrl+a → tab → 탭문자열 드래그 → alt+f3 → backspace 두번 눌러서 줄 붙여놓고 → 전체복사→
엑셀 열고 a1셀에 붙이기 → b1셀에 아래 수식 적용(그냥 붙여넣으면 됨)
=REPT(",",LEN(A1)-LEN(SUBSTITUTE(A1,",","")))
이후 셀우측하단꼭짓점(커서십자가)더블클릭 해도되고 드래그 해도되고 범위지정후 f2→ctrl+enter 해도됨 →
이후 쉼표들만 복사해서 서브라임 insert_sample로 다시 갖고온다음 빈공간에 붙여넣고, 다시 그대로 짤라서 → 일괄선택하고 NEXTVAL뒤에 붙이기
(엑셀에서 셀을 복사할때는 빈공간에 한번 옮겨서 순수텍스트로 만들어줘야한다)
★이때 중요한건 엑셀에서 갖고온걸 그대로 잘라야지, 공백인 줄을 같이복사할경우 복사한요소의 수와 붙여넣을커서의 수가 안맞아서 결과가 이상해짐
다 했으면 한번더 저장. 엑셀은 필요없으니 꺼도 됨

14. 논리테이블명(한글) 주석 추가
create&alter.sql에서 "CREATE TABLE" 잡고 alt+f3 → 위쪽화살표 → shift+end → ctrl+c →
insert_sample.sql로 다시 이동 → "INSERT INTO" 잡고 alt+f3 → 왼쪽화살표 → ctrl+v → enter

---------------------------------------------------------------------------------------------------

이후 테이블들의 관계가 몇층(depth/단계)인지 알아내야하는데
exerd에서 봤을때 외래키가 하나도 없는게 1층이고,
외래키가 1개이상 있다면, 초기값 1에서, 테이블 하나를 타고 올라갈 때마다 +1을 한다.
외래키가 2개이상있다면 각각 다 타보기. 올라가다가 또 여러갈래길(여러 외래키)이 나오면 각각 다 타보기.
최상위 루트까지의 거리가 가장 멀때(숫자가 가장 높을때) 나온 숫자가 해당테이블의 층이 된다

같은층끼리 모아 순서대로 insert문을 구성한다 (순차적으로 실행되는데 참조할 행이 미리 안만들어져있으면 삽입이 안되기때문)

더미데이터는 여기서 쓰면 편하다 https://www.mockaroo.com/

---------------------------------------------------------------------------------------------------

오라클 멀티 update 안됨. (mysql은됨)
여러개 테이블 한번에 update하려면 프로시저나 트리거로 하기

멀티 insert는 된다고함

---------------------------------------------------------------------------------------------------

가상 테이블 만들기

WITH TESTDB AS(
SELECT '20123153' CODE, '이승현' CODENM, 'Y' USE_YN FROM DUAL UNION ALL
SELECT '20156121' CODE, '박민서' CODENM, 'Y' USE_YN FROM DUAL UNION ALL
SELECT '20143328' CODE, '최유진' CODENM, 'Y' USE_YN FROM DUAL UNION ALL
SELECT '20167832' CODE, '김애신' CODENM, 'N' USE_YN FROM DUAL UNION ALL
SELECT '20134252' CODE, '김동매' CODENM, 'Y' USE_YN FROM DUAL
)
SELECT *
FROM TESTDB

---------------------------------------------------------------------------------------------------

UPSERT 쿼리 (INSERT + UPDATE)
MERGE INTO 이용. 조건에 맞는 행이 있을때 해당행을 업데이트 하는 기능

MERGE INTO TABLE_NAME TBL1
  USING TARGET_TABLE TABL2  -- 동일한 테이블일 경우 TARGET_TABLE을 DUAL로 지정
  ON TBL1.COLUMN_NAME = TABL2.COLUMN_NAME  -- 두 테이블을 JOIN하는 조건문
WHEN MATCHED THEN  --조건에 맞을 경우
    UPDATE SET COL1 = VAL1
                       ,COL2 = VAL2
                       ,COL3 = VAL3
WHEN NOT MATCHED THEN  --조건에 맞지 않을 경우
    INSERT(COL1, COL2, COL3)
    VALUES(VAL1, VAL2, VAL3)


ex)
CREATE TABLE TEST_TABLE (
	COMPANY_CODE  VARCHAR2(10) NOT NULL,--회사코드
	COMPANY_NAME VARCHAR2(50) NOT NULL --회사이름
);
MERGE INTO TEST_TABLE
USING DUAL
	ON (COMPANY_CODE = '1')
WHEN MATCHED THEN
	UPDATE SET COMPANY_NAME = '삼성전자'
WHEN NOT MATCHED THEN
	INSERT (COMPANY_CODE, COMPANY_NAME) 
	VALUES ('1','현대자동차');

---------------------------------------------------------------------------------------------------

NVL (null일때 특정값 넣기)

ex. null일때 0넣기)
SELECT NVLl컬럼명, 0) FROM 테이블명;

---------------------------------------------------------------------------------------------------

중복 없이 특정컬럼 카운트

SELECT COUNT(DISTINCT COOKIE_VAL)
FROM TGPR_LOG

---------------------------------------------------------------------------------------------------

dmd 확장자 파일 불러오기

파일 > Data Modeler > 임포트 > Data Modeler 디자인 > 파일 선택

---------------------------------------------------------------------------------------------------




















