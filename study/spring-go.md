## 🍃스프링 핵심
- 스프링 1.0 2004년 3월 출시
- 20여가지 구성
![image](https://user-images.githubusercontent.com/61215550/154407753-793775cc-26d1-4fbc-9be5-02173cbd4ca5.png)

- 여러 모듈 중 우리는!!?
  - 스프링부트, 스프링 클라우드, 스프링 데이터, 스프링 배치✔, 스프링 시큐리티
- 테스트 용이성, 느슨한 결합
- `IoC`  
- `AOP`

![image](https://user-images.githubusercontent.com/61215550/154408000-608c32eb-8c75-4b90-81d8-7018b399a04c.png)

### `IoC / DI`
- `IoC` 제어의 역전
  - 객체 new로 생성x > Spring Container
  - 즉, 개발자 > 프레임워크 (제어의 객체 관리 권한을 넘겨갔다고 "제어의 역전") 

- `DI` 의 장점
> 객체 사용하기 위해 주입한다 !!! > 외부로부터 주입받아 > 스프링 컨테이너
  - 테스트 용이
  - Mock 기술 통해 안정적 테스트 가능
  - 코드 확장 변경 > 영향 최소화 (추상화)
  - 순환참조 막는다

### `AOP` 관점지향프로그래밍
- 관점지향 프로그램
  - `Web Layer`
  - `Business Layer` 
  - `Data Layer`

- 횡단 관심
  - 반복적인 로직들은 한곳에 모아서 코딩!!!
![image](https://user-images.githubusercontent.com/61215550/154409470-0f2d1470-b693-44e9-877c-910667051823.png)
![image](https://user-images.githubusercontent.com/61215550/154409487-2b431294-2d1f-4201-a524-59544418c3d5.png)


### `Object Mapper`

## 여러가지 어노테이션
![image](https://user-images.githubusercontent.com/61215550/154413810-e93412c9-e9ef-49a0-9a3f-0b0b9b0e34e7.png)
