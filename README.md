Домашнее задание №2.

Underlay. OSPF.

Цель: Настроить OSPF для Underlay сети.

Схема.

![Alt text](lab2/shema.PNG)


**1. Config sp1:**

feature ospf

interface loopback0

  ip address 10.0.1.1/32

router  ospf UNDERLEY
  router 10.0.1.1

interface Ethernet1/1

  no switchport

  mtu 9216

  medium p2p

  ip address 10.0.3.0/31

  ip router ospf UNDERLEY area 0.0.0.0

  no shutdown

interface Ethernet1/2

  no switchport

  mtu 9216

  medium p2p

  ip address 10.0.3.2/31

  ip router ospf UNDERLEY area 0.0.0.0

  no shutdown
 
**2. Config sp2:**


feature ospf

interface loopback 0

  ip address 10.0.2.0/32

router ospf UNDERLEY

  router 10.0.2.0


interface Ethernet1/1

  no switchport

  mtu 9216

  medium p2p

  ip address 10.0.3.8/31

  ip router ospf UNDERLEY area 0.0.0.0

  no shutdown

interface Ethernet1/2
  
  no switchport

  mtu 9216

  medium p2p

  ip address 10.0.3.10/31

  ip router ospf UNDERLEY area 0.0.0.0

  no shutdown

**3. Config lif1:**

feature ospf

interface loopback 0

ip addres 10.0.4.1/32

router ospf UNDERLEY

  router 10.0.4.1

interface Ethernet1/1

  no switchport

  mtu 9216

  medium p2p

  ip address 10.0.3.1/31

  ip router ospf UNDERLEY area 0.0.0.0

  no shutdown

interface Ethernet1/2

  no switchport

  mtu 9216

  medium p2p

  ip address 10.0.3.11/31

  ip router ospf UNDERLEY area 0.0.0.0

  no shutdown

**4. Config lif2:**

feature ospf

interface loopback 0
 
 ip address 10.0.5.1/32

router ospf UNDERLEY
  
  router 10.0.5.1

interface Ethernet1/1
  
  no switchport
  
  mtu 9216
  
  medium p2p
  
  ip address 10.0.3.9/31
  
  ip router ospf UNDERLEY area 0.0.0.0
  
  no shutdown

interface Ethernet1/2
  
  no switchport
  
  mtu 9216
  
  medium p2p
  
  ip address 10.0.3.3/31
  
  ip router ospf UNDERLEY area 0.0.0.0
  
  no shutdown


  **Проверка настройки.**

  spine-1# sh ip ospf nei
 
 OSPF Process ID UNDERLEY VRF default
 
 Total number of neighbors: 2
 
 Neighbor ID     Pri State            Up Time  Address         Interface
 
 10.0.4.1          1 FULL/ -          01:04:06 10.0.3.1        Eth1/1
 
 10.0.5.1          1 FULL/ -          00:09:32 10.0.3.3        Eth1/2



spine-2# sh ip ospf ne

 OSPF Process ID UNDERLEY VRF default

 Total number of neighbors: 2

 Neighbor ID     Pri State            Up Time  Address         Interface

 10.0.5.1          1 FULL/ -          00:52:03 10.0.3.9        Eth1/1

 10.0.4.1          1 FULL/ -          00:11:15 10.0.3.11       Eth1/2


spine-2# sh ip ospf route

 OSPF Process ID UNDERLEY VRF default, Routing Table

  (D) denotes route is directly attached      (R) denotes route is in RIB
  (L) denotes route label is in ULIB          (NHR) denotes next-hop is in RIB

10.0.3.0/31 (intra)(R) area 0.0.0.0
     via 10.0.3.11/Eth1/2  , cost 80 distance 110 (NHR)

10.0.3.2/31 (intra)(R) area 0.0.0.0
     via 10.0.3.9/Eth1/1  , cost 80 distance 110 (NHR)

10.0.3.8/31 (intra)(D) area 0.0.0.0
     via 10.0.3.8/Eth1/1*  , cost 40 distance 110 (NHR)

10.0.3.10/31 (intra)(D) area 0.0.0.0
     via 10.0.3.10/Eth1/2*  , cost 40 distance 110 (NHR)




