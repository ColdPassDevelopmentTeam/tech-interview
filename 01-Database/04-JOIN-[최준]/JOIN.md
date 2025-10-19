# JOIN

## 목차
1. [JOIN란?](#join이란)
2. [JOIN 종류](#join-종류)
3. [JOIN에서 VS](#join에서-vs)
4. [JOIN과 성능](#join과-성능)
5. [JOIN 사용 시 주의점](#join-사용-시-주의-점)
6. [JOIN 알고리즘](#join-알고리즘)

<br>

## JOIN이란?

### 개념

RDB에서는 중복 데이터 피하기 위해 서로 연관된 데이터 중복 없이 여러 개의 테이블로 나누는 정규화 진행. 

테이블을 분리하는 이유는 효율적인 저장, 데이터 중복 최소화, 무결성 확보, 데이터 일관성 유지 등 때문.

<br>

이렇게 분리된 데이터, 테이블을 다시 결합하여 원하는 정보를 얻을 때 사용하는 것이 JOIN.

<br>

**JOIN**은 데이터베이스에서 두 개 이상의 테이블 연결하여 하나의 테이블처럼 만들어 데이터를 검색하는 방법

RDB에서는 JOIN 연산자를 사용해 두 테이블이 공유하고 있는, 관련 있는 컬럼을 기준으로 행을 합침

<br>

아래와 같은 방법으로 진행

```sql
SELECT 컬럼1, 컬럼2, ...
FROM 테이블1
JOIN 테이블2
ON 테이블1.공통컬럼 = 테이블2.공통컬럼;
```

<br>

관련 있는 id 컬럼을 가지고 두 테이블을 합친 결과 테이블을 만드는 것

![image.png](/img/image.png)

<br>

## JOIN 종류

**예시 테이블**

**students 테이블**

| id  | name  | dept_id |
| --- | ----- | ------- |
| 1   | Alice | 10      |
| 2   | Bob   | 20      |
| 3   | Carol | 30      |
| 4   | Dave  | 40      |

<br>

**departments**

| id  | dept_name |
| --- | --------- |
| 10  | Computer  |
| 20  | Math      |
| 30  | Physics   |
| 50  | Chemistry |

<br>

### inner join

- 교집합
- 두 테이블 모두 가지고 있는 데이터만 결과로 나옴
- **`explicit inner join`**
    - JOIN 키워드와 ON 절을 사용하여 명시적으로 두 테이블을 조인할 때 사용
    - **코드**
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        INNER JOIN departments
        ON students.dept_id = departments.id;
        ```
    
    - **결과**
        
        
        | id  | name  | dept_name |
        | --- | ----- | --------- |
        | 1   | Alice | Computer  |
        | 2   | Bob   | Math      |
        | 3   | Carol | Physics   |
- **`implicit inner join`**
    - FROM 절에 조인할 테이블들을 콤마로 나열하고, WHERE 절에서 조인 조건을 지정하는 방식
    - **코드**
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students, departments
        WHERE students.dept_id = departments.id;
        ```
        
    - **결과**
        
        
        | id  | name  | dept_name |
        | --- | ----- | --------- |
        | 1   | Alice | Computer  |
        | 2   | Bob   | Math      |
        | 3   | Carol | Physics   |

<br>

![image.png](/img/image1.png)

### outer join

- **`left outer join`**
    - 왼쪽(students) 테이블의 모든 레코드를 보여주고, 일치하지 않는 오른쪽(departments) 테이블 값은 NULL로 채움
    - **코드**
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        LEFT OUTER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - **결과**
        
        
        | id  | name  | dept_name |
        | --- | ----- | --------- |
        | 1   | Alice | Computer  |
        | 2   | Bob   | Math      |
        | 3   | Carol | Physics   |
        | 4   | Dave  | NULL      |

<br>

![image.png](/img/image2.png)

<br>

- **`right outer join`**
    - 오른쪽(departments) 테이블의 모든 레코드를 보여주고, 일치하지 않는 왼쪽(students) 값은 NULL로 채움.
    - **코드**
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        RIGHT OUTER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - **결과**
        
        
        | id   | name  | dept_name |
        | ---- | ----- | --------- |
        | 1    | Alice | Computer  |
        | 2    | Bob   | Math      |
        | 3    | Carol | Physics   |
        | NULL | NULL  | Chemistry |

<br>

![image.png](/img/image3.png)

<br>

- **`full outer join`**
    - 양쪽 테이블의 모든 레코드를 다 보여주되, 일치하지 않는 값은 NULL로 출력.
    - **코드**
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        FULL OUTER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - **결과**
        
        
        | id   | name  | dept_name |
        | ---- | ----- | --------- |
        | 1    | Alice | Computer  |
        | 2    | Bob   | Math      |
        | 3    | Carol | Physics   |
        | 4    | Dave  | NULL      |
        | NULL | NULL  | Chemistry |

<br>

![image.png](/img/image4.png)

<br>

### cross join

- 두 테이블의 모든 조합을 만들어 합침.
- 카테시안 곱이라고도 불림
- **코드**
    
    ```sql
    SELECT students.name, departments.dept_name
    FROM students
    CROSS JOIN departments;
    ```
    
- **결과**
    
    
    | name  | dept_name |
    | ----- | --------- |
    | Alice | Computer  |
    | Alice | Math      |
    | Alice | Physics   |
    | Alice | Chemistry |
    | Bob   | Computer  |
    | Bob   | Math      |
    | Bob   | Physics   |
    | Bob   | Chemistry |
    | Carol | Computer  |
    | Carol | Math      |
    | Carol | Physics   |
    | Carol | Chemistry |
    | Dave  | Computer  |
    | Dave  | Math      |
    | Dave  | Physics   |
    | Dave  | Chemistry |

<br>

![image.png](/img/image5.png)

<br>

### natural join

- 두 테이블에 이름과 타입이 같은 컬럼들 각각 자동으로 조인 조건 (equi join)으로 사용
- 중복 컬럼은 한번만 보여줌.
- **코드**
    
    ```sql
    SELECT *
    FROM students
    NATURAL JOIN departments;
    ```
    
- **결과**
    
    
    | id  | name  | dept_name |
    | --- | ----- | --------- |
    | 1   | Alice | Computer  |
    | 2   | Bob   | Math      |
    | 3   | Carol | Physics   |

<br>

### self join

- 하나의 테이블을 두 개로 간주하여 각각 별칭을 붙여 서로 조인.
- 자기 참조 관계(예, 상하 관계)에서 주로 사용.
- 예시: 직원 테이블에서 상사 찾기
    
    
    | id  | name  | manager_id |
    | --- | ----- | ---------- |
    | 1   | CEO   | NULL       |
    | 2   | Alice | 1          |
    | 3   | Bob   | 1          |
    | 4   | Carol | 2          |
- **코드**
    
    ```sql
    SELECT a.name AS employee, b.name AS manager
    FROM employees a
    JOIN employees b ON a.manager_id = b.id;
    ```
    
- **결과**
    
    
    | employee | manager |
    | -------- | ------- |
    | Alice    | CEO     |
    | Bob      | CEO     |
    | Carol    | Alice   |

<br>

![image.png](/img/image6.png)

<br>

![image.png](/img/image7.png)

<br>

## JOIN에서 VS

### using vs on

- **using이란?**
    - USING은 JOIN 구문에서 두 테이블을 연결할 때 같은 이름을 가진 컬럼을 기준으로 조인하는 방식
    - 주로 조인하려는 컬럼명이 두 테이블에서 동일할 때 사용
    - 두 테이블에서 같은 이름의 컬럼을 한 번만 작성
    - 결과 테이블에도 해당 컬럼이 한 번만 나타남
    - OUTER JOIN에서 조건을 더 추가하려면 WHERE절 등으로 처리 필요
    - INNER JOIN에서 주로 권장

- **using 사용법**
    - JOIN 뒤에 USING(조인 컬럼)
    - 예시 (employee, salary 테이블에 emp_no 컬럼 공통으로 가짐)
        
        ```sql
        SELECT *
        FROM employee e
        JOIN salary s
        USING(emp_no);
        ```

<br>
        
- **on이란?**
    - ON은 SQL JOIN 구문에서 두 테이블을 연결할 때 조인 조건을 명시하는 방식
    - 조인하려는 두 테이블의 컬럼명이 같을 수도, 다를 수도 있어 각 테이블의 컬럼을 명시적으로 지정
    - 결과에는 조인 조건에 사용된 컬럼이 양쪽 테이블 모두 출력 가능
    - 다양한 JOIN 유형에서 사용 가능

- **on 사용법**
    - JOIN 뒤에 ON 테이블1.컬럼 = 테이블2.컬럼
    - 예시 (employee, salary 테이블에서 employee_id, emp_no가 같은 의미의 컬럼)
    
    ```sql
    SELECT *
    FROM employee e
    JOIN salary s
    ON e.employee_id = s.emp_no;
    ```

<br>

- **공통점**
    - SQL JOIN에서 두 테이블을 연결하는 조건을 명시하는 구문
- **차이점**
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

- **장단점**
    - 가독성 부분 : using 승 (쿼리 짧음, 결과 중복 컬럼 제거)
    - 확장성 부분 : on 승 (컬럼명 달라도 사용 가능, 조건 확장 가능)

**`성능 이슈`**

- 대부분의 DBMS에서 **USING**과 **ON**은 내부적으로 동일한 쿼리 플랜으로 변환
- 단순 컬럼 비교 조인에서는 둘 사이의 성능 차이가 사실상 없음
- 컬럼명이 같고 단순히 조인할 때는 USING 사용
- 컬럼명이 다르거나 추가 조건이 필요한 경우에는 ON 사용
- 가독성, 유지 보수성 중심으로 접근
****
### where vs on

- **문제 발생**
    - INNER JOIN에서는 ON, WHERE 중 어디에 조건을 넣어도 상관 없음
    - OUTER JOIN에서 결과에 영향을 주고 차이가 생김

- **동작 방식**
    - **ON**
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
            
    - **WHERE**
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
| --------------- | -------- |
| 1               | Alice    |
| 2               | Bob      |
| 3               | Carol    |
| 4               | David    |

<br>

**salary 테이블**

| **emp_no** | **amount** |
| ---------- | ---------- |
| 1          | 5000       |
| 2          | 6000       |
| 3          | 7000       |

<br>

LEFT OUTER JOIN - ON 절에 조건

```sql
SELECT *
FROM employee e
LEFT JOIN salary s
  ON e.employee_id = s.emp_no AND s.amount > 6000;
```

<br>

JOIN할 때부터 amount > 6000인 급여만 employee와 연결

이렇게 join이 된다는 의미

<br>

**employee 테이블**

| **employee_id** | **name** |
| --------------- | -------- |
| 1               | Alice    |
| 2               | Bob      |
| 3               | Carol    |
| 4               | David    |

<br>

**salary 테이블**

| **emp_no** | **amount** |
| ---------- | ---------- |
| 3          | 7000       |

<br>

**결과:**

| **employee_id** | **name** | **emp_no** | **amount** |
| --------------- | -------- | ---------- | ---------- |
| 1               | Alice    | NULL       | NULL       |
| 2               | Bob      | NULL       | NULL       |
| 3               | Carol    | 3          | 7000       |
| 4               | David    | NULL       | NULL       |

<br>

LEFT OUTER JOIN - WHERE 절에 조건

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

JOIN한 직후 결과

| **employee_id** | **name** | **emp_no** | **amount** |
| --------------- | -------- | ---------- | ---------- |
| 1               | Alice    | 1          | 5000       |
| 2               | Bob      | 2          | 6000       |
| 3               | Carol    | 3          | 7000       |
| 4               | David    | NULL       | NULL       |

<br>

JOIN한 결과에서 amount가 6000 초과인 값만 남기는 것 (NULL도 제거)

<br>

**결과:**

| **employee_id** | **name** | **emp_no** | **amount** |
| --------------- | -------- | ---------- | ---------- |
| 3               | Carol    | 3          | 7000       |

<br>

**`성능 차이`** 

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

<br>

## JOIN과 성능

### Driving table 선택이 성능에 미치는 영향

**`Driving table, Driven table이란`**

- **Driving table**
    - Join시 먼저 access되는 테이블
    - outer table이라고도 불림
    - 2중 for문의 바깥쪽 for문 느낌

- **Driven table**
    - Driving table로부터 값을 받아 나중에 access되는 테이블
    - inner table이라고도 불림
    - 2중 for문의 안쪽 for문 느낌

<br>

**`동작 방식`**

- join 실행 시 2개 테이블 중 Driving, Driven table 선택됨
- join은 Driving 테이블의 join 조건 행 값 == Driven 테이블의 join 조건 행 값 찾아서 join 수행
- 각 Driving 테이블 행에 대해 Driven 테이블 행을 순회하면서 같은 값 찾는 것
- Driving 테이블의 각 행에 대해 Driven 테이블에서 조건에 맞는 데이터를 찾는 방식으로 진행
- 아래 코드와 비슷한 느낌
    
    ```java
    Driving Table 배열 길이 = 500000;
    Driven Table 배열 길이 = 1000;
    
    for(int i=0; i<500000; i++){  <- Driving Table
    	for(int j=0; j<1000; j++){  <- Driven Table
    		if(Driving Table[i]==Driven Table[j]){
    			// Join 수행!
    			break;
    		}
    	}
    }
    ```
    
- Driving table이 데이터 5000만 건이고 Driven table이 1000건이면 5000만번 반복해 Driven table 확인
- Driving table이 데이터 1000건이고 Driven table이 5000만 건이면 1000번 반복해 Driven table 확인

<br>

**`Driving table 선택이 성능에 미치는 영향`**

- **Driving table의 행 수만큼 반복적으로 Driven table을 조회**
    - 행 수가 적고, 조건으로 걸러질 가능성이 높은 테이블을 Driving table로 삼는 것이 효율적

- **데이터 수에 따른 Driving table 선택**
    - 데이터 많은 테이블이 Driving table 되면 반복 조회 횟수 많아져 느려질 수 있음
    - 데이터 적은 테이블이 Driving table 되면 반복 조회가 적어져 빨라질 수 있음
- **index는 어떤 테이블에??**
    - Driven table에는 조인 컬럼에 Index 있을 때 성능 좋음
        - Index가 있다면 Driven table 순회하지 않고 빨리 찾을 수 있어서
        - O(MN)에서 O(MlogN) 되는 느낌 (B-Tree 인덱스)
    - Driving table에는 있으면 좋지만 없어도 상관 없음
        - Driving table은 일반적으로 한번만 full scan

<br>

- 가장 작은 결과 집합이 되는 테이블을 Driving table로 잡는 것이 일반적인 원칙

- 옵티마이저는 통계정보, 인덱스 존재 여부, 조인 조건 등을 바탕으로 자동으로 어떤 테이블을 Driving table로 사용할지 결정

- 특별한 경우 hint로 개발자가 직접 Driving table 지정 가능

- LEFT JOIN의 경우에는 일반적으로 좌측 테이블, RIGHT JOIN은 우측 테이블이 Driving table

<br>

### join과 index

- **join시 index가 없다면**
    - **전체 테이블 스캔 발생**
        - 조인 조건에 맞는 데이터 위치 찾아야 함
        - index가 없어 전체 테이블 스캔 발생
        - IO 비용, 처리 시간 증가함
    
    - **조인 버퍼 사용으로 인한 메모리 부하 증가**
        - 전체 테이블 스캔 발생하니 불필요한 디스크 IO 피하기 위해 버퍼에 데이터 올려 조인
        - 매칭 후보 레코드를 메모리 버퍼에 미리 적재해서 재사용
        - 조인 및 결과 생성에 필요한 컬럼만 조인 버퍼에 적재
        - 이로 인해 메모리 사용량 크게 증가
        - 메모리 부족 시 디스크 스와핑 발생해 응답 지연, 성능 저하
        - index 사용하면 조인 버퍼 사용 X
    
    - **join 알고리즘 제한 및 최적화 실패**
        - Nested Loop Join 등 인덱스를 활용하는 효율적인 알고리즘 사용 X
        - Hash Join이나 Sort Merge Join 같은 대체 알고리즘을 강제 사용
        - 메모리, CPU 사용량 증가 (hash table 생성, 정렬)

<br>

- **join시 index가 있다면**
    - **조인 조건에 맞는 레코드만 찾으므로 매우 빠른 성능 발휘**
        - 전체 테이블 스캔 피해 성능 향상
        - index 활용하는 효율적인 join 알고리즘 사용 가능
        - 조인 버퍼 사용하지 않아 메모리 사용량 낮춤
        - 불필요한 연산, IO 작업 감소해 성능 개선
    
    - **실제 성능 차이 사례**
        - **MySQL 사례**: index 추가 전 5-6초 → index 추가 후 0.07초 (약 70배 개선)
        - **10만 건 데이터**: index  없으면 1분 55초 → index 있으면 1초 미만

<br>

- **join에서 index 사용 시 주의할 점**
    - **join 컬럼 데이터 타입 일치 필요**
        - 조인 컬럼의 데이터 타입, 문자 set 이 다르면 index 못 타는 경우가 있음
        - 또 자동 형변환 동작해 비용 발생하고 인덱스 사용 문제 생김
    
    - **join 조건에 함수, 연산자 주의**
        - 조인 조건에 함수, 연산자 등 사용 시 index 무시됨
        - Equi Join은 인덱스가 있다면 효율적으로 조인할 수 있고 성능이 좋음
        - Non Equi Join은 조인 조인 조건에 부등호 등 연산자 사용되어 인덱스 활용이 제한적으로 되어 성능 저하 일어날 수 있음
    
    - **복합 인덱스 활용**
        - 여러 컬럼 동시에 조인하면 복합 인덱스 고려
        - 순서 중요한데 자주 조인하는 컬럼을 복합 인덱스 앞쪽에 배치
    
    - **join 대신 대체 수단 고려**
        - 조인 부담될 때 윈도우 함수 등으로 대체 가능성도 고려 가능
    
    - **join은 무거운 연산**
        - join은 무거운 연산이라 과도하게 남발 X

<br>

### join 순서가 성능에 미치는 영향

- **Driving table을 작게하는 것이 중요함**
    - Driving table이 작으면 비교하는 행 수가 적어져 전체 join 연산 부담 감소
    
    - 여러 테이블 조인하는 경우도 순서 제어해 Driving table 작게
        - 어떤 순서로 join하는가에 따라 중간 결과 집합 (=Driving table 역할) 크기가 크게 바뀜
        - 작은 결과 집합 먼저 만들어지도록 해야 함
    
    - where 조건으로 많이 필터링 되어 데이터 줄어들 수 있는 테이블을 앞에 배치
        - 쿼리 논리적 실행 순서는 join > where
        - 하지만 실제는 옵티마이저가 순서 바꿔서 실행 가능
        - where로 데이터 많이 줄일 것 같으면 where 먼저 실행

- **Driven table에 index가 있는 것이 중요함**

- **INNER JOIN, OUTER JOIN에서 순서**
    - **INNER JOIN의 경우**
        - 두 테이블 간에 조인 조건에 맞는 공통 데이터(교집합)만 결과에 포함
        - 조인 순서를 바꿔도 결과는 같음 (교집합의 특성상)
        - 데이터베이스 옵티마이저는 조인 순서를 유연하게 바꿔가며 성능 최적화를 시도
        - 실행 순서 변경이 결과에 영향을 주지 않으면서, 비용을 최소화하는 방향으로 조정 가능
    
    - **OUTER JOIN의 경우**
        - 한 쪽 테이블의 모든 행을 반드시 포함
        - 조인 순서가 논리적인 결과에 영향 줌
        - LEFT OUTER JOIN에서 왼쪽/오른쪽 테이블 위치를 바꾸면 결과 집합 자체가 달라짐
        - 옵티마이저가 임의로 순서를 바꾸기 어렵고, 개발자가 순서를 명확히 지정해야 함
        - 잘못 조인 순서를 지정하면 예상치 못한 결과가 나오거나 불필요한 조인 비용이 발생 가능

<br>

## JOIN 사용 시 주의 점

### outer join 시 주의점

- **join 조건의 where, on 사용 시 차이점**
    - **on절** :
        - join할 때 조건 적용하여 어떤 행끼리 join할지 결정
        - left outer join 예시로 보면
        - right 테이블에 조건에 맞는 행 join되고 나머지 행은 NULL이 됨
        - left 테이블에 행은 모두 유지됨
    - **where절** :
        - join이 끝난 전체 결과에서 추가로 행을 걸러내는 필터 역할함
        - left outer join 예시로 보면
        - 조건에 맞는 경우 right 테이블이던 left 테이블이던 모든 행이 사라질 수 있음
    - 조인 조건은 on절에, 결과 필터링은 where절에

- **NULL 값 처리 주의**
    - 한쪽 테이블에 매칭되는 행이 없다면 컬럼들이 NULL로 채워짐
    - join 이후 조건문이나 집계 함수에서 NULL값 고려해야 함
    - COALESCE() 같은 함수로 대체하거나 IS NULL 조건 사용해야 함

- **join 대상 컬럼에 NULL 값 있는 경우**
    - inner join은 join 키가 NULL인 경우 해당 행은 결과에서 완전히 제외됨
    - outer join은 키가 NULL이여도 기준 테이블의 모든 행을 결과에 항상 포함함

- **중복 행 발생**
    - OUTER JOIN 시 기준 테이블 행 하나에 대해 join되는 테이블에 동일한 키가 여러 개 있으면 결과가 예상보다 행이 늘어나게 됨.
    - 이 점을 고려하여 필요 시 DISTINCT, GROUP BY 또는 서브쿼리, 윈도우 함수 등을 사용해야 함

<br>

## JOIN 알고리즘

### 종류 & 동작 방식

- **nested loop join**
    - 가장 기본적이고 단순한 방식
    - Driving table의 각 행에 대해 Driven table의 모든 행과 반복 비교하며 join 조건 만족하는 데이터 찾음

- **sort merge join**
    - join에 사용할 컬럼 기준으로 두 테이블 먼저 정렬
    - 정렬된 데이터를 양쪽에서 순차적으로 비교하며 join 수행

- **hash join**
    - 한 쪽 테이블 (주로 작은 테이블)을 해시 테이블로 만듬
    - 다른 테이블의 각 행에 해시 함수 적용해 빠르게 매칭되는 데이터 찾아 join

<br>

### 장단점

- **nested loop join**
    - 데이터가 적을 때 효율적
    - 데이터 많아질수록 성능 급격히 저하됨
    - 단순 구현이 장점
    - index 활용하면 조금 더 성능 끌어올릴 수 있음

- **sort merge join**
    - 데이터 미리 정렬되어 있거나, 조인에 사용되는 컬럼 index 있으면 매우 효율적
    - 대량의 데이터 처리할 때 좋은 성능 보임
    - 정렬 연산에 따른 추가 비용 발생 가능

- **hash join**
    - 대량 데이터 조인에 성능이 좋음
        - 정렬과 전체 단순 비교 없어 연산량이 적음
    - equi join에 주로 사용됨
    - 메모리 사용량이 많음
        - 해시 테이블을 만들어야 하기 때문
    - 작은 테이블에 적합함
    - 양쪽 테이블 크기가 많이 다를 때 효율적임
        - 작은 테이블을 해시 테이블로 만들고
        - 큰 테이블은 한 줄씩 읽어와 매칭 여부만 확인하면 됨