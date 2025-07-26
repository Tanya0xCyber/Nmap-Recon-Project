# 🔐 System Hardening – Metasploitable

After scanning the Metasploitable machine, I found many insecure services that can be easily attacked. In this part of the project, I fixed those weak points to make the system more secure. This is called **system hardening**, and it’s important to reduce the chances of being hacked.

---

## 🛡️ What I Fixed and Why

| Vulnerable Service | Why it's dangerous | What I did to fix it |
|--------------------|--------------------|-----------------------|
| FTP (port 21)      | Allows anyone to connect without login (anonymous login) and sends files without encryption | Turned off FTP and used SFTP instead |
| Telnet (port 23)   | Sends usernames and passwords in plain text (anyone can sniff it) | Disabled Telnet and used SSH instead |
| Port 21 and 23     | Leaving open ports invites attackers | Blocked these ports using firewall (iptables) |
| Other old services like RSH, Rlogin | These are not secure and not used anymore | Stopped them from running |

---

### 🧰 How I Fixed Each One (Step-by-Step)

# 1. ❌ Disabled Telnet and ➕ Enabled SSH

**Telnet is risky** because hackers can read your username and password from network traffic.

**Fix:**
* Stop Telnet
sudo systemctl stop telnet        <br>
sudo systemctl disable telnet

* Start SSH (more secure)
sudo systemctl enable ssh       <br>
sudo systemctl start ssh


---

# 2. ❌ Turned off FTP and ✅ Used SFTP

**FTP is unsafe** because:

* Anyone can log in (anonymous access)
* It doesn't encrypt the data

**Fix:**

* Turn off FTP
sudo systemctl stop vsftpd   <br>
sudo systemctl disable vsftpd

** Make sure SFTP is working (SFTP comes with SSH)
*  Open SSH config
sudo nano /etc/ssh/sshd_config

** Check if this line is there (and not commented)
Subsystem sftp /usr/lib/openssh/sftp-server

*  Restart SSH to apply changes
sudo systemctl restart ssh

---

# 3. 🔒 Blocked Ports 21 and 23 (Firewall Setup)

Even after turning off FTP and Telnet, their ports (21, 23) were still open. I blocked them using `iptables`.

**Fix:**

*  Block FTP port
sudo iptables -A INPUT -p tcp --dport 21 -j DROP

* Block Telnet port
sudo iptables -A INPUT -p tcp --dport 23 -j DROP

*  Save the firewall settings
sudo iptables-save > /etc/iptables/rules.v4

---

# 4. 📴 Turned off Old/Unused Services

Some services like `rsh`, `rlogin`, etc. are outdated and should not be running.

**Fix:**

* These are not always installed, but I stopped them just in case
sudo systemctl stop rsh  <br>
sudo systemctl disable rsh


---

## ✅ Final Summary

* Replaced **Telnet** ➝ **SSH** (secure remote login)
* Replaced **FTP** ➝ **SFTP** (secure file transfer)
* Blocked unused and dangerous ports: **21, 23**
* Turned off old services that nobody uses anymore

These steps helped reduce risks and made the system safer from common attacks like **password sniffing**, **unauthorized access**, and **brute force attacks**. This was the **defensive phase** of the project.
