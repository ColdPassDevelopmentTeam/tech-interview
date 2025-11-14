# EXISTS vs IN

<br>

## 목차
- [EXISTS vs IN](#exists-vs-in)
  - [목차](#목차)
  - [EXISTS vs IN](#exists-vs-in-1)
    - [exists vs in](#exists-vs-in-2)
    - [IN, NOT IN 동작 방식](#in-not-in-동작-방식)
    - [성능 비교](#성능-비교)
    - [요약](#요약)

<br>

## EXISTS vs IN

### exists vs in

| **구분** | **EXISTS** | **IN** |
| --- | --- | --- |
| 용도 | 서브쿼리 결과의 존재 유무 판단 <br> 주 테이블 값과 비교해 서브쿼리에 포함되는지 판단할 때 주로 사용 | 특정 값이 집합/서브쿼리 결과에 포함되는지 확인 |
| 동작 방식 | 메인 쿼리의 각 행마다 서브쿼리 실행, <br> 조건 만족하면 TRUE, 즉시 평가 종료(쇼트서킷) | IN 리스트 전체(서브쿼리 결과 포함)에 대해 값을 비교 |
| NULL 처리 | NULL 값이 있어도 정상적으로 처리 <br> 조건만 맞으면 TRUE | NULL이 포함된 경우(특히 NOT IN) 올바르지 않은 결과 가능 |
| 사용 예 | WHERE EXISTS (SELECT ...) | WHERE id IN (SELECT ...) |
| 비교 대상 | 값의 존재만 체크(값 반환 X) | 동일 값 집합 내 존재 여부 직접 비교 |

<br>

### IN, NOT IN 동작 방식

- IN 동작 방식
    - 컬럼의 값이 주어진 값 list or 서브쿼리 결과에 하나라도 포함되면 TRUE
    - IN절 내부적으로 OR 연산자로 처리
    - IN 리스트에 NULL 있더라도 NULL과 비교는 FALSE로 처리해 NULL 값인 행은 포함 X
    - 예시
        
        ```sql
        WHERE column IN (1, 2, NULL)
        
        WHERE column = 1 OR column = 2 OR column = NULL
        ```
        

<br>

- NOT IN 동작 방식
    - 컬럼의 값이 주어진 값 list or 서브쿼리 결과에 하나도 포함되지 않을 때 TRUE
    - NOT IN절 내부적으로 AND 연산자로 처리
    - NOT IN 리스트에 NULL 포함되면 UNKNOWN 상태되어 결과 전혀 반환되지 않음
    - 예시
        
        ```sql
        WHERE column NOT IN (1, 2, NULL)
        
        WHERE column != 1 AND column != 2 AND column != NULL
        ```
        

<br>

- IN절에 NULL 있는 경우
    - **`IN (100, NULL)`**
    - NULL은 “값이 없음” 의미해 어떤 값과 비교 불가능
    - NULL 값 가진 행은 비교에서 조건 만족하지 않는 것으로 취급
    - 따라서 NULL 값 나온 행이 조회되지 않음
- NOT IN절에 NULL 있는 경우
    - **`NOT IN (100, NULL, 40)`**
    - NULL과 비교한 것과 AND해 결과가 모두 UNKNOWN으로 평가됨
    - 따라서 아무 행도 반환되지 않는 문제 발생

<br>

### 성능 비교

- **서브쿼리 결과가 적을 때**
    - IN이 EXISTS보다 빠를 수 있음.
    - IN절은 서브쿼리 결과를 미리 메모리상에 리스트로 만들어두고 이 리스트에 대해 컬럼 값을 OR 조건으로 빠르게 비교.
    - EXISTS절은 메인 쿼리의 각 행마다 서브쿼리 실행해 조건 확인하는 방식이라 서브쿼리 반복 실행 때문에 느릴 수 있음.
- **서브쿼리 결과가 많을 때**
    - EXISTS가 IN 대비 더 빠른 경향이 있음.
    - EXISTS는 처음 TRUE 되는 순간 검색을 멈춰 빠름.
    - IN은 전체 결과를 모아서 비교하기 때문에 느림.
- **하나의 값만 검사**
    - IN이 간단하고 자연스러움
    - 단일 값 IN 절은 대부분 DBMS에서 ’**=** 연산자’와 동일하게 최적화해 성능 이슈도 없고, 단순 명료
- **컬럼이 인덱싱된 경우**
    - EXISTS가 더 효율적으로 동작 가능
    - EXISTS 내부 서브쿼리가 INDEX 생성된 컬럼을 이용해 조건에 맞는 첫 번째 행을 빠르게 찾으면 곧바로 탐색 종료하기 때문
    - INDEX는 서브쿼리의 컬럼에 걸려 있는 것
    - 원래는 메인 테이블의 컬럼 값이 1001 이라면 서브 쿼리 결과에서 컬럼 값이 1001인 것을 full table scan으로 찾던 것
    - 하지만 서브 쿼리의 컬럼에 index가 걸려 있다면 1001인 것 빠르게 찾을 수 있어 성능 향상되는 것
    - u.id가 1001인 것을 서브 쿼리에서 찾는데 o.user_id에 인덱스 걸려 있어 1001인 것 빠르게 찾는다는 의미
        
        ```sql
        SELECT *
        FROM users u
        WHERE EXISTS (
          SELECT 1
          FROM orders o
          WHERE o.user_id = u.id AND o.status = 'pending'
        );
        ```
        

<br>

### 요약

| **상황/목적** | **추천 구문** | **이유** |
| --- | --- | --- |
| 적은 건수(리스트, 결과) | IN | 가독성, 단순함 |
| 대량 데이터 비교 | EXISTS | 빠른 존재성 체크(쇼트서킷) |
| NULL 가능성 있는 경우 | EXISTS | IN/NOT IN의 NULL로 인한 오류 방지 |
| 인덱스 활용 중요 | EXISTS | 서브쿼리 인덱스 활용 가능 |