## 웹 개발 개론
- Web Site 
- API * Web Service
- User Interface

### REST
- 네트워크 아키텍처
  1. `Client, Server` 분리
  2. `Stateless`: 요청에 대해 클라이언트 상태를 서버에 저장 하지마
  3. `Cache`: 클라이언트는 서버의 응답을 Cache(임시저장) 할 수 있어야되
  4. `계층화`
  5. `인터페이스 일관성` ✔
    1. 자원의 식별
    2. __메시지__ 를 통한 리소스 조작(html, json, xml, text)
    3. 자기 서술적 매시지
    4. 애플리케이션 상태에 대한 엔진으로써 하이퍼미디어
  7. `Code on Demand(Optional)`: 자바 애플릿, 자바스크립트 등 특정한 기능을 서버로부터 클라이언트가 전달받아 코드로 실행 가능해야되

### URI 설계 패턴
#### URI
- 인터넷 자원 주소
- `https://www.fastcampus.co.kr/resource/sample/1`
#### URL
- 인터넷 상에서의 자원, 특정 파일이 어디에 위치하는지
- `https://www.fastcampus.co.kr/fastcampus.pdf`
- `URI > URL`  이렇게 하위 개념 ✔

#### URI 설계 원칙
1. `/` 계층 관계
2. 마지막 `/` 사용 금지
3. `-` 가독성 높이는데 사용
4. `_` 사용하지마
5. 소문자
6. 파일확장자는 포함 X
7. 프로그래밍 언어에 의존적인 확장자
8. 구현에 의존적인 경로 사용 X
9. 세션 ID 포함 X
10. 프로그래밍 언어의 Mathod명 사용 x
11. 명수형에는 단수보다 복수
12. 컨트롤러 이름으로는 동사나 동사구 사용
13. 경로부분 중 변하는 부분은 유일한 값
14. CRUD 기능 나타내는 거 사용 x
15. URI Query Parameter 디자인 사용
16. API 서브 도메인은 일관성있게 작성
17. 클라이언트 개발자 포털 서브 도메인은 일관성 있게
![image](https://user-images.githubusercontent.com/61215550/154179340-c4c6a5f4-8f9d-43f1-96d4-44ce608d1402.png)

#### HTTP Protocal
- TCP기반으로 한 REST의 특징 모두 구현하고 있는 웹기반의 프로토콜
- 요청/응답

![image](https://user-images.githubusercontent.com/61215550/154179515-13e3366f-9976-43dd-949b-fb9cf1d1bd60.png)
![image](https://user-images.githubusercontent.com/61215550/154179575-058e84ac-8c75-43cb-8145-97ec55634529.png)

