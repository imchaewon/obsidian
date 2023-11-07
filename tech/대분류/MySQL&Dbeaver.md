Operand should contain 1 column(s)
↓↓↓↓↓
1개의 열이 필요하지만 서브쿼리가 2개이상의 열을 반환


(conn=2809) Subquery returns more than 1 row
↓↓↓↓↓
1개의 행만 필요한 서브쿼리가 2개 이상의 행을 반환한 경우 발생.
WHERE절이나 SELECT절에서 값을 1개씩만 가져와야할경우는 서브쿼리를 쓰는게 아니라 그냥 쓰면됨(from절을 쓰지 말기)
ex) WHERE SUBSTRING_INDEX(SUBSTRING(DETAIL, INSTR(DETAIL, "name\":\"")+7),"\"",1) LIKE '%김%';


SQL Error [1064] [42000]: (conn:230) You have an error in your SQL syntax;
check the manual that corresponds to your MariaDB server version for the right syntax to use near '' at line 5
↓↓↓↓↓
1. 디비버 sql문 중간에 공백줄 있을때 커서 아무데나놓고 ctrl+enter(실행) 하면 위와같이 오류남.
	공백줄을 없애거나 sql문전체를 드래그래서 잡고 ctrl+enter(실행) 해야됨.
2. 엉뚱한 테이블에 값을 insert 하려고 했을때 → near ')'


Could not connect to address=(host=localhost)(port=3306)(type=master) : 
Socket fail to connect to host:localhost, port:3306. Connection refused (Connection refused)
도커 안켜져있을때(DB연결 안되어있을때)


java.sql.SQLSyntaxErrorException: (conn=18254) You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'WHERE DEVICE_DIV_CD = 'P' 
↓↓↓↓↓
WHERE 절보다 GROUP BY 절을 뒤에 쓴 경우


SQL Error [08000]: (conn=25705) Broken pipe (Write failed) (ui로 db수정후 저장이 안되는경우)
↓↓↓↓↓
f3 눌러서 아무 select쿼리 한번 실행하고 다시 저장


[42S02][1932] Table 'bootex.member' doesn't exist in engine
↓↓↓↓↓
도커에서 mariadb 재실행

-----

테이블 drop시켰는데 create도 안되고 drop도 안될때
→ 도커에서 이미지 restart하면 됨

-----

You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')
↓↓↓↓↓
GUI로 테이블만들때 아무컬럼도 안넣은경우

-----

java.lang.RuntimeException: [42000][1064] (conn=5) You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near
↓↓↓↓↓
자료형을 varchar2 로 만들었는지 확인 (mysql에 varchar2는 없음)

-----

[HY000][1005] (conn=93778) Can't create table `KTO`.`SRCH_LOG_PV` (errno: 150 "Foreign key constraint is incorrectly formed").

외래키를 자료형을 대상 컬럼과 똑같이 맞추기

-----

[ERROR] Caused by: org.apache.ibatis.type.TypeException: Error setting non null for parameter #3 with JdbcType null . Try setting a different JdbcType for this parameter or a different configuration property. Cause: java.sql.SQLException: Could not set parameter at position 3 (values was 0)
↓↓↓↓↓
# 주석과 mybatis 파라미터 변수 호출할때 #{} 이 충돌남
↓↓↓↓↓

주석을 # 으로 하지 말고

# (SELECT @tnmId:=#{tnmId }) M,
# (SELECT @pblcnYm:=PBLCN_YM FROM TRSS_NSLTR_MASTER WHERE TNM_ID = #{tnmId}) D,

<!-- --> 이 주석으로 바꿔야함

대신 드래그후 cmd + enter하면 실행 안되니 주의(주석까지 제거하거나 그냥 커서를 올리고 cmd + enter 해야함)

-----

join을 했는데 원하는 행개수가 안나오고 행이 * n 개씩 나온다면
join의 기준컬럼을 변경해야함. 기본키가 아닌 다른컬럼으로 하면 이상해질 수 있음

-----

join을 했는데 결과가 엄청느리게 혹은 이상하게 나온다면
조인 조건을 넣었는지 확인 (조건이 없으면 모든 레코드가 매칭되는 cross join이 됨)

----------------------------------------------------------------------------------------------------

mariaDB 로컬설치

brew install mariadb

마리아DB 서버 시작?
mysql.server start

사용자 계정으로 로그인
mysql

$ brew services start mariadb //실행
$ brew services stop mariadb //중단
$ brew services list //실행중인지 상태 확인

----------------------------------------------------------------------------------------------------

Database Navigator에서
데이터베이스 선택후 F3	: 스크립트 실행창

cmd + F2				: 스크립트 이름변경

cmd + d					: 한줄 지우기

ctrl + shift + x			: 대문자로 변환
ctrl + shift + y			: 소문자로 변환

alt + x					: 스크립트 전체 실행
cmd + enter				: SQL 문 실행
cmd +shift + enter		: SQL 문 여러줄 실행 ★★★
cmd + \				: 새 탭(결과)에서 SQL 문 실행

cmd + alt + shift + r		: 롤백
cmd + alt + shift + c		: 커밋

cmd + shift + e			: 실행 계획

cmd + k					: 다음 항목 찾기
cmd + shift + k			: 이전 항목 찾기
cmd + alt + g			: 작업 공간의 파일에서 특정 텍스트를 검색합니다.
cmd + f					: 텍스트 찾기 및 바꾸기
cmd + j					: 증분 찾기

cmd + shift + J			: 텍스트 줄 결합하기
cmd + q					: 최종 수정 위치
cmd + m				: 활성 뷰 또는 편집기의 최대화 / 복원 토글 전환
cmd + shift + 6			: 결과 패널 최대화 / 표준화

cmd + alt + e			: 텍스트 편집기 soft word wrap 토글
cmd + alt + f				: 자동정렬

cmd + shift + enter		: 현재 줄 위에 새 줄을 추가
shift + enter				: 현재 줄 아래에 새 줄을 추가

----------------------------------------------------------------------------------------------------

테이블명/별칭에 .찍었을때 컬럼명 안나오면 오타난것. 대소문자 확인

----------------------------------------------------------------------------------------------------

테이블 검색

테이블 주석으로 테이블 찾기

SELECT table_name, table_comment
FROM information_schema.tables
WHERE table_schema = 'DB명'
	AND table_comment LIKE '%검색어%';

----------------------------------------------------------------------------------------------------

컬럼 검색


컬럼명으로 테이블 찾기

SELECT TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE COLUMN_NAME LIKE '%컬럼명%';

-----

컬럼명으로 테이블 찾기(DB선택)

SELECT TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE COLUMN_NAME LIKE '%컬럼명%' AND TABLE_SCHEMA='KTO';

-----

컬럼 주석으로 테이블 찾기

SELECT table_name, column_name, column_comment
FROM information_schema.columns
WHERE table_schema = 'DB명' 
	AND column_comment LIKE '%검색어%';

----------------------------------------------------------------------------------------------------

유저

(connection을 선택하고 추가해야함. 연습시 mysql(기본으로 connection되어있는 계정)의 스크립트파일에서 해야함)

유저 목록
use mysql
select user, host from user;

조회
SELECT User, Host, Password FROM [커넥션명].USER;

생성
CREATE USER [아이디]@LOCALHOST IDENTIFIED BY '[비밀번호]';
or
CREATE USER [아이디]@'%' IDENTIFIED BY '[비밀번호]'; → '%'는 모든 ip 접속을 허용한다는 의미
or
CREATE USER [아이디]@'localhost' IDENTIFIED BY '[비밀번호]'; → 호스트를 외부접근불가로 설정. host를 다르게 하면
ip접근제어를 할 수 있음. 같은이름의 계정을 호스트를 바꿔서 여러개 생성가능

삭제
drop user [아이디];
or
drop user [아이디]@'%';
or
CREATE USER [아이디]@'localhost' IDENTIFIED BY '[비밀번호]'; → 유저만들때 localhost를 넣었으면 DROP시에도 localhost를 넣어야함


권한부여 및 적용
GRANT ALL PRIVILEGES ON 데이터베이스명.* TO '사용자명'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

-----

데이터베이스
(connection을 선택하고 추가해야함. 연습시 mysql(기본으로 connection되어있는 계정)의 스크립트파일에서 해야함)

조회
SHOW DATABASES;
or
SHOW SCHEMAS;

생성
CREATE DATABASE [데이터베이스명];
CREATE SCHEMA [데이터베이스명];

삭제
DROP DATABASE [데이터베이스명];
DROP SCHEMA [데이터베이스명];

-----

테이블

조회
show tables;

생성
CREATE TABLE 테이블명(
	COMMENT_ID INT,
	NICKNAME VARCHAR(30) UNIQUE,
	GENDER CHAR(1) NOT NULL,
	RegDate DATE,
	PRIMARY KEY(COMMENT_ID),
	FOREIGN KEY(CONTENT_ID) REFERENCES 참조테이블명(참조컬럼명)
)

----------------------------------------------------------------------------------------------------

[42000][1044] (conn=12) Access denied for user '사용자명'@'172.17.0.1' to database 'information_schema'

"information_schema"는 시스템 카탈로그 데이터베이스이므로 사용자가 데이터를 쓰거나 변경할 수 없음
대신 다른 데이터베이스에 작업해야함

----------------------------------------------------------------------------------------------------

// DB의 전체 테이블 조회
SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'DB명';

// DB의 전체 테이블명 및 테이블 코멘트 조회
SELECT TABLE_NAME, TABLE_COMMENT FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'DB명'
ORDER BY TABLE_NAME;

// 특정 테이블의 모든 컬럼 정보 조회
SHOW FULL COLUMNS FROM 테이블명;

----------------------------------------------------------------------------------------------------

자료형 (varchar2, long 은 없음)

