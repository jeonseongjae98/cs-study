## HTTP Method 종류

HTTP 메서드란 클라이언트와 서버 사이에 이루어지는 요청(Request)과 응답(Response) 데이터를 전송하는 방식을 일컫는다. 쉽게 말하면 서버에 주어진 리소스에 수행하길 원하는 행동, <u><b>**서버가 수행해야 할 동작을 지정**</b></u>하는 요청을 보내는 방법이다.

HTTP 메소드의 종류는 총 9가지가 있다. 이 중 주로 쓰이는 메소드는 5가지로 보면 된다.

- **주요 메소드**
  
  - **GET :** 리소스 조회
  - **POST:**  요청 데이터 처리, 주로 등록에 사용
  - **PUT :** 리소스를 대체(덮어쓰기), 해당 리소스가 없으면 생성
  - **PATCH :** 리소스 부분 변경 (PUT이 전체 변경, PATCH는 일부 변경)
  - **DELETE :** 리소스 삭제
- **기타 메소드**
  
  - **HEAD :** GET과 동일하지만 메시지 부분(body 부분)을 제외하고, 상태 줄과 헤더만 반환
  - **OPTIONS :** 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
  - **CONNECT :** 대상 자원으로 식별되는 서버에 대한 터널을 설정
  - **TRACE :** 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

### HTTP 메서드 - GET

- **리소스 조회 메서드 (Read)**
  
- 서버에 전달하고 싶은 데이터는 쿼리스트링를 통해서 전달
  
  - GET /members/100?username=inpa&height=200
- 쿼리스트링 외에 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 서버에서 따로 구성해야 되기 때문에 지원하지 않는 곳이 많아서 권장하지 않음
  
- 조회할 때 POST도 사용할 수 있지만, GET 메서드는 캐싱이 가능하기에 GET을 사용하는 것이 유리하다.
  

#### 정적 데이터 조회 과정

- 이미지, 정적 텍스트 문서 GET
- 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

1. 클라이언트에서 /members/100 으로 100번 멤버를 조회해서 정보를 달라고 GET 요청

<p align="center"><img src="https://i.postimg.cc/J45VcXTb/img1-daumcdn.png"></p>

2. 서버에서는 요청 메세지를 분석해 내부의 유저정보를 조회한 뒤 결과 Response를 만든다.

<p align="center"><img src="https://i.postimg.cc/HLKfs9xC/img1-daumcdn.png"></p>

**3. 서버에서 클라이어트로 응답을 해준다. 그러면 클라이언트에서 정상적으로 받으면 200 OK status를 가지며, 회원정보를 얻게 된다.**

- 예시에서는 JSON 형태의 데이터이지만 실제로는 HTML일수도 있고 이미지 같은 멀티미디어 파일일 수도 있고 다양하다.

<p align="center"><img src="https://i.postimg.cc/gjy5s9KY/img1-daumcdn.png"></p>

#### 동적 데이터 조회 과정

- 주로 검색, 게시판 목록에서 검색어로 이용
- 쿼리 파라미터 사용해서 데이터를 전달
- 쿼리 파라미터는 key1=value1&key2=value2 구조로 되어 있음

1. 요청 URL 뒤에 ?q=hello&hl=ko 쿼리 파라미터를 줘서 상세한 조회 데이터를 얻는다

<p align="center"><img src="https://i.postimg.cc/x1X5TDbc/img1-daumcdn.png"></p>

#### **HTML Form 데이터 조회 과정**

- HTML Form 태그 문서로 사용자와 UI로 상호작용하여 서버와 통신
- HTML Form 전송은 GET, POST만 지원

1. 웹문서에서 폼 입력칸에 데이터를 적고 전송 버튼을 누른다.

<p align="center"><img src="https://i.postimg.cc/SsdCfDzB/img1-daumcdn.png"></p>

2. 지정한 GET 메서드 동작에 따라 input 태그안에 들어간 값들이 쿼리스트링으로 서버로 전송된다

<p align="center"><img src="https://i.postimg.cc/25fWpPdp/img1-daumcdn.png"></p>

### HTTP 메서드 - POST

- **전달한 데이터 처리/생성 요청 메서드 (Create)**
- 메시지 바디(body)를 통해 서버로 요청 데이터 전달하면 서버는 요청 데이터를 처리하여 업데이트
- 전달된 데이터로 주로 신규 리소스 등록, 프로세스 처리에 사용
- 만일 데이터를 GET 하는데 있어, JSON으로 조회 데이터를 넘겨야 하는 애매한 경우 POST를 사용

#### JSON 데이터 전송 과정

