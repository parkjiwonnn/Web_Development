https://school.programmers.co.kr/learn/courses/30/lessons/131124  
코딩테스트 연습 > JOIN > 그룹별 조건에 맞는 식당 목록 출력하기

### 문제 요구사항

MEMBER_PROFILE와 REST_REVIEW 테이블에서 리뷰를 가장 많이 작성한 회원의 리뷰들을 조회하는 SQL문을 작성해주세요. 회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고, 결과는 리뷰 작성일을 기준으로 오름차순, 리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요.

### 정답 코드

```sql
SELECT M.MEMBER_NAME, R.REVIEW_TEXT,
    DATE_FORMAT(R.REVIEW_DATE, '%Y-%m-%d') AS REVIEW_DATE
FROM REST_REVIEW R
INNER JOIN (SELECT MEMBER_ID FROM REST_REVIEW
                     GROUP BY MEMBER_ID
                     ORDER BY COUNT(*) DESC LIMIT 1) AS B
    ON R.MEMBER_ID = B.MEMBER_ID
LEFT OUTER JOIN MEMBER_PROFILE M ON R.MEMBER_ID = M.MEMBER_ID
ORDER BY 3, 2
```