정수
tinyint			:	1byte (-128~127) (=자바의byte)
smallint			:	2byte (-32768~32767) (=자바short)
int				:	4byte (-2147483648~2147483647) -21억~21억 (=자바int)
bigint			:	8byte (-9223372036854775808~9223372036854775807) -922경~922경 (=자바long)

실수
float				:	4byte (=자바float)
double			:	8byte (=자바double)
DECIMAL(M,D)	:	M자리 정수(정밀도)와 D자리 소수점(스케일)으로 표현
부동소수점(float/double)은 100%정확하지않아서 정확한계산이 필요할때는 쓰지말고 이걸쓰는게 좋음
dicimal 앞자리는 소수자리를 포함한 총 자리수를 말하고 뒷자리는 소수자리가 차지하는 개수를 말함
decimal(5,2) 이렇게 쓰면 12345.12 가 아니라 123.12 이거다

문자열
char(자리수) : 최대길이255바이트. 고정크기
varchar(자리수) : 최대길이255바이트.가변크기
varchar2는 없음
★오라클과 다르게 글자수 제한이다 char(6) 또는 varchar(6) 이라고 했다면 한글이든 영문이든 6글자까지 들어감. 캐릭터 셋에 따라서 차이가 있을 수도 있다고 함
tinytext : 		256 byte 가변
text : 		65,535 byte (64kb) 가변
mediumtext : 	16,777,215 byte (16mb) 가변
longtext :		4,294,967,295 byte (4gb) 가변

가변은 공간 절약면에서는 효율적이지만 고정에 비해 검색속도가 월등히 떨어짐


★참고로 정수형 옆 괄호안에 INT(1), INT(5), INT(9), INT(11) 숫자설정의 의미는 ZEROFILL을 위한 숫자임
숫자를 넣었다고 해당 자리만큼 공간이 지정되는건 아니며, 화면에 숫자를 표시할 때 숫자 왼쪽에 0을 붙이라는 뜻
만약 Int(5) ZeroFill이라고 정의된 필드에서 저장된 값 3을 불러온다면 5자리에서 값길이를 제외한 나머지는 0으로 채워지게 돼서 "00003"과 같이 표시됨
ZEROFILL 속성이 지정되었을경우에만 영향을 받음★

-----

★ DB의 자료형과 자바의 자료형은 관계가 없음
자바에서 숫자를 String으로 DB에 집어넣어도 DB에서 정수형이면 자동으로 정수형으로 바뀌어서 저장됨
자바에서 숫자를 int로 DB에 집어넣어도 DB에서 문자형이면 자동으로 문자형으로 바뀌어서 저장됨
DB에서 숫자를 숫자형으로 저장해도 자바에서 불러오면 String으로 불러와짐 ( ==1 이 아니라 .equals("1") 이렇게 비교해야함)

-----

mybatis로 불러온 값 널비교

디비버에서 NULL이거나 '' 인 값을 mybatis로 불러왔을경우 NULL로 비교하는게 아니라 .equals("") 로 비교해야함

----------------------------------------------------------------------------------------------------

디비버 널 값 넣기

디비버에서 문자형 셀의 값을 비울경우 NULL이 아닌 ''가 들어간다.
이러면 컬럼을 숫자형으로 변경할수 없음

UPDATE문을 안쓰고 특정 셀을 NULL로 만들기

NULL로 만들 셀 우클릭 → Edit → NULL로 설정

----------------------------------------------------------------------------------------------------

시퀀스 비슷한거(자동증가) - AUTO_INCREMENT
해당 컬럼이 기본키로 등록이 되어있어야함

CREATE TABLE BOOKMARK_TL(
	BOOKMARK_ID INT AUTO_INCREMENT,
	.
	.
)

-----

시퀀스값 변경

ALTER TABLE [TABLE명] AUTO_INCREMENT = [시작할 값];
시작할값보다 높은 값이 존재하면 안됨

-----

테이블에 기록되어있는 시퀀스를 1,2,3,4,5...로 전체 초기화

ALTER TABLE [테이블명] AUTO_INCREMENT=1;
SET @COUNT = 0;
UPDATE [테이블명] SET [AUTO_INCREMENT 열 이름] = @COUNT:=@COUNT+1;

-----

이미 생성된 테이블에 시퀀스 넣기

ALTER TABEL [테이블명] MODIFY [컬럼명] INT NOT NULL AUTO_INCREMENT;

----------------------------------------------------------------------------------------------------

내장 함수 모음


★IF (엑셀/엑세스의 if랑 똑같음. 다른 언어의 삼항연산자)
IF(조건,참,거짓)

ex)
SELECT
	ID,
	SUM(IF(STATS_DIV_CD = 4, TRUE, FALSE)) AS ALL_VIEW
FROM
TGPR_LOG

ex2)
SELECT * FROM LOCAL_GOV_INTRD_BNNR
	WHERE LGM_ID = (SELECT LGM_ID FROM LOCAL_GOV_MASTER WHERE SAVE_STATUS = 1 LIMIT 1)
	AND MAN_ID = IF(#{_parameter} = 'PC', 'fe11d906-f242-11ea-b8bd-020027310001', 'fe11d928-f242-11ea-b8bd-020027310001');

★프로시저/사용자정의함수/트리거에서 쓰는 블럭 if 와 인라인 if 는 다름
ex)
IF (SELECT COUNT(*) FROM DETAIL_INFO WHERE FLD_GUBUN=10 AND COT_ID='a5b789d2-3d56-43d2-9e2b-c2cb2ea18bb2' != 0) THEN
ex2)
IF new.rating IS NOT NULL THEN


★ CASE - 타언어의 switch (조건과 비교할 값을 1번만 넣으면 되서 편리함)
CASE [컬럼]
	WHEN [조건] THEN [값]
	WHEN [조건] THEN [값]
	ELSE [값]
END AS 별칭

ex)
SELECT
	T.COT_ID,
	T.DICT_ID,
	CASE T.DISP_YN
		WHEN 'Y' THEN '노출'
		ELSE '비노출'
	END AS DISP_YN,
	CASE C.CONTENT_TYPE
		WHEN 12 THEN '관광지'
		WHEN 14 THEN '문화시설'
		WHEN 28 THEN '레포츠'
		WHEN 32 THEN '숙박'
		WHEN 38 THEN '쇼핑'
		WHEN 39 THEN '음식점'
		WHEN 15 THEN '축제공연행사'
		ELSE ''
	END AS CONTENT_TYPE
FROM DICT_MASTER T
LEFT OUTER JOIN CONTENT_MASTER C
ON T.COT_ID = C.COT_ID
LEFT OUTER JOIN DATABASE_MASTER D
ON C.COT_ID = D.COT_ID
WHERE 1=1


★ISNULL - 널일때 1반환


★IFNULL - 널일때 2번째 인수 반환

IFNULL(null판단값, NULL일때 출력할값)
ex) IFNULL(1,2) → 1
ex) IFNULL(NULL,2) → 2


★NULLIF - 같다면 NULL 틀리면 첫번째 인수 반환

NULLIF(비교할값1,비교할값2)
ex) IFNULL(1,1) → NULL
ex) IFNULL(1,2) → 1

-----

문자열 함수

★ASCII - 아스키 코드값
ex) ASCII('A') → 65

★CHAR - 아스키코드값에 해당하는 문자
ex) CHAR(65) → A

★BIT_LENGTH - 할당된 Bit 크기 (utf-8은 한글은 3바이트=24비트 영문은 1바이트=8비트)
ex) BIT_LENGTH('가나') → 48
ex) BIT_LENGTH('ab') → 16

★LENGTH - 할당된 Byte 크기 (utf-8은 한글은 3바이트=24비트 영문은 1바이트=8비트)
ex) BIT_LENGTH('가나') → 6
ex) BIT_LENGTH('ab') → 2

★CHAR_LENGTH - 문자의 개수
ex) CHAR_LENGTH('가가') → 2

★CONCAT - 문자 합치기 (|| 같은 연산자는 mysql에는 없음)
ex) CONCAT('가','나','다') → 가나다
ex) 컬럼1 like CONCAT('%',#{keyword},'%')) → 컬럼1 like '%${keyword}%' 랑 똑같음
ex) AND REG_DT &lt; concat(#{edate}'23:59:59.999')

★CONCAT_WS - 문자 구분자로 구분해서 합치기 (다중행 합치는건 GROUP_CONCAT을 써야함)
CONCAT_WS(구분자, 문자열1, 문자열2, [...])
ex) CONCAT_WS('/','2020','01','01') → 2020/01/01

★ELT - 특정 위치의 문자 (1번지 시작)
ELT(번지, 문자열1, 문자열2, [...])
ex) ELT(2,'가','나','다') → 나

★FIELD - 특정 위치의 문자 (1번지 시작)
FIELD(찾을문자열, '문자열1', '문자열2', [...])
ex) FIELD('나','가','나','다') → 2

★FIND_IN_SET - 쉼표(,)로 구분된 문자열에서 찾기 (공백은 없어야함)
FIND_IN_SET(찾을문자열, '문자열1, 문자열2', [...])
ex) FIND_IN_SET('나','가,나,다') → 2

★INSTR - 문자열 검색. 찾으면 index(1부터시작), 못찾으면 1반환
INSTR(원본문자열, 찾을문자열)
ex) INSTR('가나다','나') → 2

★LOCATE - INSTR와 인수만 뒤바뀜
LOCATE(찾을문자열, 원본문자열)
ex) LOCATE('나','가나다') → 2

★INSERT - 특정 자리부터 특정 길이까지 특정 문자열로 바꿈 (1번지시작)
INSERT(원본문자열,시작위치,바꿀길이,바꿀문자열)
ex) INSERT('가나다라마',2,2,'@') → 가@라마

