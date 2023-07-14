## 피드백

### CORS

- Request 조건이 충족되면 자동으로 Simple Request로 아닐 경우 Preflight Request로 요청된다.
- CORS는 Server to Server 환경에선 발생하지 않는다.

### HTTP/2

- Multiplexed Streams 설명 시 병렬 처리를 강조하여 설명하는 것이 좋을 것 같다.

### GET과 POST의 차이점

- Path Variable은 데이터를 명시적으로 표현하기 때문에 데이터를 구분하기 위해 사용
- Path Variable은 REST API에서 Resource를 관리할 때 편리하기 때문에 많이 사용

### HTTP 멱등성

- 멱등성은 서버 자원 기준이다. 즉, GET, PUT, DELETE는 멱등하다.

### DNS에 대해

- 계층 구조여서 분산 데이터 구조를 가지고 있으며, 왜 중앙 집중식이 아닌지 설명해 주는게 좋을 것 같다.

# 추가 질문

## CORS가 발생하는 원인은 무엇인가?

## TCP 연결의 순서 보장은 어떻게 보장되는가?

## TCP와 UDP의 차이점을 알려주세요

## 실제 프로젝트 개발 시 GET 요청을 사용해 봤는지

## QueryString 말고 Path Variable을 언제 사용해보고 왜 사용했는지?

## GET 요청에 Body를 왜 사용하지 않는지? 사용하면 어떻게 처리되는지?

- 사용은 가능하지만 브라우저에서 지원 안함

## HTTP Method 중 멱등성을 지키는 Method가 무엇인지?

## POST와 PUT은 내부적으로 어떻게 다르게 동작하는지?

## 인증서를 왜 사용하는지?

## 인증서를 통해서 데이터를 암호화 시키는 건지?

## 만약 요청한 URL이 캐시에 없다면 어떻게 처리되는가?
