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
    
    ```
### DTO, Converter 작성
- TempResponse 클래스에 TempExceptionDTO를 추가해줍니다 <br>
- 위에서 만든 DTO를 사용하는 함수를 Converter에 작성해줍니다 <br>
  

### Service 작성
- Service 작성 <br>


### Controller 작성
- Controller을 작성 <br>
    ```java
    @GetMapping("/exception")
    public ApiResponse<TempResponse.TempExceptionDTO> exceptionAPI(@RequestParam Integer flag){

        return null;
    }
    ```
    위의 코드에서 `@RequestParam`은 QuiryString을 받아오는 annotation입니다 <br>