★MID / SUBSTR / SUBSTRING - 특정 자리수부터 특정'길이'만큼 자르기 (자를 길이를 지정하지 않으면 끝까지 가져옴) (엑셀의 mid와 동일, 자바등의 substring과는 다름)
SUBSTRING(원본문자열,시작위치(1부터시작),[자를길이])
ex) SUBSTRING('가나다라마',2,2) → 나다
ex) SUBSTRING('가나다라마',2) → 나다라마

★SUBSTRING_INDEX - 특정위치의 특정문자열 전 까지 자름. INDEX가 음수면 오른쪽에서 검색 (1번지시작)
SUBSTRING_INDEX(원본문자열,찾을문자열,[몇번째에 있는 문자열까지 자를건지])
ex) SUBSTRING_INDEX('www..naver..com','..',2) → www..naver
ex) SUBSTRING_INDEX('www..naver..com','..',-2) → naver..com

★REPLACE - 특정 문자열을 특정 문자열로 바꿈
REPLACE(전체문자열,변경전문자열,변경후문자열
ex) REPLACE('가나다라마','나다','하하') → 가하하라마
ex) REPLACE('가나다라마',SUBSTR('가나다라마',2,2),'하하')  → 가하하라마

★REVERSE - 문자열을 뒤집음
REVERSE('가나다') → 다나가

★LEFT - 왼쪽부터 n자리
ex) LEFT('가나다',2) → 가나

★RIGHT - 오른쪽부터 n자리
ex) RIGHT('가나다',2) → 나다

★LCASE - 소문자로 (LOWER와 동일)
ex) LOWER('aBcDe') → abcde

★UCASE - 대문자로 (UPPER와 동일)
ex) UCASE('aBcDe') → ABCDE

★LPAD - 특정길이를 기준으로 왼쪽부터 남은자리수만큼 특정문자열로 채움 (원본문자열보다 입력한길이가 작을경우 오른쪽이 잘림)
LPAD(원본문자열,길이,채울문자열)
ex) LPAD('가나다',5,'@') → 가나다@@
ex) LPAD('가나다',2,'@') → 가나

★RPAD - 특정길이를 기준으로 오른쪽부터 남은자리수만큼 특정문자열로 채움 (원본문자열보다 입력한길이가 작을경우 오른쪽이 잘림)
RPAD(원본문자열,길이,채울문자열)
ex) RPAD('가나다',5,'@') → @@가나다
ex) RPAD('가나다',2,'@') → 가나

★TRIM - 양끝 공백 제거
ex) CONCAT('\'',TRIM('     가 나  '),'\'') → '가 나'

★LTRIM - 왼쪽 공백 제거
ex) CONCAT('\'',LTRIM('     가 나  '),'\'') → '가 나  '

★RTRIM - 오른쪽 공백 제거
ex) CONCAT('\'',RTRIM('     가 나  '),'\'') → '     가 나'

★REPEAT - 문자열 반복
ex) REPEAT('*',3) → ***

★SPACE - 공백 반복 ( REPEAT(' ',n) 랑 똑같음 )
CONCAT('\'',REPEAT(' ',3),'\'') → '   '

-----

숫자 함수

★FORMAT - 세자리마다 콤마, 소수 반올림
세자리 콤마					: FORMAT(1234567,0) → 1,234,567
세자리 콤마 & 소수1자리로 반올림	: FORMAT(1234567.89,1) → 1,234,567.9
세자리 콤마 & 소수1자리로 반올림	: FORMAT(1234567,1) → 1,234,567.0

★ROUND - 반올림
1의자리로 반올림				: ROUND(12.34,0) → 12
소수1자리로 반올림				: ROUND(12.34,1) → 12.3
10의자리로 반올림				: ROUND(15.34,-1) → 20

★TRUNCATE - 절삭(버림)
1의자리로 절삭					: TRUNCATE(16.54,0) → 16
소수1의자리로 절삭				: TRUNCATE(16.54,0) → 16.5
10의자리로 절삭				: TRUNCATE(16.54,-1) → 10
음수 절삭						: TRUNCATE(16.54,-0) → 16

★CEIL / CEILING - 올림
1의자리로만 올림가능			: CEIL(12.34) → 12

★FLOOR - 내림
1의자리로만 내림가능			: FLOOR(12.34) → 12
1의자리로만 내림가능			: FLOOR(-12.34) → -13

★BIN - 2진수					: BIN(10) → 1010
★OCT - 8진수					: OCT(10) → 12
★HEX - 16진수				: HEX(10) → A
★CONV - 원하는 진수로 변환
CONV(숫자,기존진수,바꿀진수)	: CONV(12,10,2) → 1100


★ABS - 절대값					: ABS(-10) → 10

★ MOD - 나머지				: MOD(10,3) → 1
							: 10 MOD 3 → 1
							: 10 % 3 → 1

★ POW - 제곱근				: POW(2,3) → 8

★ RAND - 0이상 1미만 랜덤실수	: RAND() → 0.xxx
							: TRUNCATE(RAND()*3,0) → 0,1,2 중에 하나

★ SIGN - 양수는1, 음수는-1, 0은0	: SIGN(123) → 1
							: SIGN(0) → 0
							: SIGN(-123) → -1

-----

★숫자를 문자로 (오라클의 ||) (오라클도 CONCAT이 되지만, 인수를 3개이상 쓸 수 없음)

CONCAT(숫자, 문자)

ex) CONCAT(123,'%') → 123%

더하기 연산자(+)는 안됨

-----

★문자를 숫자로

방법1. SELECT CONVERT(컬럼or값, SIGNED)
방법2. SELECT CAST(컬럼or값 AS SIGNED)

----------------------------------------------------------------------------------------------------

집계 함수

COUNT / SUM / AVG / MAX / MIN

----------------------------------------------------------------------------------------------------

★REGEXP - 정규식, 검색 패턴

~ WHERE NAME REGEXP '^a'; → a로 시작하는거 찾기
~ WHERE NAME REGEXP 'E$'; → a로 끝나는거 찾기
~ WHERE NAME REGEXP '^eat$'; → "eat" 를 찾기
~ WHERE NAME REGEXP '^...$'; → 길이가 3인 문자 찾기 (.은 임이의 문자를 의미함)


https://codingdog.tistory.com/entry/mysql-regexp-%EB%B3%B5%EC%9E%A1%ED%95%9C-%ED%8C%A8%ED%84%B4-%EB%A7%A4%EC%B9%AD%EC%9D%84-%ED%95%B4-%EB%B4%85%EC%8B%9C%EB%8B%A4

-----

숫자가 아닌 행 데이터 찾는 쿼리

SELECT * FROM [테이블] WHERE [판단할컬럼] REGEXP '[^0123456789]' = 1;
줄여서 ↓↓↓
SELECT * FROM [테이블] WHERE [판단할컬럼] REGEXP '[^0-9]';

-----

숫자만 있는 데이터

SELECT * FROM [테이블] WHERE [판단할컬럼] REGEXP '^[0-9]+$';

-----

특수문자가 포함된 행 조회

SELECT * FROM [테이블] WHERE [판단할컬럼] REGEXP '[`~!#$%^&*|\\\'\";:\/?]';

-----

데이터가 숫자이고 < 10 인 데이터들만 UPDATE

UPDATE TGPR_MASTER SET PRVD_ENTRPS_CD='4f21fe8e-b8b6-4ee4-9129-3f08ec2766d2'
    WHERE GDS_ID REGEXP '^[0-9]+$'
        AND convert(GDS_ID, signed) < 10

먼저 GDS_ID REGEXP '^[0-9]+$' 이걸로 숫자인지 판단부터 한 후 맞다면 AND 이후의 명령을 실행하게끔 해야함

-----

SELECT * FROM 테이블 WHERE 컬럼 REGEXP 'abc';
||
SELECT * FROM 테이블 WHERE 컬럼 = 'abc';

------------------------------

REGEXP_REPLACE - 정규식으로 replace

-----

숫자만 남기고 나머지 문자 제거

SELECT REGEXP_REPLACE(your_column, '[^0-9]', '') AS numbers_only FROM your_table;

----------------------------------------------------------------------------------------------------

★ JSON데이터

JSON형 데이터중에서 특정 키만 가져오기

JSON_EXTRACT(컬럼명,'$.키')


SELECT
	JSON_EXTRACT(EA.DETAIL, '$.name') AS name,
FROM 테이블


그러면
{"name":"문보현","today":2021110809,"todayCnt":1,"winningYn":"N"}
한 셀에 이렇게 들어있는 데이터들을 

"문현보"

이렇게 가져올 수 있음

-----

큰따옴표 제거

JSON_UNQUOTE(문자열)


JSON_EXTRACT(EA.DETAIL, '$.name')
"문보현"

JSON_UNQUOTE(JSON_EXTRACT(EA.DETAIL, '$.name')) AS name
문보현

----------------------------------------------------------------------------------------------------

★날짜/시간

date자료형 : 날짜만 입력가능 %Y%m%d
time자료형 : 시각만 입력가능 %H%i%S
datetime/timestamp : 둘다 입력가능 %H%i%S
밀리초 입력하고싶을때는 컬럼을 datetime(3) / timestamp(3) 이렇게 만든 후, NOW(3) 이렇게 넣어야함
마이크로초 입력하고싶을때는 컬럼을 datetime(6) / timestamp(6) 이렇게 만든 후, NOW(6) 이렇게 넣어야함
ex 밀리초) INSERT INTO aaaaaaa VALUES(date_format(NOW(3),'%Y-%m-%d %H:%i:%S.%f'))
ex 마이크로초) INSERT INTO aaaaaaa VALUES(date_format(NOW(6),'%Y-%m-%d %H:%i:%S.%f'))

