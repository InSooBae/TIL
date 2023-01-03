# Network preview

Created Time: January 3, 2023 3:22 PM
Status: ✅ Completed

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f9960df9-0449-4546-8256-cafe1e1f8c85/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230103T081230Z&X-Amz-Expires=86400&X-Amz-Signature=eb8ce6a414e31dc1a0b56d8505d4b042323388e76a48e6b1ece761c00826947d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

위 그림을 보면 대략적으로 이렇다.

> OSI 7 Layer | DOD(Department Of Defence) | TCP/IP
> 

여기서 OSI 7 Layer | DOD(Department Of Defence) 이 두 개는 Abstract와 같다.

말 그대로 개념이라는 뜻이다. 자바에서 인터페이스처럼 말이다.

그럼 TCP/IP 뭐냐? 이건 구현체이다. OSI 7 Layer | DOD(Department Of Defence)의 개념들을 구현을 한 것이다.

(여기서 인터페이스는 DOD 기준으로 생각)

Application을 구현한 **Process.** 예를 들면 jar 파일을 실행했다라고 생각해도 편할 것 같다.

Transport + Network Layer는 **TCP/IP**로 구현을 한 것이다.

Access Layer는 네트워크 랜카드와 같은 **NIC(Network Interface Card)**로 구현된 것이다.

그리고 S/W단에서 **NIC**(H/W)를 **컨트롤**하기 위해 **Device Driver**가 존재한다.

또한 **Kernel의 구성요소**들을 **User mode**에서 application이 **이용**하기 위해 **File** 형태로 **추상화**를 한다.

어떤 프로세스가 어떤 커널 요소(프로토콜의[가령 네트워크에 관련 됐다고 가정하자])를 추상화 한 것은 **File**이라 하지 않고 **Socket**이라고 한다.

TCP/IP Socket이라고 하면 TCP를 User mode의 프로세스가 접근할 수 있도록 파일 형식의 추상화한 인터페이스를 소켓이라 한다.

※ HTTP는 L7 계층의 속한다.

그리고 식별자가 존재하는데,

Access에선 MAC 주소

Network 에선 IP 주소(v4, v6)

Transport에선 Port 번호

위 3개가 식별자 이다.

- MAC 주소는 NIC(랜 카드)의 대한 식별자이다.

> LAN카드는 유/무선으로 나뉜다.
예를 들면 노트북같은 경우 NIC이 2개(유선 랜, 무선 랜)가 있다.
그러면 MAC 주소는 2개가 있는 것이다.

MAC 주소는 H/W 주소라고도 한다.
MAC 주소는 H/W이라도 변경할 수 있다.
> 

- IP 주소는 Host의 대한 식별자이다.

> Host: 인터넷에 연결된 컴퓨터
그러면 한 컴퓨터에 IP 주소는 몇개나 있을수 있을까?

N개이다.
예를 들면 한 컴퓨터가 유선 랜카드 하나만 있다고 가정하자.
NIC이 하나면 IP 주소가 하나라고 생각할 수 있는데 그것이 아니다.

IP 주소는 NIC 하나의 여러개를 바인딩할 수 있다.
> 
> 
> ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aabe362f-59ec-4b2d-a77b-785550c7c9f1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230103T081304Z&X-Amz-Expires=86400&X-Amz-Signature=6bfa80cd598e29f2c044b25236d7acafe93bb3ee4e13f4d6c321c35001957a01&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
> 
> 결론은 한 컴퓨터는 여러 개의 IP 주소를 가질 수 있다.
> 

- 포트번호는 업무에 따라 다르다.

> 소속된 업무가 user mode인 software를 개발 및 관리하는 사람에게 물어보면 **프로세스 식별자**?라고 할 수 있다.

다음은 업무가 kernel mode인 네트워크 관리자에게는 4계층에 주로 속한다.
이분들에게 포트번호를 물어보면 **서비스**라고 한다.
예를 들면 HTTP → 보통 TCP 80 번을 사용한다. 그런데 8080도 이용할 수 있다.
이렇다 보니 80번 열어주세요보다 **HTTP 서비스**를 열어달라고 한다.

S/W가 아닌 H/W에서 처리하는 부분도 있다. 예를 들면 케이블 설치 및 통신 공사분들이다.
이분들에게 포트번호를 물어보면 인터페이스 번호라고 한다.
예를 들면 공유기에 보면 랜 케이블을 꽂을 수 있을 것이다. 이때 그 단자의 번호를 얘기한다.

결론은 포트번호는 여러가지 형태로 식별의 대상이 달라질 수 있다는 것이다.
>