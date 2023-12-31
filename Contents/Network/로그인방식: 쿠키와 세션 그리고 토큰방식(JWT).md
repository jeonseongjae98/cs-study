# 쿠키


쿠키는 **Key-Value 형식의 문자열** 덩어리이다.

클라이언트가 어떠한 웹사이트를 방문할 경우, 그 사이트가 사용하고 있는 서버를 통해 **클라이언트의 브라우저에 설치되는 작은 기록 정보 파일**이다. 각 사용자마다의 브라우저에 정보를 저장하니 고유 정보 식별이 가능한 것이다.
<br>

### Cookie 인증 방식

[![01.png](https://i.postimg.cc/K8tQ8q0J/01.png)](https://postimg.cc/9DFyxp57)

1. 브라우저(클라이언트)가 서버에 요청(접속)을 보낸다.
2. 서버는 클라이언트의 요청에 대한 응답을 작성할 때, 클라이언트 측에 저장하고 싶은 정보를 응답 헤더의 Set-Cookie에 담는다.
3. 이후 해당 클라이언트는 요청을 보낼 때마다, 매번 저장된 쿠키를 요청 헤더의 Cookie에 담아 보낸다.
서버는 쿠키에 담긴 정보를 바탕으로 해당 요청의 클라이언트가 누군지 식별하거나 정보를 바탕으로 추천 광고를 띄우거나 한다.

<br>

### 쿠키 방식의 단점

- 요청 시 쿠키의 값을 그대로 보내기 때문에 유출 및 조작 당할 위험이 존재한다. (보안에 취약)
- **용량 제한**이 있어 많은 정보를 담을 수 없다
- 웹 브라우저마다 쿠키에 대한 지원 형태가 달라 **브라우저간 공유가 불가능**하다.
- 쿠키의 사이즈가 커질수록 네트워크에 부하가 심해진다.

<br>

# 세션


쿠키의 보안적 이슈 때문에, 세션은 비밀번호 등 클라이언트의 민감한 인증 정보를 브라우저가 아닌서버 측에 저장하고 관리한다. 서버의 메모리에 저장하기도 하고, 서버의 로컬 파일이나 데이터베이스에 저장하기도 한다.

<br>

---

### Session 인증 방식

[![02.png](https://i.postimg.cc/s2ccpBdW/02.png)](https://postimg.cc/1g8wS3zR)

1. 유저가 웹사이트에서 로그인하면 세션이 서버 메모리(혹은 데이터베이스) 상에 저장된다. 이때, 세션을 식별하기 위한 Session Id를 기준으로 정보를 저장한다.
2. 서버에서 브라우저에 쿠키에다가 Session Id를 저장한다.
3. 쿠키에 정보가 담겨있기 때문에 브라우저는 해당 사이트에 대한 모든 Request에 Session Id를 쿠키에 담아 전송한다.
4. 서버는 클라이언트가 보낸 Session Id 와 서버 메모리로 관리하고 있는 Session Id를 비교하여 인증을 수행한다.

<br>

---

### Session 방식의 단점

- 쿠키를 포함한 요청이 외부에 노출되더라도 세션 ID 자체는 유의미한 개인정보를 담고 있지 않는다. 
그러나 해커가 **세션 ID 자체를 탈취**하여 클라이언트인척 위장할 수 있다는 한계가 존재한다. ~~(이는 서버에서 IP특정을 통해 해결 할 수 있긴 하다)~~
- 서버에서 세션 저장소를 사용하므로 요청이 많아지면 서버에 부하가 심해진다.

<br>

# 토큰


토큰 기반 인증 시스템은 클라이언트가 서버에 접속을 하면 서버에서 해당 클라이언트에게 인증되었다는 의미로 **'토큰'을 부여**한다. 

이 토큰은 **유일**하며 토큰을 발급 받은 클라이언트는 또 다시 서버에 요청을 보낼 때 요청 헤더에 토큰을 심어서 보낸다. 

그러면 서버에서는 클라이언트로부터 받은 토큰을 서버에서 제공한 토큰과의 일치 여부를 체크하여 인증 과정을 처리하게 된다.

기존의 세션 기반 인증은 서버가 파일이나 데이터베이스에 세션 정보를 가지고 있어야 하고 이를 조회하는 과정이 필요하기 때문에 많은 오버헤드가 발생한다. 하지만 토큰은 세션과는 달리 **서버가 아닌 클라이언트에 저장**되기 때문에 메모리나 스토리지 등을 통해 세션을 관리했던 서버의 부담을 덜 수 있다.

토큰 자체에 데이터가 들어있기 때문에 클라이언트에서 받아 위조되었는지 판별만 하면 되기 떄문이다. 

토큰은 **앱과 서버가 통신 및 인증할때 가장 많이 사용**된다. 왜냐하면 웹에는 쿠키와 세션이 있지만 앱에서는 없기 때문이다.

---

### Token 인증 방식

[![03.png](https://i.postimg.cc/JnzQK1M2/03.png)](https://postimg.cc/yJ298CJm)

1. 사용자가 아이디와 비밀번호로 로그인
2. 서버 측에서 사용자(클라이언트)에게 유일한 토큰을 발급
3. 클라이언트는 서버 측에서 전달 받은 토큰을 쿠키나 스토리지에 저장해 두고, 서버에 요청을 할 때마다 해당 토큰을 HTTP 요청 헤더에 포함 시켜 전달함.
4. 서버는 전달 받은 토큰을 검증하고 요청에 응답함. (토큰에는 요청한 사람의 정보가 담겨있어 서버는 따로 DB를 조회하지 않고도 누가 요청하는지 알 수 있음)

<br>

### Token 방식의 단점

1. 쿠키/세션과 다르게 토큰 자체의 데이터 길이가 길어, 인증 요청이 많아질수록 네트워크 부하가 심해질수 있다.
2. Payload 자체는 암호화되지 않기 때문에 유저의 중요한 정보는 담을 수 없다.
3. 토큰을 탈취당하면 대처하기 어렵다. (따라서 사용 기간 제한을 설정하는 식으로 극복한다)

<br>

# JWT ****(JSON Web Token)****


JWT(JSON Web Token)란, **인증에 필요한 정보들을 암호화시킨 JSON 토큰**을 의미한다. 

JWT는 JSON 데이터를Base64 URL-safe Encode 를 통해 인코딩하여 직렬화한 것이며, 토큰 내부에는 위변조 방지를 위해 개인키를 통한 **전자서명**도 들어있다. 

따라서 사용자가 JWT 를 서버로 전송하면 서버는 서명을 검증하는 과정을 거치게 되며 검증이 완료되면 요청한 응답을 돌려준다

<br>

### JWT 구조

---

[![03-2-JWT.png](https://i.postimg.cc/3Rv07Rj6/03-2-JWT.png)](https://postimg.cc/1ny3ryjc)

JWT는 . 을 구분자로 나누어지는 세 가지 문자열의 조합이다.

Header 에는 JWT 에서 사용할 타입과 해시 알고리즘의 종류가 담겨있고, Payload 는 서버에서 첨부한 사용자 권한 정보와 데이터가 담겨있다.

마지막으로 Signature 에는 Header, Payload 를 Base64 URL-safe Encode 를 한 이후 Header 에 명시된 해시함수를 적용하고, 개인키(Private Key)로 서명한 전자서명이 담겨있다.


**Header**

- alg : 서명 암호화 알고리즘 (ex:HMAC SHA256, RSA )
- typ : 토큰 유형

**Payload**

- 토큰에서 사용할 정보의 조각들인 Claim이 담겨있다. 즉, 서버와 클라이언트가 주고받는 시스템에서 **실제로 사용될 정보에 대한 내용**을 담고 있는 섹션이다.

**Signature**

- 시그니처에서 사용하는 알고리즘은 헤더에서 정의한 알고리즘 방식(alg)을 활용한다.
- 시그니처의 구조는 (헤더 + 페이로드)와 서버가 갖고 있는 유일한 key 값을 합친 것을 헤더에서 정의한 알고리즘으로 암호화를 한다.

[![04-JWT.png](https://i.postimg.cc/63bfmDQ5/04-JWT.png)](https://postimg.cc/5YvzHKvZ)

<br>

### JWT를 이용한인증과정

---

[![05-JWT.png](https://i.postimg.cc/nV51Yb53/05-JWT.png)](https://postimg.cc/4n6tsMXc)

1. 사용자가 ID, PW를 입력하여 서버에 **로그인 인증을 요청**한다.
2. 서버에서 클라이언트로부터 인증 요청을 받으면, Header, PayLoad, Signature를 정의한다.
Hedaer, PayLoad, Signature를 각각 Base64로 한 번 더 암호화하여 **JWT를 생성**하고 이를 쿠키에 담아 **클라이언트에게 발급**한다.
3. 클라이언트는 서버로부터 받은 JWT를 로컬 스토리지에 저장한다. (쿠키나 다른 곳에 저장할 수도 있음)
API를 서버에 요청할때 Authorization header에 Access Token을 담아서 보낸다.
4. 서버가 할 일은 클라이언트가 Header에 담아서 보낸 JWT가 내 서버에서 발행한 토큰인지 일치 여부를 확인하여 일치한다면 인증을 통과시켜주고 아니라면 통과시키지 않으면 된다.
인증이 통과되었으므로 페이로드에 들어있는 유저의 정보들을 select해서 클라이언트에 돌려준다.
5. 클라이언트가 서버에 요청을 했는데, 만일 액세스 토큰의 시간이 만료되면 클라이언트는 리프래시 토큰을 이용해서
6. 서버로부터 새로운 엑세스 토큰을 발급 받는다.

<br>

### 토큰 인증 신뢰성을 가지는 이유

유저 JWT : A(Header) + B(Payload) + C(Signature) 일 때

1. 다른 유저가 B를 임의로 수정 → 유저 JWT : A + B’ + C
2. 수정한 토큰을 서버에 요청을 보내면 서버는 유효성 검사 시행
    - 유저 JWT : A + B’ + C
    - 서버에서 검증 후 생성한 JWT : A + B’ + C’ ⇒ signature 불일치
3. 대조 결과가 일치하지 않아 유저의 정보가 임의로 조작되었음을 알 수 있다.

<br>

### JWT 장점

---

1. Header와 Payload를 가지고 Signature를 생성하므로데이터 위변조를 막을 수 있다.
2. 인증 정보에 대한별도의 저장소가 필요없다.
3. JWT는 토큰에 대한 기본 정보와 전달할 정보 및 토큰이 검증됬음을 증명하는 서명 등 필요한 모든 정보를 자체적으로 지니고 있다.
4. 클라이언트 인증 정보를 저장하는 세션과 다르게,서버는 무상태(StateLess)가 되어 서버 확장성이 우수해질 수 있다.
5. 토큰 기반으로다른 로그인 시스템에 접근 및 권한 공유가 가능하다. (쿠키와 차이)
6. OAuth의 경우 Facebook, Google 등 소셜 계정을 이용하여 다른 웹서비스에서도 로그인을 할 수 있다.
7. 모바일 어플리케이션 환경에서도 잘 동작한다. (모바일은 세션 사용 불가능)

<br>

### JWT 단점

---

1. Self-contained : 토큰 자체에 정보를 담고 있으므로 양날의 검이 될 수 있다.
2. 토큰 길이 : 토큰의 Payload에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있다.
3. Payload 인코딩 : payload 자체는 암호화 된 것이 아니라 BASE64로 인코딩 된 것이기 때문에, 중간에 Payload를 탈취하여 디코딩하면 데이터를 볼 수 있으므로, payload에 중요 데이터를 넣지 않아야 한다.
4. Store Token : stateless 특징을 가지기 때문에, 토큰은 클라이언트 측에서 관리하고 저장한다. 때문에 토큰 자체를 탈취당하면 대처하기가 어렵게 된다.




## Access Token / Refresh Token


JWT도 제 3자에게 토큰 탈취의 위험성이 있기 때문에, 그대로 사용하는것이 아닌 Access Token, Refresh Token 으로 이중으로 나누어 인증을 하는 방식을 현업에선 취한다.

Access Token 과 Refresh Token은 둘다 똑같은 JWT이다. 다만 토큰이 어디에 저장되고 관리되느냐에 따른 사용 차이일 뿐이다.

- **Access Token** : 클라이언트가 갖고있는 실제로 유저의 정보가 담긴 토큰으로, 클라이언트에서 요청이 오면 서버에서 해당 토큰에 있는 정보를 활용하여 사용자 정보에 맞게 응답을 진행
- **Refresh Token**: 새로운 Access Token을 발급해주기 위해 사용하는 토큰으로 짧은 수명을 가지는 Access Token에게 새로운 토큰을 발급해주기 위해 사용. 해당 토큰은 보통 데이터베이스에 유저 정보와 같이 기록.
