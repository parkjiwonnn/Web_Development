https://school.programmers.co.kr/learn/courses/30/lessons/301650  
코딩테스트 연습 > SELECT > 특정 세대의 대장균 찾기

### 문제 요구사항

3세대의 대장균의 ID(ID) 를 출력하는 SQL 문을 작성해주세요. 이때 결과는 대장균의 ID 에 대해 오름차순 정렬해주세요.

### 정답 코드

```sql
SELECT A.ID
FROM ECOLI_DATA AS A
JOIN ECOLI_DATA AS B ON A.PARENT_ID = B.ID
JOIN ECOLI_DATA AS C ON B.PARENT_ID = C.ID
WHERE C.PARENT_ID IS NULL
ORDER BY A.ID ASC;
```
