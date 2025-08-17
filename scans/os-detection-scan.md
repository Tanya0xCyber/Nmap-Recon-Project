##  OS Detection Scan using Nmap (`-O` flag)

###  Command Used : 
    sudo nmap -O 192.168.153.129 -oN os-detection.txt

* `sudo`: Required to run OS detection
* `nmap`: The scanning tool
* `-O`: Enables OS detection
* `-oN os-detection.txt`: Saves the scan results in a readable text file

---

###  Screenshot of OS Detection Scan Output :

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Nmap-Recon-Project/blob/main/screenshots/os-detection-scan.png" alt="Nmap Scan Output" width="100%">
</p>

Key Output (Simplified)

```
OS: Linux 2.6.9 - 2.6.33
Device type: General purpose
MAC Vendor: VMware
Network Distance: 1 hop
```

This tells us:

* The system is **running a very old version of Linux**
* It's a **general-purpose machine** (not a printer, phone, or camera)
* It's running inside a **VMware virtual machine**

---

###  OS-Level Vulnerabilities :


| 🔎 Vulnerability Name           | 💬 Explanation (Non-Techie)                           | 🎯 What Hacker Can Do                    | 🛠️ Fix/Defense                                 |
| ------------------------------- | ----------------------------------------------------- | ---------------------------------------- | ----------------------------------------------- |
| **Outdated Linux Kernel**       | Very old OS version with many security holes          | Use public exploits to gain full control | Update to modern Linux version (e.g. Ubuntu 22) |
| **Dirty COW** (CVE-2016-5195)   | Bug in Linux lets users become root (admin)           | Become root from normal user             | Apply official patch / update kernel            |
| **Udev Bug** (CVE-2009-1185)    | System component can be tricked into running bad code | Get full access through race condition   | Patch udev or upgrade OS                        |
| **ASLR Not Available**          | OS memory layout is predictable                       | Makes hacking into memory easier         | Use a newer kernel with ASLR enabled            |
| **CVE-2009-2692**               | Local users can crash or hack the system              | Crash system or install backdoor         | Upgrade Linux kernel                            |
| **mmap/mremap Bug**             | Memory management bug                                 | Trick system into giving extra power     | Use safer memory functions in new versions      |
| **Kernel Hardening Missing**    | No AppArmor or SELinux protection                     | Easier to exploit vulnerabilities        | Enable security modules                         |
| **Virtualization Detected**     | MAC address shows it’s running in VMware              | May target VM-specific attacks           | Hide virtualization or limit VM access          |
| **No Automatic Updates**        | Old OS likely doesn’t auto-update                     | Misses critical patches                  | Use OS with active security support             |
| **Weak Default Configurations** | Old distros shipped with open ports or bad settings   | Find open doorways to break in           | Harden OS with secure configs                   |

---

###  Summary :

*  **OS Detected:** Linux 2.6.9 – 2.6.33
*  **Main Issue:** It’s **outdated and unsupported** with over 10 known vulnerabilities
*  **Risk Level:** High — even without service issues, attackers can exploit the **kernel itself**
*  **What to Do:**

  * Upgrade to a newer Linux distribution (like Ubuntu 22, Debian 11)
  * Apply all system patches
  * Enable protections like AppArmor or SELinux
  * Avoid exposing VMs directly to the internet
