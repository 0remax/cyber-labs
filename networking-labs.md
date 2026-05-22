# Cisco Enterprise Routing & Security Lab

### 📌 Scenario Overview
A secure corporate office architecture requiring isolated departmental traffic, secure remote administration, and explicit protection policies on the perimeter router.

### 🛠 Network Topology Configuration
Below is the deployment blueprint for secure inter-VLAN routing, interface configuration, and explicit **Access Control Lists (ACLs)** to enforce security parameters.

```cisco
! --- Base Interface Configuration ---
interface GigabitEthernet0/0
 description WAN-Facing Interface
 ip address 192.168.1.2 255.255.255.252
 ip access-group EXTERNAL_PERIMETER_ACL in
 no shutdown

interface GigabitEthernet0/1.10
 description Core Operations Network (VLAN 10)
 encapsulation dot1Q 10
 ip address 10.10.10.1 255.255.255.0

interface GigabitEthernet0/1.20
 description External Guest Traffic (VLAN 20)
 encapsulation dot1Q 20
 ip address 172.16.20.1 255.255.255.0

! --- Engineering Strict Access Control Lists ---
ip access-list extended EXTERNAL_PERIMETER_ACL
 ! Enforce: Permit established TCP traffic back into the infrastructure
 permit tcp any any established
 ! Enforce: Explicitly allow remote site VPN tunnels
 permit udp any host 192.168.1.2 eq isakmp
 ! Enforce: Deny all unauthorized internal traversal attempts
 deny ip any 10.10.10.0 0.0.0.255
 deny ip any 172.16.20.0 0.0.0.255 log
