# 전송계층과 주요 프로토콜

전송계층은 **송신자와 수신자를 연결하는 통신 서비스**를 제공하는 계층으로, 쉽게 말해 **데이터의 전달을 책임지는 역할**을 한다.  
이 계층의 대표적인 프로토콜은 **UDP**와 **TCP**이다.  

---

## UDP (User Datagram Protocol)

UDP는 **단순하고 빠른 전송**을 위한 프로토콜이다.  

### 특징
- **비연결형**: 연결 과정이 없음  
- **신뢰성 없음**: 수신 여부, 순서 보장하지 않음  
- **간단한 구조**: IP 주소와 포트 번호만 보고 전송  
- **활용 예시**: DNS 조회, 온라인 게임, 실시간 스트리밍  

### 비유
- **편지 봉투에 주소만 쓰고 우체통에 넣는 것**과 같다.  

### 헤더 구조 (8바이트 고정)
1. **Source Port (송신 포트, 16bit)**  
2. **Destination Port (수신 포트, 16bit)**  
3. **Length (전체 길이, 16bit)**  
4. **Checksum (오류 검출, 16bit)**  

### 응용
- **RTP, QUIC** 같은 프로토콜은 UDP 위에서 신뢰성·암호화를 보강한다.  

---

## TCP (Transmission Control Protocol)

TCP는 **신뢰성 있는 데이터 전송**을 보장하는 프로토콜이다.  

### 1. 연결 과정 – 3 Way Handshake
1. 클라이언트 → 서버: **SYN** (연결 요청) → `SYN_SENT`  
2. 서버 → 클라이언트: **SYN + ACK** (요청 수락) → `SYN_RECEIVED`  
3. 클라이언트 → 서버: **ACK** (확인) → `ESTABLISHED`  

### 2. 연결 종료 – 4 Way Handshake
1. 클라이언트: **FIN**  
2. 서버: **ACK** (확인) + `TIME_WAIT` 상태  
3. 서버: **FIN**  
4. 클라이언트: **ACK** (확인) → 연결 종료  

### 3. TCP 헤더 주요 필드
- **Source/Destination Port (포트 번호, 16bit씩)**  
- **Sequence Number (32bit)**: 데이터 순서 지정  
- **Acknowledgment Number (32bit)**: 수신 확인  
- **Flags (SYN, ACK, FIN, RST, PSH, URG 등)**  
- **Window Size (16bit)**: 수신 가능한 데이터 양  
- **Checksum (16bit)**: 오류 검출  
- **Options (가변)**: 확장 기능 (MSS, Timestamp 등)  

---

## TCP의 문제와 해결책

### 문제 상황
- **손실**: 패킷 유실  
- **순서 바뀜**: 패킷 순서 뒤섞임  
- **혼잡(Congestion)**: 네트워크 과부하  
- **Overload**: 수신 측 버퍼 초과  

### 해결 방법
- **흐름 제어 (Flow Control)**  
  - **Sliding Window** 메커니즘 사용  
  - 수신자가 **윈도우 크기**를 알려주면, 송신자는 그만큼만 전송  

- **혼잡 제어 (Congestion Control)**  
  - 네트워크 상황에 따라 송신 속도 조절  
  - 주요 기법:  
    - **Slow Start**: 처음엔 소량 전송, ACK 오면 기하급수적 증가  
    - **Congestion Avoidance**: 한계 근처에서 완만하게 증가  
    - **Fast Retransmit / Fast Recovery**: 손실 즉시 재전송, 윈도우 축소 후 점진 회복  
    - **AIMD (Additive Increase / Multiplicative Decrease)**: 선형 증가, 문제 발생 시 절반 감소  

---

## TCP/IP란?

- **TCP ≠ TCP/IP**  
  - **TCP**: 단일 전송계층 프로토콜  
  - **TCP/IP**: 인터넷 통신 전체를 위한 **프로토콜 모음**  

### TCP/IP 스택 구성
- **TCP, UDP, IP, ICMP, ARP** 등 포함  
- TCP와 IP가 핵심이어서 흔히 줄여서 **“TCP/IP”**라고 부른다.  

---

# 정리

- **UDP**: 빠르고 단순, 신뢰성 없음 → 게임, 스트리밍에 적합  
- **TCP**: 느리지만 신뢰성 보장 → 웹, 이메일에 적합  
- **TCP/IP**: 인터넷 프로토콜 전반을 묶어 부르는 이름  
