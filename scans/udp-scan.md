
## 📌 UDP Scan Report

> **Command Used:**
sudo nmap -sU --top-ports 100 192.168.153.129 -oN udp-top100.txt


### 🔍 What It Does:

This command runs a **UDP scan** on the **top 100 most common UDP ports** of the target (`192.168.153.129`). UDP-based services often run silently and are **missed in normal TCP scans**, making them ideal for stealthy attacks if not secured.


## 📸 Screenshot:

<p align="center">
  <img src="screenshots/udp-scan.png" alt="Nmap Scan Output" width="100%">
</p>

## 📊 Vulnerability Table

| Port | Service | What It Does                             | Risk if Misconfigured                             | What You Can Do                                      |
| ---- | ------- | ---------------------------------------- | ------------------------------------------------- | ---------------------------------------------------- |
| 53   | DNS     | Resolves domain names to IP addresses.   | Can be abused for DNS amplification or poisoning. | Disable if unused, limit recursion, keep it updated. |
| 111  | RPCBind | Helps connect to services like NFS.      | Can expose other services like NFS for attacks.   | Block externally, use firewall, restrict access.     |
| 137  | NetBIOS | Legacy Windows service for name sharing. | Can leak network info like usernames or shares.   | Disable on modern systems, block on firewall.        |
| 2049 | NFS     | Shares files across a network.           | Can allow remote file access without login.       | Disable if not needed or restrict to trusted IPs.    |

---

## 🧾 Summary of the UDP Scan

✅ Host is up and responsive. <br>
✅ 4 open UDP ports detected: `53`, `111`, `137`, `2049`.<br>
⚠️ These services can leak info or allow unauthorized access if misconfigured.<br>
🛠️ Many can be disabled or locked down using firewall rules or service configurations.<br>
🔒 This scan helps reveal **hidden risks** not seen in TCP scans.<br>
