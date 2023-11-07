TypeScript
- c나 java와 같은 c-family언어와 마찬가지로 정적 타입을 명시할 수 있음
- 자바스크립트를 실제로 사용하기 전에 있을만한 타입 에러들을 미리 잡는 것' 이 타입스크립트의 사용 목적
- interface를 쓸 수 있음
- TypeScript 파일(.ts)은 브라우저에서 동작하지 않으므로 TypeScript 컴파일러를 이용해 자바스크립트 파일로 변환해야 하는데, 이를 컴파일 또는 트랜스파일링이라 함
- ES6을 포함하는 개념


예를들어 아래와 같은 함수가 있음.
function sum(a, b) {
  return a + b;
}

이를 정의한 개발자의 의도는 아마도 2개의 숫자 타입 인수를 받아 그 합계를 반환하는 것으로 추측됨
하지만 코드상으로는 어떤 타입의 인수를 전달하여야하는지, 어떤 타입의 반환값을 리턴해야하는지 명확하지 않음
따라서 위 함수는 아래와 같이 호출될 수 있음
sum("x", "y"); // "xy"

위 코드는 자바스크립트 문법상 어떠한 문제도 없으므로 자바스크립트 엔진은 아무런 이의 제기 없이 코드를 실행할것임
이러한 상황이 발생한 이유는 변수나 반환값의 타입을 사전에 지정하지 않는 자바스크립트의 동적 타이핑에 의한 것.

위 함수를 TypeScript의 정적 타입을 써서 다시 작성하면 아래와 같음

function sum(a: number, b: number) {
  return a + b;
}

sum('x', 'y');
// error TS2345: Argument of type '"x"' is not assignable to parameter of type 'number'.

TypeScript는 정적 타입을 지원하므로 컴파일 단계에서 오류를 포착할 수 있는 장점이 있음
명시적인 타입 지정은 개발자의 의도를 명확하게 코드로 기술할 수 있음
이는 코드의 가독성을 높이고 예측할 수 있게 해주며 디버깅을 쉽게함


★TypeScript 자료형
문자열 : string. (String과 서로 다름. String은 wrapper)
숫자 : number


★Node.js 설치
https://poiemaweb.com/nodejs-basics#2-install


★타입스크립트 설치
Node.js를 설치하면 npm도 같이 설치됨.
다음과 같이 터미널(윈도우의 경우 커맨드창)에서 npm을 사용해 TypeScript를 전역에 설치
$ npm install -g typescript


★설치 확인
$ tsc -v
// Version 4.1.5


★파일 생성
// person.ts
class Person {
	private name: string;

	constructor(name: string) {
		this.name = name;
	}

	sayHello() {
		return "Hello, " + this.name;
	}
}

const person = new Person('Lee');

console.log(person.sayHello());


★트랜스파일링 실행
$ tsc [파일명]

확장자 .ts는 생략 가능
같은 디렉토리에 자바스크립트파일이 생성되는걸 확인 할 수 있음

이때 트랜스파일링된 파일의 자바스크립트 버전은 ES3 이다

자바스크립트 버전을 변경하고 싶을때는 컴파일 옵션에 --target 또는 -t 옵션을 이용할 수 있음
지원하는 자바스크립트 버전 : ES3(default), ES5, ES2015, ES2016, ES2017, ES2018, ES2019, ESNEXT

ES6 버전으로 트랜스파일링 실행
$ tsc [파일명] -t ES2015

// person.js
class Person {
    constructor(name) {
        this.name = name;
    }
    sayHello() {
        return "Hello, " + this.name;
    }
}
const person = new Person('Lee');
console.log(person.sayHello());


★트랜스파일링된 파일 실행
Node.js REPL을 이용

$ node person


★트랜드파일링 설정 파일 만들기 & 설정한 걸로 트랜스파일링
작업 폴더에서
$ tsc --init

tsconfig.json이 생성됨 (환경설정 파일)

이후 트랜스파일링시
$ tsc
만 입력하면 자동으로 폴더의 모든 ts파일이 js로 트랜스파일링됨(파일명은 입력하면 안됨. 파일명 입력시 tsconfig.json이 무시됨)


★내용 변경될시 자동으로 트랜스파일링되게 하기
--watch혹은 -w 옵션을 써서 프로세스를 켜놓으면, 디렉토리 내 ts파일이 변경되었을때 자동으로 트랜스파일링됨
$ tsc --watch

혹은 아래와 같이 tsconfig.json에 watch 옵션을 추가할 수도 있음
{
	"watch":true
}
그러면 이후에 아래 명령어를 입력했을때 -w옵션을 쓴것과 마찬가지로 트랜스파일링 & 파일 변경 감지가 시작됨
$ tsc

----------------------------------------------------------------------------------------------------

리액트에서 타입스크립트에서 쓰는법

$ npx create-react-app [프로젝트명] --template typescript

프로젝트에 App.tsx 생긴거 확인

----------------------------------------------------------------------------------------------------

interface(인터페이스)

자바랑 똑같이 쓸 수 있음

interface Props {
	getArea() : number;
}

class Rect implements Props{
	width: number;
	height: number;
	constructor(width: number,height: number){
		this.width = width;
		this.height = height;
	}
	getArea(): number { // 이걸 구현 안하면 컴파일오류발생
		throw new Error('Method not implemented.');
	}
}

