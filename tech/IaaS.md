Infrastructure as a Service

클라우드 컴퓨팅 모델 중 하나.
IaaS는 IT 인프라스트럭처, 예를 들어 가상 서버, 네트워킹, [[스토리지]] 등을 [[클라우드 제공 업체]]에서 제공받을 수 있는 서비스

가상화된 컴퓨팅 리소스, 스토리지, 네트워킹 등의 인프라를 제공하는 서비스 모델. 가장 많은 제어와 관리가 요구됨

클라우드 공급자가 하드웨어를 관리하고 가상화된 인프라를 제공하며,
사용자는 운영체제, 미들웨어, 어플리케이션 등을 직접 관리함
사용자는 가상 서버를 프로비저닝(컴퓨팅 리소스(가상머신/스토리지/네트워크)를 설정하고 사용 가능한 상태로 만드는것)하고 관리할 수 있음

ex) 일을 할 회사 건물을 임대를 해서 일을 하는 개념

-----

클라우드서비스제공자 관점에서 IaaS 를 구축할때
가상화 기술을 이용함(하이퍼바이저라는 가상화 플랫폼 이용)

 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅣ가상머신	ㅣ가상머신	ㅣ
 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅣ    하이퍼바이저	ㅣ
 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ          ( 아래쪽에서부터 보면 됨 )
ㅣ           OS             ㅣ
 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅣ        하드웨어	        ㅣ
 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

각 가상머신은 다시 아래처럼 구성되어있음

 ㅡㅡㅡㅡㅡㅡㅡㅡ
ㅣ   앱   ㅣ  앱    ㅣ
 ㅡㅡㅡㅡㅡㅡㅡㅡ
ㅣ Bin / Library ㅣ          ( 아래쪽에서부터 보면 됨 )
 ㅡㅡㅡㅡㅡㅡㅡㅡ
 |         OS        ㅣ
 ㅡㅡㅡㅡㅡㅡㅡㅡ

설명 : OS가 가상머신개수 + 1 이며, 가상머신 별 개별적 자원(CPU, 메모리 등) 할당
각 가상머신이 완전하게 격리되고, 특정 가상머신의 문제가 다른 가상머신의 문제로 전이될 가능성이 낮음

※ Bin / Library : 프로그램이 실행하는 데 필요한 환경과 관련된 파일

-----

ex) Amazon의 대다수 서비스들(EC2, S3, VPC 등), Azure의 Virtual Machines