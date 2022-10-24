## 클라이언트에서 서버로 데이터 전송
### 데이터 전달 방식은 크게 2가지

- **쿼리 파라미터를 통한 데이터 전송**
  - GET
  - 주로 정렬 필터( 검색어 )
- **메시지 바디를 통한 데이터 전송**
  - POST , PUT , PATCH
  - 회원가입 , 상품 주문 , 리소스 등록 , 리소스 변경

---

### 4가지 상황

- **정적 데이터 조회**
  - 이미지, 정적 텍스트 문서
  

- **동적 데이터 조회**
  - 주로 검색, 게시판 목록에서 정렬 필터( 검색어 )


- **HTML Form 을 통한 데이터 전송**
  - 회원 가입, 상품 주문, 데이터 변경


- **HTTP API 를 통한 데이터 전송**
  - 회원 가입, 상품 주문 , 데이터 변경
  - 서버 to 서버, 앱 클라이언트 , 웹 클라이언트( Ajax )

----

### 정적 데이터 조회
#### 쿼리 파라미터 미사용

> 클라이언트
>
> ---
>
> GET/static/star.jpg HTTP/1.1
>
> Host: localhost:8080

_GET -->_

> **/static/star.jpg**
>
> ---
> 
> HTTP/1.1 200 OK
> 
> Content-type: image/jpeg
> 
> Content-Length: 34012
> 
> lkj123kljoiasudlkjaweioluywlnfdo912u34ljko98udjklaslkjdfl;qkawj9;o4ruawsldkal;skdjfa;ow9ejkl3123123

---

### 정적 데이터 조회
#### 정리

- 이미지 , 정적 텍스트 문서
- 조회는 GET 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

---

### 동적 데이터 조회
#### 쿼리 파라미터 사용

> 클라이언트
>
> ---
>
> GET/search?<span style="color: red">**q=hello&hi=ko**</span> HTTP/1.1
>
> Host: www.google.com

_GET -->_

> 서버
>
> ---
>
> 쿼리 파라미터를 기반으로 정렬 필터해서 결과를 동적으로 생성 

---

### 동적 데이터 조회
#### 정리

- 주로 검색, 게시판 목록에서 정렬 필터( 검색어 )
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
- 조회는 GET 사용
- GET 은 쿼리 파라미터 사용해서 데이터를 전달

---

### HTML Form 데이터 전송
#### POST 전송 - 저장

> 클라이언트
>
> ---
>
> ```html
>  <form action="/save" method="post">
>       <input type="text" name="username" />
>       <input type="text" name="age" />
>       <button type="submit">전송</button>
>  </form>
> ```

_POST -->_

> 웹 브라우저가 생성한 요청 HTTP 메시지
>
> ---
>
> POST /save HTTP/1.1
> 
> Host: localhost:8080
> 
> Content-Type: <span style="color: red">application/x-www-form-urlencoded</span>
> 
> <span style="color: red">username=kim&age=20</span>

- form 태그의 submit 버튼을 클릭하면, 자동으로 form 데이터를 읽어서
- HTTP 메시지를 생성해서 보낸다
  - query 파라미터와 유사한 형식으로 보낸다


---

### HTML Form 데이터 전송
#### GET 전송 - 저장

> 클라이언트
>
> ---
>
> ```html
>  <form action="/save" method="get">
>       <input type="text" name="username" />
>       <input type="text" name="age" />
>       <button type="submit">전송</button>
>  </form>
> ```

_GET -->_

> 웹 브라우저가 생성한 요청 HTTP 메시지
>
> ---
>
> GET /save<span style="color: red">?username=kim&age=20</span> HTTP/1.1
>
> Host: localhost:8080

- get 메서드로 form 태그의 요청을 바꿔버리면 HTTP method body 를 안쓰기 때문에,
  - query 파라미터에 넣어버린다
  - 당연한거지만 save 에서는 GET 메서드를 사용하면 안된다  

- 주의! GET 은 조회에만 사용!
- 리소스 변경이 발생하는 곳에 사용하면 안됨

---

### HTML Form 데이터 전송
#### multipart/form-data

> 클라이언트
>
> ---
>
> ```html
>  <form action="/save" method="post" enctype="multipart/form-data">
>       <input type="text" name="username" />
>       <input type="text" name="age" />
>       <input type="file" name="file1" />
>       <button type="submit">전송</button>
>  </form>
> ```

_POST -->_

> 웹 브라우저가 생성한 요청 HTTP 메시지
>
> ---
>
> POST /save HTTP/1.1
>
> Host: localhost:8080
>
> **Content-Type: multipart/form-data; boundary=----XXX**
>
> ------XXX
> 
> Content-Disposition: form-data; name="username"
> 
> kim
> 
> ------XXX
> 
> Content-Disposition: form-data; name="age"
> 
> 20
> 
> ------XXX
> 
> Content-Disposition: form-data; name="file1"; filename="intro.png"
> 
> Content-Type: image/png
> 
> 109238a9o0p3eqwokjasd09ou3oirjwoe9u34ouief...
> 
> ------XXX--

- 파일 전송시 multipart/form-data 로 데이터를 전송한다
  - multipart/form-data 로 파일을 보내면 boundary 로 경계를 알아서 브라우저에서 잘라준다
  - 멀티파트로 여러개 데이터를 보내준다( 주로 바이너리 데이터들을 보낼 때 사용한다 )

---

### HTML Form 데이터 전송
#### 정리

- HTML Form submit 시 POST 전송
  - 예) 회원 가입, 상품 주문, 데이터 변경


- Content-Type: application/x-www-form-urlencoded 사용
  - form 의 내용을 메시지 바디를 통해서 전송( key=value, 쿼리 파라미터 형식 )
  - 전송 데이터를 url encoding 처리
    - 예) abc 김 -> abc%EA%B9%80


- HTML Form 은 GET 전송도 가능
  

- Content-Type: multipart/form-data
  - 파일 업로드 같은 바이너리 데이터 전송시 사용
  - 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능( 그래서 이름이 multipart )


- 참고: HTML Form 전송은 **<span style="color: red">GET,POST 만 지원</span>**

---

### HTML API 데이터 전송

> 클라이언트
>
> ---
> 
> POST /members HTTP/1.1
> 
> Content-Type: application/json
>
> {
>   "username" : "young",
>   "age"      : 20
> }

_POST -->_

> /members

- 서버로 전송하게 해주는 라이브러리들이 이미 많이있어서 그것들을 사용하면 된다

---

### HTML API 데이터 전송
#### 정리

- 서버 to 서버
  - 백엔드 시스템 통신


- 앱 클라이언트
  - 아이폰, 안드로이드


- 웹 클라이언트
  - HTML 에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용 ( AJAX )
  - 예) React, VueJs 같은 웹 클라이언트와 API 통신


- POST, PUT, PATCH : 메시지 바디를 통해 데이터 전송


- GET : 조회, 쿼리 파라미터로 데이터 전달


- Content-Type: application/json 을 주로 사용( 사실상 표준 )
  - TEXT, XML, JSON 등등
  - 예전에는 XML 등등을 많이 사용했지만, 지금은 JSON 을 사용한다