-----

Optional Property (선택적 속성)

인터페이스에서 정의한 메소드는 구현하는 클래스에서 가지고있어야하지만,
Optional프로퍼티는 말 그대로 선택적으로 구현하는 프로퍼티임
있어도 되고 없어도 되는 프로퍼티가 있다면 프로퍼티 식별자 뒤에 간단하게 ? 를 붙이면 됨

interface Shape{
	width? : number;
	height? : number;
	radius? : number;
	getArea() : number;
}

class Circle implements Shape{
	radius: number | undefined;
	getArea(): number {
		throw new Error('Method not implemented.');
	}
}

Circle클래스에서는 getArea()는 구현해야하지만 옵셔널프로퍼티는 포함하지 않아도 됨

-----

Diuck Typing(덕 타이핑)

사람이 오리처럼 행동하면 오리로 봐도 무방하다는 뜻
TypeScript의 덕 타이핑 : 어떤 객체가 특정 인터페이스에서 명시하는 메소드를 가지고 있다면 해당 객체가 그 인터페이스를 구현한 것으로 보는 것

ex)
import React from 'react';

interface Quackable{
	quack(): void;
}

class Duck implements Quackable {
	quack() {
		console.log('꽥!');
	}
}

class Person {
	quack() {
		console.log('나도 꽥!');
	}
}

function makeSomeNoiseWith(duck:Quackable):void {
	duck.quack();
}

makeSomeNoiseWith(new Duck()); // OK
makeSomeNoiseWith(new Person()); // OK

const DuckTyping = ({  }) => {
	return (
		<div>
		</div>
	)
}

export default DuckTyping;

자바스크립트는 동적타입 언어이므로 위같은 코드를 쓸 수가 있음

-----

Indexable

괄호표기법으로 동적으로 속성에 접근할 경우 index signature 가 없다는 에러메세지가 보인다.
이유는, 프로퍼티에 접근할 때 어떤 타입인지 확인할 수 없어 암묵적으로 any 타입을 사용하기 때문이다.

interface Indexable{
	[key: string]: any;
}

const dict: Indexable = {
	foo: 1,
	bar: 2
}

Object.keys(dict).forEach(k => console.log(dict[k]));
// 인덱스시그니처를 쓰지 않을경우 dict[k] 이부분에서 묵시적으로 any 타입으로 변환하므로 오류가 발생함

-----

함수 인터페이스

함수도 인터페이스로 선언할 수 있음
인터페이스를 구현한 함수에서도 똑같이 자료형을 쓰거나, 아무것도 쓰지 말아야(=any)함. 다른 자료형을 쓰면 컴파일오류 발생

interface numberOperation {
	(arg1: number, arg2: number): number; // 괄호 안에있는건 파라미터고 밖에있는건 반환자료형임
}

const sum: numberOperation = (arg1: number, arg2: number): number => {
	return arg1 + arg2;
}

const multiply: numberOperation = (arg1, arg2) => {
	return arg1 * arg2;
}

// const toArray: numberOperation = (arg1: any, arg2: any): any[] => { // Type '(arg1: any, arg2: any) => any[]' is not assignable to type 'numberOperation'.
// 	return [arg1, arg2]
// }

console.log(sum(1,2));
console.log(multiply(2,3));

-----

생성자 인터페이스

자바스크립트에서 함수는 일급객체이므로 다른 함수에 인자로 넘길 수 있음.
생성자도 마찬가지로 일급함수이므로 인자로 넘기는 것이 가능함

interface Animal{
	name: string;
	age: number;
}

interface AnimalConstructor{
	new (name: string, age: number): Animal;
}

class Dog implements Animal{
	name:string;
	age:number;
	constructor(name:string, age:number){
		this.name = name;
		this.age = age;
	}
}

class Cat implements Animal{
	name: string;
	age: number;
	constructor(name:string, age:number){
		this.name = name;
		this.age = age;
	}
}

function createAnimal(cstr:AnimalConstructor, name:string, age:number){
	return new cstr(name, age);
}

console.log(createAnimal(Dog, "팔랑", 15));
console.log(createAnimal(Cat, "쭈쭈", 10));

-----

하이브리드 타입

하이브리드 타입은 함수이기도 하면서 객체이기도 한 인터페이스이다
예를 들면 jQuery의 $ 는 객체이기도 하면서 쿼리 셀렉터 기능을 하는 함수이기도 함
이경우에 jQuery의 인터페이스를 정의하면 다음과 같이 쓸 수 있을것이다

interface jQueryElement {
  // ...
}

interface jQueryInterface {
  (string: query): jQueryElement;
  each: Function;
  ajax: Function;
  // ...
}

위처럼 함수 인터페이스의 문법과 일반 인터페이스 프로퍼티의 문법을 함께 사용할 수 있음.
사용하려는 JavaScript 라이브러리가 jQuery처럼 함수이면서도 객체로 구현된 경우, 이런 형태로 인터페이스를 정의 할 수 있음

-----

그 밖에 인터페이스가 인터페이스를 extends 키워드를 통해 확장할 수 있으며, 인터페이스끼리 다중 상속도 가능함

----------------------------------------------------------------------------------------------------





























