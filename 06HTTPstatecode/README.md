## HTTP 상태 코드

http 상태코드는 클라이언트가 서버로 요청을 보내면, 요청이 잘 처리되었는지를
response 가 올때 알려주는 기능이다( request 가 아님 )

---

### 상태 코드
#### 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx( Informational ) : 요청이 수신되어 처리중
- 2xx( Successful ) : 요청 정상 처리
- 3xx( Redirection ) : 요청을 완료하려면 추가 행동이 필요
- 4xx( Client Error ) : 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 5xx( Server Error ) : 서버 오류, 서버가 정상 요청을 처리하지 못함

---

### 만약 모르는 상태코드가 나타난다면?

- 클라이언트가 인식할 수 없는 상태코드를 서버가 반환하면?
- 클라이언트는 상위 상태코드로 해석해서 처리
- 미래에 새로운 상태코드가 추가되어도 클라이언트를 변경하지 않아도 됨
- 예)
  - 299 ??? -> 2xx( Successful )
  - 451 ??? -> 4xx( Client Error )
  - 599 ??? -> 5xx( Server Error )


---

### 1xx ( Informational )
#### 요청이 수신되어 처리중

- 거의 사용하지 않으므로 생략
  - 한번도 실무에서 본적이 없을정도...
