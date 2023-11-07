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
