## SQL json 데이터에 대해 원하는 값 추출하기

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
