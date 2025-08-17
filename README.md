#  Network Reconnaissance & Vulnerability Discovery using Nmap

This project demonstrates a beginner-friendly yet professional approach to **network scanning, vulnerability discovery**, and **initial system hardening**, using **Nmap** against a Metasploitable VM in a home cybersecurity lab.

---

##  Project Objectives

- Understand and utilize different types of Nmap scans for active network reconnaissance.
- Identify potentially vulnerable services on a target machine.
- Analyze findings from both attacker and defender perspectives.
- Suggest remediation steps for hardening exposed services.
- Build a practical, hands-on foundation for real-world red team/blue team workflows.

---

##  Tools & Setup

- **Operating Systems**: Kali Linux (Attacker), Metasploitable 2 (Target)
- **Platform**: VMware Workstation
- **Tools Used**: Nmap, Wireshark, iptables

---

##  Project Structure

```
 Network-Recon-Nmap/
├──  scans/                         # All Nmap scan result files 
│   ├── basic-scan.md              
│   ├── version-detection-scan.md<br>
│   ├── os-detection-scan.md<br>
│   ├── tcp-connect-scan.md<br>
│   ├── udp-scan.md<br>
│   └── script-scan.md<br><br>
│  
├──  screenshots/                 # Screenshots of Nmap scan outputs  
│   ├── basic-scan.png<br>
│   ├── version-detection-scan.png<br>
│   ├── os-detection-scan.png><br>
│   ├── tcp-connect-scan.png<br>
│   ├── udp-scan.png<br>
│   └── script-scan.png<br><br>
│    
├──  README.md                    # Main project overview and usage instructions   
├──  vulnerability-analysis.md    # Key vulnerabilities + risks explained simply  
├──  system-hardening.md          # Mitigations and hardening strategies

```

##  Scans Performed

| Scan Type            | Command Used                                        | Purpose |
|----------------------|-----------------------------------------------------|---------|
| 1️. Basic TCP Scan    | `nmap <target>`                                     | Discover open TCP ports |
| 2️. TCP Connect Scan  | `nmap -sT <target>`                                 | Check service accessibility |
| 3️. Version Detection | `nmap -sV <target>`                                 | Identify software versions |
| 4️. OS Detection      | `nmap -O <target>`                                  | Guess OS and device type |
| 5️. Default Script    | `nmap -sC <target>`                                 | Run common NSE scripts |
| 6️. Top 100 UDP Ports | `nmap -sU --top-ports 100 <target>`                | Discover open UDP services |

---

##  Vulnerabilities Identified

| Category           | Ports       | Services        | Description                               | Risk Level |
|--------------------|-------------|------------------|-------------------------------------------|------------|
| Remote Access       | 23          | Telnet           | Unencrypted remote login                  | 🔴 High     |
| File Transfer       | 21, 2049    | FTP, NFS         | Insecure protocols, potential leaks       | 🔴 High     |
| Weak Auth Services  | 512–514, 5900 | rsh, rlogin, VNC | No encryption or weak access control     | 🔴 High     |
| Information Leakage | 53, 137, 111| DNS, NetBIOS, RPC | May expose system & network metadata     | 🟠 Medium   |

---

##  Fixes & System Hardening

| Vulnerability       | Fix Applied / Suggested                      |
|---------------------|----------------------------------------------|
| Telnet (Port 23)     |  Replaced with SSH                         |
| FTP (Port 21)        |  Replaced with SFTP                        |
| RPC, NetBIOS, NFS    |  Restrict with firewall rules (iptables)  |
| rsh, VNC, RLogin     |  Disable unused legacy services           |

---

##  Key Learnings

- Multiple Nmap scans provide layered visibility into target systems.
- Legacy services like Telnet, FTP, and NetBIOS are highly vulnerable and should be replaced or hardened.
- UDP services are often overlooked but can leak sensitive information.
- Basic remediation steps (firewalls, encryption, secure protocols) significantly reduce the attack surface.

---





