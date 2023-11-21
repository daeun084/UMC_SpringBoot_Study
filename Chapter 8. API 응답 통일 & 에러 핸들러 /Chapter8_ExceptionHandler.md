# UMC_SpringBoot_Study


<br>

# ✅ 에러 핸들러
<br><br>

## 💫 Exception Handling 예제
### Exception Handler

- ErrorStatus에 새로운 테스트용 Exception을 추가해줍니다 <br>
    `TEMP_EXCEPTION(HttpStatus.BAD_REQUEST, "TEMP4001", "이거는 테스트");`
- Handler package에 Temp 관련 핸들러를 추가해줍니다 <br>
    ```java
       public class TempHandler extends GeneralException {
        public TempHandler(BaseErrorCode errorCode) {
            super(errorCode);
        //errorCode를 GeneralException 클래스로 전달
    } }
    ```
  <br>
  
### DTO, Converter 작성
- TempResponse 클래스에 TempExceptionDTO를 추가해줍니다 <br>
  ```java
    @Builder
    @Getter
    @NoArgsConstructor
    @AllArgsConstructor
    public static class TempExceptionDTO{
        Integer flag;
    }
  ```
- 위에서 만든 DTO를 사용하는 함수를 Converter에 작성해줍니다 <br>
  ```java
   public static TempResponse.TempExceptionDTO toTempExceptionDTO(Integer flag){
        return TempResponse.TempExceptionDTO.builder()
                .flag(flag)
                .build();
    }
  ```
  
  <br>
  

### Service 작성

`TempQueryService`라는 인터페이스를 만들고, 해당 인터페이스를 implement하는 `TempQueryServiceImpl`서비스를 작성해줍니다 <br>
```java
public class TempQueryServiceImpl implements TempQueryService{
    @Override
    public void CheckFlag(Integer flag) {
        if (flag == 1) //?? 2아님?
            throw new TempHandler(ErrorStatus.TEMP_EXCEPTION);
    }
    //에러 조건에 부합하면 에러 생성
}
```
<br>

### Controller 작성
- Controller을 작성 <br>
    ```java
        @GetMapping("/exception")
        public ApiResponse<TempResponse.TempExceptionDTO> exceptionAPI(@RequestParam Integer flag){
         tempQueryService.CheckFlag(flag);
        return ApiResponse.onSuccess(TempConverter.toTempExceptionDTO(flag));
        //쿼리 스트링으로 flag를 받은 다음 2면 Exception 발생
        //Exception 안터지면 onSuccess 함수 호출
    }
    ```
    위의 코드에서 `@RequestParam`은 QuiryString을 받아오는 annotation입니다 <br>



### ExceptionAdvice 
‼️ 우선 build.gradle에서 `validation` 의존성을 추가해줍니다 <br>

```java
@Slf4j
@RestControllerAdvice(annotations = {RestController.class})
public class ExceptionAdvice extends ResponseEntityExceptionHandler {}
```
실습에서는 `@RestControllerAdvice` 어노테이션을 사용해 해당 클래스로 Exception을 감지합니다 <br>
- 위에서 작성한 ExceptionHandler는 에러 코드를 `GeneralException`에게 전달합니다 <br>
- 여기서 `GeneralException`은 `RuntimeException`을 상속받고 있어, 결국 발생된 에러를 감지할 수 있게 됩니다 <br>
- `ExceptionAdvice`의 코드를 자세히 보면 내부에서 GeneralException의 함수를 호출하고, 이를 통해 에러에 대해 응답을 보내는 것을 확인할 수 있습니다 <br>

<br><br>

### 🔎 여기서 사용된 `@RestControllerAdvice란`, 
- 전역적으로 예외를 처리
- `@ResponseBody`가 붙어있어 응답을 Json으로 반환 *(`@ControllerAdvice`와의 차이점)*
  
<br>

Spring는 스프링 예외 처리를 미리 해둔 `ResponseEntityExceptionHandler`를 제공하고 있습니다 <br>
이 핸들러를 상속받고 메소드를 오버라이딩해서 예외에 대한 응답을 보낼 수 있습니다 <br>
상속받는 클래스에 `@RestControllerAdvice` 를 추가하면, `@RestController `annotation이 달린 클래스에서 발생한 오류를 캐치할 수 있습니다 <br><br>

위의 내용과 같이, 실습에서 `@RestController`를 가진 controller에서 생기는 에러는 `@RestControllerAdvice`가 붙은 ExceptionAdvice에서 응답하는 것을 확인할 수 있었습니다



- 장점
- 없으면 불편한 점



