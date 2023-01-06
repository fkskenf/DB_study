# @Rownum 사용방법 (MariaDB)

```java
SELECT
  @ROWNUM := @ROWNUM + 1 AS NO
  , tc.*
FROM (
     SELECT
      t.tabl_sno
      , c.clmn_sno
      , c.sort_sqnc
    FROM
      s_tabl t
    INNER JOIN s_clmn c
    ON t.tabl_sno = c.tabl_sno
    AND	c.tabl_sno= #{tabl_sno}
    ORDER BY c.sort_sqnc
    ) AS tc
,(SELECT @ROWNUM :=0) r
```
---
> MariaDB에서 rownum과 orderby를 혼용해서 사용할시 이슈발생 : 서브쿼리에서의 결과 순서를 메모리에 따로 적재하지 않기에 orderby가 무시되는 이슈
>> 해결1 : orderby가 마지막에 적용되도록 변경  
```java
SELECT
  @ROWNUM := @ROWNUM + 1 AS NO
  , tc.*
FROM (
     SELECT
      t.tabl_sno
      , c.clmn_sno
      , c.sort_sqnc
    FROM
      s_tabl t
    INNER JOIN s_clmn c
    ON t.tabl_sno = c.tabl_sno
    AND	c.tabl_sno= #{tabl_sno}
    ) AS tc
,(SELECT @ROWNUM :=0) r
ORDER BY tc.sort_sqnc
```
>> 해결2 : 서비쿼리 내부에 limit를 추가 (단, 최대 row를 고려해야한다.)
```java
SELECT
  @ROWNUM := @ROWNUM + 1 AS NO
  , tc.*
FROM (
     SELECT
      t.tabl_sno
      , c.clmn_sno
      , c.sort_sqnc
    FROM
      s_tabl t
    INNER JOIN s_clmn c
    ON t.tabl_sno = c.tabl_sno
    AND	c.tabl_sno= #{tabl_sno}
    ORDER BY c.sort_sqnc
    limit 100
    ) AS tc
,(SELECT @ROWNUM :=0) r
```
