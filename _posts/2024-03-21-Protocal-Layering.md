---
layout: single
title:  "1.2 Protocol Layering"
categories: Computer_Network
tag: [Protocol_Layering, TCP/IP]
toc: true
author_profile: false
---

# Protocol
Protocol - defines the rule both the sender and receiver.

데이터 통신을 원활하게 하기 위한 통신 규약.

There are 5 layers in TCP/IP protocol

## Protocol Layering

1. Application Layer (Layer 5)
   
   * To communicate, a process send a requst to the other process and receives a response
  
   * Process-toProcess communication is the duty of the Application Layer

2. Transport Layer (Layer 4)
   
   * giving servies to the application layer
    
   * get a message from an application program and deliver it to the corresponding application

3. Network Layer (Layer 3)

   * responsible for creating a connection between the source computer and destination computer

   * the communication at the network layer is host-to-host

4. Data-link Layer (Layer 2)

   * routers are responsible for chossing the best link

5. Physical Later (Layer 1)

   * carrying indiciduals bits in a frame across the link
   


|Layer|name|설명|
|---|---|---|
|Layer 5|Application|서비스 제공<br>HTTP,FTP,SMTP,DNS등 프로토콜 동작<br>데이터 형식, 암호화 압축등 정의|
|Layer 4|Transport|End-toEnd 데이터 전송 관리<br>TCP와 UDP 프로토콜이 대표적 <br> TCP 연결 지행적, 신뢰성 데이터 전송, <br>UDP는 비연결 지향적, 신뢰성은 낮지만 속도 중시|
|Layer 3|Network|패킬을 목적지로 전달<br>IP 프로토콜이 이 계층에서 동작<br>라우우팅 패킷 분할/재조립 기능 수행|
|Layer 2|Data link| 물리적 네트워크의 접근을 제공<br>물리주소(MAC) 사용|
|Layer 1|Physical|물리 매채를 비트스트림 전송<br>전기 신호, 광신호 등의 구체적인 전송방식 정의|

*End to End - 제3자가 엔드포인트 간에 전송된 데이터에 액세스하지 못하도록 차단하는 보안 통신 프로세스

*Packet - 정보를 보낼 때 특정 형태를 맞추어 보낸다는 것

상위 계층으로 갈수록 추상화 수준이 높아진다

각 계층은 하위 계층에 의존

데이터 전송은 Application Layer(가장 상위 계층)에서 시작된다.

Layer 5에서 생성된 데이터는 아래 계층으로 내려가며 해당 프로토콜에 따라 캡슐화(encapsulation)된다.



## Communication

![Communication_from_A_to_B](/images/communication_from_a_to_b.jpg)

The source host (Source A) need to create a messafe in the application layer and sent it down the layers.

Router is onvolved only three layer (is used only for routing)

-> Physical, Data link, Network

Switch is involved only two layer

->Physical, Data link

*Top three layer is the network, two lower layer is the link.

One of the most important concepts in protocol layering in the Internet is encapsulation/decapsulation.

* Encapsulation at the Source Host
* Decapsulation and Encapsulation at Router
* Decapsulation at the Destination Host

## Adressing in the TCP/IP protocol

![protocol](/images/protocol.jpg)

This is the table for the packet names and addresses for each layer.



Difference between Frame and Datagram

Frame

* Data-linke에서 사용되는 단위
* 물리주소를 헤더에 포함
* 신뢰성을 위해 오류 검출 및 수정기능 제공

Datagram

* Internet layer에서 사용되는 단위
* 소스와 목적지의 논리주소 (IP 주소) 를 헤더에 포함
* 신뢰성 보장이 약함


## Multiplexing and Demutiplexing

![multiplexing](/images/multiplexing.jpg)

Multiplexing : A protocol at a layer can encapsulate a paket from several next-higher layer protocol

Demultiplexing : decapsulating and delivera packe to several next-higher layer.

위 표는 TCP/IP 프로토콜 스탹의 구조를 보여준다. 

최상위 계층은 애플리케이션 계층으로, FTP(파일 전송 프로토콜), HTTP(웹 프로토콜), DNS(도메인 이름 시스템), SNMP(네트워크 관리 프로토콜)이 있다. 

전송계층에는 TCP(Transmission Control Protocol) 와 UDP (User Data Protocol)이 있다. 