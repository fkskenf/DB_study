## SQL json 데이터에서 값 조회 및 가공

### 1. 함수
```sql 
SET @json = '{
                "users" : [
                        {"name" : "Kim", "age" : 26, "country" : "kr"},
                        {"name" : "Lee", "age" : 21, "country" : "usa"},
                        {"name" : "Park", "age" : 18, "country" : "jp"},
                        {"name" : "Moon", "age" : 37, "country" : "cn"},
                        {"name" : "Ryu", "age" : 33, "country" : "kr"}
                ]
             }'; -- JSON 형식 문자열을 @json 변수에 저장
            
-- JSON 포맷 검증 -- 1
SELECT JSON_VALID(@json); 
-- JSON에서 조건에 맞는 최초 검색 위치 리턴 -- "$.users[0].country"
SELECT JSON_SEARCH(@json, 'one', 'kr'); 
-- JSON에서 조건에 맞는 모든 모든 위치 리턴 -- ["$.users[0].country", "$.users[4].country"]
SELECT JSON_SEARCH(@json, 'all', 'kr'); 
-- 두 번째 유저의 name 값 리턴 -- "Lee"
SELECT JSON_EXTRACT(@json, '$.users[1].name'); 
-- 첫 번째 유저의 hobby 속성을 생성 후 cycle 저장 -- {"users": [{"age": 26, "name": "Kim", "hobby": "cycle", "country": "kr"},....생략...
SELECT JSON_INSERT(@json, '$.users[0].hobby', 'cycle');
-- 첫 번째 유저의 name을 Hong으로 변경 -- {"users": [{"age": 26, "name": "Hong", "country": "kr"},....생략...
SELECT JSON_REPLACE(@json, '$.users[0].name', 'Hong'); 
-- 첫 번째 유저 정보를 삭제 -- {"users": [{"age": 21, "name": "Lee", "country": "usa"},....생략...
SELECT JSON_REMOVE(@json, '$.users[0]');
```
### 2. 응용 예제
```sql 
SELECT status 
FROM t_data_result
WHERE name = 
(SELECT TRIM(BOTH '"' FROM JSON_EXTRACT(t2.json, CONCAT('$.nodes['
               , (SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(JSON_SEARCH(t2.json, 'one', '8e6762fd-c07e-4f4b-b9c1-c9bcb2638fc9', NULL, '$.nodes[*].uuid'), '[', -1), ']', 1) AS a)
               , '].table_name'))) AS code  
FROM t_data_json t2 
WHERE t2.no = 1793
AND type = 'F')
```
#### json_unquote
- JSON_EXTRACT 이후 JSON_UNQUOTE(값); 을 사용해 ""를 뺀 값을 가져와주면 된다
