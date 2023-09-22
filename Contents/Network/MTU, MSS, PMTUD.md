# TCP / IP 4계층 MTU, MSS, PMTUD
## MTU
- 데이터 송수신 시 패킷이 쪼개지면서 데이터를 송수신하며, 이 때 패킷은 MTU(Maximum Transmission Unit)를 기반으로 쪼개진다.
- MTU 는 네트워크 통신시 가장 큰 PDU 의 크기를 말한다.
> 즉, 네트워킹에서 **MTU(Maximum Transmission Unit)** 란 네트워크에 연결된 장치가 받아들일 수 있는 최대 데이터 패킷 크기를 말합니다. 지하도로나 터널의 높이 제한처럼 생각할 수 있습니다. 높이 제한보다 높은 차량은 이를 통과하지 못하는 것처럼 네트워크의 MTU보다 큰 패킷은 해당 네트워크를 통과하지 못합니다.
하지만 차량과는 달리 MTU보다 큰 데이터 패킷은 작은 조각으로 잘라 MTU에 맞출 수 있습니다. 이 과정을 분할이라고 합니다. 분할된 패킷은 목적지에 도착하면 다시 조립됩니다.
MTU의 단위는 바이트입니다. "바이트"는 8개 비트의 정보(즉, 8개의 0과 1)를 의미합니다. 최대 MTU 크기는 **1,500바이트**입니다.
- L2 계층(프레임)에서 전달 받을 수 있는 L3 계층(패킷)의 최대 사이즈
- L3 계층(패킷)이 설정된 MTU 사이즈보다 클 경우 IP 단편화가 이루어져 전송 속도에 영향을 줄 수 있음
- L2 계층(프레임)은 Ethernet 헤더(14byte), 데이터(L3(패킷, MTU, 1500byte)), Ethernet 꼬리(4byte)를 포함하여 1518byte로 구성</br>
    [![1.png](https://i.postimg.cc/G2Z5Tynb/1.png)](https://postimg.cc/r0NJvzpH)</br>
- 하지만 패킷이 분리되지 않는 경우도 존재 한다!
- 이 경우 MTU 를 초과하여 분할할 수 없는 경우 아예 전달하지 않을 수도 있다!
- IPv6 는 분할을 허용하지 않고 IPv4 는 헤더에 flags 라는 필드가 존재하여 bit 가 1이되면 "Dont Fragment" 가 활성화되면서 분할이 불가능해진다.
    - 여기서 잠깐💡 IPv4와 IPv6? </br>
        - IPv4란 'Internet Protocol Version 4'라는 의미입니다. 말 그대로 인터넷 프로토콜의 4번째 판이며, 전세계적으로 사용된 1번째 인터넷 프로토콜입니다. 주소는 32비트로 구성되어 있으며 마침표로 구분되는 4개의 8비트 필드로 구분된 십진수로 작성됩니다. '점으로 구분된 십진수 형식'이라고도하며 아래의 이미지가 IPv4 주소의 예시 이미지입니다.</br>
        [![1.png](https://i.postimg.cc/c4V3GzJ6/1.png)](https://postimg.cc/dLj384rK)</br>
        현재 인터넷에서 사용되어지고 있는 표준 프로토콜은 IPv4입니다.

        - IPv6는 IPv4와 마찬가지로 'Internet Protocol Version 6'라는 의미입니다. IPv4가 32비트라는 제한된 주소 공간 및 국가별 할당된 주소가 거의 소진되고 있다는 한계점으로 인해 문제가 예상되는데 그 대안으로 IPv6 프로토콜이 제안되었습니다. 128비트의 무제한 인터넷 프로토콜 주소를 말하며 16비트 단위(0~ffff 범위)로 구분짓고 콜론(:)으로 구분 표시를 합니다. 주소 표기시 기억할 점은 맨 앞의 0은 생략될 수 있으며 연속되는 0의 경우는 콜론 2개(::)로 표현할 수 있다는 것입니다.</br>
        [![2.png](https://i.postimg.cc/C59RYZS9/2.png)](https://postimg.cc/RJQSLZ3T)</br>
        - IPv4와의 가장 큰 차이점은 IP 주소 길이가 128 비트로 늘어났다는 점입니다. 급진하는 네트워크 디바이스들의 인터넷 사용을 대비한 것이죠. 이 외에도 아래와 같은 장점들이 있습니다.

        1. 확대된 주소 공간 : 주소 길이가 128비트로 증가

        2. 단순해진 헤더 포맷 : IPv4 헤더의 불필요한 필드를 제거하여 보다 빠른 처리 가능

        3. 간편해진 주소 설정 : IPv6 프로토콜에 내장된 주소를 자동 설정 기능을 이용하여 플러그 앤플레이 설치가 가능

         4. 강화된 보안 기능 : IPv6에서는 IPSec 기능을 기본 사항으로 제공

        5. 개선된 모바일 IP : IPv6 헤더에서 이동성 지원
- PC에서도 설정된 MTU 확인 가능!!!
    [![1.png](https://i.postimg.cc/zvcN2kMK/1.png)](https://postimg.cc/MfVgv1zp)


## TCP MSS(Maximum Segement Size)
- L4(세그먼트)에서 전달 받을 수 있는 L5~L7계층(메세지)의 최대 길이
- TCP 헤더에 따라 사이즈가 달라질 수 있지만 TCP 헤더에 option이 추가 설정되지 않았다면 기본 1460byte</br>
(TCP 헤더의 option은 최대 40byte까지 추가 될 수 있음)
- **MSS ( Maximum Segment Size )** 는 TCP 에서 사용할 수 있는 데이터의 크기이자 TCP 헤더, IP 헤더를 뺀 크기를 말한다(예를 들어 터널의 높이 제한)
- 통신을 하는 양쪽 끝은 두 장치의 MTU 만이 아니라 중간의 모든 라우터, 스위치, 서버를 고려하며 네트워크 경로상에 있는 아무 장치나 MTU 보다 패킷이 크면 분할될 수 있다. </br>
[![1.png](https://i.postimg.cc/rpfqtcJf/1.png)](https://postimg.cc/WDqBQBxZ)

## PMTUD(Path MTU Discovery)
- PMTUD(Path MTU Discovery)는 수신자와 송신자의 경로 상에서 장치가 패킷을 누락한 경우 테스트 패킷의 크기를 낮추면서 MTU에 맞게 반복해 보내는 과정 </br>
[![1.png](https://i.postimg.cc/bJGPZwTp/1.png)](https://postimg.cc/xJSh7Yh4)
