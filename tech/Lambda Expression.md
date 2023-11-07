★ 람다, 람다식, Lambda Expresstion
- 함수형 프로그래밍 스타일 지원
- JDK 1.8도입
- 람다식을 사용하면 코드가 간결해지고, 컬렉션을 다루기 쉬워진다
- 람다는 자바의 메소드와 유사하다
- 매개변수를 가지는 코드블럭
- 자바의 람다식은 인터페이스를 통해 만들어진다☆
- 자바의 람다식은 익명 객체 표현을 대신한다
- 코드의 간결함, 지연 연산을 통한 퍼포먼스 향상
- 이터레이션 관련 코드를 구현하는 데 있어 불필요한 부분들을 제거 가능

람다식 기본 문법
- (자료형 매개변수) -> { 실행코드; }
- a. 매개변수 : 메소드의 매개변수와 동일한 역할
- b. -> : 화살표(Arrow). 코드 블럭을 호출하는 역할
- c. 실행코드 : 메소드의 구현부와 동일한 역할

- (int n) -> {System.out.println(n);}


MyClass m1 = new MyClass();
m1.test();

//*** 인터페이스를 구현한 클래스 객체는 되도록 인터페이스 변수를 만들어 저장하는 것이 좋다.
MyInterface m2 = new MyClass();
m2.test();

//익명 객체
MyInterface m3 = new MyInterface() {
	@Override
	public void test() {
		System.out.println("익명 객체에서 구현한 메소드");
	}
};
m3.test();

//람다식
MyInterface m4 = () -> {
	System.out.println("익명 객체에서 구현한 메소드");
};
m4.test();

다른 사용법 동일한 결과

@FunctionalInterface ← 이문장을 추가하면 메소드가 1개만 사용되도록 2개 이상이면 오류메세지를 출력함
interface MyInterface {
	void test();
}

class MyClass implements MyInterface {
	@Override
	public void test() {
		System.out.println("실명(MyClass) 객체에서 구현한 메소드");
	}
}

인터페이스 변수 = 람다식
ex) MyInterface m3 = () -> {};
- 자바는 메소드를 독립 선언하거나, 저장소에 저장을 하지 못한다
- 결국 자바에서 람다식을 다루기 위해서 반드시 인터페이스를 사용해야 한다
1. 반드시 추상 메소드를 1개만 가져야 한다
  The target type of this expression must be a functional interface
  람다가 저장해야할 메소드는 functional interface (메소드를 1개만 갖고있는 인터페이스)여야 한다
2. 람다식을 저장하는 인터페이스를 '람다식의 타겟 타입(Target Type)'이라고 한다
3. 람다식을 저장하는 인터페이스는 추상 메소드를 단 1개만 가지는데 이런 인터페이스들을
  함수형 인터페이스(Functional Interface)라고 부른다.

----------------------------------------------------------------------------------------------------

public static void main(String[] args) {
//		Ex84 : 람다식 이해. 내가 람다식을 직접 만들어서 직접 사용
//		Ex85 : JDK에서 제공하는 여러 람다식과 관련된 기능을 사용하고 싶으면
	
//		함수형 인터페이스, Functional Interface
//		- JDK 1.8부터 제공되는 서비스
//		- 람다식 저장용
//		
//		표준 API 함수형 인터페이스
//		1.Consumer : 매개변수O, 반환값X
//		2.supplier : 매개변수X, 반환값O
//		3.Function : 매개변수O, 반환값O 자유도 높음
//			4.Operator : 매개변수O, 반환값O 매개변수를 연산 후 결과를 반환하는 용도
//			5.Predicate : 매개변수O, 반환값O 매개변수를 논리 판단 후 반환
	
	m1();
}

private static void m1() {
//		Consumer
//		- 매개변수를 받아서 소비하는 일을 구현
//		- acceptXXX() 추상 메소드
	
	Consumer<String> c1 = name -> System.out.println(name);
	c1.accept("홍길동");
	c1.accept("아무개");
	
	Consumer<Integer> c2 = n -> {
		for (int i = 0; i < n; i++) {
			System.out.println(n);
		}
	};
	c2.accept(10);
}




자바 스트림

1. 입출력 스트림
- 콘솔 입출력, 파일 입출력, 네트워크 입출력
2. 스트림
- JDK 1.8
- 배열, 컬렉션 탐색을 지원

스트림, Stream
- 람다식 사용 → 코드 간결

