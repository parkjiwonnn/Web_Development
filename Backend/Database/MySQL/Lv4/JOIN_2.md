https://school.programmers.co.kr/learn/courses/30/lessons/131117  
코딩테스트 연습 > JOIN > 5월 식품들의 총매출 조회하기

### 문제 요구사항

FOOD_PRODUCT와 FOOD_ORDER 테이블에서 생산일자가 2022년 5월인 식품들의 식품 ID, 식품 이름, 총매출을 조회하는 SQL문을 작성해주세요. 이때 결과는 총매출을 기준으로 내림차순 정렬해주시고 총매출이 같다면 식품 ID를 기준으로 오름차순 정렬해주세요.

### 정답 코드

```sql
SELECT P.PRODUCT_ID, P.PRODUCT_NAME,
    SUM(P.PRICE*O.AMOUNT) AS TOTAL_SALES
FROM FOOD_PRODUCT P, FOOD_ORDER O
WHERE P.PRODUCT_ID = O.PRODUCT_ID
AND O.PRODUCE_DATE LIKE '2022-05-%'
GROUP BY PRODUCT_ID
ORDER BY TOTAL_SALES DESC, PRODUCT_ID ASC
```
