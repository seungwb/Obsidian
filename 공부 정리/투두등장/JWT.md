### JWT 란?

- JWT는 "JSON Web Token"의 약자이다
- 웹 어플리케이션에서 사용자 인증 및 정보 교환을 위해 사용되는 **토큰 기반 인증 방법**이다

### JWT 구조

```
xxxxxx.yyyyyy.zzzzzz

Header.Payload.Signature
```

- JWT는 Header, Payload, Signature로 구성되어 있다. 

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