# 이슈
```sql
-- Lock이 발생하여, 이후의 관련 테이블의 Update/Insert/Delete와 같은 쿼리문의 수행에 장애가 발생

### Cause:java.sql.SQLException: Lock wait timeout exceeded; try restarting transaction
```


# Lock 확인 
```sql
select * from information_schema.innodb_locks;

select * from information_schema.innodb_lock_waits;

select * FROM information_schema.INNODB_TRX;

SHOW processlist;

SHOW FULL processlist
```

# 원인
1. Transaction 설정으로 인한 불완전 connect 종료
2. 쿼리의 수행시간 오버

# 해결
1. Lock 발생시킨 쿼리의 관련 테이블에 INDEX 설정
2. 쿼리의 수행 속도를 높여주기 위한 쿼이 튜닝
3. 월별 파티셔닝을 통한 테이블 분할 
4. 즉시해결 : Kill 명령어를 통해 강제 종료 (kill 'ID번호')
