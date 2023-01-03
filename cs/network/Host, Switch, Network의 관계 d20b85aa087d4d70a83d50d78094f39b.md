# Host, Switch, Network의 관계

Created Time: January 3, 2023 5:11 PM

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/df230d41-a15f-4642-8a6e-a92acc735a61/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230103T191218Z&X-Amz-Expires=86400&X-Amz-Signature=0226c8975216a0ed4588396001996bd27c22f0ca8fb040dd7c8585c8b5a7fa2d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

`Host`: 네트워크에 연결된 컴퓨터

Host는 크게 `Network 이용주체`, `Network 자체를 이루는 것`이냐로 분리를 하는데

- Host가 Network 자체를 이루는 것 이를 **`Switch`**라고 한다.
    - 대표적으로 `Router` (경로 찾기 위한 스위치), Fire wall, IPS (오른쪽 두 가지는 보안 스위치)
    - 위처럼 역할에 따라 나뉜다.
- Host가 Network 이용주체이면 이를 `End-Point`라고 부른다.
    - 대표적으로 Peer, Server, Client
        - 종단점으로 그냥 존재하면 Peer라 한다.
    - 위처럼 네트워크에서 Host가 존재하는 역할에 따라 나눠진다.

네트워크 중 가장 유명한 네트워크는 `인터넷`이다.(인터넷은 Router의 거대한 집합체로도 볼 수 있다.)

`인터넷`을 이루고 있는 중요한 구성요소 2가지를 고르면 `Router`와 `DNS`가 있다.

다르게 생각하면 Router와 DNS의 집합체를 인터넷으로도 볼 수 있다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6db25887-8c08-4a7c-81d7-4a06a05cd08d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230103T191241Z&X-Amz-Expires=86400&X-Amz-Signature=441b111359020df5a295b5cd55f4b169bf05d1d7c96acebb39072f600180492d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

레이어가 높을수록 연산이 복잡 가격이 비쌈

TCP/IP 는 계층이 달라서 / 가 붙는다.

흔히 이용하는 공유기는 스위치인가?

우선 스위치는 맞다고 생각한다. 그럼 어떤 스위치냐면 L4일 듯 하다.

현대 공유기는 보통 Host 설정을 위해 DHCP(Dynamic Host Configuration Protocol) 기능이 탑재가 된 것으로 안다.(따로 별도 서버에 DHCP 서비스 설정후 라우터는 게이트웨이 역할만 수행하게도 가능)

DHCP는 UDP 기반 프로토콜이며 서버가 네트워크 클라이언트에게 IP 주소를 실시간으로 부여할 수 있도록 하였다.

사용가능한 주소를 자동으로 확인하고 클라이언트에게 IP 주소를 부여한다.

DHCP는 UDP 67(Server) 번과 68(Client) 번을 사용한다.

DHCP 동작과정 중 DHCP Discover만 봐도 IP와 포트번호(UDP 67, UDP 68)를 이용하는 것을 보아 L4까지 이용하는 것을 볼 수 있다.

### **1) DHCP Discover**

Client가 Server를 찾기 위한 메시지이다. (출발지 포트: 68번 / 목적지 포트: 67번)

Broadcast 방식으로 전송한다. (출발지 IP: 0.0.0.0 / 목적지 IP: 255.255.255.255)

Broadcast를 송신하면 DHCP 서버를 제외한 다른 장비들은 패킷을 수신하지 않는다.

![https://blog.kakaocdn.net/dn/ElZ3U/btqzaRX2PKW/TkeRBjEF1XPIV2kLbbO2p1/img.png](https://blog.kakaocdn.net/dn/ElZ3U/btqzaRX2PKW/TkeRBjEF1XPIV2kLbbO2p1/img.png)

DHCP Discover packet

이를 통해 UDP를 이용하는 것도 알 수 있어 해당 장비는 최소 L4 스위치일 것으로 예상 된다.

공유기에서 사설IP를 개인 PC or 모바일에게 할당한다. 

 

참조: [https://peemangit.tistory.com/355](https://peemangit.tistory.com/355), [https://namu.wiki/w/DHCP](https://namu.wiki/w/DHCP)