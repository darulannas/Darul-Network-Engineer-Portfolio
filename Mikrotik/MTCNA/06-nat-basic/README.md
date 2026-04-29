**1. Project Overview**

This lab covers the implementation of Network Address Translation (NAT) on a MikroTik router to enable communication between a private LAN and an external network.  
NAT allows internal devices to access the internet using a single public IP address, while also enabling inbound access to specific internal services through port forwarding.  

Before applying NAT configuration, the router must already have a working basic setup and LAN structure.  
This lab assumes that the initial configuration from Lab 1 (Internet Access) and the bridge configuration from Lab 3 (Switching) have been completed.  

This scenario reflects real-world network deployments where NAT is applied on top of an existing network infrastructure, and it aligns with fundamental concepts in MTCNA.  
<br>

**2. Network Topology**

- **MikroTik Router** — acts as gateway and NAT device  
- **LAN Network** — `172.16.10.0/24`  
- **WAN Interface** — connected to ISP  
- **Internal Client** — accesses internet via NAT  
- **External Access** — simulated for port forwarding scenario  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# Prerequisite:
# Ensure basic configuration from Lab 1 is completed:
# - IP Address configured
# - Internet connectivity working

# 1. Configure Source NAT (Masquerade)
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

# 2. Verify NAT Rule
/ip firewall nat print

# 3. Configure Destination NAT (Port Forwarding Example)
# Forward HTTP (port 80) to internal client (172.16.10.2)
/ip firewall nat add chain=dstnat protocol=tcp dst-port=80 \
action=dst-nat to-addresses=172.16.10.2 to-ports=80

# 4. Verify NAT Configuration
/ip firewall nat print

VPCS :
# Test internet connectivity (via NAT)
/ping 8.8.8.8
```

**4. Verification**

- Internal clients are able to access the internet using private IP addresses
- NAT masquerade translates private IP to public IP on outbound traffic
- Port forwarding rule directs incoming traffic to the correct internal host
- NAT rules are visible and active in the router configuration
<br>

**5. Key Learning Points**

- Understood the purpose of NAT in connecting private and public networks
- Learned how masquerade dynamically translates source addresses
- Introduced destination NAT for basic port forwarding
- Observed how NAT rules affect traffic flow
- Reinforced the relationship between NAT and firewall processing
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of hands-on learning in MikroTik NAT configuration.
It highlights how NAT plays a critical role in enabling internet access and controlling traffic direction between internal and external networks.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
