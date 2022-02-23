## `Validation`
- 미리 널 포인트 예외 발생을 검증하는 과정!!
- `implementation("org.springframework.boot:spring-boot-starter-validaton")`

### 이유
1. 검증해야할 값 > 코드 길이 길어짐
2. 구현에 따라 서비스 로직 분리 필요
3. 재사용의 한계
4. 검증 로직 변경 > 테스트 로직 ?? 변경 같이

![image](https://user-images.githubusercontent.com/61215550/155269678-8356c133-ce15-492d-9c3f-9f72a08a50b2.png)

## `Exception` 처리
> 기존 에러 내려주는 방법이 많지 않음

1. 에러 페이지
2. 4xx or 5xx
3. client >> 200외 처리 하지 x >> 200 + 별도의 에러 정보 전달 

![image](https://user-images.githubusercontent.com/61215550/155270323-766f8ae5-9945-4980-a450-0a19a9f6cbca.png)


```java
@RestControllerAdvice
public class GlobalControllerAdvice {

    @ExceptionHandler(value = Exception.class) ✔ 예외 종류
    public ResponseEntity exception(Exception e){
        System.out.println(e.getClass()); ✔ 발생한 예외 클래스 
        System.out.println("----------------------");
        System.out.println(e.getLocalizedMessage()); 

        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("");
    }
}
```
### 실제 예외처리 코드
- `ResponseEntity`
  - 개발자 >> 결과 데이터 + HTTP 상태 코드 직접 제어 가능한 클래스

```java
@Slf4j
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(BadCredentialsException.class) ✌ 예외 처리 종류
    protected ResponseEntity<Response> handleBadCredentialsException(BadCredentialsException e) {
        log.info("handleBadCredentialsException");
        return new ResponseEntity<>(
                new Response<>(ErrorCode.Login_FAILED),
                HttpStatus.UNAUTHORIZED);

    }

    @ExceptionHandler(UserCiNotFoundException.class) ✌ 예외 처리 종류
    protected ResponseEntity<Response> handleUserCiNotFoundException(UserCiNotFoundException e) {
        log.info("UserCiNotFoundException");
        return new ResponseEntity<>
                (new Response<>(ErrorCode.USER_CI_NOT_FOUND),
                        HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(UserNotFoundException.class) ✌ 예외 처리 종류
    protected ResponseEntity<Response> handleUserNotFoundException(UserNotFoundException e) {
        log.info("handleUserNotFoundException");
        return new ResponseEntity<>
                (new Response<>(ErrorCode.USER_NOT_FOUND),
                        HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class) ✌ 예외 처리 종류
    protected ResponseEntity<Response> handleMethodArgumentNotValidException(MethodArgumentNotValidException e) {
        log.info("MethodArgumentNotValidException");
        return new ResponseEntity<>(
                new Response<>(ErrorCode.DATA_NOT_VALID),
                HttpStatus.BAD_REQUEST
        );
    }

    @ExceptionHandler(DataIntegrityViolationException.class) ✌ 예외 처리 종류
    protected ResponseEntity<Response> handleDataIntegrityViolationException(DataIntegrityViolationException e) {
        log.info("DataIntegrityViolationException");
        return new ResponseEntity<>(
                new Response<>(ErrorCode.DB_ACCESS_FAILED),
                HttpStatus.CONFLICT
        );
    }
    @ExceptionHandler(CardNotFoundException.class) ✌ 예외 처리 종류
    protected ResponseEntity<Response> handleCardNotFoundException(CardNotFoundException e) {
        log.info("CardNotFoundException");
        return new ResponseEntity<>(
                new Response<>(ErrorCode.CARD_NOT_FOUND),
                HttpStatus.BAD_REQUEST
        );
    }

}
```
