https://school.programmers.co.kr/learn/courses/30/lessons/276035  
코딩테스트 연습 > JOIN > FrontEnd 개발자 찾기

### 문제 요구사항

DEVELOPERS 테이블에서 Front End 스킬을 가진 개발자의 정보를 조회하려 합니다. 조건에 맞는 개발자의 ID, 이메일, 이름, 성을 조회하는 SQL 문을 작성해 주세요. 결과는 ID를 기준으로 오름차순 정렬해 주세요.

### 정답 코드

```sql
SELECT D.ID, D.EMAIL, D.FIRST_NAME, D.LAST_NAME
FROM DEVELOPERS D
WHERE EXISTS (
    SELECT 1
    FROM SKILLCODES S
    WHERE S.CATEGORY = 'Front End'
        AND (D.SKILL_CODE & S.CODE) <> 0
)
ORDER BY
    D.ID ASC;
```

#### 비트연산

& (비트 AND 연산자)  
비트 AND 연산자는 두 숫자의 각 비트를 비교하여 둘 다 1인 비트만 1로 설정  
결과는 두 값에 공통으로 존재하는 비트를 나타냄

<> (NOT EQUAL)  
<>는 SQL에서 "같지 않다"를 의미함, !=와 같은 역할

```sql
(D.SKILL_CODE & S.CODE) <> 0 -- 비트 AND 결과가 0이 아닌 경우
```

결과가 0이 아님: D.SKILL_CODE와 S.CODE에 공통된 비트가 존재함
결과가 0: D.SKILL_CODE와 S.CODE 사이에 공통된 비트가 없음

#### EXISTS

```sql
WHERE EXISTS (
    SELECT 1
    FROM SKILLCODES S
    WHERE S.CATEGORY = 'Front End'
        AND (D.SKILL_CODE & S.CODE) <> 0
)
```

EXISTS는 서브쿼리의 결과가 존재하는지 여부를 확인하는 조건문  
서브쿼리에서 반환된 데이터가 있으면 TRUE, 없으면 FALSE를 반환  
이 연산자는 데이터의 존재 여부만 판단하며, 서브쿼리의 실제 결과값은 반환하지 않음

SELECT 1은 SQL에서 특정 값을 반환하는 간단한 쿼리  
여기서 1은 단순히 숫자 1을 의미하며, 이 쿼리는 데이터베이스에서 "결과가 있다"는 사실만 확인하려는 용도로 자주 사용됨
