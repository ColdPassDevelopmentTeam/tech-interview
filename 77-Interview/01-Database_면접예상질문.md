# Database 면접 예상 질문

<details>
<summary>SQL에서 LIKE가 무슨 일을 하고 어떠한 경우에 성능 저하를 일으킬 수 있는지 말해주세요</summary>

<br>

- LIKE 는 문자열 데이터에서 문자열 패턴 매칭에 사용되는 키워드입니다.
- 와일드카드라는 특수 문자와 함께 사용되는데 % 기호는 0개 이상의 모든 문자, _는 1개의 단일 문자를 의미합니다.
- LIKE는 %가 패턴의 가장 앞부분에 있는 경우 INDEX 사용이 제한되어 전체 테이블 스캔이 발생해 성능 저하를 일으킬 수 있습니다.

    <details>
    <summary>꼬리질문 : 그렇다면 LIKE의 성능 개선 방법에는 어떤 것이 있는지 알려주세요</summary>
    
    <br>

    - 첫번째 방법으로는 패턴 앞에 %를 피해 index가 효율적으로 사용되게 하는 것입니다.
    - 두번째 방법으로는 패턴 앞에 %가 반드시 필요한 경우 Full Text INDEX나 전문 검색 엔진을 활용하는 것입니다.
    
    </details>
</details>



<details>
<summary>Driving table 선택이 성능에 미치는 영향에 대해 알려주세요</summary>

<br>

- Driving table은 join시 먼저 access되는 테이블이고 Driven table은 Driving table로부터 값을 받아 나중에 access되는 테이블입니다. 
- Driving table의 행 수만큼 반복적으로 Driven table을 조회하기 때문에 행 수가 적고, 조건으로 걸러질 가능성이 높은 테이블을 Driving table로 삼는 것이 효율적입니다.
- 데이터 많은 테이블이 Driving table 되면 반복 조회 횟수 많아져 느려질 수 있습니다.
- 데이터 적은 테이블이 Driving table 되면 반복 조회가 적어져 빨라질 수 있습니다.

    <details>
    <summary>꼬리질문 : index는 Driven, Driving 둘 중 어떤 테이블에 있는게 좋은가요?</summary>
    
    <br>

    - Driven table에 Index가 있는 것이 성능적으로 좋습니다.
    - Index가 있다면 Driven table을 순회하지 않고 빨리 찾을 수 있어서 Driven table 조인 컬럼에 Index 있을 때 성능 좋습니다.
    - Driving table은 일반적으로 한번만 full scan하기 때문에 Driving table에는 있으면 좋지만 없어도 상관 없습니다.

    
    </details>
</details>



<details>
<summary>connection pool이 무엇이고 어떠한 장점이 있나요?</summary>

<br>

- connection pool이란 Connection 객체를 Application 실행 시 미리 일정 수만큼 생성 후 pool에 저장해두고, 필요할 때마다 Connection 할당받아 사용한 뒤 반환하는 기법입니다.
- 장점으로는
- 매번 Connection 생성, 종료에 드는 overhead를 줄여 성능이 향상됩니다.
- 또 동시에 연결되는 Connection 수를 제한해 DB 서버에 과도한 부하 방지할 수 있습니다.
- 마지막으로 Connection 관리를 중앙 집중화해 Connection 누수 및 자원 고갈 문제 방지해 안전성을 향상 시킬 수 있습니다.

    <details>
    <summary>꼬리질문 : connection pool에서 발생 가능한 문제는 어떤 문제가 있나요?</summary>
    
    <br>

    - Connection Pool에 미리 생성된 Connection 수가 Application 동시 요청량보다 부족한 경우 Connection 수 부족으로 인한 대기 시간 증가할 수 있습니다.
    - Connection Pool 크기 너무 크게 설정해 Thread Pool 크기와 Connection Pool 크기 사이 불균형 발생해 connection이 놀고 있거나 Thread 증가로 많은 Context switching 발생할 수 있습니다.
    - Application이 마지막에 Connection 적절히 반환하지 않으면 Connection 누수가 발생해 Pool이 고갈될 수 있습니다.
    - DB 서버가 Connection 끊었는데 Connection Pool은 아직 살아있다고 인식해 죽은 Connection 사용해 쿼리 실행 시 오류가 발생 가능합니다.

    
    </details>
</details>



<details>
<summary>Index는 어떤 컬럼에 거는게 좋을까요?</summary>

<br>

