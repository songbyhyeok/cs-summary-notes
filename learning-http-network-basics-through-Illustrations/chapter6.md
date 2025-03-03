# 제6장 HTTP 헤더
## 6.1 HTTP 메시지 헤더
### HTTP 1.1 메시지 구조
<table style="width: 100%; table-layout: fixed;">
  <tr>
    <td>메시지 헤더</td>
    <td>클라이언트, 서버 처리에 필요한 주요 정보를 담고 있다.</td>
  </tr>

  <tr>
    <td>개행 문자(CR+LF)</td>
    <td></td>
  </tr>

  <tr>
    <td>메시지 바디</td>
    <td>리소스 정보가 들어있다.</td>
  </tr>

</table>

* 클라이언트나 서버가 요청이나 응답을 처리하기 위한 정보가 들어있다.

### 리퀘스트의 HTTP 메시지
<table style="width: 100%; table-layout: fixed;">
  <tr>
    <td>리퀘스트 라인</td>
    <td>메소드, URI, HTTP 버전</td>
  </tr>

  <tr>
    <td>리퀘스트 헤더 필드</td>
    <td>HTTP 헤더 필드</td>
  </tr>

  <tr>
    <td>일반 헤더 필드</td>
    <td>HTTP 헤더 필드</td>
  </tr>

  <tr>
    <td>엔티티 헤더 필드</td>
    <td>HTTP 헤더 필드</td>
  </tr>

  <tr>
    <td>그 외</td>
    <td></td>
  </tr>

</table>

* 메소드, URI, HTTP 버전, HTTP 헤더 필드 등으로 구성되어 있다.

### 리스폰스의 HTTP 메시지
<table style="width: 100%; table-layout: fixed;">
  <tr>
    <td>상태 라인</td>
    <td>HTTP 버전, 상태 코드</td>
  </tr>

  <tr>
    <td>리스폰스 헤더 필드</td>
    <td>HTTP 헤더 필드</td>
  </tr>

  <tr>
    <td>일반 헤더 필드</td>
    <td>HTTP 헤더 필드</td>
  </tr>

  <tr>
    <td>엔티티 헤더 필드</td>
    <td>HTTP 헤더 필드</td>
  </tr>

  <tr>
    <td>그 외</td>
    <td></td>
  </tr>

</table>

* HTTP 메시지와 HTTP 버전, 상태코드, HTTP 헤더 필드 등으로 구성되어 있다.


## 6.2 HTTP 헤더 필드
- HTTP 메시지를 구성하는 요소 중 하나
- 클라이언트와 서버 간의 요청 및 응답에서 부가적 중요 정보를 전달
    - ex 메시지 바디의 크기, 언어, 인증 정보 등

### HTTP 헤더 필드의 구조
- 헤더 필드 명: 필드 값
  - ex Content-Type:text/html
  - ex Keep-Alive:timeout=15,max=100
- HTTP 헤더 필드가 중복된 경우
  - 브라우저마다 상이하다, 오름 혹은 내림 방식으로 우선 처리

### 4종류의 HTTP 헤더 필드
- 일반적 헤더 필드(General Header Fields)
  - 요청, 응답 메시지 둘 다 사용되는 헤더
- 리퀘스트 헤더 필드(Request Header Fields)
  - 클라이언트가 서버에 요청을 보낼 때 함께 포함하는 정보
  - 리퀘스트의 부가적 정보나 클라이언트의 정보 등이 포함
- 리스폰스 헤더 필드(Response Header Fields)
  - 서버가 클라이언트로 전송하는 리스폰스 메시지에 사용되는 헤더
  - 리스폰스의 부가적 정보나 서버의 정보 또는 클라이언트로부터 추가적인 정보 요청 등이 포함
- 엔티티 헤더 필드(Entity Header Fields)
    ```
    // 엔티티 바디의 미디어 타입을 표기
    Content-Type: text/html; charset=UTF-8
    // 응답 본문이 어떤 방식으로 인코딩 됐는지
    Content-Encoding: gzip
    ```
  - HTTP 요청 및 응답 본문에 대한 중요한 정보를 제공하는 헤더 필드
  - 클라이언트가 응답을 어떻게 처리할지 결정하는 데 도움을 준다.

### 일반 헤더 필드 종류
- Cache-Control
  - HTTP 요청과 응답에서 캐시 동작을 제어 목적
- Connection
  - 서버와 클라이언트 간의 연결 상태를 관리
  - 커넥션 연결 과정은 hop-by-hop 방식을 사용
- Date
  - HTTP 요청과 응답에서 메시지가 전송된 날짜와 시간을 나타내는 헤더
- Pragma
  - Cache-Control 헤더 이전에 사용 
  - 캐시와 관련된 설정을 제공하는 데 사용
  - 더 이상 사용되지 않는 헤더
- Trailer
  - 청크 방식으로 데이터를 보내고 나서, 메시지의 끝부분에 추가 필드를 첨부
- Transfer-Encoding
  - 서버 간 데이터 전송 방식을 정의
    - → chunked 방식
  - Hop-by-hop 방식
  - HTTP/2에서 Trailer를 제외하고는 청크 전송 방식 헤더를 모두 금지, 더 효율적인 전송 방법을 제공하기 때문
- Upgrade
  - 다른 프로토콜로 업그레이드
    - ex http 1.1 → http 2.0
  - HTTP/2는 이 헤더를 명시적 허용하지 않는다.
- Via
  - 포워드 프록시와 리버스 프록시에 의해서 추가된다
  - 메시지 전송 추적
  - 요청 루프 방지(동일한 요청 방지)
  - 프로토콜 기능 식별(프로토콜 버전, 기능 식별)
- Warning
  - 에러 통지

### 리퀘스트 헤더 필드
- Accept
  - 클라이언트가 서버에 요청을 보낼 때, 서버가 응답으로 반환할 수 있는 콘텐츠 유형(Content-Type)을 지정하는 데 사용
- Accept-Charset
  - 클라이언트가 서버로부터 받기를 원하는 문자 인코딩 형식을 지정하는 데 사용
- Accept-Encoding
  - 클라이언트가 이해할 수 있는 압축 방식을 서버에 전달하고, 서버는 이를 바탕으로 적절한 인코딩 방식으로 응답
- Accept-Language
  - 클라이언트가 선호하는 언어와 지역을 서버에 알려주는 헤더
