## 3xx - 리다이렉션

---

### 3xx ( Redirection )
#### 요청을 완료하기 위해 유저 에이전트의 추가 조치 필요

- 300 Multiple Choices
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 307 Temporary Redirect
- 308 Permanent Redirect

*유저 에이전트 : 클라이언트 프로그람( 주로 웹 브라우저 )

--

### 리다이렉션 이해

- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동( 리다이렉트 )

---

### 리다이렉션 이해
#### 자동 리다이렉트 흐름

> 요청
>
> ---
>
> GET /event HTTP/1.1
>
> Host: localhost:8080

> 응답
> 
> ---
> 
> HTTP/1.1 301 Moved Permanently
> 
> Location: /new-event

_자동 리다이렉트 -->_

> 요청
>
> ---
>
> GET /new-event HTTP/1.1
>
> Host: localhost:8080

> 응답
>
> ---
>
> HTTP/1.1 301 200 OK
>
> ...

---

### 리다이렉션 이해
#### 종류

- **영구 리다이렉션** - 특정 리소스의 URI 가 영구적으로 이동
  - 예) /members -> /users
  - 예) /event -> /new-event


- **일시 리다이렉션** - 일시적인 변경
  - 주문 완료 후 주문 내역 화면으로 이동
  - PRG: Post/Redirect/Get


- **특수 리다이렉션**
  - 결과 대신 캐시를 사용


---

### 영구 리다이렉션
#### 301, 308

- 리소스의 URI 가 영구적으로 이동
- 원래의 URL 를 사용 X, 검색 엔진 등에서도 변경 인지
- **301 Moved Permanently**
  - **리다이렉트시 요청 메서드가 GET 으로 변하고, 본문이 제거될 수 있음( MAY )**
- **308 Permanent Redirect**
  - 301 과 기능은 같음
  - **리다이렉트시 요청 메서드와 분문 유지( 처음 POST 를 보내면 리다이렉트도 POST 유지)**
- 둘다 경로가 완전히 바뀌었다는 것을 알려준다

---

### 영구 리다이렉션 - 301

> 요청
>
> ---
>
> **POST** /event HTTP/1.1
> ( POST 사용 )
> 
> Host: localhost:8080
> 
> **name=hello&age=20**
> ( 메시지 존재 )

> 응답
>
> ---
>
> HTTP/1.1 301 Moved Permanently
>
> **Location: /new-event**

_자동 리다이렉트 -->_

> 요청
>
> ---
>
> **GET** /new-event HTTP/1.1
> ( **GET 으로 변경** )
>
> Host: localhost:8080
>
> ( **메시지 제거** )

> 응답
>
> ---
>
> HTTP/1.1 200 OK
>
> ...

---

### 영구 리다이렉션 - 308

> 요청
>
> ---
>
> **POST** /event HTTP/1.1
> ( POST 사용 )
>
> Host: localhost:8080
>
> **name=hello&age=20**
> ( 메시지 존재 )

> 응답
>
> ---
>
> HTTP/1.1 **308 Permanent Redirect**
>
> Location: /new-event

_자동 리다이렉트 -->_

> 요청
>
> ---
>
> **POST** /new-event HTTP/1.1
> ( **POST 유지** )
>
> Host: localhost:8080
> 
> **name=hello&age=20**
> ( **메시지 유지** )

> 응답
>
> ---
>
> HTTP/1.1 200 OK
>
> ...

- 그런데 실무적으로는 이렇게 잘 사용하지 않는다
- event -> new-event 로 바뀌면 보통 내부적으로 전달해야하는 data 가 거의 전부 바뀌어 버린다
- ( 어짜피 다시 데이터를 보내야됨 )

---

