## 제1장 웹과 네트워크의 기본에 대해 알아보자
### 1.1 웹은 HTTP로 나타낸다.
**Protocol**
- 같은 방식으로 통신할 때, 약속이나 규칙

**HTTP(HyperText Transfer Protocol)**
- 클라이언트와 서버까지의 통신 프로토콜

### 1.2 HTTP는 이렇게 태어났고 성장했다.
**WEB**
- 지식 공유 목적으로 기술 개발 중, 고안되어 탄생

**HyperText**
- 상호간 참조 가능한 텍스트

**WWW**
- WEB이라 불리는 정보 공유 시스템을 일컫는 말
- 구성 기술
    1. HTML
        1. SGML 베이스의 문서 기술 언어
    2. HTTP
        1. 문서 전송 프로토콜
    3. URL
        1. 문서 주소 지정 방법

### 1.3 네트워크의 기본은 TCP/IP
**TCP/IP**
- IP 프로토콜 기반의 통신 프로토콜 집합
- Layer 4 (app, transport, network, link)
  - 모듈(layer) 구조로서의 확장/유지/관리 가능

**App Layer**
- 클라이언트 측의 통신
    - FTP, DNS, HTTP

**Transport Layer**
- 2개의 프로토콜 TCP/UDP 지원
- 클라이언트와 서버 사이의 데이터 흐름 제공
- IP가 패킷을 어떤 경로를 거쳐 도착지까지 전달할지 결정

**Link Layer**
- 네트워크 장비(HW) 간에 데이터를 전송하는 역할을 수행
  - device driver, nic

