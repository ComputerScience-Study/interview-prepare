# Operating System

## 프로세스와 스레드의 차이는 무엇입니까?

- 프로세스
    - 프로그램이 메모리에 올라간 상태, 컴퓨터에서 작업 중인 프로그램이다.
    - 스택, 힙, 데이터, 코드 영역이 메모리에 할당된다.
- 스레드
    - 프로세스 내 실행 흐름 단위
    - 프로세스가 할당받은 자원들을 공유하며 사용한다. 다만 스택은 스레드별로 가지고있다.

## 크롬 탭 하나는 프로세스인가요? 스레드인가요?

- 프로세스

## 가상메모리에 대해 설명해주세요

- 메모리보다 큰 프로그램을 실행하기 위해 실행하려는 프로그램의 일부만 메모리에 올려 실제 물리 메모리보다 더 큰 프로그램을 실행할 수 있게 해주는 기술이다.

## 메모리 계층구조에 대해 설명해주세요

- 레지스터, 캐시, 주기억장치, 보조기억장치 순으로 계층적으로 이루어져있다.
- 레지스터, 캐시, 주기억장치, 보조기억장치 순으로 빠르며, 용량은 작고, 가격은 비씨다
- 캐시메모리는 sram, 주기억장치는 ram, 보조기억장치는 hdd, ssd 등이 있다.

## 동기와 비동기에 대해 설명해 주세요.

- 동기는 어떠한 작업을 실행했을 때 해당 작업이 끝날 때까지 기다린 후 다음 작업을 실행한다.
- 비동기는 어떠한 작업을 실행한 후 해당 작업이 끝나기를 기다리지 않고 다음 작업을 실행한다.
- 비동기로 처리하면 작업을 동시에 처리할 수 있으므로 성능 향상을 기대해볼 수 있다.

## 세마포어와 뮤텍스의 차이에 대해 설명해주세요.

- 뮤텍스
    - 공유자원이 하나
    - lock 변수, acquire, release 함수를 통해 동기화를 해결한다
- 세마포어
    - 공유자원 여러 개
    - 사용가능한 공유 자원 수 변수, wait, signal 함수를 통해 동기화를 해결한다
    - 사용가능한 공유 자원 수가 없다면 대기 큐에 들어가고 나중에 사용가능해지면 대기 큐에 들어간 프로세스가 실행된다

## 페이징과 세그멘테이션에 대해 설명해주세요

- 페이징
    - 물리 메모리 주소 공간을 프레임 단위로 자르고 논리 메모리 주소를 페이지 단위로 잘라 페이지를 프레임에 할당하는 기술이다
    - 페이지 아웃, 페이지 인을 통해 프로그램을 실행한다

## 데드락에 대해 설명해주세요

- 발생가능성이 없는 일을 계속 기다리는 상태
- 발생조건
    - 상호 배제
    - 점유대기
    - 비선점
    - 원형대기
- 해결방법
    - 발생조건 중 하나를 만족시키지 않도록 한다
    - safe state일 때 자원을 할당한다
    - 데드락이 해결될 때까지 한 프로세스씩 종료하거나 모두 종료한다