- Authorization
  - 사용자 인증 정보를 서버로 보내는 역할을 하며, 서버가 요청된 리소스에 접근할 수 있도록 인증된 사용자인지 확인
- Expect
  - 서버가 요청을 완전히 처리하기 전에 특정 조건을 만족해야 한다고 클라이언트가 서버에 요청하는 경우 사용
- From
  - 요청을 보낸 사람의 이메일 주소나 사용자 정보를 포함하는 데 사용
- Host
  - 요청이 어떤 서버로 보내지는지에 대한 정보를 지정
- If-Match
  - 요청을 조건부로 만들어, 리소스의 ETag가 헤더에 지정된 값과 일치하는 경우에만 서버가 리소스를 반환하거나 변경
- If-Modified-Since
  - 요청을 조건부로 만들어, 서버가 리소스를 수정한 이후에만 리소스를 반환
- If-None-Match
  - 서버에 리소스가 변경되지 않았으면 리소스를 다시 보내지 말라고 요청하는 방법
- If-Range
  - 범위 요청을 조건부로 만들어, 특정 조건이 충족될 때만 리소스의 일부를 요청
- If-Unmodified-Since
  - 서버에 요청을 보낼 때, 리소스가 특정 날짜 이후로 수정되지 않았다면 요청을 처리해 달라고 조건을 걸 수 있는 방법
- Max-Forwards
  - HTTP TRACE 요청에서 사용되며, 요청이 지나갈 수 있는 최대 노드(주로 프록시)의 수를 제한합니다. 요청이 각 노드를 거칠 때마다 이 값은 감소하며, 값이 0에 도달하면 요청이 더 이상 전달되지 않고 응답이 반환
- Proxy-Authorization
  - 클라이언트가 프록시 서버에 인증을 제공하는 데 사용
- Range
  - 클라이언트가 리소스의 특정 부분만 요청할 때 사용
    - ex Range: bytes=1000-1999
- Referer
  - 리소스를 요청한 페이지의 URL을 포함하여 서버가 요청의 출처를 알 수 있게 하며, 주로 분석, 로깅, 캐싱에 사용
  - Referer x → Referrer o
- TE
  - 서버가 응답을 보낼 때 사용할 수 있는 전송 인코딩 방식을 알려주는 역할
  - 전송 인코딩은 데이터 압축이나 청크 단위로 나누어 전송하는 방법
- User-Agent
  - 클라이언트(웹 브라우저나 기타 프로그램)가 서버에 요청을 보낼 때, 클라이언트가 어떤 소프트웨어나 장치에서 요청을 보냈는지를 알려주는 역할

### 리스폰스 헤더 필드
- Accept-Ranges
  - 서버가 파일의 일부만 요청하거나, 중단된 다운로드를 이어받을 수 있게 해주는 기능을 지원
- Age
  - 객체가 프록시 캐시에 저장된 시간을 초 단위로 나타낸다.
- Etag
  - 특정 버전의 리소스를 식별하는 값
- Location
  - 페이지를 다른 URL로 리디렉션할 때 사용
- Proxy-Authenticate
  - 클라이언트에게 프록시 서버를 통해 리소스를 접근하기 전에 인증을 요구한다고 알려주는 헤더
- Retry-After
  - 사용자 에이전트(브라우저나 클라이언트)가 후속 요청을 보내기 전에 기다려야 하는 시간
- Server
  - 서버 소프트웨어에 대한 정보를 클라이언트에게 제공
- Vary
  - 주로 캐시 시스템에서 사용되며, 어떤 요청 헤더에 따라 리소스가 달라질 수 있는지 알림
- WWW-Authenticate
  - 특정 리소스에 접근하기 위해 사용할 수 있는 HTTP 인증 방법(또는 인증 요구)을 서버가 클라이언트에게 알려주는 헤더

### 엔티티 헤더 필드
- Allow
  - 특정 리소스에 대해 클라이언트가 사용할 수 있는 HTTP 메서드(GET, POST, PUT 등)를 나열
- Content-Encoding
  - 리소스 본문에 적용된 압축 방식에 관련
- Content-Language
  - 사용자는 자신의 선호 언어에 맞는 콘텐츠를 선택
- Content-Length
  - 수신자에게 전송되는 메시지 본문의 크기를 바이트 단위로 표기
- Content-Location
  - 콘텐츠 협상 후, 리소스를 가져오는 다른 URL을 알려주는 헤더
  - 서버가 여러 언어로 제공되는 콘텐츠 중 클라이언트가 요청한 언어의 리소스를 전달했다면, 그 리소스를 바로 접근할 수 있는 URL을 Content-Location에 담아 보내는 방식
- Content-MD5
  - 서버가 보낸 데이터가 손상되지 않았는지 확인
  - 서버는 데이터의 고유한 해시 값을 계산해 Content-MD5로 전달하고, 클라이언트는 받은 데이터와 그 해시 값을 비교해 데이터가 변경되지 않았는지 검증
- Content-Range
  - 요청된 데이터의 어떤 부분이 전송되고 있는지
- Content-Type
  - 리소스의 원본 미디어 타입을 알려준다.
- Expires
  - 자원의 유효 기간을 설정
- Last-Modified
  - 서버가 마지막으로 자원을 수정한 날짜와 시간을 클라이언트에게 통보

### HTTP/1.1 이외의 헤더 필드
**RFC(Request for Comments)**  
```
1) RFC 2616
HTTP-message   = Request | Response

generic-message = start-line
                 *(message-header CRLF)
                 CRLF
                 [ message-body ]

Request       = Request-Line
                *(( general-header
                | request-header
                | entity-header ) CRLF)
                CRLF
                [ message-body ]

Response      = Status-Line
                *(( general-header
                | response-header
                | entity-header ) CRLF)
                CRLF
                [ message-body ]
 
2) RFC 7230
HTTP-message   = start-line
                 *( header-field CRLF )
                 CRLF
                 [ message-body ]
```

- IETF(Internet Engineering Task Force), IAB(Internet Architecture Board)와 같은 조직에서 관리 및 발행
- 인터넷 프로토콜, 시스템, 절차 및 관련 기술에 대한 규칙과 권장 사항을 정의한 문서
- HTTP/1.1 RFC 2616 → RFC 7230 → RFC 9112 개정
- ABNF도 일반, 요청, 응답, 엔티티 헤더로 나눴으나 개정된 문서에서는 좀 더 간소화
  - 헤더가 제거되거나 사용용도에 따라 다른 카테고리로 이동
  - HTTP-message의 변경
  - 용어 변경과 문법 변경
    - 메시지 헤더(message-header) -> 헤더 필드(header-field)로 변경
    - 엔티티(Entity) ->표현(Representation)으로 변경

