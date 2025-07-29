# 🔍 Basic Nmap Scan (`nmap <target-ip>`)

## 🧪 Command Used
    nmap 192.168.153.129 -oN basic-scan.txt

## 🛠️ What It Does:
This command runs a **basic Nmap scan** on the target machine `192.168.153.129` to discover which **TCP ports** are open and what services might be running on them.

- `nmap` → the command-line tool used for network reconnaissance.
- `192.168.153.129` → target IP address (Metasploitable in this case).
- `-oN basic-scan.txt` → saves the scan output in a readable format to a file named `basic-scan.txt`.

### 🔍 Basic Nmap Scan Screenshot

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Nmap-Recon-Project/blob/main/screenshots/basic-scan.png" alt="Nmap Scan Output" width="100%">
</p>



⚠️ Vulnerabilities, Exploits, and Fixes (Basic Scan) :

Note: This scan doesn’t give versions, so we suspect vulnerabilities based on service type only.


| Port        | Service | Possible Vulnerability               | How to Exploit (Basic Idea)                  | How to Fix (Mitigation)               |
| ----------- | ------- | ------------------------------------ | -------------------------------------------- | ------------------------------------- |
| **21**      | FTP     | Anonymous login, Cleartext passwords | Try login with `ftp` → `anonymous:anonymous` | Use SFTP or disable FTP               |
| **23**      | Telnet  | Unencrypted remote access            | Sniff credentials using Wireshark or MITM    | Replace with SSH, block port 23       |
| **80**      | HTTP    | Default web app may be vulnerable    | Open in browser, test with Burp for XSS/LFI  | Use HTTPS, harden web app             |
| **139/445** | SMB     | SMBv1, Null sessions                 | Use `enum4linux` to list shares, users       | Disable SMBv1, enforce SMB signing    |
| **3306**    | MySQL   | Exposed DB port                      | Use `mysql -h <IP> -u root -p`               | Block remote access, use strong creds |
| **5900**    | VNC     | Weak/no password                     | Try VNC viewer without password              | Set strong auth, use over SSH tunnel  |
| **2049**    | NFS     | Public file shares                   | Use `showmount -e` to list exports           | Restrict IPs, use firewall            |
| **6667**    | IRC     | Might be backdoor C2 channel         | Connect using `netcat` or `irc` client       | Disable service if not needed         |

### 🧠 Summary of Basic Scan

- No critical vulnerabilities were found in this scan.
- Only open ports and basic service banners were listed.
- No version-specific weaknesses or outdated services detected in this phase.
