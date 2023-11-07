http://eclipse.org

1. 우측 상단 Download 버튼
2. Download Packages 클릭
3. Eclipse IDE for Enterprise Java Developers Windows x86_64 다운로드

JDK 확인
- C:\Program Files\Java
- C:\Program Files\Java\jdk1.8

http://oracle.com
1. 상단 메뉴 > Products > Software > Java 클릭
2. 맨하단 > Download Java now 클릭
3. Java SE 8 > JDK Download 링크 클릭
4. 테이블 목록 > Windows x64 > jdk-8u281-windows-x64.exe(166.97 MB)
5. 설치

운영체제      JDK      이클립스
32bit      32bit      32bit //오래된 노트북 상황

64bit      32bit      32bit

64bit      64bit      64bit //강의실 상황

64bit      64bit      32bit //권장X


D:\class\client //이전 수업
D:\class\server 폴더 생성

- encoding
  1. Workspaces > UTF-8
  2. CSS Files > UTF-8(맨위)
  3. HTML File > UTF-8(맨위)
  4. JSP File > UTF-8(맨위)

Apache Tomcat
- http://apache.org
- 맨하단 프로젝트 > Tomcat 클릭
- 좌측 Download > Tomcat 8 클릭
- Binary Distributions > 64-bit Windows zip 다운로드
- 압축 해제
- C:\apache-tomcat-8.5.61 이동

이클립스 <-> 아파치 톰캣
- 이클립스 > 환경 설정 > "server" 검색 > Runtime Environments 
> Add > v8.5 > Browse > "C:\apache-tomcat-8.5.61" 선택 > Finish 

이클립스 -> 아파치 톰캣 제어 //인스턴스 등록
- Servers 탭 > 링크 클릭 > v8.5 > next > finish
- 등록된 아파치 8.5를 더블클릭 > Ports > HTTP/1.1 > 8080 -> 8090 변경 > Ctrl + S


프로젝트 생성
1. New > Other > Web > Dynamic Web Project
2. Project name : "ServletTest" 
3. next, next, finish


Dynamic Web Project 구조
1. Deployment Descriptor: 사용X
2. JAX-WS Web Services: 사용X
3. Java Resources(******)
   - 작업할 Java 소스를 관리하는 폴더
   3.1 src > 소스 폴더
   3.2 Labraries > 외부 참조 jar
4. build: 사용X
5. WebContent(******)
   - 작업할 클라이언트 소스를 관리하는 폴더
   - 작업할 서버 소스를 관리하는 폴더
   - 브라우저를 통해서 요청되는 모든 리소스의 루트 폴더
   - *.html, *.css, *.js, 이미지, 동영상 등...
   - *.jsp


----------------------------------------------------------------------------------------------------

f11로 실행할때
1. Run on Server
2. Java Application

두개 있는데 자바 어플리케이션 선택 후
자바로 파일을 만들었으면 왼쪽 Project Explorer탭에서 루트폴더 클릭후 f5 하면 만든 파일이 보임

----------------------------------------------------------------------------------------------------

서블릿(Servlet)

- 자바 진영에서 처음으로 시도한 웹 서버 기술
- Server + Applet

서블릿 클래스(Servlet Class)
- *.jar 참조 → 누가 제공? → Servlet Container가 제공 → Servlet Container는 뭐냐? →
Servlet Container는 서블릿 제작에 필요한 여러가지 환경을 제공하고, 실행에 필요한 환경도 제공하는
제작 + 실행 환경 → "아파치 톰캣"


Apache Tomcat

1. Apache 프로그램
  - 웹 서버 → 웹 서비스를 제공하는 프로그램 → WS
  - 고객(브라우저)의 요청이 들어오면 해당 자원을 찾아서 돌려주는 프로그램

2. Tomcat 프로그램
  - 웹 어플리케이션 서버 → WAS(Web Application Server)
  - 웹 서버측에서 자바를 실행할 수 있는 환경을 제공하는 프로그램

Servlet 작업 규칙
→ Servlet 클래스를 선언해야 한다.
→ 각종 규칙을 지켜서 만들어야 WAS에 의해서 Servlet 클래스가 관리를 받을 수 있다.

1. 서블릿 클래스 선언하기
  a. javax.servlet.Servlet 인터페이스를 구현한다.(복잡함)
  a. javax.servlet.http.HttpServlet 클래스를 상속한다.(간편함) *****선호

2. doGet/doPost 메소드 선언
  - 둘 중 하나 선언 or 둘 다 선언
  - 반드시 1개 이상은 존재해야 한다.
  - 클라이언트(브라우저)의 요청이 들어오면 자동으로 실행되는 메소드
  - "서버에게 브라우저가 페이지를 달라고 요청을 하면 실행되는 메소드"
  - 이 메소드내에서 동적으로 HTML페이지를 만든다.(**********)
  - 메소드 작성 규칙
    a. 매개변수 작성(2개)
      1. javax.servlet.http.HttpServletRequest
      2. javax.servlet.http.HttpServletResponse
    b. 예외 미루기(2개)
      1. java.io.IOException
      2. java.servlet.ServletException

3. 동적 HTML문서 작성 구현
  - HttpServletResponse 객체의 getWriter() 메소드 호출 > PrintWriter 반환
  - PrintWriter 객체의 print~~~(), write() 메소드를 가지고 브라우저에게 돌려줄 HTML소스를 작성한다.
      (아까 Gugudan.java의 FileWriter역할과 동일)

4. 가상 주소 매핑
  - 자바 파일(*.java)은 웹을 통해서 요청/응답할 수 없다.
  - 브라우저가 자바 파일을 호출할 수 있도록 가상 주소를 만들어서 서로 연결한다.
  - WAS(Tomcat)관리 → web.xml(Deployment Descriptor, 배포 서술자)

  - 프로젝트 루트 우클릭 → Java EE Tools → Update EAR Libraries
    WEB-INF 폴더에 web.xml파일이 생김 → 더블클릭해서 열고 Design탭 말고 Source탭 클릭
  - 파일 수정시 반드시 서버를 재시작해야함
  - 브라우저가 부를 수 없는 자바 파일(서블릿)을 부르기 위한 가상 주소를 생성

<servlet>
	<servlet-name>Ex01</servlet-name>
	<servlet-class>com.test.servlet.Ex01</servlet-class>
</servlet>
<servlet-mapping>
	<servlet-name>Ex01</servlet-name>
	<!--
		서블릿 가상 주소는 자유롭게.. 되도록↓
		1. 서블릿 이름과 유사하게
		2. 되도록 소문자
		3. 확장자(~~~.프로젝트/회사키워드 , ~~~.do)
	-->
	<url-pattern>/ex01.do</url-pattern>
</servlet-mapping>

알맞게 바꾸고
이후 재생모양 버튼(Restart the server) 눌러서 서버 재시작
이후 자바파일에서 실행(f11)

----------------------------------------------------------------------------------------------------

빨간줄 오류가 난다 (클래스를 인식하지 못하는 경우)
프로젝트폴더 우클릭 → Build Path → Configure Build Path... → Libraries 탭 →
1. JRE System 라이브러리 있는지 확인(있어도 Remove후 다시 추가)
2. Apache Tomcat 라이브러리 있는지 확인

1번이 없을때(있을때도 마찬가지) 해결법 - Add Library → JRE System Library → Finish
2번이 없을때 해결법 - Add Library → Server Runtime → Next → 8.5 → Finish

----------------------------------------------------------------------------------------------------

URL(가상주소) 바꾸기

서버 더블클릭 Modules탭 → 프로젝트 선택 → Edit... → path를 /server 로 수정 → OK → ctrl+s(저장) → 리스타트(자바파일에서 f11)

----------------------------------------------------------------------------------------------------

############################
	자바파일 견본
############################

package com.test.servlet;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Calendar;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

//1. 서블릿 클래스 선언하기
//a. javax.servlet.http.HttpServlet 클래스를 상속한다.(간편함)
public class Ex01 extends HttpServlet {
//	2.doGet/doPost 메소드 선언
//	a. 매개 변수 작성(2개)
//	  1. javax.servlet.http.HttpServletRequest
//    2. javax.servlet.http.HttpServletResponse
//  b. 예외 미루기(2개)
//    1. java.io.IOException
//    2. java.servlet.ServletException
	public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
		
//		3. 동적 HTML문서 작성 구현
//		- PrintWriter를 사용해서 브라우저에게 돌려줄 HTML소스를 작성한다.
		PrintWriter writer = response.getWriter();
		
		Calendar c = Calendar.getInstance();
		
		writer.println("<html>");
		writer.println("<body>");
		writer.println("<h1>Dynamic Web Page</h1>");
		
		if (c.get(Calendar.HOUR_OF_DAY) < 12) {
			//오전
			writer.printf("%tF AM Hello~",c);
		}else {
			//오후
			writer.printf("%tF AM Bye..",c);
		}
		
		writer.println("</body>");
		writer.println("</html>");
		
		//반드시 스트림을 닫는다.(****) 이 작업이 제대로 실행되지 않으면 브라우저에게 돌려줄 페이지가 완성이 안된다.
		writer.close();
		
//		브라우저가 자바 파일을 요청한 상황
//		- 자바는 웹에서 호출가능한 포맷이 아니다. 불가능하다
//		http://localhost:8090/ServletTest/servlet/com.test.servlet.Ex01
		
		
	}
}

----------------------------------------------------------------------------------------------------

상속받고
dog입력후 ctrl spase

안에 내용 지우고
PrintWriter writer = resp.getWriter();

----------------------------------------------------------------------------------------------------

Servlet → JSP → Servlet + JSP (현재 시점)

수업
1. Servlet(맛보기)
2. JSP(본론) → 서버의 대부분 수업
3. Servlet + JSP 둘의 장점을 살린 서블릿JSP → 15년전 ~ 현재 → 실무적인 수업 → Spring

----------------------------------------------------------------------------------------------------

새프로젝트 > Dynamic Web Project > JSPTest

JSPTest > Java Resources > src > 패키지 생성(com.test.jsp)
생성한 패키지안에 hello.java 생성 후


package com.test.jsp;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

//	1. 서블릿 클래스
public class Hello extends HttpServlet{
	
//	2. doGet/doPost 메소드
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		
		
//		3. 출력
//		- 요청한 브라우저에게 돌려준 페이지 소스를 작성하기(****)
		PrintWriter writer = resp.getWriter();
		
		writer.println("<html>");
		writer.println("<body>");
		writer.println("<h1>Servlet</h1>");
		writer.println("Hello");
		writer.println("</body>");
		writer.println("</html>");
		
		writer.close();
		
	}
	
	
}




JSPTest > WebContent > WEB-INF 생성위해
프로젝트폴더(JSPTest) 우클릭 → Java EE Tools → Generate Deployment Descriptor Stub

생성된 xml들어가서 ctrl + a → ctrl + shift + F 로 탭 정렬 후


<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
	version="3.1">
	<display-name>JSPTest</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
		<welcome-file>index.htm</welcome-file>
		<welcome-file>index.jsp</welcome-file>
		<welcome-file>default.html</welcome-file>
		<welcome-file>default.htm</welcome-file>
		<welcome-file>default.jsp</welcome-file>
	</welcome-file-list>
	
	<servlet>
		<servlet-name>hello</servlet-name>
		<servlet-class>com.test.jsp.Hello</servlet-class>
	</servlet>
	
	<servlet-mapping>
		<servlet-name>hello</servlet-name>
		<url-pattern>/member/hello.do</url-pattern>
	</servlet-mapping>
	
</web-app>

----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------

JSP(Java Server Pages)

- Servlet 다음 버전

서블릿 장점
- 자바 기반(자바의 수많은 기능을 웹 페이지를 제작할때 적용할 수 있다
서블릿 장점
- HTML, CSS, JavaScript 작성이 힘들다(문자열 처리)

JSP 장점
- HTML, CSS, JavaScript 작성이 쉽다
- HTML 기반
JSP 단점
- 자바 작업에 환경이 좀 열약하다(서블릿에 비해)

----------------------------------------------------------------------------------------------------

WebContent > example 폴더 생성
그 안에 new > JSP File > ex01.jsp 생성


<body>
	
	<h1>현재 시간</h1>
	
	<%
		//자바 코드
		Calendar c = Calendar.getInstance();
	
		String time = String.format("%tT",c);
	%>
	
	<div><%=time%></div>
	
</body>


서블릿과 똑같으나 가상 주소 xml파일을 안이용하고도 가능

----------------------------------------------------------------------------------------------------

JSP 주석
<%-- <%=sum(a,b)%> --%>
<%--@ page session="false" --%>

----------------------------------------------------------------------------------------------------

JSP import

<% %> 안에서 import(임포트) 할때 커서를 중간에 두기 보다는 끝에 두고 ctrl+space 하면 더 좋음
Has|hMap → X
HashMap| → O

<%@ page import="com.test.sist.admin2.dto.MemberDTO" %>
<%@ page import="java.util.ArrayList" %>

ctrl+1 또는 ctrl+shift+o 는 jsp파일에서는 불가

----------------------------------------------------------------------------------------------------

JSP 기본 요소
1. JSP 지시자, 지시어, 선언문, JSP Directive
2. 스크립트 요소, Scripting Elements
3. 액션태그, Action Tags

1. JSP 지시자, 지시어, 선언문, JSP Directive)
- <%@ %>
- JSP 페이지를 실행하기 위해 JSP컨테이너(톰캣)에게 해당 JSP를 처리하기 위한 여러가지 환경 설정
- page 지시자
- include 지시자
- taglib 지시자

2. 스크립트 요소(Scripting Elements)
- <% %>
- 자바 구문을 사용할 수 있게 하는 요소(=서블릿과 유사한 환경을 제공)
- Scriptlet
- Expression
- Declaration