**End-to-end 헤더와 hop-by-hop 헤더**  
- 캐시와 비캐시 프록시 동작을 정의하기 위해 두 가지 카테고리로 분류
  - 종단간 헤더(End-to-end Header)
    - HTTP 프로토콜에서, 중간 프록시를 거칠 때 그 서버들이 헤더에 포함된 정보를 변경하거나 처리하지 않고, 최종 목적지까지 전달되는 동안 그대로 유지되는 헤더
        - 이 헤더는 최종 목적지까지 변경되지 않기 때문에, 데이터의 무결성을 유지하는 데 중요한 역할
  - 홉간 헤더(hop-by-hop Header)
    - HTTP 메시지가 여러 서버를 거쳐 전달될 때, 각 노드에서 처리할 수 있도록 정보를 전달하는 역할, 각 hop에서만 유효한 설정이나 지침을 담고 있다.
    - 단일 hop(한 노드를 지나갈 때)의 데이터를 정의
    - 프록시에의해 재전송되거나 캐시되어선 안된다.
    - 헤더 종류
        - Connection
        - Keep-Alive
        - Proxy-Authenticate
        - Proxy-Authorization
        - Trailer
        - TE
        - Transfer-Encoding
        - Upgrade


## 6.3 HTTP/1.1 일반 헤더 필드
- 리퀘스트 메시지와 리스폰스 메시지 양쪽에서 사용되는 헤더

### Cache-Control
- HTTP 요청과 응답에서 캐시 동작을 제어 목적
- 디렉티브 = 캐시 지시어, 지시어를 사용해서 캐시 동작 지정
- Cache-Control 헤더는 리퀘스트와 리스폰스로 분류된다.

**캐시 리퀘스트 디렉티브**  
- no-cache
  - 캐시가 응답을 재사용하기 전에 원본 서버와 응답을 검증하도록 요청
  - 캐시가 이미 신선한 응답을 가지고 있더라도, 사용자가 항상 최신 응답을 받을 수 있도록 보장
- no-store
  - 모든 캐시 시스템이 해당 요청과 응답을 저장하지 않도록 명령
- max-age
  - 클라이언트가 원본 서버에서 생성된 응답을 최대 N초 동안 재사용할 수 있도록 허용

- max-stale
  - 클라이언트가 N초 이내에 만료된 응답을 받아들일 수 있다는 의미
  - 서버가 다운되었거나 응답이 너무 느릴 때, 클라이언트가 만료된 캐시된 응답을 사용할 수 있도록 할 때 유용

- min-fresh
  - 클라이언트가 최소 N초 동안 신선한 응답을 허용한다는 의미

- no-transform
  - 중간 서버에서 콘텐츠 변형을 방지하는 역할
  - 요청에 대해 중간 캐시나 프록시 서버가 응답 콘텐츠를 변형하지 않도록 요구

- only-if-cached
  - 캐시에 이미 저장된 응답만 요청

- cache-extension
  - 새로운 디렉티브를 위해서 토큰

**캐시 리스폰스 디렉티브**  
- public
  - 응답이 공유 캐시(예: CDN, 프록시 서버)에 저장될 수 있음을 나타낸다.
  - 인증 헤더가 포함된 요청에 대한 응답에 사용된다.

- private
  - 사설 캐시
  - 응답이 개인 캐시(예: 브라우저의 로컬 캐시)에만 저장될 수 있음을 나타낸다.
  - 응답이 공유 캐시(예: CDN, 프록시 서버)에 저장되는 것을 방지

- no-cache
  - 응답이 캐시에 저장될 수 있음을 나타내지만, 저장된 응답을 재사용하기 전에 매번 원본 서버와 검증해야 함을 의미
  - 캐시로부터 오래된 리소스가 반환되는 것을 막기 위해 사용

- no-store
  - 응답이 캐시되지 않도록 하며, 민감한 정보나 변화가 잦은 데이터를 다룰 때 유용

- no-transform
  - 프록시가 응답의 내용을 변경하지 않도록 보장하며, 콘텐츠가 원본 그대로 유지

- must-revalidate
  - 보통 max-age와 함께 사용
    - 예를 들어, Cache-Control: max-age=604800 같이 설정하면, 응답이 최대 7일 동안 신선하다고 간주되며, 그 이후에는 원본 서버와 검증.

- proxy-revalidate
  - 주로 공유 캐시에서 사용되며, 응답이 만료되면 재검증
  - must-revalidate와 동일한 기능

- max-age
  - 응답이 생성된 후 N초 동안 신선하게 유지된다는 것을 나타낸다.
  - Cache-Control: max-age=604800은 캐시가 응답을 7일 동안 신선하게 유지하고 재사용할 수 있다는 의미

- s-maxage
  - 공유 캐시에서 응답의 신선도를 설정할 때 사용되며, 개인 캐시에는 영향을 미치지 않는다.

- cache-extension
  - 새로운 디렉티브를 위한 토큰

### Connection
- 서버와 클라이언트 간의 연결 상태를 관리
- 커넥션 연결 과정은 hop-by-hop 방식을 사용
- 지속적 접속 관리
- Connection: Keep-Alive
  - HTTP/1.1 이전 버전은 지속적 접속을 설정하기 위해 사용

### Date
- HTTP 메시지를 생성한 날짜를 표기

### Pragma
- HTTP/1.0 캐시와의 호환성을 위해 사용되는 구식 헤더

### Trailer
- 청크 전송 인코딩(chunked transfer encoding)을 사용할 때 메시지 본문 뒤에 추가적인 헤더 필드를 포함할 수 있게 해주는 HTTP 요청 및 응답 헤더

### Transfer-Encoding
- 네트워크 상에서 메시지를 전송할 때 사용하는 인코딩 방식을 지정하는 HTTP 요청 및 응답 헤더
- 호프별(hop-by-hop) 헤더
- 주로 청크 전송 인코딩(chunked)과 같은 방식을 지정하는 데 사용
- HTTP/2 이상에서는 이 헤더의 사용이 제한

