# UMC_SpringBoot_Study

<br>
#✅ JOIN 연산이란?
JOIN은 SQL의 문법 중 하나로, 두 테이블을 엮어 원하는 데이터를 추출하기 위해 쓰는 문법입니다 <br>
연산을 통해 여러 테이블에서 가져온 레코드들을 조합해 하나의 결과를 만들어낼 수 있습니다 <br><br>
JOIN의 종류로는 <br>
1. INNER JOIN <br> 2. OUTER JOIN <br> 3. FULL OUTER JOIN <br> 4. SELF JOIN이 있습니다.
<br>

### 1️⃣ INNER JOIN
가장 많이 사용하는 JOIN으로, 조인하는 테이블의 ON 조건에 부합하는 레코드만 조인합니다 <br>
또한 조건에 부합하지 않는 레코드는 모두 삭제됩니다
```sql
SELECT <열 목록>
FROM <첫 번째 테이블>
    INNER JOIN <두 번째 테이블>
    ON <조인 조건>
[WHERE 검색 조건]
``` 
<br>

### 2️⃣ OUTER JOIN

두 테이블 모두에 조건에 부합하는 레코드가 있어야 하는 INNER JOIN과 다르게 한 쪽 테이블에만 결과가 있어도 결과가 나옵니다 <br>
두 테이블 중 어느 테이블을 기준으로 JOIN하느냐에 따라 LEFT/RIGHT/FULL OUTER JOIN 으로 분류할 수 있습니다<br>
```sql
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
    <LEFT | RIGHT | FULL> OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
     ON <조인 조건>
[WHERE 검색 조건]
``` 
<br>
    ➡️예를 들어, LEFT OUTER JOIN을 할 때, 첫 번째 테이블의 값은 모두 유지하고, ON 조건에 부합하는 두 번째 테이블의 결과를 JOIN한다고 볼 수 있습니다 <br> 또한 첫 번째 테이블의 레코드 중 ON 조건에 부합하지 않는 레코드들은 `NULL`값을 채워 반환합니다
<br>
### 3️⃣ SELF JOIN
자기 자신을 JOIN하는 문법으로, 테이블 하나 가지고 JOIN문을 사용하면 됩니다

### 🔎 Distinct
mysql에서 지원하는 문법으로 레코드의 중복을 제거해주는 문법입니다 <br>
`"select distinct o from Order o"` 와 같이 사용하면 되지만, 페이징을 하지 못한다는 단점이 있습니다


<hr>
✏️ 4주차 워크북을 기반으로 쿼리 작성하기 <br>


### 1. 내가 진행중, 진행 완료한 미션 모아서 보는 쿼리
```sql
SELECT
``` 
<br>


### 2. 리뷰 작성하는 쿼리
```sql
``` 
<br>

### 3. 홈 화면 쿼리
(현재 선택 된 지역에서 도전이 가능한 미션 목록, 페이징 포함) <br>
```sql
``` 
<br>


### 4. 마이 페이지 화면 쿼리
```sql
``` 
<br>

