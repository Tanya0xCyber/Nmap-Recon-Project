## 🔍 Basic Nmap TCP Connect Scan (`nmap -sT`)

### ✅ Command Used :

nmap -sT 192.168.153.129 -oN tcp-connect.txt

### 📌 What it Does : 

This command runs a **TCP Connect Scan** on the target machine (`192.168.153.129`) to:

* Find **which TCP ports** are open.
* Discover **which services** are running on those ports.
* Save the results in a file named `tcp-connect.txt`.

The `-sT` option uses the full TCP three-way handshake, just like a real connection.



### 🖼️ TCP Scan Output Screenshot
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Nmap-Recon-Project/blob/main/screenshots/tcp-connect-scan.png" alt="Nmap Scan Output" width="100%">
</p>

# ⚠️ Vulnerabilities, Exploits, and Fixes (Simple & Beginner Friendly)

| Port | Service    | What’s the Risk (Simple Words)                      | How a Hacker Might Use It                | How to Fix (Mitigation)                     |
| ---- | ---------- | --------------------------------------------------- | ---------------------------------------- | ------------------------------------------- |
| 21   | FTP        | Can allow login without password (Anonymous access) | Try logging in as `ftp` with no password | Use SFTP or disable anonymous access        |
| 23   | Telnet     | Unencrypted login, very old and insecure            | Steal passwords using packet sniffers    | Replace with SSH, block port 23             |
| 80   | HTTP       | Websites can have bugs (like XSS)                   | Inject scripts or steal cookies          | Use HTTPS, validate inputs, patch web app   |
| 139  | NetBIOS    | Allows access to shared files/folders               | Connect using `smbclient` to steal files | Disable SMBv1, use firewall                 |
| 445  | SMB        | Same as above, more powerful file access            | Exploit old SMB bugs (like EternalBlue)  | Patch system, disable if not needed         |
| 3306 | MySQL      | Database may not need password                      | Use `mysql` to connect and steal data    | Use strong password, restrict remote access |
| 5432 | PostgreSQL | Same risk as MySQL                                  | Try brute-force login                    | Block unused ports, set password            |
| 5900 | VNC        | Desktop sharing without password                    | Hacker can control your desktop          | Set password, restrict access               |
| 2049 | NFS        | Shares folders over network without auth            | List files using `showmount`             | Limit access, use firewall                  |
| 6667 | IRC        | Chat server may be used to control bots             | Send commands to infected systems        | Disable if unused, monitor traffic          |
| 8009 | AJP13      | Backend Apache server may leak data                 | Perform Ghostcat attack to read files    | Update Tomcat, block AJP port if unused     |
| 8180 | Unknown    | Unidentified service – could be anything            | Scan deeper to find hidden apps          | Identify and secure the unknown service     |

---

### 🧾 Summary of the TCP Connect Scan

* ✅ **Host is up**, scanned successfully.
* ✅ **23 TCP ports** are open and running various services.
* ⚠️ Some **services may be vulnerable** if not secured.
* 🛠️ Simple misconfigurations (like no password, old services) can be fixed easily.