### Upgrade
- 주로 HTTP/1.1에서 다른 프로토콜(예: HTTP/2, WebSocket)로의 전환을 가능하게 하는 역할을 하지만, HTTP/2에서는 사용되지 않는다.

### Via
- 프록시 서버에서 요청과 응답의 전달 경로를 추적하고, 요청 루프를 방지하며, 프록시의 프로토콜 기능을 식별하는 데 사용
- 여러 프록시 서버들이 메시지를 전달한 경로를 나타내는 데 사용되며, 각 프록시는 프로토콜과 서버 정보를 기록

### Warning
- HTTP 요청과 응답에서 메시지 상태에 대한 문제를 나타내는 데 사용되는 헤더
- 메시지 상태에 대한 경고를 제공하지만, 현재는 deprecated 상태


## 6.4 리퀘스트 헤더 필드
- 브라우저에서 서버 측으로 송신된 요청 메시지에 사용되는 헤더
- 리퀘스트의 부가 정보, 클라이언트 정보, 응답 콘텐츠에 관한 우선순위 용도

### 6.4.1 Accept
- 클라이언트가 처리할 수 있는 미디어 타입 형식과, 그 우선순위를 서버에 전달하는 것
- 우선순위 처리 방식은 클라이언트가 Accept 헤더에 지정한 미디어 타입의 우선순위를 서버가 따르는 방식, 서버는 우선순위가 높은 미디어 타입부터 확인해가며, 지원 가능한 타입을 선택하여 응답을 생성

### 6.4.2 Accept-Charset
- 클라이언트가 어떤 문자 인코딩을 받아들일 수 있는지를 서버에 알리는 요청 헤더
- 이 헤더를 사용하지 않고, 문자 인코딩을 요청하면 406 오류를 반환

### 6.4.3 Accept-Encoding
- 콘텐츠 크기를 고려해서 압축을 통해 전송하게 되는데, 이때 브라우저가 해당 압축을 풀 수 있는 기술이 있는지 물어보는 것
- 서버는 클라이언트가 처리할 수 있는 압축 형식(예: gzip, deflate 등)을 확인하고, 해당 형식으로 응답을 압축하여 전송

### 6.4.4 Accept-Language
- 클라이언트가 선호하는 자연 언어를 요청

### 6.4.5 Authorization
- 사용자가 서버와 인증할 때 크리덴셜(자격 증명)을 제공하는 데 사용
- 사용자가 인증 없이 요청하면, 서버는 401 응답과 인증 방식 정보를 제공하고, 클라이언트는 이를 바탕으로 자격 증명을 보내 다시 요청한다.

**크리덴셜(credential)?**  
- 사용자가 허가된 사용자인지, 적절한 권한을 가지고 있는지를 확인하기 위한 인증 정보

### 6.4.6 Expect
- 클라이언트가 서버에게 특정 조건을 만족할 때만 요청을 처리하도록 요청하는 데 사용

### 6.4.7 From
- 사용자의 이메일 주소를 포함해 문제 발생 시 연락을 가능하게 하며, 자동화된 에이전트가 잘못 동작할 경우 제어자에게 연락하는 용도로 사용

### 6.4.8 Host
- 요청하는 서버의 도메인 이름과 포트를 지정하는 필드
- HTTP/1.1에서 유일한 필수 헤더 필드
- 동일한 IP 주소에서 여러 웹사이트를 호스팅하는 경우, 요청을 적절한 서버로 라우팅하는 데 사용

### 6.4.9 If-Match
- 서버가 요청한 자원의 ETag 값과 일치하는지 확인하여, 일치할 경우에만 요청을 처리하고, 그렇지 않으면 "412 Precondition Failed" 에러를 반환하는 조건부 HTTP 헤더
- GET 또는 HEAD 요청
  - 요청을 보낼 때 Range 헤더와 함께 사용하면, 서버는 클라이언트가 요청한 데이터 범위가 최신 자원에서 나온 것인지를 확인
  - 클라이언트가 큰 파일을 요청할 때 If-Match와 Range 헤더를 사용하여, 이전에 요청한 범위의 데이터가 변경되지 않았음을 보장하고, 서버가 동일한 범위 데이터를 제공
- Put 메소드
  - If-Match는 자원이 변경되지 않았는지 확인하는 데 사용
  - 클라이언트가 문서의 내용을 수정하려 할 때, 그 문서가 다른 사용자에 의해 이미 수정되었는지 확인하고, 수정된 상태라면 클라이언트에게 덮어쓰지 않도록 경고

**ETag (Entity Tag)**  
- 웹 서버가 리소스의 특정 버전을 식별하기 위해 사용하는 고유한 문자열
- HTTP 응답 헤더에 포함되며, 클라이언트가 서버에 요청을 보낼 때 해당 리소스가 변경되었는지 확인하는 데 사용

### 6.4.10 If-Modified-Since
- 서버가 자원이 지정된 날짜 이후에 수정되었을 경우에만 자원을 반환하고, 수정되지 않았으면 304 Not Modified 응답을 보내는 조건부 요청 헤더
- GET과 HEAD 메소드를 사용
- 사용자가 웹 페이지를 방문하고 캐시된 버전을 저장한 후, 다시 방문할 때 **If-Modified-Since**를 사용하여 페이지가 수정된 경우에만 새로 업데이트된 페이지를 받는다.
  - 예를 들어, 뉴스 사이트나 소셜 미디어 앱에서는 사용자에게 최신 정보를 제공해야 할 때, 이전에 받아본 리소스를 기준으로 변경 사항이 있는지 확인하고, 변경된 내용만 받아올 수 있다.
- 불필요한 데이터 전송을 줄이고, 캐시된 자원을 효율적으로 관리하는 데 중요한 역할

### 6.4.11 If-None-Match
- 일치하지 않으면 (자원이 수정되었거나 삭제되었을 경우), 서버는 새로운 자원을 반환
- 메서드에서는 조건이 실패하면 `412 Precondition Failed` 상태 코드를 반환

### 6.4.12 If-Range
- 범위 요청을 조건부로 만들고, 조건이 충족되면 부분 리소스를, 충족되지 않으면 전체 리소스를 반환하는데 사용
- `If-Range` 헤더는 **조건**을 정의하는 데 **`Last-Modified`** 또는 **`ETag`** 값 중 하나를 사용
- 리소스가 변경되었는지 확인하는 로직이 없으므로, 전체 리소스를 다시 다운로드해야 하는 경우가 생길 수 있다.