datetime이나 timestamp는 두가지 형식으로 입력할 수 있음
 ① yyyy-mm-dd hh:mm:ss
 ② yyyymmddhhmmss

ex)
INSERT INTO InputTest VALUES("1998-12-31 23:59:59");
INSERT INTO InputTest VALUES("19981231235959");

%Y		4글자 년
%y		2글자 년
%m		2글자 월(00~12)
%c		1~2글자 월(0~12)
%M		월(영문 전체 March)
%b		월(영문 축약 Mar)
%e		1~2글자 일(1~30)
%d		2글자 일(01~30)
%j		1월 1일부터 해당날짜까지의 일수

%W		요일(영문 전체 Monday)
%a		요일(영문 축약 Mon)
%w		요일(일=0 ~ 월=6)

%T		hh:mm:ss
%r		hh:mm:ss AM/PM
%H		시(24시간 표기법)
%l		시(12시간 표기법)
%i		분
%S		초
%f		마이크로/밀리초

%p		AM or PM

-----

현재 날짜/시간

현재 날짜&시간 - NOW() or SYSDATE()
현재 날짜 - CURDATE()

방법1. 테이블을 만들때 자료형으로는 TIMESTAMP 를 넣고
DEFAULT값으로 now() 혹은 CURRENT_TIMESTAMP() 를 넣기
REG_DATE TIMESTAMP DEFAULT CURRENT_TIMESTAMP()

방법2. 날짜시각 컬럼에 INSERT할때 NOW함수로 입력
INSERT INTO BOARD VALUES(
	2, "제목", "내용", "ADMIN", NOW()
);

-----

날짜시간 → 날짜 변환 - DATE

DATE(날짜시간)

-----

문자열 → 날짜 포맷변환 - STR_TO_DATE

함수 적용시 날짜/시각끼리 비교가 가능해짐
오라클의 TO_DATE. 형식을 문자열과 맞춰줘야함

STR_TO_DATE(str, format)

ex)
str : '20120101 00:02:22'
STR_TO_DATE(str, "%Y%m%d %H%i%S") → 날짜시각형으로 변함

ex)
str : '2012_01_20@01^01$01
STR_TO_DATE(str, '%Y_%m_%d@%H^%i$%S') → 날짜시각형으로 변함

-----

날짜 → 문자열 포맷변환 - DATE_FORMAT

오라클의 TO_CHAR.

DATE_FORMAT(날짜시각, 문자열)

ex) DATE_FORMAT(now(), '%Y년 %m월 %d일') → 2022년 08월 08일

-----

DAYOFWEEK(날짜시각)	: 요일(일요일1,토요일7)
WEEKDAY(날짜시각)	: 요일(월요일0, 일요일6)

DATE(날짜시각)		: 날짜/시각중 날짜만 %Y-%m-d 형식으로 반환
YEAR(날짜시각)		: 년
MONTH(날짜시각)		: 월
DAY(날짜시각)			: 일
DAYOFYEAR(날짜시각)	: 1월 1일부터의 해당날짜까지의 일수를 반환

TIME(날짜시각)		: 날짜/시각중 시각만 %H:%i:%S 형식으로 반환
HOUR(날짜시각)		: 시 (0~24)
MINUTE(날짜시각)		: 분
SECOND(날짜시각)		: 초

WEEK(날짜시각,type) : 1월 1일부터 해당날까지의 주수를 반환.
주의 시작을 일요일부터 할경우는 두번째 인자를 0, 월요일부터 시작할 경우는 1 을 넣는다. 결과값은 1 에서 52 이다.

-----

날짜/시각 더하기/빼기

날짜/시각 더하기 - DATE_ADD / ADDDATE
날짜/시각 빼기 -  DATE_SUB / SUBDATE
(시각만 계산하는 함수도 있긴한데 날짜함수로도 커버가능)

DATE_ADD/DATE_SUB(날짜,차이)
차이 인수는 INTERVAL 년/월/일/시/분/초/마이크로초

ex) now() → 2018-04-05 11:10:53 라고 할때,

년
date_add(now(),INTERVAL 1 YEAR)
결과 > 2019-05-05 11:10:53

월
date_add(now(),INTERVAL 1 MONTH)
결과 > 2018-05-05 11:10:53

일
date_add(now(),INTERVAL 1 DAY)
결과 > 2018-04-06 11:10:53

시
date_add(now(),INTERVAL 1 HOUR)
결과 > 2018-04-05 12:10:53

분
date_add(now(),INTERVAL 1 MINUTE)
결과 > 2018-04-05 12:11:53

초
date_add(now(),INTERVAL 1 SECOND)
결과 > 2018-04-05 12:11:54

빼기도 DATE_SUB / SUBDATE 함수로 똑같이 하거나, 더하는함수에 음수를 넣으면 됨

-----

시각만 더하기/빼기 - ADDTIME() / SUBTIME()
함수(날짜시각, 시간)

시
ADDTIME('2020-01-01 21:20:00', '1:0:0') → 2020-01-01 22:20:00
SUBTIME('2020-01-01 21:20:00', '1:0:0') → 2020-01-01 20:20:00

분
SUBTIME('2020-01-01 21:20:00', '0:1') → 2020-01-01 21:19:00

초
SUBTIME('2020-01-01 21:20:00', '1') → 2020-01-01 21:19:59

-----

날짜/시각 차이

날짜 차이 - DATEDIFF (일수 반환)
시각 차이 - TIMEDIFF (시각(%T) 반환)

함수(큰(미래) 날짜시각, 작은(과거) 날짜시각)

ex) DATEDIFF('2020-03-01 21:20:00', '2020-01-01 22:20:00') → 60
ex) TIMEDIFF('2020-01-01 23:20:00', '2020-01-01 22:20:00') → 01:00:00 (★날짜를 넣을경우 날짜도 동일해야함)
ex) TIMEDIFF('23:20:00', '22:20:00') → 01:00:00

★종료일 - 시작일은 날짜연산이아닌 숫자연산이 돼버려서 반드시 DATEDIFF 함수로 해야함
STR_TO_DATE('2022-10-18','%Y-%m-%d') - STR_TO_DATE('2022-09-28','%Y-%m-%d') 하면 100이 나옴 (20221018 - 20220918)

-----

날짜별, 시간별 통계/검색 구할때 주의사항

1일부터 2일까지라고 한다면

1일~2일 이렇게 하면
1일 00:00:00 ~ 2일 00:00:00 이렇게 되서 2일의 값은 빠진다.

해결 방법은
① 끝나는 날짜에 1일을 더해 1일~3일 이렇게 하거나,
② 끝나는 날짜의 시간을 23:59:59 이렇게 설정해야함


그런데 시간은, 기본이 59분 59초까지다 무슨말이냐면

1시부터 2시까지 라고 한다면
01:00:00~02:00:00 이게 아닌
01:00:00~02:59:59 이렇게 됨

1시~2시59분59초까지를 구하려면 HOUR함수를 써도 상관없지만

1시 0분 0초 부터 2시 0분 0초 까지를 구하려면 HOUR만 가져오면 안되고, 분이랑 초도 같이가져와야함 (DATE_FORMAT 과 %T 이용)
DATE_FORMAT을 이용하면 BETWEEN 00:00:00 AND 02:00:00 이렇게 해도 되고 BETWEEN 00 AND 02 이렇게 해도 됨 (HOUR는 59:59까지 계산됨)

ex) 1시부터 2시까지
HOUR(STR_TO_DATE('20220807@02:00:01', '%Y%m%d@%H:%i:%S')) BETWEEN '00' AND '02'
결과 : 1 (00:00:00 ~ 02:59:59)

DATE_FORMAT(STR_TO_DATE('20220807@02:00:01', '%Y%m%d@%H:%i:%S'), '%T') BETWEEN '00' AND '02'
결과 : 0 (00:00:00 ~ 02:00:00)

-----

시스템 정보 함수

★USER / SESSION_USER - 현재 사용자를 '사용자명@공인IP' 형식으로 반환
ex) USER() → front@106.251.247.138
ex) CURRENT_USER → front@%

★SCHEMA / DATABASE - 현재 접속중인 DATABASE 정보
ex) SCHEMA() → KTO

★FOUND_ROW) - 최근에 실행했던 쿼리의 행의 개수라는데 계속 1만 나오고 안되는듯

★ROW_COUNT - 최근에 실행했던 INSERT, UPDATE, DELETE문에서 실행했던 행의 개수를 구합니다. SELECT문은 -1을 반환. 이라고 써있는데 안되는듯

★VERSION - mysql 버전을 구함
ex) SELECT VERSION() → 10.4.13-MariaDB-1:10.4.13+maria~focal-log


★ SLEEP - 다음 쿼리 실행을 하기 전 잠시 멈춤
SLEEP(초)

ex)
SELECT * FROM STAFF;
SELECT SLEEP(5);
SELECT * FROM TGPR_LOG;

----------------------------------------------------------------------------------------------------

상위 n개만 출력 - LIMIT (오라클의 rownum과 비슷)

LIMIT 10 - 상위 10개 출력
LIMIT 0,10 - 0번지부터 상위 10개 출력

아래처럼 써도 됨
LIMIT(0,10)
LIMIT 10 OFFSET 0

LIMIT, OFFSET에는 수식을 못쓴다(계산을 미리 해서 계산된값을 파라미터로 받아야됨)

LIMIT #{pageNum} - 1, #{amount}
이게 안되고

LIMIT #{calc}, #{amount}
이렇게 계산해서와야됨

----------------------------------------------------------------------------------------------------

다중행을 하나의 행으로 만드는 함수 - group_concat (오라클의 LISTAGG)

SEPARATOR '구분자'
구분자 넣는 방법. 안쓰면 쉼표(,) 가 들어감