1. 클라이언트는 body에 등록할 회원 정보를 JSON 형태로 만들어 담고 서버로 전송한다.

<p align="center"><img src="https://i.postimg.cc/x1Qmhwyw/img1-daumcdn.png"></p>

2. 서버에서는 받은 메세지를 분석해 로직 대로 처리 한다. 예를 들어 데이터베이스에 등록하고 신규 아이디를 생성한다.

<p align="center"><img src="https://i.postimg.cc/zBH3V7Fw/img1-daumcdn.png"></p>

**3. 신규회원에 대한 데이터를 바디에 담아서 클라이언트로 응답한다.**

- 신규 자원 생성은 200이나 201로 응답을 보낸다.
- Location은 자원이 신규로 생성된 URI 경로를 의미한다.

<p align="center"><img src="https://i.postimg.cc/fyhWkNLZ/img1-daumcdn.png"></p>

#### HTML Form 데이터 전송 과정

- HTML Form 태그 문서로 사용자와 UI로 상호작용하여 서버와 통신
- 회원 가입, 상품 주문, 데이터 변경에 이용
- HTML Form 전송은 GET, POST만 지원

1. 웹문서에서 폼 입력칸에 데이터를 적고 전송 버튼을 누른다.

<p align="center"><img src="https://i.postimg.cc/SsdCfDzB/img1-daumcdn.png"></p>

2. 지정한 POST 메서드 동작에 따라 input 태그안에 들어간 값들이 쿼리스트링으로 서버로 전송된다

<p align="center"><img src="https://i.postimg.cc/NjLtsM4m/img1-daumcdn.png"></p>

> **[ Content-Type 헤더 종류 ]**
> 
> **Content-Type: application/x-www-form-urlencoded**
> 
> - Form의 내용을 HTTP 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)  
>   - 전송 데이터를 url encoding 처리  
>   - 예) abc김 → abc%EA%B9%80
> 
> **Content-Type: multipart/form-data**  
> - 파일 업로드 같은 바이너리 데이터 전송 시 사용
> 
> - 다른 종류의 여러 파일과 Form의 내용 함께 전송 가능. 그래서 이름이 multipart 이다.
> 
> **Content-Type: application/json**  
> - TEXT, XML, JSON 데이터 전송 시 사용

#### 파일 데이터 전송 과정

- enctype을 multipart/form-data 로 작성해 해당 폼에 파일이 있다는 것을 표시한다.
- 바이너리 데이터 전송시 사용한다.
- multipart/form-data 형식이라면 HTTP 메세지에 임의의 구분자(------XXX) 가 Form 데이터간 구분을 지어준다.
- 여러 개의 Content-Type에 대한 데이터를 보낼 수 있다.

<p align="center"><img src="https://i.postimg.cc/jjrM83L2/img1-daumcdn.png"></p>

### HTTP 메서드 - PUT

- **리소스를 대체(수정)하는 메서드 (Update)**
  
- 만일 요청 메세지에 리소스가 있으면 덮어쓰고, 없으면 새로 생성한다.
  
  - /members/100 데이터가 존재하면 기존에 것을 완전 대체 한다.
  - /members/100 데이터가 없으면 대체 할게 없으니까 새로 생성한다.

- 데이터를 대체해야 하니, 클라이언트가 리소스의 구체적인 전체 경로를 지정해 보내주어야 한다.
  
  - POST /members : 멤버 새로 추가
  - PUT /members/100 : 100번째 멤버 수정

#### PUT 요청에 리소스가 있는 경우

**1. 100번 유저의 리소스를 교체하겠다는 요청을 보낸다.**

<p align="center"><img src="https://i.postimg.cc/3r6CSfqh/img1-daumcdn.png"></p>

**2. 기존에 데이터가 있었다면 완전히 대체된다.**

<p align="center"><img src="https://i.postimg.cc/1XC9BNBR/img1-daumcdn.png"></p>

#### PUT 요청에 리소스가 없는 경우

1. 100번 유저의 리소스를 교체하겠다는 요청을 보낸다.

<p align="center"><img src="https://i.postimg.cc/wvFHxsS5/img1-daumcdn.png"></p>

2. 기존에 데이터가 없다면 POST 와 같이 신규로 생성한다.

<p align="center"><img src="https://i.postimg.cc/kM19kKNq/img1-daumcdn.png"></p>

#### PUT 요청에 일부 리소스만 변경하길 원할경우

1. age만 50으로 변경하려고 해당 데이터를 PUT으로 전달한다.

<p align="center"><img src="https://i.postimg.cc/V67QPPCD/img1-daumcdn.png"></p>

