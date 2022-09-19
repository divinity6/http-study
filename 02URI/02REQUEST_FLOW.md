## 웹 브라우저 요청 흐름

- https://www.google.com:443/search?q=hello&hl=ko

- 위의 search 로 https 로 요청을 부르면, 브라우저가 먼저 

  - https://www.google.com **( DNS 서버 조회 )** :443 **( HTTPS PORT 생략 )** /search?q=hello&hl=ko
  - 그 후, HTTP 요청 메시지 생성

> ### HTTP 요청 메시지
>
>> GET/search?q=hello&hl=ko HTTP/1.1
>> HOST: www.google.com
>

1. 웹 브라우저가 HTTP 메시지 생성
2. SOCKET 라이브러리를 통해 연결( TCP/IP 연결 - IP , PORT )
3. TCP/IP 패킷 생성, HTTP 메시지 포함

---

이렇게 TCP/IP 패킷에 감싸서 서버로 보내면, 

서버에 도착한 정보에서 TCP/IP 패킷을 까서 버리고, HTTP 메시지를 끄집어내서 해석하고 데이터를 찾는다.

( 예) query 가 hello 고, search 로 왔으니 뭔가 검색, hl 은 ko 이니깐 ,한국어구나 )

그 후 , 구글 서버에서 HTTP 응답 메시지를 맨들어 보낸다

> ### HTTP 응답 메시지
> 
>> HTTP/1.1 200 OK
>>
>> Content-Type: text/html;charset=UTF-8
>> 
>> Content-Length: 3423
>>
>> <(html)>
>> <(body)></(body)>
>> </(html)>

---

브라우저에서 이것을 받으면, 내부를 까서 HTML 렌더링을 하게된다