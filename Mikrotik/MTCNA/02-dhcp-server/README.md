**1. Project Overview**

This lab focuses on setting up a DHCP Server on a MikroTik router to provide automatic IP address assignment for devices within the local network.
Instead of configuring IP addresses manually on each client, DHCP simplifies network management by dynamically distributing IP configuration.
This setup is commonly used in office environments and is part of the core concepts covered in MTCNA.\
<br>

**2. Network Topology**

<img width="347" height="420" alt="image" src="https://github.com/user-attachments/assets/50c6ca6e-4eb4-4d21-b05f-436ebb01a0a3" />

- **MikroTik Router** — functions as gateway and DHCP Server  
- **LAN Network** — `172.16.10.0/24`  
- **WAN Interface** — connected to ISP (via DHCP)  
- **Client PC** — receives IP configuration automatically  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# 1. Configure LAN interface
/ip address add address=172.16.10.1/24 interface=ether2

# 2. Configure WAN interface (DHCP)
 /ip dhcp-client add interface=ether1 disabled=no

# 3. Configure NAT for Internet Access
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

# 4. Configure Default Route
/ip route add dst-address=0.0.0.0/0 gateway=192.168.52.2

# 5. Set DNS and allow remote requests
/ip dns set servers=8.8.8.8,1.1.1.1 allow-remote-requests=yes

# 6. Define IP Pool for DHCP Clients
/ip pool add name=pool1 ranges=172.16.10.10-172.16.10.100

# 7. Enable DHCP Server on LAN Interface
/ip dhcp-server add name=server1 interface=ether2 address-pool=pool1 disabled=no

# 8. Specify Network Parameters
/ip dhcp-server network add address=172.16.10.0/24 gateway=172.16.10.1 dns-server=8.8.8.8,1.1.1.1

# 9. Verify DHCP Server Status
/ip dhcp-server print

VPCS :
# 1. Request IP from DHCP Server
/ip dhcp

# 2. Display assigned IP configuration
/show ip

# 3. Test connectivity
/ping 172.16.10.1
/ping 8.8.8.8
```

**4. Verification**

Mikrotik :
<img width="635" height="177" alt="image" src="https://github.com/user-attachments/assets/d3bcb8c6-26c2-4816-820a-7fb5fcc16faf" />

VPCS :
<img width="470" height="391" alt="image" src="https://github.com/user-attachments/assets/bc2cb8c2-c205-4836-bc92-df89dc106060" />
<br>

**5. Key Learning Points**

- Learned how DHCP simplifies IP management in a network
- Understood how MikroTik distributes IP addresses dynamically
- Identified the role of DHCP Pool and Network configuration
- Verified successful lease assignment from router to client
- Practiced real-world implementation aligned with MTCNA fundamentals
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of hands-on practice in MikroTik networking.
It demonstrates how DHCP can streamline network configuration in practical environments.
Feedback and suggestions are always welcome.
For reference, this lab follows the MTCNA learning path:
https://mikrotik.com/training/about