### 6.4.13 If-Unmodified-Since
- 서버에 요청한 리소스가 지정된 날짜 이후에 수정되지 않았을 경우에만 요청을 처리
- 만약 리소스가 지정된 날짜 이후에 수정되었다면, 서버는 **412 Precondition Failed** 상태 코드를 반환
- 예시: 위키에서 문서를 수정하려 할 때, 해당 문서가 다른 사람이 수정한 후라면, 수정 요청이 거부된다.
- `If-Unmodified-Since` 헤더는 `Range` 헤더와 함께 사용
  - 라이언트가 리소스의 일부만 요청하면서, 요청한 범위가 수정되지 않았음을 보장하고 싶을 때 Range 헤더와 같이 사용

### 6.4.14 Max-Forwards
- TRACE 요청에서 요청이 통과할 최대 노드 수를 제한하며, 네트워크 경로를 추적하고 중간 서버들을 확인하는 데 사용

### 6.4.15 Proxy-Authorization
- **프록시 서버**와의 인증을 위해 클라이언트가 자신의 **인증 정보를 포함**하여 요청을 보내는 데 사용

### 6.4.16 Range
- 클라이언트가 리소스의 특정 부분만 요청할 수 있도록 하며, 서버는 해당 범위만 포함된 응답을 `206 Partial Content`로 반환

### 6.4.17 Referer
- 클라이언트가 서버에 **요청을 보낼 때, 이전에 방문했던 페이지**의 URL을 서버에 전달하는 역할(이 요청은 어디에서 왔는지)
- 주로 **분석**이나 **로깅**, **트래킹**을 위해 사용

### 6.4.18 TE(Transfer Encoding)
- 클라이언트가 **수용할 수 있는 전송 인코딩 방식**(예: 압축, 청크 전송)을 서버에 알리며, 서버는 이를 기반으로 데이터를 효율적으로 전송
  - 예를 들어, 클라이언트가 `TE: gzip, deflate, chunked`라고 설정하면, 서버는 데이터를 **gzip** 또는 **deflate**로 압축하거나, **청크로 분할**하여 전송할 수 있다, 클라이언트는 이러한 인코딩 방식을 받아들일 준비가 되어 있다는 것을 서버에 알리는 것

### 6.4.19 User-Agent
- 클라이언트가 사용하는 브라우저, 운영 체제, 버전 등의 정보를 포함하여 서버가 클라이언트를 식별하고, 이에 맞는 최적화된 콘텐츠를 제공할 수 있게 도와준다.


## 6.5 리스폰스 헤더 필드
- 서버가 클라이언트에게 전송하는 추가적인 정보
- 응답 본문에 포함된 데이터의 성격이나 처리 방법에 대한 정보를 제공
- 클라이언트가 서버의 응답을 어떻게 해석하고 처리해야 할지를 알려주는 중요한 역할

### 6.5.1 Accept-Ranges
- 서버가 클라이언트에게 파일의 일부만 요청하거나 중단된 다운로드를 재개할 수 있음을 알리는 역할
- 중단된 다운로드를 재개하거나 파일을 일부만 받아올 수 있다.
- **범위 요청의 유형**
  - Accept-Ranges: bytes
    - 서버가 범위 요청을 바이트 단위로 지원
  - Accept-Ranges: none
    - 서버가 범위 요청을 지원하지 않음을 의미

### 6.5.2 Age
- 주로 **프록시 서버**나 **캐시 서버**에서 데이터를 제공할 때 유용하며, 클라이언트가 최신 데이터를 요청할 때 참고할 수 있는 정보

### 6.5.3 ETag
- HTTP 캐싱과 리소스 버전 관리를 위한 중요한 헤더
- 리소스의 버전 식별자로, 리소스의 내용이 변경되지 않았을 때 서버가 불필요하게 리소스를 다시 전송하는 것을 방지
- 보통 ASCII 문자로 구성되며, 큰따옴표 안에 표시
- 클라이언트는 ETag 값을 저장하고, If-None-Match 헤더로 서버에 보내 수정 여부를 확인
- If-Modified-Since 헤더를 사용해, 클라이언트는 서버에 리소스가 최신 상태인지 확인하고, 수정된 경우에만 리소스를 새로 받아오는 요청
- Strong ETag vs Weak ETag
  - Weak ETag
    - 값의 앞부분에 “W/”가 붙는다.
    - 생성하기 쉽지만, 리소스의 비교에 유용하지 않다.
  - Strong ETag
    - 리소스의 바이트 단위로 비교가 가능하여 리소스가 변경되지 않았음을 보다 정확하게 검증할 수 있지만, 생성하는 데 더 많은 리소스가 필요

### 6.5.4 Location
- 주로 리디렉션(3XX)이나 새 리소스 생성(201 Created) 시 사용. 클라이언트에게 새로운 위치를 알려주는 역할.
- 리디렉션을 위한 URL을 알려주거나, 새로운 리소스가 생성된 경우 그 리소스의 URL을 클라이언트에게 알려주는 역할

**예시**  
- 3XX 리디렉션: 서버가 클라이언트를 다른 위치로 리디렉션할 때 사용된다.
    - 예: 서버가 `Location: http://example.com/new-location`이라고 보내면, 클라이언트는 해당 URL로 자동으로 이동한다.
- 201 Created 응답: 새 리소스가 성공적으로 생성된 후, 생성된 리소스의 위치를 알려줄 때 사용
  - 예: 서버가 `Location: http://example.com/resource/123`라고 보내면, 클라이언트는 새로 생성된 리소스를 그 URL로 접근할 수 있다.

### 6.5.5 Proxy-Authenticate
- 프록시 서버 뒤에 있는 리소스에 접근하기 위한 인증 방법을 정의
- 클라이언트가 인증을 요구하는 프록시 서버에 자신을 인증할 수 있도록 도와준다.
- 프록시 서버에 접근하기 위해 필요한 인증 방법을 클라이언트에게 알려준다.

### 6.5.6 Retry-After
- 서버가 일시적으로 요청을 처리할 수 없을 때, 클라이언트가 재요청을 하기 전에 대기해야 할 시간을 알려주는 헤더

### 6.5.7 Server
- 서버 소프트웨어 정보를 제공
- 보안상의 이유로 너무 많은 세부 정보를 포함하는 것 지양

