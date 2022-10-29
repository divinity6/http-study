## HTTP 헤더1
### HTTP 헤더 개요

---

### HTTP 헤더

- header-field = field-name ":" <span style="color:red">_OWS_</span> field-value<span style="color:red">_OWS_</span>
- ( OWS : 띄어쓰기 허용 )


- field-name 은 대소문자 구분 없음


> **start-line**
> 
> **GET** /search?q=hello&hl=ko HTTP/1.1
> 
> ---
> 
> **header**
> 
> Host: www.google.com


> **start-line**
> 
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
> 
> Content-Type: text/html;charset=UTF-8
> 
> Content-Length: 3423
> 
> ---
> 
> **body**
> 
> ````html
> <html>
>   <body>...</body>
> </html>
> ````

---

### HTTP 헤더
#### 용도

- HTTP 전송에 필요한 모든 부가정보


- 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보...


- 표준 헤더가 너무 많음
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields


- 필요시 임의의 헤더 추가 가능
  - helloworld: hihi

---

### HTTP 헤더
#### 분류 - RFC2616( 과거 )

> POST / HTTP/1.1
> 
> ---
> 
> <span style="color:red">**Request headers**</span>
> 
> Host: localhost:8000
> 
> User-Agent: Mozilla/5.0 ( Macintosh;... )... Firefox/51.0
> 
> Accept: text/html, application/xhtml+xml,..., */*;q=0.8
> 
> Accept-Language: en-US,en;q=0.5
> 
> Accept-Encoding: gzip, deflate
> 
> ---
> 
> <span style="color:green">**General headers**</span>
> 
> Connection: keep-alive
> 
> Upgrade-Insecure-Requests: 1
> 
> ---
> 
> <span style="color:blue">**Entity headers**</span>
> 
> Content-Type: multipart/form-data; boundary=12656974
> 
> Content-Length: 345

- 헤더 분류
  - <span style="color:green">**General 헤더**</span>: 메시지 전체에 적용되는 정보, 예) Connection: close
  - <span style="color:red">**Request 헤더**</span>: 요청 정보, 예) User-Agent: Mozilla/5.0 ( Macintosh; .. )
  - <span style="color:yellow">**Response 헤더**</span>: 응답 정보, 예) Server: Apache
  - <span style="color:blue">**Entity 헤더**</span>: 엔티티 바디 정보, 예) Content-Type: text/html, Content-Length: 3423

---

### HTTP BODY
#### message body - RFC2616( 과거 )

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> <span style="color:blue">**Entity 헤더**</span>
>
> Content-Type: text/html;charset=UTF-8
>
> Content-Length: 3423
>
> ---
> 
> 메시지 본문
>
> <span style="color:blue">**Entity 본문**</span>
>
> ````html
> <html>
>   <body>...</body>
> </html>
> ````

- 메시지 본문( message body )은 엔티티 본문( entity body )을 전달하는데 사용
- 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
- <span style="color:blue">**엔티티 헤더**</span> 는 <span style="color:blue">**엔티티 본문**</span>의 데이터를 해석할 수 있는 정보 제공
  - 데이터 유형( html, json ), 데이터 길이, 압축 정보 등등

---

그런데

### HTTP 표준
### 1999 년 RFC2616( <span style="color:red">x</span> ) - 폐기됨
### 2014 년 RFC7230~7235 등장

- entity header, body 라는  용어가 사라졌다
---

### RFC723x 변화

- 엔티티( Entity ) -> 표현( Representation )


- Representation = representation Metadata + Representation Data


- 표현 = 표현 메타데이터 + 표현 데이터

---

### HTTP BODY
#### message body - RFC7230( 최신 )

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> <span style="color:pink">**표현 헤더**</span>
>
> Content-Type: text/html;charset=UTF-8
>
> Content-Length: 3423
>
> ---
>
> 메시지 본문
>
> <span style="color:pink">**표현 데이터**</span>
>
> ````html
> <html>
>   <body>...</body>
> </html>
> ````

- 메시지 본문( message body )을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드( payload )
- **표현**은 요청이나 응답에서 전달할 실제 데이터
- **<span style="color:pink">표현 헤더</span>는 <span style="color:pink">표현 데이터</span>**를 해석할 수 있는 정보 제공
  - 데이터 유형( html, json ), 데이터 길이,압축 정보 등등
- 참고: 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 하지만 여기서는 생략

---

- 왜 표현이라고 애기를할까?
  - 예) 메시지 본문 데이터를 회원과 관련된 회원조회내역을 html 로 제공한다
    - 이것은 회원이라는 정보를 html 로 표현한 것이다
    - json 으로 조회를한다? 회원이라는 리소스를 실제 데이터가 http 로 전송이 될때는
    - json 으로 표현할 수 도있고, html 로 표현할 수 있다
  - 따라서, 실제 전달하는 것을 <span style="color:pink">표현</span>이라고 명확하게 정의를 했다

- <span style="color:pink">Representation</span> 의 R 이 Rest 의 R 이다