# IP주소, MAC주소, ARP, RARP

## IP 주소 (Internet Protocol Address)

- IP주소는 컴퓨터 또는 장치가 인터넷에서 식별 되는 주소이다.
- OSI 7계층에서 3계층인 네트워크 계층에서 작동하며 전 시간에 학습한 라우팅 및 네트워크 통신에서 중요한 역할을 한다.
- IPv4와 IPv6가 있으며, IPv4는 네 개의 8비트 숫자로 표현되고(32bit), IPv6 는 128bit 숫자로 표현된다.
- IP주소의 자세한 내용에 대해서는 다음 다섯 발표자가 자세히 설명해 줄 것이다.
- **IP주소간의 통신은 사실, 각 라우터 hop에서 일어나는 MAC주소와 MAC주소 통신의 연속적인 과정이다.**

## MAC 주소 (Media Access Address)

- MAC주소는 NIC(Netword Interface card) 즉, 랜 카드에 할당되며 하나밖에 존재하지 않는 **고유한 하드웨어 주소**이다. 물리적 주소(Physical Address), 이더넷 주소(Ethernet Address), BIA(Burned-In Address)라고 불리기도 한다
- OSI 7계층에서 2계층인 **데이터링크 계층**에서 작동한다.

![맥주소](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/d77acbe7-ec69-455b-a85f-cb1e15d66749)

- 48bit로 구성되어 있고, 16진수로 표기한다.
- 8자리마다 하이픈(-)이나 콜론(:), 점(.) 으로 구분되어진다.
- 상위 24bit는 OUI (Organizational Unique Identifier)라는 IEEE에서 할당 받은 제조업체 코드이며, 하위 24bit는 제조업체에서 기기를 구분하기 위한 고유 시리얼 넘버이다.

*그럼 IP주소와 MAC주소를 가지고 어떻게 통신을 한다는 거지?*

**실질적으로** **통신은 MAC 주소를 기반으로 이루어지며**, IP 주소는 논리적인 주소로, 상위 수준에서 주소 지정 및 라우팅을 처리하는 역할을 한다.

*하지만 난 목적지의 IP주소밖에 모르는데..?*

→ IP주소를 MAC주소로 변환하는 프로토콜 : **ARP**

## ARP (Address Resolution Protocol)

- **IP주소를 MAC주소와 매칭시키기 위한 프로토콜**이며 LAN(Layer 2)에서 목적지를 제대로 찾아갈 수 있도록 돕는다.
- IP주소와 MAC주소를 일대일 대응하여 테이블로 정리하는데 이를 **ARP Table또는 ARP cache**라 부른다.

### ARP 동작 방식 - 같은 LAN에 있는 호스트

Host A는 목적지인 B에게 데이터를 전송하고 싶지만, B는 최근 LAN에 추가되어 A의 ARP Table에는 B에 대한 MAC 주소가 없다.

1. A는 B의 IP주소 (192.168.30.6) 가 포함된 ARP 쿼리 패킷을 생성하여 LAN 상에 속한 모든 노드로 broad cast 한다.
  
  - A는 목적지 MAC 주소를 FF-FF-FF-FF-FF-FF 으로 설정
    
  - 같은 LAN에 있는 모든 노드는 ARP 쿼리를 받음
    

    ![같은LAN통신1](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/9189257a-2aaf-4c37-9f53-54d301b69bef)

2. IP주소가 192.168.30.6인 B는 자신의 IP주소를 목적지로 하는 것을 확인하고 Host A에게 자신의 MAC 주소를 담은 응답 패킷을 보낸다.
  
  - 응답 패킷은 A의 MAC 주소를 목적지로 한다.
    
  
  ![같은LAN통신2](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/7f9326f4-d3ac-4020-b7a6-9d16bf610ef8)
  
3. MAC 주소를 알아낸 Host A는 ARP Table에 B의 MAC 주소를 업데이트 한다.
  

### ARP동작 방식 - 다른 네트워크에 있는 호스트

1. A에서 생성된 ICMP 패킷은 네트워크 계층에서 자신의 IP주소, 상대방의 IP주소가 함께 캡슐화되어 데이터 링크 계층으로 이동
  

    ![외부네트워크통신1](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/3d2727ce-46c8-4a4e-acac-54d196272c8a)

2. 데이터 링크 계층에서는 상대방과 대역이 다르기 때문에 게이트웨이에 보내게 되는데, 게이트웨이의 MAC주소를 모른다면 게이트웨이의 MAC주소를 알아내기 위해 목적지 MAC주소를 FF:FF:FF:FF:FF:FF로 지정한 ARP request 패킷을 보낸다.
  

       ![외부네트워크통신2](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/eb938331-58b1-46b8-9bcd-0f80e0a8fda1)

3. 라우터는 브로드캐스트 된 ARP request를 받고 자신의 MAC 주소를 출발지 MAC 주소로 한 ARP reply를 보낸다.
  
  ![외부네트워크통신3](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/d04f025e-182c-4806-a0ef-37e0abdfaa28)
  
4. 게이트웨이 MAC주소를 알아낸 A는 ARP Table에 게이트웨이 IP주소와 MAC주소를 매핑한 뒤, ICMP 패킷의 MAC주소를 게이트웨이 MAC주소로 하고 다시 패킷을 보낸다.
  
  ![외부네트워크통신4](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/76b1efb0-92c4-4b98-b619-bedd2b5be24d)
  
