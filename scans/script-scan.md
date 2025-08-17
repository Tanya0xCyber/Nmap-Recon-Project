
#  Nmap Default Script Scan (`-sC`)

## Command Used : 

    sudo nmap -sC 192.168.153.129 -oN default-script-scan.txt


## What this command does :

This runs **Nmap's built-in default scripts** to detect:

* Dangerous misconfigurations
* Services leaking sensitive data
* Weak authentication or encryption settings
* Publicly available files or shares

These scripts go **beyond open ports** — they actively test how services behave and respond to common attacks.


###  Screenshot of the Output:

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Nmap-Recon-Project/blob/main/screenshots/script-scan.png" alt="Nmap Scan Output" width="100%">
</p>


### Vulnerabilities Found via Script Scan (New Table)

>  These are issues **only revealed** by script scan — not seen in basic, TCP, or version scans.

| Port    | Service    | Vulnerability / Misconfiguration    | How It Was Detected                                       | How It Can Be Exploited                                 | Fix Recommendation                               |
| ------- | ---------- | ----------------------------------- | --------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------ |
| 21      | FTP        | **Anonymous Login Allowed**         | `ftp-anon.nse` script confirmed login without credentials | Attacker can browse/download/upload files freely        | Disable anonymous login in `vsftpd.conf`         |
| 23      | Telnet     | **Banner reveals system info**      | `banner.nse` script exposed OS and hostname               | Helps attackers fingerprint system for targeted attacks | Disable Telnet, use SSH                          |
| 25      | SMTP       | **SSLv2 supported**                 | `ssl-enum-ciphers.nse` detected insecure SSL version      | SSLv2 is broken and vulnerable to decryption            | Disable SSLv2; use TLS 1.2/1.3 only              |
| 25      | SMTP       | **Expired Self-Signed Certificate** | `ssl-cert.nse` showed expired cert details                | MITM attack is easier with fake certs                   | Use valid, CA-signed certificates                |
| 111     | RPCBind    | **Enumerates RPC services**         | `rpcinfo.nse` exposed list of RPC programs                | Helps attacker target vulnerable services               | Restrict access or disable unnecessary RPC       |
| 139/445 | SMB        | **SMB Shares Leaking Data**         | `smb-enum-shares.nse` listed shared folders               | May expose sensitive files without authentication       | Restrict shares and require authentication       |
| 139/445 | SMB        | **Guest Login Allowed**             | `smb-enum-users.nse` allowed guest sessions               | Unauthorized access to network shares                   | Disable guest login in SMB settings              |
| 2049    | NFS        | **Open NFS Exports**                | `nfs-showmount.nse` exposed mountable paths               | Attacker can mount and steal server data                | Restrict NFS exports and require IP-based access |
| 512–514 | R Services | **No Authentication Needed**        | `r-services.nse` confirmed remote command access          | Attacker can run shell commands remotely                | Remove r-services from the system                |



### Summary :

*  Host is up and responded to default scripts.<br>
* Detected useful info like software versions, anonymous access, and weak configs.<br>
* Some default services are misconfigured or leaking sensitive information.<br>
* Services like FTP, NFS, SMB, and RServices are exposing data or accepting insecure logins.<br>
* These issues can be fixed by disabling anonymous access, updating services, and tightening permissions.<br>

