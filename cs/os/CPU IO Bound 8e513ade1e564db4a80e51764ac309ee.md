# CPU | IO Bound

Created Time: October 14, 2022 11:27 PM
Status: ✅ Completed

## CPU (Central Processing Unit)

프로세스의 명령어를 해석하고 실행하는 장치

## IO(Input/Output)

파일을 읽고 쓰거나, 네트워크의 어딘가와 데이터를 주고 받는 것

입출력 장치와 데이터를 주거나 받는 것

## 버스트(Burst)

어떤 현상이 짧은 시간 안에 집중적으로 일어나는 일

## CPU 버스트

임의의 프로세스가 CPU에서 한번에 연속적으로 실행되는 시간

메모리에 올라가있는 프로세스가 자기 차례가 되서 CPU에서 실행됐을 때 자신의 명령어들이 CPU에서 연속적으로 실행되는 시간

## IO 버스트

프로세스가 IO 작업을 요청하고 그 결과를 기다리는 시간

### 프로세스의 인생은 CPU 버스트와 IO 버스트의 연속

## CPU 버스트 길이에 따른 빈도


![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/12d75dca-e7f7-4f55-9ba3-8cf5f51cd7b3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221114%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221114T142517Z&X-Amz-Expires=86400&X-Amz-Signature=8a91a39ea02431d87291369af17c628b1b68374a4323e88d1a589aeeec00bc8b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

버스트의 지속시간에 따른 빈도 수가 0~8ms에 끝나는 것을 볼 수 있다.

보통의 프로세스는 CPU 작업을 한번 수행할 때 길게하지 않고 짧게 끝난다는 것을 볼 수 있다.

## CPU bound 프로세스

CPU burst가 많은 프로세스

예) 동영상 편집 프로그램, 머신러닝 프로그램

IO작업이 거의 없고 그냥 연산 작업이 많음

(머신러닝은 CPU 코어도 부족해 GPU 코어도 이용)

## IO bound  프로세스

IO burst가 많은 프로세스

(일반적인) 백엔드 API 서버

보통의 API 서버들은 HTTP Req 받으면 DB, 캐시 서버에 요청하여 그 데이터를 받아 적당한 형태로 가공하여 HTTP Res 하는 것이 일반적이다.

이때 DB, 캐시 서버에 요청하는 것이 IO 작업이다.

IO 작업은 네트워크를 타고 진행되는 것이므로 CPU에서 명령어가 여러 번 처리되는 것보다 느리다.

## CPU와 쓰레드 수의 적정선이 어디인가?

### CPU Bound 프로그램의 쓰레드 수

> 듀얼 코어 CPU에서 동작할 CPU bound 프로그램을 구현한다면 몇 개의 쓰레드를 쓰는 것이 좋을까?
> 

> Goetz(2002, 2006) recommends

CPU bound 프로그램에서 적절한 쓰레드 수는 CPU(코어) 수의 +1
> 

어찌됐던 쓰레드가 여러 개이면 Context Switching이 일어나기에 해당 코어 수 아님 코어수 +1 정도가 적절하다고 얘기한다.(CPU bound 프로그램이기에)

### IO Bound 프로그램의 쓰레드

여러 상황에 맞춰서 적절한 쓰레드 수를 찾아야한다..

**만약 API 서버가 Thread per Request 방식이면?**

(API 요청이 있을 때마다 전담 쓰레드들이 맡아서 처리하는 방식)

해당 방식이면은 API 서버에 미리 쓰레드들을 여러 개 만들어 놓고, 아직 일이 없는 쓰레드가 요청을 맡아서 처리를 한다.

이때 몇개의 쓰레드들을 미리 만들어 놓아야 하는지 여러 상황을 고려해서 결정하는 것이 필요!

ex) API 서버 하드웨어 스펙, IO Burst 버스트 비중, 예상되는 트래픽 비중 등
