### 트랜잭션 제어어(Transaction Control Language, TCL)

- **START TRANSACTION / BEGIN**
  트랜잭션 블록의 시작을 명시적으로 선언, 많은 DBMS는 기본적으로 AUTOCOMMIT 모드로 동작합니다. 다만 여러 연산을 하나의 트랜잭션으로 묶으려면 이 명령어로 시작해야 합니다.
- **COMMIT**
  현재 트랜잭션을 성공적으로 종료하고 모든 변경 사항을 영구적으로 저장합니다.
  커밋을 완료하면 트랜잭션이 보유하고 있던 모든 LOCK이 해제됩니다.
- **ROLLBACK**
  현재 트랜잭션을 종료하고, 트랜잭션 시작 이후(또는 마지막 SAVEPOINT 이후)의 모든 변경 사항을 취소하고 트랜잭션 시작 이전으로 되돌립니다. 
  비정상적인 종료 시 자동 호출 또는 사용자가 수동으로 실행할 수 있습니다.
  ```SQL
  -- 트랜잭션 시작
  START TRANSACTION;

  -- 1. A의 잔액에서 10,000원 감소
  UPDATE accounts SET balance = balance - 10000 WHERE user = 'A';

  -- 2. B의 잔액에 10,000원 증가
  UPDATE accounts SET balance = balance + 10000 WHERE user = 'B';

  -- 만약 두 작업 사이에 문제가 발생했다면...
  -- ROLLBACK; -- 모든 변경사항을 취소하고 트랜잭션 시작 전으로 되돌림

  -- 모든 작업이 성공적으로 완료되었다면...
  COMMIT; -- 모든 변경사항을 데이터베이스에 영구 저장
  ```
- **SAVEPOINT**
  트랜잭션 내에 저장점을 생성하는 명령어입니다.
  이를 통해 전체 트랜잭션을 롤백하는 대신, 특정 저장점까지만 부분적으로 롤백이 가능합니다.
  예시
  ```SQL
    START TRANSACTION;
    INSERT INTO products (id, name, price) VALUES (1, '상품A', 1000);
    SAVEPOINT A; 
    -- 저장점 A 생성

    INSERT INTO products (id, name, price) VALUES (2, '상품B', 2000);
    SAVEPOINT B; 
    -- 저장점 B 생성

    INSERT INTO products (id, name, price) VALUES (3, '상품C', 3000);

    -- 현재 상태: 상품 A, B, C가 임시로 삽입됨

    ROLLBACK TO SAVEPOINT B; -- 저장점 B 시점으로 롤백 (상품 C 삽입 취소)

    -- 현재 상태: 상품 A, B만 임시로 삽입됨

    COMMIT; -- 최종적으로 상품 A, B의 삽입을 확정
    ```

    