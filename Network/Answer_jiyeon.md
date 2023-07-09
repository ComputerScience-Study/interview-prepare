- [www.~.com에](http://www.%7E.xn--com-568n/) 접속할 때 생기는 과정에 대해 설명해주세요.(웹 동작 방식 이해)

[답변]

1. 사용자가 브라우저에 URL을 입력합니다.
2. DNS 서버에서 도메인 네임으로 서버의 주소를 찾습니다.
3. 해당 IP 주소로 tcp or udp 방식으로 통신합니다.
4. 클라이언트는 웹 서버로 HTTP 요청 메세지를 보냅니다.
5. 웹 서버는 HTTP 응답 메세지를 보냅니다.
6. 이렇게 도착한 HTTP 응답 메세지는 웹 페이지 데이터로 변환되고, 웹 브라우저에 의해 출력됩니다.


        💡 추가 질문 예상
        웹 서버: Http 프로토콜을 기반으로, 클라이언트의 요청을 서비스하는 기능을 담당
        정적, 동적(WAS에 요청)
        정적 리소스는 변화가 없는 리소스를 뜻한다. 즉, HTML, CSS, Javascript와 같이 미리 서버에 저장해두고 서버가 요청을 받으면 응답만 해주면 되는 것들을 뜻한다. 어느 사용자에게도 동일한 결과값을 보여준다.
        동적 리소스는 누가, 언제, 어떻게 서버에 요청했는지에 따라 결과값을 다르게 보여주는 리소스를 뜻한다. 사용자에게 맞춤형 콘텐츠를 제공해줄 수 있게 된다.
        
        WAS: 
        프로그램 실행 환경 및 DB 접속 기능 제공
        여러 트랜잭션 관리 기능
        업무 처리하는 비즈니스 로직 수행
        
        HTTP: (Hypertext Transfer Protocol) 클라이언트와 서버 간 통신을 위한 통신 프로토콜
        
        DNS 서버: 도메인 네임 시스템 서버로 도메인에 네트워크 주소를 저장하고있어서 사용자가 브라우저에 접근할 때 ip주소 대신 도메인으로 해당 주소에 접근이 가능합니다.
        
        - Host : 인터넷에 연결된 컴퓨터 한 대 한대
        - IP Address : host끼리 통신을 하기 위해 필요한 주소
        - IP 주소를 기억하는 것이 어렵기 때문에 DNS(Domain Name System)이 나왔습니다
            - DNS Server : 수많은 IP 주소와 도메인이 저장되어 있습니다
            - 웹에서 [www.naver.com을](http://www.naver.com/) 입력하면 DNS Server에 [www.naver.com의](http://www.naver.xn--com-yh0o/) IP 주소를 알려준 후, 그 IP 주소를 토대로 접속하는 것입니다.

DNS
https://galid1.tistory.com/53

웹 서버 vs WAS
[https://gyoogle.dev/blog/web-knowledge/Web Server와 WAS의 차이.html](https://gyoogle.dev/blog/web-knowledge/Web%20Server%EC%99%80%20WAS%EC%9D%98%20%EC%B0%A8%EC%9D%B4.html)
https://tecoble.techcourse.co.kr/post/2021-05-24-apache-tomcat/

- 3-way handshake에 대해 설명해주세요.(TCP 연결)

[답변]

- HTTP/2를 설명하고 장점 두가지를 말해보세요.

[답변]

우선 HTTP/2는 더 적은 TCP 연결을 사용
https://bentist.tistory.com/36

- DNS에 대해 설명해주세요.

[답변]

- CORS란 무엇이며 동작과정을 설명해보세요.

[답변]

- HTTP Method와 각각이 사용되는 경우에 대해서 설명해주세요.

[답변]

- HTTP와 HTTPS의 차이점은 무엇인가요?

[답변]

SSL 인증서 유무의 차이


        💡 추가 질문 예상
        SSL 인증서가 왜 필요해요?

- GET과 POST의 차이점은 무엇인가요?