3. 액션 태그(Action Tags) = JSTL(JavaServer Pages Standard Tag Library)
- <jsp:~~~> , <c:~~~>
- 프로그래밍 기능이 있는 태그 <c:if> , <c:forEach>
- JSP 기본 액션 태그 → 추가 설정없이 바로 사용 가능
- JSTL 확장 액션 태그 → jstl-1.2.jar 참조 사용 가능 (아파치사이트 → 프로젝트 리스트 → 톰캣있는곳에 jstl도 있음)
- 사용자 커스텀 액션 태그 → 직접 모든 구현 → X

4. 표현 언어 = EL(Expression Language)
- ${변수}
1) ${today} 라고 할 때 jsp엔진을 거치면 page, request, session, context 에서 "today"라는 이름표가 붙은 값을 찾음
2) null 이면 아무것도 출력하지 않고 interpolation 부분을 지워버림
3) null 이 아니면 toString()값을 끼워넣음

----------------------------------------------------------------------------------------------------

1. 지시자

page 지시자
- <%@ page 속성="값" 속성="값" 속성="값" ... %>
- JSP 페이지 상단부에 기재
- 1개 이상 작성이 가능하다.
- 톰캣에게 현재 JSP페이지의 상태를 알려주는 역할

<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" errorPage="error.jsp" %>

ⓐ language="java"
  - JSP페이지에서 사용할 서버 프로그래밍 언어 지정

ⓑ contentType="text/html; charset=UTF-8"
  - JSP 페이지 컨텐츠 기술
  - 현재 페이지는 text/html포맷의 데이터고
  - 문자셋은 UTF-8로 되어있다
  - text/html : MINE타입(파일의 종류를 나타내는 열거형)
  - 톰캣이 UTF-8로 JSP페이지를 읽는다.(***)

ⓒ pageEncoding="UTF-8"
  - 브라우저에게 돌려줄 페이지의 인코딩 방식 지정(***)
  - meta태그의 charset의 인코딩과 똑같아야함

ⓓ errorPage
  - JSP 실행중 에러가 발생하면 보여줄 페이지


include 지시자
- <%@include file="URL"%>
- 특정 JSP(HTML, Text 등) 페이지를 현재 JSP 페이지 일부에 삽입하는 기능
- 조각 페이지 : 한 페이지 이상에서 반복되는 내용을 재사용하는 용도
- <iframe> 유사
- 조각페이지에는 html태그 등 불필요한부분 빼고 필요한부분만 만들어서 사용
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%> 이게 없으면 한글깨짐
오류 나면 톰캣로그보면 contentType="text/html; charset=UTF-8" 를 지우라고 나와있음. include조각파일에 가서 해당 속성 지우기


taglib 지시자
- <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

----------------------------------------------------------------------------------------------------

2. 스크립트 요소

스크립틀릿(Scriptlet)
- <% %>
- 이 영역은 자바 영역이다.
- HTML문서안에 자바 코드를 작성할 수 있게 됨
- 사용 빈도 높음
- 비즈니스 코드 작성(데이터 처리, JDBC, 동적으로 HTML/CSS/JacaScript 조작)

표현식(Expression)
- <%= %>
- 값(상수, 변수, 메소드 반환값 등)
- 해당 위치에 값을 출력한다(HTML소스로 출력).

선언부(Declaration)
- <%! %>
- 해당 JSP페이지에서 사용할 클래스 멤버 변수와 멤버 메소드를 만드는 영역
- 메소드 선언할 때 주로 사용 → 빈도 낮음 → 대체 방법이 따로 있음
- 그 대체방법은 외부 클래스를 만들고

<%@page import="com.test.jsp.Ex04"%>
이렇게 불러온다음

<%=Ex04.sum(m1,m2)%>
이렇게 사용

----------------------------------------------------------------------------------------------------

3. 액션 태그(Action Tags)

JSTL 설정

상단에 아래 내용 추가
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
(uri=까지 치고 ctrl+spase에서 3번째)


<jstl 태그별 용도>

① c(코어) → <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
c:if : 조건문
c:choose c:when c:otherwise : switch case default 조건문
c:forEach : 반복문
c:set : 변수 할당
c:out : 출력 (사용하는 이유는 스크립트실행이나 치환(&)을 하지 않고 사용자가 입력한 문자 그대로를 출력해 XSS공격을 방어하기 위해서이다)

② fn(함수) → <%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/fn" %>
fn:length : 길이 반환
fn:substring : 문자열 자르기
ex) ${fn:substring(item.TAG_LIST,0,15)}

③ fmt(형식) → <%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
fmt:formatDate : 날짜/시간형식변경 (사용법 아래쪽 참조)
formatNumber : 숫자 포맷변경


<c:set var="asd" value="30" /> <!-- JSTL 변수 -->
(위처럼 < />하든가 <c:set var="asd" value="30"></c:set>이렇게 닫든가)
변수 선언 후 (이때 pageContext 또는 session객체의 setAttribute로 넣은것과 동일)

<c:set target="${map}" property="키" value="값" />
맵의 값을 변경

<div>c : ${asd}</div>
el로 접근

★dto객체 EL로 접근
서버에서 보낸것을 받아올때 원래라면
<%@ page import="com.test.sist.admin2.dto.MemberDTO" %> → 먼저 상단에 DTO.java파일을 수동으로 import 시키고
<%
			TextManagerDTO dto = new MemberDTO();
			String phone = ((MemberDTO)request.getAttribute("dto")).getPhone();
%>
위와같이 번거롭게 불러와야하지만

${dto.phone} 이렇게 불러오기 가능함 → dto객체를 또 담은 ArrayList를 jstl로 불러올때는 아래에 있는 forEach 이용할것

★el안에서 dto를 수정가능하다 (통으로 되어있는 전화번호/사업자등록번호 같은거 '-'로 나눌때 쓰기)
${dto.brokerNum.substring(0,2)}

★el안에서 삼항연산자도 쓸 수 있다
${vo.GNDR.equals("M") ? "남자" : "여자"}

★el안에서 문자열 결합시 '+='로 해야함 '+'는 더하기연산만됨

★앞에 0이 들어가면 자바스크립트에서 8진수가 되버리기때문에 꼭 ""(따옴표) 붙이기
★값이 뭔지 확인할때는 jsp파일 맨 꼭대기에(ctrl+home) 넣어볼것

<h2>변수 수정</h2>
<c:set var="c" value="300" />
<div>c : ${c}</div>


<h2>변수 삭제</h2>
<c:remove var="c" />
<div>c : ${empty c}</div>


<h2>조건문</h2> <!-- else if 없음 -->
<c:set var="num" value="-10" />

<c:if test="${num>0}">
	<div>${num}은 양수입니다</div>
</c:if>

<c:if test="${num<0}">
	<div>${num}은 음수입니다</div>
</c:if>


<h2>조건문2</h2>
<c:choose>
	<c:when test="${num > 0}">양수</c:when>
	<c:when test="${num < 0}">음수</c:when>
	<c:otherwise>0</c:otherwise>
</c:choose>


<h2>일반for</h2>
<c:forEach var="i" begin="1" end="10" step="1"> //step생략시 기본값 = 1
	<div>숫자 : ${i}</div>
</c:forEach>


		<h2>향상된for</h2>
<%
		String[] names = {"한가인","이열음","박수진","신세경","아이린"};
		pageContext.setAttribute("name",names);
%>
		<ol>
			<c:forEach items="${name}" var="list">
				<li>${list}</li>
			</c:forEach>
		</ol>

ex) 인스턴스를 담고있는 배열 향상된for로 출력하기
DAO로 만든 ArrayList<~~~DTO> list를 java파일에서 dispatcher.forward로 'list'로 저장해놓은 상태 → 그리고 jsp에서 호출
getter의 문자를 치환해준다 : getXXX → ${dto.XXX}
(이때 getter/setter는 첫번째문자가 소문자고 두번째문자가 대문자면, 첫번째문자를 대문자로 바꾸지 않는다)
<c:forEach items="${list}" var="dto">
<tr>
	<td>
		<input type="checkbox" class="cbDelete" name="cbDelete" value="${dto.seq}">
	</td>
	<td>${dto.sname}(${dto.sid})</td>
	<td>
	<c:if test="${dto.state == 1 or dto.state == 0}">
		<b><a href="/codestudy/member/view.do?seq=${dto.seq}">${dto.content}</a></b>
	</c:if>
	<c:if test="${dto.state == 2}">
		<a href="/codestudy/member/view.do?seq=${dto.seq}">${dto.content}</a>
	</c:if>
	</td>
	<td>${dto.regdate}</td>
</tr>
</c:forEach>


숫자 세자리콤마 포맷 <include 필요>
<fmt:formatNumber value="${price}" pattern="#,###" />

날짜시간 포맷  <include 필요>
<fmt:formatDate value="값"
[type="{time | date | both}"]
[dateStyle="{default | short | medium | long | full}"]
[timeStyle="{default | short | medium | long | full}"]
[pattern="customPattern"]
[timeZone="timeZone"]
[var="varName"]
[scope="{page | request | session | application}"] />

사용자지정 예제↓↓↓
<td><fmt:formatDate value="${vo.regdate}" pattern="yyyy-MM-dd hh:mm:ss" /></td>

----------------------------------------------------------------------------------------------------

EL(Expression Language)
- 표현식 언어
- <%= %> 기능을 대신하기 위해  만들어진 기능
- HTML소스로 출력하는 역할
- ${속성명}
- 일반적인 자바 데이터 출력이 불가능하고, pageContext/request/session/application 객체에 저장된 요소만 출력 가능

입력 : pageContext.setAttribute("abc",20);

출력 : <%=pageContext.getAttribute("abc")%>
↓
${abc}

★연산
pageContext.setAttribute("d",40);
<div>d + 10 = ${d + 10}</div>


HashMap 지원
<h2>HashMap 출력 지원</h2>

<div>이름 : <%=map.get("name")%></div>
<div>나이 : <%=map.get("age")%></div>
<div>직업 : <%=map.get("job")%></div>

<div>이름 : ${map.get("name")}</div>
<div>이름 : ${map.name}</div>
<div>이름 : ${map.["name"]}</div>


★일반 객체 지원
<%
		//자바객체 → 자바빈 or DTO(VO)
		Student s1 = new Student();

		s1.setName("한가인");
		s1.setKor(100);
		s1.setEng(90);
		s1.setMath(80);
		
		request.setAttribute("s1",s1);
		
%>
		<h2>자바 객체 출력 지원</h2>
		
		<div>이름 : <%=s1.getName()%></div>
		<div>평균 : <%=(s1.getKor() + s1.getEng() + s1.getMath()) / 3%></div>
		
		<div>이름 : ${s1.getName()}</div>
		<div>이름 : ${s1.name}</div>
		<div>이름 : ${s1["name"]}</div> <!-- 입력도 가능 -->
		<div>평균 : ${(s1.kor + s1.eng + s1.math) / 3}</div> <!-- 실수형으로 출력됨 -->


★기타
<%
		//EL은 존재하지 않는 key를 사용해도 에러발생X → Null → 아무것도 출력 안함
		String color = "";
		pageContext.setAttribute("color",color);
%>
		<div>${color}</div>
		<div>${pageContext.getAttribute("color")}</div>
		
		<!--
			empty연산자
			- 선언하지 않은 key → true
			- null값 → true
			- ""(빈문자열) → true
			- 값이 존재 → false
		-->
		<div>${empty color}</div>

배열 크기
<div>${list.size()}</div>

배열 접근
<div>${list.get(0)}</div>

============================================================

