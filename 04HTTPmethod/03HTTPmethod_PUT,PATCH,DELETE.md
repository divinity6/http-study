## HTTP 메서드 - PUT,PATCH,DELETE
HTTP 메서드는 클라이언트가 서버에 요청을할때 기대하는 행동이다.

### PUT

> PUT/members/100 HTTP/1.1
>
> Content-Type: application/json
>
>  {
>     "username" : "hello" ,
>     "age" : 20
>  }

- **리소스를 대체**
  - 리소스가 있으면 대체
  - 리소스가 없으면 생성
  - 쉽게 이야기해서 덮어버림
    - 폴더에 파일을 집어넣는 것과 똑같다
    - 폴더에 파일이 없으면 새로 생기지만 있으면 기존파일을 덮어씌워버림
    - **완전히 대체한다**
- **중요! 클라이언트가 리소스를 식별**
  - 클라이언트가 리소스 위치를 알고 URI 지정
  - POST 와 차이점
    - POST 와 다르게 **구체적인 리소스 전체경로를 다 알고 있다**
    - ( PUT/members/100 ) 클라이언트가 리소스의 정확한 위치를 알고 URI 를 지정해버리는 것!
    - POST 는 ( PUT/members )에 넣었다. 
    - 클라이언트는 100 에 맨들어질지, 200에 맨들어질지 모른다
    - 반대로 PUT 은 클라이언트에서 딱 지정을 한다.
    - 클라이언트가 리소스를 식별을 한다!
    
---

### PUT
#### 리소스가 있는 경우1

> 클라이언트
>
> ---
> 
> PUT/members/100 HTTP/1.1
> 
> Content-Type : application/json
>
>  {
>     "username" : "old" ,
>     "age" : 50
>  }

_PUT -->_


> **/members/100**
>
> ---
>
>  {
>     "username" : "young" ,
>     "age" : 20
>  }

---

### PUT
#### 리소스가 있는 경우2

> 클라이언트
>
> ---

_PUT -->_

리소스 대체
> **/members/100**
>
> ---
>
>  {
>     "username" : "**old**" ,
>     "age" : **50**
>  }

- 서버에 리소스가 있었지만, 그 리소스가 대체가 되어버린다

---

### PUT
#### 리소스가 없는 경우1

> 클라이언트
>
> ---
>
> PUT/members/100 HTTP/1.1
>
> Content-Type : application/json
>
>  {
>     "username" : "old" ,
>     "age" : 50
>  }

_PUT -->_

members/100 이라는 리소스가 없음
> **리소스가 없음**
>
> ---
> 
---

### PUT
#### 리소스가 없는 경우2

> 클라이언트
>
> ---

_PUT -->_

신규 리소스 생성
> **/members/100**
>
> ---
>
>  {
>     "username" : "**old**" ,
>     "age" : **50**
>  }

---

### PUT
#### 주의! - 리소스를 완전히 대체한다1

> 클라이언트
>
> ---
> 
> PUT/members/100 HTTP/1.1
>
> Content-Type : application/json
>
>  {
>     "age" : 50
>  }

- "username" 필드 없음
- 만약 나이만 50으로 업데이트하고싶다?

_PUT -->_

> **/members/100**
>
> ---
>
>  {
>     "username" : "**young**" ,
>     "age" : **20**
>  }

---

### PUT
#### 주의! - 리소스를 완전히 대체한다1

> 클라이언트
>
> ---

_PUT -->_

리소스 대체
> **/members/100**
>
> ---
>
>  {
>     "age" : **50**
>  }

- "username" 필드가 날아가고, 전송한 값으로 대체됨, 덮어버림
- put 은 리소스를 수정한다는 개념이 아니라, 갈아치우는 개념이라고 보는게 더 적합하다
- 따라서 , 수정을 할때는 PATCH 를 사용하면 된다

---

### PATCH

> PATCH/members/100 HTTP/1.1
>
> Content-Type: application/json
>
>  {
>     "age" : 20
>  }

- 리소스 부분 변경
  - 예전에는 PUT 만 있었지만 이런 요구사항때문에 PATCH 가 새로나왔다

---

### PATCH
#### 리소스 부분 변경1

> 클라이언트
>
> ---
>
> PATCH/members/100 HTTP/1.1
>
> Content-Type : application/json
>
>  {
>     "age" : 50
>  }
- "username" 필드 없음

_PATCH -->_

> **/members/100**
>
> ---
>
>  {
>     "username" : "young" ,
>     "age" : 20
>  }

---

### PATCH
#### 리소스 부분 변경2

> 클라이언트
>
> ---

_PATCH -->_

리소스 부분 변경
> **/members/100**
>
> ---
>
>  {
>     "username" : "young" ,
>     "age" : **50**
>  }
- age 만 50 으로 변경

---

### DELETE

> 클라이언트
>
> ---
> DELETE/members/100 HTTP/1.1
>
> Host: localhost:8080

- 리소스 제거

---

### DELETE
#### 리소스 제거1

> DELETE/members/100 HTTP/1.1
>
> Host: localhost:8080

_DELETE -->_

> **/members/100**
>
> ---
>
>  {
>     "username" : "young" ,
>     "age" : 20
>  }

---

### DELETE
#### 리소스 제거2

> 클라이언트
>
> ---

_DELETE -->_

리소스 제거
> **/members/100**
>
> ---

---

- 리소스를 부분변경할때는 PATCH 를 쓸 수 있지만,
- PATCH 가 지원안되는 서버들도 있다
  - 요즘에는 거의 된다
- HTTP 버전 자체에서 PATCH 를 못받아 들이는 경우가 있다
  - 이럴 경우에는 POST 를 사용하면 된다
  - POST 는 무적...

### HTTP 메서드의 속성

- 안전( Safe Methods )
- 멱등( Idempotent Methods )
- 캐시가능( Cacheable Methods )

HTTP 메서드마다 특징이 있다. 다음 절에서 특징에 대해 알아봄