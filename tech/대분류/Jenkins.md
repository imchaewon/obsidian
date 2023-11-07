젠킨스란

CI/CD (Continuous Integration)/지속적 배포(Continuous Deployment) 툴

-----

CI 예시

코드 푸시 및 자동 빌드: 개발자가 코드 변경을 버전 관리 시스템에 푸시하면, CI 도구는 변경을 감지하고 자동으로 빌드 작업을 시작함. 이는 코드를 컴파일하고 빌드 결과물을 생성하는 과정임

단위 테스트 실행: 빌드된 애플리케이션에 대해 단위 테스트를 자동으로 실행함. 단위 테스트는 작성한 코드의 일부 또는 전체를 테스트하여 기능을 확인하고 버그를 찾는 작업임

정적 코드 분석: CI 도구는 정적 코드 분석 도구를 활용하여 코드의 품질, 스타일, 보안 문제 등을 검사함. 이를 통해 개발자는 코드 품질을 유지하고 잠재적인 문제를 식별할 수 있음

테스트 커버리지 측정: CI 도구는 테스트 커버리지 도구를 사용하여 테스트 스위트가 얼마나 애플리케이션 코드를 커버하는지 측정함. 이를 통해 개발자는 어떤 부분이 테스트되지 않았는지 확인하고 테스트 범위를 확대할 수 있음

결과 피드백 제공: CI 도구는 빌드, 테스트 및 분석 결과를 개발팀에 제공함. 이를 통해 개발자는 빠르게 피드백을 받고 문제를 신속하게 수정할 수 있음

위와 같은 CI 작업은 코드 변경을 지속적으로 통합하고 품질을 확인함으로써 개발자들이 안정적으로 협업하고 빠른 속도로 애플리케이션을 개발할 수 있도록 도와줌

-----

CD 예시

자동 배포: CI가 성공적으로 완료된 빌드 결과물을 자동으로 스테이징 또는 프로덕션 환경으로 배포함. 이를 통해 애플리케이션의 최신 버전이 신속하게 사용자에게 제공됨

환경 구성 관리: CD 도구를 사용하여 배포 환경의 구성을 관리함. 이를 통해 환경 구성 파일을 버전 관리하고, 다양한 환경 간의 일관성을 유지할 수 있음

테스트 자동화: CD 도구를 사용하여 자동화된 테스트를 실행함. 통합 테스트, 성능 테스트, 보안 테스트 등 다양한 종류의 테스트를 자동으로 수행하여 애플리케이션의 품질을 보장함

롤백 및 복구: CD 도구는 배포 중에 문제가 발생했을 때 롤백 절차를 자동화하여 이전 버전으로 되돌릴 수 있음. 이를 통해 애플리케이션의 안정성을 유지하고 사용자에게 중단 없는 서비스를 제공할 수 있음

모니터링 및 경고: CD 도구를 사용하여 애플리케이션의 성능, 가용성, 로그 등을 모니터링하고, 필요한 경우 경고 및 알림을 설정함. 이를 통해 실시간으로 애플리케이션 상태를 파악하고 잠재적인 문제를 신속하게 대응할 수 있음

위와 같은 CD 작업은 애플리케이션의 지속적인 배포를 자동화하여 개발자와 운영팀이 애플리케이션을 안정적으로 운영하고 신속하게 변경사항을 제공할 수 있도록 도와줌

----------------------------------------------------------------------------------------------------

젠킨스 파이프라인 (젠킨스에서 프로젝트의 빌드, 배포, 테스트 등의 작업을 정의하고 실행하는데 사용되는 젠킨스의 기능)

배포 이벤트 발생 → gitLab에 있는 소스를 가져옴 → maven빌드해서 war파일 생성 → 
cp 명령어로 war파일 이동 후 docker restart 해서 톰캣을 실행중인 Docker 컨테이너를 재시작함으로써 톰캣서버 재실행

↓↓↓

파이프라인은 Jenkinsfile라는 파일에 코드로 작성됨.
젠킨스 웹 인터페이스(프로젝트 > Configuration)에서도 확인/설정 가능

-----

General

GitHub project 체크

Project url
https://gitlab.uniess.co.kr/visitkorea/visitkorea-front.git/

-----

소스 코드 관리

Git 체크

<Repositories>
Repository URL
https://gitlab.uniess.co.kr/visitkorea/visitkorea-front.git

<Credentials>
chaehun/******

<Branches to build>
Branch Specifier (blank for 'any')
origin/develop

<Repository browser>
(자동)

-----

빌드 유발

-----

빌드 환경
Add timestamps to the Console Output 체크

-----

Build Steps

Invoke top-level Maven targets

<Maven Version>
(Default)

<Goals>
clean install -P sandbox -Dmaven.test.skip=true

-----

빌드 후 조치

<SSH Server Name>
sandbox

<Pattern separator>
[, ]+

<Exec timeout (ms)>
120000

<Transfer Set Source files>
target/endpoint5.war

<Romove prefix>
target/

<Remote directory>
relase

<Exec command>
cp ~/release/endpoint5.war /usr/local/docker/tomcat_front/webapps/ROOT.war
sleep 5
docker restart tomcat-front

----------------------------------------------------------------------------------------------------














