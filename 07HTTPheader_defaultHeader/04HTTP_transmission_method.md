## 전송 방식

- Transfer-Encoding


- Range, Content-Range

---

### 전송 방식 설명

- 단순 전송


- 압축 전송


- 분할 전송


- 범위 전송

---

### 단순 전송
#### Content-Length

_GET /event -->_

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
>
> Content-Type: text/html;charset=UTF-8
>
> **Content-Length: 3423**
>
> ---
>
> **body**
>
> ````html
> <html>
>   <body>...</body>
> </html>
> ````

- 단순전송은 요청을 하면 그냥 응답을 주는데, message body 에 대한 Content-Length 를 알 수 있을 때 쓴다
- 길이를 알고, 길이값을 주는 것이다
- 단순히 요청하고 한번에 받는 것

---

### 압축 전송
#### Content-Encoding

_GET /event -->_

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
>
> Content-Type: text/html;charset=UTF-8
>
> **Content-Encoding: gzip**
> 
> Content-Length: 3423
>
> ---
>
> **body**
>
> ````text
> lkj123kljoiasudlkjaweioluywlnfdo912u34ljko98udjkl
> ````

- 서버에서 데이터를 압축해서 주는 것( 실제로 절반이상 줄어든다 )
  - 대신 이경우에는 **Content-Encoding** 을 추가로 넣어줘야 한다
  - 뭘로 압축되어있는지 넣어줘야 한다

---

### 분할 전송
#### Transfer-Encoding

_GET /event -->_

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
>
> Content-Type: text/html;charset=UTF-8
>
> **Transfer-Encoding: chunked**
>
> ---
>
> **body**
>
> ````text
> 5
> Hello
> 5
> World
> 0
> \r\n
> ````

*chunked : 덩어리 ,
- 내가 chunked( 덩어리 )로 쪼개서 보낼거야
- 즉, 
  - 5 바이트를 보낼건데 데이터는 Hello
  - 5 바이트를 또 보내는데 데이터는 World
  - 0 마지막 표시는 \r\n
  

- 이런것은 용량이 클 경우 데이터를 보내야 할때 분할해서 보내는 것
  - 참고로 분할 전송때는 Content-Length 를 넣으면 안된다
  - Content-Length 가 예상이 안됨
  - 또한, 각 chunked 마다 바이트 정보가 다 있기 때문

---

### 범위 전송
#### Range, Content-Range

_GET /event -->_

> **start-line**
>
> GET /event -->_
> 
> ---
> 
> Range: bytes=1001-2000

> **start-line**
>
> HTTP/1.1 **200 OK**
>
> ---
>
> **header**
>
> Content-Type: text/plain
>
> **Content-Range: bytes 1001-2000 / 2000**
>
> ---
>
> **body**
>
> ````text
> qweqwe1l2iu3019u2oehj1987askjh3q98y
> ````

- 이미지를 중간까지 받았을때, 연결이 끊겼을 경우, 다시요청해야 한다
- 그런데, 처음부터 다시 받으면 용량이 아깝기 때문에, 범위전송은 범위를 지정해서( Content-Range ) 요청할 수 있다

---

HTTP 의 전송방식은 위 4가지가 대표적이다