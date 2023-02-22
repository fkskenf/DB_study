# DB_study

## 성능 측정 (mariadb 기준)
```sql
EXPLAIN 함수 사용

-- Profiling 옵션의 활성화 여부 확인
SELECT @@profiling;

-- Profiling 옵션 활성화
SET profiling=1;

-- Profiling 옵션 비활성화
SET profiling=0;

-- 성능 측정 
SHOW profiles;
```

## 주의사항
> 쿼리 조회시, 조건문에 index컬럼 잘 타는지 확인 

## 길어서 부분만 출력되는 값 (mariadb 기준)
```sql
SELECT *, convert(contents USING utf8)
```
