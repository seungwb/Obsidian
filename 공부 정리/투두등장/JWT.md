### JWT 란?

- JWT는 "JSON Web Token"의 약자이다
- 웹 어플리케이션에서 사용자 인증 및 정보 교환을 위해 사용되는 **토큰 기반 인증 방법**이다

### JWT 구조

```
xxxxxx.yyyyyy.zzzzzz

Header.Payload.Signature
```

- JWT는 Header, Payload, Signature 로 구성되어 있다. 

##### 헤더 (Header)

```javascript
{ 
	"alg": "HS256", 
	"typ": "JWT" 
}
```

- Header는 두 가지 타입의 정보를 가지고 있다.
	- `alg` : Signature 해싱 알고리즘
	- `typ` : 토큰의 타입

##### 정보 (Payload)


```javascript
{
    "iss": "dnjscksdn98.com",
    "exp": "1485270000000",
    "https://dnjscksdn98.com/jwt_claims/is_admin": true,
    "userId": "dnjscksdn98",
    "username": "alex"
}
```

- Payload에는 토큰에 담을 정보가 들어있다.
- 이곳에 담는 정보의 조각을 클레임 (Claim) 이라고 부르고, Key/ Value 형식으로 이루어져 있다.
- 클레임의 종류는 Registered claims, Public claims, Private claims 로 나뉜다.
	-  등록된 클레임 ( Registered claims )
		- 등록된 클레임들은 토큰에 대한 정보들을 담기위하여 이름이 이미 정해진 클레임들이다. 필수는 아니지만, 권장되어 진다.
			- iss : 토큰을 발급한 주체(서버 또는 시스템) 의 식별자
			- sub : 토큰이 인증하는 주체 (사용자 또는 서비스)
			- aud : 토큰이 사용될 대상 시스템 또는 수신자
			- exp : 토큰 만료 시간
			- nbf : 토큰 활성 시작 시간
			- iat : 토큰 발급 시간
			- jti : 토큰 중복사용 방지를 위한 고유한 식별자 
	-  공개 클레임 ( Public claims )
		- 다른 개발자나 서비스와의 충돌을 방지하기 위해 [IANA JSON Web Token Claims Registry](https://www.iana.org/assignments/jwt/jwt.xhtml) 에 등록된 클레임을 사용하여야 한다.
		- 공개 클레임에는 누구나 읽을 수 있는 정보가 포함되므로 공개되면 안되는 정보(비밀번호, 계좌 번호 등)는 포함하면 안된다.
	-  비공개 클레임 ( Rpivate claims )
		- 비공개 클레임은 개인이나 특정 조직에서 내부적으로 정의하는 클레임이다.