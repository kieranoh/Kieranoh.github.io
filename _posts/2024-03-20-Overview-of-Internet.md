---
layout: single
title:  "1.1 Overview of the Internet"
categories: Computer_Network
tag: [Computer_Network, WAN, LAN]
toc: true
author_profile: false
---

# LAN & WAN

LAN( local area network ) 은 근거리 통신망으로 제한된 지역 내에서 컴퓨터, 프린터, 스토리지 등 장치들을 연결하는 네트워크이다.

WAN( Wide area network ) 은 광대한 지역을 연결하는 원거리 통신망으로 도시, 지역, 국가 간 거리를 포관하는 넓은 영역들을 연결한다.

difference between LAN & WAN

|LAN|WAN|
|---|---|
|Limited in size<br>interconnect host<br>privately|widw sapn<br>connect switch, router, mordem|

*modem - 정보 전달을 위해 신호를 변조하고 송신하고, 수신측에서 원래 신호로 복구하기 위한 보조장치이다. (디지털 신호 (01001) -> 아날로그 신호(진동))

## WAN
WAN의 두가지 대표적인 예시에는 Point-to-point WANs, Switched WANs가 있다.

### Point-to-point WAN

![point-to-point](/images/point-to-point_wan.png)

* connet two communicating device (cable or air)


### Switched WAN

![switched-wan](/images/switched-wan.png)

* conneted by switch

## 데이터 전송방식

데이터 전송 방식에는 Circuit Switch와 Packet Switch가 있다

|Circuit Switch|Packet Switch|
|---|---|
|전용 통신획선을 전송 기간동안 독점적으로 사용| 네트워크 자원을 동적으로 공유|
|전공 대역폭이 데이터 양과 상관없이 고정 | 패킷 단위로 데이터 전송|
|전화 네트워크 등에서 사용|패킷은 동일한 물리 회선을 공유하며 서로다른 경로를 거칠 수 있다|

*Packet - 정보를 보낼때 특정형태를 맞추어 보내는것

![Circuit-Switch](/images/CircuitSwitched.jpg)

![Packet Switch](/images/PacketSwitched.jpg)

## Difference between internet & Internet

internet - is two or more network that can communicate each other

Internet - composed of thousand of interconnected network