JSP 내장 객체(JSP Implicit Object

- 개발자가 직접 생성하지 않아도 JSP가 미리 만들어서 제공하는 객체
- 톰캣이 생성한다
- 예약어로 접근한다
- request, response, session, pageContext                 *****
- out, application				***
- config, page, exception			  *

- request, session, pageContext, application
- 내부에 사용자 데이터를 저장할 수 있는 공간을 가지고 있다
- 입출력 : setAttribute(key, value), getAttribute(key)

----------------------------------------------------------------------------------------------------

1. request객체 (요청) ★클라이언트에서 서버로 행동이 이루어지는것

  a. 클라이언트가 서버로 전송한 데이터를 가져오기
    - String text = request.getParameter("text");	→ el로 쓸 시 : ${param.text}
    - String[] cbs = request.getParameterValues("cbs");

    - ex05_form.jsp //사용자가 데이터 입력 + 서버 전송하는 페이지
    - ex05_ok.jsp // 사용자가 보낸 데이터를 수신하는 페이지


  b. 클라이언트가 서버로 전송한 데이터의 인코딩 처리
    - request.setCharacterEncoding("UTF-8");

  c. 클라이언트가 서버로 전송할 때 관련된 정보 가져오기
    ★HTTP요청 메세지 헤더 정보 / 사용자 정보
    - request.getContextPath() : 현재 페이지 URL (/sybang)
    - request.getRequestURI() : 현재 페이지 URL (/sybang/WEB-INF/views/admin2/textManager.jsp)
    - request.getRequestURL() : 전체 경로 (http://localhost:8090/sybang/WEB-INF/views/admin2/textManager.jsp)
    - request.getServletPath() : 파일명 (/WEB-INF/views/admin2/textManager.jsp)
    - request.getServerName() : (localhost)
    - request.getServerPort() : 포트 (8090)
    - request.getQueryString() : 쿼리스트링 (type=spider)
    - request.getRequestURL() + request.getQueryString()  : 쿼리 스트링도 포함한 전체 경로 (http://localhost:8090/sybang/WEB-INF/views/admin2/textManager.jsp)
    - request.getPathInfo() : (null)
    - request.getScheme() : "http" or "https"

    - 변수에 담을때 toString() 붙이기 ★
      String url = request.getRequestURL().toString()


데이터 전송하기 (ex05_form.jsp)

<h2>POST 방식으로 전송하기</h2>
<form method="POST" action="ex05_ok.jsp">
	숫자 : <input type="text" name="num">
	문자 : <input type="text" name="txt">
	<hr>
	<input type="submit" value="전송하기">
</form>

<h2>GET 방식으로 전송하기</h2>


데이터 받기 (ex05_ok.jsp)

<%

// - request.getParameter(String key);
// - key : 태그의 name값

request.setCharacterEncoding("UTF-8");

String num = request.getParameter("num");
String txt = request.getParameter("txt");

%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>데이터 받기</h1>
<div>num : <%=num %></div>
<div>txt : <%=txt %></div>

----------------------------------------------------------------------------------------------------

2. response객체 (응답) ★서버에서 클라이언트로 행동이 이루어지는것

  - HTTP 요청에 대한 응답 정보를 제어하는 객체

  a. 돌려줄 HTML페이지 제작 → response.getWriter() → PrintWriter객체 → HTML페이지 제작 → 브라우저에게 전달
    - 서블릿에서 사용O
    - JSP에서 사용X
  b. 돌려줄 HTML 페이지 인코딩 설정 → response.setCharacterEncoding("UTF-8");
    - 서블릿에서 사용O
    - JSP에서 사용X

  c. 페이지 이동하기
    response객체 : 페이지 이동하기
      1. HTML
        - <a href="URL">
        - 사용자 클릭을 통해서
      2. Javascript
        - location.href = "URL"
        - 자유롭게 프로그램 제어 가능
        - 클라이언트측 제어
        - location.href = "ex09_two.jsp";
      3. Servlet/JSP
        - response.sendRedirect("URL")
        - 자유롭게 프로그램 제어 가능
        - 서버측 제어
        - response.sendRedirect("ex09_two.jsp");
        - 자원을 건넬일이 없을때 사용★ (→하지만 세션안에 저장한것은 살아있다!!)

----------------------------------------------------------------------------------------------------

3. pageContext객체
  - 페이지 실행에 필요한 컨텍스트 정보를 저장한 객체
  - foward() 메소드 : 데이터 전달과 함께 페이지 이동에 사용
  - foward()로 이동될때에 한에서 request , response 가 살아있음

  ⓐ 페이지 이동
    - pageContext.forward(URL)
    - response.sendRedirect(URL)와 비교했을때 pageContext.forward(URL)는 이동하기 전 페이지 url이 있다
    - 서버측 이동(클라이언트를 도착시에만 방문)

  ⓑ 데이터 저장★
      페이지간의 데이터를 이동(전송)할때 사용하는 도구
      - pageContext, request, session, application
      - setAttribute(), getAttribute()


ex)

<이동전 페이지>
자원을 생성함
int num123 = 10;
request.setAttribute("num",num123);

pageContext.forward("ex10_two.jsp");


<이동후 페이지>
<div>num : <%=request.getAttribute("num")%></div>    


----------------------------------------------------------------------------------------------------

4. out객체
  - 응답 페이지 작성을 위한 출력 스트림 개체
  - 서블릿의 PrintWriter객체와 동일한 역할
  - System.out.println() 이 아니고 out.print()임
  - printf는 없음

		<h2>구구단 - 스크립틀릿 + out객체</h2>
<%
		for(int i=1;i<10;i++){
			out.println(String.format("<div>%d * %d = %d</div>",dan,i,dan*i));
		}
%>

----------------------------------------------------------------------------------------------------

5. application객체
  - 애플리케이션 컨텍스트 정보를 저장한 객체
  - 서버와 관련된 몇가지 정보를 제공

<div><%=application.getServerInfo()%></div>
<div><%=application.getContextPath()%></div>
<div><%=application.getServletContextName()%></div> : 프로젝트 이름
<div><%=application.getRealPath("ex11_out.jsp")%></div> : 인자값(상대경로)를 → 로컬 물리 경로 변환
  소스의 실제 실행경로를 돌려주는 메소드
  아파치 톰캣
  - 워크 스페이스에 있는 원본 소스를 직접 실행(사용)하지 않고
    항상 자신이 지정한 특정 폴더에 원본의 복사본을 만들어서 복사본을 실행한다.
  - 대상 : .html , .css , .js , .java , .jsp , 이미지 등 모든 파일


버전 확인법 (서블릿과 JSP는 컨테이너 버전에 따라 달라진다)
<h2>서블릿 버전</h2>
<div><%=application.getMajorVersion()%>.<%=application.getMinorVersion()%></div>

<h2>JSP 버전</h2>
<div><%=JspFactory.getDefaultFactory().getEngineInfo().getSpecificationVersion()%></div>

----------------------------------------------------------------------------------------------------

6. session객체 ★★★★★
  - 클라이언트의 세션 정보를 저장한 객체
  - 데이터 입출력
  - 상태 유지(지속) 기술
  - HttpSession session = request.getSession(); //선언

<%
	//내장객체중 사용자 데이터를 입출력하는 기능을 가진 객체들
	pageContext.setAttribute("num1",100);
	request.setAttribute("num2",200);
	session.setAttribute("num3",300);
	application.setAttribute("num4",400);	
%>

<div>num1 : <%=pageContext.getAttribute("num1")%></div>
<div>num2 : <%=request.getAttribute("num2")%></div>
<div>num3 : <%=session.getAttribute("num3")%></div>
<div>num4 : <%=application.getAttribute("num4")%></div>



현재 페이지를 몇번 방문했는지 카운트 → 누적변수
jsp페이지의 모든 자원은 페이지 소멸(브라우저에게 반환)시 전부 같이 소멸된다
웹이라는 환경은 상태 지속 불가능
→지속 가능 기술 제공

<%
if(session.getAttribute("count") == null){
	session.setAttribute("count",0); //누적 변수 역할
}
session.setAttribute("count",(int)session.getAttribute("count") + 1);
%>

<div>num : <%=session.getAttribute("count")%></div>


http:// 프로토콜의 성격
클라이언트에서 서버에게 페이지를 요청하면 페이지를 돌려주고,
(이때 세션 객체를 같이 돌려주는데, 세션에는 30분이라는 타이머가 걸려있다)
그때 클라이언트는 캐시에 복사를 한 후 서버와 물리적 연결을 끊는다(단절)
결국 보고있는 페이지는 서버에있는게 아닌 하드디스크에 저장된 페이지며(웹서버에 접속중이 아님)
때문에 랜선을 빼도, 개발자가 페이지를 수정해도, 페이지를 새로고침해서
서버로 재요청을 하지않는이상 페이지가 유지된다
(재요청을 하면 세션타이머가 다시 30분으로 초기화되는데, 만약 요청을 안하고 사이트를 나갔거나 아무짓도 안하고 시간이 지나면
세션 타이머가 끝나면서 소멸되고, 이 세션 객체가 소멸되면 서버는 사용자가 사이트에서 나간걸 확인 가능 → 오차 범위는 발생)
네이버에 접속하고 몇일뒤에 다시 접속을 했을때, 별로 달라진것이 없다면
하드디스크에 저장되어 있는 자원을 사용하고 바뀐 부분만 바꾼다 → 네트워크 트래픽 감소, 속도 증가

로그인을 한 후 아무것도 안하고 있다가 새로고침을 하는경우 로그아웃이 되는게 이 이유임

타이머 = 세션 만료 시간 (조절 가능)
이걸 늘리게 되면 서버쪽 메모리점유율이↑ (안좋다)
그리고 보안위험도 높아짐 (pc방 등에서 로그인을 했을때)

브라우저를 다 닫으면 다른 사람으로 인식 → 세션이 날라감

세션 : 서버기술
쿠키 : 클라이언트 기술 (javascript제어)


세션 컨트롤

<%=session.setAttribute("data",100);%> : 세션 값 넣기
<%=session.removeAttribute("data");%> : 세션 값 삭제
<%=session.invalidate();%> : 세션 객체 초기화 → 기존의 세션 정보를 모두 삭제하고 새걸로 교환 (신중하게)
<%=session.setMaxInactiveInterval(30);%> : 세션 타이머 변경 (특별한 업무가 아닌 이상 잘 수정 안함)


세션 정보

Session ID : <%=session.getId()%> : 내부 식별자 , 개발자는 이 값이 바꼈나 안바꼈나 체크용으로 사용
Session Creation Time : <%=session.getCreationTime()%> : 세션이 만들어진 처음 시간
Session Max Inactive Interval : <%=session.getMaxInactiveInterval()%> : 세션 초기화 타이머(초)
Session isNew : <%=session.isNew()%> : 세션이 처음 만들어진건지 확인 , 지속적으로 접속 중인지 체크용
Session Data : <%=session.getAttribute("data")%>


특정페이지에서만 세션 끄기
<%@ page session="false" %>

----------------------------------------------------------------------------------------------------

pageContext , request , session , application
  - 데이터 저장 기능 제공

pageContext : 페이지가 오청될때 태어나고 페이지가 이동되면 죽음
request : 페이지가 요청될때 태어나고 페이지가 이동되면 죽는데, sendredirect()는 페이지가 이동하면 이동되면 또 태어났다가 죽음
pageContext.foward() : 페이지가 요청될때 태어나고 페이지가 이동되도 살아있음
session : 개인 공간, 이미 태어나 있고 페이지가 이동되도 살아있음
application : 공용 공간, 첫 사용자가 방문했을때 생성, 수명이 훨씬 길다 (창을 닫거나 브라우저가 바뀌어도 살아있음)
	마지막 손님이 나갈때 죽음

수명이 길다고 좋은것은 아니다 (자원이 필요없는 페이지에서도 살아있기때문에)

============================================================

폼태그의 내용을 전송하는 방법

form.action 속성
- 데이터를 수신할 서버측의 프로그램 주소(URL)
- 서버측 프로그래밍 언어로 작성된 프로그램의 주소가 온다

form.method 속성
- 데이터를 전달하는 방식(클라이언트가 서버에게 자원을 요청하는 방식)
1. GET
    - http://localhost:8090/ClientTest/ex18_ok.jsp?name=임채원&age=23
    - http://localhost:8090/ClientTest/ex18_ok.jsp?name=%EC%9E%84%EC%B1%84%EC%9B%90&age=23
    - 데이터를 전송할 URL뒤에 붙여서 보내는 방식
    - URL(256자 제한) → GET방식으로 보내는 데이터가 짤릴 위험이 있다.
    - 소량의 데이터만 전송하는 방식
    - 한글 사용X → 영단어 or 숫자 정도만 전송하는 용도로 사용
    - URL?이름=값&이름=값&이름=값
                ↑물음표 이후 데이터를 쿼리 스트링(Query String) 이라고 부름 ★공백사용금지
    - (보안성이 필요없으면서 and 북마크 하면 좋은 페이지)는 post말고 get방식 사용하면 북마크시 쿼리스트링이 같이 저장되서 좋음★★★

2. POST
    - http://localhost:8090/ClientTest/ex18_ok.jsp
    - 데이터를 상자안에 담아서 보내는 방식
    - 전송하는 데이터가 노출이 안된다. (하지만 완전히 안보이는것은 아니기때문에 암호화 필요)
    - 전송하는 데이터의 크기에 제한이 없다.
    - form태그로 보낼때는 거의 POST방식 이용한다고 생각



★a태그로 전송 (=get방식과 동일)
  - form태그 없이 데이터를 전송할 수 있음
  - 용도에 맞게 선택해서 사용

<a href="ex05_ok.jsp?num=123&txt=han&txt2=java">ex05_ok.jsp페이지로 이동하기</a>



★자바스크립트로 전송 (=get방식과 동일)

<script type="text/javascript">
	document.getElementById("btn1").onclick = function(){
		location.href = "ex05_ok.jsp?num=111&txt=버튼&txt2=클릭함";
	}
</script>

----------------------------------------------------------------------------------------------------

Context Root Path(컨텍스트루트패스)

WebContent 폴더 내에서 적은 /aaa/가 ~WebContent/로 됨
(http://localhost:8090/jsp/hello.jsp 에서 http://localhost:8090/jsp/ 까지가 Context Root Path)

jsp에서는 루트(/)가 http://localhost:8090/
java(서블릿)에서는 루트(/)가 webContent

jsp에서는 상대경로(' ')가 현재 jsp파일이 위치한 폴더
혹은
서블릿 가상주소 action="config_site_ok.do"


설정법

서버 더블클릭 → Modules탭 → 프로젝트 선택 → edit... → path를 /JSPTest에서 /jsp로 변경 → ctrl+s

그리고 경로를 href="/jsp/example/css/bootstrap.css 이렇게 하면
/jsp가 WebContent폴더로 됨

원래프로젝트이름으로 돌아가는경우가 가끔 있다고 함
그러면 에러가나는데 주소창을 유심히 보다가 다시 설정

----------------------------------------------------------------------------------------------------

전송한 데이터의 인코딩 처리

request.setCharacterEncoding("UTF-8"); 이걸 안넣었을때

- 클라이언트가 전송한 데이터가 항상 깨지는 것이 아니다
- GET 안깨짐 , POST 깨짐
- 웹서버(Apache Tomcat) → 7.0 이전까지는 EUC-KR사용 → 8.0이후부터 UTF-8 사용
- POST로 전송하면서, 한글이 들어갈 때만 위 코드를 사용하기

jsp문서로 alert 돌려줄때 한글 안깨지게
response.setContentType("text/html; charset=UTF-8");

jsp문서로 한글 돌려줄때 안깨지게
resp.setCharacterEncoding("UTF-8");
PrintWriter writer = resp.getWriter();
writer.print("<html><head><meta charset='utf-8'></head><body>");
writer.print("<script>");
writer.print("location.href='/codestudy/ajax/ex01.do?name=" + name + "';");
writer.print("</script>");
writer.print("</body></html>");
writer.close();

----------------------------------------------------------------------------------------------------

getParameter(String key)
- key값의 컨트롤이 존재하면서 + 값을 입력하면 → 입력값 반환
- key값의 컨트롤이 존재하면서 + 값을 입력안하면 → 빈 문자열 반환
- key값의 컨트롤이 존재안하면 → null 반환

ex06_ok.jsp? → null
ex06_ok.jsp?txt1= → ""
ex06_ok.jsp?txt3= → null (txt3이란 name이 form태그내에 없으면)

----------------------------------------------------------------------------------------------------

textarea의 엔터값을 넘기면 스페이스로 바뀜

그럴때는 아래와 같이 br로 바꾸는 처리

String txt3 = request.getParameter("txt3");

txt3 = txt3.replace("\r\n","<br>");

----------------------------------------------------------------------------------------------------

input checkbox에 value를 안넣으면?

1. value가 없을때
  - 체크O → "on" 반환(예약어)
  - 체크X → null 반환
2. value가 있을때
  - 체크O → value 반환
  - 체크X → null 반환


select → option에 value를 안넣으면?

<select id="selBuseo">
	<option>부서를 선택하세요</option>
	<c:forEach items="${list}" var="buseo">
		<option value="${buseo}">${buseo}</option>
	</c:forEach>
</select>

★ 위 예시에서 option에 부서가 없는 경우 텍스트(부서를 선택하세요)가 반환된다 → value="" 이렇게 빈문자열 넣어놓기

----------------------------------------------------------------------------------------------------

다중값 배열로 받을때

<h2>체크박스들</h2>
<input type="checkbox" name="cbs" value="red"> 빨강<br>
<input type="checkbox" name="cbs" value="yellow"> 노랑<br>
<input type="checkbox" name="cbs" value="blue"> 파랑


그후 ok페이지에서

String cb2 = request.getParameter("cb2"); → 단일값 반환
String[] cbs = request.getParameterValues("cbs"); → 다중값 반환

이렇게 선언 후
아래처럼 출력

<%
			for(int i=0;i<cbs.length;i++){
%>
			<div><%=cbs[i]%></div>			
<%
			}
%>

----------------------------------------------------------------------------------------------------

라디오 / 셀렉트박스는 name은 같은이름을 여러개사용하지만
넘어가는 값은 1개이므로

getParameterValues 로 안하고 getParameter로 넘기기

----------------------------------------------------------------------------------------------------

HTTP요청 메세지 헤더 정보

<table border="1">
		<tr>
			<th>헤더명</th>
			<td>헤더값</td>
		</tr>
		
<%
		//localhost:8090
		System.out.println(request.getHeader("host"));
	
		//request.getHeader("key (=headerName)")
		Enumeration<String> e = request.getHeaderNames();
	
		while(e.hasMoreElements()){
			String name = e.nextElement(); //headerName
%>
		<tr>
			<th><%=name %></th>
			<td><%=request.getHeader(name) %></td>
		</tr>	
<%
		}
%>

----------------------------------------------------------------------------------------------------

사용자 정보

<p>서버 도메인명 : <%=request.getServerName()%></p> 
<p>서버 포트번호 : <%=request.getServerPort()%></p> 
<p>요청 URL : <%=request.getRequestURL()%></p> 
<p>요청 쿼리 : <%=request.getQueryString()%></p> 
<p>클라이언트 호스트 : <%=request.getRemoteHost()%></p> 
<p>클라이언트IP : <%=request.getRemoteAddr()%></p> 
<p>프로토콜 : <%=request.getProtocol()%></p> 
<p>요청 방식 : <%=request.getMethod()%></p> 
<p>컨텍스트 루트 경로 : <%=request.getContextPath()%></p> 


form태그를 통해 post를 사용한것만 post방식이고 나머지는 전부 get방식이다 (둘다 같이 사용 사능)
컨텍스트루트경로 = 이클립스 서버더블클릭 → 모듈 → 에디트에서 path값

----------------------------------------------------------------------------------------------------

웹프로젝트에서 jar파일 가져오는법

로컬 파일탐색기에서 jar파일 복사
WebContent → WEB-INF → lib폴더선택 → 붙여넣기

----------------------------------------------------------------------------------------------------

JSTL(JavaServer Pages Standard Tag Library)
- JSP에서 <% %>을 대신하기 위해 만들어진 기능

<c:if test=""></c:if>
<c:forEach items=""></c:forEach>

EL + JSTL 사용하면 JSP페이지에서 순수 자바 표현이 사용될 일이 없어진다

----------------------------------------------------------------------------------------------------

스토리보드 만드는 툴

1. 파워포인트
2. 발사믹 https://balsamiq.com/
3. 오븐 https://ovenapp.io/

----------------------------------------------------------------------------------------------------

DBUtil.java파일 넣는 경로

프로젝트폴더 → Java Resources → src → 패키지 폴더 ex)com.test.address → DBUtil.java

아래부터는 파일 내용
↓↓↓↓↓

package com.test.address;

import java.sql.Connection;
import java.sql.DriverManager;

//자바의 주석
//1. 단일 라인 주석
/*
 2. 다중 라인 주석 
 */
/**
 3. 자바 도큐먼트 주석
 */


//javadoc.exe - 도큐먼트 생성 도구


/**
 * DBUtil. 데이터베이스 연결 클래스입니다.
 * @author 홍길동
 */
public class DBUtil {

	private static Connection conn;
	
	/**
	 * 데이터 베이스 연결 메소드입니다.
	 * @return 연결된 Connection 객체를 반환합니다.
	 */
	public static Connection open() {
		
		//java.sql.SQLException: 부적합한 Oracle URL이 지정되었습니다
		
		//java.sql.SQLRecoverableException: IO 오류: The Network Adapter could not establish the connection
		//java.net.ConnectException: Connection timed out: connect
		
		//java.sql.SQLException: Listener refused the connection with the following error:
		//ORA-12505, TNS:listener does not currently know of SID given in connect descriptor
		String url = "jdbc:oracle:thin:@localhost:1521:xe"; 
		
		//java.sql.SQLException: ORA-01017: invalid username/password; logon denied
		String id = "hr";
		String pw = "java1234";
		
		try {

			//java.lang.ClassNotFoundException: oracle.jdbc.driver.OracleaDriver
			Class.forName("oracle.jdbc.driver.OracleDriver");
			
			conn = DriverManager.getConnection(url, id, pw);
						
			return conn;

		} catch (Exception e) {
			System.out.println("DBUtil.open()");
			e.printStackTrace();
		}
		
		return null;
		
	}
	
	
	/**
	 * 데이터 베이스 연결 메소드입니다.
	 * @param server 접속할 서버 주소입니다.
	 * @param id 접속할 계정명입니다.
	 * @param pw 접속할 비밀번호입니다.
	 * @return 연결된 Connection 객체를 반환합니다.
	 */
	public static Connection open(String server, String id, String pw) {
		
		String url = "jdbc:oracle:thin:@" + server + ":1521:xe";
		
		try {

			Class.forName("oracle.jdbc.driver.OracleDriver");
			
			conn = DriverManager.getConnection(url, id, pw);
			
			return conn;

		} catch (Exception e) {
			System.out.println("DBUtil.open()");
			e.printStackTrace();
		}
		
		return null;
		
	}
	
}


넣고 include

<%@ page import="com.test.address.DBUtil" %>

----------------------------------------------------------------------------------------------------

form태그 submit 방식로 넘기는데 자바변수를 같이 넘기려면

	<input type="hidden" name="seq" value="<%=seq%>">
</form>

이런식으로 form태그 안에다 넣어서 같이 넘긴다 (★주의 name값 빠지면 안됨)
★항상 hidden태그를 사용할때는 개발자도구에서 값이 잘 들어갔는지 확인할것

----------------------------------------------------------------------------------------------------

form태그 하나로 여러 기능을 수행하도록 만들기

<form method="post" name="Frm">
	<input type="hidden" name="mode">

위처럼 hidden속성 추가후 스크립트에서 누른 버튼에 따라 value를 바꿔서 commit()으로 전송
form.action 으로 보낼 주소도 설정 가능함

function submitChk() {
	var f = document.Frm;
	var objItem;

	if (checkEmpty(f.name)) {
		alert("성명을 입력해 주세요.");
		f.name.focus();
		return false;
	}

	for (i=1; i<=3; i++) {
		objItem = eval("f.mobile"+i);
		if (checkEmpty(objItem)) {
			alert("휴대폰번호를 입력해 주세요.");
			objItem.focus();
			return false;
		}
	}

	if (checkEmpty(f.addr)) {
		alert("주소를 입력해 주세요.");
		f.post.focus();
		return false;
	}

	if (confirm("등록하시겠습니까?")) {
		f.mode.value = "EDIT";
		f.action = "member_regOk.do";
		f.submit();
	}
}

function del() {
	var f = document.Frm;
	if (confirm("선택하신 회원을 삭제하시겠습니까?")) {
		f.mode.value = "DEL";
		f.action = "member_regOk.do";
		f.submit();
	}
}

----------------------------------------------------------------------------------------------------

★DB를 갔다 오는데에 비용이 가장많이 듦으로

재사용할수 있는 데이터는 페이지로 계속 넘겨서 사용할것

----------------------------------------------------------------------------------------------------

파일(이미지) 업로드 (사전에 cos.jar 다운 필요)

★보내는 페이지

1. 반드시 <form> 사용
2. method="POST" 사용
3. <form enctype=""> 지정
  - application/x-www-form-urlencoded : 문자열만 전송(기본값)
  - multipart/form-data : 문자열 + 비문자열 전송

<form method="POST" action="ex19_file_ok.jsp" enctype="multipart/form-data">

	<div class="well">
		<strong>문자열 : </strong>
		<input type="text" name="txt">
	</div>
	
	<div class="well">
		<strong>파일 : </strong>
		<input type="file" name="attach">
	</div>
	
	<div>
		<input type="submit" value="보내기" class="btn btn-default">
	</div>

</form>


★가져오는 페이지(_ok.jsp)

문자열 → request.getParameter()
파일 → X → 외부 라이브러리 사용 → cos.jar → MultipartRequest 사용

프로젝트폴더 → WebContent → 작업폴더 → WEB-INF → lib → cos.jar파일 넣어놓기
프로젝트폴더 → WebContent → 작업폴더 → files폴더 만들어놓기

MultipartRequest 클래스(객체)
- request 기능을 그대로 구현
- 파일 업로드 기능 추가 구현

이걸 안쓰고 불가능한이유)
<form enctype="multipart/form-data"> 이 속성을 추가하면
→ request.getParameter() 메소드 동작이 불가★★★★★

//인코딩 설정
request.setCharacterEncoding("UTF-8");

주소를 실제 실행 파일로 지정해야함
	→ 이때 java.lang.IllegalArgumentException: Not a directory 오류가 뜨면 이클립스에서 해당 폴더안에 뭐라도 아무파일한개 넣어놓기
String path = application.getRealPath("/example/files");
System.out.println(path);

path → D:\서버\.metadata\.plugins\org.eclipse.wst.server.core\tmp1\wtpwebapps\JSPTest\example\files

업로드 파일의 최대크기 저장(제한)
- 바이트 단위로 지정가능
int size = 1024 * 1024 * 100; //100메가

변수 선언
String txt = ""; //텍스트 입력값
String filename = ""; //첨부파일명
String orgfilename = ""; //첨부파일명

try{
	//MultipartRequest객체 생성
	MultipartRequest multi = new MultipartRequest(
								request, //원래 request
								req.getRealPath("/pic"), //업로드 위치
								1024 * 1024 * 10, //최대 크기
								"UTF-8", //인코딩 지정
								new DefaultFileRenamePolicy() //파일명 관리 삭제
							);
	System.out.println(req.getRealPath("/pic"));

	//첨부파일명 → 첨부파일을 안눌렀으면? null or "";
	System.out.println(multi.getFilesystemName("pic"));
	pic = multi.getFilesystemName("pic") != null?
	multi.getFilesystemName("pic") : "nopic.png";

	//텍스트 가져오기
	txt = multi.getParameter("txt");

	//파일정보(파일명,기존파일명) 가져오기
	filename = multi.getFilesystemName("attach");
	orgfilename = multi.getOriginalFileName("attach");

}catch(Exception e){
	System.out.println(e);
}


<div class="well">
	<strong>문자열 : </strong>
	<%=txt%>
</div>
<div class="well">
	<strong>파일명 : </strong>
	<%=filename%>
</div>
<div class="well">
	<strong>파일명 : </strong>
	<%=orgfilename%>
</div>


다 했으면 파일 보내고 파일탐색기 주소창에
D:\서버\.metadata\.plugins\org.eclipse.wst.server.core\tmp1\wtpwebapps\JSPTest\example\files
붙여넣고 엔터 누르면 저장된 폴더로 감

----------------------------------------------------------------------------------------------------

파일 업로드(내용추가)

1. 전송할 form태그에 enctype="multipart/form-data" 속성추가 (이걸 안하면 오류는 안나는데 파일전송이 안된다)
	★★★ 이거 추가하면 서버에서 받을때 req.getParameter로 받으려하면 오류난다
	subject = multi.getParameter("subject"); → multi객체로 받아야함

2. 파일을 받아서 저장할 폴더 먼저 WebContent안에 만들기 & 경로 입력 아래 예제에선 "/files"

String filename = "";
String orgfilename = "";
HashMap<String,String> map = new HashMap<String,String>(); //DTO로 구현해도 됨
String filename = "";
String orgfilename = "";
try {
	
	MultipartRequest multi = new MultipartRequest(
		req,
		req.getRealPath("/files/admin2"),
		1024 * 1024 * 100,
		"UTF-8",
		new DefaultFileRenamePolicy()
	);
	System.out.println("path : " + req.getRealPath("/files/admin2"));

	map.put("filename",multi.getFilesystemName("imgURL"));//폼안에 있는 <input type=file>의 name
	map.put("orgfilename",multi.getOriginalFileName("attach"));//같은 이름의 원래있던 파일을 어떻게 할지 처리할때
	map.put("type",multi.getParameter("type"));
	map.put("seq",multi.getParameter("seq"));
	map.put("subject",multi.getParameter("subject"));
	map.put("content",multi.getParameter("content"));
	
} catch (Exception e) {
	System.out.println("TextManager_reg_ok.doPost()");
	e.printStackTrace();
}

System.out.println("filename : " + filename);
System.out.println("orgfilename : " + orgfilename);

TextManagerDAO dao = new TextManagerDAO();

result = dao.add(map);


3. RealPath로 콘솔에 찍은 경로 복사후 파일탐색기에서 주소창에 붙여넣어 들어가보고 이미지가 잘 받아졌나 확인

4. 이제 dto나 map으로 다른 데이터랑 같이 묶어서 dao로 보내 추가쿼리실행

----------------------------------------------------------------------------------------------------

파일 다운로드

1.
<a href="/jsp/example/files/<%=filename%>"><%=filename%></a>
이런식으로 할경우 파일이 열려버림

2.
<a href="/jsp/example/files/<%=filename%>" download><%=filename%></a>
a태그에 download 속성 넣기 → 최신버전 브라우저만 지원(옛날브라우저는 여전히 열려버림)

3. 아래를 download.jsp로 저장해놓고
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import="java.net.URLEncoder"%>
<%@ page import="java.io.File"%>
<%@ page import="java.io.*"%>

<%
	String fileName = request.getParameter("filename");
	String orgfileName = request.getParameter("orgfilename");

	String savePath = "example/files";
	ServletContext context = getServletContext();
	String sDownloadPath = context.getRealPath(savePath);


	String sFilePath = sDownloadPath + "/" + fileName;
	byte b[] = new byte[4096];
	FileInputStream in = new FileInputStream(sFilePath);
	String sMimeType = getServletContext().getMimeType(sFilePath);
	System.out.println("sMimeType>>>" + sMimeType);

	if (sMimeType == null)
		sMimeType = "application/octet-stream";//브라우저 반환 MIME
		//text/html
		//image/gif
		//application/zip

	response.setContentType(sMimeType);
	String agent = request.getHeader("User-Agent");
	boolean ieBrowser = (agent.indexOf("MSIE") > -1) || (agent.indexOf("Trident") > -1);

	if (ieBrowser) {
		fileName = URLEncoder.encode(fileName, "UTF-8").replaceAll("/+", "%20");
	} else {
		fileName = new String(fileName.getBytes("UTF-8"), "iso-8859-1");
	}

	response.setHeader("Content-Disposition", "attachment; filename= " + orgfileName);

	ServletOutputStream out2 = response.getOutputStream();
	int numRead;

	while ((numRead = in.read(b, 0, b.length)) != -1) {
		out2.write(b, 0, numRead);
	}
	out2.flush();
	out2.close();
	in.close();
%>

저장했으면

<a href="/jsp/example/download.jsp?filename=<%=filename%>&orgfilename=<%=orgfilename%>"><%=orgfilename%></a>

이런식으로 사용 (구버전도 지원)

----------------------------------------------------------------------------------------------------

이미지 뷰어(보기)

<c:if test="${dto.imgURL.toLowerCase().endsWith('jpg') || dto.imgURL.toLowerCase().endsWith('gif') || dto.imgURL.toLowerCase().endsWith('png') }">
	<img src="/sybang/files/admin2/${dto.imgURL}">
</c:if>


다운로드

<span class="glyphicon glyphicon-floppy-disk"></span> 
<a href="/codestudy/board/download.do?filename=${dto.filename}&orgfilename=${dto.orgfilename}&seq=${dto.seq}">${dto.orgfilename}</a>
[download: ${dto.downloadcount}회]

----------------------------------------------------------------------------------------------------

1. JSP Model 1
2. JSP Model 2 → MVC

Servlet → JSP → Servlet + JSP = MVC 구현

a. 패키지 생성
  - com.test.mvc
  - com.test.mvc → Hello.java 파일 생성

b. JSP 생성
  - WebContent → hello.jsp 파일 생성
  - WebContent → WEB-INF → view 폴더 생성
  - WebContent → WEB-INF → view → hi.jsp 파일 생성

c. 프로젝트 우클릭 → EE Tools → Generate Depolyment Descriptor 생성

----------------------------------------------------------------------------------------------------

서블릿할때 오류 나면 console창 보기

"서블릿 매핑에서 유효하지 않은 <url-pattern>" 이렇게 나오면 web.xml 잘못

----------------------------------------------------------------------------------------------------

서블릿 + JSP → Model2 → MVC

//1.브라우저의 요청을 받는 첫번째 알바생
public class Ex01 extends HttpServlet{ //Controller(비즈니스 구현 + 순서 제어)
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

		//담당 업무 구현 → 비즈니스 코드 구현
		//컵 준비 + 얼음 담기
		
		String cup = "얼음이 담긴 컵";
		
//		JSP 호출
		req.setAttribute("cup",cup); //Model(데이터 관련 업무)
		
//		pageContext.foward(); → 이것과 똑같은 역할을 하는 다른 도구 제공
		RequestDispatcher dispather = req.getRequestDispatcher("/hello.jsp");
		dispather.forward(req,resp);
		
		
	}
}

