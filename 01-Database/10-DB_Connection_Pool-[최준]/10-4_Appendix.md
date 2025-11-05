# Appendix

## 퀴즈

- 1번 문제 :
    - Connection만 사용할 때 문제점으로 Connection 생성, 삭제 비용으로 인한 성능 저하가 있다.
- 1번 정답 :
    - O
    - Connection을 생성하고 삭제하는 것은 비용이 굉장히 큼
    - 왜냐하면 네트워크 연결, 세션 초기화 등 비용이 큰 작업을 하기 때문
    - 이러한 일들을 사용할 때마다 매번 하기 때문에 성능 저하 발생

<br>

- 2번 문제 :
    - Connection Pool 크기는 크게 잡는 것이 좋다.
- 2번 정답 :
    - X
    - Thread와 Connection 사이 불균형 발생
    - Thread 개수가 Connection Pool 크기만큼 많으면
        - 자원 사용량 폭증함
    - Thread 개수가 Connection Pool 크기보다 작으면
        - Connection이 놀고 있는 상황 발생 가능

<br>

- 3번 문제 :
    - Connection Pool을 사용 시 Connection 수 부족은 이제 걱정하지 않아도 됨
- 3번 정답 :
    - X
    - Connection Pool 사용해도 크기 설정 잘못하면 Connection 부족한 상황 발생 가능
    - Connection Pool 크기 잘못 설정한다면?
    - 요청에 비해 Connection 수 적은 상황 발생 가능
    - 그러면 대기 시간 증가

<br>

## 참고 자료

- https://steady-coding.tistory.com/564
- https://shuu.tistory.com/130
- https://jiku90.tistory.com/14
- https://tech-interview.tistory.com/218
- https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_connection_pool.md
- https://github.com/cheese10yun/blog-sample/blob/master/kotlin-coroutine/mysql-connection-pool.md
- https://github.com/cheese10yun/blog-sample/blob/master/kotlin-coroutine/mysql-connection-pool-2.md
- https://mangkyu.tistory.com/93