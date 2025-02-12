## 제2장 간단한 프로토콜 HTTP

### 2.1 HTTP는 클라이언트와 서버 간에 통신을 한다.
* 리소스를 요청하는 클라이언트, 응답하는 서버
<br>

### 2.2 리퀘스트와 리스폰스를 교환하여 성립
**Request**
```
// header field
POST(메소드) /form/entry(URI) HTTP/1.1(프로토콜 버전)
Host: hackr.jp
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 16
```
**Response**
```
HTTP /1.1(프로토콜 버전) 200 OK(상태 처리 결과)
// header field
Date: Tue, 10 Jul 2012 06:50:15 GMT
Content-Length: 362
Content-Type: text/html

// body field
<html>
```
<br>

### 2.3 HTTP는 상태를 유지하지 않는 프로토콜
**상태를 유지하지 않는 프로토콜 (Stateless Protocol)**
* 요청과 응답 간에 상태 정보를 관리하지 않는다.
* 이전의 요청 및 응답 데이터를 저장하지 않는다.
* 빠르고 확실하게 처리하기 위한 목적으로 사용된다.

**쿠키(Cookie)**
* 사용자 상태를 유지하기 위한 기술
<br>

### 2.4 리퀘스트 URI로 리소스를 식별
```
URI -> http://www.usagidesign.jp/photo/usagi.htm
URI -> http://www.example.com/auth/index.htm
```
* HTTP는 URI(Uniform Resource Identifier)를 사용하여 인터넷 상의 리소스를 고유하게 식별하고 지정한다.

**지정 방법**
```
GET http://hackr.jp/index.htm HTTP:1.1
```
* 모든 URI를 리퀘스트 URI에 포함

```
GET /index.htm HTTP/1.1
Host: hackr.jp
```
* Host 헤더 필드에 네트워크 로케이션을 포함한다.

```
OPTIONS * HTTP/1.1
```
* 서버 자신에게 요청하는 경우
<br>

### 2.5 서버에 임무를 부여하는 HTTP 메소드
**GET**
```
CASE.1
Request
GET /index.html HTTP / 1.1
Host: www.hackr.jp

Response
Index.html 리소스를 되돌려준다.

CASE.2
Request
GET / Index.html HTTP / 1.1
Host: www.hackr.jp
If-Modified-Since: Thu. 12 Jul 2012 07:30:0 GMT

Response
Index.html 리소스가 2012년 7월 12일 7시30분 이후에 갱신된 경우에만 리소스를 되돌려준다. 
그 이전이라면 상태 코드 304 Not Modified 리스폰스를 되돌려준다.
```
* 요청 URI로 식별된 자원을 서버에 요청하여 데이터를 조회한다.
* 서버는 요청된 자원의 내용을 해석하여 반환한다.

**POST**
```
Request
POST /submit.cgi HTTP /1.1
Host: www.hackr.jp
Content-Length: 1560(1560바이트 데이터)

Response
submit.cgi가 수신한 데이터의 처리한 결과를 되돌려준다.
```
* Entity를 전송하여 리소스를 생성하거나 변경하는 데 사용된다.
  * Entity는 사람이 이해하는 개념이나 정보 단위로, 현실 세계의 대상체를 의미한다.

**PUT**
```
Request
PUT /example.html HTTP /1.1
Host: www.hackr.jp
Content-type: text/html
Content-Length: 1560(1560 바이트 데이터)

Response
상태 코드 204 No Content 리스폰스를 되돌려준다.(서버 상에 example.html이 작성되어 있다.)
```
* 요청 본문에 포함된 데이터를 사용하여 리소스를 교체하거나 덮어쓴다 (데이터 추가 또는 기존 데이터 덮어쓰기).

**HEAD**
```
Request
HEAD /index.html HTTP /1.1
Host: www.hackr.jp

Response
index.html에 관련된 리스폰스 헤더를 되돌려준다.
```
* GET 요청과 동일한 정보를 요청하지만, 응답 본문 없이 헤더만 제공한다.
* 주로 URI의 유효성 확인, 리소스의 갱신 시간 확인 등으로 사용된다.
* 헤더 정보만 제공하므로 네트워크 트래픽을 절약

