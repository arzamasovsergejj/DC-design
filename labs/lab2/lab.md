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
end
```
