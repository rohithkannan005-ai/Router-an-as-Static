# Router-an-a-Stick
Router on a Stick
# Router-on-a-Stick Inter-VLAN Routing - Cisco Packet Tracer

## 📋 Project Overview
This project demonstrates **Router-on-a-Stick** configuration for inter-VLAN routing using Cisco Packet Tracer. A single physical router interface serves multiple VLANs using 802.1Q subinterface encapsulation, enabling communication between isolated network segments while maintaining VLAN separation at Layer 2.

## 🌐 Network Topology

![Router-on-a-Stick Topology](screenshots/router-on-a-stick-topology.png)

```
                    Router (2811)
                "Router on a Stick"
                        │
              Subinterface Encapsulation dot1Q
                        │
                   Trunk Port
                        │
                   Switch (2960-24TT)
                   /    |    |    \
                  /     |    |     \
               PC0    PC1  PC2    PC3
              
        ╔════════════╗      ╔════════════╗
        ║  VLAN 100  ║      ║  VLAN 200  ║
        ║   (Pink)   ║      ║  (Green)   ║
        ║  PC0, PC1  ║      ║  PC2, PC3  ║
        ╚════════════╝      ╚════════════╝
```

### Network Architecture:
- **Router** (Cisco 2811) - Single interface with multiple subinterfaces
- **Switch** (Cisco 2960-24TT) - Hosting two VLANs with trunk uplink
- **VLAN 100** - Department 1 (PC0, PC1)
- **VLAN 200** - Department 2 (PC2, PC3)
- **Trunk Link** - Carrying both VLANs using 802.1Q tagging

---

## 🎯 Objectives
- Configure Router-on-a-Stick for inter-VLAN routing
- Implement 802.1Q subinterface encapsulation
- Set up trunk port between switch and router
- Enable communication between different VLANs
- Demonstrate cost-effective inter-VLAN routing solution

---

## 💡 Why Router-on-a-Stick is Still Essential in 2026

### ✅ Cost-Effective Solution
- **Single Physical Interface**: Uses one router port for multiple VLANs
- **No Layer 3 Switch Required**: Eliminates need for expensive multilayer switches
- **Reduces Hardware Costs**: Ideal for budget-constrained environments
- **Minimal Port Requirements**: Saves valuable router interfaces

### ✅ Small to Medium Business (SMB) Networks
- **Branch Offices**: Perfect for remote locations with 2-5 VLANs
- **Startups**: Cost-effective solution for growing businesses
- **Small Enterprises**: Scales efficiently up to 10-15 VLANs
- **Home Labs**: Excellent for learning and testing

### ✅ Educational & Certification
- **CCNA Preparation**: Fundamental concept in Cisco certifications
- **Networking Foundation**: Core understanding of inter-VLAN routing
- **Lab Environments**: Standard practice in academic settings
- **Skill Development**: Essential for network engineers

### ✅ Legacy System Support
- **Production Networks**: Many existing networks still use this design
- **Migration Bridge**: Interim solution during infrastructure upgrades
- **Troubleshooting Skills**: Critical for maintaining older deployments
- **Backward Compatibility**: Works with legacy Cisco equipment

### ✅ Network Segmentation Benefits
- **Department Isolation**: Separates HR, Finance, IT departments
- **Security Enhancement**: VLANs provide logical separation
- **Broadcast Domain Management**: Reduces network congestion
- **Traffic Control**: Enables inter-VLAN policies and ACLs

---

## 🔧 Configuration

### Step 1: Configure VLANs on Switch
```cisco
Switch>enable
Switch#configure terminal
Switch(config)#hostname Switch0

! Create VLAN 100
Switch0(config)#vlan 100
Switch0(config-vlan)#name Department1
Switch0(config-vlan)#exit

! Create VLAN 200
Switch0(config)#vlan 200
Switch0(config-vlan)#name Department2
Switch0(config-vlan)#exit
```

### Step 2: Assign Ports to VLANs
```cisco
! Assign PC0 to VLAN 100
Switch0(config)#interface FastEthernet0/1
Switch0(config-if)#switchport mode access
Switch0(config-if)#switchport access vlan 100
Switch0(config-if)#exit

! Assign PC1 to VLAN 100
Switch0(config)#interface FastEthernet0/2
Switch0(config-if)#switchport mode access
Switch0(config-if)#switchport access vlan 100
Switch0(config-if)#exit

! Assign PC2 to VLAN 200
Switch0(config)#interface FastEthernet0/3
Switch0(config-if)#switchport mode access
Switch0(config-if)#switchport access vlan 200
Switch0(config-if)#exit

! Assign PC3 to VLAN 200
Switch0(config)#interface FastEthernet0/4
Switch0(config-if)#switchport mode access
Switch0(config-if)#switchport access vlan 200
Switch0(config-if)#exit
```

### Step 3: Configure Trunk Port
```cisco
! Configure trunk to router
Switch0(config)#interface FastEthernet0/24
Switch0(config-if)#switchport mode trunk
Switch0(config-if)#exit
```