5. ICMP 패킷을 받은 라우터는 역 캡슐화를 통해 목적지 IP주소를 확인한다. 확인 결과 목적지가 192.167.1.11인것을 확인하고 해당 MAC주소가 ARP테이블에 없으면 목적지 MAC주소를 FF:FF:FF:FF:FF:FF로 지정한 ARP request를 네트워크에 보낸다.
  
  ![외부네트워크통신5](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/1b531e7a-7df7-4698-b22e-8d4367badad1)
  
6. 브로드캐스트를 통해 B가 자신이 목적지 IP주소인 ARP request 패킷을 역 캡슐화 후, 확인하여 출발지 MAC주소가 B인 ARP reply 패킷을 게이트웨이에 보낸다.
  
  ![외부네트워크통신6](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/679e6316-ee13-47af-85b9-7ea3e006bd25)
  
7. B의 MAC주소를 ARP Table에 기록 후 받았던 ICMP의 패킷의 출발지 MAC주소를 R_2로 설정하고, 목적지 MAC주소를 B로 설정하여 보낸다.
  
  ![외부네트워크통신7](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/4ada08f5-92e2-4db0-960f-2f905429e70e)
  
8. ICMP를 받은 호스트 B는 목적지 주소가 자신인 것을 확인하고 그에 대한 응답을 보내는데, ARP Table을 참조해 게이트웨이 MAC주소를 목적지 MAC주소로 하여 패킷을 전송한다.
  
  ![외부네트워크통신8](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/fc2d15cb-6b8a-4158-8c9a-6f4770f1d07d)
  
9. IMCP reply를 전달 받은 라우터는 A에게 전달한다. (호스트 B→ 라우터 → 호스트A)
  
  ![외부네트워크통신9](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/60fce433-ac3f-40fc-9b28-a9cc5d1fc801)
  

## RARP (Reverse Address Resolution Protocol)

- ARP 와는 반대로 해당 MAC주소에 맞는 IP값을 알아오는 프로토콜이다.
- 하드디스크가 없는 터미널의 경우 초기 가동될 때 자신의 MAC주소를 담아 RARP 요청을 만들어 자신의 IP주소 정보를 받아올 때 사용한다.

## ARP 스푸핑 (ARP Spoofing)

- 혹은 ARP Cache Poisoning 이라고 한다. 공격자는 두 호스트의 통신을 감시하기 위해 두 호스트의 ARP Cache를 변경하는 공격 방법이다. 공격자는 아래 그림처럼 지속적으로 ARP 응답을 보낸다.
  
  ![ARP스푸핑1](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/115fcb7a-a9f3-4f6e-bc13-889fe88025ae)
  
- 동적으로 ARP 정보가 등록되어 있다면 1~2분이 지나면 삭제되는 것을 이용한 공격 방법이다.
  
- 공격자는 정상적인 ARP Cache를 가지고 있다.
  
  ![ARP스푸핑2](https://github.com/hajaeryul/mvc-20220927-jaeryul/assets/113097210/a62b0e00-c8df-42d6-9063-fa49a794a7d4)
  
- A는 B에게 데이터를 전송하고 싶지만, 공격자가 ARP 응답을 보냈기 때문에 A는 공격자의 MAC주소를 목적지로 하여 데이터를 전송한다.
  
- 정적 ARP cache를 구성하면 시스템 종료시까지 저장되기 때문에 대응할 수 있다.
  

## 스위치 재밍(Switch Jamming)

- 혹은 MAC Flooding 이라고 한다.
- 많은 양의 MAC 주소(=프레임 패킷)를 스위치에게 보내 스위치의 MAC Table 버퍼를 Overflow 시킨다.
- 스위치는 자신에게 들어오는 모든 패킷을 MAC Table에 저장시켜 놓기 때문에 스위치가 허브처럼 동작하게 된다.

---

### 문제1. IP호스트가 자신의 물리 네트워크 주소(MAC)는 알지만 IP 주소를 모를 경우, 서버로부터 IP주소를 요청하기 위한 프로토콜은 무엇인가?

[정보 처리 기사 실기 2021년 1회 기출 문제]

### 문제 2. 다음은 스푸핑 공격에 대한 설명이다. 괄호 안에 들어갈 알맞은 답안을 작성하시오.

[정보 처리 기사 실기 2021년 3회 기출 문제]

( ) 스푸핑은 근거리 통신망 하에서 ( ) 메시지를 이용하여 상대방의 데이터 패킷을 중간에서 가로채는 중간자 공격 기법이다. 이 공격은 데이터 링크 상의 프로토콜인 ( )를 이용하기 때문에 근거리상의 통신에서만 사용할 수 있는 공격이다.

### 문제 3. 위조된 매체 접근 제어(MAC) 주소를 지속적으로 네트워크로 흘려보내, 스위치 MAC 주소 테이블의 저장 기능을 혼란시켜 더미 허브(Dummy Hub)처럼 작동하게 하는 공격은?

① Parsing ② LAN Tapping
③ Switch Jamming ④ FTP Flooding
