https://school.programmers.co.kr/learn/courses/30/lessons/59413  
코딩테스트 연습 > GROUP BY > 입양 시각 구하기(2)

### 문제 요구사항

보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.

### 정답 코드

```sql
WITH RECURSIVE TIME AS (
    SELECT 0 AS HOUR  -- 초기값, HOUR을 0으로 설정
    UNION ALL
    SELECT HOUR + 1   -- 이전 값에 1을 더해 다음 HOUR 값을 생성
    FROM TIME         -- 자신(TIME)과 재귀적으로 결합
    WHERE HOUR < 23   -- HOUR이 23이 될 때까지 반복
)
SELECT T.HOUR, COUNT(O.ANIMAL_ID)
FROM TIME T
LEFT JOIN ANIMAL_OUTS O ON T.HOUR = HOUR(O.DATETIME) -- DATETIME 컬럼에서 시간을 추출하여 HOUR로 변환
GROUP BY T.HOUR
ORDER BY T.HOUR
```
