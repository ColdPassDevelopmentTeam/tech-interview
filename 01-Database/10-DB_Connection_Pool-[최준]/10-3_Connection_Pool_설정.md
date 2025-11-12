# Connection Pool 설정

<br>

## 목차
- [Connection Pool 설정](#connection-pool-설정)
  - [목차](#목차)
  - [Connection Pool 설정](#connection-pool-설정-1)
    - [Connection Pool 주요 설정 옵션](#connection-pool-주요-설정-옵션)
    - [Connection Pool size 설정 공식](#connection-pool-size-설정-공식)

<br>

## Connection Pool 설정

### Connection Pool 주요 설정 옵션

**최대, 최소 커넥션 개수 관련**

- **maximumPoolSize**
    - 동시에 유지할 수 있는 최대 커넥션 수
    - minimumidle과 maximumPoolSize를 보고 커넥션 추가 맺고 끊고 진행
- **minimumIdle**
    - pool에서 유지할 수 있는 최소 쉬고 있는 커넥션 수
- **idleTimeout**
    - 쉬고있는 커넥션을 유지할 최대 시간

<br>

**커넥션 수명, 재생성 관련**

- **maxLifetime**
    - 하나의 커넥션이 pool에서 존재할 수 있는 최대 시간
    - 시간 넘기면 쉬고 있으면 pool에서 바로 제거, 일하고 있으면 pool로 반환된 후 제거
    - DB 세션 타임아웃보다 조금 짧게 설정해 죽은 커넥션 사용 유지 방지
- **keepaliveTime**
    - 오래된 커넥션이 쉬고 있는 상태일 때 연결 유지 위해 요청 보낼 시간

<br>

**커넥션 대기, 타임아웃 관련**

- **connectionTimeout**
    - pool에서 커넥션을 가져올 때 최대 대기 시간
    - 커넥션 받아야 하는데 없다면 얼마나 기다릴지
    - 넘어가면 예외 던짐

<br>

### Connection Pool size 설정 공식

**기본 공식**

- CPU 코어 수와 디스크 I/O 효율을 고려한 공식이 널리 권장
- 공식:
    - $Connection Pool Size = (CPU 코어 수 × 2) + effective_spindle_count$
    - CPU 코어 수: 시스템의 물리적 또는 논리적 CPU 코어 수
    - effective_spindle_count: 하드디스크의 개수 또는 디스크가 처리할 수 있는 동시 I/O 요청 수

<br>

**이유**

- CPU 코어당 2배의 커넥션을 사용하는 이유
    - 디스크, 네트워크 I/O로 인한 스레드 블로킹 시간동안 다른 스레드 실행해 CPU 자원 효과적으로 사용하기 위해서
- effective_spindle_count를 더하는 것은 디스크 I/O 병렬성을 반영하기 위함
    - 여러 개 쿼리 동시에 실행되거나, 데이터 접근 겹치더라도 DB의 각 디스크가 별도로 요청 처리
    - 디스크가 병렬로 처리할 수 있는 I/O(디스크 요청) 처리 능력도 같이 고려하겠다는 뜻
    - DB가 동시에 처리할 수 있는 것을 반영해 늘리는 것

<br>

**고려할 것**

- 최대 커넥션 수는 DB 서버가 감당할 수 있는 한도를 넘지 않도록 주의
- 최대 커넥션 수는 실제 운영 환경에서 부하 테스트를 해가며 조절
- 너무 큰 풀 크기는 메모리 낭비나 컨텍스트 스위칭 오버헤드를 발생시킴
- 너무 작은 풀 크기는 대기 요청 증가로 성능 저하를 유발
- 애플리케이션의 동시성 수준과 트랜잭션 성격에 따라 조정이 필요
- minimumIdle 설정도 중요하며, maximumPoolSize와 적절히 맞추는 것이 바람직