SELECT
	CM.COT_ID,
	group_concat(t.TAG_NAME SEPARATOR ',') AS TAG_LIST
FROM CONTENT_MASTER CM
WHERE절
GROUP BY CM.COT_ID
LIMIT #{offset} , #{amount};


↓↓↓중복 제거시 DISTINCT 추가↓↓↓
SELECT
	CM.COT_ID,
	group_concat(DISTINCT t.TAG_NAME SEPARATOR ',') AS TAG_LIST
FROM CONTENT_MASTER CM
WHERE절
GROUP BY CM.COT_ID
LIMIT #{offset} , #{amount};


↓↓↓정렬하고싶을시 ORDER BY 추가↓↓↓
SELECT
	CM.COT_ID,
	group_concat(DISTINCT t.TAG_NAME ORDER BY TAG_NAME SEPARATOR ',') AS TAG_LIST
FROM CONTENT_MASTER CM
WHERE절
GROUP BY CM.COT_ID
LIMIT #{offset} , #{amount};


ex) 스칼라서브쿼리에서쓴경우
SELECT
.
(select group_concat(TAG_NAME order by F.TAG_NAME SEPARATOR '|')
from CONTENT_TAGS E, TAGS F
where 1=1
and E.TAG_ID = F.TAG_ID
and E.COT_ID = C.COT_ID
group by E.COT_ID) as tagName,
.
FROM~
WHERE~

----------------------------------------------------------------------------------------------------

alter 문

컬럼 추가 : ALTER TABLE [테이블명] ADD [컬럼명] [타입] [옵션];
컬럼 삭제 : ALTER TABLE [테이블명] DROP COLUMN [컬럼명];

컬럼명 변경 및 자료형 변경 : ALTER TABLE [테이블명] CHANGE [컬럼명] [변경할컬럼명] VARCHAR(12);
컬럼 자료형 변경 : ALTER TABLE [테이블명] MODIFY [컬럼명] VARCHAR(14);
테이블명 수정 : ALTER TABLE [테이블명] RENAME [변경할테이블명];

----------------------------------------------------------------------------------------------------

디비버에서 커넥션을 만드는 방법(사용자가 아님. 그냥 겉으로 보여지는껍데기인듯 속은 똑같은듯)
참고로 커넥션(제일 상위에 있는 그룹)은 그냥 DB라고 생각하면됨

1. 먼저 기본적으로 만들어지는 커넥션에서 User와 Database를 만들기
2, Create → Connection → MariaDB or MySQL → 다음

Server Host : localhost
Database : 기본커넥션에서 만든 DB아이디
Username : 기본커넥션에서 만든 User아이디
Password : 기본커넥션에서 만든 User비밀번호

3. 완료

----------------------------------------------------------------------------------------------------

ex) 자동 조회수 증가 ( 이때는 VALUES() 로 조회수 컬럼을 감싸지 않아야 한다 )
INSERT INTO TWEEK2022_EVENT_LOG(
	STATS_DIV_YMD,
	COOKIE_VAL,
	DIVICE_DIV_CD,
	SNS_ID,
	INQ_NUM
) VALUES(
	'20220504',
	'GA1.1.229326223.1643169086',
	'P',
	'aa35c184-3478-43f6-bb60-042ad47c2159',
	0
)
ON DUPLICATE KEY UPDATE
	INQ_NUM = INQ_NUM+1;


컬럼 기본값을 1로 정의하면 아래처럼 쓸 수 있음 (0이아닌 1로 기본값을 설정한 이유는 처음 insert할때는 +1이 안되므로)
↓↓↓
INSERT INTO TWEEK2022_EVENT_LOG(
	STATS_DIV_YMD,
	COOKIE_VAL,
	DIVICE_DIV_CD,
	SNS_ID
) VALUES(
	'20220504',
	'GA1.1.229326223.1643169086',
	'P',
	'aa35c184-3478-43f6-bb60-042ad47c2159'
)
ON DUPLICATE KEY UPDATE
	INQ_NUM = INQ_NUM+1;


아래처럼 굳이 컬럼명 넣고싶으면 넣어줘도 됨
,
,
INQ_NUM
) VALUES(
,
,
INQ_NUM
)

----------------------------------------------------------------------------------------------------

디비버 실행하려고 ctrl + enter 눌렀는데 줄마다 화살표 안뜨면 원하는 코드만 실행 안된거

이전 쿼리에서 끝낼때 ; 안붙였는지 확인

----------------------------------------------------------------------------------------------------

디비버 컬럼 순서 변경

컬럼 페이지 들어간 후
오른쪽 아래 위아래 화살표 있음

sql로도 할 수 도 있음
ALTER TABLE '테이블 이름' MODIFY COLUMN '컬럼 이름' '자료형' AFTER '앞에 올 컬럼 이름';
ex) ALTER TABLE user MODIFY COLUMN email varchar(20) AFTER phone;

----------------------------------------------------------------------------------------------------

한쪽 테이블에는 있고 다른 한쪽에는 없는 행 찾기 (NOT IN 이용) (#일치#불일치#포함#관계)

SELECT
	*
FROM 큰집합
WHERE 외래키 NOT IN(
	SELECT 외래키 FROM 작은집합 WHERE 외래키 IS NOT NULL
);

작은집합쪽에 NULL데이터가 한개라도 포함돼 있을경우는
WHERE 외래키 IS NOT NULL을 붙여야함

-----

한쪽 테이블에 포함되는걸 찾으려면 IN 쓰면 됨

SELECT
	*
FROM IMAGE
WHERE COT_ID IN(
	SELECT GDS_ID FROM TGPR_MASTER tm 
);

-----

조건추가 하고싶은 경우는 AND붙여서 추가하면됨

SELECT
	*
FROM EVENT_ATTEMPT
WHERE EVD_ID NOT IN(
	SELECT EVD_ID FROM TWEEK2022_EVENT_ATTEMPT
) AND EVNT_ID = "d1761a55-ed6a-4680-a0ba-3fc42c4bc6fe";

-----

OUTER JOIN을 이용한 방법

SELECT * FROM 테이블1 T1
LEFT JOIN 테이블2 T2
USING(외래키)
WHERE T2.외래키 IS NULL

----------------------------------------------------------------------------------------------------

디비버에서 결과 컬럼/값 json으로 편하게 보기 (두개 이상의 행을 비교할떄 좋음)

왼쪽에 행번호(1,2,3..)에 우클릭 하고 Advanced Copy → Copy as JSON 클릭 후 원하는곳(에디터 or JSON Parser)에 붙여넣고 보기

{
"CONTENT_MASTER": [
	{
		"COT_ID" : "7955b54f-1eda-4408-bb70-0a23aec215c2",
		"CONTENT_ID" : "133650",
		"CONTENT_TYPE" : 39,
		"CONTENT_STATUS" : 2,
		"TITLE" : "원조강변할매재첩회식당",
		"DISPLAY_TITLE" : "원조강변할매재첩회식당",
		"READ_COUNT" : 24664,
		"SHOW_FLAG" : 1,
		"CREATE_USR_ID" : "4e512b8a-60ad-11e8-8cca-00232456a22f",
		"CREATE_DATE" : "2003-04-07T15:00:00.000Z",
		"MODIFIED_DATE" : "2022-06-14T01:29:04.000Z",
		"DEPT" : "국내 온라인 홍보팀",
		"DEPT_VIEW" : "국내 온라인 홍보팀",
		"TEL" : "033-738-3588",
		"CONTENT_TYPE_OLD" : 39,
		"FINAL_MODIFIED_DATE" : "2022-06-14T01:29:04.000Z",
		"AUTH_CODE" : "",
		"CONTENT_DIV" : 0,
		"MAP_EPRSS_YN" : "Y",
		"EXCP_DIV_CD" : 1
	}
]}

----------------------------------------------------------------------------------------------------

예약어를 컬럼명/테이블명으로 사용하려면 백틱(``)로 묶으면 된다 (oracle은 ""로 묶어야함)
SELECT “DATE”, UPDATE_DT FROM “YEAR”

----------------------------------------------------------------------------------------------------

식별관계 & 비식별관계


식별관계 : 외래키를 기본키로 이용, 실선으로 표시

비식별관계 : 외래키를 일반속성으로 이용, 점선으로 표시
	부모테이블의 참조행이 없어도 자식테이블의 행을 추가할 수 있음

----------------------------------------------------------------------------------------------------

서브쿼리

메인쿼리 - 하나의 select(insert, update, delete)로만 구성된 쿼리
서브쿼리 - 메인쿼리에서 1개이상의 select를 추가한 쿼리
  - 삽입 위치 : select절, from절, where절, order by절
  - 가져온 데이터만 꺼내 사용할수있다(select할수있다)

SELECT절 서브쿼리(스칼라 서브쿼리) : 이 서브쿼리는 반드시 단일행을 리턴해야함, 집계함수(sum,count,min,max)가 많이 쓰임
FROM절 서브쿼리(인라인 뷰) : 뷰처럼 결과가 동적으로 생성된 테이블 형태로 사용할 수 있음
WHERE절 서브쿼리(중첩 서브쿼리 or 서브쿼리)

----------------------------------------------------------------------------------------------------

(ANY == SOME) / ALL 연산자

where절에 서브쿼리 쓸때 여러행과 비교시 씀 (서브쿼리의 결과행이 여러행인경우)

ex)
SELECT * FROM [테이블1] WHERE [컬럼x] > ANY (SELECT [컬럼x과 비교할컬럼] FROM 테이블2 WHERE [컬럼y] in("값1","값2","값3"))

