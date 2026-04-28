**1. Project Overview**

This lab focuses on implementing basic firewall filter rules on a MikroTik router to control traffic and protect the network.
By applying filtering policies, the router can decide which traffic is allowed or blocked, improving overall network security.

This configuration represents essential firewall practices in MTCNA and is commonly applied in real-world network environments.\
<br>

**2. Network Topology**

- **MikroTik Router** — acts as gateway and firewall  
- **LAN Network** — `172.16.10.0/24`  
- **WAN Interface** — connected to ISP  
- **Client Devices** — access internet through router with filtering rules applied  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# 1. Allow Established and Related Connections
/ip firewall filter add chain=input connection-state=established,related action=accept

# 2. Drop Invalid Connections
/ip firewall filter add chain=input connection-state=invalid action=drop

# 3. Allow ICMP (Ping) to Router
/ip firewall filter add chain=input protocol=icmp action=accept

# 4. Allow Access from LAN to Router
/ip firewall filter add chain=input src-address=172.16.10.0/24 action=accept

# 5. Drop All Other Incoming Traffic (Protect Router)
/ip firewall filter add chain=input action=drop

# 6. Allow Forward Traffic from LAN to WAN
/ip firewall filter add chain=forward src-address=172.16.10.0/24 action=accept

# 7. Drop Invalid Forward Traffic
/ip firewall filter add chain=forward connection-state=invalid action=drop

# 8. Verify Firewall Rules
/ip firewall filter print

VPCS :
# Test connectivity to internet
/ping 8.8.8.8

# Test access to router
/ping 172.16.10.1
```

**4. Verification**

<br>

**5. Key Learning Points**

- Learned how firewall filter rules control network traffic
- Understood the purpose of different chains (input, forward)
- Applied basic protection to the router from unauthorized access
- Recognized the importance of connection states (established, related, invalid)
- Verified that allowed traffic functions while unwanted traffic is restricted
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of practical training in MikroTik firewall configuration.
It highlights how basic filtering rules can enhance network security by controlling incoming and outgoing traffic.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