받을때는 jsp파일에서

<!-- jsp파일 → View(출력 업무) -->
<div><%=request.getAttribute("cup")%></div>

sendRedirect는 주소창에 이동한 페이지의 주소가 남고
위처럼 foward는 주소창에 이동하기 전 페이지의 주소가 남아있다

----------------------------------------------------------------------------------------------------

WEB-INF 폴더

WEB-INF는 브라우저에서 직접 접근(요청)할 수 없음 → private
주소를 직접 입력해서는 접근 불가

jsp파일을 바로 실행하는 실수할 일을 없애기 위해
View(보여지는)역할을 하는 페이지를 WEB-INF 폴더 밑에다 넣는다

----------------------------------------------------------------------------------------------------

war파일(압축폴더) 가져오기

import → Web → WAR file → war찾기 → Next

----------------------------------------------------------------------------------------------------

서블릿할때 web.xml에서 연결 안하고
@WebServlet("/index.do")
public class Index extends HttpServlet {

이렇게 연결가능

그리고 주소창에 뒤의 경로를 직접 입력해야함 http://localhost:8090/codestudy/index.do

----------------------------------------------------------------------------------------------------

버전

v1.2.3 - 해당하는 자리에 1씩 올림
- 1 : major version
	- 이사이트가 맞나 싶을정도로 바뀌었을때
	- ex)Model1 → Model2 개편
