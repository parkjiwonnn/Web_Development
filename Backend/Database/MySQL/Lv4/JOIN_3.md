https://school.programmers.co.kr/learn/courses/30/lessons/133027  
코딩테스트 연습 > JOIN > 주문량이 많은 아이스크림들 조회하기

### 문제 요구사항

7월 아이스크림 총 주문량과 상반기의 아이스크림 총 주문량을 더한 값이 큰 순서대로 상위 3개의 맛을 조회하는 SQL 문을 작성해주세요.

### 정답 코드

```sql
SELECT F.FLAVOR
FROM FIRST_HALF F
LEFT OUTER JOIN JULY J
    ON F.FLAVOR = J.FLAVOR
GROUP BY F.FLAVOR
ORDER BY SUM(F.TOTAL_ORDER+J.TOTAL_ORDER) DESC
LIMIT 3
```
