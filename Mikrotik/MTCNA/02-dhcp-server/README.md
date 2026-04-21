**1. Project Overview**

This lab focuses on setting up a DHCP Server on a MikroTik router to provide automatic IP address assignment for devices within the local network.
Instead of configuring IP addresses manually on each client, DHCP simplifies network management by dynamically distributing IP configuration.
This setup is commonly used in office environments and is part of the core concepts covered in MTCNA.\
<br>

**2. Network Topology**

- **MikroTik Router** — functions as gateway and DHCP Server  
- **LAN Network** — `172.16.10.0/24`  
- **WAN Interface** — connected to ISP (via DHCP)  
- **Client PC** — receives IP configuration automatically  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# 1. Define IP Pool for DHCP Clients
/ip pool add name=dhcp_pool ranges=172.16.10.10-172.16.10.100

# 2. Enable DHCP Server on LAN Interface
/ip dhcp-server add name=dhcp1 interface=ether2 address-pool=dhcp_pool disabled=no

# 3. Specify Network Parameters
/ip dhcp-server network add address=172.16.10.0/24 \
gateway=172.16.10.1 \
dns-server=8.8.8.8,1.1.1.1

# 4. Verify DHCP Server Status
/ip dhcp-server print

VPCS :
# 1. Request IP from DHCP Server
/ip dhcp

# 2. Display assigned IP configuration
/show ip

# 3. Test connectivity
/ping 172.16.10.1
/ping 8.8.8.8
