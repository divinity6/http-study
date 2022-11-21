## 캐시 무효화

---

### Cache-Control
#### 확실한 캐시 무효화 응답

- **Cache-Control: no-cache, no-store, must-revalidate**
  - 캐시를 적용안해도 웹 브라우저들이, GET 요청일경우 임의로 캐시를 하기도 하기 때문에
  - 확실하게 무효화시킬 수 있다
  - **( 절대 캐시되면 안되는 것들 : 위의 옵션을 다넣어줘야한다 )**


- **Pragma: no-cache**
  - HTTP 1.0 하위 호환

---

### Cache-Control
#### 캐시 지시어( directives ) - 확실한 캐시 무효화

- **Cache-Control: no-cache**
  - 데이터는 캐시해도 되지만, 항상 **원 서버에 검증** 하고 사용( 이름에 주의 )


- **Cache-Control: no-store**
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨
  - ( 메모리에서 사용하고 최대한 빨리 삭제 )


- **Cache-Control: must-revalidate**
  - 캐시 만료후 최초 조회시 원 **서버에 검증**해야함
  - 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504( Gateway Timeout )
  - must-revalidate 는 캐시 유효 시간이라면 캐시를 사용함


- **Pragma: no-cache**
  - HTTP 1.0 하위 호환

---

### no-cache vs must-revalidate
#### no-cache 기본 동작

> 웹 브라우저

( **1. 캐시 서버 요청** ) 

( **no-cache + ETag** ) -->


> 프록시 캐시

( **2. 원 서버 요청** )

( **no-cache + ETag** ) -->

> 원 서버

( **3. 원 서버 검증** )

> 브라우저 캐시
> 
> ---
> 
> no-cache
> 
> ETag : "aaa"

- no-cache 는 응답코드를 **프록시 캐시가 원서버**로 보낸다


- 그럼 원서버에서 응답을 보낸다


- **304 Not Modified 응답**
  - 브라우저 캐시 사용 가능


- no-cache 인데, 프록시 캐시서버에서 원 서버에 접근할 수 없는 경우,


- 캐시 서버 설정에 따라서 캐시 데이터를 반환할 수 있음
- **Error or 200 0K**
  - ( 오류 보다는 오래된 데이타라도 보여주자 )
  - 즉, 프록시 캐시도 설정에 따라 응답가능

---


### no-cache vs must-revalidate
#### must-revalidate

> 웹 브라우저

( **1. 캐시 서버 요청** )

( **must-revalidate + ETag** ) -->


> 프록시 캐시

( **Must-revalidate** )

원 서버에 접근할 수 없는 경우, **항상 오류**가 발생해야 함

**504 Gateway Timeout**

( 매우 중요한 돈과 관련된 결과로 생각해보자 ) -->

> 원 서버

> 브라우저 캐시

- 통장 잔고같은것은 프록시캐시에 있는 과거데이터가 보이면 안되듯이...

---

따라서 Cache-Control 에 no-cache, no-store, must-revalidate 속성들을 다 넣어주면 완전히 캐시하지 않는다

( HTTP 1.0 이전 하위버전 생각하면 Pragma: no-cache 도... )