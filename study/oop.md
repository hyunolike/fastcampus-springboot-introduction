## 객체지향(OOP) > 효과적인 개발방식 🤗 
- 절차지향의 문제점 ㅠ,ㅠ 해결하기 위해 탄생
- `추상화` `상속` `은닉` `재사용` `인터페이스` 등...

### 1. 객체지향 등장!
- 순차적 설계 x > 현실에 있는 사물 모델링
- 객체(Object) 행위(Method) 변수(Variable)
- __Java__ 🤣
  - C++과 달라! 
  - JVM 독립적 실행으로 설계 > 여러 플랫폼에서 호환성 제공하는 장점

### 2. 객체 설계
- 객체 == 사물 == Object
- 속성, 행위
- 객체의 3가지 요소 ✔
  -   상태 유지(객체의 상태) > `Variable`
  -   기능 제공(객체의 책임) > `Method` 
  -   고유 식별자 제공(객체의 유일성)

### 3. 물리 객체와 개념 객체
- __물리객체__
  - 실제로 사물 존재!! 
- __개념객체__
  - 실제 존재 x
  - `service` `business logic` 처리하는 부분 (if문)
- 객체 정의 + 서비스 로직
- `Method` 잘 정의하자!

## 객체지향의 4대 특성
### 1. 캡슐화
- 객체의 속성 보호하기 위해서! `Variable`
-  `Method` 설계
  - 실물 객체가 가진 기능 모두 제공
  - 서로 관련성 있게
  - 속성 선언 > 상태 변경하는 method 제공
- `Method` 종류 ✔
  - `Getter/Setter Method`
  - `CRUD Method` > 데이터 처리
  - `Business Logic Method` > 비즈니스 로직
  - 객체의 생명 주기 처리 Method > `destory()` `discount()` 등 quit() 등 소멸에 대한 method
  - 객체의 영구성 관리 Method
  -   `private` 선언 내부에 다른 Method를 통해서 사용 가능하도록
-   `Method` 속성은 반드시 1개 속할 필요 x > 여러 속성 가능
- 장점 ✔
  - 추상화 제공
  - 재사용성 향상
  - 결과적으로 유지보수의 효율성 향상
- 무결성 보장
  - 변수 > `private`
  - Method > `public`
### 2. 상속
- 하위로 내려갈수록 __구체화__ ✔
- 상속의 효과
  - 프로그램 구조에 대한 이해 향상 
  - 재사용성 향상
  - 확장성 향상
  - 유지보수성 향상
### 3. 다형성
- 하나의 개체 > 여러개로 변화 가능

### 4. 추상화 >> `모델링` 
- 구체적 > 공통적, 특정 특성 분리 > 재조합 => `추상화`

## 객체지향 설계 5원칙 `SOLID`
- 응집도, 결합도
  - 결합도 낮추고 응집도 높여!
### 1. `SRP` 단일 책임 원칙
- 어떠한 클래스를 변경해야 하는 이유 > 1가지

`기존` 
![image](https://user-images.githubusercontent.com/61215550/154170055-f3054ccc-e0c2-461f-8a9b-aa13ac9bbe1a.png)

`개선 후`
![image](https://user-images.githubusercontent.com/61215550/154170133-0dbd6afe-5527-493f-9817-343e1a2471d1.png)

### 2. `OCP` 개방 폐쇄 원칙
- 자신의 확장은 열리지만 주변의 변화는 닫혀야되

![image](https://user-images.githubusercontent.com/61215550/154170337-cb0eb7ef-af11-4510-a821-a040093f9a60.png)

### 3. `LSP` 리스코프 치환 원칙
- 서브 타입은 언제나 자신의 기반 타입으로 교체 가능해야되

![image](https://user-images.githubusercontent.com/61215550/154170410-796445f1-5c07-4550-b810-ece1485d05ba.png)


### 4. `ISP` 인터페이스 분리 원칙
- 클라이언트는 자신이 사용하지 않는 메서드에 의존 관계 맺으면 안되

![image](https://user-images.githubusercontent.com/61215550/154170499-e585ee18-638d-4d75-b74c-04461fc25d43.png)

### 5. `DIP` 의존 역전 원칙
- 자신보다 변하기 쉬운 것에 의존하지 마

![image](https://user-images.githubusercontent.com/61215550/154170620-e9b09ca4-ef83-4da0-800d-06dbc8013bed.png)

## POJO JAVA(Plain Old Java Object) 😮
- 순수한 자바 오브젝트
- 기존 `EJB`의 종속적 문제 발생 > POJO
### POJO 특징
1. 특정 규약에 종속 X
2. 특정 환경에 종속 X

### POJO Framework ✔
1. `Spring, Hibernate`
  - 객체지향 + POJO > 서비스 로직에 집중이 가능하지