**DELETE**
```
Request
DELETE /example.html HTTP /1.1
Host: www.hackr.jp

Response
상태 코드 204 NoContent의 리스폰스를 되돌려준다(example.html 서버상에서 삭제되어 있다.)
```
* 지정된 URI에 해당하는 자원을 삭제하는 요청을 보낸다.

**OPTIONS**
```
Request
OPTIONS * HTTP /1.1
Host: www.hackr.jp

Response
HTTP /1.1 200 OK
Allow: GET, POST, HEAD, OPTIONS
(서버가 제공하고 있는 메소드를 되돌려준다.)
```
* 서버 지원 메소드 확인: 서버가 특정 리소스에 대해 지원하는 메소드 목록을 확인.

**TRACE**
```
Request
TRACE / HTTP /1.1
Host: hackr.jp
Max-Forwards: 2

Response
HTTP /1.1 200 OK
Content-Type: message/http
Content-Length: 1024

TRACE / HTTP /1.1
Host: hackr.jp
Max-Forwads:2 (리퀘스트 내용을 리스폰스에 포함해서 되돌려준다)
```
* loop-back 테스트를 통해 통신 경로 상에서 발생한 에러를 디버깅하는 데 사용된다.
  * loop-back은 네트워크 테스트에서 전송된 신호를 다시 보낸 지점으로 되돌려 보내는 방식이다.
* HTTP Max-Forwards 헤더는 TRACE 요청이 지나갈 최대 노드 수를 제한하며, 이를 통해 요청의 경로를 추적할 수 있다 (프록시 수 제한).
* XST(Cross-Site Tracing)는 HTTP TRACE 메소드를 악용한 공격 방식으로, 이를 통해 HttpOnly 속성으로 보호된 세션 쿠키를 탈취할 수 있다.

**CONNECT**
```
Request
CONNECT proxy.hackr.jp:8080 HTTP /1.1

Response
HTTP /1.1 200 OK (그 뒤에 터널링을 개시)
```
* CONNECT 메소드는 클라이언트와 서버 간에 터널을 만들어, 보안 연결(주로 HTTPS)을 설정하는 데 사용
* HTTPS 프록시를 사용할 때, 암호화된 연결을 설정하기 위해 터널링을 사용한다.

<br>

### 2.6 메소드를 사용해서 지시를 내리다
**Method**
* 클라이언트가 웹 서버에 요청하는 동작의 종류를 정의하는 방법이다.
* 주요 HTTP 메소드로는 GET, POST, PUT, HEAD, DELETE, OPTIONS, TRACE, CONNECT, LINK, UNLINK 등이 있다.
* HTTP/1.1 이후 LINK와 UNLINK 메소드는 공식적으로 폐기되었다.
<br>

### 2.7 지속 연결로 접속량을 절약
- 데이터 종류, 크기가 커짐에 따라, 매번 일회성 TCP 커넥션 연결/종료 방식은 비효율적이다.
- HTTP 1.1과 1.0에서는 TCP 연결 문제를 해결하기 위해서 지속 연결(Persistent Connections) 방법을 고안

**지속 연결(Persistent Connections)**
- HTTP/1.1 표준 동작
- 연결을 종료하지 않는 이상 TCP 연결 유지
- 기존 일회성 방식으로 connection을 반복했을 때, 발생하는 오버헤드가 줄었다.
- 요청/응답 간 입출력의 성능 개선

**HTTP 파이프라인화 (HTTP Pipelining)**
- 하나의 연결로 여러 요청을 병행하여 보내고 순차적으로 응답을 처리하는 방식
- 네트워크 효율성을 높이고 응답 속도를 개선
<br>

### 2.8 쿠키를 사용한 상태 관리
* Stateless는 이전 상태를 저장하지 않기 때문에 데이터를 매번 새로 불러와야 하는 번거로움을 해결한 시스템
* 클라이언트의 상태를 파악하기 위해 요청과 응답 사이에 쿠키 정보를 추가하는 방식
* 서버는 응답에 Set-Cookie 헤더 필드를 포함하여 쿠키를 설정하고, 클라이언트는 이후 요청 시마다 이 쿠키를 포함시켜 인증 등의 상태를 관리
