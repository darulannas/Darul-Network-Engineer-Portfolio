**1. Project Overview**

This project demonstrates the initial configuration steps for enabling internet access on a MikroTik router.
The configuration covers basic setup such as system identity, IP addressing, NAT masquerade, DNS settings, and route configuration.
This is part of my MTCNA learning practice, reflecting real-world setups I have implemented in office environments.


**2. Network Topology**

<img width="374" height="447" alt="Network Topology" src="https://github.com/user-attachments/assets/7cd7ce1c-bb7d-4e36-ae00-4b6e33cb5746" />

- **MikroTik Router** — acts as gateway and NAT device  
- **LAN Network** — `172.16.10.0/24`  
- **WAN Interface** — connected to ISP (via DHCP or static IP)  
- **Client PC** — obtains IP via DHCP from the router
  

**3. Configuration Steps**

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
- VirtualBox + CHR (optional if simulated)

**7. Author Notes**

Created by Darul Annas as part of professional documentation for MikroTik network configuration practices.
This project is intended for educational and portfolio purposes.
Feel free to clone or suggest improvements.

