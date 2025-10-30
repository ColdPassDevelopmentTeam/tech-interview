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
