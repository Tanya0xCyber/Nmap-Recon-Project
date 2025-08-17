#  Version Detection Scan (`nmap -sV`)

##  Command Used :

    nmap -sV 192.168.153.129 -oN version-scan.txt


##  What It Does:

This command runs a **version detection scan** on the target machine `192.168.153.129` to discover not only which **ports** are open, but also which **services** and **versions** are running on those ports.

* `-sV` enables version detection.
* `192.168.153.129` → Metasploitable target IP.
* `-oN version-scan.txt` saves the scan result in readable format to a file.

###  Version Detection Scan Screenshot

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Nmap-Recon-Project/blob/main/screenshots/version-detection-scan.png" alt="Version Detection Output" width="100%">
</p>

---

###  Vulnerabilities, Exploits, and Fixes (Version Detection Scan)

This scan reveals detailed service versions, allowing us to identify **known vulnerabilities** for each.

| Port        | Service & Version      | Known Vulnerability (based on version)                    | How to Exploit (Basic Idea)                              | How to Fix (Mitigation)                                    |
| ----------- | ---------------------- | --------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------------------------- |
| **21/tcp**  | vsftpd 2.3.4           | Backdoor vulnerability (CVE-2011-2523)                    | Use `exploit/unix/ftp/vsftpd_234_backdoor` in Metasploit | Use SFTP or patch FTP server                               |
| **23/tcp**  | Telnet (Linux telnetd) | Unencrypted remote login                                  | Sniff credentials using MITM/Wireshark                   | Disable Telnet, use SSH                                    |
| **25/tcp**  | Postfix smtpd          | Open relay, spam abuse (depending on config)              | Test with `telnet <IP> 25`, try spoofing sender          | Restrict relay, use auth                                   |
| **80/tcp**  | Apache httpd 2.2.8     | Multiple XSS/LFI vulnerabilities in older Apache versions | Burp Suite for XSS/LFI, Nikto for web vulns              | Update Apache, use HTTPS                                   |
| **139/445** | Samba smbd 3.0.20      | Samba trans2open (CVE-2003-0201), Null sessions           | `enum4linux` or Metasploit `samba_trans2open` module     | Enforce SMB signing, patch Samba                           |
| **3306**    | MySQL 5.0.51a          | Auth bypass (CVE-2012-2122), remote root login            | Use `mysql -h <IP> -u root -p`, test weak creds          | Block external access, upgrade MySQL, use strong passwords |
| **5432**    | PostgreSQL 8.3.0       | Weak/default creds                                        | Use `psql` or Metasploit's `postgres_payload`            | Restrict access, strong creds, update PostgreSQL           |
| **5900**    | VNC (no auth required) | Full remote access without password                       | Use `vncviewer <IP>` or `msfconsole` module              | Set password, use SSH tunnel                               |
| **6667**    | Unreal IRC 3.2.8.1     | Remote code execution (CVE-2010-2075)                     | Use Metasploit: `unreal_ircd_3281_backdoor` exploit      | Disable service, patch UnrealIRCd                          |

---

###  Summary of Version Detection Scan

* Several services were found running outdated and vulnerable versions.
* FTP, Samba, IRC, MySQL, and Apache had known CVEs linked to their versions.
* Remote exploitation possible on FTP, Samba, IRC, and VNC services.