### Step 4: Configure Router Subinterfaces (Router-on-a-Stick)
```cisco
Router>enable
Router#configure terminal
Router(config)#hostname Router-on-a-Stick

! Enable physical interface
Router-on-a-Stick(config)#interface GigabitEthernet0/0
Router-on-a-Stick(config-if)#no shutdown
Router-on-a-Stick(config-if)#exit

! Create subinterface for VLAN 100
Router-on-a-Stick(config)#interface GigabitEthernet0/0.100
Router-on-a-Stick(config-subif)#encapsulation dot1Q 100
Router-on-a-Stick(config-subif)#ip address 192.168.100.1 255.255.255.0
Router-on-a-Stick(config-subif)#exit

! Create subinterface for VLAN 200
Router-on-a-Stick(config)#interface GigabitEthernet0/0.200
Router-on-a-Stick(config-subif)#encapsulation dot1Q 200
Router-on-a-Stick(config-subif)#ip address 192.168.200.1 255.255.255.0
Router-on-a-Stick(config-subif)#exit
```

### Step 5: Configure PC IP Addresses

**PC0 (VLAN 100):**
```
IP Address:  192.168.100.10
Subnet Mask: 255.255.255.0
Gateway:     192.168.100.1
```

**PC1 (VLAN 100):**
```
IP Address:  192.168.100.11
Subnet Mask: 255.255.255.0
Gateway:     192.168.100.1
```

**PC2 (VLAN 200):**
```
IP Address:  192.168.200.10
Subnet Mask: 255.255.255.0
Gateway:     192.168.200.1
```

**PC3 (VLAN 200):**
```
IP Address:  192.168.200.11
Subnet Mask: 255.255.255.0
Gateway:     192.168.200.1
```

---

## 📊 IP Addressing Scheme

### Network Summary
| Network | VLAN | Subnet | Gateway | Devices |
|---------|------|--------|---------|---------|
| Department 1 | VLAN 100 | 192.168.100.0/24 | 192.168.100.1 | PC0, PC1 |
| Department 2 | VLAN 200 | 192.168.200.0/24 | 192.168.200.1 | PC2, PC3 |

### Router Subinterface Configuration
| Subinterface | Encapsulation | VLAN | IP Address | Purpose |
|--------------|---------------|------|------------|---------|
| Gi0/0 | Physical | - | No IP | Parent interface |
| Gi0/0.100 | dot1Q 100 | 100 | 192.168.100.1 | VLAN 100 gateway |
| Gi0/0.200 | dot1Q 200 | 200 | 192.168.200.1 | VLAN 200 gateway |

### Device IP Assignments
| Device | VLAN | IP Address | Gateway | Status |
|--------|------|------------|---------|--------|
| Router Gi0/0.100 | 100 | 192.168.100.1 | - | Gateway |
| Router Gi0/0.200 | 200 | 192.168.200.1 | - | Gateway |
| PC0 | 100 | 192.168.100.10 | 192.168.100.1 | Client |
| PC1 | 100 | 192.168.100.11 | 192.168.100.1 | Client |
| PC2 | 200 | 192.168.200.10 | 192.168.200.1 | Client |
| PC3 | 200 | 192.168.200.11 | 192.168.200.1 | Client |

---

## ✅ Verification & Testing

### Check VLANs on Switch
```cisco
Switch0#show vlan brief
```
Expected output:
```
VLAN Name        Status    Ports
---- ----------- --------- -------------------------------
1    default     active    Fa0/5-23, Gi0/1-2
100  Department1 active    Fa0/1, Fa0/2
200  Department2 active    Fa0/3, Fa0/4
```

### Check Trunk Port
```cisco
Switch0#show interfaces trunk
```
Expected output:
```
Port        Mode         Encapsulation  Status
Fa0/24      on           802.1q         trunking

Port        Vlans allowed on trunk
Fa0/24      1-4094

Port        Vlans allowed and active in management domain
Fa0/24      1,100,200
```

### Check Router Subinterfaces
```cisco
Router-on-a-Stick#show ip interface brief
```
Expected output:
```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     unassigned      YES unset  up                    up
GigabitEthernet0/0.100 192.168.100.1   YES manual up                    up
GigabitEthernet0/0.200 192.168.200.1   YES manual up                    up
```

### Check Routing Table
```cisco
Router-on-a-Stick#show ip route
```
Expected output:
```
C    192.168.100.0/24 is directly connected, GigabitEthernet0/0.100
C    192.168.200.0/24 is directly connected, GigabitEthernet0/0.200
```

### Test Inter-VLAN Communication
From PC0 (VLAN 100):
```
C:\>ping 192.168.100.11  (PC1 - same VLAN) ✅
C:\>ping 192.168.200.10  (PC2 - different VLAN) ✅
C:\>ping 192.168.200.11  (PC3 - different VLAN) ✅
```

From PC2 (VLAN 200):
```
C:\>ping 192.168.200.11  (PC3 - same VLAN) ✅
C:\>ping 192.168.100.10  (PC0 - different VLAN) ✅
C:\>ping 192.168.100.11  (PC1 - different VLAN) ✅
```