이렇게 있다고 할때 WHERE절안에서 [컬럼x] 와 비교할 레코드들을 서브쿼리로 가져오고, 비교연산자 ( '>', '>=', '=', '<=', '<' ) 로 비교시
ANY는 컬럼x에있는 레코드들중에서 서브쿼리로 가져온 값들과 조건을 비교했을때 한개라도 만족시 그 레코드를 가져오고,
ALL은 컬럼x에있는 레코드들중에서 서브쿼리로 가져온 값들과 조건을 비교했을때 모두 만족시 그 레코드를 가져옴

즉, ANY는 OR연산자와 같고, ALL은 AND연산자와 같음.
= ANY (서브쿼리) 는
IN (서브쿼리) 과 똑같음 (비교값들중 하나라도 일치할경우 TRUE)

-----

숫자형 자료 비교시


10, 12, 20이 서브쿼리의 결과레코드들로 나왔다고 할때

컬럼1 > ANY 결과행값들(10, 12, 20)
이건 컬럼1 > 10 || 컬럼1 > 12 || 컬럼1 > 20 과 같으며

결국 컬럼1 > 10과 같고 (이 경우 MIN이 됨. 등호가 반대면 MAX)


컬럼1 > ALL 결과행값들(10, 12, 20)
이건 컬럼1 > 10 && 컬럼1 > 12 && 컬럼1 > 20 과 같으며

결국 컬럼1 > 20과 같음 (이 경우 MAX가 됨. 등호가 반대면 MIN)


ANY는 이상, 초과 ( >=, > ) 로 비교시 MIN()로 서브쿼리결과행값들을 감싼것과 같고
	이하, 미만 ( <=, < ) 일 경우 MAX()로 서브쿼리결과행값들을 감싼것과 같음

ALL은 이상, 초과 ( >=, > ) 로 비교시 MAX()로 서브쿼리결과행값들을 감싼것과 같고
	이하, 미만 ( <=, < ) 일 경우 MIN()로 서브쿼리결과행값들을 감싼것과 같음

-----

문자형 자료 비교시


임채원 = 임채원 || 임채원 == 김민정
임채원①		임채원	②
			김민정	③
			.
			.
①이 ②, ③.. n개중에 하나라도 일치하면 됨
↓↓↓
임채원 IN ("임채원","김민정")


반면 ALL은 하나의 행이 두개의 행과 일치해야하기때문에 서브쿼리가 같은값들만 반환할때만 TRUE가 나옴
임채원 == 임채원 && 임채원 == 김민정 ALL
임채원①		임채원	②
			김민정	③
			.
			.
①이 ②, ③.. n개모두 일치해야함 (서브쿼리의 결과행값들이 모두 똑같을때만 TRUE)

이럴때만 TRUE ↓↓↓

임채원①		임채원	②
			임채원	③

----------------------------------------------------------------------------------------------------

검색된 여러 행중 단일행만 반환하려면 ORDER BY 랑 LIMIT 1 같이 쓰면 됨

----------------------------------------------------------------------------------------------------

테이블 JOIN 시 ON / USING 차이

SELECT
	*
FROM 테이블1
LEFT JOIN
	테이블2
ON 테이블1.컬럼 = 테이블2.컬럼

컬럼명이 같을 경우 위처럼 ON을 쓰는 대신 USING을 쓸 수 있음

SELECT
	*
FROM 테이블1
LEFT JOIN
	테이블2
USING(컬럼)

----------------------------------------------------------------------------------------------------

쿼리가 잘 일치하는지 검증할때
json으로 복사한다음

보면서 하면 편함

----------------------------------------------------------------------------------------------------

CROSS JOIN (카티션 곱)

A테이블과 B테이블이 있다고 할때
A테이블의 행 하나당 B테이블의 모든행을 하나씩 조인함

행 개수는 A행*B행 이 되고
열 개수는 A열+B열 이 됨

SELECT COUNT(*) FROM A CROSS JOIN B
or
SELECT COUNT(*) FROM A,B

----------------------------------------------------------------------------------------------------

셀프조인


곤충		|	천적		|	수명
거미		|	참새		|	1년
메뚜기	|	거미		|	6개월
 ...	 	 
 
곤충 도감 테이블이 있다고 가정합시다. 이 테이블에서 '메뚜기'의 천적 곤충의 이름, 천적, 수명을 검색하려면 어떻게 해야 할까요?


방법1. 서브쿼리
SELECT 이름, 천적, 수명
FROM 곤충테이블
WHERE 이름 = ( SELECT 천적
               FROM 곤충테이블
               WHERE 곤충 = '메뚜기');


방법2. 셀프조인
SELECT B.곤충, B.천적, B.수명
FROM 곤충도감 A
    INNER JOIN 곤충도감 B
    ON A.천적 = B.곤충
WHERE A.곤충 = '메뚜기';

----------------------------------------------------------------------------------------------------

실행계획

EXPLAIN 키워드 앞에 붙이기

2행이 나와야함 (서브쿼리 대신 조인쿼리 쓰면 되는듯?)

반환시간이 10초가 넘으면 망한쿼리?

----------------------------------------------------------------------------------------------------

IF랑 SUM으로 깔끔한 코드작성

SELECT
	(SELECT COUNT(*) FROM ZIKIMI WHERE STATUS = 2 AND SNS_ID=#{snsId}) AS approval,
	(SELECT COUNT(*) FROM ZIKIMI WHERE STATUS != 2 AND SNS_ID=#{snsId}) AS noApproval
FROM DUAL

↓↓↓

SELECT
	SUM(IF(STATUS = 2, 1, 0)) AS approval,
	SUM(IF(STATUS != 2, 1, 0)) AS noApproval
FROM ZIKIMI WHERE SNS_ID = #{snsId}

----------------------------------------------------------------------------------------------------

사용자 정의 정렬

ORDER BY
	CASE WHEN title = 'aa' THEN 1
	WHEN title = 'bb' THEN 2 END

ex)
SELECT
	*
FROM DETAIL_INFO 
ORDER BY
	CASE WHEN title like '%소개' THEN 2
	WHEN title like '%내용' THEN 1 END DESC

----------------------------------------------------------------------------------------------------

db별 용량 확인

SELECT table_schema "Database", ROUND(SUM(data_length+index_length)/1024/1024,1) "MB" FROM information_schema.TABLES GROUP BY 1;

----------------------------------------------------------------------------------------------------

db 백업

mysqldump -u [사용자 계정] -p [패스워드] [원본 데이터베이스명] > [생성할 백업 DB명].sql

ex)
mysqldump -u test_user -p test_db > backup_test_db.sql
passowrd : 123456

-----

db 복원

mysql -u [사용자 계정] -p [패스워드] [복원할 DB] < [백업된 DB].sql

ex)
mysql -u test_user -p test_db < backup_test_db.sql
passowrd : 123456

------------------------------

테이블 백업

mysqldump -u [사용자 계정] -p [패스워드] [데이터베이스명] [원본 백업받을 테이블명] > [백업받을 테이블명].sql

ex)
mysqldump -u test_user -p test_db test_table > backup_test_table.sql
passowrd : 123456

-----

테이블 복원

mysql -u [사용자 계정] -p [패스워드] [복원할 DB ] < [백업된 테이블].sql

ex)
mysql -u test_user -p 123456 test_db < backup_test_table.sql
passowrd : 123456

------------------------------

모든 db백업

mysqldump --all-databases -u [사용자 계정] -p --default-character-set=euckr < [백업된 DB].sql

ex)
mysqldump --all-databases -uroot -p --default-character-set=euckr > all.sql

-----

모든 db복원

mysql --all-databases -u [사용자 계정] -p < [백업된 DB].sql

ex)
mysql -uroot -p < all.sql

----------------------------------------------------------------------------------------------------

트리거

테이블에 INSERT or UPDATE or DELETE가 발생했을때를 감지후 실행


★트리거 목록 (Statement컬럼에 내용도 있음. Created컬럼은 생성일이자 수정일임)
SHOW TRIGGERS

★트리거 삭제
DROP TRIGGER CHK_UPDATE_DETAIL_INFO

★트리거 만들기

-- 원래 mysql은 ';'를 만나면 입력을 종료한다. Trigger을 설정하는 중에 종료하지 않을 예정임에도 불구하고 중간에 ';'을 써야하는 상황이 온다. 
그때 입력의 종료를 방지하기 위해서 //를 원래 ; 같은 종료 용도로 바꾸겠다는 의미이다.
DELIMITER $$
CREATE TRIGGER update_item
#CREATE OR REPLACE update_item -- 같은 이름의 트리거가 있을 경우 덮어씀 (원래는 오류메시지가 남)
	AFTER UPDATE  -- {BEFORE | AFTER} {INSERT | UPDATE| DELETE } 중 언제 어떤 작업을 할지 정한다
	ON sale_table -- 트리거를 부착할 테이블
	FOR EACH ROW -- 아래 나올 조건에 해당하는 모든 row에 적용한다는 뜻
BEGIN
-- 트리거시 실행되는 코드
	-- 변수 선언&초기화
	DECLARE oldTag CHAR DEFAULT NULL;

	-- 변수 대입
	SET oldTag = (SELECT COUNT(*) FROM DETAIL_INFO WHERE FLD_GUBUN=10 AND COT_ID='a5b789d2-3d56-43d2-9e2b-c2cb2ea18bb2');

	-- 변수 대입 다른 방법
	select sex, birth INTO SEX1, BIRTH1 from member where ID = NEW.member;

	IF NEW.discount_rate != OLD.discount_rate THEN -- update 트리거는 old와 new 값이 존재함
		UPDATE item_table SET discount_rate = NEW.discount_rate WHERE discount_rate = OLD.discount_rate;
	END IF;
END
-- 구분자를 $$ 에서 ':' 로 다시 변경함
DELIMITER ;

