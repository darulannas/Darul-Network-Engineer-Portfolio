**1. Project Overview**

This lab covers the implementation of Network Address Translation (NAT) on a MikroTik router to enable communication between a private LAN and an external network.  
NAT allows internal devices to access the internet using a single public IP address, while also enabling inbound access to specific internal services through port forwarding.  

Before applying NAT configuration, the router must already have a working basic setup and LAN structure.  
This lab assumes that the initial configuration from Lab 1 (Internet Access) and the bridge configuration from Lab 3 (Switching) have been completed.  

This scenario reflects real-world network deployments where NAT is applied on top of an existing network infrastructure, and it aligns with fundamental concepts in MTCNA.  
<br>

**2. Network Topology**

<img width="348" height="417" alt="image" src="https://github.com/user-attachments/assets/e1bb585a-769c-44ae-85c8-db04baef8b06" />

- **MikroTik Router (R1)** — acts as NAT device and gateway  
- **LAN Network** — `172.16.10.0/24`  
- **Client** — accesses internet using private IP  
- **Web Server** — exposed using port forwarding  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# Prerequisite:
# Ensure Lab 1 (Initial Configuration) is completed:
# - IP Address configured
# - Default route available
# - Internet connectivity working

# 1. Configure Source NAT (Masquerade)
/ip firewall nat add chain=srcnat out-interface=eth1 action=masquerade

# 2. Configure Destination NAT (Port Forwarding)
# Forward HTTP traffic to internal web server
/ip firewall nat add chain=dstnat protocol=tcp dst-port=80 \
action=dst-nat to-addresses=172.16.10.3 to-ports=80

# 3. Verify NAT Rules
/ip firewall nat print

VPCS :
# Test outbound connectivity
/ping 8.8.8.8
```

**4. Verification**

Mikrotik :
<img width="580" height="95" alt="image" src="https://github.com/user-attachments/assets/24720818-e1e1-40f5-b53e-bbb600035677" />

VPC :
<img width="474" height="124" alt="image" src="https://github.com/user-attachments/assets/9cc1039d-efcd-4f53-99fc-bb75b7b24c32" />

- LAN client is able to reach external network (internet)
- Private IP address is translated to public IP using masquerade
- Incoming traffic on port 80 is forwarded to the internal web server
- NAT rules are active and visible in the configuration
<br>

**5. Key Learning Points**

- Understood how NAT enables communication between private and public networks
- Learned how masquerade dynamically handles outbound traffic translation
- Implemented destination NAT to expose internal services
- Recognized how NAT influences traffic flow through the router
- Applied practical NAT configuration aligned with MTCNA fundamentals
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of hands-on practice in MikroTik NAT configuration.
It demonstrates how NAT is used to provide internet access and control inbound traffic to internal services.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
