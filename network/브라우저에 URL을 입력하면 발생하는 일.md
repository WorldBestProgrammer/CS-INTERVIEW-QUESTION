# 브라우저에 URL을 입력하면 발생하는 일

---

1. 브라우저 주소창에 naver.com을 입력한다.
2. 브라우저가 naver.com의 유효성 검사를 한다. 
3. 적절한 url 구조라면 IP 주소를 찾기 위해 캐시에서 DNS 기록을 확인한다. 그렇지 않다면 검색한 결과를 보여준다.
4. 만약 요청한 URL(naver.com)이 캐시에 없다면, ISP의 DNS 서버가 DNS 쿼리로 maps.google.com을 호스팅하는 서버의 IP 주소를 찾는다.
5. 브라우저가 해당 서버와 TCP 연결을 시작한다.
6. 브라우저가 웹서버에 HTTP 요청을 보낸다.
7. 서버가 요청을 처리하고 응답을 보낸다.
8. 서버가 HTTP 응답을 보낸다.
9. 브라우저가 HTML 컨텐츠를 보여준다.

---
## Reference
---
https://velog.io/@khy226/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90-url%EC%9D%84-%EC%9E%85%EB%A0%A5%ED%95%98%EB%A9%B4-%EC%96%B4%EB%96%A4%EC%9D%BC%EC%9D%B4-%EB%B2%8C%EC%96%B4%EC%A7%88%EA%B9%8C