ex)
CREATE TRIGGER CONTENT_TAGS_FROM_DETAIL_INFO_INSERT BEFORE INSERT ON DETAIL_INFO FOR EACH ROW
BEGIN
    IF (SELECT COUNT(*) FROM DETAIL_INFO WHERE FLD_GUBUN = 10 AND COT_ID = NEW.COT_ID AND CONTENT_BODY <> '' AND CONTENT_BODY <> '<p><br></p>') = 0
        AND NEW.FLD_GUBUN = 10 AND NEW.CONTENT_BODY <> '' AND NEW.CONTENT_BODY <> '<p><br></p>' THEN
        INSERT INTO CONTENT_TAGS(TAG_ID, COT_ID) VALUES((SELECT TAG_ID FROM TAGS WHERE TAG_NAME REGEXP '반려동물동반여행지'), NEW.COT_ID);
    END IF;
END;

ex2)
CREATE OR REPLACE TRIGGER UPDATE_LOTTERY_CHANCE AFTER UPDATE ON TRSS_PZWNR
    FOR EACH ROW
BEGIN
    DECLARE tgmId CHAR(36);
    DECLARE cnt INT;

    SELECT TGM_ID INTO tgmId
    FROM TRSS_GOODS_DTLE
    WHERE TGD_ID = NEW.TGD_ID;

    SELECT COUNT(*) INTO cnt
    FROM TRSS_PZWNR P
             JOIN TRSS_GOODS_DTLE D USING(TGD_ID)
    WHERE D.TGM_ID = tgmId
      AND DATE(P.GIVE_DT) = CURDATE();

    UPDATE TRSS_LOTTERY_CHANCE C
    SET DDLN_YN = 1
    WHERE C.TGM_ID = tgmId
        AND LT_APLCN_YMD = CURDATE()
        AND C.LMMT_CNT < cnt;
END;


★mysql에서는 다중트리거(하나의 테이블에 동일한 트리거 여러개 부착) 지원이 안됨. 각각 따로 만들어야함

★영향을 받은 행 데이터와, 기존의 다른 테이블을 비교
DECLARE CID VARCHAR DEFAULT '';
    SET CID = COT_ID;
    IF (SELECT COUNT(*) FROM DETAIL_INFO WHERE FLD_GUBUN=10 AND COT_ID = CID) != 0 THEN


★트리거 테스트시 테스트용 테이블 하나 생성후 출력하고싶은 값을 넣으면됨
DECLARE cnt INT;
.
.
SELECT COUNT(*) INTO cnt
.
.
INSERT INTO TEST_TRSS VALUES(cnt);


★INSERT/UPDATE/DELETE 할때 DML작업 처리되기 이전의 데이터와 비교를 해야할 경우 AFTER 말고 BEFORE로 해야함
NEW.컬럼명 으로 insert될 값도 가져올 수 있음

ex) insert되는 행의 FLD_GUBUN이 10이고, insert되는 COT_ID와 일치하는 기존의 데이터중 FLD_GUBUN이 10이면서 CONTENT_BODY가 ''가 아니고
insert되는 CONTENT_BODY가 ''이 아닐때
CREATE OR REPLACE TRIGGER CONTENT_TAGS_FROM_DETAIL_INFO_INSERT BEFORE INSERT ON DETAIL_INFO FOR EACH ROW
BEGIN
    IF (SELECT COUNT(*) FROM DETAIL_INFO WHERE FLD_GUBUN = 10 AND COT_ID = NEW.COT_ID AND CONTENT_BODY <> '') = 0 AND NEW.FLD_GUBUN = 10 AND NEW.CONTENT_BODY <> '' THEN
        INSERT INTO ZZ_TMP VALUES('A');
    END IF;
END;


★트리거중인 테이블에 insert/update/delete 불가
트리거로 테이블을 감시해놓으면, 해당 테이블에 DML이 들어왔을때 교착상태 방지를 위해 잠금이 수행되고, 잠금되어있는 동안에는 다른 DML이 수행될 수 없음
트리거는 쿼리문이 완전히 실행되기 이전에 발동함. 그 증거로 바뀌기 이전의 데이터와 바뀔 데이터를 가져올 수 있는 old 필드명, new 필드명이 있음
쿼리문이 완전히 종료되는 COMMIT 또는 ROLLBAK이 일어나기 전까지, 테이블은 무결성을 위해 LOCK 상태이기때문에 동일 테이블을 트리거로 수정할 수 없음
해결방법 : 테이블을 분리하거나, 트리거를 사용하지 않고 쿼리문으로 수행해야함

★트리거에서 명시적/암시적 commit을 유발하는 행위 불가 → DDL문 사용 불가

------------------------------

INSERT / UPDATE / DELETE 문 사용시
Unknown column '컬럼명' in 'field list' 등의 오류가 뜨는데
아무리 살펴봐도 문제가 없다면

연결된 트리거의 문제일 수가 있음

----------------------------------------------------------------------------------------------------

프로시저

★프로시저 목록 조회
SHOW PROCEDURE STATUS;

★프로시저 스크립트 조회
SHOW CREATE PROCEDURE 프로시저명;

★프로시저 생성
DROP PROCEDURE IF EXISTS 프로시저명; -- 이미 프로시저가 정의 되어 있다면 삭제하는 코드
DELIMITER //
CREATE PROCEDURE procedure_name 
([ 
    [ IN | OUT ] parameter_name 
    { parameter_type | ARRAY OF parameter_type }, ... 
]) 
[ DECLARE variable_declaration;...[;] ] 
BEGIN 
    procedure_body_statement;...[;] 
END // 
DELIMITER ;

★프로시저 호출
CALL 프로시저명(매개변수들);

★ 프로시저 삭제
DROP PROCEDURE 프로시저명;

----------------------------------------------------------------------------------------------------

SELECT 쿼리 작성 순서

SELECT → FROM(JOIN) → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT


SELECT 쿼리 실행 순서

FROM(JOIN) → WHERE → SELECT → GROUP BY → HAVING → ORDER BY → LIMIT

----------------------------------------------------------------------------------------------------

GROUP BY 를 써서 그룹별 합계를 구할때

SELECT 그룹컬럼, 금액
FROM 테이블
GROUP BY 그룹컬럼

위처럼 하면 안되고 꼭 금액을 SUM()으로 묶어서 집계를 해야함
위처럼 하면 그냥 그룹컬럼의 첫번째 행(금액)이 나옴

----------------------------------------------------------------------------------------------------

GROUP BY 를 써서 그룹별 최댓값 등을 구할때,

최대값과 같이 다른 컬럼도 구하려면 일반적인 방법으로 하면 안됨


SELECT 아이디, 이름, 가격 FROM 테이블
GROUP BY 그룹컬럼
HAVING MAX(가격)
위처럼 하면 집계함수가 사용되지않은 컬럼은 첫번째행 하나만 가져와짐. HAVING은 집계결과에 대한 WHERE문이기때문에 의미없음


SELECT 아이디, 이름, MAX(가격) FROM 테이블
GROUP BY 그룹컬럼
위처럼 하면 그룹별 최대값은 정상적으로 구해지지만(CCC) 다른 컬럼(AAA,BBB)은 최대값이 아닌 첫번째 값을 참조하게됨


SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
FROM REST_INFO A
JOIN (
    SELECT FOOD_TYPE, MAX(FAVORITES) AS FAVORITES
    FROM REST_INFO
    GROUP BY FOOD_TYPE
) B
USING(FAVORITES, FOOD_TYPE)
ORDER BY FOOD_TYPE DESC
위처럼 하거나


SELECT FOOD_TYPE,REST_ID,REST_NAME, FAVORITES
FROM REST_INFO
WHERE FAVORITES IN (SELECT MAX(FAVORITES) FROM REST_INFO 
                   GROUP BY FOOD_TYPE)
GROUP BY FOOD_TYPE ORDER BY FOOD_TYPE DESC
위처럼 서브쿼리 + IN으로 하기

----------------------------------------------------------------------------------------------------

임시테이블(가상테이블)

WITH RECURSIVE 문 (mysql 5.7이하 미지원)

메모리상에 가상의 테이블을 저장
실제로 테이블을 생성하거나 데이터삽입(INSERT)를 하지 않아도 가상 테이블을 생성할 수 있음
조회후에는 자동으로 소멸됨

WITH RECURSIVE ASD AS(
    SELECT 0 AS NUM
    UNION ALL
    SELECT NUM + 1 FROM ASD WHERE NUM < 5
)
SELECT * FROM ASD


결과

NUM
0
1
2
3
4
5


쉼표(,)를 쓰면 가상테이블을 여러개 만들 수도 있음

ex) 비어있는 시간대가 있는 테이블과, 0부터 23까지 있는 가상의 1열 테이블을 합치기
WITH RECURSIVE A AS(
    SELECT 0 AS NUM
    UNION ALL
    SELECT NUM + 1 FROM A WHERE NUM < 23
), B AS(
    SELECT HOUR(DATETIME) AS HOUR, COUNT(DISTINCT ANIMAL_ID) AS CNT FROM ANIMAL_OUTS
    GROUP BY HOUR
)
SELECT *
FROM A
LEFT JOIN B
ON A.NUM = B.HOUR

NUM	HOUR	CNT
0		
1		
2		
3		7		3	
4		8		1
5		9		1
6		10		2
.
.

*를 SELECT NUM, IF(CNT IS NULL,0,CNT) 이런식으로 하면 전체시간대별 개수를 만들 수 있음

----------------------------------------------------------------------------------------------------

UNION / UNION ALL

합집합

SELECT 컬럼1, 컬럼2 FROM 테이블1
UNION
SELECT 컬럼1, 컬럼2 FROM 테이블2

컬럼의 개수가 똑같아야함

UNION은 중복을 제거한 결과를 반환하고,
UNION ALL은 모든 결과를 반환함

ORDER BY는 마지막에 사용 가능

----------------------------------------------------------------------------------------------------

