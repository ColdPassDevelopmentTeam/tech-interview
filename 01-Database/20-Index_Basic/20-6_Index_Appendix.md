# Index 부록

<br>

## 목차
- [Index 부록](#index-부록)
  - [목차](#목차)
    - [퀴즈](#퀴즈)
    - [더 공부할 것](#더-공부할-것)

<br>

### 퀴즈

퀴즈 1
- Index는 SELECT, INSERT, DELETE 성능 향상에 도움이 된다?
  
정답 1
- X
- Index는 SELECT 성능에 도움을 줌
- INSERT, DELETE, UPDATE은 크게 성능 저하

<br>

퀴즈 2
- 실행 계획 결과의 type 컬럼이 range라면 Index가 활용되고 있는 것이다.
  
정답 2
- O
- range는 범위 검색에 Index가 활용이 되었다는 의미
- type이 ALL을 제외하면 다 Index 활용은 된다는 의미
  - but 활용되는 방법이 다른 것   

<br>

퀴즈 3
- OR 조건에서 각 조건 컬럼에 Index가 존재해도 Full Table Scan 일어날 수 있다. 
  
정답 3
- O
- 여러 Index 중 어떤 것 사용할지 옵티마이저가 판단 못할 수 있음
- 또 Index 사용해도 Index merge 비용이 있어 옵티마이저가 Index 사용 포기할 수 있음

<br>

### 더 공부할 것

- 트랜잭션 & 락 관련
- join 관련
- Range Query 관련
- 커버링 인덱스
- prefix index
- full text index
    - MATCH() ... AGAINST()
- Function-based index
- spatial index
- SARGable
- INSERT와 페이지 분할(Page Split)
- 인덱스 조각화 (Fragmentation)

