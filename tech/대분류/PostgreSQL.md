[42830] ERROR: there is no unique constraint matching given keys for referenced table "vt_code_detail"

1. 부모키가 복합키일때 발생. 복합키를 참조하고싶을 경우 참조컬럼도 부모컬럼과 개수를 똑같이 맞춰서 아래처럼 묶어서 외래키로 설정해야함

ex1)
    FOREIGN KEY (dept_id, company_id) REFERENCES department (dept_id, company_id)

ex2)
alter table vt_agent_custom_log
    add constraint "vt_agent_custom_log_vt_code_detail_group_code"
        foreign key (group_code, state) references vt_code_detail (group_code, code);

2. 외래키 등록할 컬럼과 부모테이블의 데이터타입이 일치하는지 확인
3. 레코드가 연결할 부모테이블의 해당 컬럼의 레코드값들중 하나랑 일치하는지 확인 (대소문자가 달라도 안됨)
4. 외래 키 제약 조건을 추가할 때 고유한 제약 조건 이름을 지어야함

----------------------------------------------------------------------------------------------------

로컬 설치
https://www.postgresql.org/ 에서 원하는 버전 설치
$ brew install postgresql@15

실행
brew services start postgresql

Error: No available formula with the name "homebrew/core/postgresql".
Please tap it and then try again: brew tap homebrew/core
실행시 이런 오류 나면 아래 명령어 입력 후 재실행

brew tap homebrew/core


종료
brew services stop postgresql

접속
psql postgres

사용자 조회
\du

db생성
create database testdb;

db조회
\l
or
\list

db상세조회
\list+

----------------------------------------------------------------------------------------------------

mybatis xml파일에서 빨간줄 오류가 날때

',', FOR, INTO, LIMIT, LOCK, NULLS 또는 PROCEDURE이(가) 필요하지만 'OFFSET'을(를) 얻었습니다
이런식로 뜨는데,

select태그 맨 위나 맨 밑에 빈 if태그 하나 넣어주면됨

	.
	.
	<if test="1"/>
</select>

그럼 빨간줄이 사라지고 실행시 오류도 안남

----------------------------------------------------------------------------------------------------

13자리 타임스탬프를 날짜/시각으로 변환

to_timestamp(1912995045)

----------------------------------------------------------------------------------------------------

없으면 insert, 있으면 update

<insert id="updateUser" parameterType="com.okestro.vista.portal.model.user.UserDTO">
	insert into vt_user(user_name, email, phone_number, slack_id, act_start, act_end, channel_type, reg_dt)
	values (#{userName}, #{email}, #{phoneNumber}, #{slackId}, to_timestamp(#{actStart}), to_timestamp(#{actEnd}), #{channelType}, now())
	on conflict (id) do update
	set
		user_name = coalesce(#{userName}, vt_user.user_name),
		email = coalesce(#{email}, vt_user.email),
		phone_number = coalesce(#{phoneNumber}, vt_user.phone_number),
		mod_dt = now();
</insert>

----------------------------------------------------------------------------------------------------

select
	u.*,
	case when eru.user_id is not null then true else false end as receive_notifications
from vt_user u
left join vt_event_rule_user eru on u.id = eru.user_id

u테이블의 행과 연결된 eru테이블의 행이 있을때 true, 없을때 false

----------------------------------------------------------------------------------------------------

시퀀스

bigserial 등으로 컬럼을 만들었을때, 시퀀스의 기본이름은 테이블명_컬럼명_seq

현재값 조회
SELECT last_value FROM vt_metric_id_seq;

값 설정
SELECT setval('vt_metric_id_seq', 100);


참고로 시퀀스의 현재값은 마지막으로 insert가 된 숫자임. 시퀀스값이 현재 123이면 123을 마지막에 insert했다는 뜻

다음 insert할때 124로 바뀌면서 124가 저장됨

----------------------------------------------------------------------------------------------------




















