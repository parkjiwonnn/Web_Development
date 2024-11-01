https://school.programmers.co.kr/learn/courses/30/lessons/131116  
코딩테스트 연습 > GROUP BY > 식품분류별 가장 비싼 식품의 정보 조회하기

### 문제 요구사항

FOOD_PRODUCT 테이블에서 식품분류별로 가격이 제일 비싼 식품의 분류, 가격, 이름을 조회하는 SQL문을 작성해주세요. 이때 식품분류가 '과자', '국', '김치', '식용유'인 경우만 출력시켜 주시고 결과는 식품 가격을 기준으로 내림차순 정렬해주세요.

### 정답 코드

```sql
SELECT FP.CATEGORY, MP.MAX_PRICE, FP.PRODUCT_NAME
FROM FOOD_PRODUCT FP
INNER JOIN (SELECT CATEGORY, MAX(PRICE) AS MAX_PRICE
FROM FOOD_PRODUCT
WHERE CATEGORY IN ('과자', '국', '김치', '식용유')
GROUP BY CATEGORY) AS MP
ON FP.CATEGORY = MP.CATEGORY AND FP.PRICE = MP.MAX_PRICE
ORDER BY MP.MAX_PRICE DESC
```
