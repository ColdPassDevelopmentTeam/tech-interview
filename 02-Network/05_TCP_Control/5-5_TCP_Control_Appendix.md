# Appendix

## 퀴즈

- 1번 문제 :
    - 흐름 제어 중 Stop And Wait 방법은 수신자 버퍼가 작아도 문제가 없다.
- 1번 정답 :
    - O
    - Stop And Wait 방법은 수신자가 데이터 처리할 때까지 송신자가 기다려줌
    - 따라서 수신자 버퍼 오버플로우가 발생하지 않음
    - → 수신자 버퍼가 작아도 문제 없음!

- 2번 문제 :
    - 오류 감지 기법 중 Checksum에서 수신한 데이터 + Checksum하면 결과는?
    - 보기
        1. 모든 비트가 0
        2. 모든 비트가 1
        3. 가장 앞 비트가 1
        4. 가장 앞 비트가 0
- 2번 정답 :
    - 2번: 모든 비트가 1
    - 데이터를 1의 보수 덧셈으로 더함
    - 덧셈 결과에 1의 보수 취함 → Checksum
    - 1의 보수 = 비트를 반대로 바꾼 것
    - 덧셈 결과 = ~Checksum
    - ~Checksum + Checksum → 모든 비트가 1

- 3번 문제 :
    - 혼잡 제어의 원칙인 AIMD는
    - 혼잡이 없으면 혼잡 윈도우 크기를 빠르게 (지수적으로) 늘리고
    - 혼잡이 감지되면 혼잡 윈도우 크기를 조금씩 (선형적으로) 줄이는 기법
- 3번 정답 :
    - X
    - **AIMD** = (Additive Increase, Multiplicative Decrease)
    - 혼잡이 없으면 점진적 (선형적으로 천천히) 증가
        - 네트워크의 추가 여유 용량을 조심스럽게 탐색
    - 혼잡이 감지되면 지수적 (지수적으로 빠르게) 감소
        - 네트워크에 가해지는 부하를 빠르게 감소

## 참고 자료

- https://steady-coding.tistory.com/507
- https://gyoogle.dev/blog/computer-science/network/%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%20&%20%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4.html
- https://benlee73.tistory.com/186
- https://young1403.tistory.com/86
- https://nayoungs.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPIP-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4-%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4
- https://velog.io/@jsj3282/TCP-%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4-%EC%98%A4%EB%A5%98%EC%A0%9C%EC%96%B4
- https://jihyeong-ji99hy99.tistory.com/398
- https://80000coding.oopy.io/f5fe190f-bbad-4956-8789-36546f42be83
- https://wormwlrm.github.io/2021/09/23/Overview-of-TCP-and-UDP.html
- https://jjunsu.tistory.com/347
- https://seongduck.tistory.com/146