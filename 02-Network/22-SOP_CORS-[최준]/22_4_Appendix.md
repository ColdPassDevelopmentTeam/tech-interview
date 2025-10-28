# Appendix

## 퀴즈

- 1번 문제
    - https://www.example.com 과 **같은 origin**은?
    1. [http://www.example.com](http://www.example.com/)
    2. [https://www.example.com:80](https://www.example.com:80/)
    3. [https://www.example.com:443](https://www.example.com/)
    4. [https://hello.example.com](https://hello.example.com/)
- 1번 정답
    
    3. [https://www.example.com:443](https://www.example.com/)
    - port 생략 시 **기본 포트 적용**
    - 1번은 프로토콜이 다름
    - 2번은 포트 번호가 다름
    - 4번은 도메인이 다름

<br>

- 2번 문제
    - SOP가 등장한 이유는 **프론트엔드와 백엔드가 나눠지지 않아** 다른 origin으로 요청 보내는 것을 **악의적인 행위로 간주하는게 자연**스럽기 때문
- 2번 정답
    - O
    - SOP가 등장한 이유는 **프론트엔드와 백엔드가 나눠지지 않아** 모든 처리가 **같은 도메인 내**에서 일어남

<br>

- 3번 문제
    - CORS를 만족하려면 **프론트엔드는 origin 헤더**를 추가
    - **백엔드는 access-control-allow-origin 헤더** 추가
- 3번 정답
    - O
    - origin 헤더에 **담긴 origin이** access-control-allow-origin 헤더에 **포함되어 있어야 CORS 통과**

<br>

## 참고 자료

- [origin, SOP, SOP 생긴 이유 & CORS 등장 배경, CORS, CORS 요청](https://github.com/devSquad-study/2023-CS-Study/blob/main/Network/network_sop_and_cors.md)
- [CORS 요청](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#cors%EB%9E%80)
- [SOP, SOP 생긴 이유 & CORS 등장 배경, CORS, CORS 요청](https://github.com/NKLCWDT/cs/blob/main/Network/CORS.md)
- [SOP, CORS](https://velog.io/@jesop/SOP%EC%99%80-CORS)
- [origin, SOP, SOP 생긴 이유 & CORS 등장 배경, CORS 요청](https://hudi.blog/sop-and-cors/)
- [origin, SOP, CORS 요청](https://jaehyeon48.github.io/web/sop-and-cors/)
- [CORS에 대한 모든 것(Cross-Origin Resource Sharing) - medium](https://swfungineer.medium.com/cors%EC%97%90-%EB%8C%80%ED%95%9C-%EB%AA%A8%EB%93%A0-%EA%B2%83-cross-origin-resource-sharing-fc7f3271490#5114)
- https://blog.zairo.kr/entry/%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%AC%EC%9A%B4-%EC%9B%B9-%EB%B3%B4%EC%95%88-%EB%AA%A8%EB%8D%B8-%EC%9D%B4%EC%95%BC%EA%B8%B0-1-SOP-CORS