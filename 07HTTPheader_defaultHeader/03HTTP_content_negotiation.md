## 협상( 콘텐츠 네고시에이션 )
## 클라이언트가 선호하는 표현 요청

> 클라이언트가 원하는 표현( Representation )으로 달라고 서버에게 요청하는 것

- **Accept** : 클라이언트가 선호하는 미디어 타입 전달


- **Accept-Charset**: 클라이언트가 선호하는 문자 인코딩


- **Accept-Encoding**: 클라이언트가 선호하는 압축 인코딩


- **Accept-Language**: 클라이언트가 선호하는 자연 언어


- **협상 헤더는 요청시에만 사용**

---

### Accept-Language 적용 전

> /event
> 
> ---
> 
> 한국어 브라우저 사용

-- _GET /event -->_

_<-- Content-Language: **en**_ 
    
 hello( 영어 ) --
 
> 다중 언어 지원 서버
> 
> ---
> 
> 1. 기본 영어( en )
> 
> 
> 2. 한국어 지원( ko )

---

### Accept-Language 적용 후

> /event
>
> ---
>
> 한국어 브라우저 사용

-- _GET /event_

Accept-Language: **ko** -->

_<-- Content-Language: **ko**_

안녕하세요 --

> 다중 언어 지원 서버
>
> ---
>
> 1. 기본 영어( en )
>
>
> 2. 한국어 지원( ko )

---

### Accept-Language 복잡한 예시

> /event
>
> ---
>
> 한국어 브라우저 사용

-- _GET /event_

Accept-Language: **ko** -->

_<-- Content-Language: **de**_

Hallo( 독일어 ) --

> 다중 언어 지원 서버
>
> ---
>
> 1. 기본 독일어( de )
>
>
> 2. 영어도 지원( en )

- 한국어를 지원하지 않을때, 독일어보단 영어를 받고싶은 상황
- 이런상황일때, 우선순위가 필요하다!

---

### 협상과 우선순위1
#### Quality Values( q )

> GET /event
> 
> Accept-Language: _ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7_

- Quality Values( q ) 값 사용


- 0 ~ 1, **클수록 높은 우선순위**


- 생략하면 1


- Accept-Language: ( ko-KR : 한국용 한국어 - 1 생략됨 ),( ko;q=0.9 : 그냥 한국 공통어 ),( en-US;q=0.8 : 미국 영어 ),( en;q=0.7 : 공통 영어)
    1. ko-KR;q=1( q 생략 )
    2. ko;q=0.9
    3. en-US;q=0.8
    4. en;q=0.7

---

### Accept-Language 복잡한 예시

> /event
>
> ---
>
> 한국어 브라우저 사용

-- _GET /event_

Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7 -->

_<-- Content-Language: **en**_

Hello( 영어 ) --

> 다중 언어 지원 서버
>
> ---
>
> 1. 기본 독일어( de )
>
>
> 2. 영어도 지원( en )

- 영어를 독일어보다 선호하는 걸 우선순위를 통해 알기 때문에 영어를 보내주게 된다

---

### 협상과 우선순위2
#### Quality Values( q )

> GET /event
>
> Accept: text/*, text/plain, text/plain;format=flowed, <span> * </span>/<span> * </span>


- **구체적인 것이 우선한다**
  - 즉, 디테일한것이 우선한다
  - *( 별 ) : 아무거나 들어와도됨 

- Accept: **text / <span> * </span>** , **text/plain** , **text/plain;format=flowed**, **<span> * </span>/<span> * </span>**
  1. text/plain;format=flowed
  2. text/plain
  3. text/ *
  4. <span> * </span>/<span> * </span>

---

### 협상과 우선순위3
#### Quality Values( q )

- 구체적인 것을 기준으로 미디어 타입을 맞춘다


- Accept: **text / <span> * </span>**;q=0.3 , **text/html**;q=0.7 , **text/html;level=1**, **text/html;level=2**;q=0.4, **<span> * </span>/<span> * </span>**;q=0.5


| Media Type        | Quality |
|:------------------|:-------:|
| text/html;level=1 |    1    |
| text/html;        |   0.7   |
| text/plain;       |   0.3   |
| image/jpeg;       |   0.5   |
| text/html;level=2 |   0.4   |
| text/html;level=3 |   0.7   |

- text/plain 값은 기본 0.3 이다
- 그런데 이렇게 복잡하게 네고시에이션이 내려갈일은 잘 없다

---
