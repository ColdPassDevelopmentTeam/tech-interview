# Appendix

## 퀴즈

- 1번 문제 :
    - TLS SSL에서 개선하며 만들어진 것으로 SSL과 함께 현재까지 유용하게 사용되고 있다.
- 1번 정답 :
    - X
    - SSL은 보안 취약점이 발견되어 현재 사용 금지되었다.

<br>

- 2번 문제 :
    - SSL & TLS의 핵심 기능은 암호화, 무결성, 인증이다.
- 2번 정답 :
    - O
    - 대칭키, 비대칭키로 데이터를 암호화 해 기밀성을 확보함.
    - MAC을 사용해 데이터 변조되지 않음을 보장해 무결성, 안전성 확보함
    - 인증서를 통해 피싱 사이트가 아님을 인증해 신뢰성 보장함

<br>

- 3번 문제 :
    - TLS handshake 중 비대칭키 연산은 overhead에 큰 영향은 없다.
- 3번 정답 :
    - X
    - 비대칭키 연산은 CPU 부담이 큼.
    - 따라서 성능이 우수한 비대칭키 암호화를 사용해 handshake 성능 개선함.

<br>

## 추후 알아볼 것

### 암호화

- 대칭키 암호화 (예: AES)
- 비대칭키 암호화 (예: RSA, ECC)
- 해시 함수와 메시지 다이제스트 (SHA 등)
- 디지털 서명

<br>

### 디지털 인증서 & 인증 기관 (CA)

- 인증서 구조 (X.509)
- 인증 기관(CA)과 신뢰 체인
- 루트 인증서와 중간 인증서
- 인증서 검증 과정 (만료, 폐기, CRL/OCSP)
- 디지털 인증서란
- CA(Certificate Authority)의 역할
- 인증서 체인(Certificate Chain)
- 자가 서명 인증서

<br>

## 참고 자료

- https://goldenrabbit.co.kr/2024/07/29/http%EB%9E%80-https-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-%EA%B3%B5%EA%B0%9C%ED%82%A4-%EC%95%94%ED%98%B8%ED%99%94/
- https://junhyunny.github.io/information/https/
- https://net-gate.tistory.com/35
- http://www.ktword.co.kr/test/view/view.php?no=2552
- https://blog.cloudflare.com/ko-kr/even-faster-connection-establishment-with-quic-0-rtt-resumption/