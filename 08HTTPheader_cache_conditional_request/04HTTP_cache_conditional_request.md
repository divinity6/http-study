## 캐시와 조건부 요청 헤더

---

### 캐시 제어 헤더

- Cache-Control: 캐시 제어


- Pragma : 캐시 제어( 하위 호환 )


- Expires : 캐시 유효 기간( 하위 호환 )

---

### Cache-Control
#### 캐시 지시어( directives )

지금은 이 cache-control 로 Pragma , Expires 를 둘 다 할 수 있기 때문에 제일 중요하다

- Cache-Control: max-age
  - 캐시 유효 시간, 초 단위


- Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 원( origin ) 서버에 검증하고 사용
  - If-Modified-Since 등
  - 원서버 : 사실 요청을 하면 중간에 캐시 서버, 프록시 서버등을 거쳐서 원서버로 간다

- Cache-Control: no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨
  - ( 메모리에서 사용하고 최대한 빨리 삭제 )

---

### Pragma
#### 캐시 제어( 하위 호환 )

- Pragma: no-cache


- HTTP 1.0 하위 호환
  - 지금은 거의 사용하지 않음
  - 그러나 하위호환때문에 사용하기도 함


---

### Expires
#### 캐시 만료일 지정( 하위 호환 )

- expires: Mon, 01 Jan 1990 00:00:00 GMT


- 캐시 만료일을 정확한 날짜로 지정
  - max-age 는 초단위로 지정하는게 아닌, 정확한 날짜를 지정
  - ( 초 단위가 훨씬 유연하다 )


- HTTP 1.0 부터 사용


- 지금은 더 유연한 Cache-Control: max-age 권장


- Cache-Control: max-age 와 함께 사용하면 Expires 는 무시

---

### 검증 헤더와 조건부 요청 헤더

- **검증 헤더 ( Validator )**
  - **ETag**: "v1.0" , **ETag**: "asid93jkrh2l"
  - **Last-Modified**: Thu, 04 Jun 2020 07:19:24 GMT


- **조건부 요청 헤더**
  - If-Match, If-None-Match: ETag 값 사용
  - If-Modified-Since, If-Unmodified-Since: Last-Modified 값 사용