## HTTP 메서드의 속성

- 안전( Safe Methods )
- 멱등( Idempotent Methods )
- 캐시가능( Cacheable Methods )

| HTTP 메소드 |   RFC    |             요청에 Body 가 있음              |            응답에 Body 가 있음             |                  안전                  |           멱등( Idempotent )           |                캐시 가능                 |
|:--------:|:--------:|:--------------------------------------:|:------------------------------------:|:------------------------------------:|:------------------------------------:|:------------------------------------:|
|   GET    | RFC 7231 |  <span style="color: red" >아니오</span>  | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | 
|   HEAD   | RFC 7231 |  <span style="color: red" >아니오</span>  | <span style="color: red" >아니오</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | 
|   POST   | RFC 7231 |  <span style="color: green" >예</span>  | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | <span style="color: red" >아니오</span> | <span style="color: green" >예</span> | 
|   PUT    | RFC 7231 |  <span style="color: green" >예</span>  | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | 
|  DELETE  | RFC 7231 |  <span style="color: red" >아니오</span>  | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | 
| CONNECT  | RFC 7231 |  <span style="color: green" >예</span>  | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | <span style="color: red" >아니오</span> | <span style="color: red" >아니오</span> | 
| OPTIONS  | RFC 7231 | <span style="color: blue" >선택사항</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | 
|  TRACE   | RFC 7231 |  <span style="color: red" >아니오</span>  | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | 
|  PATCH   | RFC 5789 |  <span style="color: green" >예</span>  | <span style="color: green" >예</span> | <span style="color: red" >아니오</span> | <span style="color: red" >아니오</span> | <span style="color: green" >예</span> | 
출처 : https://ko.wikipedia.org/wiki/HTTP

---

### 안전
#### Safe

- 호출해도 리소스를 변경하지 않는다
- Q : 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?
- A : 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.
  - 호출했을때 변경이 일어나지 않는걸 안전하다고 한다
  - 그런데 계속 호출을 하면, log 같은게 쌓여서 서버에 장애가 일어날 수 있지 않는가?
  - 안전( Safe )는 그런 부분을 고려하지 않는다. 해당 리소스가 변했나? 변하지 않았나만 고려한다

---

### 멱등
#### Idempotent

- f( f( x ) ) = f( x )
- _한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다._
- 멱등 메서드
  - **GET** : 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다
  - **PUT** : 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다
  - **DELETE** : 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다
  - **<span style="color:red">POST</span>** : 멱등이 아니다! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다


- 활용
  - 자동 복구 매커니즘
  - 서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단 근거


- **Q: 재요청 중간에 다른 곳에서 리소스를 변경해버리면?**
  - 사용자1 : GET -> username:A, age : 20
  - 사용자2 : PUT -> username:A, age : 30
  - 사용자1 : GET -> username:A, age : 30 -> 사용자2의 영향으로 바뀐 데이터 조회
- **A: 멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지는 않는다**
  - 내가 동일한 요청을 했을때, 멱등한 부분만 같은지 고려한다

---

### 캐시가능
#### Cacheable

- 응답 결과 리소스를 캐시해서 사용해도 되는가?
- GET,HEAD,POST,PATCH 캐시가능
- 실제로는 GET,HEAD 정도만 캐시로 사용
  - POST,PATCH 는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음
  - 캐시를 하려면 KEY 가 맞아야 한다. 똑같은 리소스와 키가 맞아야 하지만, 
  - POST 는 BODY 안의 데이터까지 고려해야 하기때문에 너무 복잡해진다
  - 그러나 GET 은 URL 을 KEY 로 잡고해도 되기때문에 실제로는 GET,HEAD 정도만 캐시해둔다

