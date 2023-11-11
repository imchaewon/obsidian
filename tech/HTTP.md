Hypertext Transfer Protocol

인터넷을 통해 정보를 주고받을 때 사용되는 표준 프로토콜

웹 브라우징과 웹 서버 간의 통신을 위해 설계되었으며, 월드 와이드 웹 (World Wide Web)에서 웹 페이지, 이미지, 비디오, 오디오 및 다른 리소스를 요청하고 제공하는 데 사용됨

Text, Image, 음성, 영상, JSON, XML 등 거의 모든 형태의 데이터 전송 가능
서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
지금은 HTTP 시대!

## HTTP 메시지 구조
1. start-line - 시작 라인
	1. request-line (요청 시)
	   method [[SP]] request-target [[SP]] HTTP-version [[CRLF]]
	   ex) GET /search?q=hello&hi=ko HTTP/1.1
		1. [[HTTP 메서드]]
		2. 요청 대상
		   absolute-path\[?query] (절대경로\[?쿼리])
		3. [[HTTP 버전]]
	2. status-line (응답 시)
	   HTTP-version [[SP]] status-code [[SP]] reason-phrase [[CRLF]]
	   ex) HTTP/1.1 200 OK
			1. [[HTTP 버전]]
			2. [[HTTP 상태코드]]
			3. 이유 문구 (사람이 이해할 수 있는 짧은 상태 코드 설명글)
2. header - 헤더
   field-name: [[OWS]] field-value [[OWS]]
   ex) Host: www.google.com
	- 필드명은 대소문자 구분 없음
	- 필드명과 콜론사이를 붙여 써야함("Host :" 는 안됨)
	- HTTP 전송에 필요한 모든 부가정보
	  ex) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보
	- 표준 헤더는 종류가 매우 많음
	- 필요 시 임의의 헤더 추가 가능 (ex. helloworld: hihi). 물론 이렇게 할경우 약속된 클라이언트와 서버만 이해 가능
3. empty line - 공백 라인(CRLF). 무조건 포함돼야함
4. message body - 요청 본문
	- 실제 전송할 데이터(HTML문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능)

ex) 요청 메시지
GET /search?q=hello&hi=ko HTTP/1.1
Host: www.google.com
공백라인
요청 메시지도 body 본문을 가질 수 있음

ex) 응답 메시지
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
공백라인
\<html>
	\<body>\</body>
\</html>

- **클라이언트-서버 모델**: HTTP는 클라이언트와 서버 간의 상호작용 모델을 따름. 클라이언트는 웹 브라우저 또는 다른 HTTP 클라이언트가 되며, 서버는 웹 서버가 됨
    
- **요청-응답 프로토콜**: 클라이언트는 HTTP 요청을 생성하여 서버로 보내고, 서버는 해당 요청을 처리하고 응답을 생성하여 클라이언트로 보냄. 이러한 요청과 응답은 일반적으로 텍스트 기반으로 구성되며, 요청 및 응답 헤더 및 본문을 포함함
    
- **무상태성 (Stateless)**: HTTP는 무상태([[Stateless]]) 프로토콜이다. 각 요청은 이전 요청과 독립적으로 처리되며, 서버는 클라이언트의 이전 상태를 기억하지 않음. 이것은 간단하면서 확장 가능한 프로토콜을 제공하지만, 세션 관리와 사용자 상태를 유지하기 위해 추가적인 기술 (쿠키, 세션 등)이 필요할 수 있음.
    
- **메소드**: HTTP 요청은 다양한 메소드 ([[HTTP 메서드]])를 사용하여 작업을 정의함
    
- **URL (Uniform Resource Locator)**: HTTP 요청은 URL을 사용하여 요청 대상 리소스를 지정합니다. URL은 프로토콜 (http:// 또는 https://), 호스트 (웹 서버 주소), 포트 (일반적으로 80 또는 443), 경로 및 쿼리 문자열을 포함합니다.
    
- **상태 코드**: HTTP 응답은 상태 코드를 포함하며, 이 코드는 요청의 결과를 나타냅니다. 예를 들어, 200 OK는 성공적인 응답을 나타내며, 404 Not Found는 요청한 리소스를 찾을 수 없음을 나타냅니다.
