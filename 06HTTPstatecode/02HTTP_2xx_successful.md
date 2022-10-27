## 2xx - 성공

---

### 2xx ( Successful )
#### 클라이언트의 요청을 성공적으로 처리

- 200 OK
- 201 Created
  - 클라이언트의 요청을 통해, 서버에서 뭔가를 생성했을 경우
- 202 Accepted
- 204 No Content

---

### 200 OK
#### 요청 성공

> 요청
>
> ---
>
> GET / members/100 HTTP/1.1
> 
> Host : localhost: 8080

_Request -->_

> 응답
>
> ---
>
> HTTP/1.1 200 OK
>
> Content-Type: application/json
>
> Content-Length: 34
> 
> {
>      "username" : "young",
>      "age" : 20
> }

_<-- 200 OK_

---

### 201 Created
#### 요청 성공해서 새로운 리소스가 생성됨

> 요청
>
> ---
>
> POST / members HTTP/1.1
>
> Content-Type : application/json
>
> {
>      "username" : "young",
>      "age" : 20
> }


_Request -->_

> 응답
>
> ---
>
> HTTP/1.1 201 Created
>
> Content-Type: application/json
>
> Content-Length: 34
>
> **Location: /members/100**
> 
>  ( 생성된 리소스는 응답의 **Location** 헤더 필드로 식별 )
> 
> {
>      "username" : "young",
>      "age" : 20
> }

_<-- 201 Created_

- 서버에서 리소스를 생성했기 때문에, Location 에 해당 자원의 위치를 알려준다
- 201 은 Location 헤더가 존재한다

---

### 202 Accepted
#### 요청이 접수되었으나 처리가 완료되지 않았음


- 배치 처리 같은 곳에서 사용
- 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함

---

### 204 No Content
#### 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음

- 예) 웹 문서 편집기에서 save 버튼
- save 버튼의 결과로 아무 내용이 없어도 된다
- save 버튼을 눌러도 같은 화면을 유지해야 한다
- 결과 내용이 없어도 204 메시지( 2xx )만으로 성공을 인식할 수 있다

---

