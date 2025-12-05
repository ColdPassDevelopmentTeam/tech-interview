# JOIN 종류

<br>

## 목차
- [JOIN 종류](#join-종류)
  - [목차](#목차)
  - [JOIN 종류](#join-종류-1)
    - [inner join](#inner-join)
    - [outer join](#outer-join)
    - [cross join](#cross-join)
    - [natural join](#natural-join)
    - [self join](#self-join)
  - [전체 그림](#전체-그림)

<br>

## JOIN 종류

예시 테이블

students 테이블

| id | name | dept_id |
| --- | --- | --- |
| 1 | Alice | 10 |
| 2 | Bob | 20 |
| 3 | Carol | 30 |
| 4 | Dave | 40 |

<br>

departments

| id | dept_name |
| --- | --- |
| 10 | Computer |
| 20 | Math |
| 30 | Physics |
| 50 | Chemistry |

<br>

### inner join

- 교집합
- 두 테이블 모두 가지고 있는 데이터만 결과로 나옴
- explicit inner join
    - JOIN 키워드와 ON 절을 사용하여 명시적으로 두 테이블을 조인할 때 사용
    - 코드
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        INNER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - 결과
        
        
        | id | name | dept_name |
        | --- | --- | --- |
        | 1 | Alice | Computer |
        | 2 | Bob | Math |
        | 3 | Carol | Physics |

<br>

- implicit inner join
    - FROM 절에 조인할 테이블들을 콤마로 나열하고, WHERE 절에서 조인 조건을 지정하는 방식
    - 코드
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students, departments
        WHERE students.dept_id = departments.id;
        ```
        
    - 결과
        
        
        | id | name | dept_name |
        | --- | --- | --- |
        | 1 | Alice | Computer |
        | 2 | Bob | Math |
        | 3 | Carol | Physics |

<br>

![image1.png](./img/image1.png)

<br>

### outer join

- left outer join
    - 왼쪽(students) 테이블의 모든 레코드를 보여주고, 일치하지 않는 오른쪽(departments) 테이블 값은 NULL로 채움
    - 코드
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        LEFT OUTER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - 결과
        
        
        | id | name | dept_name |
        | --- | --- | --- |
        | 1 | Alice | Computer |
        | 2 | Bob | Math |
        | 3 | Carol | Physics |
        | 4 | Dave | NULL |

![image2.png](./img/image2.png)

<br>

- right outer join
    - 오른쪽(departments) 테이블의 모든 레코드를 보여주고, 일치하지 않는 왼쪽(students) 값은 NULL로 채움.
    - 코드
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        RIGHT OUTER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - 결과
        
        
        | id | name | dept_name |
        | --- | --- | --- |
        | 1 | Alice | Computer |
        | 2 | Bob | Math |
        | 3 | Carol | Physics |
        | NULL | NULL | Chemistry |

![image3.png](./img/image3.png)

<br>

- full outer join
    - 양쪽 테이블의 모든 레코드를 다 보여주되, 일치하지 않는 값은 NULL로 출력.
    - 코드
        
        ```sql
        SELECT students.id, students.name, departments.dept_name
        FROM students
        FULL OUTER JOIN departments
        ON students.dept_id = departments.id;
        ```
        
    - 결과
        
        
        | id | name | dept_name |
        | --- | --- | --- |
        | 1 | Alice | Computer |
        | 2 | Bob | Math |
        | 3 | Carol | Physics |
        | 4 | Dave | NULL |
        | NULL | NULL | Chemistry |

![image4.png](./img/image4.png)

<br>

### cross join

- 두 테이블의 모든 조합을 만들어 합침.
- 카테시안 곱이라고도 불림
- 코드
    
    ```sql
    SELECT students.name, departments.dept_name
    FROM students
    CROSS JOIN departments;
    ```
    
- 결과
    
    
    | name | dept_name |
    | --- | --- |
    | Alice | Computer |
    | Alice | Math |
    | Alice | Physics |
    | Alice | Chemistry |
    | Bob | Computer |
    | Bob | Math |
    | Bob | Physics |
    | Bob | Chemistry |
    | Carol | Computer |
    | Carol | Math |
    | Carol | Physics |
    | Carol | Chemistry |
    | Dave | Computer |
    | Dave | Math |
    | Dave | Physics |
    | Dave | Chemistry |

![image5.png](./img/image5.png)

<br>

### natural join

- 두 테이블에 이름과 타입이 같은 컬럼들 각각 자동으로 조인 조건 (equi join)으로 사용
- 중복 컬럼은 한번만 보여줌.
- 코드
    
    ```sql
    SELECT *
    FROM students
    NATURAL JOIN departments;
    ```
    
- 결과
    
    
    | id | name | dept_name |
    | --- | --- | --- |
    | 1 | Alice | Computer |
    | 2 | Bob | Math |
    | 3 | Carol | Physics |

<br>

### self join

- 하나의 테이블을 두 개로 간주하여 각각 별칭을 붙여 서로 조인.
- 자기 참조 관계(예, 상하 관계)에서 주로 사용.
- 예시) 직원 테이블에서 상사 찾기
    
    
    | id | name | manager_id |
    | --- | --- | --- |
    | 1 | CEO | NULL |
    | 2 | Alice | 1 |
    | 3 | Bob | 1 |
    | 4 | Carol | 2 |
- 코드
    
    ```sql
    SELECT a.name AS employee, b.name AS manager
    FROM employees a
    JOIN employees b ON a.manager_id = b.id;
    ```
    
- 결과
    
    
    | employee  | manager |
    | --- | --- |
    | Alice | CEO |
    | Bob | CEO |
    | Carol | Alice |

![image6.png](./img/image6.png)

<br>

## 전체 그림
![image7.png](./img/image7.png)