- 2 : minor version
	- 디자인이 바뀌었거나 했을때, 이전버전과 호환성이 유지될때
	- ex)차트 기능 추가
	- ex)회원검색 기능 추가
- 3 : error version
	- 작은 에러 수정등

----------------------------------------------------------------------------------------------------

jsp에서 서블릿(자바)을 import 할때 (조각페이지)

<%
	out.flush();
	RequestDispatcher dheader = request.getRequestDispatcher("/inc/header.do");
	dheader.include(request, response);
%>

----------------------------------------------------------------------------------------------------

폼 전송시 암호확인 체크

//폼이 전송되기 바로 직전에 발생하는 이벤트
$("#form1").submit(function(evt){
	//암호 , 암호확인이 일치하는지?
	if($("#pw").val() != $("#cpw").val()){
		alert("암호가 일치하지 않습니다.");

		//폼 전송을 취소
		//evt 는 window.event
		evt.preventDefault(); //발생한 이벤트의 동작을 없던일로
		return false; //발생한 이벤트의  동작을 없던일로
	}
});

----------------------------------------------------------------------------------------------------

jsp페이지 안만들거면 아래 안넣어도됨

RequestDispatcher dispatcher = req.getRequestDispatcher("/WEB-INF/views/board/writeok.jsp");
		dispatcher.forward(req, resp);

----------------------------------------------------------------------------------------------------

검색할때는 상태 유지를 위해서

form method="GET" 으로 만듦

----------------------------------------------------------------------------------------------------

404에러

- url확인 →
	1. form태그 action 경로에 / (슬래시 안붙이면 이렇게됨)
	2. java파일 가상주소에 / (슬래시 안붙이면 이렇게됨)

- 경로와 실제 파일명이 다를 경우★

- 경로 대소문자 다른지 확인 (java 가상주소경로, jsp경로) ★

- 서버에 해당 프로젝트 모듈 추가되어있는지 확인

- 추가되있다면 서버 컨텍스트루트패스가 바뀌었는지 확인★ (서버를 삭제했다 다시 만들었거나 어떤 이유로 갑자기 초기화될수있다)

- 자바페이지 새로만들고 서버 재시작 안했을때

- jsp로 실행했는지 url 확인

- 이클립스에서 파일명 바꿨을 경우 발생하기도함
	1. Project탭 → Clean
	2. 안되면 파일 새이름으로 하나 복사한다음 경로/주소 수정하고★ 그페이지는 열리나 확인

- 위의 모든 사항을 확인해봤는데도 이상이 없다면... 5분간 기다렸다가 컨텍스트 루트패스 봐 보기(딴걸로 바뀌어있을수있음)

----------------------------------------------------------------------------------------------------

405에러

GET요청 → doGet O
Post요청 → doPost O
GET요청 → doPost X (405에러)
Post요청 → doGet X (405에러)

----------------------------------------------------------------------------------------------------

500에러 - 페이지에 오류 내용 혹은 이클립스 콘솔창 잘 읽어보기

- 파일이름 대/소문자만 변경했을때
	이럴때는 Project → Clean... 혹은 파일 내용 복사후 지웠다가 다시 만들기

- OracleServiceXE / OracleXETNSListener 실행중인지 확인

- 세션 종료되어 로그인 풀렸나 확인

- 오라클 개인용 1gb 초과시 발생(1분정도 기다리면 되는 경우 있음)

- el 사용시 클래스틀림/없는DTO속성넣었는지 확인 ex) ${sdto.representative} 라고 써야되는걸 ${adto.representative} 라고 썼을때
  → 이경우는 어디서틀렸는지 웹에 나옴
  → 만일 해당페이지 DTO에 없는 다른 DTO속성을
	→ 같은페이지의 다른 쿼리스트링(?type=normal)인 상태 때문에 넣어야한다면
		ex) 아이디가 어느 테이블에는 있고 어느 테이블에는 없을때 ( ${dto.id} )
	1) <c:if test=>로 → 그 다른 쿼리스트링일때만 나오게 분기처리하거나
	2) 해당 dto에
		① 그냥 빈 필드를 만들거나 (→ 이경우 내용이 null이다),
		② 대체할수있는것이면(email을 아이디로 쓴다던지 하면) 마찬가지로 id필드를 만들고 email값 집어넣기
			→ dto.setId(rs.getString("email")); 이런식으로?

- 페이지에 빨간밑줄 오류가 있는지 확인

----------------------------------------------------------------------------------------------------

503 에러

기다렸다가 새로고침

----------------------------------------------------------------------------------------------------

505에러

서버는 켜졌는데 페이지가 안열릴때
서비스에서 oracleXE, Listener 켜져있는지 확인

----------------------------------------------------------------------------------------------------

실행했는데 사이트에 연결할수 없음 & 서버가 죽었는데 다시 안켜질때

1. 작업관리자→세부정보에서 javaw.exe 작업끝내기 ★★★

2. 같은 포트 쓰고있는게 있는지 확인
cmd에서 다음과 같이 포트를 사용하고 있는 pid를 확인하여 강제 종료 시켜준다.
> netstat -a -n -o -p tcp

포트를 사용중인 pid가 4444 일경우
> taskkill /f /pid 4444

해당 프로세스가 종료되었다. 다시 포트를 확인해본다.
> netstat -a -n -o -p tcp
없어졌나 확인후 서버 연결

3. @WebServlet("") 이름 겹친것 확인 ★이경우는 에러메세지가 어디 겹쳤다고 뜬다 (서버를 지웠다가 깔았는데 안된다면 이문제)
web.xml에서 같은 이름 사용으로 충돌이 났거나,
다른 곳에서 같은 이름의 @WebServlet("") 가상 주소를 사용하고있는지 확인
(Servers → 서버더블클릭 → Modules탭 → 동일한 Path를 사용하려고 할때도 바로 오류남)

4. Servers에서 Delete후 다시 추가

5. 서버 아예 지웠다가 다시 추가
Window → Preference → Server → Runtime Environments 에서 톰캣 서버 지우고 다시 추가 (8.5)

----------------------------------------------------------------------------------------------------

jsp페이지들 첫줄에 <%에 빨간밑줄(The superclass "javax.servlet.http.HttpServlet" was not found on the Java Build Path),
java파일 @WebServlet, HttpServlet, HttpServletRequest 등에 빨간밑줄 (WebServlet cannot be resolved to a type)

프로젝트 우클릭 → Properties → Project Facets → Java → Runtimes탭 → Apache Tomcat v8.5 체크 → Apply and Close

----------------------------------------------------------------------------------------------------

css/제이쿼리가 연결안되어있을때

Servers탭 → Modules → Path가 틀렸을 수 있음 (path를 틀리면 절대경로로 설정한것들이 import가 안됨.
path를 설정했다면 설정한 path가 루트가 되므로 path를 asd라고 했으면 브라우저에서도 localhost:8080/asd/ 까지가 기본경로임)

----------------------------------------------------------------------------------------------------

