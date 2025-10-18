# HTTP Header

## Host

- 요청하려는 서버의 도메인 이름과 포트 번호를 나타냄
- 포트가 주어지지 않으면 요청된 서버의 기본 포트를 의미함
- HOST 헤더의 필드는 HTTP/1.1 요청 메시지 내에 포함되어 전송되어야 함
- 역할 : 하나의 IP 주소로 여러 개의 웹사이트를 운영하는 서버에서, 클라이언트가 어떤 사이트에 접속하고 싶은지 알려줌
- 예시 : `Host: developer.mozilla.org`

## Accept

- 클라이언트가 이해할 수 있는 콘텐츠 유형을 알려줌
- 서버는 제안 중 하나를 선택하고, `Content-Type` 헤더로 클라이언트에게 선택된 타입을 알려줌
- 역할 : HTML, XHTML, XML 문서를 받을 수 있음을 서버에 알려줌
- 예시 : `Accept: text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8`

## Content-Type

- 응답 본문의 미디어 타입을 알려줌
- 예시 : `Content-Type: text/html; charset=utf-8`

## Accept-Language

- 클라이언트가 선호하는 자연어를 알려줌
- 서버는 제안 중 하나를 선택하고, `Content-Language` 헤더로 클라이언트에게 선택된 내용을 알려줌
- 역할 : 다국어 서비스를 제공하는 웹사이트에서 클라이언트에게 맞는 연어(프랑스어, 영어, 한국어)로 페이지를 보여주도록 요청
- 예시 : `Accept-Language: fr-CH, fr;q=0.9, en;q=0.8, ko;q=0.7, *;q=0.5`

## Content-Language

- 응답 본문의 사용된 언어를 알려줌
- 예시 : `Content-Language: de-DE`

## Accept-Encoding

- 클라이언트가 이해할 수 있는 압축 방식을 알려줌
- 서버는 제안 중 하나를 선택하고, `Content-Encoding` 헤더로 클라이언트에게 선택된 내용을 알려줌
- 역할 : 서버에게 데이터를 압축해서 보내달라고 요청
- 예시 : `Accept-Encoding: deflate, gzip;q=1.0, *;q=0.5`

## Content-Encoding

- 응답 본문이 어떻게 압축되었는지 알려줌
- 예시 : `Content-Encoding: gzip`

## User-Agent

- 요청을 보낸 클라이언트의 정보를 담고 있음
- 역할 : 서버는 클라이언트의 정보를 보고 사용자에게 보여줄 페이지를 결정할 수 있음
- 사용자 예시
  - Firefox 사용자 : `Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion`
  - Chrome 사용자 : `Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36`
  - Safari 사용자 : `Mozilla/5.0 (iPhone; CPU iPhone OS 13_5_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.1.1 Mobile/15E148 Safari/604.1`
  - 크롤러 : `Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)`

## Authorization

- 사용자의 인증 정보를 담고 있음
- 역할 : 서버는 로그인이 허가된 사용자임을 판단할 수 있음
- 예시 : `Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l`

## Cookie

- 서버가 이전에 클라이언트에 저장해 둔 작은 데이터 조각을 다시 서버로 보냄
- 역할 : 로그인 상태 유지, 장바구니 정보 저장 등 사용자의 상태를 기억하는 데 사용됨
- 예시 : `Cookie: lang=ko; theme=dark;`

## Origin

- 요청이 시작된 출처를 나타냄
- 주로 CORS 요청에 사용됨
- 역할 : 다른 도메인에서 온 요청의 경우 서버가 허용된 사이트인지 판단할 근거를 제공함
- 예시 : `Origin: https://developer.mozilla.org`

## Referer

- 현재 요청을 보낸 페이지의 이전 페이지 주소를 담음
- 역할 : 사용자가 어떤 경로를 통해 현재 페이지로 유입되었는지 분석하는 데 사용
- 예시 : `Referer: https://developer.mozilla.org/ko/docs/Web/JavaScript`

## Content-Length

- 응답 본문의 크기를 바이트 단위로 알려줌
- 예시 : `Content-Length: 1523`

## Cache-Control

- 캐시의 동작 방식을 지정함
- 역할 : 캐시의 유효 기간을 설정하거나, 캐시를 사용하지 못하게 하는 등 다양한 정책을 설정할 수 있음
- 예시 : `Cache-Control: no-cache, no-store, must-revalidate`

## Expires

- 캐시의 만료 날짜를 지정함
- 예시 : `Expires: Sun, 26 Oct 2025 00:00:00 GMT`

## Location

