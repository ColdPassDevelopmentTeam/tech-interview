# 🐘 tech-interview
안녕하세요! CS 기본부터 심화까지 함께 탐험할 스터디 레포지토리입니다. 꾸준히 지식을 쌓고 공유하며 함께 성장하는 것을 목표로 합니다.

### 🎯스터디 목표
* 컴퓨터 과학의 핵심 분야(운영체제, 네트워크, 데이터베이스 등)에 대한 깊이 있는 이해를 목표로 합니다.
* 기술의 동작 원리를 파악하고, 이를 바탕으로 문제 해결 능력을 향상시킵니다.
* 기술 면접에 자신감 있게 임할 수 있도록 CS 전공 지식을 체계적으로 정리합니다.
* 함께 지식을 공유하고 토론하며 동반 성장하는 개발 문화를 만들어갑니다.

---

## 🗓️ 스터디 일정 및 진행 방식
### **발표 일정**: 매주 **수요일**, **목요일**
### 진행 방식:
1. **주제 선정** : 스터디원은 매 주 네트워크 관련 개별 주제를 선정
2. **학습 및 자료 정리** : 각자 맡은 주제를 학습, 학습 내용을 Markdown 형식으로 정리
3. **발표 자료 제작** : 피드백을 반영하여 발표 자료 제작( Markdown, PDF, PPT 등 )
4. **발표 및 Q&A**
5. **최종 자료 업로드** : 발표가 끝난 후, 최종 발표자료를 PR에 추가
6. **PR** : 정리한 Markdown 문서를 스터디 Git Repository에 PR
7. **리뷰** : 다른 스터디원이 제출한 PR 확인 후 피드백
8. **PR merge**
  
### 폴더 구조 예시
```
📁 tech-interview/
│
├── 📁 01-Database/
│   └── ...
│
├── 📁 02-Network/
│   ├── 📁 01-OSI-7Layer/
│   │   ├── 📁src
│   │   │   ├── 📄 image1.png
│   │   │   └── 📄 image2.png
│   │   ├── 📁presentation
│   │   │   └── 📄 발표자료_홍길동.pdf
│   │   ├── 📄 README.md
│   │   ├── 📄 실습코드.sql
│   │   └── ...
│   │
│   ├── 📁 02_TCP/IP-4Layer/
│   │   ├── 📁src
│   │   |   └── ...
│   │   ├── 📁presentation
│   │   |   └── ...
│   |   ├── 📄 README.md
│   │   ├── 📄 실습코드.js
│   │   └── ...
│   └──📄README.md // 목차 정리용
│
├── 📁 03-/
│   └── ...
│
└── 📄 README.md
```

## 📚 이번 세션 주제: 네트워크 (Network)
<details>
  <summary><strong>주요 발표 내용:</strong></summary>
  
    - [x] OSI 7계층 
    - [x] TCP/IP 4계층 
    - [ ] TCP vs UDP
      - 동작 방식, 특징, 차이점
      - 헤더  
    - [ ] 3 way & 4 way handshake
    - [ ] TCP 흐름 제어 & 혼잡 제어
    - [ ] 네트워크 기기
      - 라우터, 스위치, 브리지, NIC, 리피터, 허브, VLAN, VPN 등
    - [ ] Frame, Packet, Segment, Datagram
    - [ ] HTTP vs HTTPS
      - 개념, 차이점, 동작 과정
        - HTTP 구성요소
          - 요청, 응답 헤더
          - 상태 코드
      - 특징
        - HTTP 프로토콜 특징
    - [ ] HTTP 버전별 차이
    - [ ] HTTP method
      - GET vs POST
    - [ ] HTTPS
      - SSL/TLS handshake
    - [ ] RESTful & REST
      - SOAP
    - [ ] 웹 동작 방식
    - [ ] 주소
      - IP 주소 (IPv4, IPv6)
      - 공인 IP vs 사설 IP
      - MAC 주소 & ARP
      - 서브네팅, 서브넷 마스크
    - [ ] DNS
    - [ ] 로드밸런싱
      - 프록시 서버
      - L4, L7 로드밸런서 (스위치)
    - [ ] 인증 관련
      - 쿠키 vs 세션
      - JWT
      - 세션 기반 인증 vs 토큰 기반 인증
      - OAuth
      - 대칭키 & 공개키 (비대칭키) 암호화
    - [ ] 네트워크 공격
      - SYN Flooding
      - XSS
      - CSRF
      - 방화벽
    - [ ] Web Server vs WAS
    - [ ] CDN
    - [ ] port & 소켓
    - [ ] 웹 소켓
    - [ ] Connection Timeout, Read Timeout (각종 Timeout)
    - [ ] 이더넷
    - [ ] 정책
      - CORS
      - SOP
    - [ ] 프로토콜
      - [ ] DHCP
      - [ ] ICMP
    - [ ] ARQ
    - [ ] ATM
    - [ ] IOCP
    - [ ] 통신
      - 패킷 교환 vs 회선 교환
      - 유니캐스트/멀티캐스트/브로드캐스트
    - [ ] 네트워크 분류
      - 네트워크 토폴로지
      - LAN, MAN, WAN
    - [ ] vs 3형제
      - Blocking vs Non-blocking
      - synchronous vs asynchronous
      - stateful vs stateless (HTTP 특징에서도 가능)
    - [ ] URL, URI, URN
    - [ ] 주소 변환 기술
      - NAT, 포트포워딩
  
</details>

### 🧑‍💻 참여자
|[![](https://github.com/co2plant.png?width=40px)](https://github.com/co2plant) | [![](https://github.com/CJ-1998.png?width=40px)](https://github.com/CJ-1998) | [![](https://github.com/commentLee.png?width=40px)](https://github.com/commentLee) | [![](https://github.com/seolsa1014.png?width=40px)](https://github.com/seolsa1014) | [![](https://github.com/skywalkbee300.png?width=40px)](https://github.com/skywalkbee300) |
|:---:|:---:|:---:|:---:|:---:|
| co2plant | CJ-1998 | commentLee | seolsa1014  | skywalkbee300 |
