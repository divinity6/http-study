## 인증 헤더

- Authorization: 클라이언트 인증 정보를 서버에 전달


- WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의

---

### Authorization
#### 클라이언트 인증 정보를 서버에 전달

- Authorization: Basic xxxxxxxxxxxxxxxx
  - 인증은 여러 매커니즘이 있다( 오오스 인증등... )
  - 인증마다 value 에 들어가는 값이 완전 다르다
  - 따라서, 인증은 따로 공부해보면 어떤 값을 넣어야할지 알수 있다
  - 단지, HTTP Authorization 헤더는 헤더를 제공해주는 것

---

### WWW-Authenticate
#### 리소스 접근시 필요한 인증 방법 정의

- 리소스 접근시 필요한 인증 방법 정의
    - 만약 접근을 했는데 인증이 제대로 안되거나 문제가 있을 경우 
    - 401 Unauthorized 응답에 남김

- 401 Unauthorized 응답과 함께 사용


- WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"
  - 너가 인증을 하려면 이런정보들을 참고해서 제대로된 인증정보를 만들어!! 라고 하는 것
---