### 6.5.8 Vary
- 동일한 URL에 대해 사용자의 특징(User-Agent, Accept-Encoding, Origin 등)에 따라 서로 다른 응답을 제공 및 캐시
- 데스크톱과 모바일 사용자에게 다른 콘텐츠를 제공 가능
- 요청의 특정 헤더에 따라 응답이 달라지도록 하여, 캐시가 헤더별로 별도로 관리되도록 한다.
- 응답을 캐시할 때, Vary 필드에 나열된 헤더를 기준으로 개별적으로 캐시되도록 보장

### 6.5.9 WWW-Authenticate
- 서버가 어떤 인증 방법을 지원하는지 클라이언트에게 알리는 중요한 도구

```cpp
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Basic realm="Example"
```

- 이 경우, 서버는 Basic 인증 방법을 사용해 자격 증명을 요구하고 있음을 클라이언트에게 알린다. 클라이언트는 이 정보를 바탕으로 사용자 이름과 비밀번호를 포함한 Authorization 헤더를 서버로 보내게 된다.


## 6.6 엔티티 헤더 필드
<table style="width: 100%; table-layout: fixed;">
  <tr>
    <td></td>
    <td>General Header</td>
  </tr>

  <tr>
    <td>HTTP Header</td>
    <td>Request/Response Header</td>
  </tr>

  <tr>
    <td></td>
    <td>Entity Header</td>
  </tr>

</table>

- HTTP/1.1 명세에서 엔티티 헤더(Entity Header) → 표현 헤더 필드(Representation header fields)로 대체되었다.
- HTTP 메시지의 본문(내용)에 대한 메타데이터를 설명하는 HTTP 헤더이다.

### 6.6.1 Allow
```cpp
**Allow: GET, POST**
-> 클라이언트는 리소스에 대해 GET 또는 POST 메서드만 사용할 수 있음
```

- 리소스가 지원하는 요청 HTTP 메서드의 집합을 나열
- 서버가 405 Method Not Allowed 상태 코드로 응답할 때, 대신 사용할 수 있는 요청 메서드를 알려준다.
- Allow 헤더의 값이 비어 있으면, 해당 리소스는 어떤 요청 메서드도 허용하지 않음을 의미

**405 Method Not Allowed 상태 코드가 발생하게 된 이유**  
1. **요청한 리소스가 특정 HTTP 메서드를 지원하지 않는 경우 발생**
   - ex → 리소스가 GET 메서드만 지원하는데 클라이언트가 POST를 요청한 경우 405가 반환
2. **리소스가 특정 작업만 허용하고 다른 작업을 제한할 때 발생**
   - ex → 특정 API가 데이터 수정에는 **PUT** 메서드를, 데이터 조회에는 **GET** 메서드를 사용하도록 설계되었지만, 클라이언트가 **DELETE** 메서드를 요청하면 405 상태 코드가 반환

### 6.6.2 Content-Encoding
```cpp
Content-Encoding: gzip
Content-Encoding: compress
Content-Encoding: deflate
Content-Encoding: br
Content-Encoding: zstd

// Multiple, in the order in which they were applied
Content-Encoding: deflate, gzip
```

- 리소스에 적용된 인코딩 방식과 그 순서를 나열
- 수신자가 데이터를 어떻게 디코딩해야 원본 콘텐츠 형식을 얻을 수 있는지 알려준다.

**다양한 콘텐츠 인코딩 형식**
- gzip
    - Lempel-Ziv 코딩(LZ77)과 32비트 CRC를 사용하는 형식
    - 원래 UNIX **gzip** 프로그램의 형식이며, HTTP/1.1 표준에서는 호환성을 위해 **x-gzip**을 별칭으로 표현
- compress
    - Lempel-Ziv-Welch (LZW) 알고리즘을 사용하는 형식
    - UNIX **compress** 프로그램에서 유래한 것으로, 이 프로그램은 대부분의 UNIX 배포판에서
    사라졌다.
    - 대부분의 브라우저에서 사용되지 않는다.
- deflate
    - **zlib** 구조(RFC 1950)와 **deflate** 압축 알고리즘(RFC 1951)을 사용하는 형식
- br
    - **Brotli** 알고리즘 구조(RFC 7932)를 사용하는 형식
- zstd
    - **Zstandard** 알고리즘 구조(RFC 8878)를 사용하는 형식
- Identity

**사용 예시**
```cpp
요청 예시
**Accept-Encoding: gzip, deflate**

Accept-Encoding는 클라이언트가 지원하는 콘텐츠 인코딩 방식이다.
위 예시에서는 gzip과 deflate 두 가지 압축 방법을 서버와 협상한다.

응답 예시
**Content-Encoding: gzip**

Content-Encoding는 서버가 실제로 사용한 콘텐츠 인코딩 방식이다.
위 예시에서는 gzip 압축이 사용되었음을 알린다.
```

- 클라이언트는 **Content-Encoding** 헤더를 통해 어떤 방식으로 데이터를 디코딩해야 할지 알 수 있게 된다.
  - ex → 서버가 **gzip**을 사용해서 클라이언트는 데이터를 **gzip**으로 해제하여 원본 콘텐츠를 얻을 수 있다는 사실을 알게 된다.

### 6.6.3 Content-Language
```cpp
**Content-Language: de, en**

이 문서는 독일어와 영어 사용자 모두를 대상으로 한다는 의미
```

- 문서가 어떤 언어로 작성되었는지를 나타낸 것
- 여러 언어 태그를 지정할 수 있다.
- 이 헤더를 포함하지 않거나, 언어를 미지정할 경우, 웹 페이지나 리소스가 특정 언어를 따르지 않으며, 언어와 관계없이 모든 사용자에게 제공될 수 있음을 의미

### 6.6.4 Content-Length
```cpp
Content-Length: <length>
```

- 메시지 본문의 크기를 바이트 단위로 전달한다.
- 메시지 본문의 끝을 확인하고, 데이터를 적절히 처리할 때 유용하다.

### 6.6.5 Content-Location
```cpp
Content-Location: <url>
```

- 콘텐츠 협상 후 리소스를 접근할 수 있는 직접적인 URL 제공
- 추후에는 콘텐츠 협상을 하지 않고 바로 해당 리소스 요청 가능