배열, 컬렉션 탐색
1.for문
2.향상된 for문
3.iterator
4.스트림

람다식
- (매개변수) -> {구현부;}
- 인터페이스 = (매개변수) -> {구현부;}

함수형 인터페이스(표준 API 함수형 인터페이스)
1. Consumer
  - (매개변수) -> {구현부;}
2. Supplier
  - () -> {return 반환값;}
3. Function
  - (매개변수) -> {return 반환값;}
4. Operatir
  - (매개변수) -> {return 반환값;}
  - 매개변수와 반환값이 타입 동일
5. Predicate
  - (매개변수) -> {return 반환값;}
  - 반환값의 타입이 boolean

public static void main(String[] args) {
	m1();
	m2();
}

private static void m2(){
	
//		스트림 객체 얻어오기
//		1. 배열로부터
//		2. 컬렉션으로부터
//		3. 숫자 범위로부터
//		4. 파일로부터
//		5. 디렉토리로부터
	
//		1.배열
	int[] nums1 = {10,20,30,40,50};
	
	Arrays.stream(nums1).forEach(n -> System.out.println(n));
	System.out.println();
	
//		2.컬렉션
	Data.getStringList().stream().forEach(word -> System.out.println(word));
	System.out.println();
	
//		3.숫자범위
//		- 일련의 숫자 모음이 필요할 떄 배열을 직접 만들지 않고 사용하기 위해서 제공
	IntStream.range(1,11).forEach(n->System.out.println(n));
	System.out.println();
	
	try {
//		4.파일
		Path path = Paths.get("data.txt");
//			System.out.println(path.toAbsolutePath());
		
		Files.lines(path).forEach(line -> System.out.println(line));
		System.out.println();
		
//		5.디렉토리
	Path path2 = Paths.get("."); //현재 폴더
	System.out.println(path2.toAbsolutePath());
//		dir.listFiles() 동일
//		- 자식 목록 가져오기
	Files.list(path2).forEach(p -> System.out.println(p));
	System.out.println();
	
	} catch (Exception e) {
		System.out.println("Ex_86_Stream.m2()");
		e.printStackTrace();
	}
}

private static void m1() {
	int[] ns1 = Data.getIntArray();
	System.out.println(ns1.length);
	System.out.println(Arrays.toString(ns1));
	
	int[] ns2 = Data.getIntArray();
	System.out.println(ns2.length);
	System.out.println(Arrays.toString(ns2));
	
	List<Integer> ns3 = Data.getIntList();
	System.out.println(ns3);
	
	String[] txt = Data.getStringArray(10);
	System.out.println(Arrays.toString(txt));
	
	User[] users = Data.getUserArray(5);
	
	System.out.println(Arrays.toString(users));
	
	
	System.out.println();
	System.out.println();
	System.out.println();
	
	List<Integer> nums = Data.getIntList(10);
	
//		1. for문
	for (int i = 0; i < nums.size(); i++) {
		System.out.printf("%4d",nums.get(i));
	}
	System.out.println();
	
//		2. 향상된 for문
	for (int i:nums) {
		System.out.printf("%4d",i);
	}
	System.out.println();
	
//		3. iterator
	Iterator<Integer> iter = nums.iterator();
	
	while(iter.hasNext()) {
		System.out.printf("%4d",iter.next());
	}
	System.out.println();
	
//		4.stram
	Stream<Integer> stream = nums.stream();
	
	stream.forEach(new Consumer<Integer>() {

		@Override
		public void accept(Integer t) {
			System.out.printf("%4d",t);
		}
		
	});
	
	System.out.println();
	
	nums.stream().forEach(t -> System.out.printf("%4d",t));
	System.out.println();
	
	Data.getStringList(10).stream().forEach(word -> System.out.println(word));
	System.out.println();
	
	Data.getUserList().stream().forEach(user -> {
		System.out.println("[회원정보]");
		System.out.println("이름 : " + user.getName());
		System.out.println("나이 : " + user.getAge());
		System.out.println("성별 : " + (user.getGender()==1?"남자":"여자"));
		System.out.println();
	});
	
	Data.getItemList().stream().forEach(item -> {
		System.out.println(item.getName());
		System.out.println(item.getColor());
		System.out.println(item.getSize());
		System.out.printf("%tF\n",item.getDate());
		System.out.println();
	});
	
}



