## 검증 헤더와 조건부 요청2

---

### 검증 헤더와 조건부 요청

- **검증 헤더**
  - 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
  - Last-Modified , ETag


- **조건부 요청 헤더**
  - 검증 헤더로 조건에 따른 분기
  - If-Modified-Since: Last-Modified 와 함께 사용
  - If-None-Match: ETag 와 함께 사용
  - 조건이 만족하면 200 OK
  - 조건이 만족하지 않으면 304 Not Modified

---

### 검증 헤더와 조건부 요청
#### 예시

- If-Modified-Since : 이후에 데이터가 수정되었으면?
  - **데이터 미변경 예시**
    - 캐시 : 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 10:00:00
    - **304 Not Modified**, 헤더 데이터만 전송( BODY 미포함 )
      - 너의 캐시로 리다이렉션하렴!!
    - 전송 용량 0.1M( 헤더 0.1M, 바디 1.0M )
    
  - **데이터 변경 예시**
    - 캐시 : 2020년 11월 10일 10:00:00 vs 서버 : 2020년 11월 10일 **11**:00:00
    - **200 OK**, 모든 데이터 전송( BODY 포함 )
    - 전송 용량 1.1M( 헤더 0.1M, 바디 1.0M )

---

### 검증 헤더와 조건부 요청
#### Last-Modified, If-Modified-Since 단점

- 1초 미만( 0.x 초 ) 단위로 캐시 조정이 불가능


- 날짜 기반의 로직 사용


- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 **데이터 결과가 똑같은 경우**


- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
  - 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우

---

### 검증 헤더와 조건부 요청
#### ETag, If-None-Match

- ETag( Entity Tag )


- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
  - 예) ETag: "v1.0" , ETag: "a2jiodwjekjl3"
  - 달고싶은대로 달 수 있음


- 데이터가 변경되면 이 이름을 바꾸어서 변경함( Hash 를 다시 생성 )
  - 파일의 content 가 똑같으면 같은 Hash 값이 나오고, 다르면 다른 Hash 값이 나온다


- 진짜 단순하게 ETag 만 보내서 같으면 유지, 다르면 다시 받기!

---

### 검증 헤더 추가
#### 첫 번째 요청

> 웹 브라우저
>
> 요청1
>
> ---
>
> GET /star.jpg

-->

> 서버
>
> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
>
> Content-Type: image/jpeg
>
> cache-control: **max-age=60**
>
> **ETag: "aaaaaaaaaa""**
>
> ( ETag )
>
> Content-Length: 34012
>
> ---
>
> **body**
>
> ````text
> lkj123kljoiasudlkjaweioluywlnfdo912u34ljko98udjkl
> ````

<-- star.jpg

( _**1.1M 전송**_ )

( _**ETag**_ )

( _**"aaaaaaaaaa"**_ )

> 브라우저 캐시
>
> ---
>
> **60초 유효**
>
> ( 응답 결과를 캐시에 저장 )
>
> **ETag**
> 
> **"aaaaaaaaaa"**

---

### 검증 헤더 추가
#### 두 번째 요청 - 캐시 시간 초과

> 웹 브라우저
>
> 요청1
>
> ---
>
> GET /star.jpg
> 
> **If-None-Match: "aaaaaaaaaa"**
> 
> ( 캐시가 가지고 있는, ETag )

> 브라우저 캐시
>
> ---
>
> **60초 초과**
>
> **ETag**
>
> **"aaaaaaaaaa"**

-->

> 서버
>
> **start-line**
>
> HTTP/1.1 **304 Not Modified**
>
> ---
>
> **header**
>
> Content-Type: image/jpeg
>
> cache-control: **max-age=60**
>
> **ETag: aaaaaaaaaa**
>
> Content-Length: 34012
>
> **( HTTP Body 가 없다 )**

<-- star.jpg

( _**1.1M 가정**_ )

( _**HTTP 헤더: 0.1M**_ )

( _**HTTP 바디: 1.0M**_ )

- 이렇게 전달받으면 캐시에서 사용하게 된다!

---

### 검증 헤더와 조건부 요청
#### ETag, If-None-Match 정리

- 진짜 단순하게 ETag 만 서버에 보내서 같으면 유지, 다르면 다시 받기!


- **캐시 제어 로직을 서버에서 완전히 관리**


- 클라이언트는 단순히 이 값을 서버에 제공( 클라이언트는 캐시 메커니즘을 모름 )
  - 진짜 클라이언트는 블랙박스가 된다

- 예)
  - 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도 ETag 를 동일하게 유지
  - 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신

