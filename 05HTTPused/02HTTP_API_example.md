## HTTP API 설계 예시

어떤식으로 URI 를 설계하는게 좋은지 예시

---

- **HTTP API - 컬렉션**
  - **POST 기반 등록**
  - 예) 회원 관리 API 제공


- **HTTP API - 스토어**
  - **PUT 기반 등록**
  - 예) 정적 컨텐츠 관리, 원격 파일 관리


- **HTML FORM 사용**
  - 웹 페이지 회원 관리
  - GET, POST 만 지원


---

### 회원 관리 시스템
#### API 설계 - POST 기반 등록

- 회원 관리 시스템 구축의 예
  - URI 는 항상 리소스를 식별해야 한다


- **회원** 목록 /members -> **GET**
- **회원** 등록 /members -> **POST**
  - members 컬렉션에 회원하나를 넣어주면 등록되도록...
- **회원** 조회 /members/{id} -> **GET**
- **회원** 수정 /members/{id} -> **PATCH,PUT,POST**
  - 수정시에 개념적으로는 PATCH 로하는게 제일 좋지만,
  - 게시글 수정등 특별한 경우에는 PUT 을 사용하기도 한다
  - 애매할땐 POST!
- **회원** 삭제 /members/{id} -> **DELETE**

---

### 회원 관리 시스템
#### POST - 신규 자원 등록 특징

- 클라이언트는 등록될 리소스의 URI 를 모른다
  - 회원 등록 /members -> POST
  - POST /members
    - 클라이언트가 던지면 서버가 알아서 새롭게 등록될 URI 를 맨들어준다


- 서버가 새로 등록된 리소스 URI 를 생성해준다
  - HTTP/1.1 201 Created
  - Location: **/members/100**
    - 이렇게 생성해서 다시 던져준다


- <span style="color: red">컬렉션( Collection )</span>
  - 서버가 관리하는 리소스 디렉터리
  - <span style="color: red">서버가</span> 리소스의 URI 를 생성하고 관리
  - 여기서 컬렉션은 /members
    - 이런 형식을 컬렉션이라고 부른다

---

### 파일 관리 시스템
#### API 설계 - PUT 기반 등록

- 파일 관리 시스템 구축의 예


- **파일** 목록 /files -> **GET**
- **파일** 조회 /files/{filename} -> **GET**
- **파일** 등록 /files/{filename} -> **PUT**
- **파일** 삭제 /files/{filename} -> **DELETE**
- **파일** 대량 등록 /files -> **POST**

---

### 파일 관리 시스템
#### PUT - 신규 자원 등록 특징

- 클라이언트가 리소스 URI 를 알고 있어야 한다
  - 파일 등록 /files/{filename} -> PUT
  - PUT **/files/star.jpg**


- 클라이언트가 직접 리소스의 URI 를 지정한다


- <span style="color: red">스토어( Store )</span>
  - 클라이언트가 관리하는 리소스 저장소
  - <span style="color: red">클라이언트가</span> 리소스의 URI 를 알고 관리
  - 여기서 스토어는 /files


---

그니깐, 요청하는쪽에서 URI 등 해당 객체의 정보를 알아야할때는 스토어라 부르고,
몰라도 될때는 컬렉션이라고 부르네...


컬렉션에서 요청하면 알아서 내려주는 것...

---

### HTML FORM 사용

- HTML FORM 은 **GET,POST 만 지원**
- AJAX 같은 기술을 사용해서 해결 가능 -> 회원 API 참고
- 여기서는 순수 HTML, HTML FORM 이야기
- GET,POST 만 지원하므로 제약이 있음

---

### HTML FORM 사용

- **회원** 목록 /members -> **GET**
- **회원** 등록 폼 /members/new -> **GET**
- **회원** 등록 /members/new, members -> **POST**
- **회원** 조회 /members/{id} -> **GET**
- **회원** 수정 폼 /members/{id}/edit -> **GET**
- **회원** 수정 /members/{id}/edit, /members/{id} -> **POST**
- **회원** 삭제 /members/{id}/delete -> **POST**
  - DELETE method 를 사용하지 못할때는 컨트롤 URI 를 이용하여 제거

---

### HTML FORM 사용

- HTML FORM 은 **GET,POST 만 지원**
- **컨트롤 URI**
  - GET,POST 만 지원하므로 제약이 있음
  - 이런 제약을 해결하기 위해 **동사로 된 리소스 경로** 사용
  - POST 의 /new, /edit, /delete 가 컨트롤 URI
  - HTTP 메서드로 해결하기 애매한 경우 사용( HTTP API 포함 )


- 컨트롤 URI 를 무식하게 사용하면 안된다.
  - 최대한 리소스 개념을 가지고 URI 를 설계하고, 
  - 그상황에서 안될때, 컨트롤 URI 를 사용하면 된다
  
---

### 정리

- **HTTP API - 컬렉션**
  - **POST 기반 등록**
  - **서버가 리소스 URI 결정**


- **HTTP API - 스토어**
  - **PUT 기반 등록**
  - **클라이언트가 리소스 URI 결정**


- **HTML FORM 사용**
  - 순수 HTML + HTML form 사용
  - GET, POST 만 지원

---

### 정리
#### 참고하면 좋은 URI 설계 개념


- 문서( document )
  - 단일 개념( 파일 하나, 객체 인스턴스 , 데이터베이스 row )
  - 예) /members/100, /files/star.jpg


- <span style="color: red">**컬렉션( collection )**</span>
  - 서버가 관리하는 리소스 디렉터리
  - 서버가 리소스의 URI 를 생성하고 관리
    - 즉, 지가 직접 관리함..ㅋㅋ
  - 예) /members


- <span style="color: red">**스토어( store )**</span>
  - 클라이언트가 관리하는 자원 저장소
  - 클라이언트가 리소스의 URI 를 알고 관리
    - 외부에서 위치를 알아서 요청할 수 잇지...ㅋㅋ
  - 예) /files


- **컨트롤러( controller ), 컨트롤 URI**
  - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
  - 동사를 직접 사용
  - 예) /members/{id}/delete