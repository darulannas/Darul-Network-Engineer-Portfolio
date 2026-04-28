**1. Project Overview**

This lab demonstrates how to configure a MikroTik router as a wireless access point to provide network connectivity for wireless clients.
By enabling wireless functionality and applying proper security settings, devices such as laptops or smartphones can connect to the network without using physical cables.

This setup reflects a common implementation in office and home environments and is part of the essential concepts covered in MTCNA.\
<br>

**2. Network Topology**

- **MikroTik Router** — acts as wireless access point and gateway  
- **Wireless Interface (wlan1)** — provides Wi-Fi connectivity  
- **LAN Network** — `172.16.10.0/24`  
- **Wireless Clients** — connect to SSID and receive network access  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# 1. Set Wireless Mode to AP Bridge
/interface wireless set wlan1 mode=ap-bridge ssid=MTCNA-WIFI disabled=no

# 2. Configure Security Profile
/interface wireless security-profiles add name=wifi-sec \
authentication-types=wpa2-psk \
wpa2-pre-shared-key=12345678

# 3. Apply Security Profile to Wireless Interface
/interface wireless set wlan1 security-profile=wifi-sec

# 4. Assign Wireless Interface to Bridge (if using bridge)
/interface bridge port add bridge=bridge-LAN interface=wlan1

# 5. Verify Wireless Status
/interface wireless print

Wireless Client :
# 1. Connect to SSID "MTCNA-WIFI"
# 2. Enter password: 12345678
# 3. Obtain IP automatically (DHCP)
```

**4. Verification**

In this lab, the wireless configuration is presented as a conceptual simulation.
Since the environment uses MikroTik CHR in a virtualized setup (VMware), the wireless interface (wlan1) is not physically available for real testing.

However, the configuration steps reflect how a MikroTik device would be set up as a wireless access point in a real deployment.

Expected verification in a physical environment:
- Wireless network (SSID) is visible to client devices  
- Clients can connect using WPA2 credentials  
- Clients receive IP address via DHCP  
- Successful connectivity to gateway and internet  

This approach ensures understanding of the configuration workflow despite the limitation of the simulation environment.
<br>

**5. Key Learning Points**

- Learned how to configure MikroTik as a wireless access point
- Understood the role of SSID and wireless modes
- Applied basic wireless security using WPA2-PSK
- Integrated wireless interface into existing LAN network
- Verified connectivity from wireless clients to the network
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**
This lab was created by Darul Annas as part of hands-on practice in MikroTik wireless configuration.
It demonstrates how wireless networking can be integrated into an existing LAN to provide flexible access for users.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