쿼리 로그 확인


로그가 저장되고있는지 확인. general_log가 on으로 되어있어야함
show variables where Variable_name in ('version', 'log', 'general_log');


로그 경로 확인
show variables like 'general%';


on으로 바꾸는 코드
set global general_log = 1;

----------------------------------------------------------------------------------------------------

테이블 생성일자 조회

SELECT CREATE_TIME FROM INFORMATION_SCHEMA.TABLES WHERE table_name='테이블명';

----------------------------------------------------------------------------------------------------

BETWEEN AND

>= AND <= 와 동일


컬럼명 BETWEEN 시작 AND 종료
			| |
컬럼명 >= 시작 AND 컬럼명 <= 종료

----------------------------------------------------------------------------------------------------

MySQL은 Oracle과 다르게 자동 커밋 모드가 아닌 수동 커밋 모드로 실행됨

따라서 사용자가 각각의 SQL문에 대해 명시적으로 커밋 또는 롤백을 지정해야함


트랜잭션 시작
START TRANSACTION;

트랜잭션 완료(트랜잭션 이후 모든 동작을 적용)
COMMIT;

트랜잭션이 선언되기 전 상태로 복귀
ROLLBACK;

----------------------------------------------------------------------------------------------------

ISNULL / NULLIF / COALESCE

ISNULL(값1, 값2)
1번째 인수가 NULL이면 2번째인수를 반환

NULLIF(값1, 값2)
1번째인수가 2번째인수와 같으면 NULL을 반환

COALESCE(값1, 값2 ,…)
NULL이 아닌 첫번째 값 반환

----------------------------------------------------------------------------------------------------

중복된 데이터 찾아서 그룹화후 몇개있는지 각각 개수 구하기

SELECT 컬럼명1, 컬럼명2, 컬럼명3, COUNT(*)
FROM REPAIR_REQUEST_DEPT
GROUP BY 컬럼명1, 컬럼명2, 컬럼명3
HAVING COUNT(*) > 1;

----------------------------------------------------------------------------------------------------

윈도우 함수


OVER

1 | 1행1열값 | 1행2열값
2 | 2행1열값 | 2행2열값

위처럼 결과행들에 순번을 붙인 컬럼을 추가해주는 함수

SELECT
	ROW_NUMBER() OVER(ORDER BY ${orderingTargetColumn} ${orderingTargetAscending}) AS NO,
	컬럼1,
	컬럼2,
FROM ...
WHERE ...
ORDER BY
	${orderingTargetColumn} ${orderingTargetAscending}
LIMIT
	#{offset }, #{limit }

----------------------------------------------------------------------------------------------------

INNER JOIN

A JOIN B
USING(COT_ID)
를 하면,

A테이블에 COT_ID컬럼의 값과 B테이블의 COT_ID컬럼의 값이 일치 하는것만 가져옴

INNER JOIN을 하면 B테이블에서 A테이블의 같은 컬럼을 여러행에서 참조해도 조건을 충족하는 첫번째 행만 가져옴 (결과 행 개수가 감소됨)


OUTER JOIN

A LEFT JOIN B
USING(COT_ID)
를 하면,

B테이블의 행개수와 상관없이 무조건 A테이블의 행들이 가져와짐 → X
B테이블에서 A테이블의 어떤 컬럼을 참조하는 행이 여러행이 있으면,
A LEFT JOIN B를 했을때
A만 조회한것보다 결과가 늘어남

이럴때는 A LEFT JOIN B 대신 아래처럼 하면 됨
A LEFT JOIN (SELECT DISTINCT 외래키컬럼 FROM B) [별칭] [ON 테이블.컬럼=테이블.컬럼 or USING(컬럼)]

다른 컬럼도 필요하면 , 붙여서 쓰고, DISTINCT 대신 LIMIT 1을 쓰기
LEFT JOIN (
	SELECT TNM_ID, NSLTR_TTL
	FROM TRSS_NSLTR_DTLE
	LIMIT 1
) 별칭 USING(TNM_ID)

----------------------------------------------------------------------------------------------------

특정컬럼이 중복됐으면 특정컬럼을 기준으로 상위1개만 나오게하기

ex) TP_ID가 똑같으면 REG_DT를 내림차순정렬후 상위1개씩만 출력
SELECT t1.TP_ID, t1.TRS_MN_CD, t1.WYBL_NO
FROM TRSS_TRS_HST t1
    LEFT JOIN TRSS_TRS_HST t2 ON t1.TP_ID = t2.TP_ID AND t1.REG_DT < t2.REG_DT
WHERE t2.TP_ID IS NULL
ORDER BY TP_ID

----------------------------------------------------------------------------------------------------

변수 선언 / 사용

SELECT
.
.
 FROM
	(SELECT @tnmId:=#{tnmId }) M
	(SELECT @pblcnYm:=PBLCN_YM FROM TRSS_NSLTR_MASTER WHERE TNM_ID = #{tnmId}) D
WHERE
	AND YEAR(U.SSRP_BGNG_DT) = LEFT(@pblcnYm, 4)
	AND MONTH(U.SSRP_BGNG_DT) = MID(@pblcnYm, 5)

----------------------------------------------------------------------------------------------------

사용자 정의 함수

------------------------------

함수 목록 조회
SHOW FUNCTION STATUS

함수 내용 조회
SHOW CREATE FUNCTION 함수명

------------------------------

생성
CREATE FUNCTION '함수명' (
파라미터
) RETURNS 반환할 데이터타입
BEGIN
	수행할 쿼리
	RETURN 반환할 값
END


ex)
CREATE FUNCTION `GET_NAME`(
    NAME VARCHAR(20)
    , AGE INTEGER -- 파라미터 선언
) RETURNS varchar(20) -- 반환할 데이터타입
BEGIN
    DECLARE AGE_TITLE VARCHAR(20);
    DECLARE NAME_TITLE VARCHAR(20);
    DECLARE RETURN_VALUE VARCHAR(20); -- 변수 선언
    
    SELECT CONCAT(NAME, ' IS ') 
      INTO NAME_TITLE; -- 조회한 컬럼은 INTO로 변수에 넣어야 함
    
    IF(AGE > 30) THEN
    	SET AGE_TITLE = 'OLD'; -- 값 할당
    ELSE
    	SET AGE_TITLE = 'YOUNG';
    END IF;
    
    SET RETURN_VALUE = CONCAT(NAME_TITLE, AGE_TITLE);

    RETURN RETURN_VALUE;
END

----------------------------------------------------------------------------------------------------

특정 컬럼을 이용한 중복된 행을 1개로 계산한 행개수


중복유지

SELECT COUNT(*) FROM (
    SELECT 1
    FROM TRSS_PZWNR
    WHERE TNM_ID='7f2b4956-c7e0-43a6-8338-9ec24d9ae1e2' AND PTCT_DT BETWEEN '2023-07-05 14:30' AND '2023-07-05 14:42'
    GROUP BY SSRP_ID
) A;

↓↓↓

중복제거 (SSRP_ID 컬럼 기준)

SELECT COUNT(*) FROM (
     SELECT DISTINCT SSRP_ID
     FROM TRSS_PZWNR
     WHERE TNM_ID='7f2b4956-c7e0-43a6-8338-9ec24d9ae1e2' AND PTCT_DT BETWEEN '2023-07-05 14:30' AND '2023-07-05 14:42'
     GROUP BY SSRP_ID
 ) A;

----------------------------------------------------------------------------------------------------

SELECT 결과 레코드에 순차컬럼 추가 (1,2,3,4,5...)

ROW_NUMBER() OVER (ORDER BY CNT DESC, U.CREATE_DATE DESC) AS RANKING

----------------------------------------------------------------------------------------------------

랜덤 UUID

UUID()

----------------------------------------------------------------------------------------------------

자바에서 자동 커밋모드 설정시

현재 자동커밋모드인지 확인
sqlSession.getConnection().getAutoCommit()

자동커밋모드 해제
sqlSession.getConnection().setAutoCommit(false);

자동커밋모드 해제
sqlSession.getConnection().setAutoCommit(true);

-----

자동커밋모드는 다음중 하나를 하면 자동으로 다시 설정된다고 함
Commit 호출 : connection.commit()
Rollback 호출 : connection.rollback();
연결 닫기 : connection.close();
Exception : 현재 트랜잭션 수행 중 예외가 발생하면 응용프로그램 구성에 따라 연결이 풀로 반환되거나 닫힘

----------------------------------------------------------------------------------------------------

cascade는 외래키가 있는 자식테이블에서

cascade설정을 하면, 부모 테이블의 레코드가 지워질때 자식테이블이 같이 지워지는것임

----------------------------------------------------------------------------------------------------

스케줄러

------------------------------

스케줄러 목록 조회

SHOW EVENTS

------------------------------

특정 스케줄러 조회

SHOW CREATE EVENT CHK_STAFF_PERIOD;

------------------------------

추가

CREATE OR REPLACE EVENT 스케줄러명
ON SCHEDULE EVERY [주기 숫자] [주기 날짜/시간타입]
DO
[DML문]

ex) 1일마다 체크해서 특정 날짜를 벗어난경우 값 변경
CREATE OR REPLACE EVENT CHK_STAFF_PERIOD
ON SCHEDULE EVERY 1 DAY
DO
UPDATE STAFF
SET CHK_USE = 0
WHERE NOT CURDATE() BETWEEN USE_BGNG_YMD AND USE_END_YMD;

------------------------------

삭제

DROP EVENT 스케줄러명

----------------------------------------------------------------------------------------------------

테이블 복사 (테이블정의 및 레코드들까지 통째로 복사됨)

CREATE TABLE DATABASE_SEASON_TEST AS
SELECT * FROM DATABASE_SEASON;

----------------------------------------------------------------------------------------------------















