## www.naver.com을 주소창에 입력했을 때 화면이 나타나기까지의 과정과 브라우저 렌더링과정

[![1.png](https://i.postimg.cc/kMHBZ952/1.png)](https://postimg.cc/xqKfJwMQ)

Summary

리다이렉트, 캐싱, DNS, IP 라우팅, TCP연결 구축을 거쳐 요청, 응답이 일어나는 TTFB(Time to First Byte)가 시작되고, 컨텐츠를 다운 받고 브라우저 렌더링 과정을 거쳐 네이버라는 화면이 나타난다.

---


## 리다이렉트
- 서버에서 리다이렉트 설계가 되어 있다면 입력된 주소가 아닌 다른 주소로 이동을 하게 되고, 없다면 그대로 해당 요청에 대한 과정이 진행된다.
- 
---

## 캐싱

- 해당 요청이 캐싱이 가능하지 않은지 파악하고, 캐싱이 된 요청이라면 캐싱된 값을 반환하고, 캐싱이 되지않은 새로운 요청이라면 그 다음 단계로 넘어간다.
- 캐싱은 요청된 값의 결과값을 저장하고 그 값을 다시 요청하면 빠르게 다시 제공하는 기술이다.
- **브라우저캐시**와 **공유캐시**로 나뉜다.
[![3.png](https://i.postimg.cc/qRRvbZVc/3.png)](https://postimg.cc/zLsN37f3)

### 브라우저 캐시

브라우저캐시는 쿠키, 로컬스토리지 등을포함한 캐시로, 개인캐시(private cache)라고도 한다.  브라우저 자체가 사용자가 HTTP를 통해 다운로드하는 모든 문서를 보유하는 것을 말한다. 

### 공유 캐시

공유캐시는 클라이언트와 서버 사이에 있으며, 사용자간에 공유할 수 있는 응답을 저장할 수 있다.

대표적인 예로 요청한 서버 앞단에 프록시서버가 캐싱을 하는 것이 있는데, 이를 리버스 프록시를 둬서 내부서버로 포워드한다고도 말한다.

 AWS의 cloud front, cloudflare 가 많이 쓰인다.

---

## DNS

- DNS(Domain Name System)은 계층적인 도메인 구조와 분산된 데이터베이스를 이용한 시스템으로 **FQDN**을 인터넷 프로토콜인 IP로 바꿔주는 시스템이다. 이는 DNS관련 요청을 네임서버로 전달하고 해당 응답값을 클라이언트에게 전달하는 **리졸버**, 도메인을 IP로 변환하는 **네임서버** 등으로 이루어져 있다.

- FQDN(Fully Qualified Domain Name)이란? 
호스트와 도메인이 합쳐진 완전한 도메인 이름을 말한다. 즉, www등은 호스트 부분이고, naver.com은 도메인이다.

www = host주소 또는 Third lever 도메인, sub 도메인이라고도 부름<br>
naver = second level 도메인<br>
com = top level 도메인<br>

[![4DNS.png](https://i.postimg.cc/CKM807p5/4DNS.png)](https://postimg.cc/4YMybzdR)
도메인은 그림과 같이 계층화가 되어있는데, www가 아닌 루트 도메인부터 시작해서 top level , second level, third lever 이렇게 순차적으로 주소를 찾아 IP주소를 매핑한다.  

---

### DNS캐싱

[![5DNS.png](https://i.postimg.cc/5tPC2zf3/5DNS.png)](https://postimg.cc/f39LHJtt)
미리 해당 도메인이름을 요청했었으면, 로컬 PC에 자동적으로 저장이되는데 브라우저캐싱과 OS캐싱이 있다. 
DNS서버로 요청을 전달하기 전에 캐시를 먼저 확인하고 캐시미스면 요청을 보낸다!
1. 브라우저 캐시 확인
2. OS캐시 확인 - 운영체제 안에 있는 캐쉬로 'systemcall'을 통해 내용에 접근 가능
3. 라우터 캐시 확인(공유기)
4. ISP(Internet Service Provider)캐시 확인
   
ISP 캐시에서까지 IP주소를 못찾았으면, ISP의 DNS 서버에 DNS 쿼리를 보내야한다.

즉, “www.naver.com의 IP주소 알면 알려줘” 라고 여기저기 물어보는것이다. 이를 Recursive search라고 하며 Root domain부터 순서대로 찾는다.

[![6.png](https://i.postimg.cc/sXvZQ2XR/6.png)](https://postimg.cc/vgwmCbfP)

---

## IP 라우팅

- 획득한 IP주소를 기반으로 라우팅, ARP 과정을 거쳐 실제 서버를 찾음

---

## TCP 연결 구축

[![7tcp.png](https://i.postimg.cc/Qdh9gmtm/7tcp.png)](https://postimg.cc/6ybptdC4)
브라우저가 TCP 3way-hand shake 방식으로 연결을 구축한다.

[![8tcp.png](https://i.postimg.cc/s22Mq25Z/8tcp.png)](https://postimg.cc/w1Sxsgf6)

처음에는 클라이언트가 SYN 신호를보내고, 포트 좀 열어달라고 물어보면, 서버가 SYN과 ACK를 보내고, 클라이언트가 내가 보낸 정보 맞는지 확인 후, 서버에게 잘 받았다고 ACK를 보낸다. 이러면 서로 안전하게 정보를 교환 가능한 길이 연결된다.

이러한 TCP 연결을 하는 중, Firewall과 https나 SSL이라는 접근 제한 방법이 있다.

Firewall은 불이 났을 때, 공기를 차단하는 벽처럼, 인터넷에서도 해커가 무자비한 서비스 트래픽을 보내는 경우를 대비해 Firewall을 설치해, 특정 IP주소나 어떤 지역에서 접근해 오는 신호를 차단할 수 있으며, Https/SSL은 클라이언트와 서버와의 암호화를 통해 중간에 누가 패킷을 엿듣는 것을 차단한다.

---

## 콘텐츠 다운로드

- 요청한 컨텐츠를 서버로부터 다운받음

※참고사항※

www.naver.com을 검색창에 친 시점 ~ 요청을 해서 콘텐츠 다운로드를 시작 할 때! ⇒ **TTFB (Time To First Byte)**

---

## 브라우저렌더링

[![9.png](https://i.postimg.cc/JhdsLWQY/9.png)](https://postimg.cc/v1fYrkk5)

HTML 문서를 전달받은 웹 브라우저는 먼저 브라우저 엔진을 이용해 응답 데이터에 악성 코드가 있는지를 검사한다. 악성 코드가 없다면 렌더링 엔진에게 해당 문서를 해석하여 웹 페이지를 화면에 렌더링할 것을 요청한다. 
그러면 렌더링 엔진이 응답받은 문서를 바탕으로 렌더링을 수행하고, 작업이 완료되면 브라우저 엔진이 사용자에게 화면을 보여준다.

















