## 네트워크

- [www.~.com에](http://www.%7E.xn--com-568n/) 접속할 때 생기는 과정에 대해 설명해주세요.(웹 동작 방식 이해)
    - 웹 브라우저는 캐싱된 DNS기록들을 통해 해당 도메인 주소와 대응하는 IP 주소 확인
    - 웹 브라우저가 HTTP를 사용해 DNS에게 입력된 도메인 주소를 요청
    - DNS가 웹 브라우저에게 찾는 사이트의 IP주소를 응답
    - 웹 브라우저가 웹 서버에게 IP주소를 이용해 html 문서 요청
    - 웹 애플리케이션서버(WAS)와 데이터베이스에서 우선 웹페이지 작업을 처리
    - 작업처리 결과를 웹서버로 전송
    - 웹 서버는 웹브라우저에게 html 결과 응답
    - 웹 브라우저는 화면에 내용물 출력

---

질문

1. 요청에 캐시가 없다면 어떻게 동작하나요?

---

- 3-way handshake에 대해 설명해주세요.(TCP 연결)
    - TCP/IP 프로토콜을 이용해 통신하는 응용프로그램이 데이터를 전송하기 전에 먼저 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정
        - Client → Server : TCP Synchronize sequence numbers - 연결 확인을 위해 보내는 무작위의 숫자 값
            - SYN이 무작위인 이유
                - Connection 시 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용
                    - 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용할 가능성이 높음
                - 이전 Connection으로부터 오는 패킷으로 인식할 수 있기 때문에 ISN을 무작위 난수로 사용
                    - ISN(Initial sequence numbers) - Client와 Server가 각각 처음 생성한 SYN
        - Server → Client : TCP Synchronize sequence numbers, Acknowledgement - SYN에 1을 더해 잘 받았다는 ACK
        - Client → Server : TCP Acknowledgement
        
    - 역할
        - 양쪽 모두 전송 준비가 됬다는 것을 보장
        - 데이터 전달 전 다른쪽이 준비 되었다는 것을 알 수 있도록 함
        - 양쪽 모두 상대편에 대한 초기 순차 일련번호를 얻을 수 있도록 함
---

질문

1. TCP vs UDP
2. 순서보장
    - 데이터가 안오면 데이터 재전송
        - timeout이 발생하면 서버에서 재전송함

피드백

- TCP/IP 보단 TCP가 더 좋을 듯
    - 3 way handshake는 TCP에서만 발생

---

- HTTP/2를 설명하고 장점 두가지를 말해보세요.
    - HTTP/1.1에서 성능을 집중적으로 개선한 것
        - HTTP1.1의 핵심개념(Method, status code, URI, Header 등)은 그대로 유지됨
    - HTTP 메시지를 1.1에서는 text로 전송되었다면 2.0에서는 Binary frame으로 인코딩되어 전송됨
        - HTTP/2.0 부터는 헤더와 바디가 Layer로 구분됨
    - Multiplexing
        - HTTP 헤더 메시지를 바이너리 형태의 프레임으로 나누고 하나의 커넥션으로 동시에 여러 개의 메시지스트림을 응답 순서에 상관없이 주고 받음
        - 이를 통해 Latency만 줄여주는것이 아니라 네트워크를 효율적으로 사용할 수 있게 했고, 네트워크 비용 감소
    - 클라이언트 요청에 대해 미래에 필요할 것 같은 리소스를 파악해 클라이언트에게 미리 push 해 브라우저의 캐시에 가져다놓음
        - 요청하지도 않은 리소스를 미리 보내 특정 개체가 필요할 때 바로 사용하도록 성능 향상
            - 필요 리소스를 다시 요청하는 트래픽 감소
    - Stream Prioritization
        - 클라이언트는 우선순위 지정트리를 사용해 스트림에 식별자를 설정함
            - 각각의 스트림은 1~256의 가중치를 지님
            - 하나의 스트림은 다른 스트림에게 명확한 의존성을 가짐
        - 클라이언트는 서버에게 스트림 보낼 때 가중치 우선순위를 지정해 전송
        - 요청받은 서버는 우선순위가 높은 응답이 클라이언트에 우선적으로 전달될 수 있도록 대역폭 설정
        - 응답 받은 각 프레임에는 이것이 어떤 스트림인지에 대한 고유한 식별자가 있어 클라이언트는 여러 스트림을 interleaving을 통해 서로 끼워놓으며 조립
    - HTTP Header Data Compression
        - HTTP 메시지의 헤더를 압축하여 전송
            - 이전 메시지의 헤더 내용 중 중복되는 필드는 재전송하지 않도록 설정됨
                - 중복값 존재할 경우 중복헤더 검출 후 중복된 헤더는 index 값만 전송, 중복되지 않은 헤더는 호프만인코딩 기법을 사용하는 HPACK압축방식으로 인코딩 처리


---

질문

1. HTTP/1.1에서도 여러개의 요청을 받을 수 있는데 HTTP/2와 차이점이 뭔가요
    1. 병렬성

피드백

- 병렬성 강조

---

- DNS에 대해 설명해주세요.
    - Domain Name System
    - 원래의 IP주소를 기억하기 쉬운 도메인으로 바꾸거나 도메인을 다시 IP주소로 바꿔주는 데이터베이스 시스템
    - 연결되어있는 IP 주소와 도메인이 저장된 곳이 DNS
    - 각 도메인마다 DNS와 연결해주는 서버 역할을 하는 DNS 서버(네임서버)가 존재
    - 작동방식
        - ~.com 입력
        - ~.com을 가진 네임 서버 접속
        - IP주소 확인
        - IP 주소 전달
        - IP 주소를 가진 서버로 접속

- CORS란 무엇이며 동작과정을 설명해보세요.
    - 브라우저는 보안적인 이유로 cross-origin HTTP 요청을 제한함
    - cross-origin 요청을 하기 위해선 서버의 동의가 필요
        - 서버 동의 시 요청을 허락
        - 서버 동의 매커니즘을 HTTP header를 이용해서 가능
    - 동작방식
        - Simple request
            - Simple request란
                - HTTP method: GET, HEAD, POST 중 하나
                - 설정할 수 있는 다음 헤더들만 변경
                    - Accept, Accept-Language, Content-Language
                - Content-type이 다음과 같은 경우
                    - application/x-www-form-urlencoded
                    - multipart/form-data
                    - text/plain
            - 서버로 요청
            - Origin과 응답한 헤더 Access-Control-Request-Headers의 값을 비교해 유효한 요청이면 리소스 응답
                - 유효 X면 브라우저에서 막고 에러 발생
        - preflight 요청
            - preflight란
                - Simple request가 아닌 cross-origin은 모두 preflight
                - 실제요청을 보내는 것이 안전한지 확인하기 위해 OPTIONS 메서드를 사용해 cross-origin 요청을 보냄
                    - 데이터에 영향을 미칠 수 있는 요청이므로 사전에 확인 후 본요청 전송
            - Origin 헤더에 현재 요청하는 origin과, Access-Control-Request-Method 헤더에 요청하는 HTTP method와 Access-Control-Request-Headers요청 시 사용할 헤더를 OPTIONS 메서드로 서버에 요청
                - 내용물 없이 헤더만
                - 요청 헤더
                    - origin
                    - Access-Control-Request-Method
                    - Access-Control-Request-Headers
            - 브라우저가 서버에서 응답한 헤더를 보고 유효한 요청인지 판단
                - 유효 X 면 중단, 에러 발생
                - 유효 O 면 원래 보내려던 요청을 다시 요청해 리소스 응답받음

---

질문

1. 유효한 요청인지 어떻게 판단하나?
2. CORS 왜 발생하나?

피드백

- Simple Request 요청에 부합하면 preflight가 요청가지 않음
- Server to Server는 CORS가 발생하지 않음

---

- HTTP Method와 각각이 사용되는 경우에 대해서 설명해주세요.
    - GET : 리소스 조회
        - POST도 조회 가능하지만 GET은 캐싱이 가능해 유리
    - POST : 요청 데이터 처리
        - 주로 등록에 사용됨
    - PUT : 리소스 대체(덮어쓰기)
        - 리소스 없으면 생성
        - 데이터를 대체하기 위해 클라이언트가 리소스의 구체적인 전체 경로를 지정해 보내야 함
    - PATCH : 리소스 부분 변경
        - PUT이 전체 변경, PATCH는 일부 변경
    - DELETE : 리소스 삭제
    - HEAD : GET과 동일하지만 메시지 부분을 제외하고 상태 줄과 헤더만 반환
        - 리소스 안받고 응답코드만 확인하고 싶을 때
    - OPTIONS : preflight에 사용되는 Method
        - CORS에서 사용
        - 서버의 지원 가능한 HTTP Method와 출처를 응답받아 CORS를 검사하기 위함
    - CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정
    - TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트 수행
        - 검사용 메서드

---

질문

1. 멱등성(→ 서버 자원 기준)
    1. DELETE는 멱등성!?
    2. PUT 멱등성
2. POST와 PUT 요청은 내부적으로 다른 로직인가요?

---

- HTTP와 HTTPS의 차이점은 무엇인가요?
    - HTTP의 확장버전이 HTTPS
    - HTTP는 클라이언트와 서버 간 통신을 위한 통신 프로토콜
        - 사용자가 웹사이트 방문 시 HTTP 요청 전송
        - 웹서버는 HTTP 응답으로 응답
            - 이때 웹서버와 사용자는 일반 텍스트로 교환
    - HTTPS는 기본적인 HTTP 요청 및 응답에 SSL 및 TLS 기술 결합
    - 보안적인 부분 뿐 아니라 HTTPS가 HTTP 보다 로드 속도가 빠르며 트래픽 추적이 용이함

---

질문

1. 데이터 암호화는 인증서가 아님
    1. 인증서는 여기는 안전한 서버다를 아는 용도

---

- GET과 POST의 차이점은 무엇인가요?
    - 데이터 길이 제한
        - GET요청의 경우 길이 제한이 있지만
        - POST의 경우 BODY에 메시지를 담아 전송하는데, BODY는 길이제한 없이 데이터 전송 가능
    - 요청 헤더
        - POST는 반드시 Content-Type에 요청 데이터의 타입을 표시해야 함
    - 멱등성
        - GET요청은 리소스를 조회하기 때문에 여러 번 요청하더라도 응답이 같음
        - POST요청은 리소스를 새로 생성하거나 업데이트할 때 사용되기 때문에 멱등이 아니라고 볼 수 있음

---

질문

1. 실제로 GET 메서드를 사용한 적이 있나요
    1. GET요청 시 Query String만 사용하셨나요?
        1. pass variable도 있음
            1. 이건 언제쓰나요?
2. GET 요청에 Body 넣어서 할 수 있나요?
    1. 왜 근데 사용 안하나요?

---