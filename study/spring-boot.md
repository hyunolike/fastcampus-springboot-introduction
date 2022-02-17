## 🍃Spring Boot & API 개발 방법
- 단순히 실행 > 프로덕션 수준 쉽게 개발 가능
- Spring 구성이 거의 필요x
- `java -jar` 로 실행하는 java 어플리케이션 개발 가능
- 톰켓 내장

### Build Tool
- Maven
- Gradle

### Servlet Containers
- Tomcat 9x
- Jetty 9.4
- Undertow 2.0
- Netty

## API

![image](https://user-images.githubusercontent.com/61215550/154381851-494d754b-1e80-4374-af1a-1fd75128ae45.png)

### `@RestController` 
- `Object` > `JSON` 이렇게 자동으로 바꿔준다.

```java
@RestController ✔
@RequestMapping("/api-put")
public class PutApiController {

    @PutMapping("put") ✔
    public PutRequestDto put(@RequestBody PutRequestDto putRequestDto){ ✔ 반환값을 객체로 하면 자동으로 Json 형태로 바꿔준다
        return putRequestDto;
    }
}
```

![image](https://user-images.githubusercontent.com/61215550/154388243-506fa815-c50c-4a14-a75f-bd8a13d11b9e.png)


### Get
#### `@PathVariable`
![image](https://user-images.githubusercontent.com/61215550/154380137-e370cc94-1bf0-4e60-8080-36f4dbcd5bad.png)

- pathvariable 이름 다르게 하고 싶을 때

```java
@GetMapping("/path-variable/{name}")
public String pathVariable(@PathVariable(name = "name") String pathName){
    return "나의 id는 " + pathName;
}
```

#### `QueryParam`
> http://localhost:8080/api/query-param?id=2&name=장현호 
- 크게 3가지 존재 / `KEY: VALUE` 방식!!
  1. `@RequestParm Map<key, value>`
  2. `@Request int i, @Request int j`
  3. `DTP` 객체 생성해서 사용하기 ⭐

- ⭐dto 형태 >> 현업에서 가장 많이 사용!!
- 요청, 응답 검증할 수 있으니까??!!!

```java
@GetMapping("query-param")
public String queryParamDto(UserRequest userRequest){
    System.out.println(userRequest.getName());
    System.out.println(userRequest.getEmail());
    System.out.println(userRequest.getAge());
    return userRequest.toString();
}
```

![image](https://user-images.githubusercontent.com/61215550/154381680-260cea7c-7cbd-4f29-b103-16b7a36f85c3.png)

### Post
#### JSON ⭐ 모두 키, 값으로 존재 !!!
![image](https://user-images.githubusercontent.com/61215550/154382738-f280d93f-916c-4647-a70c-10fc6a351bea.png)

- 스네이크 케이스 방식 `phone_number` ✔ 보통 많이 사용해
- 카멜 케이스 방식 `phoneNumber`


```JSON
{
  "key": "value"
}

{
  "name" : "hyun-ho",   ✔ 문자열
  "age" : 10, ✔ 숫자
  "isAgree" : false,    ✔ 불리언
  "user" : {            ✔ 객체
    "address" : "souel",
    "password" : "1234"
  },
}

{
  "user_list: [          ✔ 배열  같은 키 값으로 반복되야돼!!! ⭐
    {
      "account" : "abcd",
      "password" : "1234"
    },
    {
      "account" : "aaaa",
      "password" : "2222"
    }
  ]
}
  
}
```

#### 요청 `@RequestBody` ✔
- POST 방식은 `@RequestParam` 이 아닌 `@RequestBody` 로 한다!
- map 방식이 아닌 dto를 만들어서 사용하자! 
- 특정 이름의 매칭은 `@JsonProperty("이름")` 작성해준다

```json
{
  "account": "",
  "email": "",
  "password": "",
  "address": ""
}
```

![image](https://user-images.githubusercontent.com/61215550/154384607-09de8271-3e40-48ea-bb39-2ea38121869b.png)

```java
@PostMapping("/post")
public String post(@RequestBody PostRequestDto postRequestDto) {
    return postRequestDto.toString();
}

```
![image](https://user-images.githubusercontent.com/61215550/154385023-46a93d2a-f41b-4d95-a884-38c631f4d18b.png)


### Put
> 멱등하다! 처음 한번은 생성되고 있으면 생성하지 않아 항상 같은 상태 유지!!
- 만들고 싶은 JSON 구조로 DTO 매칭해주면 되!!! ✌
```json
{
  "name": "",
  "age": "",
  "car_list: [
    {
      "name": "",
      "car_number": ""
    },
    {
      "name": "",
      "car_number": ""
    }
  ]
}
```

`요청 DTO`
```java
@JsonNaming(value = PropertyNamingStrategy.SnakeCaseStrategy.class) ✔ 전체 스네이크 케이스로 바꿈
public class PutRequestDto {

private String name;
private int age;
private List<CarDto> carList; ✔ JSON 배열

@Override
public String toString() {
    return "PutRequestDto{" +
            "name='" + name + '\'' +
            ", age=" + age +
            ", carList=" + carList +
            '}';
}

public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public int getAge() {
    return age;
}

public void setAge(int age) {
    this.age = age;
}

public List<CarDto> getCarList() {
    return carList;
}

public void setCarList(List<CarDto> carList) {
    this.carList = carList;
}
```

`배열 DTO`
```java
private String name;
@JsonProperty("car_number")
private String carNumber;

public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public String getCarNumber() {
    return carNumber;
}

public void setCarNumber(String carNumber) {
    this.carNumber = carNumber;
}

@Override
public String toString() {
    return "CarDto{" +
            "name='" + name + '\'' +
            ", carNumber='" + carNumber + '\'' +
            '}';
}
```
`controller`
```java
@PutMapping("put")
public void put(@RequestBody PutRequestDto putRequestDto){
    System.out.println(putRequestDto);
    System.out.println(putRequestDto.getCarList());
}
```

### Delete
- 여러가지 값을 받을 필요 x

```java
@DeleteMapping("delete/{userId}")
public void delete(@PathVariable String userId, @RequestParam String account) {
    System.out.println(userId);
    System.out.println(account);
}
```
