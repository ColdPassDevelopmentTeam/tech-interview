# Appendix

## 퀴즈

- 1번 문제 :
    - USING과 ON 둘 중 USING는 추가 조건을 붙이기 쉽다
- 1번 정답 :
    - X
    - ON이 추가 조건 붙이기 좋음
    - USING은 컬럼명 같을 때만 사용해 간결, 가독성 높음

<br>

- 2번 문제 :
    - WHERE과 ON 둘 중 ON이 성능이 더 좋다.
- 2번 정답 :
    - O
    - ON절이 join할 테이블의 크기 자체 줄임
    - join하는 데이터가 작아져 연산 비용 감소

<br>

- 3번 문제 :
    - Driving table과 Driven table 중 Driving table에 INDEX가 있는 것이 좋다.
- 3번 정답 :
    - X
    - Driven table에 INDEX가 있어야 Driven table 순회하지 않고 빨리 찾을 수 있어서 성능O(MN)에서 O(MlogN)

<br>

## 참고 자료

- https://github.com/jobhope/TechnicalNote/blob/master/database/AboutJoin.md
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDatabase%20SQL%5D%20JOIN.md
- https://github.com/WeareSoft/tech-interview/blob/master/contents/db.md#join
- https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Database/SQL%20-%20Join.md
- https://github.com/devham76/tech-interview-study/blob/master/contents/db.md
- https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_join.md
- https://github.com/Songwonseok/CS-Study/blob/main/Database/JOIN.md
- https://dev-coco.tistory.com/158