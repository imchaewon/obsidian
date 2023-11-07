XXX is not defined
↓↓↓
오류가 났다는 줄(Line)을 확인

① 임포트 안한경우
사용자 컴포넌트(js파일) 임포트하기
import XXX from 'abc';

② 컴포넌트에서 default를 잘못쓴경우(복사해놓고 값을 제대로 안바꿨을때)
export default XXX


Unexpected reserved word 'await'.
↓↓↓
await 만 쓰고 async를 안쓴경우


Each child in a list should have a unique "key" prop.
↓↓↓
map쓸때 JSX태그에 아래 속성 추가해주기
key={아이템변수}


Uncaught Error: Too many re-renders. React limits the number of renders to prevent an infinite loop.
↓↓↓
useState 이용시 state세터를 함수 내부가 아니라 그냥 선언해버린경우
ex)
setCnt(cnt+);
위처럼 하면 안되고
아래처럼 세터를 함수로 감싸야함
let increase = () => {
	setCnt(cnt+1);
}


undefined is not iterable (cannot read property Symbol(Symbol.iterator))
↓↓↓
const [cnt2, setCnt2] = useState(0);
위처럼써야하는데 아래처럼 괄호를 잘못쓴경우
const [cnt2, setCnt2] = useState[0];


콘솔이 두번씩 찍힐때
index.js 에서 <React.StrictMode>태그 지우기


Could not find a required file.
  Name: index.js
  Searched in: /Users/mac/react/router/src
↓↓↓
마우스 잘못조작해서 src폴더를 publuc폴더안에 넣어버린경우


export 'default' (imported as 'BBB') was not found in 'AAA'
↓↓↓
import시 AAA에서 BBB를 가져올떄 중괄호안에 안쓴경우
ex)
import useNavigate from 'react-router-dom'→ X
import {useNavigate} from 'react-router-dom' → O


Module not found: Error: Can't resolve 'BBB' in '/Users/mac/react/AAA'
↓↓↓
import시 AAA에서 BBB를 가져오려고 하는데 AAA경로에 BBB가 없을경우


Uncaught (in promise) SyntaxError: Unexpected token < in JSON at position 0
↓↓↓
없는 JSON서버에 요청한경우


JSON서버에 요청했는데 빈배열이 나온경우
↓↓↓
서버는 맞으나 경로가 틀린경우

Can't resolve 'bootstrap/dist/css/bootstrap.min.css
↓↓↓
부스트스랩 이용시 npm 설치를 안한경우
해당 프로젝트에 설치하기
npm install react-bootstrap bootstrap

----------------------------------------------------------------------------------------------------

리액트란?

웹 프레임워크로 자바스크립트 라이브러리의 하나로써 사용자 인터페이스를 만들기 위해 쓰여진다

----------------------------------------------------------------------------------------------------

1. SPA(프로젝트 내 html파일이 1개). 리프레쉬 없이 모바일 앱처럼 쓸 수 있음
2. html없이 자바스크립트에서 다 함
3. 코드 재활용 가능

값 변하면 UI도 자동으로 바뀜

★ UI가 바뀌게 하려면 State를 써야함

----------------------------------------------------------------------------------------------------

리액트 훅 : 리액트를 할떄 필요한 유용한 함수

useState() 는 state를 만들기 위헤 씀

state가 변환되면 UI도 자동으로 바뀜

웬만한일에는 → state
잠깐 기억해야하면 → 변수

----------------------------------------------------------------------------------------------------

리액트의 특징

Data Flow : 데이터의 흐름이 한방향으로만 흐르는 단방향 데이터 흐름을 가짐

Component 기반 구조 : 컴포넌트 단위로 쪼개져있어 전체 코드를 파악하기 쉬움, UI단위로 캡슐화해 재사용성 높임

Virtual DOM : DOM은 html,css,xml등을 트리구조로 인식, 데이터를 객체로 간주하고 관리하는데,
이벤트가 발생할때마다 가상돔을 만들고, 다시 그릴때마다 실제돔과 비교하고 전후상태를 비교해 변경이 필요한 최소한만 변경후 실제돔에 반영해
앱의 효율성과 속도를 개선시킴


Props and State

Props : 부모컴포넌트애서 자식컴포넌트로 전달해주는 데이터를 말함. 쉽게말해 읽기전용 데이터.
자식컴포넌트에서 전달받은 props는 변경이 불가능하고 props를 전달해준 최상위 부모 컴포넌트만 props를 변경할 수 있다

State : 컴포넌트 내부에서 선언하며 내부에서 값을 변경할 수 있음. state는 동적인 데이터를 다룰때 사용하며, 사용자와의 상호작용을 통해
데이터를 동적으로 변경할때 씀. 클래스형 컴포넌트에만 쓸수있고, 각각의 state는 독립적임


JSX(JavaScript XML) : Javascript에 XML을 추가해 확장한 문법
리액트로 프로젝트를 개발할때 쓰므로 공식적인 자바스크립트 문법은 아님
브라우저에서 실행하기 전에 바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환됨
리액트에서 JSX사용이 필수는 아니지만 대부분의 사람들은 Javascript코드 안에서 UI관련 작업을 할때 시각적으로 더 도움이 된다고 생각한다고함

문자도 HTML도 아닌 JavaScript의 확장문법

-----

JSX 예시

//실제 작성할 JSX의 예시
function App(){
	return(
		<p>hi hello?<p>
	);
}

//위와같이 작성하면, 바벨이 다음과 같이 자바스크립트로 해석하여줌
function App(){
	return React.createElement("p", null, "hi hello?");
}

JSX는 하나의 파일에 자바스크립트와 HTML을 동시에 작성하여 편리함
자바스크립트에서 HTML을 작성하듯이 하기 때문에 가독성이 높고 작성하기 쉬울 수 있음

-----

JSX 문법

★반드시 부모 요소 하나가 감싸는 형태여야 한다.

잘못된 예)
function App(){
	return(
		<div>hi</div>
		<div>hello</div>
	);
}

올바른 코드)
function App(){
	return(
		<div>
			<div>hi</div>
			<div>hello</div>
		</div>
	);
}

위처럼 하나의 요소로 감싸지 않으면 Faild to compile 오류남

-----

★자바스크립트 표현식
JSX내에서 자바스크립트 표현식을 쓰려면 {}로 감싸면 됨

ex)
function App(){
	var name = "hangain";
	return(
		<div>
			<div>hi</div>
			<div>{name}!!</div>
		</div>
	);
}

-----

★if문 쓰는법 외부/&&연산자/삼항연산자/즉시실행함수 이용

if와 for는 JavaScript표현식이 아니기때문에 JSX내부 자바스크립트 표현식에는 쓸 수 없음
때문에 조건부에 따라 다른 렌더링시 JSX주변에서 if문을 쓰거나 {}안에서 삼항연산자를 쓴다

방법1) return문 외부에서 변수를 만들어서 사용
let secLoginout;
if(!authenticate){
	secLoginout = <div className='login-button' onClick={goToLogin}>
		<FontAwesomeIcon icon={faUser} />
		로그인
	</div>
}else{
	secLoginout = <div className='login-button' onClick={goToLogout}>
		<FontAwesomeIcon icon={faUser} />
		로그아웃
	</div>
}

