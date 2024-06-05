### Лабораторная работа 2. Построение Underlay сети(OSPF)

### Цели:
- Настроить OSPF в Underlay сети, для IP связанности между всеми сетевыми устройствами;
- Убедиться в наличии IP связанности между устройствами в OSFP домене;

![Схема.png](Схема.png)

### Настройки OSPF:
<details>
<summary> Spine_1 </summary>
  
```
spine_1#show running-config
! Command: show running-config
! device: spine-1 (vEOS-lab, EOS-4.29.2F)
!
! boot system flash:/vEOS-lab.swi
!
no aaa root
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model ribd
!
hostname spine_1
!
spanning-tree mode mstp
!
interface Ethernet1
   no switchport
   ip address 10.2.1.0/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet2
   no switchport
   ip address 10.2.1.2/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet3
   no switchport
   ip address 10.2.1.4/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet4
!
interface Ethernet5
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Loopback1
   ip address 10.0.1.0/32
   ip ospf area 0.0.0.0
!
interface Loopback2
   ip address 10.1.1.0/32
!
interface Management1
!
ip routing
!
router ospf 1
   router-id 10.0.1.0
   max-lsa 12000
!
```
```
spine_1#show ip route ospf detail

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

 O        10.0.0.1/32 [110/20] via 10.2.1.1, Ethernet1
 O        10.0.0.2/32 [110/20] via 10.2.1.3, Ethernet2
 O        10.0.0.3/32 [110/20] via 10.2.1.5, Ethernet3
 O        10.0.2.0/32 [110/30] via 10.2.1.1, Ethernet1
                               via 10.2.1.3, Ethernet2
                               via 10.2.1.5, Ethernet3
 O        10.2.2.0/31 [110/20] via 10.2.1.1, Ethernet1
 O        10.2.2.2/31 [110/20] via 10.2.1.3, Ethernet2
 O        10.2.2.4/31 [110/20] via 10.2.1.5, Ethernet3
 O        10.4.0.8/29 [110/20] via 10.2.1.1, Ethernet1
 O        10.4.0.16/29 [110/20] via 10.2.1.3, Ethernet2
 O        10.4.0.24/29 [110/20] via 10.2.1.5, Ethernet3
 O        10.4.0.32/29 [110/20] via 10.2.1.5, Ethernet3
```

<details>
<summary> Spine_1 </summary>
  
```
spine_1#show running-config
! Command: show running-config
! device: spine-1 (vEOS-lab, EOS-4.29.2F)
!
! boot system flash:/vEOS-lab.swi
!
no aaa root
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model ribd
!
hostname spine_1
!
spanning-tree mode mstp
!
interface Ethernet1
   no switchport
   ip address 10.2.1.0/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet2
   no switchport
   ip address 10.2.1.2/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet3
   no switchport
   ip address 10.2.1.4/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet4
!
interface Ethernet5
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Loopback1
   ip address 10.0.1.0/32
   ip ospf area 0.0.0.0
!
interface Loopback2
   ip address 10.1.1.0/32
!
interface Management1
!
ip routing
!
router ospf 1
   router-id 10.0.1.0
   max-lsa 12000
!
```
```
spine_1#show ip route ospf detail

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

 O        10.0.0.1/32 [110/20] via 10.2.1.1, Ethernet1
 O        10.0.0.2/32 [110/20] via 10.2.1.3, Ethernet2
 O        10.0.0.3/32 [110/20] via 10.2.1.5, Ethernet3
 O        10.0.2.0/32 [110/30] via 10.2.1.1, Ethernet1
                               via 10.2.1.3, Ethernet2
                               via 10.2.1.5, Ethernet3
 O        10.2.2.0/31 [110/20] via 10.2.1.1, Ethernet1
 O        10.2.2.2/31 [110/20] via 10.2.1.3, Ethernet2
 O        10.2.2.4/31 [110/20] via 10.2.1.5, Ethernet3
 O        10.4.0.8/29 [110/20] via 10.2.1.1, Ethernet1
 O        10.4.0.16/29 [110/20] via 10.2.1.3, Ethernet2
 O        10.4.0.24/29 [110/20] via 10.2.1.5, Ethernet3
 O        10.4.0.32/29 [110/20] via 10.2.1.5, Ethernet3
```
