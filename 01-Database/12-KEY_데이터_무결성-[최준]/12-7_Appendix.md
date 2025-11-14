# Appendix

## 퀴즈

- 1번 문제 :
    - 자연키와 대리키 중 자연키를 사용하는 것이 요즘 트렌드다.
- 1번 정답 :
    - X
    - 비즈니스, 업무 규칙과 현실 세계 데이터는 언제든 변할 수 있다.
    - 자연키는 이러한 변화에 매우 취약해 사용하는 것이 좋지 않다.
    - 대리키는 비즈니스와 완전히 분리되어 있어 영향을 받지 않는다.
    - 따라서 대리키를 사용하는 것이 좋다

<br>

- 2번 문제 :
    - FK에는 인덱스가 있어도 되고 없어도 된다.
- 2번 정답 :
    - X
    - FK는 join의 where절에서 사용함
    - FK에 인덱스가 없다면 Full Table Scan 진행함
    - 또 부모 테이블의 데이터 수정, 삭제 시 자식 테이블에 참조하는 데이터 있는지 확인함
    - FK에 인덱스가 없다면 Full Table Scan하니 큰 범위에 Lock을 걸어야 하니 성능에 문제가 됨

<br>

- 3번 문제 :
    - 트랜잭션 성능에 데이터 무결성이 영향을 미친다.
- 3번 정답 :
    - 데이터의 정확성과 일관성을 강하게 보장할수록 트랜잭션 처리 속도 느려짐
    - 왜냐하면 강하게 보장할수록 제약조건 검사, 인덱스 유지 비용, lock 관리 비용 등 커짐

<br>

## 참고 자료

- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Key.md
- https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Database/Key(%ED%82%A4).md
- https://github.com/devham76/tech-interview-study/blob/master/contents/db.md
- https://github.com/Songwonseok/CS-Study/blob/main/Database/%ED%82%A4(Key)%20%EC%A0%95%EB%A6%AC.md
- https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_key.md
- https://inpa.tistory.com/entry/DB-%F0%9F%93%9A-%ED%82%A4KEY-%EC%A2%85%EB%A5%98-%F0%9F%95%B5%EF%B8%8F-%EC%A0%95%EB%A6%AC
- https://untitledtblog.tistory.com/123
- https://cocoon1787.tistory.com/778
- https://bbbicb.tistory.com/77
- https://charstring.tistory.com/116
- https://dkkim2318.tistory.com/43
- https://devbksheen.tistory.com/entry/%EB%B3%B5%ED%95%A9-%ED%82%A4%EC%99%80-%EC%8B%9D%EB%B3%84-%EB%B9%84%EC%8B%9D%EB%B3%84-%EA%B4%80%EA%B3%84-%EB%A7%A4%ED%95%91