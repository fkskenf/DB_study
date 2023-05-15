outer join의 경우 ON절과 WHERE절에 들어가는 조건에 대해 주의해야한다.

# LEFT JOIN 경우
```sql
SELECT
  *
FROM
  leftTable LEFT JOIN rightTable
ON rightTable.조건 = 1
WHERE
  leftTable.조건 = 2
```
위 처럼 LEFT JOIN시 조건값을 아래와 같이 넣어야 원하는 결과값을 정확히 추출할 수 있다.
- ON절에는 : 오른쪽 테이블의 조건값
- WHERE에는 : 왼쪽 테이블의 조건값