- 페이지를 다른 주소로 리다이렉션 시킬 때 사용
- 예시 : `Location: /index.html`

## Set-Cookie

- 클라이언트에 쿠키를 저장하도록 지시함
- 예시 : `Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT`

## Strict-Transport-Security

- 앞으로 이 사이트에 접속할 때는 무조건 HTTPS만 사용하도록 브라우저에 강제함
- 예시 : `Strict-Transport-Security: max-age=31536000; includeSubDomains`

## Content-Security-Policy

- 신뢰할 수 있는 외부 스크립트나 리소스만 로드하도록 허용하여 XSS를 방어함
- 예시 : `Content-Security-Policy: default-src 'self';`

## X-Frame-Options

- 다른 사이트에서 `<iframe>` 등을 통해 현재 페이지를 삽입하는 것을 방지하여 클랙재킹을 막음
- 예시 : `X-Frame-Options: DENY`

## Server

- 응답을 생성한 웹 서버 소프트웨어의 정보를 알려줌
- 예시 : `Server: Apache/2.4.1 (Unix)`

## Date

- 서버가 응답을 생성한 시각을 나타냄
- 예시 : `Date: Wed, 21 Oct 2015 07:28:00 GMT`

## Connection

- 현재의 요청과 응답이 완료된 후 네트워크 연결을 계속 유지할 지 아니면 닫을 지를 결정함
- 예시 : `Connection: keep-alive`, `Connection: close`

## Keep-Alive

- `Connection: keep-alive`가 사용될 때, 연결을 얼마나 오래 유지할지에 대한 세부 설정을 전달함
- 예시 : `Keep-Alive: timeout=5, max=100`

## If-None-Match

- 클라이언트가 가지고 있는 리소스의 `ETag` 값을 서버로 보냄
- 서버는 자신이 가진 리소스의 `ETag` 값과 비교하여 값이 동일하면 본문 없는 `304 Not Modified` 응답을 보냄
- 예시 : `If-None-Match: "abcdefg12345"`
- 서버 응답
  - 변경 없음 : `HTTP/1.1 304 Not Modified`
  - 변경됨 : `HTTP/1.1 200 OK`와 함께 새로운 데이터 전송

## If-Modified-Since

- 클라이언트가 가지고 있는 리소스의 `Last-Modified` 값을 서버로 보냄
- 서버는 이 날짜 이후에 리소스가 수정되었는지 확인하고 수정되지 않았으면 `304 Not Modified` 응답을 보냄
- 예시 : `If-Modified-Since: Tue, 15 Nov 2022 08:12:31 GMT`

## ETag

- 특정 버전의 리소스를 식별하는 고유한 문자열 검사기를 제공함
- 파일의 해시값 등으로 생성되면, 내용이 조금이라도 바뀌면 ETag 값도 변경됨
- 예시 : `ETag: "abcdefg12345"`

## Last-Modified

- 리소스가 서버에서 마지막으로 수정된 날짜와 시간을 알려줌
- 예시 : `Last-Modified: Tue, 15 Nov 2022 08:12:31 GMT`

## Forwarded

- 프록시를 거치면서 손실될 수 있는 클라이언트의 원래 IP 주소, 호스트, 프로토콜 등의 정보를 담는 헤더
- 예시 : `Forwarded: for=192.0.2.43; proto=https; host=example.com`

## X-Forwarded-For

- 요청이 여러 프록시를 거칠 때, 각 프록시의 IP를 포함하여 최초 클라이언트의 IP 주소를 식별하는 데 사용됨
- 예시 : `X-Forwarded-For: 203.0.113.195, 70.41.3.18, 150.172.238.178`

## Via

- 요청과 응답이 어떤 프록시들을 거쳐 갔는지 그 경로를 기록함
- 주로 요청 흐름을 디버깅하거나 프록시 루프를 방지하는 데 사용됨
- 예시 : `Via: 1.0 fred, 1.1 p.example.net`

## Access-Control-Allow-Origin

- 해당 리소스에 접근할 수 있는 외부 도메인을 지정함
- CORS 정책의 핵심 헤더
- 역할 : 모든 사이트 접근 허용
- 예시 : `Access-Control-Allow-Origin: *`

## Permissions-Policy

- 웹사이트가 특정 브라우저 기능을 사용할 수 있는지, 또는 사용하지 못하게 할지를 제어함
- 역할 : 카메라는 허용, 마이크 및 위치 정보 기능 금지
- 예시 : `Permissions-Policy: camera=*, microphone=(), geolocation=()`

## 출처

- https://developer.mozilla.org/ko/docs/Web/HTTP/Reference/Headers
