https://school.programmers.co.kr/learn/courses/30/lessons/131532  
코딩테스트 연습 > GROUP BY > 년, 월, 성별 별 상품 구매 회원 수 구하기

### 문제 요구사항

USER_INFO 테이블과 ONLINE_SALE 테이블에서 년, 월, 성별 별로 상품을 구매한 회원수를 집계하는 SQL문을 작성해주세요. 결과는 년, 월, 성별을 기준으로 오름차순 정렬해주세요. 이때, 성별 정보가 없는 경우 결과에서 제외해주세요.

### 정답 코드

```sql
SELECT YEAR(S.SALES_DATE) AS YEAR,
    MONTH(S.SALES_DATE) AS MONTH,
    I.GENDER,
    COUNT(DISTINCT(I.USER_ID)) AS USERS
FROM ONLINE_SALE S
INNER JOIN USER_INFO I
    ON I.USER_ID = S.USER_ID
WHERE I.GENDER IS NOT NULL
GROUP BY 1,2,3
ORDER BY 1,2,3
```
