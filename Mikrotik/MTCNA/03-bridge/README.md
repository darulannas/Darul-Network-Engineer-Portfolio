**1. Project Overview**

This lab introduces the configuration of a bridge interface on a MikroTik router to enable basic Layer 2 switching functionality.
By grouping multiple physical interfaces into a single bridge, devices connected to different ports can communicate within the same network segment.

This approach is commonly applied in small network environments where a router also serves as a switch, and it represents a fundamental concept within MTCNA.\
<br>

**2. Network Topology**

- **MikroTik Router** — operates as gateway and bridge device  
- **Bridge Interface** — connects multiple Ethernet ports into one network  
- **LAN Network** — `172.16.10.0/24`  
- **Client Devices** — connected to separate ports but within the same subnet  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# 1. Create Bridge Interface
/interface bridge add name=bridge-LAN

# 2. Add Interfaces to Bridge
/interface bridge port add bridge=bridge-LAN interface=ether2
/interface bridge port add bridge=bridge-LAN interface=ether3

# 3. Assign IP Address to Bridge
/ip address add address=172.16.10.1/24 interface=bridge-LAN

# 4. Enable RSTP (optional, recommended)
/interface bridge set bridge-LAN protocol-mode=rstp

# 5. Verify Bridge Status
/interface bridge print
/interface bridge port print

VPCS :
# Client 1
/ip 172.16.10.2 172.16.10.1

# Client 2
/ip 172.16.10.3 172.16.10.1

# Test communication between clients
/ping 172.16.10.3
/ping 172.16.10.2
```
