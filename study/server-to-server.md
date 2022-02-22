## 서버(클라이언트)-서버 간의 연결
- 우리가 클라이언트 입장에서 서버에 연결해보자 ! 😮
- 아래와 같은 기술들을  사용해

![image](https://user-images.githubusercontent.com/61215550/154416195-2dcbd95e-93fb-48c5-840f-6f1547a891b3.png)

### 클라이언트 서버
1. uri 생성
2. RestTemplete 사용해 통신

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

    System.out.println(result.getStatusCode());
    System.out.println(result.getBody());

    return result.getBody();
}
```

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