return (
	<div>
		<div>
			{secLoginout}
		</div>

방법2) &&(AND연산자) 사용
{loginYn === "Y" && <div>회원입니다</div>} // 조건이 만족하지 않을 경우 아무것도 노출되지 않는다.

방법3) 내부에서 사용 (조건문 내부에서 자바스크립트는 못씀)
<div>
	{loginYn === "Y" ?
		<div>회원입니다</div>
		<div>회원~</div>
	:
		<div>비회원입니다</div>
		<div>비회원~</div>
	}
</div>

방법4) 즉시실행함수 사용 (조건문 내부에서 자바스크립트 쓸 수 있음. return연산자 필요)
<div>
	{
		(()=>{
			if(1==1){ return(
				<div className='login-button' onClick={goToLogin}>
					<FontAwesomeIcon icon={faUser} />
					로그인
				</div>
			)}else{ return(
				<div className='login-button' onClick={goToLogout}>
					<FontAwesomeIcon icon={faUser} />
					로그아웃
				</div>
			)}
		})()
	}
</div>
<div className='navSection'>
	...
</div>

-----

★ React DOM은 HTML 속성명대신 camelCase 명명규칙을 씀

1) JSX 스타일링
 - JSX에서 자바스크립트 문법을 쓰려면 {}를 써야 하기 때문에, 스타일을 적용할 때에도 객체 형태로 넣어야 함
 - 카멜 표기법으로 작성해야 함 (font-size => fontSize)

ex)
function App() {
	const style = {
		backgroundColor: 'green',
		fontSize: '12px'
	}
	return (
		<div style={style}>hello</div>
	);
}

2) class 대신 className (className은 컴포넌트를 선언한곳에서 넣어야함. 호출하는곳에서 <Box className="asd"/> 이렇게는 안됨)
ex)
function App() {
	return (
		<div className="testClass">hello</div>
	);
}


5. JSX내에서 주석 쓰는법. {}(중괄호) 안에서만 쓸수있음
한줄 : //
여러줄 : /* */

----------------------------------------------------------------------------------------------------

JSX foreach

foreach대신 map이 있음. 쓰는법은 아래와 같음

product객체의 size라는 배열이 [S, M, L] 일때

{product?.size.map(item => (
	<Dropdown.Item href="#">{item}</Dropdown.Item>
))}

----------------------------------------------------------------------------------------------------

컴포넌트는 파일명 첫글자를 대문자로 작명함 (자바 클래스처럼)

----------------------------------------------------------------------------------------------------

JSX 문법 추가설명 1

<div className="box">	// class는 className으로 씀
	<Title text="hello world" width={200} />	// Title은 리액트의 컴포넌트임. Title컴포넌트는 text, width라는 두 개의 속성값을 입력받음.
	<button onClick={() => {}}>좋아요</button>	// 리액트에서는 이벤트 처리함수를 호출할 떄 브라우저에 상관없이 통일된 이벤트 객체를 전달해줌
	<a href="/home" style={{marginTop:"10px",color:"red"}}>홈으로 이동</a>	// 스타일은 카멜표기법으로
</div>

-----

JSX 문법 추가설명 2

const[authenticate,setAuthenticate] = useState(false) // true일때 로그인

useEffect(() => {
	console.log("authenticate: ",authenticate);
},[authenticate])	// 최초 로딩 & authenticate 가 바뀔때마다 내용물을 실행

const logout = () => {
	setAuthenticate(false)
}

return (
	<div>
		<Navbar authenticate={authenticate} setAuthenticate={setAuthenticate}/>	//  컴포넌트 속성으로 state와 setState를 담기
		<Routes>
			<Route path="/" element={<ProductAll/>} />	// url이 /일경우 해당 컴포넌트를 출력
			<Route path="/login" element={<Login setAuthenticate={setAuthenticate}/>} />	// url에 따라 해당하는 컴포넌트를 출력 (setState 함수도 넘김)
			<Route path="/logout" element={<Logout setAuthenticate={setAuthenticate}/>} />
			<Route path="/product/:id" element={<PrivateRoute authenticate={authenticate}/>} />
		</Routes>

-----

useState 추가설명

const [cnt,setCnt] = useState(0);

이렇게 state를 생성한 다음

<button onClick={() => setCnt(cnt+1)}>증가</button>
이건 되는데

<button onClick={() => setCnt(cnt++)}>증가</button>
이건 안됨

<button onClick={() => setCnt(++cnt)}>증가</button>
이렇게 하려면 const 말고 let으로 해야함

----------------------------------------------------------------------------------------------------

babel

jsx를 자바스크립트로 바꿔주는 트랜스파일러

-----

설치

1. 노드.js 설치

2. 어딘가에 작업폴더 하나 만들기

3. 터미널로 들어가서 npx create-react-app hello 입력 (노드js 깔려있어야함)

그러면 hello라는 폴더가 만들어지고 그안에 앱이 설치됨

-----

설치 다른 방법

1. 터미널에 다음 명령어 입력
npm install @babel/core @babel/cli @babel/preset-react

2. cd로 작업파일위치까지 이동

3. 아래 명령어 입력해서 
JSX문법으로 만든 파일을, 바벨을 이용해서 createElement()함수를 이용한 코드로 컴파일하기

npx babel --watch [변환전 폴더] --out-dir [변환후 폴더] --presets @babel/preset-react

ex) npx babel --watch src --out-dir . --presets @babel/preset-react

한번 실행시켜놓으면 프로세스종료(ctrl+c)하기 전까지 이후 파일이 변경될때마다 자동으로 변경되어 컴파일됨

----------------------------------------------------------------------------------------------------

명령어
★ 터미널에서 명령어 실행할떄 해당 프로젝트 경로로 가서 실행햐아함

npm start
npm run build
npm run test
npm run eject

----------------------------------------------------------------------------------------------------

리액트 앱 실행

1. 터미널로 작업디렉토리(hello폴더)로 들어가서 npm start 입력
로딩후 브라우저에서 리액트 앱 나타남

2. 리액트 개발을 쉽게 하기 위한 개발자 도구 확장프로그램 다운받기
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en-US
설치완료후 크롬 껏다키면 element/console있는 탭에 리액트탭도 추가되어있음

----------------------------------------------------------------------------------------------------

CRA(Create-React-App)로 만든 리액트 폴더에서

public 폴더 : 가상 DOM을 쓰기위해 빈껍데기 html이 필요한데, 그 빈껍데기가 존재하는 폴더
src 폴더 : 리액트 개발이 이루어지는 메인폴더

-----

Public 폴더의..

favicon.ico : 페이지 아이콘 이미지파일

index.html : 가상돔이 들어가기 위한 빈껍데기 html파일

manifest.json : 사용자가 볼것으로 예상되는 영역(ex: 휴대기기 홈화면)에 웹앱이나 사이트를 나타내는 방식을 개발자가 제어하고,
사용자가 시작할 수 있는 항목을 지시하고, 시작시의 모습을 정의할 수 있는 json파일임

-----

src 폴더의..

index.js : 아래는 기본으로 만들어지는 코드인데 App.js에서 생성된 리액트 코드를 index.js에서 불러온 후, pubic에 있는 index.hmtl의 id가
'root'인 곳에다가 넣는 코드임

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);


