**1. Project Overview**

This lab introduces the configuration of a bridge interface on a MikroTik router to enable basic Layer 2 switching functionality.
By grouping multiple physical interfaces into a single bridge, devices connected to different ports can communicate within the same network segment.

This approach is commonly applied in small network environments where a router also serves as a switch, and it represents a fundamental concept within MTCNA.\
<br>

**2. Network Topology**

<img width="348" height="419" alt="image" src="https://github.com/user-attachments/assets/06133274-6969-401b-992d-f3cc68481c44" />

- **MikroTik Router** — operates as gateway and bridge device  
- **Bridge Interface** — connects multiple Ethernet ports into one network  
- **LAN Network** — `172.16.10.0/24`  
- **Client Devices** — connected to separate ports but within the same subnet  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# 1. Create Bridge Interface
/interface bridge add name=bridge1

# 2. Add Interfaces to Bridge
/interface bridge port add bridge=bridge1 interface=ether2
/interface bridge port add bridge=bridge1 interface=ether3

# 3. Assign IP Address to Bridge
/ip address add address=172.16.10.1/24 interface=bridge1

# 4. Enable RSTP (optional, recommended)
/interface bridge set bridge1 protocol-mode=rstp

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

**4. Verification**


<br>

**5. Key Learning Points**

- Understood how bridging enables communication at Layer 2
- Learned how to combine multiple interfaces into a single broadcast domain
- Observed how MikroTik can function as both router and switch
- Verified connectivity between devices on different physical ports
- Introduced basic loop prevention using RSTP
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of hands-on exploration of MikroTik switching features.
It highlights how bridge interfaces simplify network design by allowing multiple ports to behave as a single logical segment.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
