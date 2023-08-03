# Design Pattern

## 1. 사용해 본 디자인 패턴이 있나요? 있다면 어떤 패턴을 사용했고 왜 사용했나요?

생성 패턴 중 빌더 패턴을 사용한 적이 있습니다.

오버로딩을 통한 생성자를 통해 객체를 생성했었는데 각각의 케이스를 모두 고려하다보니 생성자의 갯수가 너무 많아져서 빌더 패턴을 도입하여 코드 가독성을 높이고자 사용했습니다.

## 2. MVC, MVP, MVVM 패턴에 대해 각각의 구조와 장단점을 설명해 주세요.

### MVC

model : 비즈니스 로직을 처리한다.

view: 보여지는 화면을 처리한다.

controller: 명령을 받아 라우팅을 한다.

### MVP

model

view

presenter: view에서 요청을 토대로 model을 통해 응답을 view에 전달해준다.

### MVVM

model

view

view model: view를 만들기 위한 model

## 3. 생성 패턴 중 Builder Pattern에 대해 설명해주세요.

생성 패턴 중 하나이다.

불필요한 생성자를 만들지 않고 객체를 만들 수 있으며, 체이닝을 통한 파라미터 전달을 활용하여 필드 순서를 신경쓰지 않을 수 있다.

## 4. 싱글톤 패턴에 대해 설명해주세요.

프로그램내에서 객체의 인스턴스를 한개만 생성하도록 하는 패턴이다.

객체를 한 개만 생성하니까 메모리 측면에서 좋으며, 프로그램 내에서 객체를 공유, 데이터를 공유할 때 편하다.

## 5. 디자인 패턴의 개념과 알고있는 디자인 패턴의 종류를 말해주세요.

개념: 코드를 작성하는 스타일?

종류: 싱글톤, 팩토리 메서드, 프록시, 템플릿 메소드

## 6. 결합도와 응집도에 대해 설명해주세요.

결합도: 2개 이상의 객체가 서로 관련이 있는지

응집도: 같은 행동을 하는 아이들이 한 객체에 있는지

## 7. SOLID와 GRASP에 대해 간략히 설명해주세요

### SOLID

single responsibility principle: 클래스 당 하나의 책임(기능)만 가져야한다.

open close principle: 확장에는 열려있고 변경엔 닫혀있어야한다

liskov substitution principle: 인터페이스에서 약속한대로 기능을 구현해야한다.

interface segregation principle: 나눌 수 있는 인터페이스는 나누어서 설계한다.

dependency inversion principle: 의존관계를 외부에서 결정해준다.

### GRASP

General Responsibility Assignment Software Patterns

1. information expert
    1. 역할을 수행할 수 있는 객체에 그 역할을 부여한다.
2. creator
    1. 객체의 생성은 생성되는 객체의 컨텍스트를 알고 있는 다른 객체가 있다면, 컨텍스트를 알고 있는 객체에 부여하자. A 객체와 B 객체의 관계의 관계가 다음 중 하나라면 A의 생성을 B의 역할로 부여하라.
    - B 객체가 A 객체를 포함하고 있다.
    - B 객체가 A 객체의 정보를 기록하고 있다.
    - A 객체가 B 객체의 일부이다.
    - B 객체가 A 객체를 긴밀하게 사용하고 있다.
    - B 객체가 A 객체의 생성에 필요한 정보를 가지고 있다.
3. controller
    1. 요청을 받는 객체를 만들어 처리한다.
4. low coupling
    1. 결합도를 낮게 설계한다.
5. high cohesion
    1. 응집도는 높게 설계한다.
6. polymorphism
    1. 객체의 종류에 따라 행동이 달라진다면 다형성을 사용한다.
7. pure fabrication
    1. 같은 기능이지만 information expert를 적용하여 다양한 곳에서 처리하고 있다면 한 곳에서 처리하도록 새로운 객체를 만들어 처리한다.
8. indirection
    1. 두 객체의 직접적인 coupling을 피하고 싶다면 두 객체 사이에 다른 객체를 사용한다.
9. protected variations
    1. 변경될 여지가 있는 곳에 인터페이스를 사용한다.

## 8. 구조 패턴 중 Composite Pattern에 대해 설명해주세요.

하나의 객체와 그 객체가 속한 그룹을 같은 타입으로 취급한다.

component: 상위 인터페이스

leaf: component 구현체

composite: list를 가지고 있으며, list에는 leaf, composite가 들어갈 수 있다.

root에서 하나의 함수를 호출했는데 모든 leaft에서 호출할 수 있다.