public static void main(String[] args) {
//		파이프 라인(Pipe Line)
//		- 여러개의 스트림이 연결되어 있는 구조
//		- 배열 → 스트림(중간조작) → 스트림(중간조작) → 스트림(최종소비)
//		- 중간 처리 : 필터링, 매핑, 정렬, 그룹핑 등
//		- 최종 처리 : 합계, 평균, 카운트, 최댓값, 최솟값, forEach 등
	
	m1();
}

private static void m1() {
//		필터링
//		- filter
//		- 조건에 따라 일부 요소들을 걸러내는 역할
//		- 조건에 만족하는 요소들만 남기고 불만족하는 요소들을 버린다
	
	List<Integer> nums = Data.getIntList(20);
	System.out.println(nums);
	
//		짝수만 출력
	nums.stream().forEach(num->{
		if(num % 2 == 0) {
			System.out.print(num + ", ");
		}
	});
	System.out.println();
	
//		권장↓
	nums.stream().filter(num -> num % 2 == 0).forEach(num -> System.out.print(num + ", "));
	
	Data.getUserList().stream().
		filter(user->user.getGender()==1).
		forEach(user->System.out.println(user));
	
	System.out.println();
	
	Data.getUserList().stream()
		.filter(user -> user.getHeight() >= 170 && user.getWeight() <= 75)
		.forEach(user -> System.out.println(user));
	
	System.out.println();
	
	Data.getUserList().parallelStream()
		.filter(user -> user.getHeight() >= 170)
		.filter(user -> user.getHeight() <= 75)
		.forEach(user -> System.out.println(user));
	
	System.out.println();
	
	Data.getItemList().stream()
		.filter(item -> item.getColor() == Color.YELLOW)
		.forEach(item -> System.out.println(item));
	
	System.out.println();
	
	Data.getItemList().stream()
		.filter(item -> item.getColor() == Color.YELLOW)
		.filter(item -> item.getDate().get(Calendar.DAY_OF_WEEK) == 7)
		.forEach(item -> System.out.println(item));
	
	System.out.println();
	
}


참고 : https://mangkyu.tistory.com/114

----------------------------------------------------------------------------------------------------

Stream Collector

마지막에 결과를 만들때 씀
collect()메소드에 Collectors클래스의 static메소드를 넣어서 씀

↓↓↓Collectors의 메소드들↓↓↓

<요약>
개수 모으기 - counting
최대/최소값 - maxBy, minBy
summingInt, summingLong, summingDouble)
averagingInt, averagingLong, averagingDoubl
summarizingInt, summarizingLong, summarizingDouble
합치기 joining
구분자로 합치기 : joining("구분자")
컬렉션으로 변환 : toList, toSet, toCollection

<다수준 그룹화>
groupingBy, collectingAndThen

<분할>
partitioningBy

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

람다식은 '추상메소드가 딱 하나만 존재'하는 '함수형 인터페이스' 에서만 쓸 수 있음

추상메소드를 편하게 구현한다......라고 생각???

아래는 사용 예제들

----------------------------------------------------------------------------------------------------

더하기

<Calculator.java>
interface Calculator {
	int sum(int a, int b);
}

<MyCalculator.java>
public class MyCalculator implements Calculator{

	@Override
	public int sum(int a, int b) {
		return a + b;
	}

}

<Sample>
public class Sample {
	public static void main(String[] args) {

		MyCalculator mc = new MyCalculator();
		int result = mc.sum(3, 4);
		System.out.println(result);

	}
}

를 람다로 바꾸면 ↓↓↓↓↓

<Calculator.java>
interface Calculator {
	int compare(int a, int b);
}

<Sample.java>
public class Sample {
	public static void main(String[] args) {

		Calculator c = (int a, int b) -> a + b;
		int result = c.compare(3, 4);
		System.out.println(result);

	}
}

----------------------------------------------------------------------------------------------------

(뭔가 이상한..)더하기

public interface Inter {
	int compare(int a, int b);
}

public class Cla {
	public static void sum(Inter inter) {
		int value = inter.compare(2, 5);
		System.out.println(value);
	}

	public static void main(String[] args) {
		sum((a,b) -> {
			return a + b;
		});
	}
}

----------------------------------------------------------------------------------------------------

큰 수 출력하기

public interface Mynumber {
	int getMax(int a, int b);
}

public class Ramda3 {
	public static void main(String[] args) {

		Mynumber max = (x,y) -> (x>=y) ? x : y;

		System.out.println(max.getMax(10, 30));
		
	}
}

