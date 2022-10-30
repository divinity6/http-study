## 표현

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

- Content-Type: 표현 데이터의 형식
- Content-Encoding: 표현 데이터의 압축 방식
- Content-Language: 표현 데이터의 자연 언어( 한국어, 영어등 )
- Content-Length: 표현 데이터의 길이( 명확하게 쪼개면 페이로드 헤더로 구분 가능 )


- 표현 헤더는 전송, 응답 둘다 사용

---

### Content-Type
#### 표현 데이터의 형식 설명

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

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
>
> Content-Type: application/json
>
> Content-Length: 16
>
> ---
>
> **body**
>
> ````json
> { "data" : "hello" }
> ````

- 미디어 타입, 문자 인코딩
- 예)
  - text/html; charset=utf-8
  - application/json ( 기본이 utf-8 )
  - image/png

---

### Content-Encoding
#### 표현 데이터 인코딩

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
> Content-Encoding: gzip
> 
> Content-Length: 521
>
> ---
>
> **body**
>
> ````text
> lkj123kljoiasudlkjaweioluywlnfdo912u34ljko98udjkl
> ````

- 표현 데이터를 압축하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예)
  - gzip
  - deflate
  - identity ( 압축 안하는 것 )

---

### Content-Language
#### 표현 데이터의 자연 언어

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
> Content-Language: ko
>
> Content-Length: 521
>
> ---
>
> **body**
>
> ````html
> <html>
>   안녕하세요
> </html>
> ````

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
> Content-Language: en
>
> Content-Length: 521
>
> ---
>
> **body**
>
> ````html
> <html>
>   hello
> </html>
> ````


- 표현 데이터의 자연 언어를 표현
- 예)
    - ko
    - en
    - en-US

---

### Content-Length
#### 표현 데이터의 길이

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
> Content-Length: 5
>
> ---
>
> **body**
>
> ````text
> hello
> ````


- 바이트 단위
- Transfer-Encoding( 전송 코딩 )을 사용하면 Content-Length 를 사용하면 안됨