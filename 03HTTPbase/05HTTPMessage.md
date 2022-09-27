## HTTP 메시지
### 모든 것이 HTTP - 한번 더!
#### HTTP 메시지에 모든 것을 전송

- HTML , TEXT
- IMAGE, 음성, 영상, 파일
- JSON , XML
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
- **지금은 HTTP 시대**

---

#### 예) HTTP 요청 메시지
요청 메시지도 body 본문을 가질 수 있음

> **start-line** : GET /search?q=hello&hl=ko HTTP/1.1
> 
> ---
> 
> **header** : Host: www.google.com
> 
> ---
> **empty-line** :
> 
> ---
> 
> **body** :


#### 예) HTTP 응답 메시지

> **start-line** : HTTP/1.1 200 OK
> 
> ---
> 
> **header** : Content-Type : text/html;charset=UTF-8
>
> 
> Content-Length: 3423
> 
> ---
> 
> **empty-line** :
> 
> ---
> 
> **body** :
> 
> ```html
>  <html>
>       <body>...</body>
>  </html>
> ```

#### HTTP 메시지 구조

> **start-line** 시작 라인
> 
> ---
> 
> **header** 헤더
> 
> ---
> 
> **empty-line** 공백라인 ( CRLF ) : 반드시 필요
> 
> ---
> 
> **message body**

- HTTP 는 요청 메시지와 응답메시지 구조가 다르다.

---

### 시작 라인
#### 요청 메시지

- start-line = **request-line** / status-line
  - 요청라인과, 상태 라인으로 나뉜다
- **request-line** = method _SP( 공백 )_ request-target _SP_ HTTP-version _CRLF( 엔터 )_
  - method : HTTP 메서드( GET, POST 등... )
  - request-target : 패스( 요청하는 대상 )
  - version : HTTP 버전


- HTTP 메서드( GET : 조회 )
- 요청 대상 ( /search?q=hello&hl=ko )
- HTTP Version

---

#### 요청 메시지 - HTTP 메서드

- 종류 : GET , POST , PUT , DELETE...
- 서버가 수행해야 할 동작 지정
  - GET : 리소스 조회 및 요청
  - POST : 요청 내역 처리 ( 이 리소스를 줄테니깐 처리해줘! )

---

#### 요청 메시지 - 요청 대상

- absolute-path[?query] ( 절대경로[?쿼리] )
- 절대경로="/" 로 시작하는 경로
- 참고 : *, http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다

---

#### 요청 메시지 - HTTP 버전

- HTTP Version

---

### 시작 라인
#### 응답 메시지

- start-line = request-line / **status-line**
- **status-line** =HTTP-version _SP_ status-code _SP_ reason-phrase _CRLF_


- HTTP 버전
- HTTP 상태 코드 : 요청 성공, 실패를 나타낸다
  - 200 : 성공
  - 400 : 클라이언트 요청 오류
  - 500 : 서버 내부 오류
- 이유 문구 : 사람이 이해할 수 있는 짧은 HTTP 상태 코드 설명 글

---

### HTTP 헤더

- header-field = field-name":" _OWS_ field-value _OWS_ ( OWS : 띄어쓰기 허용 )
- field-name 은 대소문자 구분 없음
- 그러나 field-value 는 대소문자를 구분한다

---

#### 용도

- HTTP 전송에 필요한 모든 부가정보
- 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트( 브라우저 ) 정보, 서버 애플리케이션 정보, 캐시 관리 정보 등등...
  - 메시지 body 빼고, 필요한 메타데이터 정보가 모두 들어있다고 이해하면 된다.
- 표준 헤더가 너무 많음
  - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
- 필요시 임의의 헤더 추가 가능
  - helloworld : hihi
  - 임의의 헤더를 추가하면 약속한 클라이언트와 서버만 이해 가능

---

### HTTP 메시지 바디
#### 용도

- 실제 전송할 데이터
- HTML 문서, 이미지 , 영상, JSON 등등 byte 로 표현할 수 있는 모든 데이터 전송 가능

---

### 단순함 확장 가능

- HTTP 는 단순하다. 스펙도 읽어볼만...
- HTTP 메시지도 매우 단순
- 크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술
  - !!**단순하지만 확장 가능한 기술이 대부분 크게 성공**

---

### HTTP 정리

- HTTP 메시지에 모든 것을 전송
- HTTP 역사 HTTP/1.1 을 기준으로 학습
- 클라이언트 서버 구조
- 무상태 프로토콜( 스테이스리스 )
- HTTP 메시지
- 단순함, 확장 가능
- **지금은 HTTP 시대**

