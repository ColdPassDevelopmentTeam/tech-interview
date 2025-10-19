# Appendix

<br>

## Appendix

### 퀴즈

- **1번 문제** :
    - UDP 헤더와 마찬가지로 TCP 헤더도 Source Port에 0을 넣어도 된다.
- **1번 정답** :
    - X
    - TCP는 양방향 통신 위해 반드시 source port 필요함.
    - 또 UDP와 달리 TCP에서는 0번 port는 예약된 port.

<br>

- **2번 문제** :
    - 패킷은 절대 나눠지지 않은 PDU이다.
- **2번 정답** :
    - X
    - 패킷은 네트워크의 MTU보다 크기 큰 경우 나눠짐.
    - 이 경우 Identification 필드로 하나의 패킷임을 확인함.

<br>

- **3번 문제** :
    - 프레임 뒤에 붙는 트레일러의 역할은?
    1. 악의적 공격 방어
    2. 프레임 끝 알리기
    3. 데이터 오류 검출
    4. 옵션 제공
- **3번 정답** :
    - 3.데이터 오류 검출
    - 프레임 뒤에 붙는 트레일러의 역할은 오류 검출.
    - CRC 알고리즘으로 FCS 만들어 송수신측이 비교.

<br>

### 참고 자료

- https://wikidocs.net/275243
- https://www.geeksforgeeks.org/computer-networks/services-and-segment-structure-in-tcp/
- https://mag1c.tistory.com/517
- https://day-night.tistory.com/104
- https://devlog-wjdrbs96.tistory.com/288
- https://freloha.tistory.com/23
- https://stdmoii.tistory.com/34
- https://blog.skby.net/%EC%88%9C%ED%99%98-%EC%A4%91%EB%B3%B5-%EA%B2%80%EC%82%AC-crc-cyclic-redundancy-check/