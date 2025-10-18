# Appendix

## 퀴즈

- 1번 문제 :
    - TLS 1.3 Handshake는 **1 RTT만 필요**하여 TLS 1.2 Handshake보다 **성능이 우수**하다.
- 1번 정답 :
    - O
    - 암호화 방식을 추측해 필요한 **공개키를 미리 보냄**
    - 암호화 방식 협상과 키 교환을 **따로 진행하지 않아 2 RTT → 1 RTT**

<br>

- 2번 문제 :
    - TLS 1.3 Handshake는 TLS 1.2 Handshake와 **같은 시점에 메시지를 암호화** 한다.
- 2번 정답 :
    - X
    - 보안 강화 위해 **암호화 시점 크게 앞당겨짐**
    - **ServerHello 이후** 메시지는 모두 **세션 키로 암호화**

<br>

- 3번 문제 :
    - 인증서의 서명은 **서버의 공개키를 해싱**한 값을 **CA의 비밀키로 암호화** 하는 것이다.
- 3번 정답 :
    - O
    - **브라우저 인증서 검증** : **CA의 공개키로 복호화** 해 **서버 공개키 해시 값과 비교**
    - **인증서 체인 검증** : **상위 CA 공개키로 서명 복호화** 해 **하위 CA 서명과 비교**

<br>

## 참고 자료

### TLS 1.3 Handshake 관련

- https://blog.naver.com/ucert/221234082080
- https://blog.pollra.com/handshake-tls-1-3/
- https://tech.buzzvil.com/blog/atech-blog-hello-tls-1-3/
- https://com-on-bappool.tistory.com/126
- https://babbab2.tistory.com/7

<br>

### 0-RTT 관련

- https://withbundo.blogspot.com/2018/01/https-ssl-session-id-session-ticket.html
- https://pat.im/1330
- https://luavis.me/server/tls-1.3

<br>

### 인증서 관련

- https://babbab2.tistory.com/5
- https://aws.amazon.com/ko/what-is/ssl-certificate/
- https://growth-coder.tistory.com/260
- https://heodolf.tistory.com/94
- https://jennana.tistory.com/53