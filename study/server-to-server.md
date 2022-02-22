## 서버(클라이언트)-서버 간의 연결
- 우리가 클라이언트 입장에서 서버에 연결해보자 ! 😮
- 아래와 같은 기술들을  사용해

![image](https://user-images.githubusercontent.com/61215550/154416195-2dcbd95e-93fb-48c5-840f-6f1547a891b3.png)

# `GET 방식`
### 클라이언트 서버
1. uri 생성
2. RestTemplete 사용해 통신 
  - `getForEntity()` 여기서 `get`ForEntity()는 요청의 GET!!

- `UriComponentsBuilder` : url 만들어주는 거
  - `encode` : 파라미터 보낼수 있기 때문에

```java
public String hello(){
    URI uri = UriComponentsBuilder
            .fromUriString("http://localhost:9090")
            .path("/api/server/hello")
            .encode()
            .build()
            .toUri();
    System.out.println(uri.toString());

    RestTemplate restTemplate = new RestTemplate();
    ResponseEntity<String> result = restTemplate.getForEntity(uri, String.class); 
    ⭐ ResponseEntity > 헤어와 같은 상세한 정보를 가져올 수 있다.

    System.out.println(result.getStatusCode());
    System.out.println(result.getBody());

    return result.getBody();
}
```
#### `UriComponentsBuilder`
- queryparam

```java
URI uri = UriComponentsBuilder
        .fromUriString("http://localhost:9090")
        .path("/api/server/hello")
        .queryParam("name","hyunho")
        .queryParam("age",1111)
        .encode()
        .build()
        .toUri();
```
- 클라이언트 서버
  - `@Post` 방식
- 서버
  - `@RequestParam` 방식

![image](https://user-images.githubusercontent.com/61215550/155056699-97053c16-cc7f-49b1-9a5d-4068eb8f628a.png)


#### JSON 형태는 어떻게 받아오지?
##### 클라이언트 서버

```json
{
  "name": "hyunho",
  "age": 28
}
```

1. `DTO` 생성(응답)
2.  서비스단 수정
3.  컨트롤러 반환값 수정

`DTO`
```java
public class UserResponse {

    private String name;
    private int age;

    @Override
    public String toString() {
        return "UserResponse{" +
                "name='" + name + '\'' +
                ", age=" + age +
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
}
```

`Service`
```java
public UserResponse hello(){ 🤗 반환값 확인
    URI uri = UriComponentsBuilder
            .fromUriString("http://localhost:9090")
            .path("/api/server/hello")
            .encode()
            .build()
            .toUri();
    System.out.println(uri.toString());

    RestTemplate restTemplate = new RestTemplate();
    ResponseEntity<UserResponse> result = restTemplate.getForEntity(uri, UserResponse.class); 🤗 DTO.class로 수정 

    System.out.println(result.getStatusCode());
    System.out.println(result.getBody());

    return result.getBody();
}
```

`Controller`
```java
@GetMapping("/hello")
public UserResponse getHello() { 🤗 DTO 반환값으로 수정
    return restTempleteService.hello();
}
```

##### 서버
1. DTO 생성
2. 컨트롤러 수정

`DTO`
```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class User {

    private String name;
    private int age;
}
```

`Controller`
```java
@RestController
@RequestMapping("/api/server")
public class ServerApiController {

    @GetMapping("/hello")
    public User hello(){ 🤗 DTO 데이터 생성 및 반환
        User user = new User();
        user.setName("hyunho");
        user.setAge(28);
        return user;
    }
}
```


![image](https://user-images.githubusercontent.com/61215550/155056033-45eeb45f-6a23-4cfb-9bd3-ec25f6db78e3.png)


### 서버

```java
@RestController
@RequestMapping("/api/server")
public class ServerApiController {

    @GetMapping("/hello")
    public String hello(){
        return "hello server";
    }
}
```

# `POST 방식` 
### 클라이언트 서버

```java
public UserResponse post(){
        // http://localhost:9090/api/server/user/{userId}/name/{userName}

        URI uri = UriComponentsBuilder
                .fromUriString("http://localhost:9090")
                .path("/api/server/user/{userId}/name/{userName}")
                .encode()
                .build()
                .expand("100", "steve")
                .toUri();
        System.out.println(uri);

        // http body -> object -> object mapper -> json -> rest templete -> http body json
        UserRequest req = new UserRequest();
        req.setName("steve");
        req.setAge(10);

        RestTemplate restTemplate = new RestTemplate();
        ResponseEntity<UserResponse> response = restTemplate.postForEntity(uri, req, UserResponse.class); 🤗 postForEntity

        System.out.println(response.getStatusCode());
        System.out.println(response.getHeaders());
        System.out.println(response.getBody());

        return response.getBody();


    }
```
