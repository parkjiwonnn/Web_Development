https://school.programmers.co.kr/learn/courses/30/lessons/59045  
코딩테스트 연습 > JOIN > 보호소에서 중성화한 동물

### 문제 요구사항

보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. 보호소에 들어올 당시에는 중성화1되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.

### 정답 코드

```sql
SELECT I.ANIMAL_ID, I.ANIMAL_TYPE, I.NAME
FROM ANIMAL_INS I
INNER JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE LIKE 'INTACT%'
AND O.SEX_UPON_OUTCOME NOT LIKE 'INTACT%'
ORDER BY ANIMAL_ID ASC
```
