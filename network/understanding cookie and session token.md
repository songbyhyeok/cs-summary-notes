# intro
요청 인증 방식에는 쿠키, 세션, 토큰이 대표적

## why authentication is required?
인증을 통한 보안, 신뢰성, 서비스
1. 서버가 요청의 적합성을 확인해 자원 탈취와 데이터 유출을 방지
2. 클라이언트를 식별하여 개인화된 데이터와 서비스를 제공
3. 인증된 사용자는 맞춤형 서비스, 정보를 지속적 제공

## cookie
브라우저 옵션 사용자 정의, 인증 목적의 브라우저에 저장되는 key-value 구조  

### advantage
데이터 식별과 상태 저장에 유용하다.

### disadvantage
* xss(cross-site-scripting)의 유출, 조작 위험성
* 용량이 제한적
* 브라우저에 따라 쿠키 호환성 문제
* 쿠키 크기 비례 네트워크 부하율

### auth method
요청 시 서버는 응답 헤더에 포함된 Set-Cookie 인증 정보를 함께 전송, 이후 요청 시 쿠키를 요청 헤더에 포함시켜야 서버가 식별 가능.

## session
유출, 조작 보완 목적으로 서버측 메모리 or DB에 저장 및 관리 방식

### advantage
사용자 정보를 관리하는 stateful

### disadvantage
* session id 탈취 및 위장 해킹 가능성
* 요청 수에 따라 서버 부하, 확장의 어려움

### auth method
![Image](https://github.com/user-attachments/assets/f5dd8983-55f3-4715-8e2a-3955dcdd80da)  
[출처: [JWT] 토큰(Token) 기반 인증에 대한 소개](https://velopert.com/2350)  

서버에 세션을 저장하고, 세션 ID를 쿠키로 클라이언트에 전달하여 이후 요청 시 세션 ID로 인증을 수행

## token
* 서버만 해독할 수 있는 암호화된 문자열로 클라이언트에게 발급된다.
* mobile APP, SPA(single page application) 주로 사용
* OAuth 2.0 protocol에서 토큰 기반 인증 방식으로 채택 중

### advantage
* https 통한 유실 및 유출의 낮은 가능성
* stateless 의한 낮은 유지보수성과 높은 확장성

### disadvantage
* 데이터 크기에 비례한 암호화된 길이로 인한 해독 과정 중 오버헤드
* 암호화되지 않은 payload
* 토큰 탈취되면 만료될 때까지 통제 불가

### auth method
![Image](https://github.com/user-attachments/assets/f91bfa9e-ab7e-4716-9f01-b8c35feb82dc)  
[출처: [JWT] 토큰(Token) 기반 인증에 대한 소개](https://velopert.com/2350)  

서버가 생성한 고유 토큰을 클라이언트가 쿠키나 스토리지에 저장한 후, 요청 시마다 http 요청 header에 포함시켜 전송. 서버는 토큰 내부 데이터를 통해 해독 및 검증 수행

<br>

# reference
- [쿠키 및 세션 토큰 이해하기](https://songbyhyeok.github.io/network/understanding-cookies-and-session-tokens/)
