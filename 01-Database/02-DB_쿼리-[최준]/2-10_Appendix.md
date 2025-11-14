# Appendix

## 퀴즈

- 1번 문제 :
    - 쿼리 실행 순서는?
- 1번 정답 :
    - **FROM, ON, JOIN  ➡  WHERE  ➡  GROUP BY  ➡  HAVING ➡  SELECT  ➡  DISTINCT  ➡  ORDER BY  ➡  LIMIT, OFFSET**

<br>

- 2번 문제 :
    - GROUP BY가 성능에 영향주는 이유는??
- 2번 정답 :
    - 대량의 데이터 정렬 및 그룹화 수행
    - 행들 그룹화 해야 해서 읽어야 하는데 INDEX 미활용 시 전체 테이블 스캔
    - 임시 테이블 메모리 한계 초과해 디스크에 생기면서 디스크 IO 과다
    - 함수, 계산식 사용 시 값 바뀌어 원본 값 기반 정렬된 INDEX 무효화

<br>

- 3번 문제 :
    - LIKE 패턴 검색이 성능 문제 일으키는 이유는??
- 3번 정답 :
    - 패턴 앞부분에 % 있는 경우 문제 발생
    - %라 모든 값을 다 확인해야 함
    - INDEX 활용 못해 전체 테이블 스캔 발생

<br>

## 참고 자료

- https://cocoon1787.tistory.com/762
- https://github.com/jobhope/TechnicalNote/blob/master/database/DBQuery.md
- https://communities.sas.com/t5/SAS-Tech-Tip/SQL-%EC%BF%BC%EB%A6%AC-%EC%8B%A4%ED%96%89-%EC%88%9C%EC%84%9C/ta-p/942092
- https://kimsyoung.tistory.com/entry/SQL-GROUP-BY-%E4%B8%8A-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%8B%A4%EC%A0%9C-%EC%A0%81%EC%9A%A9-%EB%B0%A9%EB%B2%95
- https://velog.io/@zinu/SQLD-2%EA%B3%BC%EB%AA%A9-SQL-%EA%B8%B0%EB%B3%B8-%EB%B0%8F-%ED%99%9C%EC%9A%A9-%EC%9C%88%EB%8F%84%EC%9A%B0-%ED%95%A8%EC%88%98
- https://1-day-1-coding.tistory.com/13