## URI( Uniform Resource Identifier )

- 리소스를 식별하는 통합된 방법

**URI? URL? URN?**

URI 는 로케이터( locator ), 이름( name ) 또는, 둘 다 추가로 분류될 수 있다

---

> URI( Resource Identifier)
> - 리소스를 식별하는 가장 큰 개념
> 
>> URL( Resource **Locator** )
>> 
>> 리소스의 위치 정보
>
>> URN( Resource **Name** )
>>
>> 리소스의 이름


---

#### URL( Resource Locator )

foo **( scheme )** : //example.com:8042 **( authority )** /over/there **( path )** ?name=ferret **( query )** #nose **( fragment )**

---

#### URN( Resource Name )

urn: **( scheme )** : example:animal:ferret:nose **( path )**

---

* 위처럼 URN 으로 이름을 부여하면 찾기가 힘들다.
따라서 , 거의 URL 만 사용한다

---

### URI 단어 뜻 :

- **U**niform : 리소스 식별하는 통일된 방식
- **R**esource : 자원, URI 로 식별할 수 있는 모든 것( 제한 없음 )
  - 실시간 교통정보등 구분할 수 있는 모든 것을 Resource 라고 부른다
- **I**dentifier : 다른 항목과 구분하는데 필요한 정보

---

즉, 

URL : Uniform Resource Locator

URN : Uniform Resource Name

___

### URL, URN 단어 뜻 :

- URL - Locator : 리소스가 있는 위치를 지정
- URN - Name : 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다
- urn:isbn:8960777331( 어떤 책의 isbn URN )
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
- ***앞으로 URI를 URL과 같은 의미로 이야기 함***

---
URL 분석

https://www.google.com/search?q=hello&hl=ko

### URL 전체 문법

- scheme://[ userinfo@ ]host[ :port ][ /path ][ ?query ][ #fragment ]
- https://www.google.com:443/search?q=hello&hl=ko


- 프로토콜( https )
- 호스트명( www.google.com )
- 포트번호( 443 )
- 패스( /search )
- 쿼리 파라미터( q=hello&hl=ko )

---

### URL scheme

- **scheme**: [ userinfo@ ]host[ :port ][ /path ][ ?query ][ #fragment ]
- **https**://www.google.com:443/search?q=hello&hl=ko


- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
  - 예) http, https, ftp 등등
- http 는 80 포트, https 는 443 포트를 주로 사용, 포트는 생략 가능
- https 는 http 에 강력한 보안 추가( HTTP Secure )

---
### URL userinfo

- scheme://**[ userinfo@ ]**host[ :port ][ /path ][ ?query ][ #fragment ]
- https://www.google.com:443/search?q=hello&hl=ko


- URL에 사용자 정보를 포함해서 인증
- 거의 사용하지 않음

---

### URL host

- scheme://[ userinfo@ ]**host**[ :port ][ /path ][ ?query ][ #fragment ]
- https://**www.google.com**:443/search?q=hello&hl=ko


- 호스트명
- 도메인명 또는 IP 주소를 직접 사용가능

---

### URL port

- scheme://[ userinfo@ ]host**[ :port ]**[ /path ][ ?query ][ #fragment ]
- https://www.google.com:**443**/search?q=hello&hl=ko


- 포트( PORT )
- 접속 포트
- 일반적으로 생략, 생략시 http 는 80, https 는 443
  - 일반적으로는 생략하지만 특정서버에 따로 접근해야 할때는, 입력하기도 함

---

### URL path

- scheme://[ userinfo@ ]host[ :port ]**[ /path ]**[ ?query ][ #fragment ]
- https://www.google.com:443/ **search**?q=hello&hl=ko


- 리소스 경로( path ), 보통 계층적 구조로 되어있다
- 예)
  - /home/file1.jpg
  - /members
  - /members/100,/items/iphone12

---

### URL query
- scheme://[ userinfo@ ]host[ :port ][ /path ]**[ ?query ]**[ #fragment ]
- https://www.google.com:443/search **?q=hello&hl=ko**


- key=value 형태
- ?로 시작,& 로 추가 가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불린다, 웹서버에 제공하는 파라미터, 문자 형태

---

### URL fragment
- scheme://[ userinfo@ ]host[ :port ][ /path ][ ?query ]**[ #fragment ]**
- https://docs.spring.io/spring-boot/docs/current/reference/html/getting-start.html **#getting-started-introducing-spring-boot**

- fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보가 아니다

---

