# 공인IP, 사설IP, NAT

## 공인IP(Public IP, =공용IP)

- 공인 IP주소는 **글로벌 인터넷에서 고유한 주소**를 나타내며 각 기기를 식별하고 통신을 가능하게 한다.
- 전 세계적으로는 ICANN이라는 기관이, 우리 나라는 한국인터넷진흥원(KISA)에서 관리하고 있다.
- 이를 부여 받은 인터넷 서비스 제공 업체(ISP, Internet Service Provider, 우리가 잘 알고 있는 KT, SKT, LG)가 제공하는 IP 주소이며, 전세계적으로 고유한 주소이다.
- 공인 IP주소는 **외부에 공개되어 있어서 다른 PC로부터의 접근이 가능**하다.

## 사설IP(Private IP)

- 공유기 / 라우터 등에 연결 되어있는 일반 가정 또는 회사 등의 기기에 할당된 네트워크의 IP주소이며, 로컬IP, 가상IP라고도 한다.
- 즉, 어떤 네트워크 안에서만 **내부적으로 사용되는 고유한 주소**이다.
- 사설 IP주소는 외부에 공개되어 있지 않아 **NAT방식을 이용하지 않는다면 내부에서만 접근이 가능**하다.

> 사설 IP 주소 대역
> 
> - Class A : 10.0.0.0 ~ 10.255.255.255
>   
> - Class B : 172.16.0.0 ~ 172.31.255.255
>   
> - Class C : 192.168.0.0 ~ 192.168.255.255
>   
<details>
  <summary>고정IP (Static IP)</summary>
  <div markdown="1">
    고정IP는 항상 <b>동일한 IP주소를 가지는 주소</b>로, 변경되지 않는다. 이것은 웹 서버, VPN서버, 네트워크 장비와 같은 항상 동일한 IP주소로 식별 되어야 할 때 사용된다. 공개 서비스 제공에 적합하다.
  </div>
</details>
<details>
  <summary>유동IP (Dynamic IP)</summary>
  <div markdown="1">
    유동IP는 <b>주기적으로 변경될 수 있는 주소</b>이다.<br>
    인터넷 사용자 모두에게 고정IP를 부여해 주기는 힘들기 때문에, 일정한 주기 또는 사용자들이 인터넷에 접속하는 순간마다 사용하고 있지 않은 IP 주소를 임시로 발급해준다. 대부분의 사용자는 유동IP를 사용한다.
  </div>
</details>

### 사설 IP로 IPv4 주소 고갈 문제 해결

- 위에서 언급했듯 사설IP는 어떤 네트워크에서 내부적으로 사용되는 고유한 주소이다.

철수의 노트북이 사용하는 IP는 192.168.0.1이고
영희의 노트북이 사용하는 IP도 192.168.0.1이다.

하지만 각기 다른 공인IP로 구성된 네트워크 안에서 내부적으로만 사용되는 IP이기 때문에 중복 되어도 상관이 없다.

![사설IP](https://github.com/hajaeryul/study-20221010-jaeryul/assets/113097210/c67fc065-eff8-4be5-add8-7d798f1bc979)

## NAT (Network Address Translation)

- 하나의 공인IP 주소에 여러 개의 사설IP주소를 할당 및 매핑하는 주소 변환 방식이다. 다시 말해 **사설IP를 가진 호스트가 외부의 네트워크와 통신**할 수 있도록 네트워크 주소를 변환하는 것이다.
- NAT는 공유기(라우터나 방화벽 디바이스)에서 구현되며, 주로 공개 IP주소 부족 문제를 해결하고 보안을 향상시키는 데 사용된다.
- 1 : 1 translation

> NAT 변환 순서
> 
> 1. 사설 네트워크 → 인터넷 요청 시, 출발지 사설IP를 공인 IP로 전환
>   
> 
> 2. Address Binding : 라우터의 NAT 테이블에 변환 주소 내용을 보존
>   
> 3. Address Lookup and Translation : 응답을 받을 때, 라우터에서 목적지 공인IP를 사설IP로 변환
>   
> 4. Address Unbinding : 일정 시간동안 라우터 NAT 테이블의 해당 엔트리에 패킷이 흐르지 않으면 세션 엔트리를 삭제
>   
<details>
  <summary>Static NAT</summary>
  <div markdown="1">
    하나의 사설IP와 공인IP를 1:1로 매핑
    NAT테이블이 사전에 생성
  </div>
</details>
<details>
  <summary>Dynamic NAT</summary>
  <div markdown="1">
    여러 개의 사설IP와 여러 개의 공인IP를 동적으로 N:M 매핑
    NAT테이블이 NAT 수행 시 생성
  </div>
</details>

## NAPT (Network Address Port Translation)

- NAT의 확장이며, 여러 내부 기기가 동시에 인터넷을 사용할 수 있도록 **포트 번호를 사용하여 내부 기기를 식별**한다.
- 주소 변환뿐만 아니라 포트 번호 변환도 수행하는 주소 변환 기술이다.
- 일반적으로 NAT라 하면 NAPT를 말한다. (실무에서는 PAT 라는 용어로 더 많이 사용)
- N : 1 translation

![PAT](https://github.com/hajaeryul/study-20221010-jaeryul/assets/113097210/e3465ccd-248f-4a60-8231-dd07d1b23a54)

- 호스트들은 고정 포트로 구분된 상태가 아니기 때문에 내부 → 외부 통신은 가능하지만 외부 → 내부 통신은 불가능하다.
  
  즉, 패킷의 요청이 내부에서 외부로 나갔다가 응답이 들어오는 것은 가능하지만, 애초에 외부에서의 요청 패킷이 직접 사설망으로 들어오는것은 불가능하다. 이럴때 사용하는것이 바로 포트 포워딩이다.
  

### 포트 포워딩 (Port Forwarding, =포트 매핑)

- NAT을 수행하는 장치(공유기 등)에서 설정하며 **특정 포트를 Open하고 해당 포트로 들어오는 모든 패킷을 내부의 사설 IP로 전달**해주는 기능이다.

---

### 문제. 컴퓨터 네트워킹에서 쓰이는 용어로, IP패킷의 TCP/UDP 포트 숫자와 소스 및 목적지의 IP 주소 등을 재기록하면서 라우터를 통해 네트워크 트래픽을 주고 받는 기술로 네트워크 주소 변환이라고 한다.

[정보 처리 기사 실기 2020년 기출 문제]

<details>
  <summary>정답</summary>
  <div markdown="1">
    NAT
  </div>
</details>