2. 하지만 기존 데이터가 완전히 대체되어 이름 데이터가 삭제된다. (이때는 PATCH 메소드를 이용해야 한다)

<p align="center"><img src="https://i.postimg.cc/YCccH3vK/img1-daumcdn.png"></p>

### **HTTP 메서드 - PATCH**

- **리소스 일부 부분을 변경하는 메소드** **(Update)**
- 만일 PATCH를 지원하지 않는 서버에서는 대신에 POST를 사용할 수 있다.

1. age만 50으로 변경하려고 해당 데이터를 PATCH로 전달한다.

<p align="center"><img src="https://i.postimg.cc/FFq8yZgd/img1-daumcdn.png"></p>

2. PUT과는 다르게 회원 정보에서 age만 변경된다.

<p align="center"><img src="https://i.postimg.cc/yNvrkX8N/img1-daumcdn.png"></p>

## **HTTP 메서드 - DELETE**

- **리소스 제거하는 메소드 (Delete)**
- 상태코드는 대부분 200을 사용하고 상황에 따라 204를 사용한다.

1. 100번째 멤버를 제거하기 위해 DELETE로 전달한다.

<p align="center"><img src="https://i.postimg.cc/jSXr4fSp/img1-daumcdn.png"></p>

2. 서버에서 요청을 받고 데이터베이스의 해당 리소스를 제거 한다.

<p align="center"><img src="https://i.postimg.cc/mrgWXrct/img1-daumcdn.png"></p>

## HTTP Status Code

HTTP의 상태 코드는 클라이언트가 보낸 HTTP 요청이 성공했는지 실패했는지를 서버에서 알려주는 숫자 코드다.

개발자 도구의 네트워크 탭을 보면 아래와 같이 Status 숫자 코드로 요청의 결과를 간략하게 나타내주는데, 클라이언트를 다루는 우리들은 이 숫자를 보고 결과를 단번에 유추할수 가 있게 된다.

HTTP 상태 코드는 **3자리 숫자**로 이루어져 있으며, 총 100번대 ~ 500번대 까지 존재한다. 그리고 각 상태코드의 첫 번째 자리는 최상위 코드가 되어 다음과 같이 5 개의 그룹으로 나뉘어 관리된다.

<p align="center"><img src="https://i.postimg.cc/tCGQ0kZ0/img1-daumcdn.png"></p>

**1XX : 요청이 수신되어 처리중**

**2XX : 요청 정상 처리**

**3XX : 요청을 완료하려면 추가 행동이 필요**

**4XX : 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음**

**5XX : 서버 오류, 서버가 정상 요청을 처리하지 못함**

<p align="center"><img src="https://i.postimg.cc/KYRs33kr/img1-daumcdn.png"></p>

### 1XX Informational

**1xx** 번대의 상태 코드들은 <u><b>**요청이 수신되어 처리 중**</b></u>이라는 의미를 가진다.

다만 협업에서도 잘 사용되지 않는 상태코드이기 때문에 깊게 다루어 지지는 않는다.

| 상태 코드 | 상태 메세지 | 설명  |
| --- | --- | --- |
| 100 | Continue | 처리가 되었으니 다음으로 진행 |
| 101 | Switching Protocols | 서버가 프로토콜을 전환중 |
| 102 | Processing | 서버가 요청을 아직 처리중이라 제대로된 응답을 알려줄수 없음 |
| 103 | Early Hints | 웹페이지에 필요한 리소스에 대한 힌트를 제공하여 리소스를 사전 로드하여 로딩을 빠르게 |

### 2XX Success

**2xx** 번대의 상태 코드들은 <u><b>**요청이 정상적으로 처리**</b></u>되었다는 의미를 가진다.

단순히 요청에 대한 성공을 나타내지만, 클라이언트가 어떠한 행위에 대한 성공인지에 대한 것을 나타내기 때문에, 응답을 받고 클라이언트가 취할 행위를 결정하는데 중요하면서도 정말 자주 보게될 상태 코드일 것이다.

<p align="center"><img src="https://i.postimg.cc/xTVCsK98/image.png"></p>

### **3XX Redirection**

**3xx** 번대의 상태 코드들은 <u><b>**리다이렉션**</b></u>을 의미하며, 이는 요청을 완료하려면 추가적인 작업이 필요함을 의미한다.

클라이언트가 관심 있어 하는 리소스에 대해 다른 위치를 사용하라고 말해주거나 그 리소스의 내용 대신 다른 대안 응답을 제공한다.