**TCP/IP 통신의 흐름**  
![Image](https://github.com/user-attachments/assets/bee04cfc-1bca-4da3-a2ce-7196d0717128)  
![Image](https://github.com/user-attachments/assets/4933a719-e37c-4f08-9e93-567dbecb83f8)  
출처: https://inpa.tistory.com/329  
<br>

**클라이언트 to 서버**
- **트랜스포트 계층**
  - http 메시지를 조각내서 안내 번호와 포트 번호를 붙여 네트워크 계층에 전달

- **네트워크 계층**
  - 수신지 MAC 주소를 추가해서 링크 계층에 전달

**서버 to 클라이언트**
- **캡슐화 & 역캡슐화 (encapsulation & decapsulation)**
  - **캡슐화란?**
    - 필요한 데이터(헤더)를 추가해 나가는 것
  - **캡슐화 이유**
    - 다른 네트워크와 통신하기 위해
  - **역캡슐화**
    - 수신측에서 헤더를 걷어내가는 과정

## 1.4 HTTP와 관계가 깊은 프로토콜은 IP/TCP/DNS
**IP**
- 네트워크 계층에 해당
- 패킷을 전달하는 기술

**MAC**
- NIC 고유 식별 주소

**ARP**  
![Image](https://github.com/user-attachments/assets/dee185a9-d787-479f-9864-c61cfec4ea9a)  
출처: https://code-boki.tistory.com/23  
- 단말 간 통신하기 위해서는 IP와 MAC 주소를 매핑해야 하는데, 이를 대신 수행한다.

**라우팅**
- 어떤 네트워크 안에서 통신 데이터를 보낼 때 최적의 경로를 선택하는 과정

**TCP**
- Transport Layer에 위치
- byte stream service 제공
  - 큰 데이터를 “tcp 세그먼트” 단위 패킷으로 분해하여 관리
  - 데이터의 중복이나 손실 없이 종단간 데이터의 전송을 보장하기 위함

**3-way Handshake**
- **목적**: Byte stream 서비스에서 데이터를 정확하게 전송하기 위한 연결 설정 기술
- **과정**:
  1. **송신측**: 데이터 전송을 시작하기 위해 ‘SYN’ 플래그를 설정하여 수신측에 접속 요청
  2. **수신측**: 송신측의 요청을 받고, 연결을 수락하며 ‘SYN/ACK’ 플래그로 응답
  3. **송신측**: 수신측의 응답을 확인하고, ‘ACK’ 플래그를 보내 연결이 완료됨을 통보

이 과정을 통해 양측은 안정적인 데이터 전송을 위한 연결을 설정

## 1.5 이름 해결을 담당하는 DNS
- 도메인 명에서 IP 주소로 조사하거나, IP 주소에서 도메인 명을 조사하는 서비스

## 1.6 각각과 HTTP와의 관계
**IP, TCP, DNS, HTTP**
1. **HTTP** 메시지 작성 및 리소스 요청
2. **TCP** HTTP 메시지를 패킷으로 분해, 조각내서 일련번호를 부여 및 상대방에게 패킷을 보낸다.
3. **IP** ARP를 통해 IP 주소와 MAC 주소를 매핑하여 라우터를 통해 전달
4. **TCP** 담당 상대방으로부터 패킷을 수신, 일련번호를 보고 조립
5. **HTTP** 웹 서버에 대한 요청 내용을 처리

## 1.7 URI와 URL
![Image](https://github.com/user-attachments/assets/5a00793d-e369-46a7-9382-9a6d559a7fdf)  
![Image](https://github.com/user-attachments/assets/0f46caf0-ff63-483b-b508-2053152eb2e5)  
출처: https://hstory0208.tistory.com/entry/URI%EC%99%80-URL-%EB%B9%84%EC%8A%B7%ED%95%B4%EB%B3%B4%EC%9D%B4%EB%8A%94%EB%8D%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%B4-%EB%AD%98%EA%B9%8C-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC

**URI(Uniform Resource Identifier)** 
- 자원 식별자
- 인터넷에서 요구되는 기본조건으로서 인터넷 프로토콜에 항상 붙어 다닌다.
- 하위개념으로 URL, URN 이 있다
- **구성**
  - **Uniform**
    - 리소스를 식별하는 통일된 방식
  - **Resource**
    - 자원, URI로 식별할 수 있는 모든 것
  - **Identifier**
    - 다른 항목과 구분하는데 필요한 정보

**URL(Uniform Resource Locator)** 
- 웹 사이트 주소 뿐만 아니라 컴퓨터 네트워크 상의 자원을 모두 나타내는 표기법

**URN(Uniform Resource Name)**
- 리소스에 이름을 부여하는 통합 자원명
- 리소스를 식별하는 이름(URN)만으로는 위치나 접근 방법을 알 수 없다.

**URL 구성요소**
- **<스키마>://<호스트>/<경로>?<쿼리>#<프래그먼트>**
- **스키마 (URL Scheme)**
  - 리소스 접근 방식을 정의
  - 주소의 구조 중에서 프로토콜을 지정하는 부분
    - ex - http://, https://, ftp://, mailto:, file:// 등
  - 각 스키마는 특정한 프로토콜 또는 리소스 유형

- **호스트(Host)**
  - 리소스를 제공하는 서버의 도메인 이름 또는 IP 주소 
    - ex - www.example.com, 192.168.0.1

- **경로(Path)**
  - 서버 내에서 특정 리소스를 나타내는 경로
    - ex - /index.html, /images/pic.jpg

- **쿼리(Query)**
  - URL에 전달할 추가적인 데이터를 나타내는 부분으로, 주로 ?로 시작하고 &로 구분된 키-값 쌍 형태
    - ex - ?id=123&name=example

- **프래그먼트(Fragment)**
  - URL의 특정 부분을 나타내며, 보통 웹 페이지 내의 특정 위치로 이동할 때 사용, # 뒤에 위치 
    - ex -  #section2

**URI, URL 구분**
```
1. http://www.naver.com/index.html?page=123456789&id=123
2. http://www.naver.com/index.html?page=987654321&id=456
```
- 같은 주소이지만, 서로 다른 자원을 식별하고 있기 때문에, 같은 URL 다른 URI
