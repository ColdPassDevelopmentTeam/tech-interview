# Index 생성 방법

<br>

## 목차
- [Index 생성 방법](#index-생성-방법)
  - [목차](#목차)
    - [1. 기본 문법](#1-기본-문법)
    - [2. 인덱스 종류별 생성](#2-인덱스-종류별-생성)
    - [3. 인덱스 확인 \& 삭제](#3-인덱스-확인--삭제)

<br>

### 1. 기본 문법

```sql
CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX index_name
ON table_name (column1 [(length)] [ASC|DESC], column2, ...);
```

<br>

테이블 생성 후에도 `ALTER TABLE`로 인덱스 추가 가능.

```sql
ALTER TABLE table_name 
ADD INDEX index_name (column);
```

<br>

- `index_name` : 인덱스 이름 (직접 지정, 생략 시 DBMS가 자동 생성)
- `table_name` : 인덱스를 생성할 테이블
- `column` : 인덱스를 걸 컬럼
- `length` : 문자열 컬럼 인덱스 생성 시 접두사 길이 지정
- `ASC | DESC` : MySQL 8.0 이상부터 지원 (오름차순/내림차순)

<br>

### 2. 인덱스 종류별 생성

(1) 일반 인덱스 (Non-Unique Index)

- 가장 기본적인 인덱스
- 중복 허용
- 하나의 컬럼에만 인덱스를 생성

```sql
CREATE INDEX idx_users_email
ON users (email);
```

<br>

(2) 유니크 인덱스 (Unique Index)

- 컬럼 값 중복 불가.
- 해당 컬럼의 모든 값이 중복되지 않도록 보장하는 인덱스
- UNIQUE 제약 조건을 만족시키며 인덱스도 함께 생성됨
- PRIMARY KEY는 자동으로 UNIQUE 인덱스로 생성

```sql
CREATE UNIQUE INDEX idx_users_username
ON users (username);
```

<br>

(3) 복합 인덱스 (Composite Index)

- 여러 컬럼을 묶어서 하나의 인덱스로 생성.
- **Left-most Rule(접두사 규칙)** 적용됨.
- WHERE 절에서 인덱스의 첫 번째 컬럼을 포함하는 조건으로 검색할 때 매우 효율적
- 컬럼의 순서가 매우 중요

```sql
CREATE INDEX idx_orders_userid_date
ON orders (user_id, created_at);
```

<br>

(4) 부분 인덱스 (Prefix Index)

- VARCHAR나 TEXT 같이 긴 문자열 컬럼의 경우
- 컬럼값 전체가 아닌 앞부분의 일부 글자만을 지정하여 인덱스로 만들 수 있음
- 인덱스의 크기를 줄여 저장 공간을 절약하고, 검색 속도 향상 가능
- 컬럼 뒤에 길이 지정 (아래는 20자만 잘라 인덱스 생성하는 것)

```sql
CREATE INDEX idx_users_email_prefix
ON users (email(20));
```

<br>

(5) 전문 검색 인덱스 (Full-Text Index)

- 자연어 검색용 (문자열 전체 검색 최적화)
- `CHAR`, `VARCHAR`, `TEXT` 같은 텍스트 데이터에서 **내용 전체**를 대상으로 검색하기 위한 인덱스
- `LIKE '%검색어%'` 보다 훨씬 빠르고 정확하게 자연어 검색을 할 수 있음
- 보통 `MATCH() ... AGAINST()` 구문과 함께 사용
- MySQL에서 `CHAR`, `VARCHAR`, `TEXT` 컬럼에 사용 가능

```sql
CREATE FULLTEXT INDEX idx_articles_content
ON articles (content);
```

<br>

(6) 공간 인덱스 (Spatial Index)

- GIS 데이터 타입(`GEOMETRY`, `POINT`, `LINESTRING`, `POLYGON`)에 사용.
- 지도나 좌표와 같은 위치 기반 데이터를 매우 빠르게 검색하기 위해 사용

```sql
CREATE SPATIAL INDEX idx_locations_point
ON locations (location);
```

<br>

### 3. 인덱스 확인 & 삭제

- 인덱스 목록 확인

```sql
SHOW INDEX FROM table_name;
```

- 인덱스 삭제

```sql
DROP INDEX index_name ON table_name;
```