특정 영역에만 아무것도 안뜰때

★★★★★일단 이클립스 콘솔창 열어서 잘 읽어보기 
	→ 기능 위임 파일(DAO) 안에서 오류일 가능성 99퍼 (OutOfBoundsException 등)

----------------------------------------------------------------------------------------------------

★★★★★★★★★★★★★★★★★★★★
페이지 내에서 어떤건 잘나오고 어떤건 안나올때

1. 복사 붙여넣기 하고 안 고친게 있는지 (이전께 남아있는게 있는지) 꼮 확인할것 (setAttribute 등)

이걸 확인하지 않고 그냥 넘어가면 나중에 에러도 안나고 되긴 되는데 이상하게 일부만 안되는 현상 발생
→ 이때 이걸 찾느라 sout 일일이 하나하나 찍어보고 시간이 엄청 소요될 수 있음

2. 이클립스 콘솔 오류 메세지 잘 보기

→ jps페이지에서 dto안에 없는 속성을 el로 가져온경우 그부분 이후부터 쫙 안나옴
ex) ${dto.address} → ${dto.addddd} 

----------------------------------------------------------------------------------------------------

부적합한 열 인덱스/이름 (DB불러오는 부분에서 발생)

1. String sql = " " ← 여기서 테이블명을 다른 테이블을 가져왔거나,
2. dto.setSeq(rs.getString("address")); ← 테이블에 없는 컬럼을 가져오려고 했을때

논리 오류 방지 ★★★★★★★★★★★★★★★★★★★★
반드시 String sql = "" 에 넣기전에  먼저 sqlDeveloper에서 확인해보고, 그 결과가 내가 원하는 값이 맞는지 확인
	- insert/update/delete문은 sqldeveloper에서 실제 테스트 할거면 commit필수
	- 다른 테이블명을 가져왔거나, 조인쿼리를 잘못 했는지 확인必

※ 논리 오류는 사용자가 의도한 작업을 프로그램에서 수행하지 못하는 오류이다
코드는 오류 없이 컴파일 및 실행될 수 있지만 작업 결과가 의도된 바와 다를 수 있다
작성자가 예상한 알고리즘 등이 틀렸다는 것을 나타내는데,
따라서 에러 메세지가 따로 나타나지 않아 오류를 교정하는 것이 어렵다

----------------------------------------------------------------------------------------------------

결과 집합을 모두 소모했음

resultSet을 if 또는 while로 안묶었을때 발생

----------------------------------------------------------------------------------------------------

인용부호가 요구됩니다.

따옴표("")로 묶어야 할걸 안묶었을때 발생

----------------------------------------------------------------------------------------------------

★★★
쿼리스트링을 받아와야하는데 자꾸 null이 나올때
페이지가 다른페이지로 이동되서 쿼리스트링이 빠졌는지 확인

쿼리 스트링 값이 이상할때
?key=value&key=value 를
?key=value?key=value 이렇게 오타낸경우

----------------------------------------------------------------------------------------------------

dto로 보낸게 el로 안나올때

올바른 예) ${dto.address}

1. 달러를 빠뜨렸거나 → {address} → 문자 그대로 출력됨
2. dto안에 없는 속성을 썼거나 → ${dto.adddddd} → 이렇게 쓴 부분 이후부터 쫙 안나옴
3. 앞에 dto를 안썼거나(없는 변수를 쓴경우) → ${address} → null이 출력된다.

----------------------------------------------------------------------------------------------------

콘솔에 오류도 안나는데 값이 안나올때 or 예상과 다른 결과가 나올때

1. if문을 사용한적이 있나요?
	→ 문자열 비교를 equals()메소드로 안하고 ==연산자로 했는지 확인
	→ null 인지 빈문자열인지 먼저 체크하기

2. 제이쿼리로 태그를 선택한적이 있나요?
	→ 태그명,따옴표("),선택자(#.) 확인

3. sql = ""로 데이터를 select한적이 있나요?
	→ where조건에 맞는 값이 아무것도 없어서 안나오는것
	(만약 조인쿼리로 했다면 inner join / outer join 사용 구분 잘 하기)

4. sql =""로 데이터를 update/delete한적이 있나요?
	→ where 조건이 이상하지 않은지, pstat를썻다면 ?값이 올바르게 들어갔는지 자세히 살펴보기 (0개의 행 업데이트)

----------------------------------------------------------------------------------------------------

특정 부분에 내용이 안나오고 오류메세지는 다음과 같을때
java.lang.StringIndexOutOfBoundsException: String index out of range: 

ex) db내용 받는 while문에서 substring을 사용한경우 내용중 일부레코드가 값의길이가 다를때 발생
	→ 정해놓은형식(글자수,한글/영문/숫자)에 안맞는 데이터를 사용자가 저장할수 없도록 유효성검사 필수

----------------------------------------------------------------------------------------------------

새로고침하고 서버를 끊었다가 연결해도 반영이 안되는 경우 → 기다려야함

----------------------------------------------------------------------------------------------------

jsp는 빨간밑줄이 그어졌지만 에러가 아닌경우가 종종 있음

----------------------------------------------------------------------------------------------------

빈값 체크시 null도 아니고 빈문자열("") 도 아닐때

아래 중 하나
	.equals("null")
	.equals("")

----------------------------------------------------------------------------------------------------

jdbc 여러 테이블을 한방에 불러올때

1. 조인쿼리로 하는 방법
	*를 안쓰고, 컬럼 하나하나 적은다음 중복되는 컬럼은 별칭(as) 붙여서 가져오기
	→ dto.setSeq(rs.getString("bseq"));
2. view로 하는 방법
	→ 오라클에서 view만들고 jsbc로 그 view를 불러오기

----------------------------------------------------------------------------------------------------

이클립스로 서버 내용을 수정을 했을때 .java파일은 서버를 한번 실행시키면 반영되고
.jsp파일은 그냥 저장만 하고 웹페이지에서 새로고침하면된다

----------------------------------------------------------------------------------------------------

input 이름 다 똑같이 → 가독성, spring에서 필요

1. <input name="이름" id=""
2. 테이블의 컬럼명
3. dto의 멤버변수명

----------------------------------------------------------------------------------------------------

페이징

=====
.java
		int nowPage = 0;		//현재 페이지 번호
		int totalCount = 0;		//총 게시물 수
		int pageSize = 10;		//한페이지 당 출력 개수
		int totalPage = 0;		//총 페이지 수
		int begin = 0;			//rnum 시작 번호
		int end = 0;			//rnum 끝 번호
		int n = 0;				//페이지바 관련 변수
		int loop = 0;			//페이지바 관련 변수
		int blockSize = 10;		//페이지바 관련 변수
		
		
		//list.do
		//list.do -> list.do?page=1
		//list.do -> list.do?page=2
		
		String page = req.getParameter("page");
		
		if (page == null || page == "") {
			//기본 -> page = 1
			nowPage = 1;
		} else {
			nowPage = Integer.parseInt(page);
		}
		
		//nowPage -> 현재 보려는 페이지 번호
		//1page -> where rnum between 1 and 10
		//2page -> where rnum between 11 and 20
		//3page -> where rnum between 21 and 30
		
		begin = ((nowPage - 1) * pageSize) + 1;
		end = begin + pageSize - 1;
		
		map.put("begin", begin + "");
		map.put("end", end + "");
		
		
		Member_listDAO dao = new Member_listDAO();
		
		if (t.equals("normal") || t.equals("null")) { //회원메뉴
			req.setAttribute("member_tName","회원");
			req.setAttribute("member_t","N");
			
			list = dao.getMemberInfo(map);
			int cnt = dao.getMemberCnt();
			
			req.setAttribute("list",list);
			req.setAttribute("cnt",cnt);
			
		}else if (t.equals("broker")) { //중개사메뉴
			req.setAttribute("member_tName","중개사");
			req.setAttribute("member_t","B");
			
			ArrayList<BrokerDTO> list2 = new ArrayList<BrokerDTO>();
			
			
		}else if (t.equals("firm")) { //업체메뉴
			req.setAttribute("member_tName","업체");
			req.setAttribute("member_t","F");
			
			ArrayList<FirmDTO> list2 = new ArrayList<FirmDTO>();
			
		}
		
		
		totalCount = (int) req.getAttribute("cnt"); //총 게시물 수
		System.out.println(totalCount); //274개
		
		totalPage = (int)Math.ceil((double)totalCount / pageSize); //총 페이지 수
		System.out.println(totalPage); //27페이지면 -> 28페이지
		
		String pagebar = "";
		
		loop = 1;
		n = ((nowPage - 1) / blockSize) * blockSize + 1;
		
		//이전 10페이지
		if (n == 1) {
			pagebar += String.format("<li class='disabled'>"
					+ "            <a href=\"#!\" aria-label=\"Previous\">"
					+ "                <span aria-hidden=\"true\">&laquo;</span>"
					+ "            </a>"
					+ "        </li>");
		} else {				
			pagebar += String.format("<li>"
					+ "            <a href=\"/sybang/admin2/member_list.do?page=%d\" aria-label=\"Previous\">"
					+ "                <span aria-hidden=\"true\">&laquo;</span>"
					+ "            </a>"
					+ "        </li>", n - 1);
		}
		
		
		
		while (!(loop > blockSize || n > totalPage)) {
			
			if (nowPage == n) {
				pagebar += "<li class='active'>";
			} else {
				pagebar += "<li>";
			}
			
			pagebar += String.format("<a href=\"/sybang/admin2/member_list.do?page=%d\">%d</a></li>", n, n);
			
			loop++;
			n++;
		}
		
		
		//다음 10페이지로 이동
		if (n > totalPage) {
			pagebar += String.format("<li class='disabled'>"
					+ "            <a href=\"#!\" aria-label=\"Next\">"
					+ "                <span aria-hidden=\"true\">&raquo;</span>"
					+ "            </a>"
					+ "        </li>");
		} else {
			pagebar += String.format("<li>"
					+ "            <a href=\"/sybang/admin2/member_list.do?page=%d\" aria-label=\"Next\">"
					+ "                <span aria-hidden=\"true\">&raquo;</span>"
					+ "            </a>"
					+ "        </li>", n);
		}
		
		//2.
		req.setAttribute("list", list);
		req.setAttribute("pagebar", pagebar);
		req.setAttribute("nowPage", nowPage);
		
		
		
		
		RequestDispatcher dispatcher = req.getRequestDispatcher("/WEB-INF/views/admin2/member_list.jsp");
		dispatcher.forward(req, resp);

