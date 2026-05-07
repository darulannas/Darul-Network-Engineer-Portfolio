**1. Project Overview**

This lab demonstrates how to implement basic bandwidth management using Simple Queue on a MikroTik router.
By applying traffic limits to specific clients, network administrators can control bandwidth usage and maintain fair network performance across users.

This configuration is commonly used in office and small-scale environments to prevent excessive bandwidth consumption from a single device.
The lab assumes that basic LAN connectivity and routing have already been configured beforehand.\
<br>

**2. Network Topology**

- **MikroTik Router** — acts as gateway and bandwidth controller  
- **LAN Network** — `172.16.10.0/24`  
- **Client A** — bandwidth limited using Simple Queue  
- **Client B** — normal network client  
<br>

**3. Configuration Steps**
```bash
MikroTik :
# Prerequisite:
# Ensure LAN connectivity is working properly

# 1. Create Simple Queue for Client A
/queue simple add name=Client-A target=172.16.10.2 \
max-limit=2M/2M

# 2. Verify Queue Configuration
/queue simple print

# 3. Monitor Queue Traffic
/queue simple monitor 0

VPCS :
# Test connectivity
/ping 172.16.10.1

# Perform bandwidth usage test (simulation)
# Example: download or continuous ping traffic
```

**4. Verification**

- Client A bandwidth is limited according to configured values
- Queue statistics display active traffic usage
- Other clients remain unaffected by the bandwidth limitation
- Queue rules are visible and active in MikroTik configuration
<br>

**5. Key Learning Points**

- Learned how QoS can control bandwidth allocation per client
- Understood the role of Simple Queue in traffic management
- Applied upload and download limits to specific devices
- Observed real-time traffic monitoring through queue statistics
- Practiced basic QoS implementation aligned with MTCNA concepts
<br>

**6. Tools Used**

- MikroTik RouterOS v6
- Putty (for configuration)
- VMware + CHR (for simulated)
<br>

**7. Author Notes**

This lab was created by Darul Annas as part of hands-on practice in MikroTik traffic management.
It demonstrates how Simple Queue can be used to manage bandwidth utilization and improve network stability in shared environments.

This documentation follows the MTCNA learning path:
https://mikrotik.com/training/about