----------------------------------------------------------------------------------------------------

메소드 참조(::) → 다른 메소드를 복사한다고 생각하면되는데 정확히는 복사가 아니고 참조임.
함수형 인터페이스는 완전 함수 취급하듯 호출할 수 있음

<MathBox.java>
public class MathBox {
	private int instance_value;

	public MathBox() {}

	public MathBox(int value) {
		this.instance_value = value;
	}

	// 더하기
	public int sum(int a, int b) {
		return a + b;
	}

	// 빼기
	public int sub(int a, int b) {
		return a - b;
	}

	// 나누기 (스태틱 멤버로 함)
	public static int div(int a, int b) {
		return a / b;
	}

	//곱하기 (스태틱 멤버로 함)
	public static int mul (int a, int b) {
		return a * b;
	}

	public int getSumWithInstance(int a, int b) {
		return this.instance_value + a + b;
	}
}

<Function.java>
@FunctionalInterface
public interface Function {
	int func(int a, int b);
}

<Run.java>
public class Run {
	public static void main(String[] args) {

		MathBox box = new MathBox();
		Function sum = box::sum; // 인스턴스 멤버이기 때문에 box라는 인스턴스를 통해서만 접근 가능
		Function mul = MathBox::mul; // static 멤버이기 때문에 MathBox라는 클래스를 통해서 접근이 가능

		System.out.println(sum.func(1, 2)); // 3
		System.out.println(mul.func(1, 2)); // 2

		Number n = new Number(2,3);
		n.print(sum); // 5
		n.print(mul); // 6

	}
}

----------------------------------------------------------------------------------------------------

매개변수 O,  반환 X

인터페이스 코드
public interface Printable {
	void print(String s);
}

<OneParamNoReturn.java>
public class OneParamNoReturn {
	public static void main(String[] args) {

		Printable p;

		p = (String s) -> { System.out.println(s); }; // 줄임 없는 표현
		p.print("Lamda exp one.");

		p = (String s) -> System.out.println(s); // 중괄호 생략 (내용이 1줄일때 가능)
		p.print("Lamda exp two.");

		p = (s) -> System.out.println(s); // 매개변수 형 생략
		p.print("Lamda exp three.");

		p = s -> System.out.println(s); // 매개변수 소괄호 생략 (매개변수가 한개일때 가능)
		p.print("Lamda exp four.");

		p = System.out::println; // 메소드 레퍼런스 (매개변수를 생략하고 :: 뒤에 메소드를 붙임, 매개변수가 1개일때 쓸 수 있음)
		p.print("Lamda exp five.");

	}
}

-----

매개변수 O, 반환 O

인터페이스 코드
public interface Calculate {
	int cal(int a, int b);
}

클래스 코드
public class TowParamAndReturn {
	public static void main(String[] args) {

		Calculate c;

		c = (a, b) -> { return a + b; };
		System.out.println(c.cal(1, 2));

		c = (a, b) -> a + b;
		System.out.println(c.cal(1, 2));

	}
}

★ 메소드 몸체에 연산이 발생되면 그 결과가 반환의 대상이 됨

----------------------------------------------------------------------------------------------------

@FunctionalInterface 어노테이션

함수형 인터페이스에 부합하는지를 확인하기 위한 어노테이션.

@FunctionalInterface
public interface Calculate {
	int cal(int a, int b);
	int cal2(int a, int b);
}

위처럼 인터페이스에 메소드가 두개 이상일경우 빨간줄이 나오고 커서 갖다대면 아래와 같은 오류로 알려줌

Invalid '@FunctionalInterface' annotation; Calculate is not a functional interface
(@FunctionalInterface 어노테이션이 타당하지 않고, Calculate 는 함수형 인터페이스가 아니다)


static이나 default 가 붙은 메소드는 포함되어 있어도 괜찮음. 마찬가지로 함수형 인터페이스에 해당함

@FunctionalInterface
public interface Calculate {
	int cal(int a, int b);

	default int plus(int a, int b) { return a + b; };

	static int sub(int a, int b) { return a - b; };

}

-----

인터페이스를 제네릭으로 정의

자바에 정의되어있는 4가지의 함수형 인터페이스

Function<T,R>
Cunsumer<T>
Predicate<T>
Supplier<T>

-----



----------------------------------------------------------------------------------------------------






























