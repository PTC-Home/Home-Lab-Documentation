# Home-Lab-Documentation
This is a documentation of the simulated SOC using Wazuh and pfSense to observe changes to victims like an Ubuntu server and Windows 11 pro from an attacker like Kali Linux

# Project Overview
This project demonstrates the design and deployment of a hardened enterprise network enclave. It features a dual-homed **pfSense** firewall acting as the perimeter gateway, protecting a "Crown Jewel" **Nextcloud** data server and a **Windows 11** enterprise workstation. The entire environment is monitored by a centralized **Wazuh (SIEM/XDR)** manager.

---

##  Tech Stack
| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Firewall/Gateway** | pfSense (FreeBSD) | Perimeter security, NAT/Internal routing, DHCP. |
| **SIEM/XDR** | Wazuh (Ubuntu 24.04) | Centralized log analysis, FIM, and Active Response. |
| **Cloud Target** | Nextcloud (Ubuntu) | Application-layer target (Private Cloud security). |
| **Workstation** | Windows 11 Pro | Enterprise endpoint (Sysmon & GPO monitoring). |
| **Attacker** | Kali Linux | Offensive testing (Hydra, Nmap, Metasploit). |

---

##  Network Blueprint
The lab utilizes an isolated **Internal Network** (SOC-LAN) to ensure all traffic is forced through the pfSense inspection point.

* **Internal Network (SOC-LAN):** `192.168.1.0/24`
* **External Network (WAN):** VirtualBox NAT (Gateway Only)

###  Static IP Registry
| Machine | IP Address | Role |
| :--- | :--- | :--- |
| **pfSense** | `192.168.1.1` | Default Gateway / DNS |
| **Wazuh Server** | `192.168.1.102` | Central Log Collector |
| **Nextcloud** | `192.168.1.10` | Linux Data Target |
| **Windows 11** | `192.168.1.101` | Enterprise Workstation |
| **Kali Linux** | `192.168.1.50` | Attacker / Management |

---

##  VirtualBox Hardware Specifications
| VM Name | vCPU | RAM | Storage | Adapter Type |
| :--- | :---: | :---: | :---: | :--- |
| **pfSense** | 2 | 2GB | 20GB | NAT & SOC-LAN |
| **Wazuh** | 2 | 8GB | 50GB | SOC-LAN |
| **Nextcloud** | 2 | 4GB | 40GB | SOC-LAN |
| **Windows 11** | 2 | 4GB | 64GB | SOC-LAN |
| **Kali Linux** | 2 | 2GB | 40GB | SOC-LAN (Promiscuous) |

---

##  Repository Structure
* `01-Network-Infrastructure/`: pfSense configuration screenshots and firewall rules.
* `02-SOC-Management/`: Wazuh installation logs and custom detection rules.
* `03-Target-Deployment/`: Hardening guides for Windows 11 and Nextcloud.
* `04-Attack-Simulation/`: Documentation of brute-force and vulnerability scans.
* `05-Defensive-Results/`: Evidence of automated blocks and incident alerts.

---

## pfSense Install
* **Installation:** Smooth Install with no issues
* **Lock-out resolved:** Password reset on Console's GUI 

---

##  Wazuh Install
* **Quick-Start:** `curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash wazuh-install.sh -a`, takes about 5-15 minutes
* **Admin-Password:** Issue with password after install fixed  

---

##  Troubleshooting
* **pfSense:** Resolved a GUI lockout by utilizing the console's password reset/service restart utility (Option 3/16).
* **Wazuh:** Manually invoked the wazuh-passwords-tool.sh utility via absolute pathing to force-update the admin cryptographic hash.



