# JOIN에서 vs

<br>

## 목차
- [JOIN에서 vs](#join에서-vs)
  - [목차](#목차)
  - [JOIN에서 VS](#join에서-vs-1)
    - [using vs on](#using-vs-on)
    - [where vs on](#where-vs-on)

<br>

## JOIN에서 VS

### using vs on

- using이란?
    - USING은 JOIN 구문에서 두 테이블을 연결할 때 같은 이름을 가진 컬럼을 기준으로 조인하는 방식
    - 주로 조인하려는 컬럼명이 두 테이블에서 동일할 때 사용
    - 두 테이블에서 같은 이름의 컬럼을 한 번만 작성
    - 결과 테이블에도 해당 컬럼이 한 번만 나타남
    - OUTER JOIN에서 조건을 더 추가하려면 WHERE절 등으로 처리 필요
    - INNER JOIN에서 주로 권장
- using 사용법
    - JOIN 뒤에 USING(조인 컬럼)
    - 예시 (employee, salary 테이블에 emp_no 컬럼 공통으로 가짐)
        
        ```sql
        SELECT *
        FROM employee e
        JOIN salary s
        USING(emp_no);
        ```
        

<br>

- on이란?
    - ON은 SQL JOIN 구문에서 두 테이블을 연결할 때 조인 조건을 명시하는 방식
    - 조인하려는 두 테이블의 컬럼명이 같을 수도, 다를 수도 있어 각 테이블의 컬럼을 명시적으로 지정
    - 결과에는 조인 조건에 사용된 컬럼이 양쪽 테이블 모두 출력 가능
    - 다양한 JOIN 유형에서 사용 가능
- on 사용법
    - JOIN 뒤에 ON 테이블1.컬럼 = 테이블2.컬럼
    - 예시 (employee, salary 테이블에서 employee_id, emp_no가 같은 의미의 컬럼)
    
    ```sql
    SELECT *
    FROM employee e
    JOIN salary s
    ON e.employee_id = s.emp_no;
    ```
    

<br>

- 공통점
    - SQL JOIN에서 두 테이블을 연결하는 조건을 명시하는 구문
- 차이점
    - 컬럼명
        - using은 두 테이블의 컬럼명이 같을 때만 사용 가능
        - on은 컬럼명이 같거나 달라도 사용 가능
    - 결과 컬럼
        - using은 공통 컬럼을 한번만 결과에 표시
        - on은 조인에 사용된 컬럼이 모두 결과에 표시
    - 추가 조건
        - using은 추가 조건 붙이기 어려움 (AND, OR 등)
        - on은 추가 조건, 함수, 연산 등 자유롭게 확장됨
    - 가독성
        - using은 간결하고 중복 컬럼 방지로 가독성이 높음
        - on은 보다 명확하고 복잡한 조건에 길어질 수 있음

<br>

- 장단점
    - 가독성 부분 : using 승 (쿼리 짧음, 결과 중복 컬럼 제거)
    - 확장성 부분 : on 승 (컬럼명 달라도 사용 가능, 조건 확장 가능)

<br>

**성능 이슈**

- 대부분의 DBMS에서 **USING**과 **ON**은 내부적으로 동일한 쿼리 플랜으로 변환
- 단순 컬럼 비교 조인에서는 둘 사이의 성능 차이가 사실상 없음
- 컬럼명이 같고 단순히 조인할 때는 USING 사용
- 컬럼명이 다르거나 추가 조건이 필요한 경우에는 ON 사용
- 가독성, 유지 보수성 중심으로 접근

<br>

### where vs on

- 문제 발생
    - INNER JOIN에서는 ON, WHERE 중 어디에 조건을 넣어도 상관 없음
    - OUTER JOIN에서 결과에 영향을 주고 차이가 생김
- 동작 방식
    - ON
        - JOIN하는 두 테이블을 결합할 때 조인 조건으로 사용
        - 두 테이블을 결합하는 시점에서 조건을 검사해 어떤 행들을 조인할지 결정
        - join 전에 조건을 필터링해 join할 테이블이 줄어듬
        - 조인 대상 행을 결정하는 용도
        - 예시
            
            ```sql
            SELECT *
            FROM A
            INNER JOIN B
            ON A.id = B.id AND A.status = 'active';
            ```
            
    - WHERE
        - JOIN이 완료된 후 결과 행들을 필터링할 때 사용
        - JOIN 결과 중에서 조건을 만족하는 행만 최종 출력
        - join 후에 조건을 필터링해 결과 테이블이 줄어듬
        - 조인 결과를 제한하는 필터링 용도
        - 예시
            
            ```sql
            SELECT *
            FROM A
            INNER JOIN B
            ON A.id = B.id
            WHERE A.status = 'active';
            ```
            

<br>

**결과**

**employee 테이블**

| **employee_id** | **name** |
| --- | --- |
| 1 | Alice |
| 2 | Bob |
| 3 | Carol |
| 4 | David |

**salary 테이블**

| **emp_no** | **amount** |
| --- | --- |
| 1 | 5000 |
| 2 | 6000 |
| 3 | 7000 |

<br>

**LEFT OUTER JOIN - ON 절에 조건**

```sql
SELECT *
FROM employee e
LEFT JOIN salary s
  ON e.employee_id = s.emp_no AND s.amount > 6000;
```

<br>

JOIN할 때부터 amount > 6000인 급여만 employee와 연결

이렇게 join이 된다는 의미

**employee 테이블**

| **employee_id** | **name** |
| --- | --- |
| 1 | Alice |
| 2 | Bob |
| 3 | Carol |
| 4 | David |

**salary 테이블**

| **emp_no** | **amount** |
| --- | --- |
| 3 | 7000 |

<br>

**결과:**

| **employee_id** | **name** | **emp_no** | **amount** |
| --- | --- | --- | --- |
| 1 | Alice | NULL | NULL |
| 2 | Bob | NULL | NULL |
| 3 | Carol | 3 | 7000 |
| 4 | David | NULL | NULL |

<br>

**LEFT OUTER JOIN - WHERE 절에 조건**

```sql
SELECT *
FROM employee e
LEFT JOIN salary s
  ON e.employee_id = s.emp_no
WHERE s.amount > 6000;
```

<br>

JOIN 후 결과에서 salary amount > 6000인 행만 남김 (NOT NULL만 남음).

<br>

**JOIN한 직후 결과**

| **employee_id** | **name** | **emp_no** | **amount** |
| --- | --- | --- | --- |
| 1 | Alice | 1 | 5000 |
| 2 | Bob | 2 | 6000 |
| 3 | Carol | 3 | 7000 |
| 4 | David | NULL | NULL |

<br>

JOIN한 결과에서 amount가 6000 초과인 값만 남기는 것 (NULL도 제거)

<br>

**결과:**

| **employee_id** | **name** | **emp_no** | **amount** |
| --- | --- | --- | --- |
| 3 | Carol | 3 | 7000 |

<br>

**성능 차이** 

OUTER JOIN에서는 ON, WHERE 사용 위치에 따라 성능과 결과가 달라질 수 있다. 

**ON과 WHERE의 경우는 JOIN을 할 대상(범위)이 달라진다.**

<br>

- ON
    - DBMS가 조인 과정에서 미리 조건을 적용
    - 조인 대상이 되는 데이터 양이 줄어듬
    - 조인하는 데이터가 작아져 이후 연산 비용이 감소
- WHERE
    - 조인이 끝난 후 전체 결과에서 조건을 필터링
    - 많은 행이 조인되어 일시적으로 더 큰 결과 만들어짐
    - 큰 결과에서 다시 필터링

<br>

INNER JOIN에서는 ON, WHERE 절 모두 거의 동일한 실행계획을 만들기 때문에 성능 차이가 크지 않다.

OUTER JOIN에서는 ON 절 조건이 조인 시점의 데이터 크기 자체를 줄여 성능상 더 효율적. 

WHERE 절은 조인 이후 데이터를 한 번 더 걸러내기 때문에 처리해야 할 데이터량이 불필요하게 많아져 성능 저하 있을 수 있다.