App.js : 아래는 리액트 코드를 생성하는 부분으로 App라는 클래스를 생성한 후 리액트 컴포넌트를 상속받음. 그러면 리액트 컴포넌트 메소드를 쓸수있게됨
return으로 받는 값들은 나중에 html코드로 바뀌게 됨. 그렇게 생성된 App함수를 export문법을 통해 내보냄

import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

----------------------------------------------------------------------------------------------------

src폴더 내에서, app.js 와 index.js 만 남기고 다른 파일들을 모두 지우기

그럼 실행시 오류가 나는데

-----

App.js의 내용을 아래처럼 바꾸기

import React, {Component} from 'react';

class App extends Component {
	render(){
		return <div className="App">hello</div>;
	}
}

export default App;

-----

package.json에서 "scripts": { 부분에
"test":~
"eject":~
필요없는 두줄 지우기

-----

index.js의 내용을 아래처럼 바꾸기

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));

-----

잘 작동되는지 브라우저에서 테스트

----------------------------------------------------------------------------------------------------

State 와 Props
둘다 데이터를 다룰 때 사용되는 개념으로, 하위 컴포넌트에 상속이 가능함

state : 하나의 컴포넌트가 가질 수 있는 변경 가능한 데이터(변수를 저장할수 있는 객체?)
props : State와 달리 값을 변경불가 (현재 버전에서는 안 쓰는것을 추천)

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

state를
return (
	<div>
		<div>{asd}</div>
이렇게 return안에서(JSX에서) 쓴 경우 세터로 인해 값이 "바뀔"때마다 UI가 다시 그려지면서
스크립트가 재호출되고 & JSX의 {} 안에 있는 값이 바뀜 (세터를 실행했다 하더라도 값이 안바뀌었으면 아무 일도 안일어남)


State를 활용한 예제


App.js의 내용을 아래처럼 바꾸기

import React, {Component} from 'react';

class App extends Component {
	state = {
		hello: 'hello app js'
	}

	render(){
		return <div className="App">hello....... {this.state.hello}</div>;
	}
}

export default App;


잘 작동되는지 테스트

-----

this.state.hello 값을 변경하는 하는 메소드를 만들어 보기

App.js의 내용을 아래처럼 바꾸기


import React, {Component} from 'react';

class App extends Component {

	state = {
		hello: 'hello app js!'
	}

	handleChange = () => {
		this.setState({
			hello: 'bye app js!'
		});
	}

	render(){
		return(
			<div className="App">
				<div>{this.state.hello}</div>
				<button onClick={this.handleChange}>click me!</button>
			</div>
		);
	}
}

export default App;

잘 작동되는지 테스트
html에서는 이벤트를 걸때 onclick이지만 JSX에서는 onClick으로 카멜표기법을 씀
JSX파일에서 메소드를 호출할때 this.handleChange() 이렇게 하면 JSX가 html로 바뀌는 과정에서 실행이 되어버리기때문에 괄호를 생략해야함
이벤트에 따옴표도 쓰면 안됨 ex)onclick="{}" → X

----------------------------------------------------------------------------------------------------

숫자를 올리는 메소드 만들어보기

import React, {Component} from 'react';

class App extends Component{
	state = {
		count: 0
	}
	countUp = () => {
		this.setState({
			count: this.state.count + 1
		});
	}

	render(){
		return(
			<div className="App">
				<div>{this.state.count}</div>
				<button onClick={this.countUp}>count up!</button>
			</div>
		);
	}
}

export default App;

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

Props를 활용한 예제

----------------------------------------------------------------------------------------------------

ex) 문자열 불러와 출력하기

<index.js>
App태그의 속성으로 message라는 속성명과 값을 넣음

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
	<App message="hello Message" />, 
	document.getElementById('root')
);


<App.js>
this.props.변수명으로 꺼냄

import React, {Component} from 'react';

class App extends Component{
	render(){
		return(
			<div className="App">
				<div>{this.props.message}</div>
			</div>
		);
	}
}

export default App;

-----

ex) props로 객체를 보내고 받기

