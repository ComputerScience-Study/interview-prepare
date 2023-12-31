### 1. 사용해 본 디자인 패턴이 있나요? 있다면 어떤 패턴을 사용했고 왜 사용했나요?

- MVC 패턴을 통해 어떻게 코드 중복을 줄였나요?
  ### 피드백
  - MVC 패턴으로 코드 중복보단 유지보수를 위해 사용하는게 맞는거 같다

### 2. MVC, MVP, MVVM 패턴에 대해 각각의 구조와 장단점을 설명해 주세요.

- MVC 패턴에서는 유지보수성 장점을 얘기했는데 MVP 패턴의 장단점은 무엇인가요?
- MVVM의 장단점은?
- MVC 패턴과 MVP 패턴의 가장 큰 차이점은?
  ### 피드백
  - MVP는 View와 Presenter는 1:1 관계 Controller는 1:n 관계
  - 질문에 있는데 MVC만 장단점 얘기하고 나머지 안함.
  - MVC, MVP, MVVM으로 발전하는 방향으로 설명하면 좋을 것 같다.

### 3. 생성 패턴 중 Builder Pattern에 대해 설명해주세요.

- Builder Pattern을 사용하면서 좋았던 점은?
- 개발 중반에 Builder Pattern을 도입했다 했는데, 처음부터 사용하지 않은 이유?
- 굳이 Builder Pattern을 사용하지 않고 기본 생성자에 Setter를 사용하면 되지 않는지?
  ### 피드백
  - 실제 사용 경험을 얘기해서 좋았던 것 같고, 프로젝트 중간에 사용한 경험도 매우 좋았다.
  - Setter를 사용하지 않는 이유에서 객체의 불변성을 강조하면 좋겠다.

### 4. 싱글톤 패턴에 대해 설명해주세요.

- 싱글톤을 구현할 때 어떤 코딩 스타일을 사용하는지?
- 직접 구현해 봤는지?
- 싱글톤 패턴을 사용 시 주의할 사항은?
- 메모리 관리가 중요하다 했는데 어떻게 관리해야 되는지 예시를 들어주세요.
  ### 피드백
  - 싱글톤은 메모리를 많이 사용하진 않지만 GC에 회수가 되지 않으므로 무분별한 사용은 메모리릭을 발생할 수 있다

### 5. 디자인 패턴의 개념과 알고있는 디자인 패턴의 종류를 말해주세요.

- 디자인 패턴을 코드를 작성하는 스타일이라 했는데 디자인 패턴을 쓰면 좋은점은?
- 말씀하신 디자인 패턴 종류 중 하나만 추가적으로 설명해 주세요.

### 6. 결합도와 응집도에 대해 설명해주세요.

### 7. SOLID와 GRASP에 대해 간략히 설명해주세요.

### 8. 구조 패턴 중 Composite Pattern에 대해 설명해주세요.

- Composite Pattern은 트리 구조로 구성한다 했는데 Composite Pattern을 언제 사용하는지?
- 단일 객체와 복합 객체에 대해 설명해 주세요.
