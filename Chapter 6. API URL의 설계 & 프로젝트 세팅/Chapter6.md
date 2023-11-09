# UMC_SpringBoot_Study

### ✅ API란?
Application Programming Interface <br>
간단히 요약하자면, 애플리케이션이 요청과 응답을 주고 받는 체계이며, 어떤 요청을 보내고 어떤 응답을 받아 어떤 데이터를 전달받을 수 있는지를 정리한 규격(interface)으로 볼 수 있습니다. <br>
API는 사용자가 보다 쉽게 프로그래밍 할 수 있도록 도와주고 애플리케이션 간의 상호작용을 원활히 할 수 있도록 도와줍니다. <br>

### ✅ REST API란?
Representational State Transfer API <br>
REST API는 HTTP를 기반으로 하는 웹 서비스 아키텍쳐로, <br>
**HTTP URL**을 통해 자원을 명시하고, **HTTP Method**를 통해 자원에 대한 CRUD Operation을 명시해 통신하는 방법입니다. <br><br>
- 장점 -> 서버와 클라이언트의 역할을 정확하게 분리할 수 있고, 의도하는 바를 쉽게 파악할 수 있음 <br>
- 단점 -> HTTP Method의 형태가 제한적
<br><br>
**🔎 API EndPoint** -> 해당 API를 호출하기 위한 HTTP Method + URL  <br>

### ✅ HTTP Method란?
REST 방식으로 통신할 때 필요한 작업을 표시하는 방식으로, 서버가 수행해야 하는 동작을 지정하는 방법이다. <br>
자주 사용하는 5가지 종류로는, <br>
- GET -> 조회<br>
- POST -> 생성 <br>
- PUT -> 갱신(전체) <br>
- PATCH -> 갱신(일부)<br>
- DELETE -> 삭제 <br><br><br>
**간단한 예제를 먼저 살펴보겠습니다.**<br>
서버의 도메인 주소가 https://umc.com일 때, 사용자가 해당 주소에서 로그인을 하는 api endpoint는 <br> 
`POST/https://umc.com/users/login`로 표시할 수 있습니다. <br>

end point로는 api가 어떤 동작을 수행할 것인지 쉽게 알 수 있습니다. <br>
그러나, 실제 어떤 정보를 가지고 해당 동작을 수행할 것인지는 알 수 없죠. <br>
이러한 실제 데이터들을 사용하기 위해, 세부적인 API 설계가 필요합니다 <br>
<br>
<hr>

## 세부적인 API 설계
### 1️⃣ path variable
유일하게 api endpoint에 속하는 요소로, **하나의 특정 대상을 식별**할 때, {}로 식별 값을 넣어 서버에 전달하는 역할을 합니다. <br>
`GET/users/articles/{articleId}` <br><br>

### 2️⃣ query string
보통 **검색 조회 + `GET`요청** 때 자주 사용되는 요소로, <br>
`GET/users/articles?name=umc`와 같이 name이 umc인 글들을 찾는 코드를 작성할 수 있습니다. <br><br>
⚠️ 쿼리 스트링은 end point가 아니므로, api endpoint 자체는 `GET/users/articles`로 작성해야 한다고 합니다! <br>


### 3️⃣ request body
POST 방식을 사용해 데이터들을 서버에 전송할 때, 데이터를 URL에 그대로 노출하는 것은 굉장히 위험할 수 있습니다. <br>
따라서 이러한 위험을 막기 위해, **Request Body**를 사용해 데이터를 **JSON** 형식 또는 **Form-Data** 형식으로 전달할 수 있습니다. <br>

### 4️⃣ request header
header는 데이터 **전송과 관련된 기타 정보들**(메타 데이터)이 담기는 부분입니다. <br>
body에 담기는 데이터의 형식 혹은 데이터, 혹은 토큰을 담기도 합니다. <br>
<br><br><br><hr>

# WorkBook
**API Endpoint, Request Body, Request Header, query String, Path variable**이 포함된 간단한 API 명세서 만들기 <br><br>

### ✅ 홈 화면
- API Endpoint <br>
`GET /api/home` <br>
- ResponseBody <br>
```json
{
    "address" : "안암동"
    "missions" : [
        {
            "mission_id" : "1"
            "store_name" : "반이학생마라탕" //가게 이름 
            "region_name" : " " //지역 이름
            "deadline" : "7" //마감 기한
            "content" : "10,000원 이상의 식사" //미션 내용
            "point" : "500" //포인트
            "category" : "중식당" //식당 카테고리
        },
        {
            "mission_id" : "2"
            "store_name" : "반이학생마라탕"
            "region_name" : " "
            "deadline" : "7"
            "content" : "10,000원 이상의 식사"
            "point" : "500"
            "category" : "중식당"
        }
    ]
}
```

<br><br>

### ✅ 마이 페이지 리뷰 작성
- API Endpoint <br>
`POST /review/` <br>
- RequestBody <br>
```json
    {
    "review_id" : "1"
    "user-id" : "닉네임1234"
    "stars" : "4.5" //별점
    "contents" : "음 너무 맛있어요 포인트도 얻고 ..." //리뷰내용
    "image" : "이미지파일" 
    "create_time" : "2022.05.14"
    "store-name" : "반이학생마라탕마라반"
}
``` 

<br><br>

### ✅ 미션 목록 조회
- API Endpoint <br>
`GET /api/missions` <br>
- ResponseBody <br>
```json
{
    "missions" : [
        {
            "mission_id" : "1"
            "store_name" : "반이학생마라탕" //가게 이름 
            "region_name" : " " //지역 이름
            "deadline" : "7" //마감 기한
            "content" : "10,000원 이상의 식사" //미션 내용
            "point" : "500" //포인트
        },
        {
            "mission_id" : "2"
            "store_name" : "반이학생마라탕" //가게 이름 
            "region_name" : " " //지역 이름
            "deadline" : "7" //마감 기한
            "content" : "10,000원 이상의 식사" //미션 내용
            "point" : "500" //포인트
        }
    ]
}
```

<br><br>

### ✅ 미션 성공 누르기
- API Endpoint <br>
`PATCH/usermission/{usermission-id}` <br>
- RequestBody <br>
```json
    "status" : "SUCCESS"
``` 

<br><br>

### ✅ 회원 가입하기
소셜로그인 고려X
- API Endpoint <br>
`POST /api/sign` <br>
- RequestBody <br>
```json
    "name" : "Dooly"
    "gender" : "Female"
    "birth" : "1900.01.01"
    "address" : "Busan"
    "phone_num" : "010-0101-1010"
    "prefer_food" : ["방어", "닭발", "초밥"]
``` 
- RequestHeader <br>
```json
{
    "user_id" : "1"
    "token" :
}
```
<br><br>