**콘텐츠 협상(Content Negotiation)**  
클라이언트가 요청하는 데이터 형식에 따라 서버가 적합한 형식을 선택해 제공하는 과정

**Content-Location과 Location의 차이점**
- Content-Location는 서버가 콘텐츠 협상을 통해 여러 형태(언어, 형식 등) 중 하나의 리소스를 제공할 때, 클라이언트에게 이 리소스를 접근할 수 있는 정확한 URL을 알려주는 역할
- Location 헤더는 리디렉션을 위한 URL을 알려주거나, 새로운 리소스가 생성된 경우 그 리소스의 URL을 클라이언트에게 알려주는 역할

**사용 예시**
- 문서의 URL이 `https://example.com/documents/foo`일 경우, 요청의 `Accept` 헤더에 따라 `Content-Location` 헤더가 다르게 설정될 수 있다.

```cpp
요청 헤더 / 응답 헤더 예시:
요청 헤더: Accept: application/json, text/json
응답 헤더: Content-Location: /documents/foo.json

요청 헤더: Accept: application/xml, text/xml
응답 헤더: Content-Location: /documents/foo.xml

요청 헤더: Accept: text/plain, text
응답 헤더: Content-Location: /documents/foo.txt
```

- 클라이언트는 `Accept` 헤더를 사용해 원하는 콘텐츠 형식을 서버에 알린다.
- 서버는 이를 바탕으로 적합한 형식으로 응답하며, `Content-Location` 헤더를 통해 리소스의 정확한 URL을 알려준다.
- 클라이언트는 그 URL을 기억하고, 이후에는 콘텐츠 협상 없이 직접 해당 URL을 요청할 수 있다.

### 6.6.6 Content-MD5
- HTTP 메시지에서 콘텐츠의 무결성을 검증하는 데 사용되는 헤더
- MD5는 해시 함수 중 하나로, 데이터를 고정된 길이의 해시 값으로 변환하여 원본 데이터의 변경 여부를 확인
  - 송신자는 콘텐츠의 MD5 해시 값을 계산하여 이 값을 `ContentMD5` 헤더에 포함시키고, 수신자는 동일한 방식으로 콘텐츠의 MD5 값을 계산한 후 이를 비교하여 데이터의 무결성을 확인
- 데이터 무결성을 확인하는 간단하고 효율적인 방법이지만, 보안이 중요한 환경에서는 더 강력한 해시 알고리즘을 사용하는 것이 좋다

**사용 예시**  
- **파일 업로드 및 다운로드**
  - 클라이언트가 서버에 파일을 업로드할 때, `ContentMD5` 헤더를 사용하여 파일의 무결성을 확인
  - 서버는 이 값을 이용해 전송된 파일이 정확히 도착했는지 확인
- **응답 검증**
  - 서버에서 클라이언트로 콘텐츠를 응답할 때, `ContentMD5` 헤더를 포함시켜 클라이언트가 전송된 데이터가 손상되지 않았는지 검증

**한계**  
- MD5 해시 값이 충돌을 일으킬 수 있기 때문에 암호화된 메시지나 해시 검증에 대한 보안 요구 사항이 높은 경우에는 SHA-256과 같은 더 안전한 해시 알고리즘이 선호된다.

### 6.6.7 Content-Range
```cpp
Content-Range: <unit> <range>/<size>
Content-Range: <unit> <range>
Content-Range: <unit> <size>
```

- 서버가 반환하는 데이터의 일부가 전체 데이터에서 어디에 해당하는지를 알려주는 정보
  - ex → 100MB짜리 파일이 있고, 그 중 일부만 요청 시, 요청된 데이터가 전체 파일에서 어느 부분인지를 알려준다.

**상태 코드**  
- **206 Partial Content**
  - 요청한 데이터의 일부만 반환할 때 사용
  - ex → 0-9999 바이트 요청할 경우, 서버는 206 Partial Content와 함께 응답하고, Content-Range 헤더에 "bytes 0-9999/20000"처럼 전체 크기와 범위를 알려준다.
- **416 Range Not Satisfiable**
  - 요청한 범위가 잘못되었을 때 사용
  - ex → 20000-30000 바이트를 요청했을 경우에, 파일이 15000 바이트밖에 없으면, 서버는 416 상태 코드와 함께 요청 범위가 불가능하다는 것을 알려준다.

### 6.6.8 Content-Type
```cpp
Content-Type: <media-type>
Content-Type: text/html; charset=utf-8
Content-Type: multipart/form-data; boundary=ExampleBoundaryString**
```

- 리소스가 원래 가지고 있는 미디어 타입을 나타낸다.
- 리소스가 어떤 형식의 데이터인지(예: 텍스트, 이미지, 비디오 등) 클라이언트에게 알려준다.
- 응답과 요청에서 다르게 사용된다.

**요청**  
- 메서드 요청을 보낼 때, 클라이언트는 Content-Type 헤더를 사용하여 서버로 보내는 데이터의 형식을 지정
  - 클라이언트가 서버로 JSON 데이터를 보낸다면, 요청 헤더에 `Content-Type: application/json`을 포함

**응답**  
- 서버가 반환하는 데이터의 형식을 클라이언트에게 알린다.
  - JSON 데이터를 반환하면 `Content-Type: application/json`

### 6.6.9 Expires
```cpp
**Expires: <day-name>, <day> <month> <year> <hour>:<minute>:<second> GMT

ex -> Expires: Wed, 21 Oct 2025 07:28:00 GMT 
해당 리소스가 2025년 10월 21일 07:28:00 GMT 이후에 만료된다고 표시
```

- HTTP 캐싱에서 응답이 만료된 시간을 정의
- 리소스가 언제 만료되는지를 나타낸다.
- Expires: 0은 리소스가 이미 만료되었음을 나타내고, 클라이언트는 새로 데이터를 요청해야 한다.
- Expires 헤더는 HTTP/1.0에서 주로 사용되며, HTTP/1.1에서는 Cache-Control 헤더가 더 널리 사용된다.
  - Cache-Control은 Expires보다 더 많은 제어 옵션을 제공
  - Expires와 Cache-Control은 함께 사용될 수 있다.

### 6.6.10 Last-Modified
```cpp
**Last-Modified: <day-name>, <day> <month> <year> <hour>:<minute>:<second> GMT**
```