### Trace Route Path
```
C:\>tracert 192.168.200.10
```
Expected output:
```
Tracing route to 192.168.200.10 over a maximum of 30 hops:
  1   <1 ms   <1 ms   <1 ms   192.168.100.1    (Router)
  2   <1 ms   <1 ms   <1 ms   192.168.200.10   (PC2)
```

---

## 🛠️ Equipment Used
- **Router**: Cisco 2811 (x1)
- **Switch**: Cisco 2960-24TT (x1)
- **End Devices**: PC-PT (x4)
- **Cables**: Copper Straight-Through

---

## 📚 Key Concepts Demonstrated

### 1. Router-on-a-Stick Architecture
- **Single Physical Interface**: One port serves multiple VLANs
- **Subinterfaces**: Logical interfaces for each VLAN (Gi0/0.100, Gi0/0.200)
- **802.1Q Encapsulation**: Industry-standard VLAN tagging protocol
- **Cost Efficiency**: Saves router ports and reduces hardware costs

### 2. Inter-VLAN Routing
- **Layer 3 Routing**: Router provides gateway between VLANs
- **Different Subnets**: Each VLAN has its own IP network
- **Default Gateway**: Each VLAN points to its respective subinterface
- **Routing Decision**: Router forwards packets between VLANs

### 3. VLAN Trunking (802.1Q)
- **VLAN Tagging**: Each frame tagged with VLAN ID
- **Trunk Port**: Carries multiple VLANs on single link
- **Native VLAN**: VLAN 1 by default (untagged traffic)
- **Allowed VLANs**: Can restrict which VLANs traverse trunk

### 4. Network Segmentation
- **Broadcast Domain Separation**: VLANs isolate broadcast traffic
- **Security Zones**: Logical separation of departments
- **Traffic Management**: Router controls inter-VLAN communication
- **ACL Application**: Can apply access control between VLANs

---

## 🔍 Router-on-a-Stick vs Layer 3 Switch

| Feature | Router-on-a-Stick | Layer 3 Switch |
|---------|-------------------|----------------|
| **Cost** | Lower (uses existing router) | Higher (multilayer switch) |
| **Performance** | Limited by single link | Wire-speed routing |
| **Scalability** | Good for 5-15 VLANs | Excellent for 100+ VLANs |
| **Complexity** | Simple configuration | More complex setup |
| **Best Use Case** | Small networks, branch offices | Enterprise networks |
| **Hardware** | Any router with subinterface support | Requires Layer 3 switch |
| **Latency** | Slightly higher | Minimal (ASIC-based) |
| **Port Utilization** | Saves router ports | Dedicated SVI per VLAN |

---

## 🔧 Troubleshooting Guide

| Problem | Possible Cause | Solution |
|---------|---------------|----------|
| VLANs can't communicate | Subinterface not configured | Add subinterfaces with dot1Q |
| Trunk not working | Wrong switchport mode | Set to `switchport mode trunk` |
| Router interface down | Physical interface shutdown | `no shutdown` on Gi0/0 |
| Wrong gateway | PC misconfigured | Verify default gateway matches subinterface IP |
| Encapsulation mismatch | Missing dot1Q on subinterface | Add `encapsulation dot1Q [vlan-id]` |
| VLAN not in trunk | Trunk VLAN restriction | Check `show interfaces trunk` |

---

## 🚀 How to Run This Project
1. Download and install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
2. Clone this repository
3. Open `router-on-a-stick.pkt` in Packet Tracer
4. Verify all interfaces show "up/up" status
5. Test ping between PCs in same VLAN
6. Test ping between PCs in different VLANs
7. Use simulation mode to visualize packet flow

---

## 📁 Repository Structure
```
router-on-a-stick/
├── README.md
├── router-on-a-stick.pkt
├── screenshots/
│   ├── router-on-a-stick-topology.png
│   ├── vlan-verification.png
│   └── ping-test.png
└── configs/
    ├── router-config.txt
    └── switch-config.txt
```

---

## 💡 Learning Outcomes
- Understanding Router-on-a-Stick concept and use cases
- Configuring 802.1Q subinterface encapsulation
- Implementing trunk ports for VLAN traffic
- Troubleshooting inter-VLAN routing issues
- Comparing Router-on-a-Stick vs Layer 3 switching
- Designing cost-effective network solutions

---

## 🌟 Real-World Applications

### When to Use Router-on-a-Stick:
✅ **Small branch offices** (5-20 employees)  
✅ **Budget-constrained environments**  
✅ **Networks with 2-10 VLANs**  
✅ **Existing router infrastructure**  
✅ **Educational/lab environments**  

### When to Use Layer 3 Switch Instead:
❌ **Enterprise core networks** (high traffic)  
❌ **Data centers** (low latency required)  
❌ **Networks with 20+ VLANs**  
❌ **Mission-critical applications**  
❌ **High-performance requirements**  

---

## 📜 License
This project is for educational purposes.

---

## 🤝 Contributing
Feel free to fork this project and submit pull requests for improvements!

---

**Note**: Router-on-a-Stick remains a relevant and cost-effective solution for small to medium networks in 2026, particularly in branch offices, educational institutions, and environments where Layer 3 switches are not economically justified.