=====
DAO.java
		public ArrayList<MemberDTO> getMemberInfo(HashMap<String,String> map) {
		
		try {
			ArrayList<MemberDTO> list = new ArrayList<MemberDTO>();
			
			String sql = "select * from (select m.*, rownum as rnum from tblMember m where delFlag != 1) where rnum between ? and ? order by rnum desc";
			
			pstat = conn.prepareStatement(sql);
			pstat.setString(1,map.get("begin"));
			pstat.setString(2,map.get("end"));
			
			rs = pstat.executeQuery();

			while (rs.next()) {
				MemberDTO dto = new MemberDTO();
				
				dto.setSeq(rs.getString("seq"));
				dto.setEmail(rs.getString("email"));		

				list.add(dto);
				
			}
			
			return list;

=====
.jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

	<table class="admin_style_02">
		<tr align="center">
			<!-- 회원타입 N:일반, B:중개사, F:업체 -->
			<th width="20%">ID<c:if test="${member_t != 'F'}">(이메일)</c:if></th>
			<c:if test="${member_t == 'B'}">
			<th width="15%">사업자대표명</th>
			</c:if>
			<c:if test="${member_t == 'N'}">
			<th width="10%">이름</th>
			<th width="10%">성별</th>
			<th width="10%">나이</th>
			</c:if>
			<c:if test="${member_t == 'F'}"><th width="20%">이메일</th></c:if>
			<c:if test="${member_t != 'N'}">
			<th width="20%">승인여부</th>
			<th width="20%">승인일자</th>
			</c:if>
			<th width="15%">연락처</th>
			<!-- <th width="7%">접속수</th>
			<th width="13%">최근 접속일</th>
			<th width="13%">가입일</th> -->
			<th width="20%">관리</th>
		</tr>
		<c:forEach items="${list}" var="dto">
		<tr>
			<td>${dto.id}</td> <!-- 아이디 -->
			<c:if test="${member_t != 'F'}"><td>${dto.name}</td></c:if> <!-- 이름 -->
			<c:if test="${member_t == 'F'}"><td>${dto.email}</td></c:if> <!-- 이메일 -->
			<c:if test="${member_t == 'N'}">
			<td>${dto.gender}</td> <!-- 성별 -->
			<td>${dto.age}</td> <!-- 나이 -->
			</c:if>
			<c:if test="${member_t != 'N'}">
			<td>미승인</td> <!-- 승인여부 -->
			<td>2021-02-01</td> <!-- 승인일자 -->
			</c:if>
			<td>${dto.phone}</td> <!-- 연락처 -->
			<td align="center"><span class="btn btn-primary btn-xs" onclick="userInfo()">회원정보</span></td>
		</tr>
		</c:forEach>
	</table>

	<nav class="pagebar">
		<ul class="pagination">
			${pagebar}
		</ul>
	</nav>

----------------------------------------------------------------------------------------------------

계층형 게시판 (=답변형 게시판)
- thread, dtpth 컬럼 추가
1. 새글 쓰기
    a. 게시물 중 가장 큰 thread를 찾아서 그 값에 +1000 한 값을 새글의 thread값으로 사용한다.(단,첫번째 글은 이전 글이 존재하지 않기 때문에 일단 1000을 넣는다.)
    b. 새글의 depth는 무조건 0을 넣는다.
2. 답변글 쓰기
    a. 게시물의 모든 thread값 중 답변들의 부모글 thread값보다 작고, 이전 새글의 thread값보다 큰 글들을 모두 찾아서 thread - 1 업데이터 한다.
    b. 답변글의 thread값은 부모글의 thread - 1을 넣는다.
    c. 답변글의 depth값은 부모글의 depth + 1을 넣는다.

----------------------------------------------------------------------------------------------------

jsp파일로 치환코드가능한 css파일

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page contentType="text/css" %>

<%
	String siteColor1 = "#486BB8";
%>

----------------------------------------------------------------------------------------------------

서블릿에서 세션에 접근해 로그인 구현

@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) → post방식으로 받는다

String id = req.getParameter("id");
String pw = req.getParameter("pw");

MemberDAO dao = new MemberDAO();
MemberDTO dto = new MemberDTO();

dto.setId(id);
dto.setPw(pw);

int result = dao.login(dto); //1 or 0

-----
이부분은 login() 메소드를 만든 DAO파일
sql = "select count(*) as cnt from tblMember where id = ? and pw = ?"; → sql문에서 카운트를 시켜
if (rs.next()) {
	return rs.getInt("cnt"); //1 또는 0 인 반환값을 넘긴다
}
-----

이후 반환값이 1인경우 로그인 성공, 그렇지않다면 실패로 나누고

if (result == 1) {
	HttpSession session = req.getSession(); → 사이트에 머무르는 동안 유지되도록 세션을 만든다
	session.setAttribute("id", dto.getId()); → 그리고 '인증을받았다는 티켓' 역할을 하는 값으로 아이디를 넣는다

	이후부분은 사이트 전역에 계속 들고 다녀야 하는 정보가 있으면 세션에 추가하는 것
	MemberDTO rdto = dao.getMember(id);

	session.setAttribute("name",rdto.getName());
	session.setAttribute("pic",rdto.getPic());
	session.setAttribute("regdate",rdto.getRegdate());
	session.setAttribute("seq",rdto.getSeq());
	session.setAttribute("email",rdto.getEmail());

	모두 마쳤다면 메인으로 페이지 이동
	resp.sendRedirect("/codestudy/index.do");
}else{
	로그인 실패시
	PrintWriter writer = resp.getWriter();

	writer.print("<html><body>");
	writer.print("<script>");
	writer.print("alert('failed');");
	writer.print("history.back();");
	writer.print("</script>");
	writer.print("</body></html>");
			
	writer.close();
}

----------------------------------------------------------------------------------------------------

ArrayList 에 담겨있는 DTO 조작

for (BoardDTO dto : list) {
	
	//날짜에서 시간 잘라내기
	dto.setRegdate(dto.getRegdate().substring(0, 10));
	
	//제목이 너무 길면 자르기
//			if (dto.getSubject().length() > 34) {
//				dto.setSubject(dto.getSubject().substring(0, 34) + "..");
//			}
	
}

----------------------------------------------------------------------------------------------------

웹클라이언트(브라우저) ↔ [통신] ↔ 웹서버

1. iframe 사용 + 타이머(선택)
2. Ajax
3. WebSocket

	<script type="text/javascript">
		const url = "ws://echo.websocket.org";
		let ws;
		
		$("#btn1").click(function(){
			
			/* 웹소켓 → 서버와 통신
			1. 소켓 생성
			2. 서버 접속
			3. 통신(데이터 주고 받기)
			4. 서버 접속 종료 */
			
//			1 + 2
			ws = new WebSocket(url);
			
//			3. 비동기 사건 → 이벤트 구현 + 콜백

//			서버와 연결되는 순간 발생
			ws.onopen = function(evt){
				console.log("서버와 연결되었습니다.");
				ws.send("Hello"); //나 → 서버
			};

//			서버가 나에게 메시지를 보내는 순간 발생
//			서버 -> 나
			ws.onmessage = function(evt){
				console.log("서버에서 클라이언트에게 메세지를 전달했습니다.")
				console.log(evt.data);
				
//				소켓 연결 종료
				ws.close();
			};

//			서버와 연결이 종료되는 순간 발생
			ws.onclose = function(evt){
				console.log("서버와 연결이 끊겼습니다.");
			};

//			에러가 발생할때 발생
			ws.onerror = function(evt){
				console.log("error",evt.data, "color:tomato");
			};
			
		});
	</script>

----------------------------------------------------------------------------------------------------

//webSocket 서버
// - Endpoint(중단점) : 네트워크 통신에서 상대방의 주소
@ServerEndpoint("/chatserver")
public class Ex03Server {
	
	//현재 서버에 접속한 클라이언트의 WebSocket Session 목록
	private static ArrayList<Session> list = new ArrayList<Session>();

	@OnOpen
	public void handleOpen(Session userSession) {
		
		//클라이언트 연결 요청 + 접속
		System.out.println("클라이언트 접속 성공");
		
		//if (list.size() < 2) {
			list.add(userSession); //접속자 관리
		//} else {
			//userSession.getBasicRemote().sendText("유저가 꽉찼습니다.");
		//}
		
		//System.out.println(list); //덤프
		
		for (Session session : list) {
			//목록내에서 현재 접속한 사람이 아닌 사람 -> 나 빼고 나머지
			if (session != userSession) {
				
				try {
					
					//해당 세션에 연결된 클라이언트에게 메시지를 전달한다.
					session.getBasicRemote().sendText("다른 유저가 접속했습니다.");
					
				} catch (Exception e) {
					System.out.println(e);
				}
				
			}
		}
		
	}
	
	@OnClose
	public void handleClose(Session userSession) {
		
		System.out.println("클라이언트 접속 해제");
		
		//접속을 끊은 유저는 세션 리스트에서 제거
		list.remove(userSession);		
	}

	@OnError
	public void handleError(Throwable t) {
		t.printStackTrace();
	}
	
	@OnMessage
	public String handleMessage(String message, Session userSession) {
		
		//클라이언트 -> 서버 -> 다른 클라이언트
		
		//강아지#안녕하세요.
		int index = message.indexOf("#");
		
		String user = message.substring(0, index);
		String txt = message.substring(index + 1);
		
		for (Session session : list) {
			if (session != userSession) {
				try {
					session.getBasicRemote().sendText(message);
				} catch (Exception e) {
					System.out.println(e);
				}
			}
		}
		
		
		return null;
	}
	
}

----------------------------------------------------------------------------------------------------

Ajax(Asynchronous JavaScript and XML) Asynchronous : 비동기

- 비동기 자바스크립트 & XML
- 비동기 자바스크립트 통신
- 비동기 통신 + 자바스크립트 기반(소켓)
- 자바스크립트를 사용해서 브라우저와 웹 서버 간의 데이터를 주고 받는 기술
- 서버와 통신할 때 XML형식으로 데이터를 주고 받는다
- 서버와 통신할 때 JSON형식으로 데이터를 주고 받는다
- JSON > XML

Ajax 특징(장점) or WebSocket
개발비용, 가볍게 : Ajax < WebSocket
업무범위, 유지보수 : Ajax < WebSocket
1. 깜빡임 없이(페이지 새로고침 없이) 서버와 데이터를 주고받을 수 있다 → 50점
2. 최소한의 데이터만 서버와 주고받을 수 있다 → 100점
	- 네이버 검색어 자동입력, 회원가입시 아이디 중복검사, 맵(지도) 구현 등

new XMLHttpRequest() ← 소켓의 한종류 :: ★Ajax
→ 이것을 랩핑해놓은것... jquery Ajax

아작스와 서버의 통신 관계 3가지 경우
Ajax → 데이터 → Server
Ajax → Server → 데이터 → Ajax
Ajax → 데이터 → Server → 데이터 → 데이터


사용법

$().fn() → 특정 태그에 종속된 함수
$.fn() → 전역 함수 (누구에게도 종속되지 않는..)
$.ajax();

ajax() → 이것도 가능은하지만 알아보기힘들어서 안쓴다.


$.ajax({
	type:"POST", //필수:: 요청 메소드(GET or Post → 판단기준 : 데이터가 큰지 / 작은지)
	url:"/codestudy/ajax/ex02data.do", //필수:: 응답 프로그램 주소(acrion)
	data:"aa=aaa&bb=bbb",
		// 문자열(text)로 보내기 (쿼리스트링형)
		// VO객체나 String으로 받을 수 있다
		// 데이터를 한개 보낼때 key=를 안넣으면 자동으로 append돼서 asd= 이렇게 보내진다 →  replace로 없애거나 json객체로보내기
		// 쿼리스트링 형식에서 벗어난 기호는 유니코드로 치환되어 보내진다 (',' → %2C / '=' → %3D)
		// 스프링 컨트롤러에서 받으려면 받을 파라미터에 @RequestBody 필요
		// ★VO객체로 받으려면 VO파라미터에 @RequestBody 빼야함 (안할시 ajax415에러)
		// ★VO객체로 받으려면 contentType: "application/json; charset-utf-8", 속성 빼야함 (안할시 VO에 값 안들어가서 null출력)
		// String으로 받으려면 파라미터에 @RequestBody를 추가해야함 (안할시 ""출력) (contentType:json은 없어도됨)

	data:$("폼이름").serialize(),
		// 폼요소의 키/값들을 문자열(text)로 보낼때 사용. submit과 동일하게 모든 form내 input을 문자열로 전송한다
		// 그냥 submit시 보내지는 방식과 동일 (쿼리스트링형 문자열)
		// VO객체나 String으로 받을 수 있다
		// 전송되는 데이터를 확인하려면 ajax밖에서 console.log로 찍어보고 받을때 String으로도 받아서 log.info찍어보기
		// ★VO객체로 받으려면 VO파라미터에 @RequestBody 빼야함 (안할시 ajax415에러)
		// ★VO객체로 받으려면 contentType: "application/json; charset-utf-8", 속성 빼야함 (안할시 VO에 값 안들어가서 null출력)
		// String으로 받으려면 파라미터에 @RequestBody를 추가해야함 (안할시 ""출력) (contentType:json은 없어도됨)

	data: JSON.stringify({
		"aa": aaa,
		"bb": bbb
	}),
		// json형 문자열로 보내기
		// Map이나 String으로 받을 수 있다
		// ★JSON.stringify()로 객체를 감싸 문자열로 만들어야한다
		// ★contentType: "application/json; charset-utf-8", 속성을 추가해야한다 (안할시 객체로들어감)
		// 받을때는 Map<String,String/Object> 또는 String 으로 받을 수 있다
		// ★스프링 컨트롤러에서 받으려면 받을 파라미터에 @RequestBody 필요 (안할시 ""출력)
		// json형으로 넘어온데이터를 Map으로 받으면{"aa":aaa,"bb":bbb} 이렇게 받아지고
		// json형으로 넘어온데이터를 String으로 받으면{aa=aaa, bb=bbb} 이렇게 받아짐

	data: {
		"aa": aaa,
		"bb": bbb
	},
		// json형 객체로 보내기
		// 몇개 안되는 데이터를 간단히 보낼때 편리
		// ★contentType:json 쓰면 안된다 (쓰면 ajax500에러))
		// 컨트롤러에서 받을때 보내는 이름 (aa, bb)와 받는 이름이 '일치' 해야한다 String aa, String bb
		// 컨트롤러에서 받을때 어노텐션 아무것도 쓰지 말거나, @RequestParam으로 써야됨 @RequestBody 쓰면 안됨

	//contentType: "application/json; charset-utf-8", //선택:: 보내는 데이터의 형식 (json으로 보낼때 객체를 문자열화 하기위해 필요)
		//(기본값:application/x-www-form-urlencoded; charset=utf-8)
	//dataType:"text", //선택:: 돌려받을 데이터의 형식(text or xml or json .. 기본값은 데이터형식에 맞게 설정된다. ex) map으로받을땐 json)
	async:true, // 선택:: true(비동기) or false(동기) (기본값:true)
	cache : false // 선택:: true(캐시 사용) or false(캐시 사용안함) (기본값: true)
	xhrFields: {
		withCredentials: true // 선택:: 클라이언트와 서버가 통신할때 쿠키와 같은 인증 정보 값을 공유하겠다는 설정
	},
	traditional:true, /* 배열 보낼때는 이거 넣고 contentType: "application/json; charset-utf-8" 쓰면 안되고, data:{datas:배열객체}
			이렇게 { } 감싸고 키를 넣어서 json형으로 만들고 받을때는 List말고 String[]으로 받아야하고
			@RequestParam("datas") String[] a1 일케 파라미터로받거나
			String[] a1 = req.getParameterValues("datas"); 이렇게 받아야함 @requestBody는쓰면안됨*/
	
	success:function(data){ //선택:: 돌려받는 데이터가 있을때만 구현 (데이터가 잘 안갖고와지면 스프링.txt 참고)
		console.log(data);
		console.log(data.ID);
	},
	error:function(a,b,c){//선택:: 예외처리 이벤트(catch절)
		console.log(a,b,c);
	}
});

★ajax내부에서는 ajax외부로 return값이 안갖고가지고, return으로 ajax외부까지 break를 할수 없음
ajax내부에서(가령 success내부) return을 쓰면 undefind가 받아짐
밖에 변수를 만들어서 ajax안에서 변수값을 바꾸고 ajax밖에서 return을 써야함

★ajax에서 async(비동기)를 true로 할시 ajax밖에있는것들이 실행되고 나서 ajax내부가 마지막에 실행되는듯 (=순서가 없어짐)
때문에 ajax가 실행되고 나서도 처리할 문장이 남아있다면 (순차적으로 실행되게하고싶으면) async(비동기)를 꼭 false로 바꾸기

★ 파일 전송시에는 contentType 과 processData 두 옵션을 false로 해야함. 안그러면 null로 날아감
- contentType : false 로 선언 시 content-type 헤더가 multipart/form-data로 전송되게 함
- processData : false로 선언 시 formData를 string으로 변환하지 않음
+++
<form> 태그에 enctype="multipart/form-data"
or
enctype: multipart/form-data,
+++
pom.xml에 추가
<dependency>
	<groupId>commons-fileupload</groupId>
	<artifactId>commons-fileupload</artifactId>
	<version>1.3.3</version>
</dependency>
<dependency>
	<groupId>commons-io</groupId>
	<artifactId>commons-io</artifactId>
	<version>2.4</version>
</dependency>
+++
bean 추가해야함
<bean id="multipartResolver"
	 class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
	<property name="maxUploadSize">
		<value>100000</value>
	</property>
	<property name="uploadTempDir" ref="uploadDirResource" />
</bean>
+++
그리고 아래처럼 받기
@PostMapping("filetest")
public String m1(MultipartHttpServletRequest files){
	Iterator<String> iter = files.getFileNames();
	MultipartFile file = null;
	String fieldName = "";
	while (iter.hasNext()) {
		fieldName = iter.next();
		file = files.getFile(fieldName);
		System.out.println(Objects.requireNonNull(file).getOriginalFilename());
		System.out.println(file.getSize());
		System.out.println(file.getContentType());
	}
	return "success";
}


클라이언트가 서버로 데이터를 보내는 방식
//		1. <form> + submit
//		2. url?key=value
//		3. ajax
//		결론. 서버는 클라리언트가 어떤 방식으로 데이터를 보냈는지 구분하지 않는다.


1. 돌려줄 데이터에 한글이 들어있으면
resp.setCharacterEncoding("UTF-8");
2. 돌려줄 데이터가 순수한 텍스트(문자열) 라면 (생략가능하지만 적는게 좋다고함)
resp.setCharacterEncoding("text/plain");

_data.java _ok.java 파일에서 아래처럼 데이터를 주면 success로 받는다

PrintWriter writer = resp.getWriter();

writer.print(result);

writer.close();

★dispatcher.forward로 보내는게 아님

-----

복사용(검색유도-ajaxset)
$.ajax({
	type:"POST",
	url:"/abcd",
	data:$(f).serialize(),
	async:false,
	success:function(data){
		console.log(data);
	},
	error:function(a,b,c){
		console.log(a,b,c);
	}
});

----------------------------------------------------------------------------------------------------

xml로 보내는 방법

★jsp페이지
<input type="button" value="xml" id="btn2" class="btn btn-default">
<hr>
<div id="result2"></div>

$("#btn2").click(function(){
	$.ajax({
		type:"GET",
		url:"/codestudy/ajax/ex05xmldata.do",
		dataType:"xml", //돌려받는 데이터를 XML형식으로 받겠다
		success:function(result){

			$(result).find("user").each(function(index,item){
				//alert($(item).html());
				console.log($(item).find("seq").text());
				console.log($(item).find("name").text());
				console.log($(item).find("id").text());
				console.log($(item).find("email").text());
				console.log(" ");
			});
			
		},
		error:function(a,b,c){
			console.log(a,b,c);
		}
	})
})


★자바페이지
resp.setCharacterEncoding("UTF-8");
resp.setContentType("text/xml");

MemberDAO dao = new MemberDAO();
ArrayList<MemberDTO> list = dao.list();

PrintWriter writer = resp.getWriter();

writer.print("<?xml version=\"1.0\" encoding=\"UTF-8\"?>");

writer.print("<data>");
	for (MemberDTO dto : list) {
	writer.print("<user>");
		writer.print("<seq>");
		writer.print(dto.getSeq());
		writer.print("</seq>");
		writer.print("<name>");
		writer.print(dto.getName());
		writer.print("</name>");
		writer.print("<id>");
		writer.print(dto.getId());
		writer.print("</id>");
		writer.print("<email>");
		writer.print(dto.getEmail());
		writer.print("</email>");
	writer.print("</user>");
	}
writer.print("</data>");

writer.close();

----------------------------------------------------------------------------------------------------

json으로 보내는 방법
- XML 처럼 네트워크상에서 데이터를 주고받을때 형식으로 많이 사용
- json에서는 홑따옴표(') 사용 불가 → 쌍따옴표("")사용 (이스케이프 : \"\")
- 앞의 속성명도 따옴표로 묶는것은 관례이다

JSON → JavaScript Object Notation
{
	"name":"value",
	"age":20
}


아래는 json방식으로 db받아서 테이블로 출력하는 예제 (마지막 속성 쉼표(",")를 없애는거 만들어야함)

★jsp페이지
<select id="selBuseo">
	<option value="">부서를 선택하세요.</option>
	<c:forEach items="${list}" var="buseo">
		<option value="${buseo}">${buseo}</option>
	</c:forEach>
</select>
<hr>
<table id="tblList" class="table table-bordered">
	<thead>
		<tr>
			<th>번호</th>
			<th>이름</th>
			<th>부서</th>
			<th>직위</th>
			<th>급여</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

$("#selBuseo").change(function(){
	if ($(this).val() != "") {
		$.ajax({
			type : "GET",
			url : "/codestudy/ajax/ex05jsondata.do",
			data : "buseo=" + $(this).val(),
			dataType : "json",
			success : function(result) {
				
				$("#tblList tbody").html(""); //초기화
				
				$(result).each(function(index,item){
					
					let temp = "";
					
					temp += "<tr>";
					temp += "	<td>" + item.num +"</td>";
					temp += "	<td>" + item.name + "</td>";
					temp += "	<td>" + item.buseo + "</td>";
					temp += "	<td>" + item.jikwi + "</td>";
					temp += "	<td>" + item.basicpay + "</td>";
					temp += "</tr>";
					
					$("#tblList tbody").append(temp);
				});
			},
			error : function(a, b, c) {
				console.log(a, b, c);
			}
		});
	}
});


★자바페이지
resp.setCharacterEncoding("UTF-8");
resp.setContentType("application/json");

PrintWriter writer = resp.getWriter();

String buseo = req.getParameter("buseo");

MemberDAO dao = new MemberDAO();
ArrayList<InsaDTO> list = dao.listInsa(buseo);

String temp = "";

temp += "[";
	for(InsaDTO dto : list) {
		temp += "{";
		temp += String.format("\"num\":\"%s\",", dto.getNum());
		temp += String.format("\"name\":\"%s\",", dto.getName());
		temp += String.format("\"buseo\":\"%s\",", dto.getBuseo());
		temp += String.format("\"jikwi\":\"%s\",", dto.getJikwi());
		temp += String.format("\"basicpay\":\"%s\"", dto.getBasicpay());
		temp += "}";
		temp += ",";
	}

temp = temp.substring(0, temp.length()-1);
temp += "]";

writer.print(temp);

writer.close();

----------------------------------------------------------------------------------------------------

$.ajax() 디버깅
	→ status, responseText에 뭐가 찍히는지 볼것
		400 → 전달할 쿼리스트링 (data : "") 틀렸는지 미리 console.log로 찍어서 전달할 값이 잘 나오는지 확인
		404 → 보낼주소 (url : "") 틀렸나 확인
		405 → (type : "") 틀렸나 확인

	→ 서블릿(data.java) 페이지에서 실행하면 보내줄 테이터가 모두 화면에 출력된다
		→ 변수일 경우 페이지에서 해당 이벤트를 발생시킨 후 이클립스 Console 창에서 확인한다

$.ajax() 사용시 유의할 점
ajax를 통해 form의 값을 전송 할 경우 <input type="submit"....> 형태가 아니나 <button type="button"...> 을 사용하는 것이 좋음.
다시말해 form문이 ajax코드 없이 자체적으로 submit 버튼을 통해 전송 되지 않는지 명확히 한 후 ajax 전송 부분을 구현

----------------------------------------------------------------------------------------------------

jdbc작업할때

DAO 클래스 생성자로 conn = DButil.open();을 넣어놓으면 한줄 안써도 되는 약간의 편리함

public TextManagerDAO() {
	conn = DBUtil.open();
}

----------------------------------------------------------------------------------------------------

줄바꿈(개행,엔터) 문자 출력하기

dto.setContent(dto.getContent().replace("\r\n", "<br>"));

설명)
textarea 등에서 엔터를 입력받아서 db에 저장하면 \r\n으로 저장된다
오라클에서 select 한다음 <질의결과>에서 내용 더블클릭 하면 줄바꿔진거 보임

이걸 입력받을때 <br>로 바꿔서 저장할수도 있고,
출력할때 <br>로 바꿔서 출력할수도있다

----------------------------------------------------------------------------------------------------

Mixed Content: The page at '%' was loaded over HTTPs, but requested an insecure image '%'.

HTTPS로 통신하다가 HTTP로 연결되는 통신이 중간에 발생하면 보안정책에 의해 browser에서 block된다.
Google Chrome에서 HTTPS 페이지를 방문하면 브라우저가 JavaScript 콘솔의 오류 및 경고로서 혼합 콘텐츠가 있음을 경고한다.
활성 혼합 콘텐츠가 있는 경우에는 빨간색 오류로 표시가 된다.

경고/오류는 HTTP://URL로 표시된 부분을 수정해야 사라진다.

웹폰트 CDN으로 연결한것중 HTTP URL이 있는지 확인
@import url(http://fonts.googleapis.com/css?family=Open+Sans);

----------------------------------------------------------------------------------------------------

이클립스 jsp 편집창에서 화면이 지맘대로 움직이는 현상 제거

방법1.
Windows -> Preferences -> Java -> Editors -> Folding -> Enable Folding (uncheck)
For HTML, JSP, XML etc in eclispe : Windows -> Preferences -> General -> Editors -> Structured Text Editors -> Enable Folding (uncheck)

방법2. 스펠링 체크를 해제
window-preferences-General-Editor-TextEditor-Spelling → Enable spell checking 해제

----------------------------------------------------------------------------------------------------

페이지마다 별도로 추가해야하는것들 (include가 안되는것들)

<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" language="java" %>
이나
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>

이런건 추가된페이지를 include해도 안돼서 직접 추가해야하고

<%@ include file="/resources/css/style.css.jsp" %>

위처럼 include같은 경우
include로 include가 되어있는 페이지를 불러와도 해당다른페이지의 include가 유지된다

----------------------------------------------------------------------------------------------------

jstl 동적변수 ( c:set 이용 )

map.상위포문의특정키에대한value들
이걸하고싶을때 상위포문의특정키에대한value 를 c:set을 이용해 변수에 넣고
map.[] 이렇게 꺼내면 된다 이때 .은 빼야한다 → map[]

<c:forEach items="${part}" var="pList">
	<c:set var="cd" value="${pList.CODE}" />
	<li>${pList.NAME}</li>
	<ul>
	<c:forEach items="${map[cd]}" var="exr">
		<li class='fc-event fc-h-event fc-daygrid-event fc-daygrid-block-event'>
			<div class='fc-event-main'>${exr.NAME}</div>
		</li>
	</c:forEach>
	</ul>
</c:forEach>

----------------------------------------------------------------------------------------------------

mybatis ResultMap 쓰는법

ResultMap은 DB 필드값과 DTO객체의 프라퍼티(변수)명이 다를 때 사용한다.
ResultMap id에 사용할 임의의 이름을 기술하고 type(type="Department")에는 DTO명을 적어준다.
<result column="department_id" property="deptId" />
column 에는 DB의 필드명을 적고 property에는 DTO 프라퍼티명을 적어준다.

select태그는 resultMap을 써서 resultMap으로 보낸다
→ resultMap을 거쳐서 VO나 map으로 보낸다


<resultMap id="calendarResult" type="com.fitper.domain.CalendarVO">
	<result column="start1" property="start"/>
	<result column="end1" property="end"/>
</resultMap>

<select id="getCalendarList" resultMap="calendarResult">
	SELECT
		id,
		title,
		TO_char(start1, 'YYYY-MM-DD"T"HH24:MI:SS') AS start1,
		TO_char(end1, 'YYYY-MM-DD"T"HH24:MI:SS') AS end1,
		ALLDAY,
		TEXTCOLOR,
		BACKGROUNDCOLOR,
		BORDERCOLOR
	FROM CALENDAR
</select>

----------------------------------------------------------------------------------------------------

클라이언트 ip가져오기

실행중인 로컬서버에서 요청을 보내면 0:0:0:0:0:0:0:1 이렇게 나오고,
같은공유기의 다른기기로 접속하면 사설ip주소가 나옴

String ipAddress = request.getRemoteAddr();
System.out.println("ipAddress1: " + ipAddress1);

String ipAddress2 = request.getHeader("X-Forwarded-For");
if (ipAddress2 == null)
	ipAddress2 = request.getRemoteAddr();
System.out.println("ipAddress2: " + ipAddress2);

InetAddress address = InetAddress.getByName(request.getRemoteAddr());
String clientIP = address.getHostAddress();
System.out.println("ipAddress3: "+clientIP);

위 방법들은 웹 서버가 외부에 공개되어 있어야 하며(배포), 또한 해당 서버가 현재 요청을 받고 있는 클라이언트와 동일한 네트워크에 위치하지 않아야 함
이는 로컬에서는 외부에서 해당 컴퓨터에 접근할 수 없기 때문. 따라서 해당 서비스를 배포한 후 외부에서 접근하여야만 공인IP주소를 확인할 수 있음

아래는 외부에서 제공하는 서비스를 이용하여 로컬 네트워크의 공인 IP 주소를 가져오는 방법이다

URL whatIsMyIp = new URL("http://checkip.amazonaws.com");
BufferedReader in = new BufferedReader(new InputStreamReader(
		whatIsMyIp.openStream()));
String ip = in.readLine();
System.out.println("ipAddress4: "+ip);

checkip.amazonaws.com 대신 icanhazip.com도 됨

----------------------------------------------------------------------------------------------------