<App.js>
const obj1 = {
	a: "aa",
	b: "bb"
}
return (
	<div>
		<WeatherBox objjj={Obj1}/>

objjj라는 key에 objjj라는 객체가 담김

const WeatherBox = (p) => {
	console.log(p);
↓↓↓
objjj: {
	a: "aa"
	b: "bb"
}

console.log(p.objjj.a) → aa


이때 받는 컴포넌트에서 보낸 키를 중괄호로 감싸서 받으면 한겹이 벗겨져서 좀 더 편하게 받을 수 있음
const WeatherBox = ({objjj}) => {
	console.log(objjj);
↓↓↓
{
	a: "aa"
	b: "bb"
}

console.log(objjj.a) → aa

----------------------------------------------------------------------------------------------------

상속받아 값을 변경하기

<App.js>

import React, {Component} from 'react';

class App extends Component{
	state = {
		count: 0
	}
	countUp = () => {
		this.setState({
			count: this.state.count + 1
		});
	}

	render(){
		return(
			<div className="App">
				<div>{this.props.message1}</div>

				<h3>Props Test</h3>
				<div className="inside-app-props">
					<InsideApp1
						count={this.state.count}
						countUp={this.countUp}
					/>
				</div>
			</div>
		);
	}
}

class InsideApp1 extends Component{
	render(){
		return(
			<div>
				<p>{this.props.count}</p>
				<button onClick={this.props.countUp}>click me!</button>
			</div>
		);
	}
}

export default App;

----------------------------------------------------------------------------------------------------

createElement(component, props, ...children)

첫번째 인수 : 문자열 or 리액트 컴포넌트.
	component의 인수가 문자열이면 html 태그에 해당하는 폼 요소가 생성됨. 예를들어 문자열 p를 입력하면 html p태그가 생성됨

두번쨰 인수 : props는 컴포넌트가 사용하는 데이터를 나타냄. 돔 요소의 경우 style, className 등의 데잉터가 사용될 수 있음

세번째 인수 : 해당 컴포넌트가 감싸고 있는 내부 컴포넌트를 가리킴. div 태그가 두개의 p태그를 감싸고 있는 경우 다음과 같이 작성가능
<div>
	<p></p>
	<p></p>
</div>

↓↓↓

createElement(
	'div',
	null,
	createElement('p',null,'hello'),
	createElement('p',null,'hello'),
)

----------------------------------------------------------------------------------------------------

ReactDOM.render()

컴포넌트 생성을 다 한 뒤 마지막에 html에 넣으려면
ReactDOM.render함수를 통해서 html요소에 넣어야함

const domContainer = document.querySelector("#react-root");
ReactDOM.render(React.createElement(Container), domContainer);

----------------------------------------------------------------------------------------------------

웹팩

자바스크립트로 만든 프로그램을 배포하기 좋은 형태로 묶어주는 도구

<file1.js>
export default function func1(){}
export function func2(){}
export const variable1 = 123;
export let variable2 = "hello";

<file2.js>
import myFunc1, {func2, variable1, variable2} from ".file1.js";

<file3.js>
import{func2 as myFunc2} from  "./file1.js";

코드를 내보낼때는 export 키워드를 씀
코드를 사용하는 쪽에서는 import, from 키워드를 씀
default키워드는 한 파일에서 한번만 사용할 수 있음
default키워드로 내보내진 코드는 괄호없이 가져올 수 있고, 이름은 원하는 대로 정할 수 있음

<file1.js>에서 내보낸 func1함수는 <file2.js>에서 myFunc1이라는 이름으로 가져왔음
default키워드 없이 내보내진 코드는 괄호로 감싸서 가져와야함
가져올때는 내보낼때 쓴 이름 그대로 가져와야하고, 원한다면 as 키워드를 이용해서 이름을 변경해서 쓸 수 있음

-----

웹팩 쓰는법

1. "webpack-test" 라는 폴더를 만들기

2. 터미널에서 해당 폴더를 찾아가기

3. 아래 코드 실행하기
npm init -y

그러면 package.json파일이 만들어짐


4. "webpack-test"폴더에
index.html,
src폴더,
	src폴더 밑에 index.js,
	src폴더 밑에 Button.js

를 만들고 index.html파일에는 다음 코드 입력

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>
	<h2>안녕하세요. 이 프로젝트가 마음에 드시면 좋아요 버튼을 눌러 주세요.</h2>
	<div id="react-root"></div>
	<script src="dist/main.js"></script>
</body>
</html>


5. 아래 명령어를 실행함
npm install webpack webpack-cli react react-dom

그럼 node_modules폴더 및 그안에 react폴더와 react-dom폴더가 만들어지고 그 폴더들 안에는
react.production.min.js / react.development.js , react-dom.production.min.js / react-dom.development.js 파일들이 각각 들어있고
추가로 package-lock.json파일도 만들어짐


6. index.js에 아래 내용 입력
import React from "react";
import ReactDOM from "react-dom";
import Button from "./Button.js";

function Container(){
	return React.createElement(
		"div",
		null,
		React.createElement("p", null, "버튼을 클릭해주세요"),
		React.createElement(Button, {label: "좋아요"}),
		React.createElement(Button, {label: "싫어요"})
	);
}
const domContainer = document.querySelector("#react-root");
ReactDOM.render(React.createElement(Container), domContainer);


7. Button.js 에 아래 내용 입력
import React from "react";

export default function Button(props){
	return React.createElement("button", null, props.label);
}

8. 웹팩을 이용해서 두개의 js파일을 하나로 합치기
"webpack-test"폴더에서 아래명령어 입력
npx webpack

그럼 dist폴더가 생기고 그 안에 main.js가 생김


9. html 화면에 버튼 두개가 나오면 성공

----------------------------------------------------------------------------------------------------

create-react-app

리액트로 웹 어플리케이션을 만들기 위한 환경을 제공함
create-react-app 안에 바벨과 웹펙도 포함되어있음

이외에도 테스트 시스템, HMR(hot-module-replacement), ES6+문법, css후처리 등 거의 필수라고 할 수 있는 개발 환경도 구축해줌
이러한 개발환경을 직접 구축할경우 시간이 오래걸릴 뿐만 아니라 유지보수도 해야함
create-react-app을 이용하면 기존 기능을 개선하거나 새로운 기능을 추가했을때 패키지 버전만 올리면 됨

또 어떤 문제를 해결하기 위한 선택지가 여러 개일 때 create-react-app에서 가장 합리적인 선택을 해줌

-----

쓰는법

create-react-app을 이용한 개발환경 설치

1. 터미널에서 작업폴더 루트로 이동

2. 아래 명령어 입력해서 개발환경 설치
npx create-react-app [폴더명]

ex) npx create-react-app cra-test


2-2. 만약 npm버전이 낮아서 안된다면 아래명령어 입력
npm install -g create-react-app
create-react-app [폴더명]


3. 아래 명령어 입력
cd cra-test
npm start

그럼 웹페이지가 띄워짐. 프로세스종료(ctrl+c)하면 띄워진 웹페이지도 꺼짐


4-1. src폴더 밑에 App.js로 들어간 후 텍스트 수정해보기
Learn React → 리액트

4-2. App.css에서 .App-link의 색상 바꿔보기
color: hotpink;

변경된 내용을 바로 확인할 수 있는것은 HMR이라는 기능 덕분인데, npm start실행시 create-react-app이 로컬서버를 띄워준다
npm start는 개발모드에서 동작하므로 배포할 떄 사용하면 안됨

-----

create-react-app폴더 구조

cra-test
|
|ㅡREADME.md
|
|ㅡnode_modules
|
|ㅡpackage.json
|
|ㅡpublic
|	|
|	|ㅡfavicon;ico
|	|
|	ㅡindex.html
|
ㅡ  src
	|
	|ㅡApp.css
	|
	|ㅡApp.js
	|
	|ㅡApp.test.js
	|
	|ㅡindex.css
	|
	|ㅡindex.js
	|
	|ㅡlogo.svg
	|
	ㅡserviceWorker.js


index.html / index.js / package.json 파일을 제외한 나머지 파일은 데모 앱을 위한 파일이기 때문에 마음대로 수정하거나 삭제해도 됨

index.html에서 참조하는 파일은 public 폴더밑에 있어야함

★public폴더 밑에있는 자바스크립트 파일이나 css파일을 <link>나 <script> 를 이용해서 index.html에 직접 연결하는것보다는
src폴더 밑에서 import 키워드를 써서 연결시키는게 좋음
그래야 js파일이나 css파일의 경우 빌드시 자동으로 압축됨

이미지나 폰트파일도 마찬가지로 src폴더 밑에서 import키워드를 써서 연결시키는게 좋음
웹팩에서 해시값을 이용해서 url을 생성해주기때문에 파일의 내용이 변경되지않으면 브라우저 캐싱효과를 볼 수 있음

-----

주요 명령어

npm start : 개발모드로 프로그램을 실행하는 명령어. 개발모드로 실행하면 HMR이 동작하기 떄문에 코드를 수정하면 화면에 즉시 반영됨
	개발모드에서 코드에 에러가 있을 때는 브라우저에 에러메시지가 출력되는데
	에러미시지가 출력된 영역을 클릭하면 에러가 발생한 파일이 에디터에서 열림

http환경으로 실행하려면 아래 명령어 입력
맥 : HTTPS=true npm start
윈도우 : set HTTPS=true && npm start


npm run build : 배포환경에서 사용할 파일을 만들어줌. 빌드 후 생성된 js파일과 css파일을 열어보면 사람이 읽기 힘든 형식으로 압축돼있음

----------------------------------------------------------------------------------------------------

index.js : html에 리액트컴포넌트를 얹어주는 역할 ( <App /> 으로)

App.js : 시작파일

----------------------------------------------------------------------------------------------------

컴포넌트를 쉽게 만들 수 있도록 단축어를 쓸 수 있는 플러그인

ES7 React/Redux/React-Native snippets

다운후 아래 축약어 이용 가능

rafce : 리액트 컴포넌트 생성


모든 컴포넌트는 반드시 하나의 <div></div> 가 감싸고 있어야함 (하나의 덩어리를 리턴해야함)

----------------------------------------------------------------------------------------------------

import / export

리액트를 태그화(컴포넌트) 시켜서 쓸 수 있음

-----

★export

컴포넌트를 담을 js파일(ex. Box.js)을 만들고
rafce 입력후 자동완성 (export까지 자동으로 완성됨)

export default App; // default는 1개만 가능
export {App2}; // 그 외에는 이렇게

-----

★import

import [태그로 쓸 이름] from "[컴포넌트 경로]"

import "./App.css";
import Box2 from "./componemt/Box";

이러면 return ( ); 안에서 아래처럼 사용 가능
return(
	<div>
		<Box2/>
		<Box2/>
	</div>
);

----------------------------------------------------------------------------------------------------

컴포넌트에서 변수 쓰기 (props)


1. 람다 매개변수에 변수 넣기 (이름 아무거나 상관없음. 그리고 .키 이렇게 쓰기)
const Box = (p) => {
  return (
	<div className="box">
		Box1
		<p>{p.name}</p>
	</div>
  )
}


2. 쓰는곳에서 속성키/값 넣기
<div>
	<Box name="리사"/>
	<Box name="지수"/>


----------------------------------------------------------------------------------------------------

state

react(반응) 는 state에 반응한다 → state가 변하면 ui가 바뀐다


<state를 안썼을 때>

let cnt = 0;

function increaseNum(){
	console.log(cnt);
	cnt++;
}

return (
	<div>
		<div>{cnt}</div>
		<button onClick={increaseNum}>클릭!</button>
	</div>
);

위처럼 변수를 증가시킨 후 console.log()로 찍으면 변화되는 값이 찍히는걸 볼 수 있는데
{} 로 출력을 했을때는, 증가된 변수가 제대로 출력되지않는 현상이 있음


이는 리액트가 DOM을 다시 그리는 비용이 많이 드는 문제때문에,
변수의 값이 바뀌었다고 DOM이 다시 로드되지는 않으며

state값을 바꿔야함


<state 쓰는 방법>

1. useState를 import하기
import {useState} from 'react'

2. state변수를 만들기 위해 useState(초기값) 메소드(리액트 훅)를 씀. (루트함수 안에 넣어야 하며, const로 선언하기)
const [cnt2, setCnt2] = useState(0);

3. set state 를 실행하는 함수 생성
const increaseNum2 = () => {
	setCnt2(cnt2 + 1);
	console.log(cnt2);
}

4. 호출
<div>{cnt2}</div>
<button onClick={increaseNum2}>클릭!</button>


★★★★★★★★★★
state를 set하는 함수는 비동기적으로 실행되어, increaseNum2() 함수의 내용물이 모두 끝난 이후에(콜백함수,setTimeout포함), setState끼리만 따로 모아 실행된다
때문에 세터로 깂을 바꾸고 console.log()를 찍어도 변하기 전의 값이 찍혀있음

★★★★★★★★★★
state가 하나라도 바뀌는 순간(state세터가 실행되는순간) 리랜더링(컴포넌트를 다시 실행. 컴포넌트가 다시 그려짐) 됨
파일에서 제일 바깥에있는 함수가 다시 실행되는것. 이로인해 변수를 초기화하는 코드도 다시 실행된다 (state변수는 초기화X. 유지됨)
잠깐동안만 기억해야 하는게 있으면 state안쓰고 일반 변수 쓰면됨

-----

ex2) 클릭을 했을때 객체의 값을 참조해서 내용이 바뀌게 하기

const choice = {
	rock: {
		name: "rock",
		src: "http://gdimg.gmarket.co.kr/463580244/still/600?ver=1631615157"
	},
	scissors: {
		name: "scissors",
		src: "http://www.kogl.or.kr/upload_recommend/2018/%EC%86%8C%EB%A1%9D%EB%8F%84%EB%B3%91%EC%9B%90/thumb_B004-C001-0003-10_L.jpg"
	},
	paper: {
		name: "paper",
		src: "https://img.freepik.com/free-vector/background-with-a-crumpled-paper-effect_1048-14358.jpg?w=2000"
	}
}

function App() {

	const [userSelect,setUserSelect] = useState(null);

	const pick = (p) => {
		setUserSelect(choice[p]);
		console.log("선택됨",p);
	}

	return (
		<div>
			<div style={{display:"flex"}}>
				<Box name="you" src="" item={userSelect}/> 이런식으로 props를 써서 Box.js에 바뀐 state값을 넘기거나
				<img id="test" src={userSelect && userSelect.src}></img> 현재 컴포넌트에서 쓸 수 있음. 대신 최초에 UI를 그릴때 userSelect는 값이 null(초기값)이므로
										null이 아닐때만 값을 넣기 위해 and(&&) 조건을 걸어서 앞이 true(null이 아닐때 true가 나옴) 일때 뒤에것이 실행되도록 처리를 해줘야함
			</div>
			<button onClick={() => pick("scissors")}>가위</button>
			<button onClick={() => pick("rock")}>바위</button>
			<button onClick={() => pick("paper")}>보</button>
		</div>
  	);
}

----------------------------------------------------------------------------------------------------

JSX 태그 속성


class는 className이라고 써야함

<div className="c1"></div>

-----

JSX 에서는 인라인 스타일을 쓸때


<div style={{display:"flex"}}>

반드시 이렇게 중괄호 2개를 써야하며 문자열 값은 따옴표로 감싸야 함. 속성명은 따옴표 안써도됨


스타일 안에 변수를 넣으려면 아래처럼 쓰기
style={{background:p.color}}
style={{border:"2px solid " + p.color}}

-----

JSX 속성값에서 삼항연산자,탬플릿리터럴(`${}`) 등 쓰기 가능

color={uRslt=="승" ? "red" : uRslt=="패" ? "blue" : "orange"}

-----

함수 선언시

function App() {

	const pick = () => {
		console.log("선택됨");
	}

	return (
		<div>
		.
		.

위처럼 루트 function 안에 써야함

-----

이벤트속성을 쓸때

onClick={}
이렇게 카멜 표기법으로 써야함

-----

이벤트속성에 함수를 넣을때

<button onClick={play}>가위</button>
{함수명} 이렇게 () 없이 넣으면 되고,

파라미터가 들어간 함수를 쓸때는
<button onClick={play("scissors")}>가위</button>
이렇게 쓰면 되는데, 문제는 괄호를 넣으면 처음에 ui를 그릴때 play함수를 실행시켜버린다

그래서 아래처럼 () => 를 앞에 붙여서 써야됨
<button onClick={() => play("scissors")}>가위</button>

----------------------------------------------------------------------------------------------------

객체 만들때는

const choice = {
	rock: {
		name: "rock",
		src: "http://gdimg.gmarket.co.kr/463580244/still/600?ver=1631615157"
	},
	scissors: {
		name: "scissors",
		src: "http://www.kogl.or.kr/upload_recommend/2018/%EC%86%8C%EB%A1%9D%EB%8F%84%EB%B3%91%EC%9B%90/thumb_B004-C001-0003-10_L.jpg"
	},
	paper: {
		name: "paper",
		src: "https://img.freepik.com/free-vector/background-with-a-crumpled-paper-effect_1048-14358.jpg?w=2000"
	}
}

function App() {

위처럼 루트 function 밖에다 써도 됨

----------------------------------------------------------------------------------------------------

useEffect() - 리액트 라이프사이클의 componentDidMount() 처럼 발동함 (랜더 후 바로 실행함)

useEffect는 함수 하나와, 배열 하나를 인수로 받음
useEffect(함수, []);

익명함수를 쓸 경우
useEffect(function(){
},[])

혹은
useEffect(()=>{
},[])


임포트 하기
import {useState,useEffect} from 'react'


ex) 페이지 로드 후 실행되게 (배열에 값을 추가해도 페이지 랜더 후(UI가 그려진 후) 최초1회 실행됨)
useEffect(() => {
	console.log("useEffect1 fire");
},[]);

ex) 특정 state값이 변환될때 마다 실행되게 하려면 배열 안에 state를 넣으면 됨 (변화한 state값을 가져올 수 있음)
useEffect(() => {
	console.log("useEffect2 fire);
	console.log("cnt: " + cnt);
},[cnt]);

ex) 여러개의 state를 트리거 하려면 배열에 더 추가하면됨 (두 state중 하나라도 값이 바뀌면 실행되며, 값 두개가 바뀌었을경우 한번만 실행됨. 두번실행되지않음)
useEffect(() => {
	console.log("useEffect2 fire);
	console.log("cnt: " + cnt);
	console.log("cnt2: " + cnt2);
},[cnt, cnt2]);


제일 최초에는 실행이 안되게끔 하려면
if조건문 추가하기

----------------------------------------------------------------------------------------------------

리액트 부트스트랩 설치

npm install react-bootstrap bootstrap

설치했으면 아래 두가지 방법중 하나로 쓸 수 있음(밑에거 추천)

import Button from 'react-bootstrap/Button';
// or less ideally
import { Button } from 'react-bootstrap';


css 파일도 App.js에 불러오기
import 'bootstrap/dist/css/bootstrap.min.css';


버튼 등 공식문서 사용예시
https://react-bootstrap.github.io/components/buttons/

-----

컨테이너 쓰는법

1. 임포트
import { Container, Row, Col } from 'react-bootstrap';

2. 필요한곳에서 쓰기 (lg속성을 이용해 Col을 12할로 나눌 수 있음)
<Container>
	<Row>
		<Col lg={2}>
			<img src={product?.img}/>
		</Col>
		<Col lg={10}>
			<div>{product?.title}</div>
			<div>{product?.price}</div>
		</Col>
	</Row>
</Container>

----------------------------------------------------------------------------------------------------

옵셔널체이닝을 이용한 조건부 랜더링

<div>{weather && weather.name}</div>
↓↓↓
{weather?.name}

----------------------------------------------------------------------------------------------------

동적으로 배열 개수만큼 JSX 태그 만들기

<Button variant="warning">Paris</Button>
<Button variant="warning">new york</Button>
<Button variant="warning">tokyo</Button>
<Button variant="warning">seoul</Button>
↓↓↓
<App.js>
const cities = ['paris','new york', "tokyo", "seoul"];
.
.
return (
.
.
	<WeatherButton cities={cities}/>

<WeatherButton.js>
return (
.
.
{cities.map((item)=>(
	<Button variant='warning'>{item}</Button>
))}

JSX내에서 자바스크립트 쓸때는 {}(중괄호) 로 감싸야함 

{cities.map((item)=>
	<div>
		<Button variant='warning'>{item}</Button>
		<span>aaa</span>
	</div>
)}
이런식으로 슬 수도 있음


----------------------------------------------------------------------------------------------------

리액트 스피너 (로딩바)
https://www.npmjs.com/package/react-spinners

<설치>
npm install --save react-spinners

<임포트>
import ClipLoader from "react-spinners/ClipLoader";

<쓰고싶은곳에 넣기>
<ClipLoader color={color} loading={loading} cssOverride={override} size={150} />

색깔넣고 cssOverride는 빼도 됨
loading은 true일때는 나오고 false일때는 안나옴


useState를 만들어서 상황에 따라 boolean값 변화시키기

const [loading, setLoading] = useState(false);

setLoading(true); ★
let url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${key}&units=metric`;
let response = await fetch(url);
let data = await response.json();
setWeather(data);
setLoading(false); ★


로딩스피너 true/false 여부에 따라, 로딩이 안끝났을때 UI안보여주기 (3항연산자 이용)

return (
	<div className='container'>
		{
			loading?
				<ClipLoader color="#f88c6b" loading={loading} size={150} />
			:<div>
				<WeatherBox weather={weather} city={city}/>
				<WeatherButton cities={cities} setCity={setCity}/>
			</div>
		}
	</div>
);

----------------------------------------------------------------------------------------------------

리액트 라우터

리액트 라이브러리라는 라이브러리를 이용해서 웹페이지를 여러개를 그려줌
페이지가 하나지만 안에있는 내용을 바꾸면서 페이지가 여러개인것처럼 보이게 할 수 있음


<설치> ★이때 cd명령어로 라우터를 쓸 프로젝트 폴더로 가서 해야함

$ npm install react-router-dom@6


<쓰는법>

① index.js에서 아래 임포트
import { BrowserRouter } from "react-router-dom";

② <App /> 을 <BrowserRouter></BrowserRouter> 로 감싸기 (기존의 <React.StrictMode></React.StrictMode>는 제거)


③ App.js에서 아래 임포트
import { Routes, Route, Link } from "react-router-dom";

이중에서 Link는 아직 안쓸거라 지워도됨


④ <Routes></Routes>로 전체를 감싸고, 각각의 페이지로 쓸 부분들을 <Route path="URL경로" element={컴포넌트}></Route>로 감싼다
Routes는 상황에 맞게 컴포넌트를 스위칭 해주는 역할을 함(이전버전에서는 이름이 스위치였음)


<Routes>
	<Route path="/" element={<Homepage />} />
	<Route path='/about' element={<Aboutpage />} />
</Routes>

path="/"는 path="" 이렇게 해도 됨


아래처럼 <Routes>태그 바깥쪽에 <h1>라우터</h1> 이렇게 쓰면 해당 내용은 모든페이지에 나옴
return (
	<div>
		<h1>라우터</h1>
		<Routes>
			<Route path="" element={<Homepage />} />
			<Route path='/about' element={<Aboutpage />} />
		</Routes>
	</div>
);

-----

Link

라우터끼리 왔다갔다 할 수 있는 기능 (= html a태그 href)

<쓰는법>

① 쓰고싶은곳에서 Link 임포트
import { Link } from "react-router-dom";

② <Link to="이동할URL" />
<Link to="/about">about페이지로 이동</Link>

-----

useNavigate

라우터끼리 왔다갔다 할 수 있는 기능. Link를 안쓰고 버튼으로 이동하고 싶을때 함수에서 쓸 수 있음 (= 자스의 location.href)


<쓰는방법①>

1. 쓰고싶은곳에서 useNavigate 임포트
import { useNavigate } from 'react-router-dom'

2. useNavigate()를 변수에 대입후 함수안에서 쓸 수 있음
const navigate = useNavigate()
const gotoHompage = () => {
	navigate("/");
}
.
.
<button onClick={gotoHompage}>Home으로 이동</button>


<쓰는방법②>

1. 쓰고싶은곳에서 Navigate 임포트
import { Navigate } from 'react-router-dom'

2. 아래처럼 컴포넌트로 바로 쓸 수있음
const PrivateRoute = ({authenticate}) => {
  return authenticate == true ? <ProductDetail/> : <Navigate to="/login"/>;
}

-----

id를 이용해 뒤에 뭐가 붙어도 연결되게 하는법
/products/1 or /products/2 or /products/asd

<Route path='/products/:id' element={<ProductDetailpage />} />

:id 말고 :xxx 이렇게 아무렇게나 해도됨

-----

★useParams - URL 파라미터 받기

① 쓰고싶은곳에서 useParams 임포트
import { useParams } from 'react-router-dom';

② 아래처럼 useParams 작성
const params = useParams();
console.log("param:", params);
return (
.
.

③ 이후 브라우저에서 URL에 파라미터 붙여서 해당페이지 들어가서 콘솔 보기
http://localhost:3000/products/123

param: {xx: '123'}
그러면 위처럼 <Route>에 써놨던 key와 URL로 입력한 파라미터값이 찍혀있는걸 확인할 수 있음
<Route path='/products/:xx' element={<ProductDetailpage/>}/>


이걸 변수로 받으면 아래처럼 되고
const XXX = useParams();
console.log(XXX) → {id: '2'}

중괄호로 묶어서 받으면 벗겨져 값만 빠져나옴 (대신 이때는 라우트에 넣은 키를 넣어야함 <Route path="/abc/:XXX" 에서 XXX )
const {id} = useParams();
console.log(id) → 2

-----

아래처럼 여러개 쓰는것도 가능함

<Route path='/products/:xx/:asd' element={<ProductDetailpage/>}/>
↓↓↓
http://localhost:3000/products/123/aaa
↓↓↓
param: {xx: '123', asd: 'aaa'}

이때는 브라우저에 http://localhost:3000/products/123 이렇게만 입력했을때는 페이지로 연결 안됨

-----

JSX로 화면에 출력하기

const param = useParams();							// 방법①
const {xx} = useParams();							// 방법②
return (
	<div>
		<h1>ProductDetailpage: {param.xx}</h1>		// 방법①
		<h1>ProductDetailpage: {xx}</h1>			// 방법②
	</div>
)

-----

★useSearchParams - 쿼리스트링 값 가져오기

<쓰는법>

① 쓰고싶은 곳에서 useSearchParams 임포트
import { useSearchParams } from 'react-router-dom'

② 쿼리스트링 값 가져오기
let [query, setQuery] = useSearchParams();
console.log("query: ", query.get("id"));
return (
.
.

③ Link 나 useNavigate() 로 URL이동시켜주기 (주소창에 직접 쳐도 무방함)
<Link to="/products?qqq=shirt">product페이지로 이동</Link>

-----

★Navigate - 페이지 리다이랙트 시키기(권한이 없을경우 등)


ex) 로그인을 했을경우 유저페이지를 보여주고 로그인을 안했을경우 로그인페이지를 보여주기

① 임포트하기
import { Navigate } from "react-router-dom";

② useState임의로 만들기 (false=비로그인, true=로그인 이라고 가정)
const [auth,setAuth] = useState(false);

③ 함수 만들기
const PrivateRoute = () => {
	return auth ? <Userpage /> : <Navigate to="/login" />;
}

auth가 true (로그인 한) 상태면 <Userpage /> 컴포넌트를 호출하고, false면 "/login" 으로 보내기


④ "/user" URL에 컴포넌트 넣기
<Route path='/user' element={<PrivateRoute />} />

----------------------------------------------------------------------------------------------------

리액트에서 api요청하려면 항상 useEffect / async / await 써야함

const getProductDetail = async()=>{
	let url = `http://localhost:3333/products/${id}`
	let response = await fetch(url);
	let data = await response.json();
	console.log(data);
}

----------------------------------------------------------------------------------------------------

리액트에서 JSON Server 쓰는법

zero coding으로 가짜 REST API json서버를 쓸 수 있음


json server npm 검색해서 사이트 들어가면 쓰는법이 나와있음

1. 아래 명령어 입력해 json-server 설치 (루트에서 설치하기)
npm install -g json-server

2. json형 데이터가 있는 .json 파일을 만들어서 root에 위치시켜놓기
그러면 호출시 그 데이터가 받아아짐

3. 새로운 터이널을 열고 프로젝트 이동 후 아래 명령어 입력해 json-server 실행 (포트를 변경해서 실행)
json-server --watch [json파일.json] --port 3004

4. 이제 RESTful API를 통해 요청 할 수 있음
{
	"products":[
		{
			"id":0,
			"img":"https://lp2.hm.com/hmgoepprod?set=source[/ec/ef/ecef9d77c56c519e24a76b83331ae2c18f73f50d.jpg],origin[dam],category[],type[LOOKBOOK],res[y],hmver[1]&call=url[file:/product/main]",
			"title":"벨티드 트윌 코트",
			"price":99900,
			"choice":true,
			"new":true,
			"size":["S","M","L"]

		},
		.
		.

위와같은 데이터가 있다고 할때

localhost:3004/products 이렇게 들어가면 전체 데이터가 나오고
localhost:3004/products/2 이렇게 들어가면 id값에 해당하는 정보가 나옴


그럼 아래처럼 async / useEffect로 불러와서 쓸 수 있음
const getProducts = async () => {
	let url = "http://localhost:3004/products";
	let response = await fetch(url);
	let data = await response.json();
	console.log(data);
}
useEffect(() => {
	getProducts();
},[])


useState에 담기
const [productList,setProductList] = useState([]);
const getProducts = async () => {
	let url = "http://localhost:3004/products";
	let response = await fetch(url);
	let data = await response.json();
	setProductList(data);
}


----------------------------------------------------------------------------------------------------

리액트에서 form 태그 쓸때, submit이 동작되면 새로고침이 되어버리므로

form태그의 onsubmit이벤트에 event.prevent를 넣어서 새로고침을 막아야함

button type="submit" 이라고 되어있는 버튼을 눌렀을때 기능을 넣고싶을때도
<button>태그의 click이벤트가 아닌 <form>태그의 onsubmit이벤트로 넣어야함

----------------------------------------------------------------------------------------------------

리액트 프로젝트 배포

-----

json서버 배포하기(My JSON Server가 내 깃허브 레파지토리의 db.json을 읽어서 데이터를 반환해줌)

1. 아래 My JSON Server 사이트 접속 후 설명 참고하기
https://my-json-server.typicode.com/

2. 깃허브에서 레파지토리 생성
추후 해당 레파지토리 안에 db.json파일이 들어가야함


3. 프로젝트에서 json server를 쓰는곳들의 url을 다 바꾸기 (깃허브 레파지토리 생성된페이지 상단에 경로 나와있음)

https://my-json-server.typicode.com/<your-username>/<your-repo>
이떄 <your-username>은 깃허브 이름 넣으면 되고, <your-repo>는 레파지토리 이름 넣으면 됨

http://localhost:3333/products?q=${searchQuery}
↓↓↓
https://my-json-server.typicode.com/imchaewon/shoppingmall/products?q=${searchQuery}


4. 만들어놓은 레파지토리에 프로젝트 올리기 (깃허브 레파지토리 생성된페이지에 명령어 나와 있음)

cd react/shoppingmall/ // 해당 폴더로 들어가기
git init // .git 폴더 생성
git add . // 모든 내용 스테이지에 올리기 (object폴더에 프로젝트내용이 담기고 index파일도 생성됨)
git commit -m "firstcommit" // 커밋 (logs폴더가 생기며 그안에 커밋내역이 생기고 refs폴더에 참조기록이 저장됨. COMMIT_EDITMSG 파일도 생김)
git remote add origin https://github.com/imchaewon/shoppingmall.git // 로컬 프로젝트와 원격 프로젝트의 연결고리 만들기 (config파일에 원격저장소정보가 추가됨)
git push -u origin master // 원격 저장소로 보내기


5. db.json 파일 잘 올라가있는지 확인하기

-----

Netlify 에서 배포하기

1. 아래 사이트 접속
https://netlify.com/

2. github로 회원가입하기

3. import from git 클릭 → GitHub

4. 프로젝트 선택

5. Build command 내용 변경
CI=false npm run build

6. Deploy site 클릭

7. Site deploy in progress 가 나오는걸 확인

8. Production: master@HEAD 클릭


9. 잘 나오는지 확인

7:13:47 PM:  ────────────────────────────────────────────────────────────────
7:13:47 PM:   1. Build command from Netlify app                             
7:13:47 PM: ────────────────────────────────────────────────────────────────

위처럼 안나오고

No url found for submodule path '~~~' in .gitmodules
이렇게 나오면

아래 명령어 입력후 다시해보기
git rm -r 프로젝트명 --cached
git commit -m "clean up folders"
git push


다시 실행시켜서
마지막에 Build script success 잘 나오는거 확인


10. Completed 라고 써있는 목록을 누르기 (lucent-kheer-6d86a6 누르기)
https://lucent-kheer-6d86a6.netlify.app 이런식으로 주소가 나옴

누르기


11. 사이트 잘 나오는지 확인

12. 뭔가 잘안나오고 아래와 같은 오류가 난다면
Uncaught (in promise) SyntaxError: Unexpected token '<', "<!DOCTYPE "... is not valid JSON

13. 도메인 변경하고싶으면
Sites목록 클릭후 Domain settings → Options 버튼 → Edit site name → 도메인 수정

----------------------------------------------------------------------------------------------------

리덕스

state를 중앙집중화 시킬 수 있는 라이브러리

props는 원래 부모컴포넌트에서 자식컴포넌트로만 넘길 수 있어서 props가 많아질경우 구조가 복잡해짐
이를 해결하기 위한 공통으로 쓰이는 state를 저장해두기위한 '저장소'가 Redux 이다

각각의 컴포넌트들이 필요할때 어느 노드에 있던지 저장소에 요청해 값을 받아올 수 있음

		useDisptch
Component	→	Action	→	Reducer	→	Store
	↑									   ↓
	  ←				     ←				←
				     useSelector

★컴포넌트 : 액션을 만듬. (행동 ex. 상품정보 가져와)

★리듀서 : 특별하지 않고 함수임. case가 많은것. 행동지침에 따라서 store를 업데이트함
	ex) 로그인을 할때 액션이 로그인하기를 던지면 리듀서가 그걸 캐치함
	case "로그인하기"
		return {
			id: userId,
			password: userPassword,
			authenticate: true
		}

★스토어 : 단순한 객체. state들을 가지고있다가 리듀서가 값을 바꾸면 바뀜
	스토어의 값이 바뀌면 컴포넌트가 리랜더링됨

★useDispatch : 액션을 보내는 훅
★useSelector : 스토어에 있는 값을 가져올때 씀

-----

설치

redux 및 react redux 설치

프로젝트 폴더로 이동 후
npm install redux@4.1.2 react-redux

-----

App.js에 숫자와 숫자를 올리는 버튼 UI 그려놓기
function App() {
	return (
		<div>
			<h1>{cnt}</h1>
			<button onClick={increment}>증가</button>
		</div>
	);
}

Provider 라는 컴포넌트를 이용해서 리덕스에 store를 넣어야함

1. index.js파일에서 아래 변경 (Provider컴포넌트에 store를 넣어 보냄)
<React.StrictMode>
	<App />
</React.StrictMode>
↓
<Provider store={store}>
	<App />
</Provider>

2. Provider 임포트
import {Provider} from 'react-redux'

3-1. store 만들기
src폴더 안에 폴더 생성 (이름: redux)

3-2. redux 폴더 안에 파일 생성 (이름: store.js)

3-3. store.js 에 내용 추가
import { createStore } from 'redux';

let store = createStore(reducer);


4-1 reducer 만들기
redux폴더안에 폴더 생성 (이름: reduce)

4-2. reduce폴더 안에 파일 생성 (이름: reduce.js)

4-3. 내용 추가
let initialState={
	cnt:0
}

function reducer(state=initialState,action){
}

export default reducer;


5-1. store.js에서 reducer가져오기
import reducer from './reducer/reducer'

5-2. 내보내기
export default store;

6. index.js에서 store가져오기
import store from './redux/store'

7-1. App.js에서 useDispatch 가져오기
import {useDispatch} from 'react-redux'

7-2. dispatch 선언
const dispatch = useDispatch();

8. 쓰고싶은곳에서 dispatch함수 사용 (액션을 보낸것)
const increment = () => {
	dispatch({type:"INCREMENT"})
}

dispatch함수는 인수로 type(필수)과 payload(선택)를 받는데
type은 액션의 이름을 넣기(어떤 동작을 할지)


9. reducer는 자동으로 dispatch가 보낸 액션을 받아올 수 있음
reducer.js에서 콘솔로그 찍어보기

function reducer(state=initialState,action){
	console.log("action: ", action);
}


10. 브라우저에서 버튼 눌러보면 아래 내용이 찍힌것을 확인할 수 있음
action:  {type: 'INCREMENT'}

11. 조건문과 action.type을 이용해 객체 반환
function reducer(state=initialState,action){
	console.log("action: ", action);
	if(action.type === "INCREMENT"){
		return {...state, cnt :state.cnt+1};
	}
	return {...state}
}

...state를 넣은 이유는 다른state들이 있어도 그거랑 상관없이 cnt만 바꿔야 하기때문
let initialState={
	cnt:0,
	asd:0,
	.
	.
}


12-1. App.js에서 사용하기
기존 state 주석
//const [cnt,setCnt] = useState(0);
//setCnt(cnt+1);

12-2. useSelector 임포트
import {useDispatch, useSelector} from 'react-redux'

12-3. 변수에 대입
const cnt = useSelector(state => state.cnt);

useSelector는 함수를 매개변수로 받는데, state를 전부 받아서 cnt속성만 들고옴.
그 값을 cnt로 대입시킴


13. 버튼 누르면 숫자 잘 올라가나 테스트

14. 다른 컴포넌트에서 쓰고싶다면 useSelector만 임포트 하면됨
import React from 'react'
import {useSelector} from 'react-redux'

const Box = () => {

	const cnt = useSelector((state) => state.cnt);

	return (
		<div>this is Box {cnt}</div>
	)
}
export default Box


15. payload는 함수에서 파라미터 같은 것임
App.js에서 내용 수정

dispatch({type:"INCREMENT"})
↓↓↓
dispatch({type:"INCREMENT", payload:{num:5}})

한번에 증가시킬 양을 5씩 증가시키겠다


16. 브라우저에서 버튼클릭해보면 payload도 담겨있는거 확인


17. reducer.js에서 내용 수정

return {...state, cnt: state.cnt + 1};
↓↓↓
return {...state, cnt: state.cnt + action.payload.num};


18. 5씩 증가되는거 확인

------------------------------

복습

1. index.js
import {Provider} from 'react-redux';
import store from './redux/store'

<Provider store={store}>
	<App />
</Provider>


2. store.js
import { createStore } from "redux";
import reducer from './reducer/reducer'

let store = createStore(reducer);

export default store


3. reducer.js
let initialState = {};

function reducer(state=initialState, action){

}

export default reducer


기본 세팅 완료

----------------------------------------------------------------------------------------------------

