**리다이렉션(Redirection)** 은 클라이언트가 요청한 URL에 대해 다른 URL을 다시(re) 지시(direct)하여 다른 주소로 이동할 수 있게 하는 기술이다. HTTP 에 사용되는 리다이렉션은 크게 3가지 종류로 나눌 수 있다.

- 영구 리다이렉션(Permanent) : 특정 리소스의 URL 이 **영구적으로 이동**
- 일시 리다이렉션(Temporary) : 특정 리소스의 URL 이 **일시적으로 이동**
- 특수 리다이렉션(Special) : 캐시를 활용할 것인지에 대한 여부

<p align="center"><img src="https://i.postimg.cc/7ZdZjcz3/image.png"></p>

### **4XX Client Error**

**4xx** 번대의 상태 코드들은 <u><b>**클라이언트 오류**</b></u>를 의미하며, 잘못된 문법 등의 오류로 인해 서버가 요청을 수행할 수 없고 그 원인이 클라이언트에게 있음을 뜻한다. 잘못 구성된 요청 메세지 같은 것이 있을 수 있으며, 존재하지 않은 URL 요청도 있을 수 있다.

<p align="center"><img src="https://i.postimg.cc/DfxFtHkS/image.png"></p>

<p align="center"><img src="https://i.postimg.cc/kGp0Brqw/image.png"></p>

<p align="center"><img src="https://i.postimg.cc/FHcMsnqg/image.png"></p>

### **5XX Server Error**

**5xx** 번대의 상태 코드들은 <u><b>**서버 오류**</b></u>를 의미하며, 400 번대와 동일하게 오류로 인한 요청 처리 실패를 의미하지만 원인이 서버에게 있음을 뜻한다.

4XX 상태코드와 5XX 상태코드 모두 오류를 반환하는 응답 코드이지만, 4XX는 클라이언트의 요청에 문제가 있는 것이기에 요청 메세지를 검토하여 수정한 뒤 재전송하면 해결이 가능하지만, 5XX 는 서버에 문제가 있는 것이기 때문에 서버 자체의 상태를 보아야 하는 차이가 있다.

<p align="center"><img src="https://i.postimg.cc/KzYpL99W/image.png"></p>

<p align="center"><img src="https://i.postimg.cc/hvzCZXRb/image.png"></p>

## REST API

**REST API란 REST를 기반으로 만들어진 API를 의미합니다. REST API를 알기 위해 REST부터 알아보도록 하겠습니다.**

### REST란?

REST(Representational State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미합니다.

#### **즉 REST란**

1. HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
2. HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해
3. 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.

#### REST 구성 요소

REST는 다음과 같은 3가지로 구성이 되어있다. 

1. **자원(Resource) : HTTP URI**
2. **자원에 대한 행위(Verb) : HTTP Method**
3. **자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load**

#### REST의 특징

1. Server-Client(서버-클라이언트 구조)
2. Stateless(무상태)
3. Cacheable(캐시 처리 가능)
4. Layered System(계층화)
5. Uniform Interface(인터페이스 일관성)

#### REST의 장단점

장점 

- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해 준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

단점 

- 표준이 자체가 존재하지 않아 정의가 필요하다.
- HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 정보의 값을 처리해야 하므로 전문성이 요구된다.
- 구형 브라우저에서 호환이 되지 않아 지원해주지 못하는 동작이 많다.(익스폴로어)

### REST API란?

****RESPT API란 REST의 원리를 따르는 API를 의미합니다.****

****하지만 REST API를 올바르게 설계하기 위해서는 지켜야 하는 몇가지 규칙이 있으며 해당 규칙을 알아 보겠습니다.****

### REST API 설계 예시

**1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.**

> Bad Example [http://khj93.com/Running/]
> 
> Good Example[http://khj93.com/run/]

**2. 마지막에 슬래시 (/)를 포함하지 않는다.**

> Bad Example [http://khj93.com/test/]
> 
> Good Example  [http://khj93.com/test]

**3. 언더바 대신 하이폰을 사용한다.**

> Bad Example [http://khj93.com/test_blog]
> 
> Good Example  [http://khj93.com/test-blog]

**4. 파일확장자는 URI에 포함하지 않는다.**

> Bad Example [http://khj93.com/photo.jpg]
> 
> Good Example  [http://khj93.com/photo]

**5. 행위를 포함하지 않는다.**

> Bad Example [http://khj93.com/delete-post/1]
> 
> Good Example  [http://khj93.com/post/1]

### RESTful이란?

RESTFUL이란 REST의 원리를 따르는 시스템을 의미합니다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아닙니다.  REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며

모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있습니다.