- 카디널리티가 높은 컬럼
- 실제 작업에서 많이 활용되는 컬럼
- INSERT, UPDATE, DELETE가 자주 발생하지 않는 컬럼
- Primary key, 되도록 작은 데이터 타입 가지는 컬럼에 거는 것이 좋습니다.

    <details>
    <summary>꼬리질문 : Index가 적용이 안되는 경우에는 어떠한 경우가 있나요?</summary>
    
    <br>

    - 첫번째로 Index가 설정된 컬럼을 WHERE절 조건으로 걸지 않으면 Index가 적용되지 않고 Full Table Scan이 발생합니다.
    - 두번째로 인덱스 컬럼에 함수를 적용하거나 연산이 들어가면 인덱스가 무시됩니다.
    - 세번째로 LIKE 연산자에서 %가 앞에 위치하는 경우 인덱스가 적용되지 않습니다.
    - 마지막으로 인덱스 컬럼의 데이터 타입과 다른 타입과 비교할 경우 인덱스가 적용되지 않습니다.

    
    </details>
</details>



<details>
<summary>더티 리딩이 무엇이고 왜 이것이 문제가 되나요?</summary>

<br>

- 커밋되지 않은 데이터를 다른 트랜잭션이 읽는 현상입니다. 롤백 시 잘못된 데이터를 참조하게 되어 데이터 일관성이 깨집니다.

    <details>
    <summary>꼬리질문 : 더티 리딩을 방지하기 위해선 어떻게 해야하나요?</summary>
    
    <br>

    - READ COMMITTED 이상의 격리 수준을 사용하거나, 잠금(Lock)으로 커밋 전 데이터 접근을 막습니다.
    
    </details>
</details>



<details>
<summary>만약 현재 S-LOCK으로 트랜잭션을 진행중, X-LOCK 의 쓰기요청이 들어온다면 허용이 될까요?</summary>

- 허용되지 않습니다. S-LOCK은 읽기 전용이기 때문에 쓰기(X-LOCK) 요청은 대기 상태에 들어갑니다.

    <details>
    <summary>꼬리질문 : 낙관적 LOCK 과 비관적 LOCK에 대해 설명이 가능한가요?</summary>

    - 낙관적은 충돌이 드물다고 가정하고 커밋 시점에 검증, 비관적은 처음부터 락을 걸어 충돌을 방지합니다.
    </details>
</details>



<details>
<summary><h3>SQL에서 조인에 대해서 설명해주세요</h3></summary>
    > 두 개의 테이블을 서로 묶어서 하나의 결과를 만들어 내는 것을 의미합니다.
    <details>
    <summary><h4>꼬리질문 : 왼쪽 테이블에 있는 값이 오른쪽 테이블에 없는 값일 때, left 조인과 right 조인을 비교해서 설명해주세요.</h4></summary>
        > left 조인은 왼쪽 테이블 값은 무조건 결과에 포함되고 오른쪽 테이블에 일치하는 값이 없으면 null로 표시됩니다. 반대로 right 조인은 왼쪽 테이블만 있는 값은 제외되고 오른쪽 테이블의 모든 값은 포함됩니다.
    </details>
    <details>
    <summary><h4>꼬리질문 : SQL에서 쿼리의 수행 순서에 대해 설명해주세요.</h4></summary>
        > from, join > where > group by > having > select > distinct > order by > limit, offset
    </details>
</details>



<details>
<summary><h3>데이터 정규화란 무엇인지 설명해주세요.</h3></summary>
    > 데이터의 중복을 최소화하고, 데이터의 일관성 및 무결성을 확보하기 위해 테이블을 분해하는 과정입니다.
    <details>
    <summary><h4>꼬리질문 : 이상 현상의 종류에 대해 알려주세요.</h4></summary>
        > 삽입 이상은 존재하지 않는 값은 삽입 할 수 없는 문제가 발생하는 것이고, 수정 이상은 하나의 데이터를 수정함으로써 데이터의 일관성이 깨져버리는 것이고, 삭제 이상은 데이터를 삭제함으로써 다른 데이터까지 사라지는 문제가 발생하는 것을 의미합니다.
    </details>
</details>



<details>
<summary><h3>DELETE, TRUNCATE, DROP의 차이를 비교해서 설명해주세요.</h3></summary>
    > DELETE는 테이블의 특정 행만 지울 수 있으며 롤백이 가능합니다. 하지만 TRUNCATE는 테이블의 구조만 남기고 모든 행만 지우며 롤백이 불가능합니다. DROP은 테이블 자체의 구조를 지우는 방식이며 역시 롤백이 불가능한 방식입니다.
</details>



<details>
<summary><h3>데이터베이스의 트랜잭션이 가져야 할 ACID 속성에 대해 설명해주세요.</h3></summary>
    > 원자성(A)은 트랜잭션은 모든 연산은 전부 성공하거나 실패해야 한다는 것이고, 일관성은(C)은 트랜잭션 실행 전과 후 일관성 상태를 유지해야 한다는 것이고, 독립성(I)은 여러 트랜잭션이 동시에 실행될 때 각 트랜잭션은 독립적으로 실행되어야 한다는 것이고, 지속성(D)은 성공한 트랜잭션의 결과는 영구적으로 저장되어야 한다는 것입니다.
</details>
