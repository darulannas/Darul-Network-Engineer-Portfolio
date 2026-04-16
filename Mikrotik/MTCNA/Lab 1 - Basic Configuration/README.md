**1. Project Overview**

This project demonstrates the initial configuration steps for enabling internet access on a MikroTik router.
The configuration covers basic setup such as system identity, IP addressing, NAT masquerade, DNS settings, and route configuration.
This is part of my MTCNA learning practice, reflecting real-world setups I have implemented in office environments.\
<br>

**2. Network Topology**

<img width="349" height="420" alt="Network Topology" src="https://github.com/user-attachments/assets/580050d7-efe5-4484-a75d-34e89b64ec63" />

- **MikroTik Router** — acts as gateway and NAT device  
- **LAN Network** — `172.16.10.0/24`  
- **WAN Interface** — connected to ISP (via DHCP or static IP)  
- **Client PC** — obtains IP via DHCP from the router
<br>

**3. Configuration Steps**
```bash
# 1. Set system identity
/system identity set name=MTCNA-Router

# 2. Configure LAN interface
/ip address add address=172.16.10.1/24 interface=ether2

# 3. Configure WAN interface (DHCP)
 /ip dhcp-client add interface=ether1 disabled=no

# 4. Configure NAT for Internet Access
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

# 5. Set DNS and allow remote requests
/ip dns set servers=8.8.8.8,1.1.1.1 allow-remote-requests=yes
```

**4. Verification**

**5. Key Learning Points**
- Understood the purpose of default routing for internet access.
- Practiced creating NAT rules using masquerade.
- Learned how DNS and DHCP clients are used in RouterOS.
- Verified connectivity using ping and traceroute.
- Applied practical concepts from MTCNA curriculum in a real environment.

**6. Tools Used**
- MikroTik RouterOS v6
- WinBox (for GUI configuration)
- VMware + CHR (for simulated)

**7. Author Notes**

Created by Darul Annas as part of professional documentation for MikroTik network configuration practices.
This project is intended for educational and portfolio purposes.
Feel free to clone or suggest improvements.
This documentation is inspired by the MTCNA outline, which you can review here:
https://mikrotik.com/training/about


