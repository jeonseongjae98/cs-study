## 전송계층 리마인드

![00](https://github.com/NoRuTnT/practice/assets/114069644/0fe611ae-7206-446b-8732-6dd86c25589c)  
**연결형 통신**  
신뢰할 수 있고 정확한 데이터를 목적지에 문제 없이 전달하는 통신  
신뢰성/정확성을 위해 여러 번 확인하고 데이터를 보낸다.  

**비연결형 통신**  
데이터를 빠르고 효율적으로 전달하는 통신  
효율성을 위해 확인 절차 없이 일방적으로 데이터를 보낸다.  

#### TCP(Transmission Control Protocol)
![11](https://github.com/NoRuTnT/practice/assets/114069644/54537998-cf55-4668-baed-c754ac22853d)  

전송 계층에서 신뢰할 수 있는 정확한 통신을 제공하는, 신뢰성/정확성이 우선인 연결형 통신 프로토콜  

## TCP 연결수립과정  
TCP를 이용한 데이터 통신을 할 때 프로세스와 프로세스를 연결하기위해 가장 먼저 수행되는 과정  
ex)파일 전송, 게임 등등  
1. 클라이언트가 서버에게 요청 패킷을 보내고
2. 서버가 클라이언트의 요청을 받아들이는 패킷을 보내고
3. 클라이언트는 이를 최종적으로 수락하는 패킷을 보낸다.

**위의 3개의 과정을 3Way Handshake라고 부른다.**   

## 과정설명
1. 서버에 패킷을 만들어서 보낸다 (ipv4캡슐화, 이더넷 캡슐화)  

![image](https://github.com/NoRuTnT/practice/assets/114069644/76ac8900-b279-40a0-b832-0897afc9c018)  

2. flag코드는 syn:1 seqnum은 100(무작위) acknum은0(없음)  

![image](https://github.com/NoRuTnT/practice/assets/114069644/ad0fe81e-88cd-4f10-9a48-e9f9cfcbf494)  


3. 서버는 캡슐화풀고 목적을 확인한뒤 응답패킷을 클라이언트에게 보냄(발신지포트주소,목적지포트주소 변경)  

![image](https://github.com/NoRuTnT/practice/assets/114069644/72bc47de-d8ba-420d-8acd-8aeee834a46f)  

 

4. flag코드는 syn:1 ack:1 seqnum은 2000(무작위) acknum은101(받은 패킷의 seqnum에 +1을 해줌) : 클라이언트와 서버 둘이 seqnum,acknum을 이용해 동기화 하는 과정 

![image](https://github.com/NoRuTnT/practice/assets/114069644/6211d88b-dc6e-445d-beea-19f47061e1cb)  


5. 연결응답을 확인하고 syn에대한 응답패킷을 다시보냄
   
![image](https://github.com/NoRuTnT/practice/assets/114069644/3f7e96c9-a80e-4fea-a3c7-0441ea99b312)  


6. flag코드는 ack:1 seqnum은 101(받은패킷의 acknum을 그대로사용) acknum은2001(받은 패킷의 seqnum에 +1을 해줌)  

![image](https://github.com/NoRuTnT/practice/assets/114069644/5e2132e5-89a5-4487-924e-38c3eb41e9d1)   

## 3Way Handshake중 서버상태
![22](https://github.com/NoRuTnT/practice/assets/114069644/64838d57-4620-4c81-bf94-70fe943921ec)  
![image](https://github.com/NoRuTnT/practice/assets/114069644/7818d9d3-d0dd-440d-869d-234c15dd8e5c)  
1. 서버에서는 서비스를 제공하기 위해 클라이언트의 접속을 받아들일 수 있는 LISTEN 상태로 대기합니다.  
2. 클라이언트에서 통신을 시도할 때 SYN 패킷을 보내는데, 클라이언트에서는 이 상태를 SYN-SENT라고 부릅니다.    
3. 클라이언트의 SYN을 받은 서버는 SYN-RECEIVE 상태가 되고, SYN-ACK로 응답합니다.  
4. SYN-ACK 응답을 받은 클라이언트는 ESTABLISHED 상태로 변경되고, 그에 대한 응답을 서버로 다시 보냅니다.  
5. 서버에서도 클라이언트의 이 응답을 받고 ESTABLISHED상태로 변경됩니다.  
6. 여기서 ESTABLISHED상태는 서버와 클라이언트 간의 연결이 성공적으로 완료되었음을 나타냅니다.

## 3Way Handshake를 이용해 서버를 공격하는방법
1. SYN Flooding
3way handshaking 과정중 서버는 2단계 에서 (클라이언트로 부터 요청을받고 응답을 하고난후 다시 클라이언트의 응답을 기다리는 상태)  
연결을 메모리 공간인 백로그큐(Backlog  Queue) 에 저장을 하고 클라이언트의 응답(ack)  3단계를 기다리게 된다.  
일정 시간 (default 로 UNIX/LINUX : 60초 , Windows : 256초 , Apache : 300 초이며 수정 가능) 동안 응답이 안오면 연결을 초기화한다.  
이점을 이용한 공격법이 SYN Flooding이다.
악의적인 공격자가 실제로 존재하지 않는 클라이언트IP로 응답이 없는 연결을 초기화 하기전에 또 새로운 연결 즉 1단계 요청만 무수히 많이 보내어 백로그 큐를 포화 상태로 만들어 다른 사용자로 부터 더이상에 연결 요청을 못 받게 하는 공격 방법이다.

**SYN Flooding 대응방법**  
대응책으로는 연결 타이머 시간을 짧게 하거나 백로그 큐 사이즈를 늘리는법,   
정해진 시간동안 들어오는 연결 요구의 수를 제한하는법, 쿠키(cookie)라는 것을 이용해서 전체 연결이 설정되기 전까지는 자원의 할당을 연기하는 법이 있다.  


2. 세션하이재킹  
위에서 알아본바와 같이 동기화상태는 클라이언트의 seq와 서버가가지고있는 클라이언트의 seq가 같고 서버의 seq가 클라이언트가가지고있는 서버의 seq와 같아야한다.  
Client_My_Seq=Server_Client_Seq  
Server_My_Seq=Client_Server_Seq  
TCP 3Way HandShake은 서버/클라이언트의 상호 세션 연결 과정에서 발생하는 시퀀스 넘버를 가로채 이를 이용해 공격자가 정상적인 클라이언트라고 위장한 후 연결을 시도하는 것이 세션하이재킹이다.  