- 리소스가 마지막으로 수정된 시간을 나타낸다.
- 조건부 요청에서 유효성 검사기로 사용된다.
  - ex → 클라이언트가 이미 저장한 리소스와 요청한 리소스가 같은지 확인할 때 사용

**조건부 요청에서의 사용**  
If-Modified-Since 또는 If-Unmodified-Since와 함께 사용되어, 요청한 리소스가 마지막 수정 이후 변경되었는지 또는 수정되지 않았는지를 확인하는 데 사용

- **If-Modified-Since**
  - 클라이언트가 보낸 Last-Modified 날짜 이후에 리소스가 수정되었는지 확인하려면, 서버는 리소스의 수정 시간이 이 날짜 이후인 경우에만 해당 리소스를 다시 전송
- **If-Unmodified-Since**
  - 클라이언트가 보낸 Last-Modified 날짜 이후에 리소스가 변경되지 않았는지 확인하려면, 서버는 리소스가 수정되지 않은 경우에만 요청을 처리

**ETag와의 차이점**  
- Last-Modified는 리소스의 수정 시점을 기준으로 처리하기 때문에, 실제로 어떻게 변경되었는지를 정확하게 알 수 없다.
- ETag는 리소스의 내용을 나타내는 고유한 값(보통 해시값)으로, 리소스의 변경 여부를 더 정확히 판단할 수 있다.


## 6.7 쿠키를 위한 헤더 필드
- 서버가 사용자의 웹 브라우저로 보내는 작은 데이터 조각
- 브라우저는 쿠키를 저장하고, 새 쿠키를 생성하거나 기존 쿠키를 수정하여 나중에 요청 시 서버로 다시 전송할 수 있다.
- 웹 애플리케이션이 제한된 양의 데이터를 저장하고 상태 정보를 기억할 수 있다.
- 유저 식별과 상태 관리에 사용되고 있는 기술

### 6.7.1 Set-Cookie
```cpp
Set-Cookie: <cookie-name>=<cookie-value>
Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>
Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>
Set-Cookie: <cookie-name>=<cookie-value>; HttpOnly
Set-Cookie: <cookie-name>=<cookie-value>; Max-Age=<number>
Set-Cookie: <cookie-name>=<cookie-value>; Partitioned
Set-Cookie: <cookie-name>=<cookie-value>; Path=<path-value>
Set-Cookie: <cookie-name>=<cookie-value>; Secure

Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Strict
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Lax
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=None; Secure

// Multiple attributes are also possible, for example:
Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>; Secure; HttpOnly
```

- 서버에서 사용자 에이전트(브라우저)로 쿠키를 보내는 데 사용
- 여러 개의 쿠키를 보내려면, 각 쿠키에 대해 별도의 `Set-Cookie` 헤더를 포함해야 한다.

**Expires**
- 쿠키의 만료 날짜를 HTTP 날짜 형식으로 정의
- 설정하지 않으면 세션 쿠키로 취급되며, 클라이언트가 종료될 때 삭제

**Path**
- 쿠키가 전송될 URL의 경로를 정의합니다. 이 경로에 해당하는 요청에서만 쿠키가 전송
  - 예를 들어, `Path=/docs`는 `/docs`, `/docs/`, `/docs/Web/` 경로에서 쿠키를 보낸다.

**Domain**
- 쿠키를 전송할 도메인을 정의
- 도메인 값을 설정하면 해당 도메인 및 모든 하위 도메인에서 쿠키를 사용할 수 있다.
- 여러 하위 도메인(예: `www.example.com`, `shop.example.com`)에서 동일한 쿠키를 공유하고 싶을 때 `Domain` 속성을 설정
- 특정 도메인에서만 유효하도록 하여, 다른 도메인에서는 접근할 수 없도록 제한

**Secure**
- HTTPS 요청에서만 쿠키가 서버로 전송
- 이를 통해 중간자 공격을 방지

**HttpOnly**
- JavaScript에서 쿠키에 접근할 수 없도록 설정
  - 예를 들어, `document.cookie`를 통한 접근을 막는다.
- XSS 공격을 방지하는 데 도움이 된다.
- 이 속성이 부여된 쿠키는 JS [document.cookie]에서 읽어들일 수 없다.

### 6.7.2 Cookie
```cpp
Cookie: <cookie-list>
Cookie: name=value
Cookie: name=value; name2=value2; name3=value3
```


## 6.8 그 이외의 헤더 필드
### **6.8.1 X-Frame-Option**
- 브라우저가 페이지를 `<frame>`, `<iframe>`, `<embed>`, 또는 `<object>`로 렌더링할 수 있는지 여부를 나타내는 데 사용
- 웹사이트는 이를 사용하여 클릭재킹(clickjacking) 공격을 방지
  - 자사 콘텐츠가 다른 사이트에 삽입되지 않도록 할 수 있다.

**DENY**  
  - 페이지가 다른 사이트에서 로드되었을 때뿐만 아니라 동일한 사이트에서 로드될 때도 프레임에 로드되는 시도가 실패  

**SAMEORIGIN**  
  - 페이지가 프레임에 포함된 사이트가 페이지를 제공하는 사이트와 동일한 경우에만 프레임에 표시  

**ALLOW-FROM origin (Deprecated)**  
  - 더 이상 사용되지 않으며, 대신 Content-Security-Policy의 `frame-ancestors`를 사용해야 한다.  

### 6.8.2 X-XSS-Protection
- 이 기능은 더 이상 권장되지 않는 옵션, 비표준 기능
- 최신 브라우저에서는 Content-Security-Policy를 사용하여 XSS 공격을 방지하는 것이 더 효과적

### **DNT(Do Not Track)**
- 개인 정보 수집을 거부하는 의사를 나타내는 요청 헤더
- DNT는 더 이상 권장되지 않으며, 더 이상 표준에 포함되지 않는다.
- Global Privacy Control (GPC)가 DNT를 대체하며, `Sec-GPC` 헤더를 사용하여 서버와 통신

### **P3P(Platform for Privacy Preferences)**
- 웹사이트가 개인정보 보호 정책을 사용자에게 알리기 위해 사용하는 HTTP 헤더
- XML 형식으로 개인정보 수집 및 처리 방침을 정의하고, 사용자가 웹사이트의 개인정보 보호 방침을 쉽게 이해할 수 있도록 돕는다.
- P3P는 더 이상 사용되지 않으며, 대신 **CSP**와 **GPC**가 개인정보 보호를 위한 최신 기술로 대체







