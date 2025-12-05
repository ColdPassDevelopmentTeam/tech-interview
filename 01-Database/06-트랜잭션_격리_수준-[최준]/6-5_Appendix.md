# Appendix

## 퀴즈

- 1번 문제 :
    - READ_COMMITTED 격리 수준에선 Dirty Read가 일어나지 않는다.
- 1번 정답 :
    - O
    - Dirty Read는 Commit 되지 않은 데이터에도 접근 가능해 발생하는 문제
    - READ_UNCOMMITTED 수준에서만 발생

<br>

- 2번 문제 :
    - 격리 수준이 높아질수록 ______는 강해지고 ______는 낮아진다.
- 2번 정답 :
    - 격리 수준이 높아질수록 데이터 일관성은 강해지고 트랜잭션 동시 처리 성능은 낮아진다.
    - 격리 수준이 높아질수록 Lock의 개수나 적용 범위가 넓어져 데이터 일관성이 높아짐
    - 그에 따라 격리 수준이 높아질수록 트랜잭션 동시 처리 성능이 낮아짐

<br>

- 3번 문제 :
    - READ_COMMITTED에서 트랜잭션 중간에 다른 트랜잭션의 데이터 쓰기를 막는다.
- 3번 정답 :
    - X
    - READ_COMMITTED에서 중간에 다른 트랜잭션의 데이터 쓰기를 막지 않음
    - Unrepeatable Read 발생

<br>

## 추후 알아볼 것

- MVCC란
- Gap Lock이란

<br>

## 참고 자료 & 같이 보면 좋을 자료

- https://mangkyu.tistory.com/299
- https://mangkyu.tistory.com/300
- https://mangkyu.tistory.com/288
- https://github.com/jobhope/TechnicalNote/blob/master/database/IsolationLevel.md
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md
- https://github.com/WeareSoft/tech-interview/blob/master/contents/db.md#%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80
- https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_transaction_isolation_level.md
- https://kjsu0209.github.io/Tech-Interview/database/db