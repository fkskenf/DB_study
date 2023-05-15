# 인덱스가 안 되는 쿼리
## INDEX를 만들어 둔다고 모든 쿼리에서 INDEX를 활용하는 것은 아니다.

1. 인덱스 입힌 컬럼을 가공
> WHERE SUBSTR(컬럼명, 1,4) = ‘2019’
> - 해결 → WHERE 컬럼명 LIKE ‘2019%’
2. 인덱스가 있는 열 이름에는 함수나 연산을 가함
> WHERE count*10=100
> - 해결 →  WHERE count=100/10
3. 인덱스 컬럼의 묵시적 형변환(같은 타입으로 비교해야함)
> WHERE 컬럼명 = ‘20190730’
> - 해결 → WHERE 컬럼명 = TO_DATE(‘20190730’, ‘YYYYMMDD’)
4. 인덱스 컬럼 부정형 비교.
> WHERE 컬럼명 != ‘10’
> - 해결 → WHERE 컬럼명 IN(‘20’, ‘30’)
5. LIKE %가 앞에 위치.
> WHERE 컬럼명 LIKE ‘%2019’
> - 해결 → or 조건 사용 WHERE 컬럼명 IN(‘102019’,‘202019’,‘302019’)
 

# ORDER BY 와 GROUP BY에 대한 인덱스
## INDEX는 ORDER BY와 GROUP BY에도 영향을 끼치는데 다음과 같은 경우에는 INDEX를 타지 않는다.

1. ORDER BY 인덱스컬럼1, 컬럼2 : 복수의 키에 대해서 ORDER BY를 사용한 경우
2. WHERE 컬럼1='값' ORDER BY 인덱스 컬럼 : 연속하지 않은 컬럼에 대해 ORDER BY를 실행한 경우
3. ORDER BY 인덱스컬럼1 DESC, 인덱스컬럼2 ASC : DESC와 ASC를 혼합해서 사용한 경우
4. GROUP BY 컬럼1 ORDER BY 컬럼2 : GROUP BY와 ORDER BY의 컬럼이 다른 경우
5. ORDER BY ABS(컬럼) : ORDER BY 절에 다른 표현을 사용한 경우
