Uniform Resource Identifier(통합 자원 식별자)

URI 안에 [[URL]]과 [[URN]]이 있음

Uniform: [[리소스]] 식별하는 통일된 방식
Resource: 자원, URL로 식별할 수 있는 모든 것(제한 없음)
Identifier: 다른 항목과 구분하는 데 필요한 정보

URL : https://example.com:8042/over/there/name?=ferret#nose
	스키마: https
	authority: example.com:8042
	path: over/there
	query: name=ferret
	nose: fragment

URN : example:animal:ferret:nose
	그냥 자원에 이름을 부여한것. 위치는 변할 수 있지만 이름은 변하지 않음
	URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
	거의 사용하지 않고, 이런게 있다 정도로만 알고있기

## 좋은 URI 설계
URI 는 [[리소스]]만 식별, [[리소스]]와 행위를 분리
'회원을 등록'하고 '회원을 조회'하고 '회원을 수정'하는게 [[리소스]]가 아님. '회원' 이 [[리소스]]임
리소스 : 회원
행위 : 조회, 등록, 삭제, 변경
리소스는 명사, 행위는 동사(미네랄을 캐라)
행위는 [[HTTP 메서드]]로 하면 됨






