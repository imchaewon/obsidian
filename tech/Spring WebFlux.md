[[Spring]] [[Framework]] 의 일부로, [[리액티브 프로그래밍]]을 지원하는 [[프레임워크]]

- Spring 5부터 지원하는 리액티브 웹 [[프레임워크]]


[[리액티브 프로그래밍]]

------------------------------

Reactive Streams를 구현한 구현체
- [[RxJava]]
- Java 9 Flow AP

----------------------------------------------------------------------------------------------------

Blocking I/O 방식

- 작업쓰레드가 종료될 때까지 요청을 한 쓰레드는 차단됨
- 이러한 단점을 보완하기 위해 멀티 쓰레딩 기법을 통해 추가 쓰레드를 할당할 수 있음
	그러나 CPU 대비 많은 수의 쓰레드를 사용하는 애플리케이션은 비효율적이다
	- 컨텍스트 스위칭(Context Switching)으로 인한 쓰레드 전환 비용 발생
 	- 메모리 사용에 있어서 오버헤드 발생
	- 쓰레드 풀에서 응답 지연 문제 발생

------------------------------

Non-Blocking I/O 방식

- 작업쓰레드의 종료와 상관없이 요청을 한 쓰레드는 차단되지 않음
- 적은 수의 쓰레드를 사용하기 때문에 쓰레드 전환 비용이 적게 발생함

따라서 CPU 대기 시간 및 사용량에 있어서도 효율적임
그러나, CPU를 많이 사용하는 작업이 포함되어있을 경우에는 성능 향상에 악영향을 줌
또한, 사용자 요청에서 응답까지의 과정에 Blocking I/O요소가 포함되어 있을 경우 Non-Blocking의 이점을 발휘하기 힘듦

----------------------------------------------------------------------------------------------------

Spring MVC → Blocking I/O 방식

요청 당 하나의 쓰레드를 사용함
과도한 쓰레드 사용으로 인한 CPU 대기시간이 늘어나고 메모리 사용에서 오버헤드가 발생함

------------------------------

Spring WebFlux → Non-Blocking I/O 방식

하나의 쓰레드로 대량의 요청을 처리함
적은수의 쓰레드를 사용하므로 CPU와 메모리를 효율적으로 사용함
CPU를 많이 사용하는 복잡한 계산을 요청할 경우 다른 요청들을 처리할 수 없음(이 경우 복잡한 계산을 처리하는 별도의 전용 쓰레드를 두거나, 외부 시스템에 이런 복잡한 계산을 위임해서 처리해야함)
요청에서 응답까지 Fully Non-Blocking이여야 진정한 효과를 발휘함

----------------------------------------------------------------------------------------------------

Spring MVC

학습시간이 상대적으로 짧음
10년 이상 주도적으로 사용된 명령형 프로그래밍 기반 기술이기 때문에 숙련된 개발자를 찾기가 쉬움. 따라서
기업에서도 신규 프로젝트를 안정적으로 진행할 수 있는 가능성이 높음

------------------------------

Spring WebFlux

학습 난이도가 비교적 높은편 (리액티브 프로그래밍 자체가 학습 난이도가 높기때문)
선언형 방식의 Non-Blocking 프로그래밍 지식을 갖춘 숙련된 개발자를 찾는것이 어려움. 따라서
기업에서는 개발 인력면에서나 기술적인 측면에서나 위험 부담을 감수해야 할 가능성이 높음

----------------------------------------------------------------------------------------------------














