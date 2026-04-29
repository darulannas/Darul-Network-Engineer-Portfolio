**1. Project Overview**

This lab introduces static routing configuration on MikroTik routers to enable communication between different networks.
By defining static routes, routers can determine the correct path for forwarding traffic to remote subnets.

Before implementing static routing, the network must already have basic connectivity and proper LAN segmentation.
This lab assumes that the initial setup from Lab 1 (Internet Access), bridge configuration from Lab 3, and NAT setup from Lab 6 are already in place.

This scenario reflects a common real-world setup where multiple routers are used to connect separate networks, and static routing is applied to ensure proper communication between them.\
<br>

**2. Network Topology**

- **R1** — connects LAN 1  
- **R2** — connects LAN 2  
- **Inter-router link** — used for routing between networks  
<br>

**3. Configuration Steps**
```bash
R1 (MikroTik) :
# 1. Configure IP Address on LAN
/ip address add address=172.16.10.1/24 interface=bridge-LAN

# 2. Configure IP Address on Link to R2
/ip address add address=10.10.10.1/30 interface=ether1

# 3. Add Static Route to LAN 2
/ip route add dst-address=172.16.20.0/24 gateway=10.10.10.2

R2 (MikroTik) :
# 1. Configure IP Address on LAN
/ip address add address=172.16.20.1/24 interface=bridge-LAN

# 2. Configure IP Address on Link to R1
/ip address add address=10.10.10.2/30 interface=ether1

# 3. Add Static Route to LAN 1
/ip route add dst-address=172.16.10.0/24 gateway=10.10.10.1

VPCS :
# Client A (LAN 1)
/ip 172.16.10.2 172.16.10.1

# Client B (LAN 2)
/ip 172.16.20.2 172.16.20.1

# Test connectivity between networks
/ping 172.16.20.2
/ping 172.16.10.2
```

**4. Verification**

- Devices in different networks can communicate successfully
- Ping between Client A and Client B is successful
- Routing table contains static routes for remote networks 
<br>

**5. Key Learning Points**

- Learned how static routes define paths between networks
- Understood the role of gateway in routing decisions
- Practiced configuring point-to-point links between routers
- Verified inter-network communication using static routing
- Recognized how routing expands network scalability
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of hands-on practice in MikroTik routing configuration.
It demonstrates how static routing enables communication between separate networks in a simple and controlled manner.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
