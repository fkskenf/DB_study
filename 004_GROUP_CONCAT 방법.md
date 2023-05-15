# GROUP_CONCAT
- 여러 row의 값들을, 구분자를 가진 하나의 row로 만들고 싶을때 사용

# 코드
```sql 
WITH t1 AS (
    (
      SELECT '시작 {' AS json
    )
    UNION ALL
    (
      SELECT
        GROUP_CONCAT(json SEPARATOR ',') AS json -- 콤마 구분자
      FROM
        t2
      <where>
        <if test="list!=null">
          group IN
          <foreach collection="list" item="item" open="(" close=")" separator=",">
            '${item}'
          </foreach>
        </if>
      </where>
    )
    UNION ALL
    (
      SELECT '} 끝' AS json
    )
)
SELECT
  GROUP_CONCAT(json SEPARATOR '') AS json -- 구분자 없이 모든 row 합치기
FROM
  t1
```
