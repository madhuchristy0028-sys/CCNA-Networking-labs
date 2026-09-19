Lab 01: Inter-VLAN Routing & Centralized DHCP

📌 Project Overview
This project demonstrates a multi-VLAN enterprise campus network implemented in Cisco Packet Tracer. It showcases **Inter-VLAN Routing using the Router-on-a-Stick (ROAS)** architecture, **Centralized DHCP with Relay Services**, and **Local DNS Resolution** across multiple switches.

Network Topology
<img width="1365" height="437" alt="image" src="https://github.com/user-attachments/assets/9cd57caa-e902-4745-a6e4-84133b129aa8" />



## 📐 Network Architecture & VLAN Design

| VLAN ID | Subnet / Network | Purpose | Default Gateway |
| :--- | :--- | :--- | :--- |
| **10** | `192.168.10.0/24` | Servers & Printers | `192.168.10.1` |
| **20** | `192.168.20.0/24` | User Subnet A | `192.168.20.1` |
| **30** | `192.168.30.0/24` | User Subnet B | `192.168.30.1` |
| **40** | `192.168.40.0/24` | User Subnet C | `192.168.40.1` |
| **50** | `192.168.50.0/24` | User Subnet D | `192.168.50.1` |

---

## 🛠 Key Features & Technical Implementation

### 1. Router-on-a-Stick (ROAS)
* Configured sub-interfaces on `Router0` with `802.1Q` encapsulation for each VLAN.
* Acts as the default gateway for all subnets, enabling inter-VLAN traffic routing.

### 2. Centralized DHCP & Relay Agent
* A single DHCP server (`Server0`) on **VLAN 10** dynamically assigns IP addresses, subnet masks, default gateways, and DNS server details to end-devices across all VLANs.
* Configured `ip helper-address 192.168.10.10` on all non-VLAN 10 sub-interfaces on `Router0` to forward layer 2 DHCP broadcasts across VLAN boundaries via unicast relay.

### 3. Trunking & Switching
* Standardized `802.1Q` trunk links across inter-switch connections (`Switch0`, `Switch1`, `Switch2`) and the router link to ensure tagged frames traverse the infrastructure correctly.

### 4. Local DNS Resolution
* Configured an `A Record` (`intranet.lab` -> `192.168.10.10`) on the server to test application-layer reachability across subnets.



## ✅ Verification & Testing

### 1. Dynamic IP Allocation (DHCP Relay)
End devices across VLANs (e.g., VLAN 50) successfully lease dynamic IP configurations from `Server0`.

DHCP Verification
<img width="538" height="714" alt="image" src="https://github.com/user-attachments/assets/29f574a0-a594-40b9-956c-63d2b63f70d6" />


### 2. Same-VLAN reachability (across switches)
Verified Layer 2 switching reachability across switches for devices within the same VLAN.

Same VLAN Reachability
<img width="498" height="691" alt="same Vlan" src="https://github.com/user-attachments/assets/2a1eedff-fd7f-404f-9770-ec5e0e46b771" />


### 3. Inter-VLAN routing (through the router)
Verified Layer 3 ICMP reachability across different VLANs routed through `Router0`.

Inter-VLAN Routing
<img width="545" height="690" alt="across vlan" src="https://github.com/user-attachments/assets/6abe8b56-e7b6-4d31-91dc-31c93f24eb0d" />






