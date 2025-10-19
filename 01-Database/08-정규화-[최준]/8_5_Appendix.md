# Appendix

## 퀴즈

- 1번 문제 :
    - 정규화 하지 않은 RDB에서 일어날 수 있는 이상 현상은?
- 1번 정답 :
    - 삽입 이상
        - 원치 않는 정보까지 입력해야 함
    - 삭제 이상
        - 원하지 않는 값까지 함께 삭제됨
    - 갱신 이상
        - 한 곳만 갱신 시 나머지와 불일치 발생

<br>

- 2번 문제 :
    - 정규화의 단점은?
- 2번 정답 :
    - 성능 저하 가능성
        - 조회 시 join 연산이 많아짐
    - 복잡성 증가
        - 테이블과 관계 많아짐
    - 쓰기 작업 비용 증가
        - 여러 테이블에 전부 작업해야 함

<br>

- 3번 문제 :
    - 반정규화를 진행 시 데이터 무결성은 향상되지만 성능이 저하될 수 있다.
- 3번 정답 :
    - X
    - 반정규화는 **성능 향상 목적**으로 **의도적으로 중복 허용**해 **데이터 무결성 저하**될 수 있음

<br>

## 알아보면 좋을 것

- 정규화 과정에서의 자주 하는 실수
- ORM과 정규화
- sql, nosql에서 정규화

<br>

## 참고 자료

### Github
- https://github.com/jbee37142/Interview_Question_for_Beginner/tree/main/Database#%EC%A0%95%EA%B7%9C%ED%99%94%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%EC%A0%95%EA%B7%9C%ED%99%94(Normalization).md
- https://github.com/devham76/tech-interview-study/blob/master/contents/db.md
- https://github.com/Songwonseok/CS-Study/blob/main/Database/%EC%A0%95%EA%B7%9C%ED%99%94.md
- https://github.com/devSquad-study/2023-CS-Study/blob/main/DB/db_erd_normalization.md
- https://github.com/cheese10yun/TIL/blob/master/Database/%EC%A0%95%EA%B7%9C%ED%99%94.md
  
### 블로그
- https://cocoon1787.tistory.com/564
- https://dev-coco.tistory.com/158
- https://goodgid.github.io/DB-Normalization%282%29/
- https://velog.io/@wisdom-one/%EC%A0%95%EA%B7%9C%ED%99%94Normalization
- https://catisstudying.tistory.com/42
- https://soultree.inblog.io/sqld-%EB%B0%98%EC%A0%95%EA%B7%9C%ED%99%94denormalization-part-1-29292
- https://hyeri0903.tistory.com/190