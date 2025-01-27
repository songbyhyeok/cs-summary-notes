
# what is the proxy server ?
<img src="https://github.com/user-attachments/assets/55525dce-eb32-46bd-8b48-752d2a572180" style="width: 80%; height: auto">

자체 IP 주소를 사용하여, 클라이언트와 웹 서버 간의 중개 목적의 게이트웨이

## how does it work ?
1. ISP를 통해 웹 서버에 연결을 설정하고, 프록시는 사용자 IP를 은닉한 후 자체 IP를 사용하여 웹 서버에 전달
2. 웹 서버에서 응답 값을 프록시에게 반환.
3. 응답 값 보안 검사 후에 클라이언트에게 전달.

## keypoints
* **제어와 관리**  
요청 및 응답 간 (방화벽, 모니터링 시스템) 제공, 프록시 유형과 프로토콜 종류에 따라 추가 기능적 보안 제공.  
* **위치 기반 브라우징 전략**  
특정 지역.국가에 우회 및 접근 가능한 비즈니스 제공  
* **IP 익명**  
클라이언트 IP 은닉 후 자체 IP 사용, 이를 통해 익명성 보장과 광고.수집으로부터 보호  
* **캐싱**  
자주 방문하는 사이트를 캐싱하여 트래픽과 대역폭을 최적화  

## disadvantage
* **데이터 유출**  
전송 데이터, 로그 일부 데이터는 암호화 처리가 되어있지 않아, 유출 가능성  
* **불완전한 네트워크**  
무료로 사용 가능한 상용 프록시는 비교적 보안과 성능에 취약  
* **제한적 기능**  
앱 개별적 작동 및 설정이 동반되기 때문에 기능이 제한적  

## types of proxy
### forward proxy
<img src="https://github.com/user-attachments/assets/1169b4f0-4bf9-489e-aa77-2a8d4b3d673d" style="width: 80%; height: auto">

클라이언트 뒤에 위치하며, 클라이언트와 웹 서버 간 중개 역할을 수행하는 클라이언트 측 서버

### reverse proxy
<img src="https://github.com/user-attachments/assets/fa5e24b6-61e5-439b-9d47-e6660911e0b4" style="width: 80%; height: auto">

웹 서버 앞에 위치하며, 클라이언트로부터 오는 요청을 전달하는 서버측 서버  

**how does it work?**  
```
1. 클라이언트가 웹 서비스에 요청  
2. 리버스 서버가 이를 가로채고, 서버의 구조, 부하, 라우팅 규칙 등을 고려하여 요청을 처리할 백엔드 서버를 결정 후 분배 
3. 백엔드 서버가 처리 후, 응답을 프록시로 전송 
4. 리버스 서버가 응답을 클라이언트에게 전달  
```

**structural benefits**  
```
* 서버 익명화
* 로드밸런싱
* 모니터링 시스템
* 네트워크 트래픽 흐름 관리
* 캐싱
* DDos 방어
* 콘텐츠 스트리밍
```
<br>