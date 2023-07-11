# Network

## [www.~.com에](http://www.%7E.xn--com-568n/) 접속할 때 생기는 과정에 대해 설명해주세요.(웹 동작 방식 이해)

<aside>
💡

1. **브라우저 주소창**에 [www.~.com](http://www.%7E.xn--com-568n/)을 입력한다.
2. 브라우저가 [www.~.com](http://www.%7E.xn--com-568n/)의 **IP 주소**를 찾기 위해 **캐시**에서 **DNS 기록**을 확인한다.
3. 만약 요청한 URL이 캐시에 없다면, **ISP의 DNS 서버**에서 **DNS 쿼리로** [~.com](http://www.%7E.xn--com-568n/)을 **호스팅**하는 서버의 IP 주소를 찾는다.
4. 브라우저가 해당 서버와 **TCP 연결**을 시작한다.
5. 브라우저가 웹서버에 **HTTP 요청**을 보낸다.
6. 서버가 요청을 처리하고 **응답**을 보낸다.
7. 서버가 **HTTP 응답**을 보낸다.
8. 브라우저가 **HTML** 콘텐츠를 보여준다.
</aside>

### **1. 브라우저 주소창에 [www.~.com](http://www.%7E.xn--com-568n/)을 입력**

- 브라우저 주소창에 URL 입력 또는 링크 클릭

### **2. 브라우저가 URL의 IP주소를 찾기 위해 캐시에서 DNS기록을 확인**

- 브라우저 캐시
  - 브라우저는 이전에 방문한 웹 사이트의 DNS 기록을 일정 기간 동안 저장
- OS 캐시
  - 브라우저가 컴퓨터 OS에 시스템 호출을 통해 DNS 기록을 가져옴
- 라우터 캐시
  - 라우터의 로컬 네트워크 캐시에서 DNS 기록을 저장한 캐시를 확인
- ISP 캐시
  - ISP(Internet Service Provider)는 **DNS 서버**를 가지고 있는데, 해당 서버에서 DNS 기록 캐시를 검색할 수 있음

### **3. 캐시에 기록이 없다면, ISP의 DNS서버에서 DNS 쿼리로 URL을 호스팅하는 서버의 IP 주소를 찾음**

- **DNS 리커서(DNS Recursor)**에서 **재귀적 질의(Recursive Query)**를 통해 필요한 IP 주소를 찾거나, 찾을 수 없다는 오류 응답을 반환할 때까지 한 DNS 서버에서 다른 DNS 서버로 검색을 반복

![](./image/ghs_dns.png)

<aside>
🤚 **DNS 리커서(DNS Recursor)**
ISP의 DNS 서버를 **DNS 리커서(DNS Recursor)**라고 부르는데, DNS 리커서는 인터넷의 다른 DNS 서버에 답변을 요청하여 URL의 적절한 IP 주소를 찾는 일을 담당한다. 다른 DNS 서버는 도메인 아키텍처를 기반으로 DNS 검색을 수행하므로 **네임 서버(Name Server)**라고 한다.

</aside>

### **4. 브라우저가 해당 서버와 TCP 연결을 시작**

- 브라우저가 올바른 IP 주소를 수신하면 **TCP(Transmission Control Protocol)** 라는 **전송 제어 프로토콜**을 사용하여 연결을 구축

### **5. 브라우저가 웹 서버에 HTTP 요청을 보냄**

- 페이지의 컨텐츠를 요청하기 위해 서버에 HTTP 요청을 전송

<aside>
🤚 ****HTTP 요청 구성요소****

- 요청 라인
- HTTP의 요청 라인에 클라이언트가 수행하려는 작업에 대한 정보를 포함
  `GET /blog/hello-world HTTP/1.1`
- 요청 헤더
  `Host: 호스트`
  `User-Agent: 사용자 에이전트
    Accept: 클라이언트가 이해 가능한 컨텐츠 타입이 무엇인지를 나타냄`
- 본문
</aside>

### **6. 서버가 요청을 처리하고 응답을 보냄**

- 서버에는 **요청을 수신**하고, 해당 내용을 request handler에 전달하여 응답을 읽고 생성하는 역할의 **웹 서버**(예: Apache, IIS)가 포함
- **Request handler**는 요청, 요청의 헤더 및 쿠키를 읽고 필요한 경우 서버의 정보를 업데이트하는 프로그램(NET, PHP, Ruby, ASP 등)
- response를 특정 포맷으로(JSON, XML, HTML)으로 작성

### **7. 서버가 HTTP 응답을 보냄**

- 서버 응답에는 요청한 웹 페이지와 함께 상태 코드(status code), 압축 유형(Content-Encoding), 페이지 캐싱 방법(Cache-Control), 설정할 쿠키, 개인 정보 등이 포함

<aside>
🤚 **상태 코드(Status Code)**

- **1xx (Information Response)**: 정보 메시지만을 나타낸다. 서버가 요청을 받았으며 서버에 연결된 클라이언트는 계속해서 작업을 하라는 뜻.
- **2xx (Successful Response)**: 서버와의 요청이 성공함을 나타냄
- **3xx (Redirection Message)** : 요청 완료를 위해 추가 작업 조치가 필요함을 의미함. 위 사진의 **301(Moved Permantly)**는 요청한 리소스의 URI가 변경 되었음을 뜻한다.
- **4xx (Client Error Response)** : 클라이언트의 Request에 에러가 있음을 의미함.
- **5xx (Server Error)** : 서버 측의 오류로 request를 수행할 수 없음.
</aside>

### **8. 브라우저가 HTML 콘텐츠를 보여줌**

- 응답받은 HTML을 화면에 단계별로 표시
  1. HTML 골격을 렌더링
  2. HTML 태그를 확인하고 이미지, CSS 스타일시트, 자바스크립트 파일 등과 같은 웹 페이지의 추가 요소에 대한 GET 요청
  3. [www.~.com](http://www.%7E.xn--com-568n/) 페이지가 브라우저에 나타남

## 3-way handshake에 대해 설명해주세요.(TCP 연결)

### TCP란?

TCP는 Transport Layer에서 사용되는 프로토콜이다.

TCP는 신뢰성이 높고 연결 지향성 서비스를 제공한다. 그러므로 정보 전달에 있어 안정적으로, 순서대로, 에러 없이 교환할 수 있도록 하는 것에 목적을 둔 프로토콜이다.

이러한 특징으로 장치들 사이에 논리적인 접속을 성립(establish)하기 위하여 handshake를 사용한다. **3-Way Handshake 는 TCP의 접속, 4-Way Handshake는 TCP의 접속 해제 과정이다.**

### 3-Way Handshake 란?

3-Way Handshake는 데이터를 전송하기 전에 정확한 전송을 보장하기 위해 사전에 세션을 수립하는 과정이다.

양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한쪽에서 다른 쪽이 준비되었다는 것을 알 수 있다.

### 플래그 정보

![Handshaking 과정에서 세그먼트에 설정되는 Flag](./image/ghs_flag.png)

Handshaking 과정에서 세그먼트에 설정되는 Flag

### 포트 상태 정보

![3-Way Handshaking 과정에서 포트 상태](./image/ghs_port.png)

3-Way Handshaking 과정에서 포트 상태

### 3-Way Handshake 동작 과정

![3-Way Handshaking 동작 과정](./image/ghs_handshake.png)

3-Way Handshaking 동작 과정

### 1. Client → Server (SYN)

- 서버에 접속을 요청하는 SYN 패킷을 전송한다.
- 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 새그먼트를 전송한다.
- Client는 SYN을 보낸 후 SYN/ACK 응답을 기다리는 SYN_SENT 상태가 된다.

### 2. Server → Client (SYN/ACK)

- LISTEN 상태인 Server가 SYN을 받고, 클라이언트에게 요청을 수락(ACK)했으며 접속 요청 프로세스인 클라이언트도 포트를 열어달라(SYN)는 메시지를 전송한다.
- ACK Number필드를 Sequence Number + 1로 지정하고 SYN과 ACK 플래그 비트를 1로 설정한 새그먼트 전송
- SYN을 받은 서버는 SYN_RECEIVED 상태가 된다.

### 3. Client → Server (ACK)

- 클라이언트는 서버의 응답을 받았다는 의미로, ACK Number필드를 Sequence Number + 1로 지정하고 서버로 ACK 플래그가 설정된 새그먼트를 전송한다.
- ACK 요청을 보낸 클라이언트는 ESTABLISHED 상태가 된다.
- ACK를 받은 서버는 ESTABLISHED 상태가 된다.

### 4-Way Handshake 란?

3-Way Handshake가 세션을 수립하는 과정이었다면 4-Way Handshake는 세션을 종료하기 위해 수행되는 과정이며, 여기서 FIN 플래그를 사용한다.

### 포트 상태 정보

![4-Way Handshaking 과정에서 포트 상태](./image/ghs_port_4way.png)

4-Way Handshaking 과정에서 포트 상태

### 4-Way Handshake 동작 과정

![4-Way Handshaking 동작 과정](./image/ghs_4way_handshake.png)

4-Way Handshaking 동작 과정

### 1. Client → Server (FIN)

- close()가 호출되면 연결을 종료한다는 FIN 패킷을 보낸다.
- FIN 패킷에는 ACK로 포함되어있다.
- FIN 패킷을 보낸 후 FIN_WAIT_1 상태가 된다.

### 2. Server → Client (ACK)

- FIN 패킷을 받은 서버는 응답 패킷 ACK를 보낸다.
- 응답 패킷 ACK를 보낸 후 CLOSE_WAIT 상태가 된다.
- 아직 남은 데이터가 있다면 마저 전송을 마친 후에 close( )를 호출한다.
- 클라이언트는 ACK 패킷을 받은 후 FIN_WAIT_2 상태가 된다.

### 3. Server → Client (FIN)

- 데이터를 모두 보냈다면, 서버는 FIN 패킷을 클라이언트에게 보낸 후에, 승인 번호를 보내줄 때까지 기다리는 LAST_ACK 상태로 들어간다.

### 4. Client → Server (ACK)

- 클라이언트는 FIN 패킷을 받고, 확인했다는 ACK 응답을 보낸다.
- ACK 응답을 보낸 후 클라이언트는 TIME_WAIT 상태가 된다.
- TIME_WAIT 상태는 의도치 않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지한다.
- 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 CLOSED 상태로 들어간다.
- 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed) - 기본 240초

### HTTP/2를 설명하고 장점 두가지를 말해보세요.

HTTP/2는 기존 HTTP/1 의 확장으로 기존의 HTTP/1과의 호환성을 유지하며 성능에 초점을 맞춘 프로토콜입니다. HTTP/2의 장점으로는 Multiplexed Streams와 Binary protocol이 있습니다.

Multiplexed Streams는 기존의 Pipelining과 달리 한 개의 Connection으로 동시에 여러 개의 메시지를 주고 받을 수 있습니다. 즉, 하나의 TCP 연결을 통해 여러 데이터 요청을 병렬로 전송할 수 있습니다. 응답은 순서에 상관 없이 Stream으로 주고 받기 때문에, 훨씬 빠른 속도로 데이터 통신이 가능합니다.

Binary protocol은 기존 HTTP/1에서 사용된 frame의 복잡성을 편리하게 해주고, 텍스트와 공백들이 섞여 혼동이 발생하던 명령들보다 명령어를 단순하게 구현할 수 있습니다. Binary protocol을 사용하면 데이터의 파싱이 더 빠르고, 오류 발생 가능성이 낮아지며 네트워크 지연 시간을 줄이고 처리량을 개선하여 네트워크 리소스를 효과적으로 사용할 수 있습니다.

### DNS에 대해 설명해주세요.

DNS란 사람이 읽을 수 있는 도메인 이름을 IP 주소로 변환하는 시스템입니다. 도메인 이름을 사용했을 때 입력한 도메인을 실제 네트워크상에서 사용하는 IP 주소로 바꾸고 해당 IP 주소로 접속하는 과정이 필요한데, 이러한 과정 전체 시스템을 DNS라고 합니다. DNS는 상위 기관과 하위 기관과 같은 계층 구조를 가지는 분산 데이터베이스 구조를 가지고 있습니다. 그 이유로는 중앙 집중식 서버의 경우 공격을 받거나 문제가 생기면 전체 웹 서비스가 멈출 수 있으므로 계층 구조로 되어있습니다.

### CORS란 무엇이며 동작과정을 설명해보세요.

CORS란 Cross Origin Resource Sharing의 약자로 말 그대로 풀이하면 ‘교차 출처 자원 공유’입니다. 즉, 다른 출처의 자원을 공유한다는 뜻으로 간단히 다른 출처의 자원을 요청하여 사용하고 공유한다는 의미입니다.

CORS의 동작 과정은 Preflight Request, Simple Request, Credentialed Request 3가지가 있습니다.

Preflight Request는 일반적으로 웹 어플리케이션을 개발할 때 가장 흔하고 많이 사용하는 방식으로, 요청을 한번에 보내지 않고 예비 요청과 본 요청으로 나누어서 서버로 전송합니다. 예비 요청에서 OPTIONS 메서드로 요청하며 CORS를 허용하는지 확인 후 본 요청을 보냅니다.

Simple Request는 예비 요청(Preflight)을 보내지 않고 바로 서버에 본 요청을 한 후, 서버가 이에 대한 응답의 헤더에 Access-Control-Allow-Origin을 통해 브라우저가 CORS 정책 위반 여부를 검사하는 방식입니다. 하지만 Simple Request는 이름과 다르게 조건이 복잡하고 많기 때문에 Preflight Request 방식을 가장 많이 사용합니다.

Credentialed Request는 다른 출처간 통신에서 좀 더 보안을 강화하고 싶을 때 사용하는 방식으로, credentials 옵션을 통해 쿠키 정보나 인증과 관련된 헤더의 정보를 담을 수 있습니다. 만약 헤더에 인증 정보가 담긴다면 브라우저는 추가적인 검사를 진행합니다. Access-Control-Allow-Origin에 \*를 사용할 수 없고 명시적인 URL 이어야 하며, 응답 헤더에는 반드시 Access-Control-Allow-Credentials:true가 존재해야 합니다.

### HTTP Method와 각각이 사용되는 경우에 대해서 설명해주세요.

HTTP의 주요 Method는 GET, POST, PUT, DELETE, PATCH 이렇게 5가지가 있습니다.

GET 요청은 서버에 존재하는 데이터를 요청하는 것이며, POST 요청은 서버에 데이터를 생성하는 것을 요청합니다. PUT 요청은 서버에 존재하는 데이터를 수정하거나 존재하지 않으면 생성합니다. DELETE 요청은 서버에 데이터를 제거할 것을 요청합니다. PATCH 요청은 서버에 존재하는 데이터를 일부 수정합니다.

### HTTP와 HTTPS의 차이점은 무엇인가요?

HTTPS는 HTTP에 데이터 암호화가 추가된 프로토콜입니다. HTTP는 80번 포트를 사용하지만 HTTPS는 443번 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원합니다.

### GET과 POST의 차이점은 무엇인가요?

GET은 서버에서 어떤 데이터를 가져와서 보여줄 때 사용합니다. 즉, 어떤 값이나 내용, 상태 등을 바꾸지 않는 경우에 사용됩니다. 이에 반해 POST는 서버상의 데이터 값이나 상태를 바꾸기 위해서 사용합니다. GET 요청은 Body를 사용하지 않고 쿼리 스트링을 사용하여 값을 전달하지만 POST 요청은 Body에 데이터를 담아서 전송합니다. GET은 데이터 길이에 제한이 있으며, 캐시가 가능하지만 POST는 데이터 길이에 제한이 없으며, 캐시되지 않는 차이점이 있습니다.
